# TIL (Today I Learned )

## 2025

### 2/10
#### Redux saga
- Redux로 애플리케이션에서 비동기적으로 API를 호출하여 데이터를 가져오는 일과 같은 Side Effect를 쉽게 처리하기 위해 사용한다.
- API 를 순차적으로 처리하기, 기존 요청 취소하기 등 까다로운 비동기 작업을 다루는 상황에 유용하다.
- Redux Thunk 다음으로 많이 사용되고 있다.
- Redux saga는 부수 효과들을 처리하기 위해 Generator라는 ES6 기능을 사용한다.
- Generator 사용시 비동기 흐름을 표준 동기 코드처럼 보이게 하여 비동기 흐름을 쉽게 읽고 쓰고 테스트 할 수 있다.
- 

## 2024

### 11/8
#### Package Manager 비교 분석
- Npm
   - 설치하는 것 깊이가 깊어짐 -> (개선한 것) 같은 너비로 디펜던시 설치함
   - 문제점) 비효율적인 설치, Phantom Dependency(유령 의존성)
- Yarn berry
    - Zip 파일 (.yarn > cache 하위) 로 설치
    - pnp(Plug'n'Play) 구조
    - 장점)
       - dependency를 압축파일로 관리- dependency 용량 낮음
       - -> 의존성을 git 으로 관리 가능 (-> zero-install 이라고 부름) ->  CI에서 의존성 설치 시간 줄어 빌드 시간 감소
    - 문제점)
        - zip파일 이름 길음 -> cmd  —cwd 옵션을 별도로 명시해줌
        - node module 고려해 만든 패키지는 호환안됨
- PNpm
    - 필요 개념 정리
        - 하드링크
           -  물리적 복사X, 하나의 파일을 여러 위치에서 동일하게 참조하도록 연결하는 방식.
           -  여러 하드링크가 동일한 파일을 가리킴, 디스크 공간 추가로 사용X.
        - 소프트링크 (심볼릭 링크)
           -  파일/폴더의 위치를 가리키는 포인터 역할.
           -  원본파일이 삭제되면 소프트링크는 유효하지 않는다.
    - pnpm은 중앙저장소 역할을 하는 Global Cache 디렉토리에 패키지를 저장한다.
    - **.pnpm 폴더 <-> Global Cache : 하드링크**
        - .pnpm 은 패키지 저장소를 위한 로컬 캐시 처럼 동작함
        - Global Cache 에 있는 lodash를 하드링크로 연결해 .pnpm 폴더로 가져옴
    - **node_module 폴더 <-> .pnpm : 소프트 링크**
        - node_module/lodash 는 .pnpm 폴더 내의 loads 파일 위치를 소프트 링크로 연결함.
#### MonoRepo
- Nx, TurboRepo
    - 중점적으로 CI 관리 해줌
    - TurboRepo
        - **학습, 설치, 설정 간단함.** 
        - Next, React만 지원한다. (JS, TS 코드를 위해 최적화된 빌드 시스템)
        - 캐싱을 사용해 동일한 작업 진행하지 않음
        - 작업을 병렬적으로 수행해 멀티태스킹 극대화함.
        - **Pnpm** 을 권장한다.  
        - 설계도 만들어줌 (수정시 수정본만 따로 만들어줌) -> TurboRepo에서 원격 캐싱도 지원
    - NX
        - 복잡하고 큰 monorepo 관리에 편하다
        - 모든 프레임웍 지원. **Yarn berry, yarn workspace** 를 추구함.


### 11/4
- Chart 관련 라이브러리 Search, 비교
   - Chart.js
      - MIT License
      - 지원가능: JS, Angular, React, Vue
   - HighChart 
      - 기능적으로 제공하는 부분이 많음. input data 가 자유로움
      - 지원가능: JS, Angular, React, Vue, **AngularJS, JQuery**
   - RealGrid
      - 문서화, 메뉴얼 정리 잘 되어있음
      - 주요 객체들 GridView, DataProvider, DataField, DataColumn, ItemModel(GridItem) 제공
- 개발시 디자인 패턴
   - https://brunch.co.kr/@oemilk/113  
       
 
- 저작권
   - MIT: 누구나 사용가능, 저작권 표기 해야함, 저자는 SW에 대해 아무런 책임을 지지 않는다.
   - GPL: GPL 라이선스 코드를 사용했다면 해당 소스 공개 의무가 있음.
   - LGPL(Lesser GPL): GPL에서 경량화된 버전. 

