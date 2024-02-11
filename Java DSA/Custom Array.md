```java 
package com.practice;  
  
import java.util.Arrays;  
  
public class Array {  
  
private int[] arr;  
private int index = 0;  
  
public Array(int size) {  
arr = new int[size];  
}  
  
public void insert(int num) {  
if(arr.length == index) {  
expand();  
}  
this.arr[index++] = num;  
}  
  
public void expand() {  
int[] new_arr = new int[index*2];  
for(int i=0; i<arr.length; i++)  
{  
new_arr[i] = arr[i];  
}  
arr = new_arr;  
}  
  
public int indexOf(int num) {  
for(int i=0; i<index; i++){  
if(arr[i] == num) {  
return i;  
}  
}  
return -1;  
}  
  
public int removeAt(int indx) {  
if(indx >=arr.length || indx < 0) {  
return -1;  
}  
int num = arr[indx];  
  
for(int i=indx; i< arr.length-1; i++)  
{  
arr[i] = arr[i+1];  
}  
index--;  
return num;  
}  
  
public void print() {  
for(int i=0; i<index; i++)  
{  
System.out.print(arr[i] + " ");  
}  
System.out.println();  
}  
}
```