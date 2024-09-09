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

To interact with the linked list, we can create methods to add, iterate, remove, and search for nodes in the sequence.

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


func (linkedList *LinkedList) IterateList() {
  var node *Node

  for node = linkedList.headNode; node != nil; node = node.nextNode {
    fmt.Println(node.property)
  }
}

func (linkedList *LinkedList) LastNode() *Node {
  var node *Node
  var lastNode *Node

  for node = linkedList.headNode; node != nil; node = node.nextNode {
    if node.nextNode == nil {
      lastNode = node
    }
  }

  return lastNode
}


func (linkedList *LinkedList) AddToEnd(property int) {
  var lastNode *Node

  var node = Node{
    property: property,
    nextNode: nil,
  }

  lastNode = linkedList.LastNode()

  if lastNode != nil {
    lastNode.nextNode = &node
  } else {
    // if linked list is empty
    linkedList.headNode = &node
  }
}

func (linkedList *LinkedList) NodeWithValue(property int) *Node {
  var node *Node
  var nodeWith *Node

  for node = LinkedList.headNode; node != nil; node = node.nextNode {
    if node.property == property {
      nodeWith = node
      break
    }
  }

  return nodeWith
}

func (linkedList *LinkedList) AddAfter(nodeProperty int, property int) {
  var node = Node{
    property: property,
    nextNode: nil,
  }

  var nodeWith = linkedList.NodeWithValue(nodeProperty)

  if nodeWith != nil {
    node.nextNode = nodeWith.nextNode
    nodeWith.nextNode = &node
  }
}
```

Then we can create a linked list and add nodes to it.

```go
func main() {
  var linkedList = LinkedList{}
  linkedList.AddToHead(1)
  linkedList.AddToHead(3)
  linkedList.AddToHead(5)

  linkedList.IterateList()
  fmt.Println(linkedList.LastNode().property)
}
```

### Doubly Linked Lists

In a doubly linked list, each node has a reference to the next and previous node in the sequence. This allows for easier traversal of the list in both directions.

```go
// Node class
type Node struct {
  property int
  nextNode *Node
  previousNode *Node
}

// Doubly Linked list class
type DoublyLinkedList struct {
  headNode *Node
}
```

To interact with the doubly linked list, we can create methods to add, iterate, remove, and search for nodes in the sequence.

```go
func (doublyLinkedList *DoublyLinkedList) AddToHead(property int) {
  var node = Node{
    property: property,
    nextNode: nil,
    previousNode: nil,
  }

  if doublyLinkedList.headNode != nil {
    node.nextNode = doublyLinkedList.headNode
    doublyLinkedList.headNode.previousNode = &node
  }
  doublyLinkedList.headNode = &node
}

func (doublyLinkedList *DoublyLinkedList) AddAfter(nodeProperty int, property int) {
  var node = Node{
    property: property,
    nextNode: nil,
    previousNode: nil,
  }

  var nodeWith = doublyLinkedList.NodeWithValue(nodeProperty)

  if nodeWith != nil {
    node.nextNode = nodeWith.nextNode
    node.previousNode = nodeWith
    nodeWith.nextNode = &node
  }
}

func (doublyLinkedList *DoublyLinkedList) AddToEnd() {
  var lastNode *Node

  var node = Node{
    property: property,
    nextNode: nil,
    previousNode: nil,
  }

  lastNode = doublyLinkedList.LastNode()

  if lastNode != nil {
    lastNode.nextNode = &node
    node.previousNode = lastNode
  } else {
    doublyLinkedList.headNode = &node
  }

}

func (doublyLinkedList *DoublyLinkedList) NodeBetweenValues(firstProperty int, secondProperty int) *Node {
  var node *Node
  var nodeWith *Node

  for node = doublyLinkedList.headNode; node != nil; node = node.nextNode {
    if node.previousNode != nil && node.nextNode != nil {
      if node.previousNode.property == firstProperty && node.nextNode.property == secondProperty {
        nodeWith = node
        break
      }
    }
  }

  return nodeWith
}

```

There are some methods that are the same for both singly and doubly linked lists, such as `IterateList`, `LastNode`, and `NodeWithValue`. Even the declaration of the linked list is the same for both singly and doubly linked lists, the only difference is the type of the head node.

```go
func main() {
 var doublyLinkedList DoublyLinkedList
 doublyLinkedList = DoublyLinkedList{}
 doublyLinkedList.AddToHead(1)
 doublyLinkedList.AddToHead(3) doublyLinkedList.AddToEnd(5)
 doublyLinkedList.AddAfter(1,7)
 fmt.Println(doublyLinkedList.headNode.property)
 var node *Node
 node = doublyLinkedListt.NodeBetweenValues(1,5)
 fmt.Println(node.property)
}
```
