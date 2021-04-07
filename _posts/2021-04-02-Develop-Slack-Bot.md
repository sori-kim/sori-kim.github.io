---
layout: post
title:  "Slack api로 사내 휴가관리 슬랙봇을 만들었던 여정(1) - 슬래시 커맨드"
tags: Project
---

## 슬랙 봇을 만들게 된 배경 🤖

 지금 소속된 팀에서는 슬랙 api를 활용하여 데일리 스크럼 리마인더나 코로나 확진자 현황을 알려주는 등 다양한 방법으로 슬랙을 활용하고 있다. 
항상 슬랙봇을 어떻게 만드는지 궁금하기도 했고 마침 팀에 휴가를 관리하는 툴이 필요했던 상황이었어서 휴가관리 슬랙 봇 (이하 `휴가봇`)을 만들어보게 되었다.

 사실 벌써 휴가봇을 만든지도 시간이 꽤 흘렀지만 최근에 휴가봇을 유지보수할 일이 생겨서 오랜만에 코드를 들여다봤는데 내 코드지만 마치 남의 코드를 보는 것 마냥 새로운게 아닌가... (눈물) 
 마침 블로그를 새로 만들어 열정 만수르인 지금이 기회다 싶어 묵혀놨던 주제인 휴가봇 만들기를 정리해보려고 한다.

## 전체적인 플로우

<img width="705" alt="스크린샷 2021-04-03 오후 4 49 07" src="https://user-images.githubusercontent.com/60246689/113472219-a50f8980-949c-11eb-9282-2405b110cd76.png">

먼저 Slack api의 **Slash Command**라는 기능으로 `/휴가`라고 입력하면 휴가봇이 활성화 된다. 
휴가봇이 가진 기능은 크게 1. 새로운 휴가 등록 2. 휴가 조회 및 삭제 두 가지로 구분 된다. 

새로운 휴가 등록 버튼을 누르면 (Slack api의 **interactive components**) 휴가등록 모달창이 활성화된다. 
원하는 휴가 기간 및 시간을 선택 후 등록 버튼을 누르면 입력된 값을 타당성 검증 후 타당한 경우 DB에 저장되고 채널에 새로운 휴가가 등록되었다는 메세지가 전송된다.
타당성 검증에 통과하지 못하면 타당하지 않은 원인과 함께 휴가를 등록할 수 없다는 메세지를 리턴받는다.

휴가 조회를 누르면 유저가 등록한 모든 휴가 목록을 볼 수 있다. 
삭제를 원하는 경우 휴가를 선택하여 삭제 버튼을 클릭하면 DB에서 상태가 업데이트 되고 해당 휴가가 취소되었다는 메세지가 채널에 전송된다.

그리고 aws lambda가 매일 오전 10시에 그 날 휴가자가 있는 지 DB를 조회하여 휴가자가 있는 경우 채널에 안내 메세지를 전송한다. 휴가자가 없으면 그대로 종료된다.


사용한 기술스택은 다음과 같다.

Express.js, AWS RDS(mysql), AWS Lambda, AWS Event Bridge, AWS EC2, PM2 이다. 


<br />

## 개발용 서버 등록하기
Slack api에서 제공하는 기능들을 사용하기 위해서는 My Apps의 Basic Information에서 원하는 기능을 선택하고 해당 기능에 Request URL을 등록 해야한다.
먼저 Slash Commands를 등록하자.

<img width="1208" alt="스크린샷 2021-04-03 오후 5 19 13" src="https://user-images.githubusercontent.com/60246689/113472861-c2deed80-94a0-11eb-998d-e2d2e9ec4ce5.png">

Request URL에 등록된 주소는 말하자면 Slack api에서 해당 주소로 요청이 오면 Slash Command 기능을 활성화 시켜주는 것이다.

