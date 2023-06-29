

# 개요

## 사용방법
```js
const section = document.querySelector("#main_content3");
const io = new IntersectionObserver((entries, observer) => {
    entries.forEach((item, index) => {
        if(item.isIntersecting) {
            scrollBy({
                top:item.boundingClientRect.top,
                left:0,
                behavior:"smooth"
            })
            startScrollSwiper();
        } else{
            stopScrollSwiper();
        }
    })
}, {threshold : 0.8}) // 80%로 등장했을 경우
io.observe(section);
```
