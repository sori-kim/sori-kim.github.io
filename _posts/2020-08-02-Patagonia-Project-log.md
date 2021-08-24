---
layout: post
title: 'Wecode 2차 프로젝트 Patagonia 웹사이트 개발 회고'
tags: 'Review'
---

## 한달 만에 지난 프로젝트를 회고하는 이유

이제는 말할 수 있을 것 같다.  
프로젝트가 끝난 후 무엇보다 중요한 건 내 코드를 다시 뜯어보며 새로 배운 것과 보완할 점에 대해 정리하는 것이라는 걸 잘 알고 있다.

하지만 그때 당시에는 내 코드를 외면하고 싶었다.  
욕심 많은 내가 욕심보다 훨씬 부족한 결과물을 가지고 프로젝트를 종료하게 되었다는 것을 스스로 인정하고 싶지 않았던 것 같다.

하지만 내가 외면한다고 해서 내 코드가 사라지는 것도 아니고, 어쨌든 내가 뜨겁게 시간과 노력을 쏟아부었던 소중한 결과물임에는 변함 없다.

그래서 최근에 부트캠프를 수료하고나서야 조금씩 프로젝트 코드를 열어서 다시 보면서
또 새로 보완도 하기 시작했고, 그제서야 리뷰를 적어두고 싶다는 마음이 들어서 이렇게 회고를 적게 되었다.

## 1. 진행한 프로젝트 소개

2차 프로젝트는 아웃도어 스포츠 브랜드 '파타고니아(Patagonia)' 북미 사이트를 개발하는 프로젝트였다. 프론트 2명, 백앤드 2명이 팀이 되어 2주동안 개발을 진행했고, 1차 프로젝트와 마찬가지로 애자일 기반의 스크럼 방식으로 프로젝트를 진행하여 총 2회 스프린트, 데일리 스탠드업 미팅을 진행하며 프로젝트를 운영했다. 또한 Git flow를 따라 협업을 진행했고 git rebase를 사용하여 프론트 간 코드를 병합했다.

## 2. 기술 스택

- Front-End : HTML, CSS, JavaScript, React.js (Hooks), Styled-component
- Back-End : Python, Django, MYSQL
- 배포 : AWS

## 3. 프로젝트의 목표

**전체적인 목표**

- React hooks와 Styled-Component를 사용하여 프론트 개발 익히기
- 스스로 공식 문서를 보고 새로운 기술, 라이브러리 적용하는것에 익숙해지기
- trello 협업 툴을 활용과 Git Rebase, Agile 개발 시스템 적용

**기능구현에 대한 목표**

- 파타고니아 미국 본사 사이트의 메인, 카테고리 메인, 상품 상세 페이지, 장바구니(카트) 인터페이스 구현하기
- 카테고리 내 색상별 필터 기능 구현하기
- Back-End API를 통해 데이터 통신하기
- 외부 API를 활용한 소셜 로그인 구현하기 (kakao)
- 마이페이지 및 개인정보 수정하기 기능 구현
- Redux를 활용하여 전역상태관리 (카트 구현하기)

## 4. 내가 맡은 역할

### 1. 메인 랜딩페이지 구현

- Header와 Footer를 제외한 메인랜딩페이지 구현
- 순수 자바스크립트로 Careousel Slider 구현
- React Slick.js를 활용한 Scroll event 구현

  <img width="1440" alt="스크린샷 2020-08-02 오후 4 36 12" src="https://user-images.githubusercontent.com/60246689/89137262-7a1e1000-d572-11ea-81c6-d67607e0c28a.png">

  <img width="1440" alt="스크린샷 2020-08-03 오전 10 21 01" src="https://user-images.githubusercontent.com/60246689/89137438-0d574580-d573-11ea-9d30-a3deb02dd1ee.png">

  <img width="1440" alt="스크린샷 2020-08-03 오전 10 27 09" src="https://user-images.githubusercontent.com/60246689/89137692-e9483400-d573-11ea-8ae9-0ff3049dcc2d.png">

### 2. 로그인 페이지 구현

- 다음 kakao api를 활용한 소셜로그인 구현

<img width="1440" alt="스크린샷 2020-08-03 오전 10 29 15" src="https://user-images.githubusercontent.com/60246689/89137779-3cba8200-d574-11ea-8d43-fe0334d38c35.png">

