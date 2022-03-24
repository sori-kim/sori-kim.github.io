---
layout: post
title:  "Rollup + TypeScript + Storybook으로 UI 컴포넌트 라이브러리 개발하기"
tags: Project
---

## UI 컴포넌트 라이브러리를 개발하게 된 배경 
이번에 입사한 회사에서 기존의 개발자분이 개발한 코드를 기반으로 회사 서비스의 메인 페이지를 리뉴얼 하는 프로젝트를 맡아서 하게 되었다.
기존에 있던 컴포넌트들이 문서화되어 있지 않았기 때문에 이를 한 눈에 파악하기도 어려웠고 결과적으로 효율적이지 못한 개발을 할 수 밖에 없었다. 
그래서 그동안 꼭 써보고싶었던 Storybook을 써봐야겠다 생각하고 팀에 이야기를 했는데 어쩌다보니 일이 커져서 별도의 사내 UI 컴포넌트 라이브러리를 만들게 되었다...^^;;   
개발 환경은 `Rollup` + `Storybook` + `Typescript`를 사용했했는데, 나름 처음 써보는 게 많았고 삽질도 많았던 만큼 이번에 배운 내용을 정리 해두려고 오랜만에 포스팅을 한다.


## Rollup
rollup은 webpack처럼 여러 모듈이나 파일을 작게 만들어주는 번들러이다. 
라이브러리와 같은 프로젝트를 번들링 할 때에는 webpack보다 rollup을 더 일반적으로 사용하는데, rollup과 webpack을 비교해서 간단하게 짚어보고 넘어가자면 

### Webpack의 문제점 
- ESM(ES Module)형태의 번들이 불가능하다. (CommonJS 형태)
- 빌드할 때 중복 코드가 제거되지 않는다.
- 빌드할 때 기본 용량이 크다.
- webpack3에서 tree shaking이 잘 이루어지지 않는다.

### Rollup은 Webpack의 문제를 보완할 수 있다
1. ESM 형태로 번들이 가능하다.
    - Tree shaking의 조건은 코드가 ESM 형태여야 하지만 webpack은 ESM 형태로 번들할 수 없기 때문에 각각의 파일로 변환해야한다. (즉, 하나의 es 모듈로 변환 불가)
    - **반면 rollup은 여러 모듈(파일)을 한 모듈로 합치면서 ESM 형태로 번들이 가능하다.**
    - 개별 파일로 배포하는 것보다 파일 하나로 통합하여 배포하는 것이 관리 및 편의성 면에서도 더 좋음

2. 모듈간의 import / export 과정이 사라지기 때문에 중복되는 코드가 제거된다.
    - webpack은 `import` 는 `__webpack_require__`로 바뀌고 `export`는 `exports 오브젝트`로 바뀌면서 코드가 증가한다. 또한 상수를 사용하면 상수 이름을 그대로 사용하고 uglify가 되지 않기 때문에 코드가 증가할 수 있음.
    - 하지만 rollup은 여러개의 모듈을 하나의 scope로 합쳐진 단일 모듈로 만든다. 그리고 상수이름도 uglify 되기 때문에 코드가 감소함
    - 또한 바벨 플러그인을 이용하여 assign, extends 같은 ES6 이상의 문법을 ES5로 바꾸면서 생기는 polyfill 같은 경우에는 이 함수가 파일의 개수만큼 증가한다.
    - rollup은 하나의 모듈로 합치고 동일한 polyfill은 하나만 존재한다.
3. 빌드하여 생성된 코드가 webpack에 비해 1.2kb 가량 작다.
4. webpack에서 tree shaking이 잘 되지 않는 경우 (import한 모듈을 사용한 함수를 사용하지 않는 경우)를 해결할 수 있다. (여러 모듈을 한 파일로 합치기 때문에 )
5. webpack과 다르게 코드들을 동일한 수준으로 호이스팅 한 후 한 번에 번들링을 진행하기 때문에 속도에서는 webpack보다 빠르다.

