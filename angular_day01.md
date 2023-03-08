## 1.了解Angular的运行顺序，main.ts，application.ts的运行顺序是如何的？
### (1)angular的运行顺序
> main.ts是启动的起点，platformBrowserDynamic这个函数是浏览器平台的工厂函数,执行会返回浏览器平台的实例，然后对根模块进行初始化，链式的将所有的依赖的Module都给加载进来。每个应用程序都是通过模块的using bootstrapModule方法创建的。

> 创建应用程序时，Angular会检查根模块AppModule，AppModule的属性bootstrap用于引导应用程序。此属性通常来来引导应用程序的组件。然后Angular在DOM中找到作为自举组件的选择器的元素，并初始化该组件。

### (2)main.ts，application.ts的运行顺序
> 先运行main.ts,后运行application.ts

## 2.了解angular的配置件,angular.json,tsconfig.json, package.json 这些文件是做什么的？
> angular.json：angular-cli的配置文件。

> tsconfig.json：TypeScript编辑器的配置。

> package.json：定义项目所需要的各种模块，以及项目的配置信息（比如名称、版本、许可证、如何启动项目、运行脚步等元数据）。

## 3.了解angular的路由，什么是路由？ 增加一个test路由路径
### 什么是路由？
> 在保证只有一个 HTML 页面，且与用户交互时不刷新和跳转页面的同时，为 SPA 中的每个视图展示形式匹配一个特殊的 url。在刷新、前进、后退和SEO时均通过这个特殊的 url 来实现。