### 3. 상품 상세페이지 구현

- url-parameter를 활용한 라우팅 구현 및 카테고리 페이지와 데이터 연동
- JavaScript filter 메서드를 활용하여 데이터 필터링처리
  (상품 컬러 옵션 클릭 시 해당 컬러의 사진 필터 후 화면에 렌더링)

  <img width="1440" alt="스크린샷 2020-08-03 오전 10 34 32" src="https://user-images.githubusercontent.com/60246689/89137979-eef24980-d574-11ea-87d4-3fceb04afbf3.png">

  <img width="1440" alt="스크린샷 2020-08-03 오전 10 33 00" src="https://user-images.githubusercontent.com/60246689/89137983-f1ed3a00-d574-11ea-846f-e42f86622e38.png">
  <img width="1440" alt="스크린샷 2020-08-03 오전 10 33 13" src="https://user-images.githubusercontent.com/60246689/89138002-016c8300-d575-11ea-9639-aa73a6f0fad9.png">

### 4. 마이페이지 구현 (20' 8' 추가)

- 회원정보 조회 및 수정 기능 구현
- 커스텀 hooks를 통한 input 상태값 관리
- 백앤드 API 호출 및 데이터 통신 (GET, PATCH)

<img width="1440" alt="스크린샷 2020-08-01 오후 4 17 39" src="https://user-images.githubusercontent.com/60246689/89138391-696f9900-d576-11ea-9839-7a1891174ab7.png">
<img width="1440" alt="스크린샷 2020-08-03 오전 10 45 36" src="https://user-images.githubusercontent.com/60246689/89138413-7b513c00-d576-11ea-832c-ebb52d9c2c5d.png">

<br />
<br />
<br />
<br />

## 5. 기록하고 싶은 코드

### 1) 순수 자바스크립트로 slider 구현

```jsx
const SlideCarousel = props => {
  const data = props.data
  const [slideImages, setSlideImages] = useState([])
  const [currentSlide, setCurrentSlide] = useState(0)
  const [positionX, setPositionX] = useState(-200)

  useEffect(() => {
    if (data !== undefined) {
      setSlideImages(data.images)
    }
  })

  const nextSlide = () => {
    let TOTAL_SLIDES = slideImages.length
    if (currentSlide >= TOTAL_SLIDES - 2) {
      return
    } else {
      setCurrentSlide(currentSlide + 1)
      setPositionX(positionX - 450)
    }
  }

  const prevSlide = () => {
    if (currentSlide === 0) {
      return
    } else {
      setCurrentSlide(currentSlide - 1)
      setPositionX(positionX + 450)
    }
  }
}
```

변수 slideImages 실질적으로 슬라이더를 구현하고 싶은 이미지 데이터들이다.  
useEffect hook을 통해 컴포넌트가 마운트 되었을때 setSlideImages()로 데이터를 할당했다.
변수 currentSlide는 0으로 초기값을 설정하고 클릭했을때마다 값을 증감시키는 용으로 사용했다.
변수 positionX는 슬라이더가 움직이는 X축의 값을 설정하는 용으로 사용했다.

그리고 nextSlide()와 prevSlide() 함수를 만들어서 좌, 우 화살표 클릭에 대한 이벤트핸들러로 사용했다.
nextSlide()부터 살펴보면, totalSlide라는 변수를 만들어서 전체 이미지데이터의 길이를 값으로 할당했다.
그리고 currentSlide값이 totalSlide값보다 크거나 같으면 그대로 return 하면서 슬라이더가 멈추고
currentSlide가 total보다 작으면 currentSlide에 1씩 추가하면서 positionX의 값도 내가 이동하고싶은만큼 추가했다.

반대로 prevSlide에서는 currentSlide가 0이 되었을때만 멈추면 되기 때문에 totalSlide와 비교할 필요 없이
좀 더 간단하게 구현했다.



### 2) kakao api로 소셜 로그인 구현

소셜 로그인 구현은 이번이 처음이었는데, 프론트부분에서 복잡한건 많이 없었다.
그래도 처음 해본 만큼 기록해두려고 코드를 가져왔다.

