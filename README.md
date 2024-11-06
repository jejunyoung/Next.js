2024/11/06 수업내용

2024/10/06 수업내용

# Next.js

## 202030329\_제준영

[1과](#1과)  
[2과](#2과)  
[3과](#3과)  
[4과](#4과)  
[5과](#5과)  
[6과](#6과)  
[7과](#7과)

## 7과

### UI 라이브러리

- UI라이브러리, 프레임워크, 유틸리티는 필수 X
- 생산성 향상 및 UI 일관성
- Chakra UI
- ~~Tailwind Css~~ Tailwind UI
- Headless

### Chakra UI

- 버튼, 모달, 입력등 다양한 내장 컴포넌트 제공
- dark mode, light mode 지원
- 타입스크립트로 작성되여 있음

### ~~Tailwind CSS~~ Tailwind UI

- 리액트 컴포넌트을 제공하지 않음
- ~~CSS 클래스만 제공한다~~
- Next.js는 TailwindCSS을 많이 사용
- 변수값을 조정하여 개성있는 디자인을 만들 수 있음
- 클래스 이름이 너무 길다
- dark mode, light mode 지원
- ~~Headless와 같이 사용한다~~ 지금은 꼭 같이 사용이 강요가 아니다
- ```
   <p className="mx-auto mt-2 max-w-lg text-balance text-center text-4xl font-semibold tracking-tight text-gray-950 sm:text-5xl">
  ```

## 6과

### Styled JSX

- Styled in JS
- CSS를 JS에서 사용
- globals로 적용해서 사용 할 순 있지만 사용시 주의
- 자동 완성 기능을 사용 할 수 없음 (확장 기능으로 vs에서도 사용 가능)
- 리액트 하이드레이션이 끝나면 css를 다시 생성해야해서 느리다
- next.js 내장 컴포넌트

### CSS 모듈

- 이름.module.css
- Styled JSX의 단점을 보안하기 위해 사용
- next.js 내장 컴포넌트

## 5과

### 디렉토리 구조 구성

- 특정 파일과 디렉토리 지정된 위치
- node modules: 의존성 패키지를 설치하는 디렉토리

### 아토믹 디자인

- atomes: 가장 기본직인 컴포넌트
- molecules: atomes에 속한 컴포넌트을 조합하는 곳
- organisms: atomes, molecules을 섞어서 만들는 것
- templates: 위에 모든 컴포넌트를 사용하여 페이지 구성

### 유틸리티 구성

- 컴포넌트로 만들필요가 없는 것
- 로그파일

### 데이터 불러오기

## 4과

[Layout](#layout)  
[Page Layout](#page-layout)  
[App Layout](#app-layout)

### Layout

- 실행 할때 고전된 레이아웃

### Page Layout

#### app.jsx

- app.jsx 가 가장 먼저 실행되는 파일

  ```
    import "@/styles/globals.css";

    export default function App({Component, pageProps}){
      return <Component{...pageProps} />;
    }
  ```

- Component, pageProps은 내가 요청한 페이지
- 데이터가 없으면 ({})로 반환

#### document.jsx

- document.jsx는 app.jsx다음에 실행되는 파일

  ```
    import { Html, Head, Main, NextScript } from "next/document";

    export default function Document() {
      return (
        <Html lang="en">
        <Head />
        <body>
          <Main />
          <NextScript />
        </body>
      </Html>
      );
    }
  ```

- 이벤트나 css는 이것에 선하지 않는다

### App Layout

- app디렉토리 아래 layout.jsx 위치함
- layout.jsx는 app.jsx, document.jsx 대체
- 삭제해도 실할할때 자동 생성

  ```
    import { Inter } from "next/font/google";
    import "./globals.css";

    const inter = Inter({ subsets: ["latin"] });

    export const metadata = {
      title: {
        default: "Hello Next.js", //타이틀이 없으면
        template: "daelim: %s" // 타이틀이 있으면 daelim: 타이틀 이름
        },
      description: "Generated by create next app",
    };

    export default function RootLayout({ children }) {
      return (
        <html lang="ko">
          <body className={inter.className}>{children}</body>
        </html>
      );
    }
  ```

- 타이틀을 다 다르게 하고 싶으면 타이틀 이름이 필요한 곳에 가져가서 사용한다

  ```
    app/
      about/
        - page.jsx
        - layout.jsx
      layout.jsx
  ```

  ```
    export const metadata = {
      title: "Create Next App",
    };

    export default function Layout({ children }) {
      return (
        <html lang="en">
          <body>{children}</body>
        </html>
      );
    }
  ```

  ### static resoure

- 이미지 CLS 문제 해결
- lazy loading 기술
- PlaceHolder 제공

### Image Component -local

- public 에 저장

### image component - romote

- next.config.mjs에 설정
  ```
    images: {
      remotePatterns:[
        {
          protocol:'htpps',
          hostname: 'cdn.pixabay.com',
        }
      ]
    }
  ```

## 3과

[라우팅 시스템](#라우팅-시스템)  
[동적 라우팅](#동적-라우팅)

### 라우팅 시스템

- ~~React는 React 라우팅을 사용~~
- Next는 파일시스템 기반 페이지 라우팅 사용
- page는 js,jsx,ts,tsx파일의 이름으로 라우팅
- 라우팅시 디렉토리 안쪽에 만들어야 한다
  ```
  pages/
      - index.jsx
      - constact.jsx
  ```
- next는 디렉토리 이름으로 라우팅
  ```
    app/
      - page.jsx
      - constact/
        - page.jsx
  ```
- 라우팅에 기본 세그먼트를 만들고 싶으면 [slug].jsx 파일이
  ```
    pages/
      -bar/
        - index.jsx
        - [foo].jsx
  ```
- 라우팅에 포갈적 세그먼트를 만들고 싶으면[...slug].jsx 파일이 (가져올때 배열로 가져온다)
  - 값이 없으면 404 오류를 출력
  ```
    pages/
      -bar/
        - index.jsx
        - [...foo].jsx
  ```
- 라우팅에 포갈적 세그먼트(언디파인) 만들고 싶으면[[slug]].jsx 파일 (가져올때 배열로 가져온다)
  - 값이 없어도 오류가 없음
  ```
    pages/
      -bar/
        - index.jsx
        - [[...foo]].jsx
  ```
- 동적 라우팅은 중첩이 가능

### 동적 라우팅

- ```
    export default function FooId(props) {
    return (
      <>
        <h1>
          Foo {props.params.fooId} {props.searchParams.country}
        </h1>
      </>
    );
  }
  ```

## 2과

[바벨 플로그인](#바벨-플로그인-nextjs-12-이후-지원-중지)  
[플로그인 설치](#플로그인-설치)  
[렌더링 전략](#렌더링-전략)  
[SSR](#ssr)  
[SSG](#ssg)  
[api 사용하기](#api사용하기)

### 바벨 플로그인 (next.js 12 이후 지원 중지)

- 파이프라인은 공식적으로 채택되지 않은 연산자
- 사용하기 위해 바벨 플로그인 설치

```
  npm install --asve-dev @babel/pugin-proposal-pipeline-operator @babel/core
```

### 플로그인 설치

- 지워하지 않는 기능 , 채택되지 않는 기능을 사용하기 위해서는 플로그인 설치

```
 npm install ...
```

### 렌더링 전략

- next.js는 Gatsby 서버 사이드 렌더링 둘 다 가능하다

### SSR

- 쿠키 관리, 주요 API, 데이터 검증등 같은 작업을 서버에서 처리
- 데이터를 클라이언트에 노출할 필요가 없다
- 클라이언트 환경이 자바스크립트를 사용하지 못하거나 오래된 브라우저를 사용하더라도 서비스를 제공할 수 있다

### SSG

- 정적 페이지는 단순 html 파일이므로 CDN을 통해 파일 제공
- 페이지를 요청해도 클라이언트나 서버가 무언가를 처리할 필요가 없다
- 외부 API룰 호출, 데이터 베이스 접속, 보호해야 할 데이터에 접근 할 일이 없다

### api사용하기

- ```
    let data = await fetch("https://api.vercel.app/blog");
    let posts = await data.json(); //json형테의 데이터를 가져올때 사용
  ```
  ```
    return (
    <ul>
      {posts.map((post) => (
        <li key={post.id}>
          <div>{post.id}</div>
          <div>{post.title}</div>
          <div>{post.content}</div>
          <div>{post.author}</div>
          <div>{post.date}</div>
        </li>
      ))}
    </ul>
  );
  ```
-

## 1과

[Next.js](#nextjs-1)  
[서버 사이드 렌더링(SSR)](#서버-사이드-렌더링)  
[정적 사이드 렌더링(SSG)](#정적-사이드-렌더링)  
[증분 정적 재생성(ISR)](#증분-정적-재생성)  
[자동 폴리핀](#자동-폴리필)

### Next.js

- 리액트를 더 편하게 사용하기 위해 사용하는 자바스크립트 웹 프레임워크
- 리액트가 제공하지 않는 여러가지 기능을 제공한다

### Next,js에서 제공하는 기능들

- 코든 분할
- 파일 기반의 라우팅 기능
- 경로 기반 프리페칭
- 서버 사이드 렌더링(SSR)
  - 지금은 리액트에서도 사용할 수 있지만 사용하기 힘들다
- 정적 사이드 렌더링(SSG)
- 증분 정적 재생성(ISR)
- 자동 폴리필
- 타입 스크립트 제공
- 이미지 최적화
- 다국어 지원

### 서버 사이드 렌더링

- 검색에 힘듬
- 실시간 렌더링으로 계속 변하는 상황에 사용

### 정적 사이드 렌더링

- 전체를 올려서 속도를 빠르지만 수정 불가

### 증분 정적 재생성

- 주기적으로 한번 렌더링
- 정적 사이드 렌더링을 주기적으로 반복

### 자동 폴리필

- 자동으로 최신 버전으로 만들건 구형으로 변환할 수 있도록 해준다

### 이미지 최적화

- JPS,PNG 등을 자동으로 webp로 변환해준다
  - webp를 크기가 작아서 사용하기 좋다
- 플레이스 홀더(이미지 대기화면) 자동 생성
