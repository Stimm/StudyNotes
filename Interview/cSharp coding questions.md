
1: How to reverse a string
	a. Quick and easy
		Convert the string into an array and then loop though the array from both ends swaping characters.
	b. If its a string we can use the string.reverse() method

2: Check to see if a string is a palindrome.
	a. Palindroms with no spaces.
		Declare a bool called flag
		Convert the string into a string array
		Loop through the string array and compair the I and J of the array to make sure they are the same if not set flag to false
	
	b. Clean the string by using the split function with " " as the designated character then add the substrings together.
	Declare a bool called flag
		Convert the string into a string array
		Loop through the string array and compair the I and J of the array to make sure they are the same if not set flag to false

	c. C# way
		simply create a new string and == to inputstring.reverse() check to see if equale

3: given a sequence of words reverse the order of the words in the string.
	a. Quick and easy
			Split the string by " " and then add them back in in reverse order seprated by a " ". 
			Substring + " " + outPutstring

4: given a sequence of words reverse the words in that sequence.
	a. Quick and easy
		Split the sequence by " ".
		Take each substring and reverse it ether by sequance or by building a reversedSubstring string
		Add the String to a output string which will be outputString + " " + reversedSubstring

5: Count how many times characters are used in a string
	a. Quick and easy
		Use mapping 
		Create a Dictonary with the key pair value of Char and Int. Dictonary<char, int> chaDick = new Dictonary<foo, bar>
		loop though the string and check to see if the string exists.
		if(chaDick.ContainsKey(char))
			chaDickp[char]++
		else
			charDick.add(char,1)

6: Remove duplicate characters from a string *
	a. Quick and easy
		 Create a output string
		 Loop though the string and check to see if the new string contains a character
		 If not add the new character
		 if it dose move to the next character.

7:find the sub strings
	a. Quick and easy
		Use two nested loops
		Firs loop keeps the starting posiction
		Second loop walks though string capturing a ever increacing range of characters till it reaches the end.
			List<string> stringList = new List<string>()
			for(int i = 0; i<sting.legth(); i++)
				string substring = "";
				for(int j = i; j<string.length(); j++)
					substring = substring+string[j]
				stringList.Add(substring)

8:How to perform Left circular rotation of an array?

	a. Quick and easy
		i = the number of times we are going to loop (array.length)
		j = starting posiction
		while(i<lenght)
		intlist.add(posiction in array j)
		j++
		if J > arraylength then j = 0;

	b. Inmemory solution (Ie dont create another array)
		A bit harder and one I found it hard to get my head around, please review.
		take the array [1, 2, 3, 4, 5]
		What we want to do is keep track of the last element, and then step through the rest of the array backwords swaping the last element with the current element.
		[1, 2, 3, **4**, **5**]
		[1, 2, 3, **5**, **5**]
		[1, 2, 3, **5**, **4**]
		[1, 2, 3, **5**, **4**]
		[1, 2, **3**, 5, **4**]
		[1, 2, **4**, 5, **4**]
		[1, 2, **4**, 5, **3**]
		temp = array size-1
		array[array.length-1] = array[j-1]
		array[j-1] = temp

9: How to perform Right Circular rotation of an array

10: Check to see if a number is a prime *
	a: Solution
		There are 4 rules for prime checking
		if the number is 1 then it is a prime
		if the number is 2 then the number is not prime
		if the number mod (%) 2 == 0 then it is not prime

		find the square root of the number (int)math.floor(math.square(number))
		then loop though the number cchecking to see if it is root
		for(int i = 3; I<squarRoot; i +=2){ *
			if(number % i ==0) number is not a prime
		}

Get all the sums of a number *
	a: Solution
		we need to find each range of sums and add them together 
		Sum += number %10
		We then can remove that range from the total number
		Number /= 10

Find the second higherst number in an array
	a.Solution
		Declare a First and second int  = 0
		foreach(int i in array ){
			if(i > first){
				Second = first;
				first = i
			} else{
				if(i > second && i < first){
					second = i;
				}	
			}
		}

Convert a 3d array into a 2 array

	a.Solution.
		Thing to remember is to get the X and Y lengths to use the GetLength method
		x = array.GetLength(0); y = array.Getlength(1);
		Then we do a nexted loop and add the elements to a new array or a list.
		for(int i = 0; i < x; i++){
			for(int j = 0; i < y; j++){
				list.add(array[i,j] )
			}
		}

Implament a Stack

	a. C# solution
		Stack<int> intStack = new Stack<int>()
		intStack.push(1);
		intStack.pop();
	b. Coded solution
		Create a List of objects and then write two methods. Push(int) and Pop()
		Push will add items to a list.
		Pop will take the last item off the list, if list is empty return a error message	

Implament a Queue
	a. C# solution
		Queue<int> intQueue = new Queue<int>()
		intQueue.Enqueue(1)
		intQueue.Decueue()
	b.Coded solution
		Create a list of objects and make two methods Enqueue() and Dequeue()
		Enqueue will take a item and add it to a list
		Dequeue will Get the first item from the list and then removeAt(0)

Implament inheratence
	

Implament ploymorphisem

Fizz bang

LINQ