# ArraysJS

A lot of what i do with JavaScript involves manipulating arrays. I wrote this library, to make my life easier by extending the 
JavaScript Array prototype. It worked! Use with creativity, and it will serve you well ... Holla, if you think of something that should be there. I'd be quite willing to add to and remove functions. I hope ArraysJS makes your life easier too. 

## Getting Started

To use, download a copy of the Arrays.js file, and reference in your web page. Have fun using ArraysJSs.

### Prerequisities

I have tried as much as possible to free ArraysJS of dependencies on third-party javascript javascript libraries. ArraysJS has no dependencies, and runs entirely on pure javascript.

```
Give examples
```

### Installing

Add a script reference to the Arrays.js file
```
<script src="js/arrays.js"></script>
```

### Features

#### Array.prototype.add(item)

###### Parameters
*item:* The object, array or literal to be added to the array.

###### Usage
This is very similar to Array.prototype.push, however it returns the resultant array, so that you can chain other prototype functions.
```
var arr = [1,2,3];
arr.add(4).add(5).add(6);
console.log(arr); //should print out [1,2,3,4,5,6]
```

#### Array.prototype.addif(item, [property_name])

###### Parameters
*item:* The object, array or literal to be added to (if not exists) the array.

*[property_name]:* A string, specifying the property name of the array's children objects to check.

###### Usage
Adds an item into the array, if the array does not already have an child with the same value, or an child whose property (with key property_name) has the same value as item[property_name]. The argument, [property_name] is optional.
```
var arr = [1,2,3]
arr.addif(4); //[1,2,3,4]
arr.addif(4); //[1,2,3,4]
arr.addif(5); //[1,2,3,4,5]
```

When dealing with Array of objects,
```
var arr = [{
  id: 1,
  name: "john doe"
},
{
  id: 2,
  name: "alfred pete"
}];
arr.addif({
  id: 1,
  name: "john doe"
}, 'id') //does not add this object to the array, because an item with the same key already exists
```

#### Array.prototype.toggle(item, [property_name])
###### Parameters
*item:* The object, array or literal to be added to (if not exists) or removed from (if exists) the array.

*[property_name]:* A string, specifying the property name of the array's children objects to check.

##### Usage
```
var arr = [1,2,3];
arr.toggle(1); //[2,3]
arr.toggle(1); //[2,3,1]

arr = [{
  id: 1,
  name: "john doe"
},
{
  id: 2,
  name: "alfred pete"
}];
arr.toggle({
  id: 1,
  name: "john doe"
}, 'id') //removes the object from array arr where id is 1
arr.toggle({
  id: 1,
  name: "john doe"
}, 'id') //pushes the object unto the array arr
```

#### Array.prototype.addRange(arrs)
###### Parameters
*arrs:* An array of objects, which will each be inserted into the calling Array

##### Usage
```
var arr = [1,2,3];
arr.addRange([4,5,6]) //[1,2,3,4,5,6]
```

#### Array.prototype.from(index)
Returns a sub-array containing items from the specified index to the end of the parent-array
###### Parameters
*index:* An integer, which determines which point to start counting from 

##### Usage
```
var arr = [1,2,3,4,5,6]
arr.from(2) //[3,4,5,6]
```

#### Array.prototype.first([count])
###### Parameters
*[count]:* An optional parameter; If not set, this function returns the first item in the array, or if the array is empty, it returns an empty object {} instead. If set to an integer, it returns the first [count] children of the array.=

##### Usage
```
var arr = [1,2,3]
arr.first() // 1
arr.first(2) // [1,2]
arr.first(1) // [1]
```

#### Array.prototype.last([count])
Similar to Array.prototype.first, this starts from the end of the array rather than from the first item when counting.
###### Parameters
*[count]:* An optional parameter; If not set, returns the last item in the array. If set, the [count] last items in the array are returned in positional order as a sub-array

##### Usage
```
var arr = [1,2,3]
arr.last() // 3
arr.last(2) // [2,3]
arr.first(1) // [3]
```

#### Array.prototype.where(prop, val)
Gets a sub-array with items whose specified property match a specified value
###### Parameters
*val:* The value that the properties have to match to be valid
*prop:* The key of the properties in question. It has to be a literal object. E.g. A string, Number, or even a boolean

##### Usage
```
var arr = [{
  id: 1,
  level: 3,
  name: "john doe"
},
{
  id: 2,
  level: 4,
  name: "alfred pete"
},
{
  id: 3,
  level: 3,
  name: "elton john"
}];
arr.where('level', 3) //returns the objects containing names 'john doe' and 'elton john'
```

