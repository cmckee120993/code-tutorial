# split() Method for Regular Expressions Code Tutorial

JavaScript uses a variety of regular expressions (regex) to accomplish tasks. Regex match character combinations within strings in order to manipulate them. This tutorial will walk you through when and how to use the JavaScript regex through the function split(). 

## Summary of split() and Regex

split() takes a string and divides each character in it into an order list. These characters (or substrings) can then be searched for and manipulated like an array of characters of the original string. In fact, if you were to return the entire string after it has been split, you would get an array of the string. Regex are then used in conjunction with split in order to manipulate where and how strings will be split!

Note: Regex can be used in many other JavaScript methods, such as: exec(), test(), match(), matchAll(), replace(), replaceAll(), and search(). For the purposes of supplying examples through one method, I have chosen to focus on split rather than introducing a variety of methods to exemplify regex patterns and uses. 

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)

## Regex Components
Before you're able to work with the split() method, you need to identify a string. You can put the string in quotes directly before split, but working with a constant simplifies the process. The first works directly with the string, the second stores the string to be put used with the function later:

1. 'Clay is really happy today!'.split(); 
2. const str = 'Clay is really happy today!';

After this, you can add the function after the constant "str". This will split the one string into an array of substrings. In the parentheses after the split, you can identify a separator and a limit, both of which are optional. The separator is used for splitting in a specific way; if it is not used, the method makes an array with the entire original string. THe limit parameter will allow you to limit how many splits can be made in a string. Any parts of the string left after that limit are excluded from the array.

Doing the function without the parameters will return an array with the entire string in tact:

console.log(str.split());
returns: Clay is really happy today!

This returns the entire original string without any way to manipulate the data further. For example, you could not use dot notation to access a specific letter or piece since it that entire string is currently the only thing in the array.

In order to access the string in pieces throughout the array, you could use single or double quotes as your separator. For example:

console.log(str.split(''));
returns: ["C","l","a","y"," ","i","s"," ","r","e","a","l","l","y"," ","h","a","p","p","y"," ","t","o","d","a","y","!"]

Because I am using single quotes as my separator, the entire string will be put into an array by each individual character, even the spaces. This will hold true even if you put the split into another constant/variable. Putting it into another variable allows you to manipulate it easier. For example:

const myArray = str.split('');

In the above, I can now access each element of the array using dot notation when I want to use the data. console.log(myArray[1]); for example, will give me the letter "l". Separators can also be letters or punctuation, like in the following example:

const myArray = str.split('y');
console.log(myArray);
returns: ["Cla"," is reall"," happ"," toda","!"]

All of the 'y's are removed, and the other letters/spaces are grouped together based on where the 'y's were in the string.

The limit is the final optional component of the method. If you only want your string to be cut twice where there is a 'y', then write it as follows:

const myArray = str.split('y', 2);
console.log(myArray);
returns: ["Cla"," is reall"]

Everything after that second 'y'—because it is after the limit that I set for the split—is now completely removed from the array. 

### Anchors
This method can use anchors to specify where things should be split. * is used for the beginning of a string and $ for the end of a string. In the following list of names, I want to split it so eaach name maintains the space between the first and last name; however, I want to remove the spaces before the first and after the last name of each person. Here's how I can do that:

const names = 'Clayton McKee ; Nicolas Murati; Sabrina Kennelly ;Jennifer Noji;';

    I want this list of names to print out as follows: ["Clayton McKee","Nicolas Murati","Sabrina Kennelly","Jennifer Noji"]

const removeExtras = /\s*(?:;|$)\s*)/;

    This constant will function as my separator in the split method. See below for further character classes—the \s refers to spaces. This separator using the * for a space before the ;, and the $ for a space after allows me to remove the extra and print out the names.

const nameList = names.split(removeExtras);
console.log(nameList);
returns: ["Clayton McKee","Nicolas Murati","Sabrina Kennelly","Jennifer Noji",""]

### Quantifiers
 

### OR Operator

### Character Classes
Various character classes can be used as separators. Here is a list of possible options: 
Character Class  | Meaning
------------- | -------------
\d  | Matches any Arabic numeral
\D  | Matches any non Arabic numeral
\s  | Matches any spaces (space, tab, etc.)
\S  | Matches a single character other than a space
\t  | Matches a tab
\r  | Matches a return

### Flags
The 'u' flag is only used if the separator is another regex. The u flag is for unicode, which allows you to access the numeric value of a character. This is paraticularly useful with emojis and allows them to be separated where their codes differ. For example:

console.log("😄😄".split(/(?:)/u));
returns: [ "😄", "😄" ]

    Note: The /(?:)/ allows the emojis to be split between one another. Without the u, the console will print out the following numeric values: ["\ud83d","\ude04","\ud83d","\ude04"]; the u flag at the end allows the emojis to be printed. 

### Grouping and Capturing
Grouping and capturing are only used when splitting with a regex to include parts of the separator in the result. Capturing parentheses can be used to group together the character class. For example:

const str = '1, Clay is really happy today! 2, it is nice outside';
const splits = str.split(/(\d)/);
console.log(splits);
returns: ["","1",", Clay is really happy today! ","2",", it is nice outside"]

In what is returned, all letters and spaces are grouped together, while all numbers are split apart from the rest of the characters. This is becuase the separator is using numerical digits (through the character class \d) as the separator in the capturing parentheses. A similar thing was done in the above example under flags. 

### Bracket Expressions
Bracket expressions are not used in the split() method itself; however, all data is returned in array brackets. You can, thus, access the various components of the array through dot notation as shown above. 

### Greedy and Lazy Match
Greedy and lazy match both function in this method to eliminate exact or semi-exact matches. For example:

let regexp = /".+"/g;
let str = '"Clay" is "happy" today';
console.log( str.split(regexp));
returns: [""," today"]

The two components of the array include everything that is not in quotes as the regexp above being used as a separator removes it from the string (it is split at the start and end quote). Because the above is greedy, it will do it every time it sees quotation marks and even eliminates the is because it falls between quotation marks (technically). If we make it lazy—like in the following example—it only cuts where a word is surrounded by quotations marks (so only "Clay" and "happy" are taken out). 

let regexp = /".+?"/g;
let str = '"Clay" is "happy" today';
console.log( str.split(regexp)); 
returns: [""," is "," today"]

    Note: The question mark (?) after the + is what makes it a "lazy" match.

### Boundaries
Word boundaries are not necessary with the split method because you can just split the string at the word without needing to put a boundary around it.

let regexp = "Clay";
let str = 'Clay is happy today';
console.log( str.split(regexp)); 
returns: [""," is happy today"]

    Clay is no longer a part of the phrase.

Boundaries do become useful when you have a word that has a part of the word you do want to cut in it. For example, the following grammatically incorrect string: 

let regexp = /\bClay\b/;
let str = 'Clay is Clayhappy today';
console.log( str.split(regexp)); 
returns: [""," is Clayhappy today"]

    If I wanted to keep my made up emotion of "Clayhappy" without cutting "Clay" from it (like I would do had I just used a regular split of the string "Clay" without boundaries), I would need to add the /\bSTRING\b/. 

### Back-references

### Look-ahead and Look-behind

## Author

A short section about the author with a link to the author's GitHub profile (replace with your information and a link to your profile)
