---
layout: post
title: Angular Routing - <strong>Basics</strong>
subtitle: 라우팅과 내비게이션
categories: angular
section: angular
description: 단일 페이지 어플리케이션(Single Page Application, SPA)은 모던 웹의 패러다임이다. SPA는 기본적으로 단일 페이지로 구성되며 기존의 서버 사이드 렌더링과 비교할 때, 배포가 간단하며 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다는 장점이 있다.
---

* TOC
{:toc}

![angular Logo](/img/angular-logo.png)

# 1. SPA (Single Page Application)

단일 페이지 어플리케이션(Single Page Application, SPA)은 모던 웹의 패러다임이다. SPA는 기본적으로 단일 페이지로 구성되며 기존의 서버 사이드 렌더링과 비교할 때, 배포가 간단하며 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다는 장점이 있다.

link tag를 사용하는 전통적인 웹 방식은 새로운 페이지 요청 시마다 정적 리소스가 다운로드되고 전체 페이지를 다시 렌더링하는 방식으로 동작하므로 새로고침이 발생된다. 이것은 변경이 필요없는 부분을 포함하여 전체 페이지를 갱신하는 것으로 비효율적이다.

SPA는 웹 애플리케이션에 필요한 모든 정적 리소스를 애플리케이션 최초 기동 시에 한번만 다운로드한다. 이후 새로운 페이지 요청 시, 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신하므로 전체적인 트래픽을 감소할 수 있고, 전체 페이지를 다시 렌더링하지 않고 변경되는 부분만을 갱신하므로 새로고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다.

모바일의 사용이 증가하고 있는 현 시점에 트래픽의 감소와 속도, 사용성, 반응성의 향상은 매우 중요한 이슈이다. SPA의 핵심 가치는 사용자 경험(UX) 향상에 있으며 부가적으로 애플리케이션 속도의 향상도 기대할 수 있어서 모바일 퍼스트(Mobile First) 전략에 부합한다.

모든 소프트웨어 아키텍처에는 trade-off가 존재하며 모든 애플리케이션에 적합한 은탄환(Silver bullet)은 없듯이 SPA 또한 구조적인 단점을 가지고 있다. 대표적인 단점은 아래와 같다.

초기 구동 속도
: SPA는 웹 애플리케이션에 필요한 모든 정적 리소스를 애플리케이션 최초 기동 시에 모두 다운로드하기 때문에 초기 구동 속도가 상대적으로 느리다. 하지만 SPA는 웹페이지보다는 애플리케이션에 적합한 기술이므로 트래픽 감소, 속도, 사용성, 반응성의 향상 등의 장점을 생각한다면 결정적인 단점이라고 할 수는 없다.

SEO(검색엔진 최적화) 문제
: SPA는 서버 사이드 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델(클라이언트 사이드 랜더링 방식)이다. 따라서 SEO는 언제나 단점으로 부각되어 왔던 이슈이다. 하지만 SPA는 정보의 제공을 위한 웹페이지보다는 애플리케이션에 적합한 기술이므로 SEO 이슈는 심각한 문제로 볼 수 없다. Angular 또는 React 등의 SPA 프레임워크(React는 라이브러리로 구분된다)는 서버 사이드 랜더링을 지원하는 SEO 대응 기술이 이미 존재하고 있어 SEO 대응이 필요한 페이지에 대해서는 선별적 SEO 대응이 가능하다.

# 2. Routing

라우팅이란 출발지에서 목적지까지의 경로를 결정하는 기능이다. 애플리케이션의 라우팅은 사용자가 태스크를 수행하기 위해 어떤 화면(view)에서 다른 화면으로 화면을 전환하는 내비게이션을 관리하기 위한 기능을 의미한다. 일반적으로 사용자가 요청한 URL 또는 이벤트를 해석하고 새로운 페이지로 전환하기 위한 데이터를 취득하기 위해 서버에 필요 데이터를 요청하고 화면을 전환하는 일련의 행위를 말한다.

