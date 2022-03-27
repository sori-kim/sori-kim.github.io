---
layout: post
title:  "Github Packages를 이용하여 npm에 라이브러리 배포하기"
tags: Project
---

## 시작하기 전에
지난 포스팅에 어쩌다보니 회사에서 사용하는 UI 컴포넌트 라이브러리를 개발하게 된 이야기를 했다. 
드디어 얼마전에 npm에 private 라이브러리로 배포를 하게 되었고 오늘은 이 내용을 정리하려고 한다.  
사실 처음 환경 설정할때는 대강 만들어서 빌드해보고 휘리릭 넘어가버렸는데 실제로 배포 단계에 오니 좀 더 신경써서 
요모조모 확인해보고 그동안 미처 신경쓰지 않았던 `package.json` 작성도 굉장히 중요한 것이었음을 새삼 알게 되었다...^^ 


## Github Packages ?
`github packages`는 소프트웨어 패키지를 비공개 또는 공개적으로 호스팅할 수 있는 소프트웨어 패키지 호스팅 서비스다.  
패키지 배포는 `npm`을 이용해서도 배포할 수 있지만 private 배포를 위해서는 비용을 지불해야하는 단점이 있다.  
그래서 이번 ui 컴포넌트 라이브러리를 배포할 때는 고민 없이 Github packages를 사용하게 되었다.

## 시작하기 전에 필요한 것
당연히 github 계정이 있어야하고, `personal access token`을 준비해야한다.
토큰은 **GitHub -> 사용자 -> Settings -> Developer Settings -> Personal Access Token** 에서 발급할 수 있다.

`generate new token`을 클릭하고 scope에서 `write:pacakages` 와 `delete:packages`를 필수로 선택한다. 

<img width="1188" alt="스크린샷 2022-03-27 오후 6 37 55" src="https://user-images.githubusercontent.com/60246689/160275686-3499e0f8-6bf5-4901-ad4c-ea8ff0dab28c.png">

이제 프로젝트의 루트에 .npmrc 파일을 생성하고 아래 정보를 추가한다.
```
//npm.pkg.github.com/:_authToken={TOKEN}
@username:registry=https://npm.pkg.github.com/
```

package.json 파일에서 `@sori-kim/design-system-practice` 같이 앞에 `@sori-kim`이 붙는 패키지에 대해서는 공식 npm 저장소 http://registry.npmjs.org/ 대신 GitHub Package Registry https://npm.pkg.github.com/에서 찾아서 다운로드하겠다는 의미이다.

## 패키지 배포하기 
### 1. package.json 수정하기

- `name`은 `@username(조직명)/package` 의 형태로 작성해준다.  
- `description`, `repository`, `bugs`, `author`, `license`를 작성한다.
- `publishConfig`를 작성한다.
  - `https://nmp.pkg.github.com` 
  - 이 패키지는 npm저장소가 아니라 GitHub Package Regsitry에 배포한다는 의미

```json
{
  "name": "@sori-kim/design-system-practice",
  "version": "1.0.0",
  "description": "UI Component Library Practice",

  "repository": {
    "type": "git",
    "url": "https://github.com/sori-kim/design-system-practice.git"
  },
  "publishConfig": {
    "registry": "https://npm.pkg.github.com/"
  },
  "bugs": {
    "url": "https://github.com/sori-kim/design-system-practice.git",
    "email": "soriosie@gmail.com"
  },
  "author": "Sori Kim",
  "license": "ISC"
}

```

- main, files 필드를 채워준다.
  - main: 진입점 파일 (.js)
  - files: 패키지에 포함될 파일 (개발시에만 사용되는 파일이나 소스코드를 제외할 수 있음.)
```json
{
  "main": "build/index.js",
  "files": [
    "build"
  ]
}
```

### 2. npm 명령어로 배포하기
마지막으로 버전 명을 확인하고 다음 명령어로 배포를 실행한다.
참고로, 한번 배포한 버전으로는 다시 배포 할 수 없기 때문에 신중하게 배포를 해야한다.
```shell
npm publish
```

### 3. 배포한 라이브러리 설치하기
배포가 잘 되었는지, 라이브러리가 잘 작동하는지 확인하기 위해 설치해보자.
설치할때에는 .npmrc에서 설정했던 변수명에 내 `personal access token`을 입력해서 설치해야한다.

```shell
 TOKEN={personal_access_token} npm i @sori-kim/design-system-practice@1.0.0
```

설치 후 `node_modules`안에 내 패키지를 확인해보면 `build`와 `package.json`만 있는 형태로 잘 들어가 있는 것을 확인할 수 있다.

<img width="231" alt="스크린샷 2022-03-27 오후 7 08 38" src="https://user-images.githubusercontent.com/60246689/160276604-15acf106-1820-4d5f-8dda-98a5e2ff069b.png">