#### Array.prototype.sort([type])
I know there is a native implementation of Array.prototype.sort, but i guess i was feeling a bit like superman when i wrote this. Anyway, the real kicker on this one is its ability to sort (using bubble sort) in ascending or descending order
###### Parameters
*[type]:* An optional parameter; If not set or if set to 'asc', the array is sorted in ascending order. If set to 'desc' or anything besides 'asc', the array is sorted in descending order

##### Usage
```
var arr = [3,2,1,3,5,4,6]
arr.sort(); // [1,2,3,3,4,5,6]
```

#### Array.prototype.isort([type])
Insertion sort. Very useful for large arrays
###### Parameters
*[type]:* An optional parameter; If not set or if set to 'asc', the array is sorted in ascending order. If set to 'desc' or anything besides 'asc', the array is sorted in descending order

##### Usage
```
var arr = [3,2,1,3,5,4,6]
arr.isort(); // [1,2,3,3,4,5,6]
```

#### Array.prototype.bsearch(item)
Performs binary search on a sorted array for the item specified in the argument. THe index of the item is returned. If not found, -1 is returned. Useful for when dealing with very large arrays
###### Parameters
*item:* The literal object to be found

##### Usage
```
var arr = [3,2,1,3,4,5,6]
arr.bsearch(1) // 2
arr.bsearch(7) // -1
```

#### Array.prototype.sortBy([prop], [type])
Sorts the array in ascending or descending order by its children's properties with key (prop)
###### Parameters
*[prop]:* The property key by which the array is to be sorted. If not specified, Array.prototype.sort is executed instead
*[type]:* Specifies whether the array should be sorted in ascending or descending order. value 'asc' translates to ascending order, while 'desc' translates to 'descending' order

##### Usage
```
var arr = [{
  id: 1,
  level: 3,
  name: "john doe"
},
{
  id: 2,
  level: 4,
  name: "alfred pete"
},
{
  id: 3,
  level: 3,
  name: "elton john"
}];
arr.sortBy('level') //sorts array arr by level in ascending order
arr.sortBy('level', 'desc') //sorts array arr by level in descending order
```

#### Array.prototype.sortfn(fn)
Performs a sort on the Array based on a function that compares the potential current and next items in the array. 
###### Parameters
*fn:* A function that takes in item1 and item2 as parameters. If not specified, or if set to a value that is not a function, it takes the default value
```
function (val1, val2) { return val1 > val2 } //which makes sure the array is sorted in ascending order
```

##### Usage
```
var arr = [3,2,1,3,4,5,6]
arr.sortfn(function (val1, val2) { return val1 < val2 }) //[6, 5, 4, 3, 3, 2, 1] sorts in descending order.
```

#### Array.prototype.isSorted([type])
Returns a boolean indicating whether the array is sorted or not
###### Parameters
*[type]:* Indicates the sorted type to check for. 'asc' translates to ascending. 'desc' translates to descending

##### Usage
```
var arr = [1,2,3,4,5,6];
arr.isSorted() //true
arr.isSorted('asc') //true
arr.isSorted('desc') //false
```

#### Array.prototype.insert(item, index)
Inserts an item into an index in the array, while the items at the right of the index are shifted to the right
###### Parameters
*item:* The object to be inserted
*index:* The integer index, in which the object item should be inserted

##### Usage
```
var arr = [1,2,3,4,5,6];
arr.insert(7, 2); //[1,2,7,3,4,5,6]
```

#### Array.prototype.clear()
Empties an array

##### Usage
```
var arr = [1,2,3,4,5,6];
arr.clear() // []
```

#### Array.prototype.count(item, index)
Returns the length of the array ... Redundant, huh? :D

##### Usage
```
var arr = [1,2,3,4,5,6];
arr.count(); // 6
```

#### Array.prototype.indexOfProp(item, prop)
Returns the index of the first instance of an object, in the array's items or among the array's items' properties specified by key [prop]
###### Parameters
*item:* The object to be found
*index:* The integer index, in which the object item should be inserted

##### Usage
```
var arr = [{id: 1},{id: 2},{id: 3},{id: 4}];
arr.indexOfProp(3, 'id') // 2
```

#### Array.prototype.contains(item, [prop])
Returns a boolean value indicating whether the array contains the object item, or checks the values in key [prop] of the array's items
###### Parameters
*item:* The object to be found
*[prop]:* The key to be searched. If specified, it compares object item with child_object[prop]

##### Usage
```
var arr = [{id: 1},{id: 2},{id: 3},{id: 4}];
arr.contains(3, 'id') // true
arr.contains(7, 'id') // false
arr.contains(7, 'prop') // false
arr.contains(3) // false
```

#### Array.prototype.distinct([prop])
Results distinct elements in the array or uses a key if specified
###### Parameters
*[prop]:* if specified, makes the array distinct by its elements[prop] value

##### Usage
```
var arr = [1,1,4,2,3,2,3,4,5,4,4,2,2,1];
arr.distinct() //[1,4,2,3,5]
```