브라우저가 화면을 전환하는 경우는 아래와 같다.

1. 브라우저의 주소창에 URL을 입력하면 해당 페이지로 이동한다.

2. 웹페이지의 링크(a 태그)를 클릭하면 해당 페이지로 이동한다.

3. 브라우저의 뒤로가기 또는 앞으로가기 버튼을 클릭하면 사용자가 방문한 웹페이지의 기록(history)의 뒤 또는 앞으로 이동한다.

AJAX 요청에 의해 서버로부터 데이터를 응답받아 화면을 생성하는 경우, 브라우저 주소창의 URL은 변경되지 않는다. 이는 사용자의 방문 history를 관리할 수 없음을 의미하며, SEO(검색엔진 최적화) 이슈의 발생 원인이기도 하다. **history 관리를 위해서는 각 페이지는 브라우저의 주소창에서 구별할 수 있는 유일한 URL을 소유하여야 한다.**

# 3. Angular Router 개요와 위치 정책(Location strategy)

## 3.1 개요

Angular는 단일 페이지 어플리케이션(SPA)을 위한 클라이언트 사이드 내비게이션 구현 방식으로 Angular 라우터를 제공한다. Angular 라우터는 선언적 방식으로 라우트를 구성하고 라우트에 해당하는 컴포넌트를 매핑한다. 즉, 사용자의 요청 URL을 해석하고 애플리케이션의 뷰를 담당하는 컴포넌트와 연결하는 역할을 한다.