### 增加路由路径test
```typescript
const routes: Routes = [
  { path: 'first-component', component: FirstComponent },
  { path: 'second-component', component: SecondComponent },
  { path: 'test', component: TestComponent }
];
```
```html
<nav>
  <ul>
    <li><a routerLink="/first-component" routerLinkActive="active" ariaCurrentWhenActive="page">First Component</a></li>
    <li><a routerLink="/second-component" routerLinkActive="active" ariaCurrentWhenActive="page">Second Component</a></li>
    <li><a routerLink="/test" routerLinkActive="active" ariaCurrentWhenActive="page">My test</a></li>
  </ul>
</nav>
<router-outlet></router-outlet>
```
## 4.了解angular的常用的指令，for ,if ,switch，写一个 demo
### NgFor
```javascript
export class TestComponent {
  list = [
    {
      name: '小明',
      age: 18
    },
    {
      name: '小红',
      age: 20
    },
    {
      name: '小王',
      age: 28
    }
  ]
}
```
```html
<ul>
  <li *ngFor="let item of list">姓名：{{item.name}}年龄：{{item.age}}</li>
</ul>
```
![截屏2023-03-08 14.49.44.png](https://cdn.nlark.com/yuque/0/2023/png/32470501/1678258200269-72ce1f8d-c141-4ded-bddb-bd9dc12df80b.png#averageHue=%23e8e8e8&clientId=uecc1ee49-000f-4&from=drop&id=u45cbb5d3&name=%E6%88%AA%E5%B1%8F2023-03-08%2014.49.44.png&originHeight=93&originWidth=214&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9338&status=done&style=none&taskId=ufb95100c-e021-4ace-8e56-97777a84a2c&title=)
### NgIf
```javascript
export class TestComponent {
  isShow = true
}
```
```html
<div *ngIf="isShow">show</div>
<div *ngIf="isShow;else test"></div>
<ng-template #test>
    <div style="color:red">not show</div>
</ng-template>
```
### NgSwitch
```javascript
export class TestComponent {
  switch = 'stout'
}
```
```html
<!-- ngSwitch -->
<div [ngSwitch]="switch">
    <div *ngSwitchCase="'stout'">stout</div>
    <div *ngSwitchCase="'slim'">slim</div>
    <div *ngSwitchCase="'vintage'">vintage</div>
    <div *ngSwitchCase="'bright'">bright</div>
    <!-- . . . -->
    <div *ngSwitchDefault>
        <ng-container *ngTemplateOutlet="test"></ng-container>
    </div>
</div>
<ng-template #test>
    <div style="color:red">not show</div>
</ng-template>
```
## 5.了解angular的ng-container、 ng-template、 ng-content的使用，写一个demo
### ng-container
> 书写时就是个html标签，但是实际页面不会生成任何元素，一般都用作逻辑处理

```javascript
containerList = [
  {
    name:'lz',
    isShow:true
  },
  {
    name:'jl',
    isShow:false
  },
  {
    name:'hjl',
    isShow:true
  }
]
```

```html
<ng-container *ngFor="let item of containerList">
  <div style="color:red" *ngIf="item.isShow">{{item.name}}</div>
</ng-container>
```
![截屏2023-03-08 15.24.45.png](https://cdn.nlark.com/yuque/0/2023/png/32470501/1678260296287-354d348a-d6d2-4bc0-a3b9-75bd9b17ad7a.png#averageHue=%23282d32&clientId=uecc1ee49-000f-4&from=drop&id=uae495a12&name=%E6%88%AA%E5%B1%8F2023-03-08%2015.24.45.png&originHeight=23&originWidth=435&originalType=binary&ratio=1&rotation=0&showTitle=false&size=9940&status=done&style=none&taskId=uf9a9c3cf-4c8b-4b4e-9cb5-f440e65aae4&title=)
```html
<div *ngFor="let item of containerList">
    <div style="color:red" *ngIf="item.isShow">{{item.name}}</div>
</div>
```
![截屏2023-03-08 15.25.21.png](https://cdn.nlark.com/yuque/0/2023/png/32470501/1678260328909-573fe077-a3ae-4b5b-a252-ffab75d97cfe.png#averageHue=%2323262a&clientId=uecc1ee49-000f-4&from=drop&id=u81fb8cfc&name=%E6%88%AA%E5%B1%8F2023-03-08%2015.25.21.png&originHeight=111&originWidth=468&originalType=binary&ratio=1&rotation=0&showTitle=false&size=18556&status=done&style=none&taskId=uc0864938-f886-49f9-a21d-a3c9b4ea1dd&title=)
### ng-template
> <ng-template> 是一个模板元素，用于Angular与结构指令结合使用

```html
<!-- ngIf && ngIf else -->
<div *ngIf="isShow">show</div>
<div *ngIf="isShow;else test"></div>
<!-- ngSwitch -->
<div [ngSwitch]="switch">
    <div *ngSwitchCase="'stout'">stout</div>
    <div *ngSwitchCase="'slim'">slim</div>
    <div *ngSwitchCase="'vintage'">vintage</div>
    <div *ngSwitchCase="'bright'">bright</div>
    <!-- . . . -->
    <div *ngSwitchDefault>
        <ng-container *ngTemplateOutlet="test"></ng-container>
    </div>
</div>
<ng-template #test>
    <div style="color:red">not show</div>
</ng-template>
```
### ng-content
> 内容投影，可以在其中插入或投影要在另一个组件中使用的内容，类似于vue中的插槽

```html
<!-- 父组件 -->
<app-content>
  <p>qweqwe</p>
  <div class="contentTest">select_content</div>
</app-content>
<!-- 子组件 -->
<p>content works!</p>
<ng-content></ng-content>
<ng-content select=".contentTest"></ng-content>
```
## 6.了解angular的事件，html+ts如何绑定？
### html
```html
<button (click)="isShow=!isShow">My_Click</button>
<button (click)="myEent()">event-button</button>
<input type="text" (keyup.enter)="keyEvent()">
```
```javascript
export class TestComponent {
  isShow = true
  
  myEent = (): string => {
    console.log(123);
    return 'qwe'
  }
  
  keyEvent = () => {
    console.log('key');
  }
}
```
### ts
```javascript
@HostListener('window:click',['$event.target'])
  onClick(targetElement:string){
    console.log('you clicked on',targetElement) 
  }
```
