# Redux

- Redux - complex state managment tool with a single store as CDS (central data store)
- Reducers - manages the state and returns the newly updated state
- Actions - actions have 2 property types:
	- Unique identifier
	- Payload with data
- Dispatch - used to send actions to update the data

## Setup
1. After React app is created, install redux and react-redux libraries (`npm install redux react-redux`)
1. Create a folder in `/src` and title it `store`
2. Add new file names `index.js`
3. Inside `index.js`:
```
import {createStore} from 'redux'

const reducerFn = (state, action) => {

}

const store = createStore(reducerFn)
```
