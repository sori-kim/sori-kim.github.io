---
layout: post
title: 'Dooboolab  기업협업 인턴 회고'
tags: 'Review'
---

## 짧았던 인턴생활을 회고하며

4주간 진행되었던 Dooboolab에서의 인턴 생활은 동기들과 함께 부둥부둥해주며 생활하던 부트캠프 밖을 벗어나,본격적으로 개발자의 사회에 첫 발을 딛는 시간이었다.

내가 인턴으로 한달동안 지냈던 `Dooboolab`은 국내 최초의 'Community driven company'로, 'React Native Seoul' 이라는 RN 개발자들을 위한 커뮤니티를 운영하며 오픈소스들을 개발하는 곳이다.

RN 개발자라면 반드시 `Dooboolab`과 `React Native Seoul`을 한 번은 거쳐간다는 이야기가 들릴 정도로 활발한 활동을 펼치고 있는 기업이다.

이런 곳에서 짧은 시간 동안이나마 인턴을 경험 할 수 있다는 건 나같은 병아리 개발자에게 정말 감사한 일이었다.
짧았던 시간이지만 개발자로서의 시야를 넓히게 해주었던 시간을 기억하기 위해서 이 회고를 적는다.

## 사회에서의 첫 발은 늘 가장 어렵다

인턴 첫 날 킥오프를 하며 깨달은 건, 그동안 공부했던 것들이 사막의 모래알 만큼의 미미한 수준이었다는 거다.

Dooboolab은 React Native의 개발 업계를 이끌고 있는 것 뿐만 아니라, GraphQL과 Relay, TypeScript, Jest, CircleCI, Storybook 등 온갖 핫한 프레임워크와 툴을 활용하여 탄탄한 개발을 하고 있었다.

React Native 개발자들이 손쉽게 초기세팅을 할 수 있도록 기본폴더구조부터 테스팅까지 적용된 보일러플레이트 `dooboo-cli`,
React Native ui component인 `dooboo-ui`를 오픈소스로 개발하여 공유하고 하고 있다는 것에 정말 놀랐다.

그 덕분에 인턴을 시작하고 며칠 간은 계속 어안이 벙벙한 상태로 개발의 감을 잡아가기 위해 노력해야만했다.
너무 많은 새로운 지식들이 쏟아져서 어디서부터 접근해야할지 모르겠던 게 솔직한 심정이었다.

하지만 그렇다고 해서 계속 어리둥절해하고 있을 수 많은 없는 법.  
얼른 정신을 차리고 조금씩 내가 할 수 있는 수준에서 일을 탐색해나가기로 했다.  
뒤집어서 생각해보면 그만큼 많은 걸 배우고 개발자로서의 시야를 넓힐 수 있는 기회가 주어진 거였으니까. 작지만 나만의 목표를 잡고 본격적으로 개발을 해보기로 했다.

## 그래서 내가 세운 목표는...

눈에 보이는 크고 멋진 것을 만들지는 못할지라도, 아래의 것들을 시도해보는 것으로 세웠다.

- 다양한 개발자 경험을 해보고 오픈소스에 기여하는 구조에 대해 이해하기.
- React Native와 TypeScript를 적용하여 개발을 해보기.
- TDD(Test Driven Development)를 이해하기.

<br>

## 내가 수행했던 역할과 과제

