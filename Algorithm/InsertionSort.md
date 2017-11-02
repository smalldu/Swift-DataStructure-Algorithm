### 插入排序 Insertion Sort

从第二个数开始排序，如果第二个数比第一个小则换位置     第三个数跟第二个比较 如果比第二个大则不动如果比第二个小则换，再和第一个比较 一次计算所有数

```swift
func insertionSort(_ array:[Int])->[Int] {
  var a = array
  for x in 1..<a.count{
    var y = x
    while y>0 && a[y]<a[y-1] {
      a.swapAt(y-1, y)
      y -= 1
    }
  }
  return a
}
```

使用示例： 

```swift
let list = [10,9,0,5,28,-1,98,2,4,8]
let sortedList = insertionSort(list)
print(sortedList)  // 结果： [-1, 0, 2, 4, 5, 8, 9, 10, 28, 98]
```

上面的排序结果没问题，但是我们还可以对速度上进行优化。我们一直在对比然后`swap`，其实我们可以不使用`swap` 
我们将所有的元素进行右移动

```
[ 3, 5, 8, 4 | 6 ]   临时变量记住 4
           *

[ 3, 5, 8, 8 | 6 ]   4<8 8右移动 
        --->
        
[ 3, 5, 5, 8 | 6 ]   4<5 5右边移动
     --->
     
[ 3, 4, 5, 8 | 6 ]   4<3 false  把4放在5的位置 
     *
```


代码：

```swift
func insertionSort1(_ array: [Int])->[Int] {
  var a = array
  for x in 1..<a.count {
    var y = x
    let temp = a[y]
    while y>0 && temp<a[y-1] {
      a[y] = a[y-1]
      y -= 1
    }
    a[y] = temp
  }
  return a
}
```

使用示例：

```swift
let list1 = [10,9,0,5,28,-1,98,2,4,8]
let sortedList1 = insertionSort(list)
print(sortedList1)
```

以上的算法并不是通用的而且只支持从小到大的排序,那么我们来写一个更通用的

```swift
func insertionSort<T>(_ array: [T], _ isOrderBefore: ((T,T) -> Bool) ) -> [T] {
  var a = array
  for x in 1..<a.count {
    var y = x
    let temp = a[y]
    while y>0 && isOrderBefore(temp,a[y-1]){
      a[y] = a[y-1]
      y -= 1
    }
    a[y] = temp
  }
  return a
}
```

使用示例：

```swift 
let list2 = [10,9,0,5,28,-1,98,2,4,8]
let sortedList2 = insertionSort(list2, <)
let sortedList3 = insertionSort(list2, >)

print(sortedList2) // [-1, 0, 2, 4, 5, 8, 9, 10, 28, 98]
print(sortedList3) // [98, 28, 10, 9, 8, 5, 4, 2, 0, -1]
```


最后，更遵循swifty的写法应该是放在extension里

代码
```swift
extension Array{
  func insertionSort(_ isOrderBefore: ((Element,Element) -> Bool))->[Element]{
    var a = self
    for x in 1..<a.count {
      var y = x
      let temp = a[y]
      while y>0 && isOrderBefore(temp,a[y-1]){
        a[y] = a[y-1]
        y -= 1
      }
      a[y] = temp
    }
    return a
  }
}

let list3 = [10,9,0,5,28,-1,98,2,4,8]
print(list3.insertionSort(<))  // [-1, 0, 2, 4, 5, 8, 9, 10, 28, 98]
print(list3.insertionSort(>))  // [98, 28, 10, 9, 8, 5, 4, 2, 0, -1]
```

插入排序在大多数数据已经排序好的集合来说表现非常好，对比较小的数组排序也非常好，因为它有两层循环，所以最慢的时间复杂度是O(2^n)，相比快速排序和合并排序O(nlog n)，他们是专门处理数据量比较大的情况

相比系统的sort，在100元素以内相差非常小，数据量变大O(2^n)就表现的比较差了。

[英文学习地址](https://github.com/raywenderlich/swift-algorithm-club/tree/master/Insertion%20Sort)
[维基百科地址](https://en.wikipedia.org/wiki/Insertion_sort)



















