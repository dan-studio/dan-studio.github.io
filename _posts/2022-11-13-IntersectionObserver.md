---
layout: single 

title:  "Intersection Observer"  
categories: javascript
createDate: "2022-11-13"
tags: javascript
toc: true
header: true
sidebar: true
---

Intersection Observer란 타겟 요소와 상위 요소 또는 최상위 Document의 Viewport 사이의 Intersection 내의 변화를 비동기적으로 관찰하는 방법이다. 

Intersection 정보는 다음과 같은 이유때문에 필요하다. 

* 페이지가 스크롤 되는 도중에 발생하는 이미지나 다른 컨텐츠의 지연 로딩. 
* 스크롤 시에, 더 많은 컨텐츠가 로드 및 렌더링되어 사용자가 페이지를 이동하지 않아도 되게 하는 infinite-scroll을 구현하기 위해 
*  사용자에게 결과가 표시되는 여부에 따라 작업이나 애니메이션을 수행할지 여부를 결정.

```js
const useElementOnScreen = (options) => {
  const target = useRef();
  const [isLoaded, setIsLoaded] = useState(false);
  
  const callbackFunction = (entries) => {
    const [entry] = entries
    setIsLoaded(entry.isIntersecting);
  };
  useEffect(() => {
    const observer = new IntersectionObserver(callbackFunction, options);
    if (target.current) 
    setTimeout(()=>{
      observer.observe(target.current);
    },1500)
    return () => {
      if (target.current) observer.unobserve(target.current);
    };
  }, [target, options]);

  return [target, isLoaded]

};
```

파이널 프로젝트를 진행하면서는 useElementOnScreen이라는 custom hook을 만들고 내부에  useEffect를 통해 IntersectionObserver을 생성해 useRef로 지정한 DOM이 observer에 관측이 되면 useState의 상태가 true로 변하여 해당 상태 변화를 통해 데이터의 페이지를 1씩 증가시키는 방식으로 무한스크롤을 구현하였다.