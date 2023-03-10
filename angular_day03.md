## 自定义事件
> 效果和vue中的emit相同，可用于子组件向父组件传值

### 示例
```html
<!-- 父组件 -->
<app-show-image (mgClicked)="mgClicked($event)"></app-show-image>
```
```typescript
//父组件
mgClicked = (info:object) => {
  console.log(info);
}
```
```typescript
//子组件
@Output() mgClicked: EventEmitter<any> = new EventEmitter()
```
```typescript
//子组件调用
this.mgClicked.emit({
  position:{
    x:$event.offsetX,
    y:$event.offsetY
  },
  preImg:this.preImg,
  curImg:this.imgArr[this.targetImgIndex],
  date
})
```
## 自定义指令
### 创建指令
> ng generate directive directiveName

![截屏2023-03-10 13.45.16.png](https://cdn.nlark.com/yuque/0/2023/png/32470501/1678427124409-34e5da3d-360c-4711-94f7-94a38ceddb05.png#averageHue=%234b7560&clientId=ucd06b2d7-df4f-4&from=drop&id=u703e9ace&name=%E6%88%AA%E5%B1%8F2023-03-10%2013.45.16.png&originHeight=277&originWidth=447&originalType=binary&ratio=1&rotation=0&showTitle=false&size=55423&status=done&style=none&taskId=uee22dbe1-32d5-4dde-82e2-99fc9ff403b&title=)
```typescript
import { Directive, ElementRef } from '@angular/core';

@Directive({
  selector: '[appMyDirective]'
})
export class MyDirectiveDirective {

  constructor(private el:ElementRef) {
    //逻辑
    this.el.nativeElement.onclick = () => {
      console.log(this.el.nativeElement.tagName);
      this.el.nativeElement.style.backgroundColor = 'pink'
    }
  }

}

```
### 使用指令
```html
<h1 appMyDirective>my diretive</h1>
```
## 自定义管道
> ng g pipe  pipeName

```html
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'myDate'
})
export class MyDatePipe implements PipeTransform {
     
  transform(value: Date, ...args: string[]): unknown {
  //逻辑 

	//返回值为经过处理的数据
  return null
}

```
### 使用
```html
<h3>{{newTime|myDate:"yyyy-MM-dd hh:mm:ss"}}</h3>
```