### 10/22
- Tailwind란
    -  많은 유틸리티(Utility) 클래스로 이루어진 CSS 프레임워크이다.
- CSS inline style 문제점
    ``` 
      <button style="border-radius: 0.25rem; background-color: rgb(59 130 246); padding-top: 0.5rem; padding-bottom: 0.5rem; padding-left: 1rem; padding-right: 1rem; ">
    ```
    - 위와같이 inline style 로 해버리면 pseudo element 쓸수없음
    - 미디어 쿼리 사용 불가 ->  반응형 웹 구현 불가 


      

### 10/18
- styled-component v6 부터 달라진점
   -  Pseudo-class 에 대해 앞에 '&' 안붙이면 동작안함
       - e.g.  :last-child  ->  &:last-child 로 해야 동작함
 - e2e test tool
   - playwright: chrome extension으로도 지원함

### 10/11
- next middleware
   - Next13 부터 도입됨
   - Edge Runtime 이 사용된다.
       - Edge Runtime 이란?
           - Node.js API의 일부로 경량화 된 버전이다.
           - 리소스 사용을 최소화해 속도는 높지만, 제한적이다. (이에 비해 Node.js는 시작 속도가 느리다.)
   - 격었던 이슈
       - SSL 에러가 발생했는데 Edge Runtime 에서는 SSL Option을 넣을 수 없었음.
       - https import 를 못함
       - node runtime에서는 secureOptions: crypto.constants.SSL_OP_LEGACY_SERVER_CONNECT 옵션 넣어서 해결 됨
- jsx 
    - 'cannot be used as a jsx component.' 에러 해결하기
    - 아래 추가 후 해결
    - "resolutions": {
        "@types/react": "18.0.28"
     }          

### 9/26
- BroadcastChannel, PostMessage 차이점
    -  PostMessage: 단방향 통신, cross origin 가능
    -  BroadCastChannel: 양방향 통신, same origin 만 가능, 브로드케스트 함   

