---
layout: post
title:  "Slack api로 사내 휴가관리 슬랙봇을 만들었던 여정(2) - 휴가 등록 기능"
tags: Project
---


## Interactive Components에 개발용 서버 등록하기 

앞서 다루었던 Slash Commands에 Request URL을 등록한 것과 마찬가지로 Interactive Components에도 개발용 서버와 엔드포인트를 Request URL에 등록한다. 

<img width="1158" alt="스크린샷 2021-04-03 오후 6 27 58" src="https://user-images.githubusercontent.com/60246689/113474336-5cf76380-94aa-11eb-8ac7-627158ec5f38.png">


## interactive Components 라우터 만들기 

이제 슬래시 커맨드로 활성화된 메세지에서 `새로운 휴가 등록하기`, `휴가 조회하기` 버튼을 클릭하면 그에 해당하는 모달창을 띄워야 한다. 

인터랙티브 컴포넌트에 등록 가능한 request URL은 한 개인데, 버튼과 모달창이 둘 다 인터랙티브 컴포넌트에 해당한다. 그래서 
크게 두가지 컴포넌트 유형에 대해 등록인지 조회인지 구분하여 코드를 작성해야한다.

요청이 1) 버튼일 경우 --> 휴가 등록이면 registerModal 활성화  / 휴가 조회면 retrieveDeleteModal 활성화
2) 모달일 경우 ---> 휴가 등록이면 registerModal에 대한 액션 정의 / 휴가 조회면 retrieveDeleteModal에 대한 액션 정의 

req.body를 콘솔에 찍어보면 payload 안에 내가 필요한 정보들이 있는 걸 알게된다. 여기 안에 있는 정보들을 가지고 코드를 쓰면 된다.


```javascript
const interactions = async (req, res) => {
  const payload = JSON.parse(req.body.payload);
  const { trigger_id, actions, view, user } = payload;
  const userId = user.id;

  res.status(200).send();

   if (actions && actions[0].type === 'button') {
    //action type이 버튼이면 휴가등록 모달 또는 휴가조회삭제 모달 활성화
    ....    
  } else if (view.type === 'modal') {
    //view type이 모달이면 모달에서 정의하고 싶은 액션 정의   
   }

```

