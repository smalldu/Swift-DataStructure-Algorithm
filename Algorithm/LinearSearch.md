### 线性检索  Linear Search 

其实就是普通的 循环便利检索出对应的下标

```swift
func linearSearch<T: Equatable>(_ array: [T], _ object: T) -> Int? {
  for (index, obj) in array.enumerated() where obj == object {
    return index
  }
  return nil
}
```


使用示例：

```swift
let array = [5, 2, 4, 7]
linearSearch(array, 2)  
```


时间复杂度O(n) 

这个很简单，也是最容易想到的方式。

