### Binary Search 二分法检索

快速找到数组中的某个元素 ，其实系统已经有`index(of:)`方法来帮我们检索数组的元素

```swift
let numbers = [11,58,3,21,34,54,66,-9,98,765]
numbers.index(of: 98) // 8
```

系统的`index(of:)`用的顺序查找，代码大概是这样的,不过系统是放在Extension中

```swift
func linearSearch<T: Equatable> (_ a: [T],_ key: T)-> Int?{
  for i in 0..<a.count{
    if a[i] == key{
      return i
    }
  }
  return nil
}
```


没有什么特殊的 就是一层循环，但是在最差的情况下，我们需要遍历整个array，如果你的数组非常大，速度将会变得很慢，我们可以使用经典的二分法提升速度，不断的从中间分隔数组知道查找的value，时间复杂度O(log n)1,000,000个元素的数组只需要20步就可以找到value，十亿元素只需要30步，但是我们好像也不需要这么大的数组吧。。

听起来很酷，但是有一个缺点，这个数组必须是已经排序好的。

流程 先取数组中间的值然后和两边对比大小 决定取那一半，不断重复。使用了递归的思想

看下代码：

```swift
func binarySearch<T: Comparable>(_ a: [T], key: T, range: Range<Int>) -> Int? {
  if range.lowerBound >= range.upperBound{
    return nil
  } else {
    let midIndex = range.lowerBound + (range.upperBound-range.lowerBound)/2
    if a[midIndex] > key{
      return binarySearch(a, key: key, range: range.lowerBound..<midIndex)
    }else if a[midIndex]<key{
      return binarySearch(a, key: key, range: midIndex..<range.upperBound)
    }else{
      return midIndex
    }
  }
}
```

使用示例：

```swift
// 数组必须是排序好的 否则二分法将无法正常工作
let numbers1 = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67]
let index3 = binarySearch(numbers1, key: 53, range: 0 ..< numbers1.count)
print(index3) // Optional(15)
```


我们也可以不适用递归，而是用迭代的方式

```swift
func binarySearch1<T: Comparable>(_ a: [T],key: T) -> Int?{
  var lowerBounds = 0
  var upperBounds = a.count
  while lowerBounds<upperBounds {
    let midIndex = lowerBounds+(upperBounds-lowerBounds)/2
    if a[midIndex] == key {
      return midIndex
    }else if a[midIndex] < key{
      lowerBounds = midIndex - 1
    }else{
      upperBounds = midIndex
    }
  }
  return nil
}
```


当然我们也可以直接放再扩展中

```swift
extension Array{
  func binaryIndex(of _ key: Element) -> Int? {
    var lowerBounds = 0
    var upperBounds = a.count
    while lowerBounds<upperBounds {
      let midIndex = lowerBounds+(upperBounds-lowerBounds)/2
      if a[midIndex] == key {
        return midIndex
      }else if a[midIndex] < key{
        lowerBounds = midIndex - 1
      }else{
        upperBounds = midIndex
      }
    }
    return nil
  }
}
```


学习地址：https://github.com/raywenderlich/swift-algorithm-club/tree/master/Binary%20Search
维基百科地址：https://en.wikipedia.org/wiki/Binary_search_algorithm