### 8/29
- img tag의 srcset 속성
    - 반응형에서 다양한 크기의 이미지를 지원한다.
    ``` 
       <img 
        srcset="images/500.png 500w, images/300.png 300w, images/150.png 150w"
        sizes="(min-width:960px) 500px, (min-width:640px) 300px, 320px" 
        src="images/150.png" 
        alt="gray-box">
     ```
    - srcset: 이미지의 경로, 이미지의 원본 크기 지정
    - size: 반응형 조건, 그에 따른 이미지 크기 지정
    - x,w,size 서술자를 사용한다
        - x: ratio 단위
        - w: 너비로 px 단위
    - [예제](https://www.heropy.dev/p/5Gl8hX)

### 8/8
- frontend 오류 탐지 툴
    - Sentry: https://tech.kakaopay.com/post/frontend-sentry-monitoring/ 

### 5/8
- React19 hook (아직 실험적 문법)
    - use (promise): 프로미스 전달시 해당 프로미스가 해결 될 때까지 react는 중단됨
    - use (context): useContext와 유사하지만 루프 및 조건문 내에서 호출 가능
    - useFromState: <form> 의 action 프로퍼티에 함수 전달 가능, 비동기 폼 액션 기능 지원, 폼이 마지막으로 제출됐을 때 액션의 반환 값에 접근 가능
    - useFormStatus: <form> 의 상태 정보, 제출중인지/성공적으로 제출했는지
    - useOptimistic: action이 제출되는 동안 사용자 인터페이스를 optimistically하게 업데이트 가능    


### 4/23
- text color에 linear-gradient 값 주기
``` 
  background: linear-gradient(180deg, #ffffff -20.51%, #c49551 127.45%);
  background-clip: text; /* 배경이 텍스트로 적용되도록 설정 */
  color: transparent; /* 텍스트의 실제 색상을 투명하게 설정 */
``` 

### 4/15
- 수정되지 않은 파일까지 stash 하기
    - git stash --include-untracked

### 3/15
- Debounce
    -  여러개의 Event 가 발생하고 특정 시간이 지났을 때 마지막 Event를 발생시켜주는 것 (e.g. input box 입력)
- Throttle
    - 여러 Event가 발생했을 때 특정 주기마다 Event를 발생시켜 주는것 (e.g. 무한 스크롤) 

### 2/27
- transient props: $isVisible 과 같은 props 으로 styled component에 transient props 로 넘겨주면 DOM 에서 인식하지 않는다.

### 2/22
- JS Closure
    - 함수안에 내부함수를 정의한 형태로
    - 사용 Case: 정보 캡슈화, 상태유지(e.g. useState), 전역 변수 사용 억제 등을 위해 사용한다.
    - 함수가 만들어진 환경을 기억한다.
    - (클로저로 js 의 queue 를 구현할수도 있지 않을까?
- [CSS] text-wrap: balance;
    - wrap 된 text의 갯수를 비슷하게 맞춰줌
- [CSS] scrollbar-gutter: stable both-edges
    - scroll bar를 위한 공간 남겨둠
- [CSS] aspect-ratio: 16/9
    -  16:9 비율로 화면에 보여줌
- [CSS] object-fit: cover
    - 이미지가 요소를 덮도록 크기가 조정. 

### 2/15
- 백그라운드가 항상 중앙 정렬하기(화면 사이즈 줄여도 가운데 위주로 보임) background-position: center;
- background: url(...) 설정 후에 background-position 을 지정해야지 동작함.

### 2/6
- 알림 서비스 구현시 통신 방식
    - SSE: Server -> Client로 데이터 전달, HTTP 프로토콜 그대로 이용 가능함
    - websocket: 양방향 통신 

### 1/10
- absolute 속성 가운데 정렬하기
    - transform: translate(-50%,0);
    - left: 50%; 

## 2023
### 1/18
- SWR(stale while revalidate)
    - React Query 와 유사함
    - 캐시로 데이터를 반환 후, fetch 요청을 하고 최종적으로 최신화 된 데이터를 가져올 수 있다.
    - 페이지에 다시 포커스 하거나 탭을 전환할 때 SWR 은 자동으로 데이터를 갱신한다.
    - const { data, error, isValidating, mutate } = useSWR(key, fetcher, options)  형태로 사용
        - mutation 사용시 optimistic UI 사용이 가능하다. (e.g. 좋아요 버튼 클릭시 좋아요에 불이 들어오고 난 후 서버로 요청이 갔다옴)
    - TODO) Slack clone coding 계속하기
### 1/30
- animation, transition, keyframe
    - TODO) animation을 이용한 미니게임 
### 2/9
- docType
    - 브라우저에게 문서형식을 알려준다.  (HTML이 어떤 버전으로 작성 되었는지 미리 선언한다.)
    - 2가지 용도
        - 표준모드 선언: 엄격모드, 표준모드, 비표준모드, 거의표준모드
        - HTML 버전 선언
### 2/13
- Svelte
    - virtual dom 사용하지 않는다.
    - 적은 코드로 구혀 ㄴ가능하고 이로 인한 유지보수성이 좋다.
### 2/14
- refresh token 의 의미가 있는가?
    - refresh token, access token 관련해서 TD 님이랑 의견을 나눔
    - refresh token 또한 결국 browser 쪽에 저장해야하고 refresh token을 이용해 access token을 발급 받아야하는데 보안상 의미가 있는가? 
    - 현재는 access token 만으로 cookie에 저장, clinet 의 sign on 상태에서 token을 다시 갱신해버림
    - 결론: access token은 필수지만 refresh token은 선택적이다. 개발하고자하는 프로젝트의 성격마다 refresh token을 도입 유무를 결정해야한다. 
    - 두가지 token이 꼭 필요한가를 TD님이 chat GPT 에게 물어봤는데 다음과 같이 답변을 줬다.