Angular는 사용자의 요청 URL의 패스(path, 경로)와 컴포넌트의 쌍으로 구성된 라우트 설정을 참조하여 뷰를 출력한다. 라우트 설정의 예는 아래와 같다.

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];
```

## 3.2 Location strategy

a 태그의 href 어트리뷰트를 사용하지 않는 AJAX는 URL을 변경시키지 않는다. 따라서 브라우저 주소창의 URL이 변경되지 않는다. 이는 브라우저의 뒤로가기, 앞으로가기 등의 history 관리가 동작하지 않음을 의미한다. 물론 코드 상의 history.back(), history.go(n) 등도 동작하지 않는다. 새로고침을 클릭하면 주소창의 주소가 변경되지 않기 때문에 언제나 첫페이지가 다시 로딩된다. 하나의 주소로 동작하는 AJAX 방식은 SEO 이슈에서도 자유로울 수 없다.

Angular는 2가지의 위치 정책(Location strategy)을 제공한다. 각 페이지는 브라우저의 주소창에서 구별할 수 있는 유일한 URL을 소유하게 된다.

- PathLocationStrategy (HTML5 Histroy API 기반 내비게이션 정책)

- HashLocationStrategy (Hash 기반 내비게이션 정책)

### 3.2.1 PathLocationStrategy (HTML5 Histroy API pushState 기반 내비게이션 정책)

HTML5의 Histroy API pushState 메소드를 사용하는 정책으로 '/service', '/about'와 같이 URL 패스(path)를 기반으로 한다.

```
localhost:4200/service
```

PathLocationStrategy는 **Angular 라우터의 기본 정책**으로 pushState 메소드를 별도로 호출할 필요가 없다. 특별한 이유가 없는 한 사용자가 보다 쉽게 ​​이해할 수 있는 URLPathLocationStrategy를 사용하는 것을 권장한다. 이후 서버 사이드 렌더링을 도입하려면 PathLocationStrategy를 사용하여야 한다.

### 3.2.2 HashLocationStrategy (Hash 기반 내비게이션 정책)

URL 패스에 fragment identifier의 고유 기능인 앵커(anchor)를 사용하는 정책으로 '/#/service', '/#/about'과 같이 [해시뱅](https://blog.outsider.ne.kr/698)을 기반으로 한다. URL이 동일한 상태에서 hash가 변경되면 브라우저는 서버에 어떠한 요청도 하지 않는다. 즉, hash는 변경되어도 서버에 새로운 요청을 보내지 않으며 따라서 페이지가 갱신되지 않는다. HashLocationStrategy는 대부분의 브라우저에서 동작한다.

```
localhost:4200/#/service
```

Hash 기반 내비게이션 정책을 기본으로 사용하려면 루트 모듈의 imports 프로퍼티를 아래와 같이 수정한다.

```typescript
// app.module.ts
...
@NgModule({
  imports: [
    BrowserModule,
    // RouterModule.forRoot(routes)
    RouterModule.forRoot(routes, { useHash: true })
...
```

라우팅 모듈을 사용하는 경우, imports 프로퍼티를 아래와 같이 수정한다.

```typescript
// app-routing.module.ts
...
@NgModule({
  // imports: [RouterModule.forRoot(routes)],
  imports: [RouterModule.forRoot(routes, { useHash: true })],
  ...
})
...
```

# 4. 라우터 구성 요소

이제 라우터를 구성하는 요소에 대해 살펴보도록 하자. 일반적으로 라우터는 아래의 수순으로 작성한다.

1. 라우트 구성
  [Route](https://angular.io/api/router/Route) 인터페이스의 배열(Routes 타입)을 사용하여 요청 URL의 패스와 컴포넌트의 쌍으로 만들어진 라우트를 구성한다.
2. 라우트 등록
  [RouterModule.forRoot](https://angular.io/api/router/RouterModule#forRoot) 또는 [RouterModule.forChild](https://angular.io/api/router/RouterModule#forChild)를 호출하여 라우트 구성이 포함된 모듈을 생성하고 루트 모듈 또는 기능 모듈에 등록한다.
3. 뷰의 렌더링 위치 지정
  라우터가 컴포넌트를 렌더링하여 뷰를 표시할 영역인 `<router-oulet>`을 구현하는 [RouterOutlet](https://angular.io/api/router/RouterOutlet) 디렉티브를 선언하여 컴포넌트 뷰가 렌더링될 위치를 지정한다. RouterOutlet 디렉티브는 루트 컴포넌트 또는 기능 모듈의 컴포넌트에 선언한다.
4. 내비게이션 작성
  [RouterLink](https://angular.io/api/router/RouterLink) 디렉티브를 사용한 HTML 링크 태그를 사용하여 내비게이션을 작성한다.

우선 라우팅 대상인 HomeComponent, ServiceComponent, AboutComponent,NotFoundComponent 컴포넌트를 작성하여 보자.

```typescript
// pages/home.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',
  template: `<div class="home">Home</div>`,
  styles: [`.home { font-size: 2em; padding: 60px; }`]
})
export class HomeComponent {}
```

```typescript
// pages/service.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-service',
  template: `<div class="service">Service</div>`,
  styles: [`.service { font-size: 2em; padding: 60px; }`]
})
export class ServiceComponent {}
```

```typescript
// pages/about.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-about',
  template: `<div class="about">About</div>`,
  styles: [`.about { font-size: 2em; padding: 60px; }`]
})
export class AboutComponent {}
```

```typescript
// pages/not-found.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-not-found',
  template: `<div class="not-found">Not Found</div>`,
  styles: [`.not-found { font-size: 2em; padding: 60px; }`]
})
export class NotFoundComponent {}
```

pages 폴더의 컴포넌트들을 일괄 공개하는 index.ts를 생성한다.

```typescript
// pages/index.ts
export * from './home.component';
export * from './about.component';
export * from './service.component';
export * from './not-found.component';
```

## 4.1 라우트 구성

Angular는 사용자의 요청 URL의 패스(path, 경로)와 컴포넌트의 쌍으로 만들어진 라우트 구성을 참조하여 뷰를 출력한다. 뷰를 출력한다는 것은 라우터 구성의 컴포넌트를 활성화하는 것을 의미한다. 라우트 구성의 예는 아래와 같다.

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];
```

