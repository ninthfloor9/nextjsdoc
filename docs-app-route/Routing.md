### Routing Fundamentals

모든 애플리케이션의 기본 구조는 라우팅입니다. 이 페이지에서는 웹의 라우팅에 대한 기본 개념과 Next.js에서 라우팅을 처리하는 방법을 소개합니다.

***

#### Terminology

먼저, 문서 전체에서 다음 용어들이 사용될 것입니다. 간단히 참고해주세요:

<img src="../assets/terminology-component-tree.avif" width=auto, height=auto>

- 트리(Tree): 계층 구조를 시각화하는 데 사용되는 규칙입니다. 예를 들어, 부모 및 자식 컴포넌트로 구성된 컴포넌트 트리, 폴더 구조 등이 있습니다.

- 서브트리(Subtree): 새로운 루트(첫 번째)에서 시작하여 마지막(잎)까지 이어지는 트리의 일부입니다.

- 루트(Root): 트리 또는 서브트리에서 첫 번째 노드로, 루트 레이아웃과 같은 역할을 합니다.
잎(Leaf): 자식이 없는 서브트리의 노드입니다. 예를 들어 URL 경로에서의 마지막 segment를 의미합니다.

***

#### The `App` Router

Next.js 13 버전에서, Next.js는 React Server Components를 기반으로 한 새로운 App Router를 도입했습니다. 이 App Router는 공유 레이아웃, 중첩 라우팅, 로딩 상태, 에러 처리 등을 지원합니다.

App Router는 app이라는 새로운 디렉토리에서 작동합니다. app 디렉토리는 페이지 디렉토리와 함께 작동하여 점진적으로 채택할 수 있습니다. 이를 통해 기존 동작을 유지하면서 일부 route를 새로운 동작으로 전환할 수 있습니다. 애플리케이션이 페이지 디렉토리를 사용하는 경우, 이전 동작을 위한 페이지 라우터 문서도 참조하십시오.

```
Good to know: 

App Router는 Pages Router보다 우선합니다. 
디렉토리 간의 route는 동일한 URL 경로로 해석되지 않아야 하며, 
충돌을 방지하기 위해 빌드 시간 오류가 발생합니다.
```

<img src="../assets/next-router-directories.avif" width=auto, height=auto>

기본적으로, app 디렉토리 내부의 컴포넌트는 React Server Components입니다. 
이는 성능 최적화를 위한 것으로, 쉽게 채택할 수 있도록 해주며, 
Client Components도 사용할 수 있습니다.

```
Recommendation:
Server Components에 익숙하지 않은 경우 Server and Client Components 페이지를 확인해보세요.
(https://nextjs.org/docs/getting-started/react-essentials)
```

***
#### Roles of Folders and Files

Next.js는 파일 시스템을 기반으로 하는 라우터를 사용합니다. 여기에서:

