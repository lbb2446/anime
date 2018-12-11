# [anime.js](http://animejs.com) ![](http://img.badgesize.io/juliangarnier/anime/master/anime.min.js.svg?style=flat&color=18FF92)

<img src="http://animejs.com/documentation/assets/img/readme/animejs-logo.gif" width="100%" />

>*Anime* `(/ˈæn.ə.meɪ/)` 是一个轻量级的JS动画库. 可以作用于所有 CSS 属性, 独立的 CSS 变换, SVG 和任意 DOM 属性, 以及 JavaScript 对象.

⚠️ **从 v1.x如何迁移 ? 请移步 [changelog](https://github.com/juliangarnier/anime/releases/tag/v2.0.0)** ⚠️

### 主要功能

* [Keyframes](#keyframes): Chain multiple animation properties.
* [Timeline](#timeline): 一起同步多个实例.
* [Playback controls](#playback-controls): 开, 暂停, 重开, seek（回溯） 等动画或者时间轴.
* [CSS transforms](#individual-CSS-transforms):独特的CSStransforms类型的动画属性
* [Function based values](#function-based-values): Multiple animated targets can have individual value.
* [SVG Animations](#svg): 运动轨迹, 绕线运动 和 变形动画.
* [Easing functions](#easing-functions): 使用已构建好的动画曲线或者 创建你自己的贝塞尔曲线.

### Demo 和 例子

* [CodePen demos and examples](http://codepen.io/collection/b392d3a52d6abf5b8d9fda4e4cab61ab/)
* [juliangarnier.com](http://juliangarnier.com)
* [animejs.com](http://animejs.com)
* [kenzo.com/en/thejunglebook](https://kenzo.com/en/thejunglebook)
* [Stress test](http://codepen.io/juliangarnier/pen/9aea7f045d7db301eab41bc09dcfc04d?editors=0010)

### 浏览器支持情况

| Chrome | Safari | IE / Edge | Firefox | Opera |
| --- | --- | --- | --- | --- |
| 24+ | 6+ | 10+ | 32+ | 15+ |

## Usage

```bash
$ npm install animejs
# OR
$ bower install animejs
```

```javascript
import anime from 'animejs'
```

  [手动下载](https://github.com/juliangarnier/anime/archive/master.zip) and link `anime.min.js` in your HTML:

```html
<script src="anime.min.js"></script>
```

然后开始开发:

```javascript
anime({
  targets: 'div',
  translateX: [
    { value: 100, duration: 1200 },
    { value: 0, duration: 800 }
  ],
  rotate: '1turn',
  backgroundColor: '#FFF',
  duration: 2000,
  loop: true
});
```

# API

## Targets（目标）

 `targets` 属性定义elements或者JS对象发生动画.

| Types | Examples
| --- | ---
| CSS Selectors(css选择器) | `'div'`, `'.item'`, `'path'`, `'#el path'` ...
| DOM Element(dom对象) | `document.querySelector('.item')`
| NodeList (dom对象集合)| `document.querySelectorAll('.item')`
| `Object` (js对象)| `{prop1: 100, prop2: 200}`
| `Array` (数组)| `['div', '.item', domNode]`

➜ [Targets 案例](http://animejs.com/documentation/#cssSelector)

## Animatable properties

| Types | Examples
| --- | ---
| CSS | `opacity`, `backgroundColor`, `fontSize` ...
| Transforms | `translateX`, `rotate`, `scale` ...
| Object properties |  `Object`中所有包含数值类型的属性
| DOM attributes | 所有 DOM 包含 数值 属性 
| SVG attributes |所有 SVG 包含 数值 属性 

➜ [Animatable properties examples](http://animejs.com/documentation/#cssProperties)

### CSS

<img src="http://animejs.com/documentation/assets/img/readme/prop-css.gif" width="332" />

所有CSS属性都能被做动画:

```javascript
anime({
  targets: 'div',
  left: '80%', // Animate all divs left position to 80%
  opacity: .8, // Animate all divs opacity to .8
  backgroundColor: '#FFF' // Animate all divs background color to #FFF
});
```

➜ [CSS properties example](http://animejs.com/documentation/#cssProperties)

### 独特的 CSS 转换

<img src="http://animejs.com/documentation/assets/img/readme/prop-transforms.gif" width="332" />

CSS 中的transforms类被单独提取出来:

```javascript
anime({
  targets: 'div',
  translateX: 250, // Animate all divs translateX property to 250px
  scale: 2, // Animate all divs scale to 2
  rotate: '1turn' // Animate all divs rotation to 1 turn
});
```

➜ [CSS Transforms example](http://animejs.com/documentation/#CSStransforms)

### JavaScript Object 属性

<img src="http://animejs.com/documentation/assets/img/readme/prop-js-obj.gif" width="332" />

所有 `Object`  包含数值的属性都可以做动画:

```javascript
var myObject = {
  prop1: 0,
  prop2: '0%'
}

anime({
  targets: myObject,
  prop1: 50, // Animate the 'prop1' property from myObject to 50
  prop2: '100%' // Animate the 'prop2' property from myObject to 100%
});
```

➜ [Object properties example](http://animejs.com/documentation/#JSobjectProp)

### DOM 属性

<img src="http://animejs.com/documentation/assets/img/readme/prop-dom-attr.gif" width="332" />

所有 `Dom属性`  包含数值的属性都可以做动画:

```html
<input value="0">
```

```javascript
anime({
  targets: input,
  value: 1000, // Animate the input value to 1000
  round: 1 // Remove decimals by rounding the value
});
```

➜ [DOM Attributes example](http://animejs.com/documentation/#domAttributes)

### SVG Attributes

<img src="http://animejs.com/documentation/assets/img/readme/prop-svg-attr.gif" width="332" />

所有 `SVG属性`  包含数值的属性都可以做动画:

```html
<svg width="128" height="128" viewBox="0 0 128 128">
  <polygon points="64 68.73508918222262 8.574 99.9935923731656 63.35810017508558 67.62284396863708 64 3.993592373165592 64.64189982491442 67.62284396863708 119.426 99.9935923731656"></polygon>
</svg>
```

```javascript
anime({
  targets: 'polygon',
  points: '64 128 8.574 96 8.574 32 64 0 119.426 32 119.426 96'
});
```

➜ [SVG Attributes example](http://animejs.com/documentation/#svgAttributes)

## 属性参数

<img src="http://animejs.com/documentation/assets/img/readme/prop-parameters.gif" width="332" />

定义了 duration, delay and easing 针对所有的动画属性.<br>
可以对这些属性做单独或者全部的操作:

| Names | Defaults | Types | Info
| --- | --- | --- | ---
| duration | `1000` | `number`, `function`  | 毫秒
| delay | `0` | `number`, `function`   | 毫秒
| easing | `'easeOutElastic'` | `function`  | [缓动函数类型](#easing-functions)
| elasticity | `500` | `number`, `function` | 范围 [0 - 1000]
| round | `false` | `number`, `boolean`, `function` | Power of 10

```javascript
anime({
  translateX: {
    value: 250,
    duration: 800
  },
  rotate: {
    value: 360,
    duration: 1800,
    easing: 'easeInOutSine'
  },
  scale: {
    value: 2,
    duration: 1600,
    delay: 800,
    easing: 'easeInOutQuart'
  },
  delay: 250 // All properties except 'scale' inherit 250ms delay
});
```

➜ [Property parameters examples](http://animejs.com/documentation/#duration)

## Function based property parameters

<img src="http://animejs.com/documentation/assets/img/readme/fb-parameters.gif" width="332" />

对每一个动画的目标可以得到不同的属性参数.<br>
 function 默认返回3个参数: `target`, `index`, `targetsLength`.

```javascript
anime({
  targets: 'div',
  translateX: 250,
  rotate: 180,
  duration: function(target) {
    // Duration based on every div 'data-duration' attribute
    return target.getAttribute('data-duration');
  },
  delay: function(target, index) {
    // 100ms delay multiplied by every div index, in ascending order
    return index * 100;
  },
  elasticity: function(target, index, totalTargets) {
    // Elasticity multiplied by every div index, in descending order
    return 200 + ((totalTargets - index) * 200);
  }
});
```

➜ [Function based parameters examples](http://animejs.com/documentation/#functionBasedDuration)

## 动画参数

<img src="http://animejs.com/documentation/assets/img/readme/anim-parameters.gif" width="332" />

Parameters relative to the animation to specify the direction, the number of loops or autoplay.

| Names | Defaults | Types
| --- | --- | ---
| loop | `false` | `number`, `boolean`
| direction | `'normal'` | `'normal'`（正常）, `'reverse'`（颠倒）, `'alternate'`（交替）
| autoplay | `true` | `boolean`

```javascript
anime({
  targets: 'div',
  translateX: 100,
  duration: 2000,
  loop: 3, // Play the animation 3 times
  direction: 'reverse', // Play the animation in reverse
  autoplay: false // Animation paused by default
});
```

➜ [Animation parameters examples](http://animejs.com/documentation/#alternate)

## 属性值

### 单个值

定义 动画的最终值<br>
Start value is the original target value, or default transforms value.

| Types | Examples | Infos
| --- | --- | ---
| Number | `100` | Automatically add original or default unit if needed
| String | `'10em'`, `'1turn'`, `'M21 1v160'`, `'50%'` | Must contains at least one numerical value
| Relative values | `'+=100px'`, `'-=20em'`, `'*=4'` | 加、减、乘原属性值
| Colors | `'#FFF'`, `'rgb(255,0,0)'`, `'hsl(100, 20%, 80%)'` | 接受 3 or 6位十六进制, rgb, 或者 hsl 值

➜ [Values examples](http://animejs.com/documentation/#unitlessValue)

```javascript
anime({
  targets: 'div',
  translateX: 100, // Add 'px' by default (from 0px to 100px)
  rotate: '1turn', // Use 'turn' as unit (from 0turn to 1turn)
  scale: '*=2', // Multiply the current scale value by 2 (from 1 to (1 * 2))
  backgroundColor: '#FFF', // Animate the background color to #FFF (from 'rgb(0,0,0)' to 'rgb(255,255,255)')
  duration: 1500
});
```

### From > To values

<img src="http://animejs.com/documentation/assets/img/readme/value-from-to.gif" width="332" />

使用动画开始于某一个值

```javascript
anime({
  targets: 'div',
  translateX: [100, 200], // Translate X from 100 to 200
  rotate: ['.5turn', '1turn'], // Rotate from 180deg to 360deg
  scale: ['*=2', 1], // Scale from 2 times the original value to 1,
  backgroundColor: ['rgb(255,0,0)', '#FFF'], // Will transition the background color from red to white
  duration: 1500
});
```

➜ [Specific initial value example](http://animejs.com/documentation/#specificInitialValue)

### Function based values

<img src="http://animejs.com/documentation/assets/img/readme/value-fb.gif" width="332" />

 与 [function based property parameters](#function-based-property-parameters)一样.<br>
对每一个动画的目标可以得到不同的属性参数.<br>
 function 默认返回3个参数: `target`, `index`, `targetsLength`.

```javascript
anime({
  targets: 'div',
  translateX: function(el) {
    return el.getAttribute('data-x');
  },
  translateY: function(el, i) {
    return 50 + (-50 * i);
  },
  scale: function(el, i, l) {
    return (l - i) + .25;
  },
  rotate: function() { return anime.random(-360, 360); },
  duration: function() { return anime.random(800, 1600); },
  delay: function() { return anime.random(0, 1000); }
});
```

➜ [Function based value example](http://animejs.com/documentation/#functionBasedPropVal)

### Keyframes

<img src="http://animejs.com/documentation/assets/img/readme/value-keyframes.gif" width="332" />

Keyframes(关键帧) 使用 对象数组定义.<br>
Instance's `duration` is divided by the number of keyframes of each properties if not specified.

```javascript
anime({
  targets: 'div',
  translateX: [
    { value: 250, duration: 1000, delay: 500, elasticity: 0 },
    { value: 0, duration: 1000, delay: 500, elasticity: 0 }
  ],
  translateY: [
    { value: -40, duration: 500, elasticity: 100 },
    { value: 40, duration: 500, delay: 1000, elasticity: 100 },
    { value: 0, duration: 500, delay: 1000, elasticity: 100 }
  ],
  scaleX: [
    { value: 4, duration: 100, delay: 500, easing: 'easeOutExpo' },
    { value: 1, duration: 900, elasticity: 300 },
    { value: 4, duration: 100, delay: 500, easing: 'easeOutExpo' },
    { value: 1, duration: 900, elasticity: 300 }
  ],
  scaleY: [
    { value: [1.75, 1], duration: 500 },
    { value: 2, duration: 50, delay: 1000, easing: 'easeOutExpo' },
    { value: 1, duration: 450 },
    { value: 1.75, duration: 50, delay: 1000, easing: 'easeOutExpo' },
    { value: 1, duration: 450 }
  ]
});
```

➜ [Specific keyframes properties example](http://animejs.com/documentation/#keyframes)

## Timeline(时间轴)

### Basic timeline

<img src="http://animejs.com/documentation/assets/img/readme/timeline.gif" width="332" />

通过创建一个时间轴来播放动画序列:

```javascript
var myTimeline = anime.timeline();
```

时间轴可以接受与动画对象一样的参数: `direction`, `loop` and `autoplay`.

```javascript
var myTimeline = anime.timeline({
  direction: 'alternate',
  loop: 3,
  autoplay: false
});
```

在时间轴上新增一个动作 `.add()` :

```javascript
myTimeline
  .add({
    targets: '.square',
    translateX: 250
  })
  .add({
    targets: '.circle',
    translateX: 250
  })
  .add({
    targets: '.triangle',
    translateX: 250
  });
```

可以通过`myTimeline.children`获取子对象

➜ [Basic timeline example](http://animejs.com/documentation/#basicTimeline)

### Timeline animations offsets（时间轴动画补间？）

`offset` 在时间轴中定义开始时间

#### Relative offset（相对时间）

<img src="http://animejs.com/documentation/assets/img/readme/timeline-relative.gif" width="332" />

Defines starting time relative to the previous animations duration.

| Types | Examples | Infos
| --- | --- | ---
| `+=` | `'+=100'` | Starts 100ms after the previous animation ends（后延）
| `-=` | `'-=100'` | Starts 100ms before the previous animation ends（前推）
| `*=` | `'*=2'` | Starts at 2 times the previous animations duration

```javascript
myTimeline
  .add({
    targets: '.square',
    translateX: 250
  })
  .add({
    targets: '.circle',
    translateX: 250,
    offset: '-=600' // Starts 600ms before the previous animation ends
  })
  .add({
    targets: '.triangle',
    translateX: 250,
    offset: '-=800' // Starts 800ms before the previous animation ends
  });
```

➜ [Relative offset example](http://animejs.com/documentation/#relativeOffset)

#### Absolute offset（绝对时间）

<img src="http://animejs.com/documentation/assets/img/readme/timeline-absolute.gif" width="332" />

定义了一个绝对的起始时间与数量在时间轴上

```javascript
myTimeline
  .add({
    targets: '.square',
    translateX: 250,
    offset: 1000 // Starts at 1000ms
  })
  .add({
    targets: '.circle',
    translateX: 250,
    offset: 500 // Starts at 500ms
  })
  .add({
    targets: '.triangle',
    translateX: 250,
    offset: 0 // Starts at 0ms
  });
```

➜ [Absolute offset example](http://animejs.com/documentation/absoluteOffset)

## 回放控制

Play, pause, restart, seek animations or timelines.

### Play / Pause

<img src="http://animejs.com/documentation/assets/img/readme/playback-play-pause.gif" width="332" />

```javascript
var playPauseAnim = anime({
  targets: 'div',
  translateX: 250,
  direction: 'alternate',
  loop: true,
  autoplay: false // prevent the instance from playing
});

playPauseAnim.play(); //  Manually play
playPauseAnim.pause(); //  Manually pause
```

➜ [Play / Pause example](http://animejs.com/documentation/#playPause)

### Restart

<img src="http://animejs.com/documentation/assets/img/readme/playback-restart.gif" width="332" />

```javascript
var restartAnim = anime({
  targets: 'div',
  translateX: 250,
  direction: 'alternate',
  loop: true,
  autoplay: false
});

restartAnim.restart(); // Restart the animation and reset the loop count / current direction
```

➜ [Restart example](http://animejs.com/documentation/#restartAnim)

### Reverse

<img src="http://animejs.com/documentation/assets/img/readme/playback-reverse.gif" width="332" />

```javascript
var reverseAnim = anime({
  targets: 'div',
  translateX: 250,
  direction: 'alternate',
  loop: true
});

reverseAnim.reverse(); // Change the animation direction
```

➜ [Reverse example](http://animejs.com/documentation/#reverseAnim)

### Seek（回溯）

<img src="http://animejs.com/documentation/assets/img/readme/playback-seek.gif" width="332" />

回溯到选定的时间点

```javascript
var seekAnim = anime({
  targets: 'div',
  translateX: 250,
  delay: function(el, i, l) { return i * 100; },
  elasticity: 200,
  autoplay: false
});

seekAnim.seek(500); // Set the animation current time to 500ms
```

➜ [Seek example](http://animejs.com/documentation/#seekAnim)

## Callbacks

<img src="http://animejs.com/documentation/assets/img/readme/callbacks-all.gif" width="332" />

执行一个函数在开始,更新或完成的时候

| Names | Types | Arguments | Info
| --- | --- | --- | ---
| update | `function`| animation `Object` | Called at time = 0
| begin | `function` | animation `Object` | Called after animation delay is over
| complete | `function` | animation `Object` | Called only after all the loops are completed

➜ [Callbacks examples](http://animejs.com/documentation/#allCallbacks)

### Update

`update()` 在播放的时候,每一帧都会触发.

```javascript
var myAnimation = anime({
  targets: '#update .el',
  translateX: 250,
  delay: 1000,
  update: function(anim) {
    console.log(anim.currentTime + 'ms'); // Get current animation time with `myAnimation.currentTime`, return value in ms.
    console.log(anim.progress + '%'); // Get current animation progress with `myAnimation.progress`, return value in %
  }
});
```

➜ [Update example](http://animejs.com/documentation/#update)

### Begin

`begin()` 会毁掉一次，在delay结束的时候

```javascript
var myAnimation = anime({
  targets: '#begin .el',
  translateX: 250,
  delay: 1000,
  begin: function(anim) {
    console.log(anim.began); // true after 1000ms
  }
});
```

Check if the animation has begun with `myAnimation.began`, return `true` or `false`.

➜ [Begin example](http://animejs.com/documentation/#begin)

### Run

`run()` 在delay结束的时候后的每一帧.

```javascript
var myAnimation = anime({
  targets: '#run .el',
  translateX: 250,
  delay: 1000,
  run: function(anim) {
    console.log(anim.currentTime);
  }
});
```

➜ [Run example](http://animejs.com/documentation/#run)

### Complete

`complete()` 动画结束的时候调用.

```javascript
var myAnimation = anime({
  targets: '#complete .el',
  translateX: 250,
  complete: function(anim) {
    console.log(anim.completed);
  }
});
```

Check if the animation has finished with `myAnimation.completed`, return `true` or `false`.

➜ [Complete example](http://animejs.com/documentation/#complete)

## Promises

`myAnimation.finished` 一旦动画运行结束返回一个Promise对象 ？？returns a Promise object which will resolve once the animation has finished running.

➜ [Promises example](http://animejs.com/documentation/#finishedPromise)

## SVG

### Motion path

<img src="http://animejs.com/documentation/assets/img/readme/svg-motion-path.gif" width="332" />

使 DOM elements沿着SVGpath运动和翻转:

```javascript
// Create a path `Object`
var path = anime.path('#motionPath path');

var motionPath = anime({
  targets: '#motionPath .el',
  translateX: path('x'), // Follow the x values from the path `Object`
  translateY: path('y'), // Follow the y values from the path `Object`
  rotate: path('angle')  // Follow the angle values from the path `Object`
});
```

➜ [Motion path example](http://animejs.com/documentation/#motionPath)

### Morphing（变形）

<img src="http://animejs.com/documentation/assets/img/readme/svg-morphing.gif" width="332" />

使动画在两个SVG图形之间的过渡:

```html
<svg class="shape" width="128" height="128" viewBox="0 0 128 128">
  <polygon points="64 68.64 8.574 100 63.446 67.68 64 4 64.554 67.68 119.426 100"></polygon>
</svg>
```

```javascript
var svgAttributes = anime({
  targets: '.shape polygon',
  points: '64 128 8.574 96 8.574 32 64 0 119.426 32 119.426 96'
});
```

形状需要相同数量的点.

➜ [Morphing example](http://animejs.com/documentation/#morphing)

### Line drawing(绘线)

<img src="http://animejs.com/documentation/assets/img/readme/svg-line-drawing.gif" width="332" />

照着一个SVG的形状的线条绘制动画:

```javascript
anime({
  targets: '.shape path',
  strokeDashoffset: [anime.setDashoffset, 0]
});
```

➜ [Line drawing example](http://animejs.com/documentation/#lineDrawing)

## Easing functions（缓动函数）

The `easing` parameter can accept either a string or a custom Bézier curve coordinates (array).

| Types | Examples | Infos
| --- | --- | ---
| String | `'easeOutExpo'` | 已有的函数名称
| `Array` | [.91,-0.54,.29,1.56] | 定义贝塞尔曲线坐标轴 ([x1, y1, x2, y2])

### Built in functions

Linear easing: `'linear'`（线性，平滑）

Penner's equations:

| easeIn | easeOut | easeInOut
| --- | --- | ---
| easeInQuad | easeOutQuad | easeInOutQuad |
| easeInCubic | easeOutCubic | easeInOutCubic
| easeInQuart | easeOutQuart | easeInOutQuart
| easeInQuint | easeOutQuint | easeInOutQuint
| easeInSine | easeOutSine | easeInOutSine
| easeInExpo | easeOutExpo | easeInOutExpo
| easeInCirc | easeOutCirc | easeInOutCirc
| easeInBack | easeOutBack | easeInOutBack
| easeInElastic | easeOutElastic | easeInOutElastic
```
这部分的贝塞尔曲线参数是我从他的源码中拿过来的和上面的table一一对应
在谷歌控制台中 使用如下样式再点击图例可以看到具体图形运动轨迹: transition: all 1s cubic-bezier(0.46, 0.03, 0.52, 0.96)
 In: [
      [0.550, 0.085, 0.680, 0.530], /* inQuad */
      [0.550, 0.055, 0.675, 0.190], /* inCubic */
      [0.895, 0.030, 0.685, 0.220], /* inQuart */
      [0.755, 0.050, 0.855, 0.060], /* inQuint */
      [0.470, 0.000, 0.745, 0.715], /* inSine */
      [0.950, 0.050, 0.795, 0.035], /* inExpo */
      [0.600, 0.040, 0.980, 0.335], /* inCirc */
      [0.600,-0.280, 0.735, 0.045], /* inBack */
      elastic /* inElastic */
    ],
    Out: [
      [0.250, 0.460, 0.450, 0.940], /* outQuad */
      [0.215, 0.610, 0.355, 1.000], /* outCubic */
      [0.165, 0.840, 0.440, 1.000], /* outQuart */
      [0.230, 1.000, 0.320, 1.000], /* outQuint */
      [0.390, 0.575, 0.565, 1.000], /* outSine */
      [0.190, 1.000, 0.220, 1.000], /* outExpo */
      [0.075, 0.820, 0.165, 1.000], /* outCirc */
      [0.175, 0.885, 0.320, 1.275], /* outBack */
      (a, p) => t => 1 - elastic(a, p)(1 - t) /* outElastic */
    ],
    InOut: [
      [0.455, 0.030, 0.515, 0.955], /* inOutQuad */
      [0.645, 0.045, 0.355, 1.000], /* inOutCubic */
      [0.770, 0.000, 0.175, 1.000], /* inOutQuart */
      [0.860, 0.000, 0.070, 1.000], /* inOutQuint */
      [0.445, 0.050, 0.550, 0.950], /* inOutSine */
      [1.000, 0.000, 0.000, 1.000], /* inOutExpo */
      [0.785, 0.135, 0.150, 0.860], /* inOutCirc */
      [0.680,-0.550, 0.265, 1.550], /* inOutBack */
      (a, p) => t => t < .5 ? elastic(a, p)(t * 2) / 2 : 1 - elastic(a, p)(t * -2 + 2) / 2 /* inOutElastic */
    ]
```
➜ [Built in easing functions examples](http://animejs.com/documentation/#penner)

Usage:

```javascript
anime({
  targets: 'div',
  translateX: 100,
  easing: 'easeOutExpo' // Default 'easeOutElastic'
});
```

Elasticity of Elastic easings can be configured with the `elasticity` parameters:

```javascript
anime({
  targets: 'div',
  translateX: 100,
  easing: 'easeOutElastic',
  elasticity: 600 // Default 500, range [0-1000]
});
```

➜ [Elasticity examples](http://animejs.com/documentation/#elasticity)

### Custom Bézier curves

Define a Bézier curve with an `Array` of 4 coordinates:

```javascript
anime({
  targets: 'div',
  translateX: 100,
  easing: [.91,-0.54,.29,1.56]
});
```

Custom Bézier curves coordinates can be generated here <https://matthewlein.com/ceaser/>

➜ [Custom Bézier curves example](http://animejs.com/documentation/#customBezier)

### Defining custom functions

扩大已经有的动画函数在`anime.easings`里.

```javascript
// Add custom function
anime.easings['myCustomEasingName'] = function(t) {
  return Math.pow(Math.sin(t * 3), 3);
}

// Usage
anime({
  targets: 'div',
  translateX: 100,
  easing: 'myCustomEasingName'
});

// add custom Bézier curve function
anime.easings['myCustomCurve'] = anime.bezier([.91,-0.54,.29,1.56]);

// Usage
anime({
  targets: 'div',
  translateX: 100,
  easing: 'myCustomCurve'
});
```

➜ [Custom easing functions example](http://animejs.com/documentation/#customEasingFunction)

## Helpers

### anime.speed = x

Change all animations speed (from 0 to 1).

```javascript
anime.speed = .5; // Slow down all animations by half of their original speed
```

### anime.running

Return an `Array` of all active Anime instances.

```javascript
anime.running;
```

### anime.remove(target)

Remove one or multiple targets from the animation.

```javascript
anime.remove('.item-2'); // Remove all elements with the class 'item-2'
```

### anime.getValue(target, property)

Get current valid value from an element.

```javascript
anime.getValue('div', 'translateX'); // Return '100px'
```

### anime.path(pathEl)

Create a path Function for motion path animation.<br>
Accepts either a DOM node or CSS selector.

```javascript
var path = anime.path('svg path', 'translateX'); // Return path(attribute)
```

➜ [Motion path example](http://animejs.com/documentation/#motionPath)

### anime.setDashoffset(pathEl)

An helper for line drawing animation.<br>
Sets the 'stroke-dasharray' to the total path length and return its value.

```javascript
anime({
  targets: '.shape path',
  strokeDashoffset: [anime.setDashoffset, 0]
});
```

➜ [Line drawing example](http://animejs.com/documentation/#lineDrawing)

### anime.easings

Return the complete list of built in easing functions

```javascript
anime.easings;
```

### anime.bezier(x1, x2, y1, y2)

Return a custom Bézier curve easing function

```javascript
anime.bezier(x1, x2, y1, y2); // Return function(t)
```

### anime.timeline()

Create a timeline to synchronise other Anime instances.

```javascript
var timeline = anime.timeline();
timeline.add([instance1, instance2, ...]);
```

➜ [Timeline examples](http://animejs.com/documentation/#basicTimeline)

### anime.random(x, y)

Generate a random number between two numbers.

```javascript
anime.random(10, 40); // Will return a random number between 10 and 40
```

====

[MIT License](LICENSE.md). © 2017 [Julian Garnier](http://juliangarnier.com).

Thanks to [Animate Plus](https://github.com/bendc/animateplus) and [Velocity](https://github.com/julianshapiro/velocity) that inspired `anime.js` API, [BezierEasing](https://github.com/gre/bezier-easing) and [jQuery UI](https://jqueryui.com/) for the easing system. [Tim Branyen](https://github.com/tbranyen) For the Promise implementation.