라우트 구성은 [Route](https://angular.io/api/router/Route) 인터페이스를 사용하여 배열로 구성한다. Routes 타입은 [Route](https://angular.io/api/router/Routes) 인터페이스 배열의 [Type Aliase](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)이다.

```typescript
// @angular/router/src/config.d.ts
export declare type Routes = Route[];
```

Route 인터페이스는 @angular/router에 포함되어 있으며 코드는 아래와 같다.

```typescript
// @angular/router/src/config.d.ts
export interface Route {
  path?: string;
  pathMatch?: string;
  matcher?: UrlMatcher;
  component?: Type<any>;
  redirectTo?: string;
  outlet?: string;
  canActivate?: any[];
  canActivateChild?: any[];
  canDeactivate?: any[];
  canLoad?: any[];
  data?: Data;
  resolve?: ResolveData;
  children?: Routes;
  loadChildren?: LoadChildren;
  runGuardsAndResolvers?: RunGuardsAndResolvers;
}
```

Route 인터페이스의 path 프로퍼티는 URL 패스(경로)를 나타내는 문자열이고 component 프로퍼티는 컴포넌트 타입을 나타낸다.

예를 들어 루트 패스 '/'가 요청되면 HomeComponent를 사용하여 뷰를 표시하는 경우, 라우트 구성은 아래와 같다. **패스의 '/'는 기술하지 않는다.**

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent }
];
```

'/service'라는 URL 패스가 요청되면 ServiceComponent를 활성화하고, '/about'라는 URL 패스가 요청되면 AboutComponent를 활성화하여 뷰를 출력하는 경우, 라우트 구성은 아래와 같다.

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent }
];
```

URL 패스에 매칭하는 라우트 정보가 없다면 path 프로퍼티에 '**'를 사용하여 아래와 같이 라우트를 구성한다.

```typescript
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];
```

`path: '**'`는 반드시 라우트 구성의 가장 마지막에 위치하여야 한다. 만약 가장 앞에 위치하면 '**'는 모든 URL 패스에 매칭되어 이후에 선언된 라우트가 적용되지 않는다.

계층적인 라우트를 구성하려면 children 프로퍼티를 사용한다. 예를 들어 URL 패스가 '/todos', '/todos/:id'의 경우, 아래와 같이 라우트를 구성할 수 있다. URL 패스의 두번째 세그먼트 :id는 라우터 파라미터이며 컴포넌트에게 전달되는 값을 할당한다. 예를 들어 '/todos/10'과 같이 값을 할당하면 컴포넌트에게 id값으로 10이 전달된다.

```typescript
const routes: Routes = [
  { path: 'todos', children: [
    { path: '', component: TodosComponent },
    { path: ':id', component: TodoDetailComponent }
  ] }
];
```

data 프로퍼티는 컴포넌트로 전송할 데이터이다. 이 데이터는 컴포넌트로 전송된다.

```typescript
const routes: Routes = [
  { path: 'todos',
    component: TodosComponent,
    data: { content: 'Angular' }
  }
];
```

redirectTo 프로퍼티는 요청을 리다이렉트할 때 사용한다. URL 패스가 정확히 매칭할 때 리다이렉트하려면 pathMatch 프로퍼티를 함께 사용한다. pathMatch 프로퍼티에 문자열 'full'을 설정하면 path 프로퍼티의 패스와 요청 URL 패스 전체가 정확하게 매칭할 때 리다이렉트한다. pathMatch 프로퍼티를 사용하지 않으면 URL 패스의 앞부분만 매칭하여도 리다이렉트한다.

```typescript
const routes: Routes = [
  { path: 'todos', redirectTo: '/todolist' },
  { path: 'todos/:id', redirectTo: '/todolist/:id', pathMatch: 'full' },
];
```

## 4.2 라우트 등록

