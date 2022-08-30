---
layout: single 

title:  "[React] React-Redux project(day29)" 
categories: React
tags: react
toc: true
header:
  teaser: /assets/images/React.jpeg
sidebar: 
---

이제 게시물의 CRUD는 완료가 되었다.

# ADD
![](https://velog.velcdn.com/images/danchoi/post/c56df186-9922-4625-8a28-4717612ae643/image.gif)

```js
// db에 데이터를 넣음
export const __addMusic = createAsyncThunk(
  "music/ADD_MUSIC",
  async (payload, thunkAPI) => {
    try {
      const data = await axios.post("http://localhost:3001/list", payload);
      return thunkAPI.fulfillWithValue(data.data);
    } catch (error) {
      return thunkAPI.rejectWithValue(error);
    }
  }
);
```

```js
const musics = createSlice({
  name: "musics",
  initialState,
  reducers: {},
  extraReducers: {
  // addMusic Thunk
    [__addMusic.pending]: (state) => {
      state.isLoading = true;
    },
    [__addMusic.fulfilled]: (state, action) => {
      state.isLoading = false;
      state.list.push(action.payload);
    },
    [__addMusic.rejected]: (state, action) => {
      state.isLoading = false;
      state.error = action.payload;
    },
    }
    })
```



# UPDATE

![](https://velog.velcdn.com/images/danchoi/post/5dba95da-e472-48f5-a44f-463c2cbc9fcc/image.gif)

```js
//데이터 수정
export const __updateMusic = createAsyncThunk(
  "music/UPDATE_MUSIC",
  async (payload, thunkAPI) => {
    try {
      const data = await axios.patch(
        `http://localhost:3001/list/${payload.id}`,
        payload
      );
      return thunkAPI.fulfillWithValue(data.data);
    } catch (error) {
      return thunkAPI.rejectWithValue(error);
    }
  }
);
```

```js

const musics = createSlice({
  name: "musics",
  initialState,
  reducers: {},
  extraReducers: {
    // updateMusic Thunk
    [__updateMusic.pending]: (state) => {
      state.isLoading = true;
    },
    [__updateMusic.fulfilled]: (state, action) => {
      state.isLoading = false;
      state.list = state.list.map((music) =>
        music.id === action.payload.id ? { ...action.payload } : music
      );
    },
    [__updateMusic.rejected]: (state, action) => {
      state.isLoading = false;
      state.error = action.payload;
    },
  },
});

```



# DELETE

![](https://velog.velcdn.com/images/danchoi/post/369aab81-f0cd-45a4-bf28-37ea514b0c1d/image.gif)

```js
//db내 데이터 삭제
export const __deleteMusic = createAsyncThunk(
  "music/DELETE_MUSIC",
  async (payload, thunkAPI) => {
    try {
      const data = await axios.delete(`http://localhost:3001/list/${payload}`);
      return thunkAPI.fulfillWithValue(payload);
    } catch (error) {
      return thunkAPI.rejectWithValue(error);
    }
  }
);
```

```js
const musics = createSlice({
  name: "musics",
  initialState,
  reducers: {},
  extraReducers: {
    // deleteMusic Thunk
    [__deleteMusic.pending]: (state) => {
      state.isLoading = true;
    },
    [__deleteMusic.fulfilled]: (state, action) => {
      state.isLoading = false;
      state.list = state.list.filter((music) => music.id !== action.payload);
    },
    [__deleteMusic.rejected]: (state, action) => {
      state.isLoading = false;
      state.error = action.payload;
    },
  },
});
```