__ES 모듈의 라이브러리를 만들고 있는 경우 =>  `Rollup`  
code spliting이 필요하거나 static asset이 많은 경우, 안정성을 추구해야되는 경우 혹은 CommonJS 종속성이 많은 경우 => `webpack`__


## Storybook
스토리북은 UI Component를 테스팅하는데에 유용한 도구이다. 내가 개발한 컴포넌트의 스토리를 작성하여 상태별로 다른 컴포넌트를 시각화 할 수 있다.  
또 스토리북에서 제공하는 유용한 플러그인들이 많기 때문에 이를 활용하여 비개발자도 개발 지식 없이 컴포넌트를 컨트롤할 수 있는 형태를 제공할 수도 있다.  
Redux action도 관리할 수 있고 또 server를 mocking하여 독립된 테스트 환경도 구축할 수 있어서 잘만 활용하면 정말 좋은 도구라고 생각한다.


## 프로젝트 환경 설정하기

### 1. 기본 프로젝트 폴더 구조 설정하기 

먼저 프로젝트를 구성하는 기본적인 라이브러리들을 설치해준다. 
```shell
npm init
yarn add -D react react-dom @types/react styled-components @types/styled-components 
```

그리고 react, react-dom, styled-components는 추후에 다른 프로젝트에서 내 컴포넌트가 사용될 때 필요한 것이기 때문에 peer dependency에 넣어준다.

```json
{
  "peerDependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2",
    "styled-components": "^5.3.3"
  }
}
```

기본적인 폴더 구조를 다음과 같이 만들어준다.
```
src 
 ㄴ components
      ㄴ Button
           ㄴ index.tsx
           ㄴ Button.stories.tsx
 ㄴ types
      ㄴ typing.ts
 ㄴ index.ts
 package.json
 tsconfig.json
 rollup.config.json
 babelrc.json
 .gitignore 
 
```
components 폴더 안에 index.tsx에 내 컴포넌트를 정의하고 src 안에 있는 index.ts에서 export 하는 형태를 취한다.

```typescript
// index.ts
export { default as Button } from "components/Button";
```
### 2. 타입스크립트 설치 & tsconfig 설정하기  
타입스크립트를 설치해준다.
```shell
yarn add -D typescript
```

tsconfig.json 파일을 생성하여 config를 설정해준다. 나는 다음과 같이 작성해주었다.
```json
{
  "compilerOptions": {
    "declaration": true,
    "declarationDir": "./build",
    "baseUrl": "./",
    "paths": {
      "asset/*": [ "src/asset/*" ],
      "components/*": [ "src/components/*" ],
      "features/*": [ "src/features/*" ],
      "lib/*": [ "src/lib/*" ],
      "types/*": [ "src/types/*" ]
    },
    "target": "es5",
    "lib": ["dom", "dom.iterable", "esnext"],
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "jsx": "react",
    "typeRoots": [
      "types"
    ],
    "plugins": [{"name" : "typescript-plugin-css-modules" }]
  },
  "include": [
    "**/*",
    "types/typings.d.ts"
  ],
  "exclude": ["node_modules", "build", "**/*.stories.tsx"]
}
```

- `"declaration": true`와 `"declartionDir": "./build"`를 통해 빌드할 때 컴포넌트에서 사용된 타입들을 자동으로 생성해 빌드 폴더에 넣어주는 역할을 한다.
- `baseUrl`: 프로젝트의 시작점
- `paths`: import 경로를 절대경로로 커스텀 변경한다
- `exclude`: 여기에 해당되는 파일 및 폴더는 빌드 할 때 타입들을 생성하지 않는다.

types 폴더 안에 `typings.d.ts` 파일을 생성해주고 타입 정의가 필요한 확장자 등을 정의해준다. 나는 svg파일과 jpg, png 파일을 위한 타입 정의를 추가 했다.
```typescript
declare module "*.svg" {
  import * as React from "react";

  export const ReactComponent: React.FunctionComponent<
    React.SVGProps<SVGSVGElement>
  >;

  const src: string;
  export default src;
}

declare module "*.jpg";
declare module "*.png";
```

