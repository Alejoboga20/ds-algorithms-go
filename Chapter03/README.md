# Linear Data Structures

A data structure is said to be linear if its elements form a sequence or a linear list. Some of the linear data structures are: Lists, Sets, Tuples, Stacks, Queues, Deques, etc.

## Lists

A list is a collection of ordered elements that are used to store list of items. Unlike array lists, these can expand and shrink dynamically

```go
package main

import "fmt"

func main() {
    var list []int
    list = []int{1, 2, 3, 4, 5}
    fmt.Println(list)
}
```

### Linked Lists

A LinkedList is a sequence of nodes that have properties and a reference to the next node in the sequence. They are not stored in contiguous memory locations, which makes them different from arrays.

To create a linked list, we need to create a Node class and a LinkedList class. The Node class will have a property and a reference to the next node in the sequence. The LinkedList class will have a reference to the head node in the sequence.

```go
// Node class
type Node struct {
  property int
  nextNode *Node
}

// Linked list class
type LinkedList struct {
  headNode *Node
}
```

To interact with the linked list, we can create methods to add, remove, and search for nodes in the sequence.

```go
func (linkedList *LinkedList) AddToHead(property int) {
  var node = Node{}
  node.property = property

  // check if linked list has a head node
  if linkedList.headNode != nil {
    node.nextNode = linkedList.headNode
  }
  linkedList.headNode = &node
}
```

Then we can create a linked list and add nodes to it.

```go
func main() {
  var linkedList = LinkedList{}
  linkedList.AddToHead(1)
  linkedList.AddToHead(3)
  linkedList.AddToHead(5)
}
```
