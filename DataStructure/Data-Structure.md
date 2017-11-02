Data-Structure

### 栈

Stack Data Structure 栈 LIFO  后进先出 例如: UINavigation push pop
>push 新增一个元素  peek 查看栈顶元素 pop 移除一个元素

```swift
struct Stack<Element>{
  private var array: [Element] = []
  mutating func push(_ element: Element){
    array.append(element)
  }
  mutating func pop() -> Element? {
    return array.popLast()
  }
  mutating func peek()-> Element?{
    return array.last
  }
  var count: Int{
    return array.count
  }
  var isEmpty: Bool{
    return array.isEmpty
  }
}
```


### 队列

Queue 队列 FIFO 先进先出

```swift
public struct Queue<Element>{
  private var array: [Element] = []
  public var isEmpty: Bool {
    return array.isEmpty
  }
  public var count: Int{
    return array.count
  }
  public mutating func enqueue(_ element: Element){
    array.append(element)
  }
  public mutating func dequeue(_ element: Element)-> Element?{
    if isEmpty {
      return nil
    }else{
      return array.removeFirst()
    }
  }
  public var front: Element? {
    return array.first
  }
}
```