### 3. Rollup 설치 & rollup.config.js 설정하기 
이제 이번 환결설정의 메인(?)이라고 할 수 있는 부분. rollup과 관련 라이브러리들을 설치해준다.
```shell
yarn add -D rollup rollup-plugin-typescript2 rollup-plugin-postcss @rollup/plugin-commonjs @rollup/plugin-node-resolve rollup-plugin-peer-deps-external @rollup/plugin-image @svgr/rollup @rollup/plugin-alias @rollup/plugin-url
```

rollup.config.js 파일을 생성하고 설정 내용을 추가해준다.
```js
import resolve from "@rollup/plugin-node-resolve";
import typescript from "rollup-plugin-typescript2";
import peerDepsExternal from "rollup-plugin-peer-deps-external";
import commonjs from "@rollup/plugin-commonjs";
import postcss from "rollup-plugin-postcss";
import alias from "@rollup/plugin-alias";
import image from "@rollup/plugin-image";
import svgr from "@svgr/rollup";
import url from "@rollup/plugin-url";
import pkg from "./package.json";

const external = [
  ...Object.keys(pkg.devDependencies),
  ...Object.keys(pkg.peerDependencies),
];
const extensions = [".js", ".jsx", ".ts", ".tsx"];

const aliasPlugin = alias({
  entries: [
    { find: "asset/*", replacement: "./asset/*" },
    { find: "components/*", replacement: "./components/*" },
    { find: "features/*", replacement: "./features/*" },
    { find: "lib/*", replacement: "./lib/*" },
    { find: "types/*", replacement: "./types/*" },
  ],
});

export default {
  input: "./src/index.ts",
  output: [
    {
      dir: "build",
      format: "esm",
      exports: "named",
      sourcemap: true,
    },
  ],
  preserveModules: false,
  plugins: [
    peerDepsExternal(),
    resolve({ extensions }),
    commonjs({
      include: /node_modules/,
    }),
    aliasPlugin,
    typescript({
      useTsconfigDeclarationDir: true,
      tsconfig: "./tsconfig.json",
    }),
    postcss({
      extract: false,
      modules: true,
    }),
    image(),
    svgr(),
    url(),
  ],
  external,
};

```
- input: entry 파일 (빌드 시작점) 
- output: 
  - dir: build 결과물 폴더
  - format: esm 또는 cjs
  - exports: Name for UMD export 
  - sourcemap: sorcemap generate 여부 
- preserveModules: 빌드된 결과물이 기존 폴더 구조를 유지하도록 할지 여부
- external: 외부 라이브러리 정의 
- plugins: 
  - rollup-plugin-peer-deps-external
    - peerDependency로 설치된 라이브러리의 코드가 번들링된 결과에 포함되지 않고, import 구문으로 불러와서 사용할 수 있게 만들어주는 플러그인
  - @rollup/plugin-node-resolve
    - node_modules에서 third party 모듈을 사용하는 용도, js 이외의 확장자 (ts, tsx) 파일을 불러오기 위해서도 이 플러그인을 필요로 함
  - @rollup/plugin-commonjs
    - 외부 노드 모듈이 es6 으로 변환되지 않았을 경우 es6 으로 변환하는 플러그인
  - @rollup/plugin-alias
    - 절대 경로로 지정한 alias를 찾아서 빌드 할 때 다시 변환 해주는 플러그인 
  - rollup-plugin-postcss
    - scss,css 관련 플러그인
  - rollup-plugin-typescript2
    - typescript 관련 플러그인


package.json의 main을 빌드한 결과물을 바라보도록 수정해주고, 빌드 관련 script를 추가한다.
```json
{
  "main": "./build/index.js",
  "scripts": {
    "build": "rollup -c"
  }
}
```

