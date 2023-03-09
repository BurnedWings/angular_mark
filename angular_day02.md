## 1.了解模块的概念，编写一个lazy router
### 模块
> 在 Angular 应用中，至少会存在一个 NgModule，也就是应用的根模块（AppModule）,通过引导这个根模块就可以启动整个项目像开发中使用到 FormsModule、HttpClientModule 这种 Angular 内置的库也都是一个个的 NgModule，在开发中通过将组件、指令、管道、服务或其它的代码文件聚合成一个内聚的功能块，专注于系统的某个功能模块

### 常见的NgModule
| **模块名称** | **模块所在文件** | **功能点** |
| --- | --- | --- |
| BrowserModule | @angular/platform-browser | 用于启动和运行浏览器应用的基本服务 |
| CommonModule | @angular/common | 使用 NgIf、NgFor 之类的内置指令 |
| FormsModule | @angular/forms | 使用 NgModel 构建模板驱动表单 |
| ReactiveFormsModule | @angular/forms | 构建响应式表单 |
| RouterModule | @angular/router | 使用前端路由 |
| HttpClientModule | @angular/common/[http](https://angular.cn/api/common/http) | 发起 http 请求 |

## 了解angular component的生命周期顺序，并了解什么是interface
### 生命周期顺序
#### ngOnChanges()
用途
> 当 Angular 设置或重新设置数据绑定的输入属性时响应。该方法接受当前和上一属性值的 [SimpleChanges](https://angular.cn/api/core/SimpleChanges) 对象 

时机
> 如果组件绑定过输入属性，那么在 ngOnInit() 之前以及所绑定的一个或多个输入属性的值发生变化时都会调用。

#### ngOnInit()
用途
> 在 Angular 第一次显示数据绑定和设置指令/组件的输入属性之后，初始化指令/组件。欲知详情，参阅本文档中的[初始化组件或指令](https://angular.cn/guide/lifecycle-hooks#oninit)。

时机
> 在第一轮 ngOnChanges() 完成之后调用，只调用**一次**。而且即使没有调用过 ngOnChanges()，也仍然会调用 ngOnInit()（比如当模板中没有绑定任何输入属性时）。

#### ngDoCheck()
用途
> 检测，并在发生 Angular 无法或不愿意自己检测的变化时作出反应。

时机
> 紧跟在每次执行变更检测时的 ngOnChanges() 和 首次执行变更检测时的 ngOnInit() 后调用。

#### ngAfterContentInit()
用途
> 当 Angular 把外部内容投影进组件视图或指令所在的视图之后调用。

时机
> 第一次 ngDoCheck() 之后调用，只调用一次。

#### ngAfterContentChecked()
用途
> 每当 Angular 检查完被投影到组件或指令中的内容之后调用。

时机
> ngAfterContentInit() 和每次 ngDoCheck() 之后调用。

#### ngAfterViewInit()
用途
> 当 Angular 初始化完组件视图及其子视图或包含该指令的视图之后调用。

时机
> 第一次 ngAfterContentChecked() 之后调用，只调用一次。

#### ngAfterViewChecked()
用途
> 每当 Angular 做完组件视图和子视图或包含该指令的视图的变更检测之后调用。

时机
> ngAfterViewInit() 和每次 ngAfterContentChecked() 之后调用。

#### ngOnDestroy()
用途
> 每当 Angular 每次销毁指令/组件之前调用并清扫。在这儿反订阅可观察对象和分离事件处理器，以防内存泄漏

时机
> 在 Angular 销毁指令或组件之前立即调用。

### interface
> TypeScript的核心原则之一是对值所具有的_结构_进行类型检查。 它有时被称做“鸭式辨型法”或“结构性子类型化”。在TypeScript里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。

```typescript
interface LabelledValue {
  label: string;
}
function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
onChange
onInit
doChecked
afterContentInit
afterContentChecked
afterViewInit
afterViewChecked
onDestroy
> - 自定义事件（要求在自定义component部分）
> - 自定义component:写一个自定义组件，组件的功能是展示图片，点击图片可以切换图片（图片的地址存放在一个对象数组中，使用接口定义对象的属性 需要包含图片的信息，必须包含的属性有图片的名称和资源地址，可选的参数有图片的尺寸(也要用接口定义尺寸信息 包含width 和 height)），写一个自定义的imgClicked事件，当点击图片的时候,返回内容有鼠标点击图片的位置（属性的key value如 position : {x : 0, y : 0}）、上一张图片的信息、当前切换图片的信息,点击时的时间戳，组件要求输入图片信息对象数组，如果没有输入，则展示默认的图片对象数组
> - 自定义directive:写一个指令，可以给当前绑定指令的元素添加一个点击事件，输出当前元素的标签，并改变元素的背景色
> - 自定义Pipe:编写一个管道符指令，功能是将一个数字类型的时间戳(如1675139055)转化成时间字符串(默认格式为 "yyyy-MM-dd hh:mm:ss" 并且可以通过参数的形式指定格式 如指定 "yyyy MM-dd" )