라우트는 모듈 단위로 구성한다. 따라서 구성된 라우트는 모듈에 등록되어야 한다.

루트 모듈에 라우트 구성을 추가하여 보자. 먼저 라우터 모듈을 import하고 라우트 구성을 추가한다.

```typescript
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
// 라우터 모듈
import { Routes, RouterModule } from '@angular/router';

import { AppComponent } from './app.component';

// 컴포넌트 임포트
import {
  HomeComponent,
  ServiceComponent,
  AboutComponent,
  NotFoundComponent
} from './pages';

// 라우트 구성
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];
...
```

@NgModule 데코레이터의 imports 프로퍼티에 RouterModule.forRoot 메소드를 호출하여 모든 라우트 구성을 포함한 라우터 모듈을 생성하고 루트 모듈에 등록한다. forRoot 메소드는 루트 모듈에 라우트 구성을 등록할 때 사용한다.

```typescript
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
// 라우터 모듈
import { Routes, RouterModule } from '@angular/router';

import { AppComponent } from './app.component';

// 컴포넌트 임포트
import {
  HomeComponent,
  ServiceComponent,
  AboutComponent,
  NotFoundComponent
} from './pages';

// 라우트 구성
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    ServiceComponent,
    AboutComponent,
    NotFoundComponent
  ],
  imports: [
    BrowserModule,
    RouterModule.forRoot(routes), /* 모든 라우트 구성을 포함한 라우터 모듈을 생성하고 루트 모듈에 등록 */
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

위와 같이 라우트 구성을 루트 모듈에 직접 등록할 수도 있으나 라우트 구성이 커지면 라우팅 모듈을 별도 작성하고 그것을 루트 모듈에 등록하는 방식이 유리할 수 있다.

참고로 Angular CLI의 ng new 명령어로 프로젝트를 생성할 때, routing 옵션(--routing)을 추가하면 아래의 내용이 자동 처리된다.

- 라우팅 모듈 app-routing.module.ts를 자동 생성한다.
- app.component.ts에 `<router-outlet></router-outlet>`을 추가한다.
- 루트 모듈 app.module.ts에 라우팅 모듈을 import한다.

라우트 구성을 위한 AppRoutingModule을 아래와 같이 작성한다.

```typescript
// app-routing.module.ts
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';

// 컴포넌트 임포트
import {
  HomeComponent,
  ServiceComponent,
  AboutComponent,
  NotFoundComponent
} from './pages';

// 라우트 구성
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'service', component: ServiceComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: NotFoundComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)], /* 모든 라우트 구성을 포함한 모듈을 생성하고 라우팅 모듈에 추가 */
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

루트 모듈에 라우팅 모듈을 등록한다.

```typescript
// app.module.ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
// 라우팅 모듈 임포트
import { AppRoutingModule } from './app-routing.module';

import { AppComponent } from './app.component';

// 컴포넌트 임포트
import {
  HomeComponent,
  ServiceComponent,
  AboutComponent,
  NotFoundComponent
} from './pages';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    ServiceComponent,
    AboutComponent,
    NotFoundComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule /* 라우팅 모듈 등록 */
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

## 4.3 RouterOutlet

[RouterOutlet](https://angular.io/api/router/RouterOutlet)는 라우터가 컴포넌트를 렌더링하여 뷰를 표시할 영역인 `<router-oulet>`을 구현한 디렉티브로 컴포넌트의 뷰를 렌더링할 위치를 설정한다.

```html
<router-outlet></router-outlet>
```

RouterOutlet 디렉티브는 루트 컴포넌트 또는 기능 컴포넌트(feature component)에서 선언한다.

## 4.4 RouterLink

Angular 라우터를 사용하기 위해 컴포넌트의 템플릿에는 뷰를 전환하기 위한 a 태그의 href 어트리뷰트 대신 [RouterLink](https://angular.io/api/router/RouterLink) 디렉티브를 사용하여 URL 패스를 지정한다. a 태그의 href 어트리뷰트를 사용한다면 서버로 요청이 발생하기 때문이다.

```html
<!-- app.component.ts -->
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/service">Service</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