- 폴더는 route를 정의하는 데 사용됩니다. route는 루트 폴더부터 페이지.js 파일이 
포함된 최종 리프 폴더까지의 파일 시스템 계층 구조에 따른 중첩된 폴더 경로입니다. 
Defining Routes를 참조하세요.(https://nextjs.org/docs/app/building-your-application/routing/defining-routes)

- 파일은 route segment에 대해 표시되는 UI를 생성하는 데 사용됩니다. 
special files 을 참조하세요. (https://nextjs.org/docs/app/building-your-application/routing#file-conventions)

***

#### Route Segments

각 폴더는 route segment 나타냅니다. 
각 route segment 는 URL 경로의 해당 segment와 매핑됩니다.

<img src="../assets/route-segments-to-path-segments.avif" width=auto, height=auto>


***

#### Nested Routes

Nested Routes를 만들려면 폴더를 서로 중첩시킬 수 있습니다. 예를 들어, `app` 디렉토리 안에 두 개의 새로운 폴더를 중첩함으로써 새로운 `/dashboard/settings` route를 추가할 수 있습니다.

`/dashboard/settings` route는 세 개의 segment로 구성됩니다:

- / (Root segment)
    - dashboard (segment)
    - settings (leaf segment)

***

#### File Conventions

Next.js는 특정 동작을 가진 UI를 생성하기 위해 일련의 특수 파일을 제공합니다.

- layout: segment와 해당 자식들을 위한 공유 UI
- page: route의 고유한 UI 및 route를 공개적으로 접근 가능하게 만듦
- loading: segment와 해당 자식들을 위한 로딩 UI
- not-found: segment와 해당 자식들을 위한 찾을 수 없음(UI)
- error: segment와 해당 자식들을 위한 에러 UI
- global-error: 전역 에러 UI
- route: 서버 사이드 API 엔드포인트
- template: 특수화된 재렌더링 레이아웃 UI
- default: 병렬 route의 대체 UI

```
Good To know:

Special File 에는 .js, .jsx 또는 .tsx 파일 확장자를 사용할 수 있습니다.
```

***

#### Component Hierarchy

Route Segment의 특수 파일에 정의된 React 컴포넌트는 특정한 계층 구조로 렌더링됩니다:

- `layout.js`
- `template.js`
- `error.js` (React error boundary)
- `loading.js` (React suspense boundary)
- `not-found.js` (React error boundary)
- `page.js` or nested `layout.js`

<img src="../assets/file-conventions-component-hierarchy.avif" width=auto, height=auto>

nested route 에서 segment의 컴포넌트는 부모 segment의 컴포넌트 안에 중첩됩니다.

<img src="../assets/nested-file-conventions-component-hierarchy.avif" width=auto, height=auto>

***

#### Colocation

자신의 파일(예: 컴포넌트, 스타일, 테스트 등)을 앱 디렉터리 내의 폴더에 함께 배치하는 옵션이 제공됩니다.
폴더는 경로를 정의하지만, page.js 또는 route.js에서 반환된 내용만 공개적으로 접근할 수 있습니다.

<img src="../assets/project-organization-colocation.avif" width=auto, height=auto>

***

#### Server-Centric Routing with Client-side Navigation

페이지 디렉터리와는 달리 App Router는 클라이언트 측 라우팅을 사용하는 것이 아니라 서버 중심의 라우팅을 사용하여 서버 구성 요소와 서버에서의 데이터 가져오기와 일치시킵니다. 서버 중심의 라우팅을 사용하면 클라이언트는 경로 맵을 다운로드할 필요가 없으며, 서버 구성 요소에 대한 동일한 요청을 사용하여 경로를 조회할 수 있습니다. 이 최적화는 모든 애플리케이션에 유용하지만, 많은 경로를 가진 애플리케이션에 더 큰 영향을 미칩니다.

라우팅은 서버 중심이지만, 라우터는 링크 컴포넌트(Link Component)를(https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#link-component) 사용하여 클라이언트 측 네비게이션을 구현합니다. 이는 싱글 페이지 애플리케이션(Single-Page Application)의 동작과 유사합니다. 즉, 사용자가 새로운 경로로 이동할 때 브라우저는 페이지를 다시로드하지 않습니다. 대신 URL이 업데이트되고 Next.js는 변경된 세그먼트만 렌더링합니다.(https://nextjs.org/docs/app/building-your-application/routing#partial-rendering)

또한, 사용자가 앱을 탐색하는 동안 라우터는 React 서버 구성 요소 페이로드의 결과를 클라이언트 측 메모리 캐시에 저장합니다. 이 캐시는 경로 세그먼트별로 분할되어 임의의 수준에서 무효화가 가능하며, React의 동시 렌더링을 통해 일관성을 보장합니다. 이는 특정 경우에 이전에 가져온 세그먼트의 캐시를 재사용할 수 있어 성능을 더욱 향상시킵니다.

링크(Linking) 및 탐색(Navigating)에 대해 더 자세히 알아보려면 추가 정보를 확인하세요.
(https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating)

***

#### Partial Rendering

Next.js에서 형제 라우트 간 이동(예: 아래의 /dashboard/settings와 /dashboard/analytics) 시에는 변경되는 route의 레이아웃과 페이지만을 가져와 렌더링합니다. subtree의 segment 위에 있는 요소는 다시 가져오거나 다시 렌더링하지 않습니다. 이는 레이아웃을 공유하는 route에서 형제 페이지 간에 이동할 때 레이아웃이 유지되는 것을 의미합니다.

<img src="../assets/partial-rendering.avif" width=auto, height=auto>


부분 렌더링을 사용하지 않을 경우, 각 탐색마다 전체 페이지가 서버에서 다시 렌더링됩니다. 업데이트되는 segment만 렌더링하면 전송되는 데이터 양과 실행 시간이 감소하여 성능이 향상됩니다.

***

#### Advanced Routing Patterns

App Router은 더 고급 라우팅 패턴을 구현하는 데 도움이 되는 일련의 규칙도 제공합니다. 이러한 패턴은 다음과 같습니다:

- 병렬 라우트(Parallel Routes): 독립적으로 탐색할 수 있는 두 개 이상의 페이지를 동시에 동일한 뷰에 표시할 수 있게 해줍니다. 이를 사용하여 자체 하위 네비게이션이 있는 분할 뷰에 사용할 수 있습니다. 예: 대시보드(Dashboards).
(https://nextjs.org/docs/app/building-your-application/routing/parallel-routes)

- 라우트 가로채기(Intercepting Routes): 특정 라우트를 가로채고 다른 라우트의 문맥(context)에서 표시할 수 있게 해줍니다. 현재 페이지의 문맥(context)을 유지하는 것이 중요한 경우에 사용할 수 있습니다. 예: 한 가지 작업을 편집하면서 모든 작업을 볼 수 있는 경우 또는 피드(feed)에서 사진을 확대하는 경우.
(https://nextjs.org/docs/app/building-your-application/routing/intercepting-routes)

이러한 패턴을 사용하면 더 풍부하고 복잡한 UI를 구축할 수 있으며, 소규모 팀과 개발자에게는 예전에는 복잡했던 기능을 구현할 수 있는 기회를 제공합니다.