우리에게 주어진 과제는 Dooboolab의 오픈소스 프로젝트 중 하나인 [dooboo-ui](https://github.com/dooboolab/dooboo-ui)의 컴포넌트를 개선하고 새로운 컴포넌트를 개발하는 것이었다.

dooboo-ui는 말하자면 google의 material-ui처럼 누구나 쉽게 사용할 수 있고 커스터마이징 할 수 있는 `ui component 플랫폼`이다.

storybook을 통해 ui를 유저가 직접 테스트 해볼 수 있게 구현되어 있고, react native를 기반으로 만들어진 컴포넌트이지만 웹과 모바일에서 모두 사용 가능한 cross-platform이라는 것이 특징적이었다.

현재 어느정도 개발된 컴포넌트들이 있었고 이용하고 있는 개발자들 역시 꽤 있는 상태에서,  
이 dooboo-ui를 더욱 풍성하게 만들 수 있게 새로운 컴포넌트들을 개발하기로 했다.

## 전반부 (1-2주차)

dooboo ui의 코드 자체가 TypeScirpt를 기반으로 이루어져 있어서 이 부분에 대한 공부가 선행되어야지 코드를 이해할 수 있겠다고 판단했다. 그래서 초반 2주동안은 React Native가 React와 어떻게 다른지와 TypeScript, Jest 등에 대해 공부하는 시간을 가졌다.

그리고 React Native가 기본적으로 어떤 특징들을 갖고 있는지 이해하기 위해 기존에 개발했던 Instagram 클론 프로젝트를 RN으로 바꿔보는 작업과 React Navigation의 원리를 공부했다.

사실 시간이 지난 뒤 생각해보면 이 부분은 컴포넌트를 개발하는데에 있어서 큰 도움이 되지는 않았지만 뼈대를 모른 채 부품을 만든다는 것에 대한 불안감, 그리고 앱개발에 대한 호기심과 갈증이 어느정도 해소될 수 있는 계기로 작용했다.

## 후반부 (3-4주차)

본격적으로 컴포넌트 개발을 시작했다.  
나는 modal이 웹과 앱에서 보편적으로 많이 사용되고 중요한 컴포넌트라고 판단하여 modal 구현을 맡아서 개발을 하게 되었다.

사실 코드의 재사용성과 컴포넌트화의 중요성에 대한 이야기를 귀가 닳도록 들었지만 실제 프로젝트를 할 때 코드에 적용하기란 쉽지 않았다.  
 2주동안 프로젝트를 완성해야했기 때문에 일단 기능이 돌아가는 코드를 만들면 그걸로 만족하기에 급급했고,
간단한 컴포넌트의 재사용 조차 시도해보려다가 포기했었다.

그런데 이번 프로젝트의 핵심이 바로 `재사용 가능한 컴포넌트 개발`이었고,  
나 뿐만 아니라 누구나 그걸 가지고 원하는대로 커스터마이징 할 수 있게 틀을 잡아줘야했다.  
개발을 시작하고 생전 처음해보는 작업이어서 초반에 어떻게 구조를 잡아야할지 감을 전혀 잡지 못해서 오랜시간 구글링을 하며 방황했다...  
그러다가 나를 살려준 것은 다름 아닌 `react children` 개념이었다.

## React children prop : 컴포넌트에서 다른 컴포넌트를 담기

React 공식문서에는 children prop을 `합성 vs 상속` 카테고리에서 설명하고 있다.  
공식문서에서 이 부분이 특히 중요한 것 같으니 여러번 읽으면서 숙지해둬야겠다. [참고](https://ko.reactjs.org/docs/composition-vs-inheritance.html)

어떤 컴포넌트들은 어떤 자식 엘리먼트가 들어올 지 미리 예상할 수 없는 경우가 있다.  
주로 ‘박스’ 역할을 하는 Sidebar 혹은 Dialog와 같은 컴포넌트에서 특히 자주 볼 수 있는데,  
이러한 컴포넌트에서는 children prop을 사용하여 자식 엘리먼트를 출력에 그대로 전달하는 것이 좋다.

참고로, React API에는 이 props와 함께 사용할 수 있는 React.Children.map, React.Children.forEach, React.Children.count, React.Children.only, React.Children.toArray등 여러가지 방법이 있다.

<br>

children prop의 간단한 사용법은 아래와 같다.

```jsx
//부모 컴포넌트
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">Welcome</h1>
      <p className="Dialog-message">Thank you for visiting our spacecraft!</p>
    </FancyBorder>
  )
}
```

```jsx
//자식 컴포넌트
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  )
}
```

FancyBorder JSX 태그 안에 있는 것들이 FancyBorder 컴포넌트의 children prop으로 전달된다. FancyBorder는 {props.children}을 div 안에 렌더링하므로 전달된 엘리먼트들이 최종 출력되는걸 알 수 있다.

<br>

## dooboo-ui Modal Component의 구조

내가 dooboo-ui에 제안을 했던 modal component는 일단 앞서 언급했던 react children props를 주요하게 사용했고,  
부모 컴포넌트가 modal을 컨트롤하는 props를 정의할 수 있게끔 하는 일반적인 라이브러리 방식대로 만들었다.

`modalVisible`은 modal이 보여지고 사라지게 하는 boolean값이고,  
`closable`은 modal 내부의 삭제 아이콘 유무를 컨트롤 하는 boolean값,
`backdropClosable`은 modal 백그라운드를 클릭했을때 모달창이 사라지게 하는 boolean값이다.  
그리고 modal의 `mode`는 기본적인 팝오버 형태의 'default'와  
선택가능한 dropdown이 나타나는 'modalPicker' mode 두 가지를 만들었다.

props 이름은 최대한 직관적으로 만들기 위해 노력했다.

```jsx
function ModalPage(props: Props): React.ReactElement {
  const { style, textStyle } = props

  const [modalVisible, setModalVisible] = useState < boolean > false
  const [isAnimated, setIsAnimated] = useState < boolean > false

  const openModal = (): void => {
    setModalVisible(true)
  }
  const closeModal = (): void => {
    setModalVisible(false)
  }

  return (
    <Container>
      <ModalOpenButton
        onPress={(): void => {
          setIsAnimated(true)
          openModal()
        }}
      >
        <Text
          style={[
            textStyle,
            { color: '#ffff', fontWeight: '600', fontSize: '17px' },
          ]}
        ></Text>
      </ModalOpenButton>
      {modalVisible && (
        <Modal
          visible={modalVisible}
          closable={true}
          backDropClosable={true}
          onClose={closeModal}
          style={style}
          isAnimated={isAnimated}
          animationType={'up'}
          animationSpeed={500}
          mode={'default'}
          data={data}
          initialValue={'Dooboolab'}
          value={value}
          setValue={setValue}
        >
          >
          <Text
            style={[
              textStyle,
              { color: '#088EDF', fontWeight: '600', textAlign: 'center' },
            ]}
          >
            Hello, I am Modal 🤘🏻
          </Text>
        </Modal>
      )}
    </Container>
  )
}
```

그리고 modal 컴포넌트 코드는 다음과 같이 짰다.  
유저가 컴포넌트에 특정 props를 지정하지 않아도 동작할 수 있도록 몇가지 기본값들을 지정해두었다.

이번에 처음 타입스크립트를 써보면서 가장 유용하게 사용했던 것이 바로 interface였다.  
컴포넌트가 필요로 하는 props들을 가장 위에 정의해놓으니까 코드의 가독성도 높아지고,  
어떤 props가 어떤 데이터타입으로 들어오는지 확인하면서 코드를 작성할 수 있어서 도움이 많이 되었다.

아직은 타입 정의하는 게 어렵긴 하지만 타입스크립트는 이렇게 조금씩 적용해나가면서 익숙해져도 나쁘지않을 것 같다.

```jsx
import {
  Animated,
  GestureResponderEvent,
  Picker,
  TouchableOpacity,
  ViewStyle,
} from 'react-native'
import React, { useRef, useState } from 'react'

import styled from 'styled-components/native'
interface Props {
  visible: boolean;
  closable?: boolean;
  backDropClosable?: boolean;
  onClose?: () => void;
  children: React.ReactElement;
  style?: ViewStyle;
  isAnimated?: boolean;
  animationType?: string;
  animationSpeed?: number;
  mode?: string;
  data?: [];
  initialValue?: string;
  value?: string;
  setValue?: React.Dispatch<React.SetStateAction<string>>;
}

interface StyledProps {
  visible: boolean;
}
function Modal(props: Props): React.ReactElement {
  const {
    visible = false,
    closable = true,
    backDropClosable = true,
    onClose,
    children,
    style,
    isAnimated = false,
    animationType = 'up',
    animationSpeed = 700,
    mode = 'default',
    data,
    initialValue,
    value,
    setValue,
  } = props

  const close = (e: GestureResponderEvent): void => {
    if (onClose) {
      onClose(e)
    }
  }

  function CloseButton(): React.ReactElement {
    return (
      <TouchableOpacity onPress={onClose}>
        <StyledBtn source={require('../__assets__/close.png')} />
      </TouchableOpacity>
    )
  }

  function ModalPicker(props): React.ReactElement {
    const { data, value, setValue } = props

    return (
      <StyledPicker>
        <Picker
          selectedValue={value}
          onValueChange={(itemValue): void => {
            setValue(itemValue)
            alert('Selected!')
          }}
        >
          {data.map((option, index) => {
            return (
              <Picker.Item
                value={option.label}
                label={option.label}
                key={index}
              />
            )
          })}
        </Picker>
      </StyledPicker>
    )
  }

  const defaultAnimation = useRef(new Animated.Value(300)).current
  const fadeAnimation = useRef(new Animated.Value(0)).current
  const zoomAnimation = useRef(new Animated.Value(0.8)).current

  if (animationType === 'default') {
    Animated.timing(defaultAnimation, {
      toValue: 10,
      duration: animationSpeed,
      useNativeDriver: true,
    }).start()
  }

  if (animationType === 'fadeIn') {
    Animated.timing(fadeAnimation, {
      toValue: 1,
      duration: animationSpeed,
      useNativeDriver: true,
    }).start()
  }

  if (animationType === 'zoom') {
    Animated.timing(zoomAnimation, {
      toValue: 1,
      duration: animationSpeed,
      useNativeDriver: true,
    }).start()
  }

  return (
    <>
      <ModalOverlay
        visible={visible}
        onPress={backDropClosable ? close : null}
      />
      <ModalWrapper
        as={Animated.View}
        visible={visible}
        style={[
          isAnimated && animationType === 'up'
            ? { transform: [{ translateY: defaultAnimation }] }
            : null,
          isAnimated && animationType === 'fadeIn'
            ? { opacity: fadeAnimation }
            : null,
          isAnimated && animationType === 'zoom'
            ? { transform: [{ scale: zoomAnimation }] }
            : null,
        ]}
      >
        <ModalInner style={style}>
          {closable && <CloseButton />}
          {mode === 'modalPicker' && <ModalPicker data={data} />}
          {children}
        </ModalInner>
      </ModalWrapper>
    </>
  )
}
```

React Native 개발은 React 개발 방식에서 크게 벗어나지 않되, 주로 사용하게 되는 컴포넌트 요소들이 RN 고유의 것이라는 것 정도만 달라서 어렵지 않았다.

다만, 애니메이션을 적용하는 부분이 React와 다르게 완전히 새로워서 초반에 modal에 애니메이션을 적용하는데에 애를 먹었다.
공식 문서를 보면서 연구했던 게 도움이 되었다.

```jsx
const defaultAnimation = useRef(new Animated.Value(300)).current
const fadeAnimation = useRef(new Animated.Value(0)).current

if (animationType === 'default') {
  Animated.timing(defaultAnimation, {
    toValue: 10,
    duration: animationSpeed,
    useNativeDriver: true,
  }).start()
}

if (animationType === 'fadeIn') {
  Animated.timing(fadeAnimation, {
    toValue: 1,
    duration: animationSpeed,
    useNativeDriver: true,
  }).start()
}
```

내가 쓴 방법은 useRef를 이용해서 초기값을 정의해준 뒤,  
 Animated.timing() 이라는 함수를 이용해서 내가 원하는 변경값을 toValue값으로 주고,  
어떤 속도로 변화를 주고 싶은지 duration에 넣어주는 식으로 구현했다.
useNativeDriver는 ios에서 네이티브코드를 컨트롤하는 어떤 프롭스인걸로 추정된다.

그리고 style에 css를 적용해주면 되는데 다음과 같이 코드를 썼다.  
 참고로, style 프롭스 안에 배열 형태로 여러가지 스타일을 주는 건 React Native만의 문법이다.

```jsx
 <ModalWrapper
    as={Animated.View}
    visible={visible}
    style={[
      isAnimated && animationType === 'default'
       ? { transform: [{ translateY: defaultAnimation }] }
       : null,
      isAnimated && animationType === 'fadeIn'
       ? { opacity: fadeAnimation }
       : null
        ]}>
```

<br>

## 기업협업 인턴, 그 후의 이야기

아쉬움이 많았던 인턴 생활이다.  
개발자로서 처음 하는 사회생활이다보니 긴장도 많이 했고,
더군다나 오픈소스 기여하는 프로젝트는 처음이었어서 과연 내 비루한 코드로
PR을 날려도 되는지 고민하다가 결국 시간에 쫓겨 마지막 주에 처음으로 자신 없는 PR을 날리게 되었다.
개인적으로 완성도 있는 코드를 짜서 보여주고 싶다는 욕심도 한 몫 했던 것 같다.

그런데 정말 감사하게도 dooboolab의 개발자 분들은 정말 꼼꼼히 내 코드를 봐주셨다. 예상하지 못한 일이었다.
그리고 자연스럽게 내가 아마 더 많은 pr을 날렸다면 더 많은 코드리뷰를 받고 더 많이 배울 수 있었을 텐데... 라는 아쉬움의 감정이 뒤따라왔다.

오픈소스 라는 건 정말 소수의 실력있는 개발자만이 참여할 수 있는 영역의 것이라고 생각했지만, 실은 그렇지 않았다.  
나도 언제든지 기여하고 싶은 분야의 레포를 fork하는 것을 시작으로 오픈소스 기여 작업에 참여할 수 있는 거였다.
이 깨달음 만으로도 이미 굉장히 소중한 경험을 했다는 생각이 든다.

게다가 이런 오픈소스 프로세스와 코드리뷰 외에도 dooboolab의 대표 hyo가 개발자로서 너무 좋은 마인드와 자세를 갖고 계셔서,
그 분이 이야기해주시는 개발자에게 필요한 자세같은 조언이 참 인상적이었다. (어디선가 들었는데 dooboo가 꼰대의 반대되는 '말랑말랑한' 의미를 갖고 있다고 한다.)

비록 인턴은 끝났지만 dooboo-ui에 계속적으로 기여하면서 이 경험을 지속해보고싶다.  
(내 modal이 merge되는 그날까지... to be continue 😂)
