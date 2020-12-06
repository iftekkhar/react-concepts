## Mounting -- >

### constructor -->  
1. will get called when new component is created.
2. initializing state & Binding the event handlers
3. DOnt cause side effects ex. HTTP requests
4. Have to call super()
5. only place to directly overwrite state

### static getDerivedStateFromProps( props, state) --> rarely used
1. doesnt have "this" cause its a private method
2. Set the state (When state depends on the props)
3. shouldnot cause sideeffects
4. returns null or object --> That represents the updated state
5. Called verytime a component is rerendered

### render -->
1. only required function
2. pure function
3. Can not change state

###componentDidMount -->
1. Called only once after the componet and all its childern has been rendered
2. Perfect place to cause sideEffects


## Updating

### static getDerivedStateFromProps --> 

###shouldComponentUpdate(nextProp, NextState) --> 
1. It can compare the previous state & props & The next state & Props values & Decide should the components update or not
2. Used for performance optimization
3. SHouldnt call setState or cause sideeffects

### render

### getSnapshotBeforeUpdate (prevProps, prevState) --> rately used

1. Called right before changes from the virtual doms are to be reflected in the Real DOM
2. Used to Capture some information from the dom. ie. user scroll prosition, and return the same position after updating has been done.
3. returns null or a value .. The value will be passed as the third parameter of the next lifecycle method.

### componentDidUpdate(prevProp, PreState, SnapshotValue)
1. called after the rerender is finished.
2. Can cause side effects (Need to compare first)


## Unmounting

### componentWillUnmount()-->
1. Invoked immedieatly before component is unmounted or distroyed
2. Cleanup can be done in this phase


## Error Handeling

### static getDerivedStateFromError-->
1. used to fall back UI useing error boundary

### componentDidCatch(error, info) -->
1. use to log the error


#HOC & Render Props --> Reusable Comp
