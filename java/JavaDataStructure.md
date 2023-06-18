
**Table of Content**
- [Collection Interface](#collection-interface)
  - [Basics](#basics)
  - [List Interface](#list-interface)
    - [ArrayList](#arraylist)
    - [Vector](#vector)
    - [Stack](#stack)
    - [LinkedList](#linkedlist)
  - [Queue Interface](#queue-interface)
    - [Queue Interface](#queue-interface-1)
      - [Deque Interface](#deque-interface)
    - [ArrayDeque](#arraydeque)
    - [PriorityQueue](#priorityqueue)
  - [Set Interface](#set-interface)
    - [HashSet](#hashset)
    - [LinkedHashSet](#linkedhashset)
    - [SortedSet Interface](#sortedset-interface)
      - [NavigableSet Interface](#navigableset-interface)
        - [TreeSet](#treeset)
- [Map Interface](#map-interface)
  - [HashMap](#hashmap)
    - [LinkedHashMap](#linkedhashmap)
  - [HashTable](#hashtable)
  - [Sorted Map Interface](#sorted-map-interface)
    - [Navigable Map Interface](#navigable-map-interface)
      - [TreeMap](#treemap)


# Collection Interface

![DS](https://i.ytimg.com/vi/GdAon80-0KA/maxresdefault.jpg)

## Basics

**Dynamic Array**: 
Has a initial array, and when it fills all the elements, it creates another array and copy all of the elements into new array. the newly created array is 50% bigger than old one. the cost of grow is `O(n)`.

- adding is usually constant. if grows `linear O(n)`
- removing is `linear o(n)`.
- getByIndex is Constant `O(1)`.
- traverse is `linear o(n)`, but because it use a sequential memory address, it is fast, and use cpu cache.


**LinkedList**: 
In LinkedList Adding has constant complexity. Almost every other operation needs traverse including get(index), remove(element), remove(index), add(index,element), traverse complexity is o(n).

- adding is constant `O(1)`.
- traverse is o(n) but because it has random memory address. it do not use cache, and it has a performance overhead.


## List Interface

### ArrayList
it use Dynamic List under the hood.

### Vector
Vector also use dynamic list under the hood. but Vector is thread safe, also its grow factor is 100%.

therefor it has a performance overhead to handle synchronized.

### Stack
Stack extends Vector.

### LinkedList
- It implement a Doubly Linked List.
- It also implement `Deque`, we can use this class for Stack, and Queue.

## Queue Interface

### Queue Interface
- add
- **offer**: offer use add under the hood.
- **poll**: return current value and remove it from queue, if queue is empty returns `null`.
- remove: return current value and remove it from queue, if queue is empty return `exception`.
- **peak**: return current value, if queue is empty returns `null`.
- element: return current value, if queue is empty return `exception`.

#### Deque Interface

add
- offerFirst()
- offerLast()
- addFirst()
- addLast()
- push > addFirst()

remove

- pollFirst()
- pollLast()
- removeFirst()
- removeLast()
- pop() > removeFirst()

read

- peekFirst()
- peekLast()
- getFirst()
- getLast()

We can use `LinkedList` or `ArrayDeque` as Solid implementation of Queue. `LinkedList` is a common choose.

For Stack: We have `LinkedList`, `Stack`, `ArrayDeque`. but normally use `stack`.

### ArrayDeque
- ArrayDeque implements DynamicArray.
- grow factor of 50%

### PriorityQueue
- PriorityQueue implements DynamicArray.
- grow factor of 50%
- the object should implement `Comparable` interface. (`Natural Ordering`)
- we can give a custom comparator by implementing `Comparator` interface. (`Total Ordering`)
- if we give comparator and our object implements comparable, always comparator is preferred.

## Set Interface
- Set does not accept duplicated element.
- containsAll(Collection): check if set has all elements
- addAll(collection): union
- removeAll(collection b): difference
- retainAll(collection): intersection
- clear()


### HashSet

- Use `HashMap`.
- Does not keep any order, random order.
- use `hashCode` and `equals`. We have to override on classes.

### LinkedHashSet
- Use `LinkedHashMap`.
- Keep insertion order.
- Has a bit overhead, because it need to keep order links.

### SortedSet Interface

- element are sorted either by natural ordering or total ordering.
- it gets comparator in constructor.

#### NavigableSet Interface

- pollFirst, poll Last
- ceiling, floor: equal or greater/lower
- higher, lower: strictly greater/lower

##### TreeSet

- use `TreeMap`.


# Map Interface

**Map properties:**

- Defines mapping from keys to values (key/value pair is `Entry`).
- All keys are `unique`.
- both keys and values must be `object`.
- it can be viewed as collection via a `keySet`, a `valueSet` or a `EntrySet`
- use `hashCode` and `equals`.
  
**Map Interface**:
  
- put(key,value)
- get(key)
- remove(key)
- containsKey(key)
- containsValue(value)

bulk operation:
- putAll
- keySet()
- values()
- entrySet()

## HashMap

- unordered
- not thread-safe
- one null key

### LinkedHashMap

- ordered
- maintains order in access order
- ordering can be specified in constructor

## HashTable

- unordered
- thread-safe - comes with performance penalty.
- no null key


## Sorted Map Interface

- Keys are sorted, either natural ordering or total ordering
- firstKey(), lastKey()
  
### Navigable Map Interface

- pollFirstEntry, pollLastEntry
- firstEntry, lastEntry
- ceilingEntry, floorEntry
- higherEntry, lowerEntry

#### TreeMap

- Uses `balanced trees`
- searching is `logarithmic time`, Hashmap is constant time.