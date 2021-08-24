---
layout: post
title: 'Wecode 1차 프로젝트 Subway 웹사이트 개발 회고'
tags: 'Review'
---

## 1. 진행한 프로젝트 소개

부트캠프에서 웹개발을 배운지 5주차에 드디어 첫번째 팀 프로젝트를 2주 동안 진행했다. 주제는 샌드위치 브랜드 '서브웨이(Subway)'의 웹 사이트를 개발하는 프로젝트였다. 프론트 3명, 백앤드 2명의 모두 부트캠프에서 처음으로 개발을 배운 사람들로 이루어진 팀원들과 함께 프로젝트를 진행했다.

한국 서브웨이 웹사이트를 기본 뼈대로 잡고 클론을 진행했고 한국 서브웨이 사이트에 없는 회원가입,로그인 / 커스터마이징 기능의 경우 미국 서브웨이 사이트를 참고해서 기능을 추가하는 식으로 단순한 클론이 아니라 사용자 입장에서 좀 더 효과적으로 다가올 수 있는 서비스를 개발해보려고 노력했다. (20' 6월 웹사이트 기준)

<br>
<br>

## 2. 기술 스택

- 프론트앤드: HTML, CSS, JavaScript, React.js, Sass
- 백앤드: Python, Django, MySQL

## 3. 내가 맡은 역할

1. 메인페이지 구현

   - CRA 초기세팅
   - 메인 페이지 내 filter 처리를 하여 카테고라이징한 메뉴 섹션 구현
   - slick-slider.js 라이브러리 활용
   - url-parameter를 활용하여 메뉴의 상품 클릭 시 상세 상품페이지로 이동되는 라우팅 기능
   - Header(Dropdown Navbar) / footer 컴포넌트 작업

2. 커스터마이징 페이지 구현 (w.영목)

   - 상품 상세 페이지에서 연결되는 커스터마이징 기능 레이아웃 작업
   - 각 상품 상세페이지에서 url-parameter로 연결하여 각 샌드위치의 default-ingredients가 화면에 렌더링 되도록 작업
   - default-ingredients에서 빵 선택 컴포넌트와 연결
   - 선택한 빵이 커스터마이징 페이지에 반영 되도록 구현 (로컬스토리지)
   - 토핑선택 버튼 클릭시 토핑 선택 페이지로 이동되고 선택된 토핑들이 커스터마이징 페이지에 반영 되도록 구현 (로컬스토리지)

<br>

## 4. 성장한 부분과 아쉬운 부분

### 1) 성장한 부분

- CRA 초기세팅에 익숙해졌다. <br>
  리액트를 배운지 고작 2주만에 프로젝트를 진행다는 점에서 오는 불안감이 상당했다. 게다가 이 전에 미니 프로젝트로 진행했던 인스타그램 클론 코딩 프로젝트때 CRA 초기세팅을 하는데에 어려움을 겪여서 이번에도 걱정을 안고 있었다. 그러다 내가 메인페이지를 담당하게 되면서 자연스럽게 초기세팅까지 해서 git에 올리는 작업을 맡아서 했다. 팀원들이 함께 도와줘서 큰 어려움 없이 하기도 했지만 이번 경험을 하면서 기본적인 팀 프로젝트 작업의 flow를 알게 된 것 같아서 만족스럽다.

  <br>

- Git의 협업 flow에 익숙해졌다. <br>
  앞서 말했던 초기세팅과 마찬가지로 git에 대한 개념도 단순히 add / commit / push밖에 잘 알지 못하다가 이번 프로젝트를 하면서 비로소 컨플릭트도 경험해보고 merge를 한번 하는게 이렇게 쉽지않다는 것 또한 알게 되었다. 전에는 컨플릭트 한번 날까봐 노심초사 하면서 다른 사람 파일 건드리는게 두려웠는데 이제는 컨플릭트를 크게 두려워하지 않게 된 것 같다. 커밋메세지도 정성들여서 쓰는 연습을 하면서 커밋 하나 하나에 좀 더 책임감을 가지고 신중하게 작업을 하기 시작하게 된 것 같다.

  <br>

- sass를 사용하는게 많이 익숙해졌다. <br>
  sass를 활용하여 nesting 기능만 쓰다가 이번 프로젝트때 common styling을 위해 mixin과 변수 설정 등의 기능들을 활용해봤는데, 특히 서브웨이 메인 컬러나 폰트 컬러 등을 변수화해놓고 필요할때마다 꺼내 쓰니까 정말 편했다. css 작업을 하는데에 있어서 삶의질이 한 층 향상된 걸 느끼며 코딩했다.

<br>

- react에서 자주 사용하는 javascript 메서드가 좀 더 익숙해졌다. <br>
  Array.map()이나 Array.filter() 등을 react에서는 컴포넌트 작업을 하면서 정말 많이 사용하는데 이번 기회에 fetch 후에 돌아오는 백앤드 데이터를 state에 저장하고 이 데이터들을 핸들링하는 방법에 대해 충분히 연습할 수 있는 시간을 가졌다. 그럼에도 불구하고 map은 아직도 여전히 어려워서 2차때 더 많이 연습하고 편안해질 수 있도록 하고 싶다.

  <br>

- react를 활용하는 웹개발을 할 때에 유용하게 사용되는 기술에 대해 알게 되었다. <br>
  url-parameter/부모자식간의 함수로 값 주고받기(lifting-state-up)/ 클릭핸들러 함수에 인자 전달하여 원하는 결과 뽑아내기 / 객체를 활용하여 active-tab 구현하기 등 웹사이트 개발을 위해 실질적으로 필요한 테크닉들을 배우고 적용해보는 기회가 되었다.

<br>

### 2) 아쉬운 점

아쉬운 점이 정말 너무 x 1000 많은데 2차 플젝때 더 많이 보완할 수 있도록 노력하자고 나를 다독이고 싶다. <br>

- css 화면 비율 유지될 수 있도록 레이아웃 잡는 법에 대한 이해 부족 <br>
  vh나 퍼센트로 width/height 값을 잡는 식으로 큰 그림을 먼저 잡고 min-max를 잘 활용해서 반응형이 적절하게 들어가게 해야하는데 그 부분에 대한 이해가 아직 부족해서 프로젝트 발표 전까지 화면이 깨질까봐 전전긍긍하면서 작업했다.

* react children에 대한 공부를 못해서 컴포넌트를 일부만 변경해서 활용하고싶을때 하지 못함

* modal을 적용해보고싶었는데 ui만 만들어놓고 실제로 써보지를 못함

* 지도 api를 활용해서 매장찾기 기능을 넣고 싶었는데 시간 부족으로 해보지 못함

* 가장 아쉬움이 크게 남은 '커스터마이징' 기능 구현. <br>
  생각보다 너무 어려운 작업이어서 시간을 오래 소모하다보니 결과적으로 다양한 페이지를 구현해내지 못했다.<br>
  그리고 백앤드와의 소통을 원활하게 하지 못해서 프론트쪽에서 필요한 데이터가 어떤게 있는지 정확하게 요청하지 못하다보니, 후에 필요한 데이터가 있는데 포기해야하는 상황이 발생했다..... 😷 <br>
  실제 현업에서 리액트를 사용하는 프로젝트의 경우 대부분 전역 상태관리를 할 수 있게 해주는 redux를 활용한다고 하는데 이번 프로젝트 단계에서는 아직 그 부분에 대한 이해 없이 결과물을 만들어내야했고, 아쉬운대로 localStorage에 데이터를 저장하는 방법을 사용했는데
  후에 리덕스를 배운 후 이부분을 다시 멋지게 개선하고 싶다.

## 5. 기록하고 싶은 코드

멘토님들의 코드리뷰와 함께 고생했던 팀원들의 도움을 정말 많이 받으며 프로젝트를 진행했던지라 기록하고싶은 코드도 많다.
나중에 여력이 될때 구현했던 기능별로 코드를 다시 정리하고싶은데 이번에는 몇가지만 적어두려고 한다.

### onclick 함수에 인자를 전달하여 데이터 카테고리별로 분류

subcategory_id 별로 샌드위치의 종류가 다르게 분류된 데이터를 onClick함수에 그 아이디값을 인자로 전달해서 특정 카테고리명을 클릭할때마다 filter된 데이터를 setState하는 식으로 구현했다. 그리고 각각 카테고리명이 클릭할때마다 색상 역시 활성화 되어야 하기 때문에 isActive라는 state를 만들어서 인자로 전달한 id값에 따라 클래스이름을 토글로 만들었다.

<br>

```jsx
class MenuSection extends React.Component {
  state = {
    sandwich: [],
    filtered_sandwich: [],
    isActive: 1,
  }

  componentDidMount() {
    fetch(`${URL}/product/sandwich`)
      .then(res => res.json())
      .then(res =>
        this.setState({
          sandwich: res.sandwiches,
          filtered_sandwich: res.sandwiches.filter(
            item => item.subcategory_id === 1
          ),
        })
      )
  }

  handleCategoryClick = menu => {
    const { sandwich } = this.state
    this.setState({
      filtered_sandwich: sandwich.filter(item => item.subcategory_id === menu),
      isActive: menu,
    })
  }

  render() {
    return (
      <div className="MenuSection">
        <div className="title">Subway's Menu</div>
        <ul className="category">
          <li
            onClick={() => this.handleCategoryClick(1)}
            className={isActive === 1 ? 'isActive' : 'notActive'}
          >
            <a>클래식</a>
          </li>
          <li
            onClick={() => this.handleCategoryClick(2)}
            className={isActive === 2 ? 'isActive' : 'notActive'}
          >
            <a>프레쉬&라이트</a>
          </li>
          <li
            onClick={() => this.handleCategoryClick(3)}
            className={isActive === 3 ? 'isActive' : 'notActive'}
          >
            <a>프리미엄</a>
          </li>
          <li
            onClick={() => this.handleCategoryClick(4)}
            className={isActive === 4 ? 'isActive' : 'notActive'}
          >
            <a>아침메뉴</a>
          </li>
        </ul>
        <div className="main_button">
          <a className="button_order">
            <img src={franchise} alt="icon" />
            <p>주문하기</p>
          </a>
          <a className="button_map">
            <img src={map} alt="icon" />
            <p>매장찾기</p>
          </a>
        </div>
      </div>
    )
  }
}

export default MenuSection
```

### url-parameter를 활용하여 페이지 간 데이터 연결

페이지의 전반적인 플로우는 다음과 같다. <br>
menu_details라는 상품상세페이지에서 '커스터마이징' 버튼을 클릭했을때 해당 샌드위치에 관련된
커스텀 페이지로 이동한다. 그리고 이 커스텀페이지에서 '토핑선택하기'라는 버튼을 클릭하면 토핑 페이지로 이동하고, 여기서 선택한 토핑 데이터들이 다시 커스텀페이지로 돌아와 반영되어야한다. <br>
이런식으로 세 페이지가 서로 긴밀하게 연결되어야 하기 때문에 url-parameter라는 동적 라우팅을 활용하여 기능을 구현했다. <br>
page_key라는 값을 state에 담고 이 값은 바로 this.props.match.params에 담긴 데이터에 해당되어 페이지 이동을 유발하는 트리거 버튼을 클릭했을때 이 값을 담고 이동할 수 있게끔 했다.

```jsx
//Routes.js
<Route exact path="/menu_details/:key" component={Menu_Details} />
<Route exact path="/custom/:key" component={Custom} />
<Route exact path="/toppings/:key" component={Toppings} />
```

```jsx
//menu_details.js
class Menu_Details extends React.Component {
  state = {
    sandwich: [],
    nutrition: [],
    prev: [],
    next: [],
    id: "",
  };

  componentDidMount = () => {
    window.scrollTo(0, 0);
    this.getData();
  };

  componentDidUpdate = (prevProps) => {
    if (prevProps.match.params.key !== this.props.match.params.key) {
      this.getData();
    }
  };

  getData = () => {
    const num = this.props.match.params.key;
    fetch(`${URL}/product/sandwich/?product_id=${num}`)
      .then((res) => res.json())
      .then((res) =>
        this.setState({
          sandwich: res.product,
          nutrition: res.nutrition,
          prev: res.all_subcategory_products[0],
          next: res.all_subcategory_products[1],
          id: res.product.id,
        })
      );
  };

  render(){
      return(
        <Header />
          <MenuNav />
          <MenuTitle />
        <OrderButton id={id} />
        <MenuSelector />
      )
  }

//OrderButton.js
  render(props) {
    return (
      <div className="btn_wrapper">
        <button>장바구니 추가</button>
        <Link to={`/custom/${this.props.id}`}>
          <button onClick={this.handleUser}>커스터마이즈</button>
        </Link>
      </div>
    );
  }
```

```jsx
//Custom.js
export default class Custom extends React.Component {
  state = {
    isActive: false,
    isShown: "noshow_bread",
    customized: [],
    product_name: "",
    page_key: [],
    default_bread: [],
    default_topping: [],
    cart: [],
    topping: [],
  };

  componentDidMount() {
    const topping_LS = JSON.parse(localStorage.getItem("newTopping"));
    const bread_LS = JSON.parse(localStorage.getItem("newBread"));
    fetch(
      `${URL}/product/sandwich/customization/?product_id=${this.props.match.params.key}`
    )
      .then((res) => res.json())
      .then((res) => {
        this.setState({
          added_bread: bread_LS,
          default_bread: res.all_bread.filter(
            (bread) => bread.name.includes("top") || bread.name.includes("플랫")
          ),
          default_ingredients: res.default_ingredients,
          default_topping: res.default_ingredients.slice(
            1,
            res.default_ingredients.length - 1
          ),
          product_name: res.product_name,
         page_key: this.props.match.params.key,
        });
      }

 render(){
     return(
     <Link
        className="linkOrder"
        to={`/toppings/${this.state.page_key}`}
    >
        <OrderBox
            handleOrder={this.handleOrder}
            orderName={this.state.product_name}
        />
    </Link>
     )
 }
```

```jsx
//toppings.js
getData = () => {
  fetch(`${URL}/product/sandwich/customization/topping/`)
    .then((res) => res.json())
    .then((res) =>
      this.setState({
        toppings: res.all_toppings,
        page_key: this.props.match.params.key,
        selectedToppings: res.all_toppings.filter(
          (topping) => topping.ingredient_category_id === 2
        ),
      })
    );
};

componentDidMount = () => {
  this.getData();
};

render(){
    return(
    <Link to={`/custom/${this.state.page_key}`}>
        <button onClick={this.sendTopping}>토핑 추가</button>
    </Link>
    )
}
```

## 6. 느낀 점

이번 프로젝트는 나 스스로에게 갖고 있던 잘못된 인식과 기대감 같은 것이 조금 깨어짐을 경험한 시간이었다.
난 내가 팀 안에서 리드가 필요한 순간에는 리드를 하고, 팀 안에서 의견 조율을 잘 하며 마지막까지 완성도있게 프로젝트를 마칠 수 있는 사람이라고 기대했다. 하지만 예상외로 나는 프로젝트에서 중요한 부분이라고 생각되었던 기능을 포기하지 않고 싶어했고,
그게 우리가 배운 지식만으로는 구현이 쉽지 않은 부분이었음에도 인정하려고 하지 않았던 것 같다.

결국 프로젝트의 꽤 긴 시간을 그 기능에 투자했지만 각자의 기대에 못미치는 결과로 프로젝트를 종결하게 되었다.
만약 일찍이 그 기능을 포기하고 다른 페이지들을 더 많이 개발했다면 어땠을까, 하는 아쉬움이 남는다.
하지만 우리가 긴 시간 했던 삽질들이 결코 헛된 시간이 아니었다고 이야기하고 싶고, 훗날 그걸 스스로에게 증명하고 싶다.

감사하게도 좋은 팀원들을 만나서 정말 재밌게 코딩하고 회의하며 프로젝트를 했던 시간이었다.
부트캠프에서 프로젝트가 시작되기전에는 혼자서 나에게 주어진 과제를 수행하며 개발을 배웠기 때문에 남들보다 뒤쳐지면 안된다는 은근한 압박을 느끼며 개발을 해야했다.
그러다 팀 프로젝트를 팀원들과 함께해보니 내 옆사람들이 경쟁자가 아닌,
함께 고민하고 힘을 합치는 동료였다는걸 비로소 알게 되었다. 개발은 외로운 혼자만의 싸움 같은 게 아니었다.

첫 프로젝트는 이런 깨달음을 알게 해준 것 만으로도 정말 많이 소중한 시간이었다.
프로젝트 최종 발표 전 날 새벽 5시까지 마지막 스탠드업 미팅을 하고 어떻게든 발표를 위해 마무리를 하기 위해 팀원들과 지새웠던 그 새벽이 꽤 오랫동안 기억이 날 것 같다.
이렇게 추억만 많이 만들었던 서브웨이 프로젝트 회고를 마친다. 🥪

<img src="https://user-images.githubusercontent.com/60246689/88529945-a64e0400-d03b-11ea-97fc-5fa893b01546.PNG" />
<img src="https://user-images.githubusercontent.com/60246689/88529948-a817c780-d03b-11ea-8379-fcccd1279b52.PNG"  />
<img src="https://user-images.githubusercontent.com/60246689/88529951-a948f480-d03b-11ea-84f0-c36835b70fab.PNG"  />

<br />
<br />