RouterLink 디렉티브는 자신의 값을 라우터에 전달한다. 라우터는 이를 전달받아 해당 컴포넌트를 활성화하여 뷰를 출력한다.

루트 컴포넌트에 RouterLink 디렉티브를 선언하여 보자.

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <nav>
      <a routerLink="/">Home</a>
      <a routerLink="/service">Service</a>
      <a routerLink="/about">About</a>
    </nav>
    <router-outlet></router-outlet>
  `,
  styles: [`
    nav {
      height: 60px;
      background-color: #4a4c88;
    }
    nav > a {
      line-height: 60px;
      margin: 0 60px;
      color: #fff;
      text-decoration: none;
      font-weight: bold;
      text-transform: uppercase;
      opacity: 0.7;
    }
    nav > a:hover {
      opacity: 1.0;
    }
  `]
})
export class AppComponent {}
```

RouterLink 디렉티브가 선언된 링크를 클릭하면 routerLink의 값이 라우터로 전달된다. 예를 들어 두번째 링크를 클릭하면 '/service'가 라우터로 전달되고 이에 해당하는 SeviceComponent를 활성화하여 RouterOutlet 영역에 뷰를 렌더링할 것이다.

## 4.5 RouterLinkActive

[RouterLinkActive](https://angular.io/api/router/RouterLinkActive) 디렉티브는 현재 브라우저의 URL 패스가 RouterLink 디렉티브에서 **지정한 URL 패스의 트리에 포함**되는 경우, RouterLinkActive에 지정된 클래스명을 DOM에 자동으로 추가한다.

```html
<a routerLink="/service" routerLinkActive="active">Service</a>
```

예를 들어 위의 경우, 현재 브라우저의 URL 패스가 '/' 또는 '/service'인 경우, routerLinkActive 디렉티브가 지정한 active 클래스가 DOM에 자동 추가된다.

브라우저의 URL 패스가 RouterLink 디렉티브에서 **지정한 URL 패스와 정확히 일치**하는 경우, RouterLinkActive에 지정된 클래스명을 DOM에 자동으로 추가하려면 아래와 같이 routerLinkActiveOptions 디렉티브를 사용한다.

```html
<a routerLink="/service"
  [routerLinkActiveOptions]="{ exact: true }"
  routerLinkActive="active">Service</a>
```

한개 이상의 클래스를 지정할 경우, 아래와 같이 지정한다.

```html
<a routerLink="/service" routerLinkActive="class1 class2">Service</a>
<a routerLink="/service" [routerLinkActive]="['class1', 'class2']">Service</a>
```

RouterLinkActive 디렉티브를 적용한 루트 컴포넌트는 아래와 같다.

```typescript
// app.component.ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <nav>
      <a routerLink="/"
        routerLinkActive="active"
        [routerLinkActiveOptions]="{ exact: true }">
        Home</a>
      <a routerLink="/service"
        routerLinkActive="active"
        [routerLinkActiveOptions]="{ exact: true }">
        Service</a>
      <a routerLink="/about"
        routerLinkActive="active"
        [routerLinkActiveOptions]="{ exact: true }">
        About</a>
    </nav>
    <router-outlet></router-outlet>
  `,
  styles: [`
    nav {
      height: 60px;
      background-color: #4a4c88;
    }
    nav > a {
      line-height: 60px;
      margin: 0 60px;
      color: #fff;
      text-decoration: none;
      font-weight: bold;
      text-transform: uppercase;
      opacity: 0.7;
    }
    nav > a:hover, nav > a.active  {
      opacity: 1.0;
    }
  `]
})
export class AppComponent {}
```

<iframe src="https://stackblitz.com/edit/routing-exam?embed=1&file=app/app.component.ts&hideExplorer=1" frameborder="0" width="100%" height="600"></iframe>

# 5. navigate 메소드

템플릿의 링크 태그를 사용하지 않고 컴포넌트 클래스의 코드만으로 화면을 전환하기 위해서는 navigate 메소드를 사용한다. 간단한 예제를 통해 navigate 메소드를 살펴보도록 하자.

루트 모듈은 아래와 같다.

```typescript
// app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { Routes, RouterModule } from '@angular/router';

