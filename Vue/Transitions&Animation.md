# Transitions & Animation

## Transition
- 對過渡中切換的class：如果用沒有名字的`<transition>`, 則`v-`是默認前綴; 如果用有`<transition name="my-transition">`, 則
- 在下列情況中可以給任何元素或組件添加進入/離開過渡：
    - `v-if`
    - `v-show`
    - 動態組件
    - 組建根節點
- Transition Classes
如果用沒有名字的`<transition>`, 則`v-`是默認前綴; 
如果用有`<transition name="my-transition">`, 則`v-enter`替換為`my-transition-wnter`
    - `v-enter`: 过渡的开始状态。在元素被插入之前生效，在元素被插入之后的下一帧移除。
    - `v-enter-active`: 过渡生效时的状态。在元素被插入之前生效，在过渡/动画完成之后移除。
    - `v-enter-to`: 过渡的结束状态。在元素被插入之后下一帧生效 (与此同时 v-enter 被移除)，在过渡/动画完成之后移除。
    - `v-leave`: 过渡的开始状态。在离开过渡被触发时立刻生效，下一帧被移除。
    - `v-leave-active`: 过渡生效时的状态。在离开过渡被触发时立刻生效，在过渡/动画完成之后移除。
    - `v-leave-to`: 在离开过渡被触发之后下一帧生效 (与此同时 v-leave 被删除)，在过渡/动画完成之后移除。

- Animations
在animaiton中`v-enter`class在節點插入`DOM`後不會立即刪除, 而是在`animationend`事件觸發時刪除
![](https://cn.vuejs.org/images/transition.png)

- Custom Transition Classes 自定義過渡類名:
`enter-class`
`enter-active-class`
`enter-to-class`
`leave-class`
`leave-active-class`
`leave-to-class`
---
## 參考來源
[animate.css](https://animate.style/) -＠keyframes寫成的函式庫
[Velocity.js](http://velocityjs.org/) -第三方 JavaScript 动画库