# 36기 1차 프로젝트 'BODYLIKE' 
![스크린샷 2022-08-26 오후 4 28 45](https://user-images.githubusercontent.com/107386533/186849064-278872a7-fc09-4ac6-bb1f-77d3d01f0958.png)

- 바디 용품 커머스 사이트 '바디럽'을 클론하였습니다. 
- 외부 라이브러리 사용 없이, React CRA 툴을 사용하여 구현하였습니다. 

## 개발 기간
- 2022년 8월 16일 ~ 2022년 8월 25일 10일

## 팀 코너 
- 프론트엔드 개발자 : 최규선, 조은지, 조민재
- 벡엔드 개발자 : 이지현, 백민석

## 사용 기술 
- 프론트엔드 : JavaScript, React.js, Sass
- 백엔드 : Node.js, MySQL 8.0, Postman, Express 
- 협업 툴 : Trello, Slack, googleSheet

## 구현 기능 
- 최규선 : 메인 페이지, 페이지네이션, 리뷰 페이지 
- 조은지 : 로그인/회원가입 페이지, 상품 상세 페이지
- 조민재 : 내비게이션 바/푸터, 상품 검색 기능, 장바구니 페이지

<br />
<br />

#### 로그인/회원가입 페이지
![로그인](https://blog.kakaocdn.net/dn/btGJ8L/btrKGp2I5Pl/do5RvatE0KIkYPpOWQ93y0/img.gif)
- 로그인창에서 회원가입 버튼 누를시 회원가입 창으로 넘어갑니다
- 회원가입창/ 로그인창에서 아이디 창 '@', 5글자 && 비밀번호 창 5글자 이상 입력시 회원가입 버튼 활성화 (비밀번호 영문 소대문자 없을 시 알림창 뜸)
- 로그인창에서 id, pw 기입 후 로그인 버튼 누를 시 서버와 통신 후 로컬 스토리지에 토큰 발급, 메인창으로 넘어갑니다
- 왼측 상단 로고 클릭시 메인으로 이동


<br />

**상세 설명**


로그인 창 / 회원 가입은 총 두 개의 js 파일로 만들었고 (scss 제외)
login.js 파일엔 같은 html 안에서 location을 써 다른 url을 가질 수 있도록 했습니다

 
LOGIN_DATA/ SIGNUP_DATA를 상수 데이터로 만들어 페이지가 바뀌면 각각 객체에 담긴 값을 보이게끔 했고
한 버튼에 각각 다른 기능이 들어가야 하므로 이를 isSelectLogin 에 담아 User.js에 넘겨주었습니다
(이때 title, btnText, img 라는 이름으로 다시 구조분해할당 )
이는 onClick {isSelectLogin ? toLogin : toSignup} 으로 기능 구현했습니다

Fetch 함수를 써 서버와 통신하고
로그인하는 버튼 (서버에게 Input 값을 보내어 회원 여부를 판단하고 일치하다면 토큰을 발급해 로컬스토리지에 넣게 함)과 
회원가입 하는 버튼 (서버에게 input 값을 보내어 JWT를 이용해 토큰을 발급하게 함) 을 페이지 URL마다 다르게 넣었습니다




<br />
<br />
<br />

#### 상품 상세 페이지

![상세](https://blog.kakaocdn.net/dn/Gn5Xk/btrKGRDLagS/NbKK2AwoV19ixffDPoDqR0/img.gif)
![상세2](https://blog.kakaocdn.net/dn/dltnVp/btrKGOf9axq/4l3PCVMFlp4R9Y3MfMnBbk/img.gif)


- 상품 정보 옆 리뷰 버튼 누르면 하단 리뷰로 슬라이드
- 상품 카운트 음수로 내려갈 시, 재고 이상 누를 시 알림창이 뜹니다
- 상품 카운트 누른 후 장바구니 클릭 시 로그인 되어 있을 시 모달창 뜨면서 장바구니/쇼핑하기 버튼이 뜨고 로그인 안 되어 있을 시 알람창 뜨며 로그인 창으로 이동
- 모달 창에서 장바구니 가기 클릭시 제품이 장바구니에 담기며 장바구니로 이동 

<br />
<br />


**상세 페이지 기능 구현 관련**


상세 정보를 받아오는 (동적 데이터 사용, method : GET) 함수와 장바구니로 가기 버튼과 구매하기 버튼에 총 3개의 Fetch 함수를 사용했습니다

<br />
<br />

**상품 정보를 받아오는 fetch 관련**

params 를 이용해 정보를 받고 params.id를 productId 라는 변수에 넣어 url 끝에 넣어주었습니다
product 데이터는 객체 안의 배열로 오기 때문에 useState에 ([]) 빈 배열을 넣어 주었고
데이터 형식에 따라 각각 name, thumbnail_image_url, price, detail, stock 을 구조 분해 할당해 각각 필요한 곳에 넣었습니다

<br />
<br />

**장바구니 / 구매하기 fetch 함수 관련**

token 변수는 장바구니와 구매하기 버튼 둘 다 사용하므로 상단에 올려놓았습니다.
if 문을 써 얼리 리턴을 위해 token이 없을 경우를 먼저 짰는데 굳이 서버와 통신하지 않아도 토큰 여부를 프론트엔드에서 먼저 확인해 결과를 보여줄 수 있게 했습니다.
method : post 로 서버에 수량을 담아 보내주었고 수량이 재고가 넘을 시 (status 401번) 재고 수량이 부족하다는 알림이 뜨게 했습니다.

재고 수량 관련해서 서버에서 401 코드로 재고 이상 구매 할 수 없도록 막아 놓았으나 이중 보안을 위해 제품 카운트 할 시 알림창에 뜨게끔 막아놓았습니다.
각각 up버튼, down버튼 각각 삼항자를 써 얼리 리턴 형식으로 로직을 짰습니다.
 
<br />

**상세 페이지 내 리뷰 칸으로 슬라이드 하는 기능**

useRef 를 homeRef 변수에 담아 이를 가장 마지막에 있는 리뷰창에 근접한 div에 넣어주었습니다.
스르륵 넘어갈 수 있도록 {behavior : 'smooth'} 스타일을 걸었습니다.


<br />
<br />
<br />



** 커뮤니케이션 **

<br />
<br />

** Trello **

![트렐로](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FOKkVP%2FbtrKHcvccXv%2Fceqr7TPFi7dpRckPgnkoEk%2Fimg.png)

팀원과 작업 진행 사항 공유를 위해 트렐로를 사용하였습니다.

<br />
<br />


** google SpreadSheet (API 명세서 공유) **

![구글시트](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqLyv3%2FbtrKHw1idfO%2Fqg4bV8unkSuTshi8T8CIkk%2Fimg.png)

백엔드 분들과 URL, data 형식 등 원활한 소통을 위해 googlesheet 를 사용하였습니다.

<br />
<br />

** flow-chart  **

![플로우차트](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fn7wGI%2FbtrKJ4JJ638%2FU2K1flR17hVMtVzKLd6FU1%2Fimg.jpg)


전체적인 흐름을 되짚어 보기 위해 프로젝트 5일차, 전 팀원이 모여 플로우 차트를 짜는 회의를 진행하였습니다.
백엔드-프론트엔드와의 소통과 프론트엔드 안에서의 소통이 원활하게 이루어져 소통이 어긋났던 부분을 세세히 체크했습니다.

<br />
<br />
<br />

# Reference
- 이 프로젝트는 바디럽 사이트를 참조하여 학습목적으로 만들었습니다.
- 실무수준의 프로젝트이지만 학습용으로 만들었기 때문에 이 코드를 활용하여 이득을 취하거나 무단 배포할 경우 법적으로 문제될 수 있습니다.
- 이 프로젝트에서 사용하고 있는 사진 대부분은 위코드에서 구매한 것이므로 해당 프로젝트 외부인이 사용할 수 없습니다.