```jsx
const loginWithKakao = () => {
  window.Kakao.Auth.login({
    success: authObj => {
      console.log('success : ', authObj)
      fetch('http://3.34.144.236:8080/member/kakao', {
        headers: {
          Authorization: authObj.access_token,
        },
      })
        .then(res => res.json())
        .then(res => {
          if (res.message === 'SUCCESS') {
            localStorage.setItem('patago_token', res.token)
            alert('Successfully Signed in!')
          }
        })
    },
    fail: function(err) {
      alert('Sorry, Please Check your information again!')
      console.log('에러', err)
    },
  })
}
```

소셜로그인의 경우 프론트에서 받게 되는 토큰이 총 2개인데 하나는 카카오 토근, 다른하나는 우리팀 백앤드에서 보내주는 토큰이다.  
그래서 kakao 로그인 메서드를 가지고 최초 호출을 해보면 success일 시, 카카오에서 보내주는 access token을 볼 수 있다.

이 토큰을 header에 담아서 백앤드 api에 호출을 하면 백앤드에서는 이 토큰을 가지고 다시 카카오에서 받아온 DB를 가지고 회원을 식별한다. 만약 DB에 없는 회원일 경우, 회원가입 처리를 시키고 있는 회원은 유저 고유의 토큰을 돌려보내준다.

그럼 프론트에서 그 토큰을 로컬스토리지에 저장시키고 로그인 처리를 완료하면 된다.

### 3) 데이터 필터링

파타고니아에서는 유난히 필터링 기능이 많았다. 그래서 필터링과 map 메서드로 ui 구현에 있어서 많이 익숙해진 시간이었다.

```jsx
//필터링 함수
const filterColor = color => {
  const tempArr = { ...props.data }
  if (filteredProducts) {
    tempArr.option = tempArr.option.filter(
      option => option.color_code === color
    )
    setFilteredProducts(tempArr)
  }
}
```

위의 코드를 짜면서 애를 꽤 오래 먹었는데, 그 이유는 객체를 복사할때 불변성을 유지하면서 복사하는 것에 대해 개념적으로만 알고 있었지 실질적으로 활용해본 적이 전무했기 때문이다. 그래서 불변성을 유지하지 않고 복사했을때 원본 데이터까지 바뀌어버려서 삽질을 하다가 해결하게 된 코드가 바로 위의 코드블럭이다. 그래서 이 코드는 꼭 기억하려고 가져왔다.

위의 함수를 props로 자식 컴포넌트 <Thumbnail />에 내려줬고, 이 자식컴포넌트에서는 map 메서드를 활용해 옵션의 섬네일 사진들이 렌더링 + 각 사진들에 필터링 메서드가 적용되도록 구현했다.

```jsx
const Thumbnail = props => {
  const [clickedThumbNail, setClickedThumbnail] = useState(false)

  const handleThumbNail = id => {
    setClickedThumbnail(id)
  }

  return (
    props.thumbnail !== undefined &&
    props.thumbnail.map(thumb => {
      return (
        <ImgWrap onClick={() => props.filterColor(thumb.code)}>
          <ThumbnailWrap>
            <IMG
              src={thumb.image_url}
              onClick={() => handleThumbNail(thumb.id)}
              alt="thumnails"
            />
            <Icon isActive={clickedThumbNail === thumb.id}>
              <i class="fas fa-check-circle"></i>
            </Icon>
          </ThumbnailWrap>
        </ImgWrap>
      )
    })
  )
}

export default Thumbnail
```

### 여러개의 input창을 한번에 관리하는 custom hook

이건 프로젝트가 끝나고 최근에 보완하면서 추가하게 된 기능이다.
hook의 파워를 체감하게 해준 녀석인데, 일단 내가 구현한 ui는 유저의 개인정보를 수정할 수 있는 페이지라서
여러개의 input창이 있고 상태관리를 통해 변경된 값을 백앤드에 보내줘야했다.

처음에는 useState로 매 input마다 만들다가 onChnage 이벤트 핸들러 함수를 만들다가 이게 아닌데..라는 생각이 들어서 공부하다 새로 배운 custom hook을 적용했다.

먼저 useInputState.js라는 파일을 만들었다.

```jsx
import { useCallback, useState } from 'react'

function useInputState(defaultState) {
  const [state, setState] = useState(defaultState)

  const handleChangeState = useCallback(({ target: { value } }) => {
    setState(value)
  }, [])

  return [state, setState, handleChangeState]
}

export default useInputState
```