그런데 내가 만든 서버를 배포를 해서 도메인을 등록하기 전까지는 개발용 localhost 서버를 이용해야 하는데, 
이를 위해 ngrok라는 프로그램을 이용한다. ngrok는 localhost 서버에 주소를 부여해주는 프로그램인데, ngrok의 간단한 사용 방법은 [공식 홈페이지](https://dashboard.ngrok.com/get-started/setup)에서 안내되어 있다. 

회원가입 후 받은 authToken으로 인증을 하고 내가 개발하려는 포트 번호 입력하면 된다.
그러면 http://fb58ab29435b.ngrok.io 와 같은 주소가 터미널에 나오는데 이 주소를 slack api의 Request URL에 내가 원하는 엔드포인트(e.g. /slash/leave)와 함께 입력하면 된다. 

<img width="1075" alt="스크린샷 2021-04-03 오후 5 46 08" src="https://user-images.githubusercontent.com/60246689/113473446-7b5a6080-94a4-11eb-85ae-7ca4c6ac920f.png">

새로운 기능을 추가할 때마다 ReInstall to Workspace 버튼을 클릭하여 적용시켜주어야 한다. 


## Express로 서버의 라우터 등록 

이제 본격적으로 서버 작업을 하는데, 먼저 app.js에 라우터를 등록한다.

```javascript
const slashRouter = require('./routes/index');

const express = require('express');
const bodyParser = require('body-parser');

const app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use('/slash', slashRouter);

const port = process.env.PORT;
app.listen(port, () =>
  console.log(`app listening at http://localhost:${port}`)
);

module.exports = app;
```

```javascript
// routes/index.js
const express = require('express');
const slashCommand = require('./slashCommand');
const interactions = require('./interactions');

const router = express.Router();

router.post('/leave', slashCommand);
router.post('/interactions', interactions);

module.exports = router;

```

## Slash Commands 라우터 만들기 
다음으로는 슬래시 커맨드 요청이 일어났을때 받아주는 라우터 작업을 한다.
나는 slack에서 제공하는 `@slack/web-api` 라는 라이브러리를 이용해서 슬래시 커맨드 요청이 일어나면 슬랙에 메세지를 보내는 기능을 만들 것이다.
slack 공식 홈페이지의 [interactive messages](https://api.slack.com/messaging/interactivity#components)를 참고하면서 구성했다.

```sh
$ npm install @slack/web-api 
```

`@slack/web-api`에서 webClient를 이용해서 botToken을 입력하여 인증을 하고, 원하는 체널의 id와 함께 blocks에 메세지 내용을 입력하면 해당 채널에 메세지를 보낼 수 있다.  
botToken은 xoxb로 시작하는 토큰으로, slack api의 [OAuth & Permissons](https://api.slack.com/apps/A01142VT6E4/oauth?)에서 확인할 수 있다. 
토큰은 쉽게 노출되지 않도록 환경변수 파일 안에 보관 하는 걸 권장한다.

```javascript
// postIntroMessage.js
const { WebClient } = require('@slack/web-api');
require('dotenv').config();

const postIntroMessage = async (channel_id) => {
  const botToken = process.env.OAUTH_BOT_TOKEN;
  const webClient = new WebClient(botToken);

  await webClient.chat.postMessage({
    channel: channel_id,
    blocks: [
      {
        type: 'actions',
        elements: [
          {
            type: 'button',
            text: {
              type: 'plain_text',
              emoji: true,
              text: '새로운 휴가등록하기',
            },
            style: 'primary',
            value: 'register',
          },
          {
            type: 'button',
            text: {
              type: 'plain_text',
              emoji: true,
              text: '휴가 조회/삭제하기',
            },
            style: 'danger',
            value: 'delete',
          },
        ],
      },
    ],
  });
};

module.exports = postIntroMessage;
```

```javascript
const postIntroMessage = require('../lib/api/message/postIntroMessage');

const slashCommand = async (req, res) => {
  const { user_id } = req.body;

  await postIntroMessage(user_id);
  await res.status(200).send('');
};

module.exports = slashCommand;
```


이제 슬랙에서 내가 설정한 슬래시커맨드 키워드를 입력하면 메세지가 전송되는 걸 확인할 수 있다.

<img width="403" alt="스크린샷 2020-12-21 오후 7 13 36" src="https://user-images.githubusercontent.com/60246689/113474101-af378500-94a8-11eb-9555-b57ea42f5b3a.png">

<img width="583" alt="스크린샷 2020-12-21 오후 7 12 44" src="https://user-images.githubusercontent.com/60246689/113474097-a8a90d80-94a8-11eb-8986-39b5bec350c3.png">



다음 포스팅에서는 Interactive Components를 이용하여 새로운 휴가를 등록하는 기능을 만들겠다.


 