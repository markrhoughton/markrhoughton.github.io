---
title: "Closures"
date: 2022-09-26T17:53:03+01:00
draft: false
tags:
    - swift
---

When writing functions that expect functions as arguments
```
func calculator(numberA: Int, numberB: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(numberA, numberB)
}
```

rather than writing the expected argument as an explicit named function

```
func addOperation(nA: Int, nB: Int) -> Int {
    return nA + nB
}
```

and calling it like
```
calculator(numberA: 8, numberB: 3, operation: addOperation)
```

we can pass it as a closure instead
```
calculator(numberA: 8, numberB: 3, operation: { (nA: Int, nB: Int) -> Int in
    return nA + nB
})
```

which can be simplified in a number of ways.
We can remove the unnecessary return statement
```
calculator(numberA: 8, numberB: 3, operation: { (nA: Int, nB: Int) -> Int in
    nA + nB
})
```

and drop the argument label for final argument closures
```
calculator(numberA: 8, numberB: 3) { (nA: Int, nB: Int) -> Int in
    nA + nB
}
```

then allow swift to infer the types
```
calculator(numberA: 8, numberB: 3) { (nA, nB) -> Int in
    nA + nB
}
calculator(numberA: 8, numberB: 3) { (nA, nB) in
    nA + nB
}
calculator(numberA: 8, numberB: 3) { (nA, nB) in nA + nB }
```

Finally we can use anonymous arguments
```
calculator(numberA: 8, numberB: 3) { $0 + $1 }
```

These simplifications show how straightforward it would be to extend this to other operations
```
calculator(numberA: 6, numberB: 5) { $0 - $1 }
calculator(numberA: 9, numberB: 23) { $0 * $1 }
calculator(numberA: 15, numberB: 4) { $0 / $1 }
```


A few examples of closures in practice can be seen using the `map` function
```
let someArray = [7,3,2,6,4,8,3,9]


print(someArray.map({$0 + 1}))
print(someArray.map({"\($0) cakes"}))

let otherArray = someArray.map({ item in
    (7*item + 4) * 3
})
print(otherArray)
```