``` 
Oauth2 인증할때 access token과 refresh token이 필수야?

일반적으로 OAuth2 인증 시 access token은 필수이며, refresh token은 선택 사항입니다. 
Access token은 인증된 사용자를 대신하여 API 또는 서비스에 대한 액세스를 제공하는 데 사용되며, 일반적으로 짧은 유효 기간을 갖습니다. 
반면, refresh token은 액세스 토큰이 만료될 때 새로운 액세스 토큰을 얻기 위해 사용될 수 있습니다.따라서, access token만 사용해도 
인증 및 권한 부여를 수행할 수 있지만, 보안을 높이기 위해 더 긴 유효 기간을 가진 refresh token을 사용할 수도 있습니다. ```
``` 

### 2/16
- PWA (Progressive Web App)
    - 모바일 앱 + 웹 기술의 결합이다.
    - 표준을 준수하는 브라우저를 사용하는 어떠한 플랫폼에서라도 동작하도록 고안되었다.
    - 네이티브 앱은 해당 플랫폼에 맞는 구현 기술을 익혀야하지만 PWA 를 사용하면 통합해서 개발 가능하다.
    - PWA는 별도의 빌드/배포 과정이 필요없다. 모든 웹 페이지를 대상으로 가능하다.

### 2/27
- .gitattributes 파일
    - 디렉토리와 파일 단위로 다른 설정을 적용 할 수 있는데 이렇게 경로별로 설정하는 것을 git attribute 라고 부른다.
    - 참고자료: https://git-scm.com/book/ko/v2/Git%EB%A7%9E%EC%B6%A4-Git-Attributes
    
### 2/28
(window로만 작업하던 환경에서 mac환경으로 작업하려니 몇가지 문제가 발생했음)
- mac os로 443 port 사용시 sudo 로 실행해줘야함
    - sudo npm 으로 start 해주면 나중에 꺼줘도 해당 port 가 계속 열려있는 문제가 발생함
    - 해결) yarn 으로 실행 시 위의 사항 해결됨
    - 참고자료: github.com/npm/cli/issues/3110   아래쪽
- mac host 이름 변경해주기
    - /private/etc/hosts 파일 수정하기 
    
### 3/2
- Next.js v13 개선점
    - hydration 부분 개선됨
    - Turbopack (webpack을 대체해 사용, 700배 빠른 Rust 기반임) 사용으로 빌드 속도가 4배 빨라짐
    - app/  디렉토리 구조로 변경 (기존 pages/)
        - layouts.js: 레이아웃 처리
        - loading.js: 로딩 상태 
        - 서버 컴포넌트
    - next/image: layout switching 자동으로 해준다.
    - next/font: layout switching 자동, 구글 폰트가 내장되어 있다.
    - React 18에서 업데이트된 기능에 맞게 추가함: Streaming, Transitions, Suspense.
- Zunstand 상태관리 라이브러리
    - Redux 와 같은 Flux 구조
    - 보일러플레이트 간단함
    - immer 개념 사용
    - Context Api의 불필요한 렌더링 방지
    - Redux Devtools 를 사용해 디버깅이 쉽다. 

### 3/3
- Next.js prerendering 기능  
    - v12
        - getServerSideProps: SSR 기능 (데이터가 계속 바껴야할 떄 사용함)
        - getStaticProps/getStaticPaths: SSG 사용시 사용함
    - v13
        - 추가적으로 ISR (Incremental Static Regeneration) 사용가능
        
### 3/7
- Next 13버전이 beta 버전 (app/ 디렉도리 활용), stable 버전(font, image, script component 업데이트 내역)으로 나눠서 가이드함
- css 의 direction을 rtl 으로 설정해주면 오른쪽-> 왼쪽 순서로 페이지가 구성된다 (기본: ltr)
   
         
### 3/13
- n*n box layout을 구성하기 위해 flex-wrap, flex-basis, flex-shrink, flex-grow 사용 후 각 item 에 max-width 값을 주자

### 3/17
- Nest.js
    - express, typeorm 을 wrapping함
    - spring 구조로 되어있다.
    - module, controller, service 구조  (controller 가 제공하는 것 많음)
    - module: dependency 관리
    - controller: 사용자 접근에 대한 endpoint 관리
    - service: business logic 담당
    - app.module: db type 넣어줌, 
- TypeORM 이란?
    - TypeORM(Real DB, 실제 db를 사용한다) vs PrismaDB(Cloud 주소로 data를 web에 넣고 뺀다)
    - TypeORM 호환에 대한 장점이있다. (DB가 어떤 것으로 선언되었는지에 상관 없이 js로 db에 접근 가능하다)
    
### 3/27
- next.js 에서 error 다루기
- SSR: pages/500.js 와 같이  ${statusCode}.js 파일을 만든다
- CSR: error boundaries 사용

### 3/28
 - next.js SSR 에서 getServerSideProps 의 캐싱 가능
 ```
 export async function getServerSideProps({ req, res }) {
  res.setHeader(
    'Cache-Control',
    'public, s-maxage=10, stale-while-revalidate=59'
  )

  return {
    props: {},
  }
}
 ```
 
 
 ### 3/28
 - next.js dev, product 모드일 때 다른점 더 확인
 - https://nextjs.org/learn/foundations/how-nextjs-works/rendering
 
 ### 4/24
 - TODO) webpack, rollup 비교 
 
 ### 4/26
 - AI 검색엔진 : https://yozm.wishket.com/magazine/detail/1944/

 ### 6/13
 - Next Script component 사용시 strategy의 lazyOnload 옵션을 사용하면 script 로 가져오는 UI 가 깜빡거리는 현상 fix 가능 
    (defaut: afterInteractive, optiosn: beforeInteractive, lazyOnload, worker)

 ### 6/23
 - Next.js 에서 i18n 사용시 next-i18next 을 사용해야하고 SSR 에서 serverSideTranslations 을 사용해 context.locale 정보를 넘겨줘야함

### 7/23
- StyledComponent 에서 mixin 사용하기
- e.g. 자주 사용하는 flex box 적용
  ```
  // theme.ts 에서 정의
  export const mixins = {
  // flex
  flexBox: (direction = 'row', align = 'center', justify = 'center') => `
    display: flex;
    flex-direction: ${direction};
    align-items: ${align};
    justify-content: ${justify};
  `,

  // style 사용하는 쪽에서

  ${({ theme })} => theme.flexBox('row', 'center', 'flex-start');
  ```

### 9/14
특정 페이지id 값으로 scroll이동 처리
```
  useEffect(() => {
    if (typeQuery === 'mySpot') {
      const targetElement = document.getElementById('mySpotClass')
      if (targetElement) {
        targetElement.scrollIntoView({ behavior: 'smooth' })
      }
    }
  }, [typeQuery])
```

### 10/18
- react의 use 라는 hook이 실험적 문법으로 나옴 https://react.dev/reference/react/use

### 11/14
- grid layout으로 card item 갯수 별로 배치하기
```
    display: grid;
    grid-template-columns: repeat(4, 1fr); // 4칸짜리 만들기
    /* repeat() 함수 사용법 */
    grid-template-rows: repeat(2, 1fr);         /* 1fr 1fr */
    grid-template-columns: repeat(3, 1fr 2fr);  /* 1fr 2fr 1fr 2fr 1fr 2fr */
```


### 11/16
- offsetHeight, scrollHeight 차이점
    - offsetHeight : 요소의 높이. 패딩, 스크롤 바, 테두리(Border)가 포함. 마진은 제외된다.
    - scrollHeight : 요소에 들어있는 컨텐츠의 전체 높이
      (ellipse로 ... 후 내용 hidden 시 사용했었음)

### 11/28
- 안드로이드 웹뷰로는 html textarea의 maxLength가 적용이 안됨
    - 관련 이슈: https://stackoverflow.com/questions/11754575/jelly-bean-webview-not-working-well-with-html-maxlength-attribute-for-text-box
 
### 12/18
- URI, URL, URN 차이점
    - URI (URL, URN을 포함, 모든 path이다.)
        - e.g. http://torang.co.kr/user?id=107
    - URL 
        - e.g. http://torang.co.kr/user/107
    - URN
        - e.g. torang.co.kr/index
 
- Monorepo 구축 도구인 Lerna 종료, 대신 Nrwl 을 사용하면 됨
    - https://github.com/lerna/lerna/issues/3121
    - https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html
 
### 12/26
- HTML tag 정리
    - b: bold체 지정.
    - strong: bold체 + 중요한 tag 사용시 사용함.
    - i:  이텔릭체 지정.
    - em: 이텔릭체 + emphasized (강조, 중요한)  텍스트를 지정한다.
    - mark: highlighted text를 지정.
    - del:  deleted text 지정
    - ins: inserted text 지정 (underlined)
    - sub: 아래에 쓰인 text
    - sup: 위에 쓰인 text
    - p: paragraphs 단락 지정.
    - pre: 작성된 그대로 보여진다. preformatted(형식화된) text 이다.
    - hr: 수평 줄 삽입
    - q: 짧은 인용문 e.g. “내용”
    - blockquote: 긴 인용문 블록을 지정한다.   
