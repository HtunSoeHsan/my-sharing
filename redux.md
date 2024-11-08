
![Unidirectional Data Flow in React](https://media2.dev.to/dynamic/image/width=800,height=,fit=scale-down,gravity=auto,format=auto/https://www.exploringreact.com/wp-content/uploads/2020/11/unidirectional.png)

## State Management In React 
- useState
- context
- library (1.Redux, 2., ...)

### Redux data flow ( one way data flow)

![enter image description here](https://www.freecodecamp.org/news/content/images/2022/06/2.png)

![enter image description here](https://d33wubrfki0l68.cloudfront.net/01cc198232551a7e180f4e9e327b5ab22d9d14e7/b33f4/assets/images/reduxdataflowdiagram-49fa8c3968371d9ef6f2a1486bd40a26.gif)

##
## Redux
- React Redux
- Redux Toolkit 

## Redux Toolkit (package of redux)
- install
- Store
- Hook
- Slice

## Setup redux toolkit in project
1. Install
```console
npm i react-redux @reduxjs/toolkit
```
2. Create Store

```js
import { configureStore } from "@reduxjs/toolkit";

// ...

export const store = configureStore({
  reducer: {},
});

// Infer the `RootState` and `AppDispatch` types from the store itself
export type RootState = ReturnType<typeof store.getState>;
// Inferred type: {posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch;
```
3. Create Hook
 ```js
   js import { useDispatch, useSelector } from 'react-redux'
    import type { RootState, AppDispatch } from './store'
    // Use throughout your app instead of plain `useDispatch` and `useSelector`
    export const useAppDispatch = useDispatch.withTypes<AppDispatch>()
    export const useAppSelector = useSelector.withTypes<RootState>() 
 ```
4. Create Slice
   ```js import { createSlice } from '@reduxjs/toolkit'
    import type { PayloadAction } from '@reduxjs/toolkit'
    import type { RootState } from '../../app/store'
    
    // Define a type for the slice state
    interface CounterState {
      value: number
    }
    
    // Define the initial state using that type
    const initialState: CounterState = {
      value: 0,
    }
    
    export const counterSlice = createSlice({
      name: 'counter',
      // `createSlice` will infer the state type from the `initialState` argument
      initialState,
      reducers: {
        increment: (state) => {
          state.value += 1
        },
        decrement: (state) => {
          state.value -= 1
        },
        // Use the PayloadAction type to declare the contents of `action.payload`
        incrementByAmount: (state, action: PayloadAction<number>) => {
          state.value += action.payload
        },
      },
    })
    
    export const { increment, decrement, incrementByAmount } = counterSlice.actions
    
    // Other code such as selectors can use the imported `RootState` type
    export const selectCount = (state: RootState) => state.counter.value
    
    export default counterSlice.reducer
   ```

## Wrap with Provider
```js
    import React from 'react'
    import ReactDOM from 'react-dom'
    import './index.css'
    import App from './App'
    import { store } from './app/store'
    import { Provider } from 'react-redux'
    
    ReactDOM.render(
      <Provider store={store}>
        <App />
      </Provider>,
      document.getElementById('root')
    )
```
### Using redux dev tool extension 

https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd

