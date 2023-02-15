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