이 안에는 state, setState 뿐만아니라 handleChangeState 함수까지 한번에 정의해놓고 들어오는 인자에 따라 재사용을 할 수 있게 만든것이다. defaultState라는 인자에 어떤값을 넣어도 이제 상태관리를 할 수 있게 되었다.

이 hook을 내가 적용하려는 페이지에 import하여 사용한 코드는 다음과 같다.
이 custom hook은 children props와 함께 최근에 공부한 것 중에 가장 유용하다고 자부할 만큼 좋은 것 같다.

```jsx
const EditProfilePage = () => {
  const [firstname, setFirstname, handleChangeFirstname] = useInputState('')
  const [lastname, setLastname, handleChangeLastname] = useInputState('')
  const [email, setEmail, handleChangeEmail] = useInputState('')

  useEffect(() => {
    fetch(`http://3.34.144.236:8080/member/`, {
      method: 'GET',
      headers: {
        Authorization: token,
      },
    })
      .then(res => res.json())
      .then(res => {
        setFirstname(res.member_info.firstname)
        setLastname(res.member_info.lastname)
        setEmail(res.member_info.email)
      })
  }, [])

  return (
    <ProfileDetails>
      <Label>First Name</Label>
      <InputWrap
        onClick={() => handleInputClick(1)}
        clicked={num === 1 ? clicked : null}
      >
        <StyledInput
          type="text"
          value={firstname}
          placeholder="First name"
          onChange={handleChangeFirstname}
        />
      </InputWrap>
    </ProfileDetails>
  )
}
```

## 5. 느낀점

회고를 쓰길 잘 했다는 생각이 든다.  
그 전에는 그냥 무조건 내가 원하는 결과물을 못 얻었다는 생각에 외면하기에 급급했다. 원래 자기 자신의 치부는 들여다보고싶지 않은 법이니까....  
하지만 이번 기회로 내 코드를 다시 한 번 찬찬히 돌아보니까 이건 치부가 아니라 성과였다.  
그리고 지금은 여기에서 더 성장했다는 걸 스스로 알고 있어서 그런지 더 편안하게 보고 지난 날을 점검할 수 있었던 시간이었다.

가장 아쉬웠던 건, 꼭 하고싶었던 Redux를 이용한 전역상태관리를 해보지 못했던 것이다.  
하지만 2주라는 기간 내에 무언갈 만들어낸다는건 사실 쉬운 일이 아니다.  
게다가 hooks와 Styled Component, git rebase 모두 이번 프로젝트를 하면서 처음으로 시도해보고 사용했던 거라서 그때 당시 느낌으로는 정말 더듬거리며 코드를 치는 기분으로 한 줄 한 줄 코딩을 했었다.
그때는 한 페이지를 만들더라도 새로운 기술 적용하는것에 의의를 두고 해보자 라는 마음으로 했었으니까,
그것에 대한 목표는 달성했다.

그리고 무언갈 해보지 못해서 아쉬움이 든다면 그건 그냥 하면 된다.

그래서 부트캠프 수료 후 취업준비를 하면서 기능구현에 대한 작은 목표를 설정했다.  
바로, 장바구니 기능을 `Redux`를 활용하여 구현해보는 것.

감사하게도 프로젝트를 함께 했던 백앤드 개발자 영빈님과 마음이 맞아서 이러한 작업을 할 수 있게 되었다.
프로젝트를 보완하고 싶을때 백앤드와 여건이 맞지 않았다면 약간의 난관에 부딪쳤을 것 같은데, 먼저 영빈님께서 새로운 api를 개발하시고 컨택을 해주셨다. 새로 만들고 싶은 페이지가 더 있다면 이야기해달라는 말씀과 함께.  
프로젝트를 함께 할때에도 멘탈관리에 도움을 많이 받았었던 것도 참 감사했는데 수료 후에도 좋은 분과의 인연은 계속 되는 것 같다.

어쨌든 이렇게 길었던 2차 프로젝트 회고를 마쳐야겠다.  
가까운 미래에 전역상태관리를 드디어 할 수 있게 되었을때 기분 좋게 이 곳에 돌아와 셀프 자랑타임을 가질 생각이다. (야심찬 포부)

<br>
<br>
<br>
