Arrays in c# work like arrays in other languages.
They are non dynamic data structures for storying elements of the same data type

**Declaring an Array**
To define indacate the Data type followed by [] brackets and then a name such as
String[] catNames;

To initeate a String with values simple follow the name of the string with a = and curly brackets containing a coma sepreated list of values

String[] catNames = {"Tabby", "Bob"};

**Navigating an Array**
Like other languages the first element of an Array is the 0th position. 

You can return the first element of an array as such
Console.WriteLine(catNames[0]);

Should you wish to change a element in an array you can simple set the element at a spesfic posiction to its new values 

catNames[0] = "Chriss";

**Length of an Array**
To get the Length of an array you can check the Length attrabute of an array 
Console.WriteLine(catNames.Length);

**Other ways to declare an Array**
Array of a specific length containing null values
String[] catNames = newString[4];

Array of a specific length containing values
String[] catNames = newString[4] {"Tabby", "Bob", "Frank", "Shit"};

Looping thought Arrays

Two main ways to loop though Arrays are The for Loop and the Foreach loop

The For Loop 
**for**(int i=0; i<catNames.Length; i++){
	Console.WriteLine("The cat's name is "+catNames[i]);
}

The foreach loop

**foreach**(*type variableName* **in** *arrayName*){
	Do something to each element in an array
}

example

foreach(String name in catNames){
	Console.WriteLine("The cat's name is "+name);
}

**Sorting Arrays**

c# offers inbuilt sorting solutions such as the **Array classes Sort method** 

**Sort** will sort an array of **strings** **alphabetically**  
String[] catNames = newString[4] {"Tabby", "Bob", "Frank", "Shit"};
Array.Sort(catNames);

**Sort** will sort an array of **Integers** in **ascending** order   
int[] myNumbers = {5, 1, 2, 3, 4};
Array.Sort(myNumbers);
myNumbers = {1, 2, 3, 4, 5};

## System.Linq Namespace
The System.Linq Namespace offers further ways of sorting such as `Min`, `Max`, and `Sum`

```csharp
Console.WriteLine(myNumbers.Max());  // returns the largest value
Console.WriteLine(myNumbers.Min());  // returns the smallest value
Console.WriteLine(myNumbers.Sum());  // returns the sum of elements
```

## Multidimensional Arrays

**Declaring a Two-Dimensional Array**
To declare a 2d array simply indacate the number of dimensions with in the [] by the DataType with the use of ','.

int[,] numbers;

To predefine its values use nested {}
int[,] numbers = {{1,2,3}, {4,5,6}};

**Navigating an Array**
Two-Dimensional arrays are still arrays and as such the initial position of both axes of an array are 0.

To return the Number '1' from the numbers 2dArray we must look for the element in the first posiction of both arrays, ie 0,0;

Console.WriteLine(numbers[0,0]);

and if we wanted to change the the number 4 to be another number we can still perform the same operation as a normal array.

numbers[1,0] = 7;
Console.WriteLine(numbers[1,0]);


Looping thought Arrays

Just as before there are two ways of looping though Two-dimensional arrays for and foreach but with one difference. 

While the foreach will work the same way 

```csharp
int[,] numbers = { {1, 4, 2}, {3, 6, 8} };

foreach (int i in numbers)
{
  Console.WriteLine(i);
} 
1
4
2
3
6
8```

the for will require another nested for loop

int[,] numbers = { {1, 4, 2}, {3, 6, 8} };

for(int i = 0; i < numbers.**GetLength(0)**; i++){
	for(int k = 0; j < numbers.**GetLength(0)**; j++){
		Console.WriteLine(numbers[i,j]);
	}
}