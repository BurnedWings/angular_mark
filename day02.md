## 双向数据绑定

```html
<input type="text" [(ngModel)]="data">
```

```js
data='歪比歪比'
```

### 注意:需要在app.module.ts里引入FormsModule

```js
import { FormsModule } from '@angular/forms'
```

```js
imports: [
    BrowserModule,
    AppRoutingModule,
    //以下
    FormsModule
    //以上
  ],
```

