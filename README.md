# React Concepts
1. If the state of the parerent updates , all of it's children will rerender unless said otherwise ( useing react.memo )
2. unnessary Render : Whre components goes through render phase but not the commit phase .
3. Components can change it's State but not props
4. Create-react-App Creates CSR(Client Side Rendering) - > though with Next.js or Gatsby we can achieve SSR & SSG.
5. Jsx is not not understood by the browser we need bable as the transpiler (Comes pre configured with create-react-app api).
6. We need web pack to bundle everything (Comes pre configured with create-react-app api)
***

## Reacts' Philosophy 
1. To keep every component a pure function
2. One way data binding (Parent -> Child)
***
## When to use: 
1. Web Apps where SEO is not Important (Crawlers cant not craw on CSR websites)
3. Very Fast & Interactive UI is Needed

## React Hooks : 
1. Provides Better Performance. (minifies better)
2. Saves us the from the confusion of the 'this' keyword 
3. Provides a way to use stateful logic. 
4. Does not replace 100% class based components yet the left out methods have very rare usage.
5. Classes & Hooks can be mixed though hooks can not be used inside classes . 
***

### useState():
1. Uses a setter & Getter function to change and access the sate
2. Directly mutating state will create bugs. We need to access the setter function to update the sate. When state is updated react will rerender the compoment everytime.
3. As it uses the setter function, everytime for updating the state it needs to have a unique premitive value or reference to update the state.
4. That is why for premitive type we can change the state directly in setState function but in case of objects & Array we first need to copy it then change it and assign the copied object to the state , because we need to update the object's reference in the setter function to actually update the state.
5. In case of same value provided in the state : 
 	 - a. for initial render : component will not rerender ( will bailout)
	  - b. for re-renders : component will rerender one more time then it will bailout ( it is done to make sure that the "bailout" will not cause any problem. )
6. The initial state argument is used during the initial render and after that when the state has been set by using the setter value the initial value is disregarded.
7. State can be changed in the parent component 
8. From the Child component state or props can not be changed but we can pass a callback function fromt he child to change the state of it's parent
9. The setter function is a Async Function 
***

### useReducer()
1. more suited for managing state objects that contain multiple sub-values.
***

### useCallback() & useMemo()
These two hooks are provided for optimizing the performance . we need to remember that when optimizing the render of one component react will also skip rerendering the components entire subtree because it's effectively stoping the default behaviour. However if the prop of the parent component changes (therefore the state of the greatparent is changed then the default behavious will be envoked to make sure every component is synced .  

1. useCallback()
	- Returns a memoized Callback.
	- When ever we pass a callback function with every rerender of it's parent a new reference of that function is created . That is why the component having that callback function will rerender even if the props or state to that children is not changed. 
	- To optimize this we can cache a function using useCallback hook, wich will take a dependency array. So whenever we need to cache a function we can use the useCallback hook.
1. useMemo()
	- Returns a memoized value of a function.
	- Pass a “create” function and an array of dependencies. useMemo will only recompute the memoized value when one of the dependencies has changed. This optimization helps to avoid expensive calculations on every render.
	- usefull when we need to memorize a value of an expensive function
	- So whenever we need to cache a function's value we can use the useCallback hook.

``` javascript
useCallback(fn, deps) is equivalent to useMemo(() => fn, deps).
```

### React.memo:
When The the parent component rerenders all of it's child will also rerender . To optimize this we can use React.memo and pass the child component. React.memo will performe a shallow comparison (as deep comparison is expensive) between the two props and update only if the props has changed. But it is advised not to use react.memo everytime because if it is found in the shallow comparison that the props has changed react will perform a deep comparison and rerender. 

"If you are familiar with React.PureComponent then React.memo is quite straightforward as it is exactly similar to React.PureComponent. We use React.PureComponent with class component while React.memo works with functional components. It is not a hook"
***



##Mounting -- >

###constructor -->  
1. will get called when new component is created.
2. initializing state & Binding the event handlers
3. DOnt cause side effects ex. HTTP requests
4. Have to call super()
5. only place to directly overwrite state

###static getDerivedStateFromProps( props, state) --> rarely used
1. doesnt have "this" cause its a private method
2. Set the state (When state depends on the props)
3. shouldnot cause sideeffects
4. returns null or object --> That represents the updated state
5. Called verytime a component is rerendered

###render -->
1. only required function
2. pure function
3. Can not change state

###componentDidMount -->
1. Called only once after the componet and all its childern has been rendered
2. Perfect place to cause sideEffects


##Updating

###static getDerivedStateFromProps --> 

###shouldComponentUpdate(nextProp, NextState) --> 
1. It can compare the previous state & props & The next state & Props values & Decide should the components update or not
2. Used for performance optimization
3. SHouldnt call setState or cause sideeffects

###render

###getSnapshotBeforeUpdate (prevProps, prevState) --> rately used

1. Called right before changes from the virtual doms are to be reflected in the Real DOM
2. Used to Capture some information from the dom. ie. user scroll prosition, and return the same position after updating has been done.
3. returns null or a value .. The value will be passed as the third parameter of the next lifecycle method.

###componentDidUpdate(prevProp, PreState, SnapshotValue)
1. called after the rerender is finished.
2. Can cause side effects (Need to compare first)


##Unmounting

###componentWillUnmount()-->
1. Invoked immedieatly before component is unmounted or distroyed
2. Cleanup can be done in this phase


##Error Handeling

###static getDerivedStateFromError-->
1. used to fall back UI useing error boundary

###componentDidCatch(error, info) -->
1. use to log the error


#HOC & Render Props --> Reusable Comp

