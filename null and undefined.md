### null和undefined区别

#### The difference between null and underfind

First of all , Undefined and Null are both basic data types. Each of these two data types has only one value, which is undefined and null



undefined means undefined, which null means empty object. when a general variable is declared but not ye defined, it will return undefined. null is mainly used to assgin values to variables that may return objects as initialization.



Undefined is not a reserved word in JavaScript ,which meas that it can be used as a variable name, but this approach is vary dangerous as it can affect the judgment of the undefined value . We can obtain secure undefined values through some methods, such as void 0.



When using typeof to judge these two types, Null typing will return  “Object”，which is a historiacl problem. Return true when using a double equal sign to compare two types of values,  and return false when using a triple sign.



### Sum:

First of all , Undefined and null are both basic data types.

underfined means underfined , while null means empty object. 

when a general variable is declared but not yet defined, it will return undefined. Null is mainly used to assign values that may return object as initiazation.