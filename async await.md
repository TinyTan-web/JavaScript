## understanting of async/await

​	async/ awati is **actually the syntax sugar of Generator **.The effect it can achieve can be realized by then chain. It was developed to optimize the then chain. Literally, async is the abbreviation of  " asynchronous ", await is waiting, so it is easy to understand that **async is used to declare that a function is asynchronous**, and **await is used to wait for an asynchronous method to complete**. Of course, the syntax forces that **await can only appear in the async function.**



​	Therefore,  **an async function returns a Promise object**, async funtions, including function statements, function expressions, and  Lambda expresions,all return a Promise object. If literal value is returned from function, async wraps this value with Promise.resolve(), converting it into a Promise object.



​	An async function returns a Promise obejct.Therefore, when it's not possible to use await at the outermost level to obtain its return value, the appropriate approach is to use the origin method: handling the Promise object with a then() chain.when if the async function does not return a value? It is easy to image that it will return **Promise.resolve(undefined)；**

​	Think about the characteristics of Promise - namely, their non-blocking nature - executing an async function without await results in its immediate execution, returning a Promise object without blocking subsequent statements. This behavior is consistent with functions that return a Promise object.



​	**note:** Promise.resolve(x) can be viewed as a shorthand for new Promise(resolve => resolvep(x) )。**It is used to quickly wrap literal objcts or other objects into Promise instances.  **
