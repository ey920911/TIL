# TIL
Today I Learned 

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
- URI (URL, URN을 포함, 모든 path이다.)
    - e.g. http://torang.co.kr/user?id=107
- URL 
    - e.g. http://torang.co.kr/user/107
- URN
    - e.g. torang.co.kr/index
