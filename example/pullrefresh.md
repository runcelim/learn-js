重叠元素如何冒泡

1. 当一个元素的滚动位置处于其顶端时，做一个下拉手势，将会对元素进行刷新


在touchstart事件中，检测元素的滚动位置是否在其顶端，若是，则记录起始手指位置，并继续
在touchmove事件中，检测当前手指位置和起始位置的相对关系，若是下拉，则进入下拉状态
在下拉状态中，继续监听touchmove事件，并更新UI，通常会拉出一个隐藏的元素，通过其提示用户继续下拉可以刷新
下拉到一定程度，超过阈值，则可以进入Release to Refresh状态，通常也会在UI上做一些提示
在下拉手势结束时，检测下拉程度是否超过阈值，若是，则进行更新，否则恢复原貌


示例 : https://dl.dropboxusercontent.com/u/26978903/scrollz/mobile.html

https://apeatling.com/demos/web-ptr/

pull-to-refresh    --> release-to-refresh  --> refreshing...


检测触摸屏幕的手指何时改变方向: orientationchange 

知识点
1. 滚动条的位置 滚动条到父元素的位置

    Element.scrollTop 

这个Element.scrollTop 属性可以设置或者获取一个元素距离他容器顶部的像素距离。一个元素的 scrollTop 
是可以去计算出这个元素距离它容器顶部的可见高度。
当一个元素的容器没有产生垂直方向的滚动条,那它的 scrollTop 的值默认为0


scrollTop 不为 0 时,正常下拉看本地的最新数据,为 0 时,继续下拉,此时记录下拉距离,超过阈值,提示 释放刷新,手指释放,
此时从服务端取数据

2. 计算 touchMove 距离

touch.pageY  
touch.clientY  

3. TouchEvent.touches

   TouchEvent.targetTouches

注意偏移坐标单位,如果移动端使用 rem 作为布局单位应该如何处理


不能用top，这样效率很低，建议采用CSS3，在拖拽的时候判断拖拽情况使用 transform 的 translate3d 或者 translateY
 （使用3d触发GPU渲染效率好），拖拽结束后判断和初始状态的情况，使用 transition 完成页面平滑过度。建议找些案例的
 JS来看。
