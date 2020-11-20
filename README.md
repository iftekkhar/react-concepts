# React Concepts

## React Philosophy 
1. If the state of the parerent updates , all of it's children will rerender unless said otherwise ( using memo or callback hook)
2. unnessary Render : Whre components goes through render phase but not the commit phase .
2. Components can change it's State but not props


## React Hooks : 
1. Provides Better Performance.
2. Saves us the from the confusion of the 'this' key word 

### useState():
1. Uses a setter & Getter function to change and access the sate
2. Directly mutating state will create bugs. We need to access the setter function to update the sate. When state is updated react will rerender the compoment everytime.
3. As it uses the setter function, everytime for updating the state it needs to have a unique premitive value or reference to update the state.
4. That is why for premitive type we can change the state directly in setState function but in case of objects & Array we first need to copy it then change it and assign the copied object to the state , because we need to update the object's reference in the setter function to actually update the state.
5. In case of same value provided in the state : 
  a. for initial render : component will not rerender ( will bailout)
  b. for re-renders : component will rerender one more time then it will bailout ( it is done to make sure that the "bailout" will not cause any problem. )
6. The initial state argument is used during the initial render and after that when the state has been set by using the setter value the initial value is disregarded.
7. State can be changed in the parent component 
8. From the Child component state or props can not be changed but we can pass a callback function fromt he child to change the state of it's parent
9. It's a Async Function 

### React.memo:
When The the parent component rerenders all of it's child will also rerender . To optimize this we can use React.memo and pass the child component. React.memo will performe a shallow comparison (as deep comparison is expensive) between the two props and update only if the props has changed. But it is advised not to use react.memo everytime because if it is found in the shallow comparison that the props has changed react will perform a deep comparison and rerender. 