#### Array.prototype.remove(item, [prop])
Removes all instances of an item from the array
###### Parameters
*item:* The item to be removed
*[prop]:* if specified, finds the item whose item[prop] value matches item, and removes it

##### Usage
```
var arr = [1,1,4,2,3,2,3,4,5,4,4,2,2,1];
arr.remove(1); //[4,2,3,2,3,4,5,4,4,2,2]
arr = [{age: 2},{age: 2},{age: 2},{age: 3}]
arr.remove(2, 'age') // [{age: 3}]
```

#### Array.prototype.removeAt(index)
Removes an item at an index from the array
###### Parameters
*index:* The integer index of the item to be removed

##### Usage
```
var arr = [1,2,3,4];
arr.removeAt(1); //[1,3,4]
arr = [{age: 2},{age: 2},{age: 2},{age: 3}]
arr.removeAt(0) // [{age: 2},{age: 2},{age: 3}]
```

#### Array.prototype.shuffle()
rearranges an array randomly

##### Usage
```
arr.shuffle(); //scatters its elements
```

#### Array.prototype.range(start, end)
Returns an array with numbers ranging from [start] to [end]
###### Parameters


##### Usage
```
var arr = [1,1,4,2,3,2,3,4,5,4,4,2,2,1];
arr.remove(1); //[4,2,3,2,3,4,5,4,4,2,2]
arr = [{age: 2},{age: 2},{age: 2},{age: 3}]
arr.remove(2, 'age') // [{age: 3}]
```

#### Array.prototype.select(prop)
Returns an array whose 
###### Parameters

##### Usage
```
var arr = [{age: 2},{age: 2},{age: 2},{age: 3}]
arr.select('age') // [2,2,3]
```

#### Array.prototype.isEmpty()
Returns a boolean indicating 
###### Parameters

##### Usage
```
var arr = [];
arr.isEmpty(); // true
arr.add(1).isEmpty() //false
```

#### Array.prototype.each(fn)
Works like Array.prototype.forEach, pass in a function to manipulate the array's elements. In defence, i didn't know about Array.prototype.forEach when i wrote this function. One major difference is this gives you access to the loop index.

##### Usage
```
var arr = [1,2,3];
arr.each((i) => { 
   i *= 2;
   console.log(arr.index);
}); //[1,4,9]
//console output
/*
0
1
2
*/
```

#### Array.prototype.flatten()
Converts an array containing arrays as elements, into an array of objects, by listing out the child arrays as objects 

##### Usage
```
var arr = [
  [1,2,3],
  [4,5,6],
  [7,8,9]
];
arr.flatten(); //[1,2,3,4,5,6,7,8,9]
```

#### Array.prototype.paginate(maxsize)
Groups the array elements, in groups of [maxsize] lengths

##### Parameters
*maxsize:* the maximum size of the sub-groups before a new sub-group is created

##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.paginate(3);
/*
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
]
*/
```

#### Array.prototype.min()
returns the minimum element in the array
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.min(); // 1
```

#### Array.prototype.max()
returns the maximum element in the array
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.max(); // 9
```

#### Array.prototype.average()
returns the average element in an array of numbers
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.average(); // 5
```

#### Array.prototype.sum()
returns the sum of the elements in an array of numbers
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.sum(); // 45
```

#### Array.prototype.sync(second_array, [prop])
Copies elements from second_array into an array if such an element does not exist
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
var arr2 = [3,7,4,12,0]
arr.sync(arr2); // [1,2,3,4,5,6,7,8,9,12,0]
```

#### Array.prototype.random([count])

##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.random() //returns a random item from arr
arr.random(2) //returns two random items from arr
```

#### Array.prototype.all(fn)
Returns a boolean that indicates whether or not all elements in the array satisfy a condition specified by the function argument (fn)
##### Usage
```
var arr = [1,2,3,4,5,6,7,8,9];
arr.all((i) => i > 0) //return true
arr.all((i) => i >= 3) //return false
arr.all(function (i) { return i >= 5; }) //return false
```

#### Array.prototype.frequency(value, prop)
Counts the occurences of instances of object value in the array, or in the property prop values.
##### Usage
```
var arr = [1,2,1,3,2,2,1,4,5,3,4,5,6,7,8,9];
arr.frequency(1); // 2
arr.frequency(2); // 3
```

#### Array.prototype.trim()
remove all falsy (null, undefined, 0, etc) elements from the array. 
##### Usage
```
var arr = [1,2,3, undefined, null, 0];
arr.trim(); // [1,2,3]
```

## Built With

* Pure Javascript

## Contributing

Not yet

## Versioning

I haven't gotten around to reading about versioning on git

## Authors

**Ikechi Michael**


## License

This project is licensed under the MIT License

## Acknowledgments

* Hat tip to Life and Science
* etc
