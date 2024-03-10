## Bidirectional data binding

We can use `Object.defineProperty` to implement bidirectional data binding. It can pass three parameters.



- obj: the object on which to define the property.
- prop: a string or Symbol specifying the key of the property to be defined or modified.
- descriptor: the descriptor for the property being defined or modified.



There are two main types in property descriptor: data descriptors and accessor descriptors.
Both data descriptor and accessor descriptor are object, they share the following optional keys:
`configurable` :
when this is set to false:



- the type of this property cannnot be changed between data property and accessor property, and 
-  the property may not be deleted, and 
-  other attributes of its descriptor cannot be changed.
  Defaults to false. 



`enumerable` :



- if it's true, meaning this property is enumerable. Defaults to false.



Date descriptor has other following optional keys:
`value`: The value associated with the property. Defaults to undefined.
`writable`:  If it's true, the associated value with property can be modified by assignment operator. Defaults to false.



Accessor descriptor has the following optional keys:
`get`: A function which serves as a getter for the property. It will be called when access this property. Defaults to undefined.
`set`: A function which serves as a setter for the property. It will be called when this property is assigned a value. Defaults to undefined.



Object property descriptors can be either data descriptors (value, writable) or access descriptors (get, set), but there should not be both descriptors. If the property descriptors has both [value or writable] and [get or set] keys, an exception is thrown.



```plain
  let obj = {}
  let input = document.getElementById('input')
  let span = document.getElementById('span')
  // 数据劫持
  Object.defineProperty(obj, 'text', {
  configurable: true,
  enumerable: true,
  get() {
  return input.value;
  },
  set(newVal) {
  console.log('数据更新了')
  input.value = newVal;
  span.innerHTML = newVal;
  }
  })
  // 输入监听
  input.addEventListener('keyup', function(e) {
  obj.text = e.target.value
})
```



In this code. we define an empty object named obj. We can use getter and setter of object.definedProperty() to read and assign the property value. When we access the text property, the get function will be invoked,  returning the value of input. By adding an event listener on the input, we can get the value of input when the value changed, and set the value of text property to the target value. So the set function will be invoked when the value of text property is modified, and the new modified value will be passed in the set function, so inside the set function, we set the value of input and the innerHTML of span to the new value. In this process , we can implement bidirectional data binding.