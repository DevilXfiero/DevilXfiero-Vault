## Lookup - O(1)
## Insert - O(n)
## Delete - O(n)
deleting first element need to shift all the elements.


# Initializing Array

```java
// Initializing array  
int[] nums = new int[3];  
nums[0] = 1;  
nums[1] = 2;  
nums[2] = 3;  
  
// Initialize known array  
int[] numbers = {1, 2, 3};  
System.out.println(Arrays.toString(numbers));
System.out.println(numbers.length);
```

[[Custom Array]]


# Dynamic Array
- Linked List
- ArrayList

## ArrayList

```java
// Vector: grow on full - 100% - synchronized - single thread can access that  
// ArrayList: 50%  
ArrayList<Integer> list = new ArrayList<>();  
list.add(10);  
list.add(20);  
list.add(30);  
list.get(0); // get the element at index = 0
list.remove(0);  
list.indexOf(20); // first occurrence  
list.lastIndexOf(30); // last occurrence  
Boolean present = list.contains(20);  
list.size();  
Integer[] listToArray = list.toArray(new Integer[0]);  
System.out.println(list);
```


## Linked List

**LOOKUP** 
  By Value - O(n)
  By Index - O(n)

**INSERT** 
  At the End - O(1)
  At the Beginning - O(1)
  In the Middle - O(n)

**DELETE**
  From the Beginning - O(1)
  From the End - O(n) 
  From the Middle - O(n)

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
list.reverse(); // inplace reverse 
var array = list.toArray();
linkedList.size();
```