import { AppComponent } from './app.component';
import { TodosComponent } from './todos.component';

// 라우트 구성
const routes: Routes = [
  { path: 'todos', component: TodosComponent }
];

@NgModule({
  imports: [
    BrowserModule,
    RouterModule.forRoot(routes)
  ],
  declarations: [ AppComponent, TodosComponent ],
  bootstrap:    [ AppComponent ]
})
export class AppModule { }
```

라우트 패스 /todos의 뷰를 담당하는 TodosComponent는 아래와 같다.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-todos',
  template: `<p>Todos</p>`
})
export class TodosComponent {}
```

루트 컴포넌트를 아래와 같이 작성한다.

```typescript
// app.component.ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-root',
  template: `
    <button (click)="gotoTodos()">goto todos</button>
    <router-outlet></router-outlet>
  `
})
export class AppComponent {
  constructor(private router: Router) {}

  gotoTodos() {
    // /todos로 이동
    this.router.navigate(['/todos']);
  }
}
```

'goto todos' 버튼을 클릭하면 /todos로 이동한다. 이때 링크 태그를 사용하지 않았지만 [Router](https://angular.io/api/router/Router) 클래스의 멤버인 navigate 메소드를 통해 화면 전환이 가능하다. Router 클래스의 인스턴스는 의존성 주입을 통해 컴포넌트로 주입받아 사용한다.

<iframe src="https://stackblitz.com/edit/navigate-method-exam?embed=1&file=app/todo-detail.component.ts&hideExplorer=1" frameborder="0" width="100%" height="500"></iframe>

# 6. 컴포넌트 간의 라우터 상태 전달

화면 전환시에 라우트 파라미터(Route Parameter)를 사용하여 컴포넌트에 데이터를 전달하는 방법에 대해 살펴보도록 하자.

RouterLink 디렉티브는 자신의 값을 라우터에 전달하고 라우터는 이를 전달받아 해당 컴포넌트를 활성화하여 뷰를 출력한다.

```html
<a routerLink="/todo">...</a>
```

이때 라우트 파라미터를 컴포넌트에 전달할 수 있다. 예를 들어 URL 패스가 'todo/:id'인 경우, URL 패스의 두번째 세그먼트 :id는 라우터 파라미터이며 컴포넌트에게 전달되는 값을 할당한다. 예를 들어 ‘/todos/10’과 같이 값을 할당하면 컴포넌트에게 id값으로 10이 전달된다.

```typescript
// app.module.ts
const routes: Routes = [
  { path: '', component: TodosComponent },
  { path: 'todo/:id', component: TodoDetailComponent }
];
```

라우터 파라미터의 값은 RouterLink 디렉티브에 URL 패스의 세그먼트로 구성된 배열을 할당한다. 배열의 첫번째 요소는 URL 패스이며 두번째 요소가 라우터 파라미터의 값이다. 이 값은 컴포넌트로 전달된다.

```html
<a [routerLink]="['todo', todo.id]">...</a>
```

navigate 메소드를 사용할 경우, 아래와 같이 URL 패스의 세그먼트로 구성된 배열을 인수로 전달한다.

```typescript
this.router.navigate(['/todo', todo.id]);
```

`<router-oulet>` 영역에 렌더링된 컴포넌트는 [ActivatedRoute](https://angular.io/api/router/ActivatedRoute) 객체를 통해 라우터 상태(Router state)에 접근할 수 있다. ActivatedRoute는 의존성 주입에 의해 컴포넌트 내에서 참조할 수 있으며 아래와 같은 프로퍼티를 제공한다.

```typescript
interface ActivatedRoute {
  snapshot: ActivatedRouteSnapshot
  url: Observable<UrlSegment[]>
  params: Observable<Params>
  queryParams: Observable<Params>
  fragment: Observable<string>
  data: Observable<Data>
  outlet: string
  component: Type<any>|string|null
  ...
}
```

<!-- | 프로퍼티        | 내용
|:--------------|:-------------------------------------
| url           | 라우트 패스의 각 세그먼트들로 구성된 문자열의 배열을 포함하는 옵저버블이다.
| data          | 라우트 구성에 설정한 데이터 객체를 포함하는 옵저버블이다.
| paramMap      | 라우터에 전달된 라우트 파라미터의 맵을 포함하는 옵저버블이다.
| queryParamMap | 모든 라우트가 공유하는 쿼리 파라미터의 맴을 포함하는 옵저버블이다.
| fragment      | 옵저버블이다.

An Observable of the URL fragment available to all routes.
| outlet        | The name of the RouterOutlet used to render the route. For an unnamed outlet, the outlet name is primary.
| routeConfig   | The route configuration used for the route that contains the origin path.
| parent        | The route's parent ActivatedRoute when this route is a child route.
| firstChild    | Contains the first ActivatedRoute in the list of this route's child routes.
| children      | Contains all the child routes activated under the current route. -->

ActivatedRoute 객체의 인스턴스는 의존성 주입을 통해 컴포넌트로 주입받는다.

```typescript
import { ActivatedRoute } from '@angular/router';
...
export class TodoDetailComponent {
  constructor(private route: ActivatedRoute) { }
```

라우트 파라미터의 값을 취득할 때는 ActivatedRoute의 paramMap 프로퍼티를 사용한다. paramMap 프로퍼티는 라우터에 전달된 라우트 파라미터의 맵을 포함하는 옵저버블이다.

Angular는 URL 패스가 변경되어도 해당 컴포넌트가 변경되지 않는다면 해당 컴포넌트를 소멸시키지 않고 재사용한다. 따라서 컴포넌트가 소멸되지 않은 상태에서 라우터 파라미터만 변경된 라우터 상태를 연속으로 수신할 수 있기 때문에 paramMap을 옵저버블로 제공한다. paramMap의 get 메소드에 라우트 파라미터 이름을 인자로 전달하여 라우트 파라미터를 취득한다.

```typescript
export class TodoDetailComponent implements OnInit {

  todoId: number;

  constructor(private route: ActivatedRoute) { }

  ngOnInit() {
    this.route.paramMap
      .subscribe(params => this.todoId = +params.get('id'));
  }
}
```

옵저버블 스트림이 아닌 특정 시점의 상태만을 조회하는 경우, ActivatedRoute의 snapshot 프로퍼티를 사용할 수 있다. snapshot 프로퍼티는 옵저버블로 래핑되지 않은 paramMap 객체를 반환한다.

```typescript
ngOnInit() {
  this.todoId = +this.route.snapshot.paramMap.get('id');
}
```

<iframe src="https://stackblitz.com/edit/route-parameter-exam?embed=1&file=app/app.component.ts&hideExplorer=1" frameborder="0" width="100%" height="500"></iframe>

# Reference

* [Angular Routing & Navigation](https://angular.io/guide/router)

* [Route](https://angular.io/api/router/Routes)

* [RouterOutlet](https://angular.io/api/router/RouterOutlet)

* [RouterLink](https://angular.io/api/router/RouterLink)

* [RouterLinkActive](https://angular.io/api/router/RouterLinkActive)

* [Router](https://angular.io/api/router/Router)

* [ActivatedRoute](https://angular.io/api/router/ActivatedRoute)
