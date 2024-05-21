![[0_M7YuoDdy3b8EhBr6.png]]

## Arrays
- Fixed in size
- Fast for data retrivals
- Compact memory usage if size is known
- Delete operation very hard

2D Arrays

```java
char[][] board = new char[3][3];  
  
for(int i=0; i<3; i++) {  
for(int j=0; j<3; j++) {  
board[i][j] = '-';  
}  
}  
  
  
board[0][0] = 'O';  
board[1][0] = 'O';  
board[2][0] = 'O';  
  
char[][] boardTwo = new char[][] {  
new char[] {'O','-','-'},  
new char[] {'O','-','-'},  
new char[] {'O','-','-'},  
};  
System.out.println(Arrays.deepToString(board));  
System.out.println(Arrays.deepToString(boardTwo));
```

## List

- An ordered collection aka sequence
- Allow duplicates 
- Not Fixed in size like arrays
- Fast for data retrivals
- Various Implementations - ArrayList, Stack,Vector, LinkedList etc.

```java
List random = new ArrayList();  
random.add("blue");  
random.add("purple");  
  
random.add(1);  
random.add(new Object());  
  
// we need to tell datatype to avoid adding random objects  
List<String> colors = new ArrayList<>();  
List<String> colorsUnmodifiable = List.of(  
"blue",  
"pink",  
"purple"  
);  
colors.add("orange");  
colors.add("purple");  
System.out.println(colors);  
System.out.println(colorsUnmodifiable);  
System.out.println(colors.size());  
System.out.println(colors.contains("orange"));  
System.out.println(colors.contains("pink"));  
  
for(int i =0; i<colors.size(); i++) {  
System.out.println(colors.get(i));  
}  
  
for(String color: colors) {  
System.out.println(color);  
}  
  
colors.forEach(System.out::println);
```

- Difference between Vector and ArrayList is that vector is synchronized. If a thread-safe implementation is not needed, it is recommended to use ArrayList.

## Stack

- Stack class represents a last-in-first-out (LIFO) stack of objects.
- It extends class Vector with five operations that allow vector to be treated as stack 
- The usual push and pop operations are provided as well as method top peek at the top item on the stack


```java
Stack<Integer> stack = new Stack<>();  
stack.push(1);  
stack.push(2);  
stack.push(7);  
System.out.println(stack.peek());  
System.out.println(stack.size());  
System.out.println(stack.pop());  
System.out.println(stack.size());  
System.out.println(stack.empty());
```


## Queue 

FIFO (First In First Out)
A collection designed for holding elements prior to processing.

queue interface extends Collection  
deque extends queue  
priority queue implements queue  
  
* add(E element) -> pool is full Exception  
* offer(E element) -> No exception  
* E poll() -> NE  
* E remove() -> E  
* E peek() -> NE  
* E element -> E

## Deque

extend queue to allow double-ended queues  
can work as stack LIFO and also as queue FIFO  
addFirst  
addLast  
offerFirst  
offerLast  
E getFirst()  
E getLast()

## LinkedList
```java
LinkedList<Integer> linkedList = new LinkedList<>();  
linkedList.addLast(30);  
linkedList.addFirst(10);  
linkedList.getFirst();  
linkedList.get(0); // get the element at index = 0  
linkedList.getLast();  
linkedList.removeFirst();  
linkedList.remove(0);  
linkedList.removeLast();  
linkedList.indexOf(20); // first occurrence  
linkedList.lastIndexOf(30); // last occurrence  
linkedList.contains(20);  
linkedList.size();  
System.out.println(list);
```

 Iteration
```java
static record Person(String name, int age) {}

LinkedList<Person> linkedList = new LinkedList<>();  
linkedList.add(new Person("DevilX", 21));  
linkedList.add(new Person("Rose", 18));  
  
ListIterator<Person> personListIterator = linkedList.listIterator();  
while (personListIterator.hasNext()) {  
System.out.println(personListIterator.next());  
}
```


## Sets 

A collection that contains no duplicate elements.
Set doesn't guarantee order.

TreeSet - preservers order backed by TreeMap
HashSet - backed by HashMap

```java
Set<Ball> balls = new HashSet<>();  
balls.add(new Ball("blue"));  
balls.add(new Ball("blue"));  
balls.add(new Ball("orange"));  
balls.add(new Ball("purple"));  
balls.forEach(System.out::println); // to make set works correctly you must override equals and hashCode method in class to compare by value not by reference
```


## Map

- Collection of key value pairs
- A map cannot contain duplicate keys

<key,value> pair called and entry  
no duplicate keys, unique  
Object put(K key, V value)  
Object get(Object key)  
Object remove(Object key)  
boolean containsKey(Object key)  
boolean containsValue(Object value)  
int size()  
boolean isEmpty()  


we have to pass key which goes through HashFunction - function that produces hashCode
HashCode - mapping an Object to its Integer value
hash function always produce same hash code for  given object

Lookups become fast in maps because of HashCode.
