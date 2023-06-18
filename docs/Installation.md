### Installation

시스템 요구 사항:

- Node.js 16.8 이상
- macOS, Windows (WSL 포함), Linux를 지원합니다.

***

#### Automatic Installation

`create-next-app`을 사용하여 새로운 Next.js 앱을 만드는 것을 권장합니다. 이는 모든 설정을 자동으로 해줍니다. 프로젝트를 생성하려면 다음을 실행하세요:

```
Teminal

npx create-next-app@latest
```

설치과정에서 다음의 프롬프트가 표시됩니다.

```
Terminal

What is your project named? my-app
Would you like to use TypeScript with this project? No / Yes
Would you like to use ESLint with this project? No / Yes
Would you like to use Tailwind CSS with this project? No / Yes
Would you like to use `src/` directory with this project? No / Yes
Use App Router (recommended)? No / Yes
Would you like to customize the default import alias? No / Yes
```

Next.js는 이제 TypeScript, ESLint, 
그리고 Tailwind CSS 설정을 기본으로 제공합니다.
또한 애플리케이션 코드에 src 디렉토리를 사용할 수도 있습니다.

프롬프트 이후, create-next-app은 프로젝트 이름으로 된 
폴더를 생성하고 필요한 dependency를 설치합니다.

```
Good to know: 

새로운 프로젝트에서 Pages Router (https://nextjs.org/docs/pages)를 
사용할 수는 있지만, 

React의 최신 기능을 활용하기 위해 App Router로 
새로운 애플리케이션을 시작하는 것을 권장합니다.
```

***

#### Manual Installation

수동으로 새로운 Next.js 앱을 만드려면, 필요한 패키지를 설치하세요

```
Terminal

npm install next@latest react@latest react-dom@latest
```

package.json 파일을 `scripts:`에 아래와 같이 추가하세요

```
package.json

{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

이러한 스크립트는 애플리케이션 개발의 다른 단계를 나타냅니다:

```
dev: 개발 모드에서 `Next.js`를 실행하기 위해 next dev를 실행합니다.
build: 애플리케이션을 프로덕션 용도로 빌드하기 위해 `next build`를 실행합니다.
start: Next.js 프로덕션 서버를 시작하기 위해 `next start`를 실행합니다.
lint: Next.js의 내장 ESLint 구성을 설정하기 위해 `next lint`를 실행합니다.
```

##### Create the app folder

그 다음으로, `app` 폴더를 생성하고 `layout.tsx`와 `page.tsx` 파일을 추가해주세요. 이 파일들은 사용자가 애플리케이션의 루트를 방문할 때 렌더링됩니다.

![app-getting-started.avif](../assets/app-getting-started.avif)