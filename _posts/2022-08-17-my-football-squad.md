--- 
layout: single 
title:  "[React] my-football-squad (day17)" 
categories: React
tags: react
toc_sticky: true
header:
  teaser: "https://velog.velcdn.com/images/danchoi/post/f878b56d-be1a-4b6c-927b-da886ab9bfa6/image.jpeg"
sidebar: 
    nav: "main"
---

![post-thumbnail](https://velog.velcdn.com/images/danchoi/post/f878b56d-be1a-4b6c-927b-da886ab9bfa6/image.jpeg)

이전에 만들어 본 Todo List를 복습하고자 조금 더 많은 input들을 첨가하고 응용해 새로운 리엑트 프로젝트를 만들어 보았다.

## 이름하여
# my-football-squad
![](https://media.giphy.com/media/p3cgmVTX2kcdV3GUUj/giphy.gif)
![](https://velog.velcdn.com/images/danchoi/post/564ee544-333e-4034-a914-a7bbdaf92835/image.png)


Form 컴포넌트의 input란에 축구선수를 입력하면 포지션별로 나눠 Lists 컴포넌트에 출력해준다.
또한 포지션별로 배치된 선수의 수를 파악해 4-4-2,4-3-3 등 포메이션또한 출력해준다.

## Player
![](https://velog.velcdn.com/images/danchoi/post/270437ba-f4e3-463a-948c-1b6c0ac50720/image.png)

직접 <input type='text' placeholder="player name"/>로 입력받을 경우 출력시 Player 요소들의 통일성을 위해 toUpperCase()메서드를 사용하여 대문자로 통일해주었다.

~~~jsx
const Player = ({ list, remove }) => {
  const { id, firstname, lastname, position, club, nationality } = list;
  return (
    <div className="player">
      <div className={position}>
        <h4>{position}</h4>
      </div>
      <h4>
        Name: {firstname.toUpperCase()} {lastname.toUpperCase()}
      </h4>
      <h4>Club: {club.toUpperCase()}</h4>
      <h4>Nationality: {nationality}</h4>
      <hr></hr>
      <button onClick={() => remove(id)}>Delete</button>
    </div>
  );
};
~~~

## Lists
![](https://velog.velcdn.com/images/danchoi/post/90b74069-584a-4706-b619-4b2f4bc8a54f/image.png)

filter()메서드를 사용해 입력한 포지션 별로 등록시 배치되는 위치를 나누어주었고 List 상단에 수비수, 미드필더, 공격수별로 등록된 Player 수를 더해 포메이션을 출력한다.
~~~jsx
const Lists = ({ lists, remove }) => {
  return (
    <div className="field">
      <h2>Your Squad is
      </h2>
      <h1>
        {lists.filter((list) => list.position === "DF").length}-
        {lists.filter((list) => list.position === "MF").length}-
        {lists.filter((list) => list.position === "FW").length}
      </h1>
      <h2>Formation
      </h2>
     
      <div className="position">
        {lists
          .filter((list) => list.position === "FW")
          .map((list, idx) => (
            <Player list={list} key={idx} remove={remove} />
          ))}
      </div>
      
      <div className="position">
        {lists
          .filter((list) => list.position === "MF")
          .map((list, idx) => (
            <Player list={list} key={idx} remove={remove} />
          ))}
      </div>
      
      <div className="position">
        {lists
          .filter((list) => list.position === "DF")
          .map((list, idx) => (
            <Player list={list} key={idx} remove={remove} />
          ))}
      </div>
      
      <div className="position">
        {lists
          .filter((list) => list.position === "GK")
          .map((list, idx) => (
            <Player list={list} key={idx} remove={remove} />
          ))}
      </div>
    </div>
  );
};
~~~


## Form
![](https://velog.velcdn.com/images/danchoi/post/294848e3-f6b7-4837-86f9-f27eb40af011/image.png)
<input type='text' placeholder="input type='text'"> 뿐만 아니라 
          <label>position: </label><input type="radio" name="position"/><label for="forward">Forward</label><input type="radio" name="position"/><label for="midfilder">Midfilder</label><input type="radio" name="position"/><label for="defender">Defender</label><input type="radio" name="position"/><label for="goalkeeper">Goalkeeper</label>
          
및 select, option![](https://velog.velcdn.com/images/danchoi/post/1c3c617a-d34b-4268-a7ba-0aef81472a82/image.png)을 추가하여 값을 받아온다.
```jsx
const Form = ({
  firstname,
  lastname,
  club,
  nationality,
  onChangeHandler,
  onSubmitHandler,
}) => {
  return (
    <div>
      <form>
        <div className="form">
          <label>first name: </label>
          <input
            name="firstname"
            type="text"
            placeholder="first name"
            value={firstname}
            onChange={onChangeHandler}
          />
          <label> last name: </label>
          <input
            name="lastname"
            type="text"
            placeholder="last name"
            value={lastname}
            onChange={onChangeHandler}
          />
        </div>
        <div className="form">
          <label>position: </label>
          <input
            type="radio"
            id="forward"
            name="position"
            value="FW"
            onChange={onChangeHandler}
          />
          <label for="forward">Forward</label>
          <input
            type="radio"
            id="midfilder"
            name="position"
            value="MF"
            onChange={onChangeHandler}
          />
          <label for="midfilder">Midfilder</label>
          <input
            type="radio"
            id="defender"
            name="position"
            value="DF"
            onChange={onChangeHandler}
          />
          <label for="defender">Defender</label>
          <input
            type="radio"
            id="goalkeeper"
            name="position"
            value="GK"
            onChange={onChangeHandler}
          />
          <label for="goalkeeper">Goalkeeper</label>
        </div>
        <div className="form">
          <label>Club: </label>
          <input
            name="club"
            type="club"
            placeholder="club"
            value={club}
            onChange={onChangeHandler}
          />
        </div>
        <div className="form">
          <label for="nationality">Nationality: </label>
          <select><option>Choose Nationality</option></select>
        </div>
        <div className="form">
          <button id="submit" type="submit" onClick={onSubmitHandler}>
            register
          </button>
        </div>
      </form>
    </div>
  );
};
```

그리하여 결과물은 이렇다.
![](https://velog.velcdn.com/images/danchoi/post/744055f9-cd78-43b5-aca5-2db6ff687b13/image.gif)
![](https://media.giphy.com/media/uWujshK7HCgr0nS0PT/giphy.gif)

직면한 문제:
position의 input type을 radio로 설정하니 submit이후 모든 항목들이 초기화될 때 radio만 초기화가 되지 않는 상황이 발생하였다.
 ![](https://velog.velcdn.com/images/danchoi/post/5ac396c7-481a-43eb-a2a4-0c3d76df5ac5/image.png)

![](https://velog.velcdn.com/images/danchoi/post/f705b30c-c51d-478d-b900-f7c972cd285d/image.png)
혼자 여러 검색을 하며 checked:false를 주기 위해 노력을 했으나 결국 해결하지 못하여 기술매니저님께 여쭤보았다.
그로 인해 알게된 결론은 input태그 안에 직접
~~~js
 <input checked={position==='FW'?true:false}
            type="radio"
            id="forward"
            name="position"
            value="FW"
            onChange={onChangeHandler}
          />
~~~
checked 값을 넣고 그에 해당하는 value를 삼항연산자를 통해 반환해 주면 submit 시에 초기화가 된다는 것이었다.


후기:
1. 메서드를 사용할 때 소괄호 중괄호를 혼동하지 말자.미세한 차이(오류)가 발목잡는다.
2. 공식문서를 잘 활용하자.
3. 해결해보고 안되면 질문을 하자(소심하면 안됨)
