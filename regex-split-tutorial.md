# split() Method for Regular Expressions Code Tutorial

JavaScript uses a variety of regular expressions (regex) to accomplish tasks. Regex match character combinations within strings in order to manipulate them. This tutorial will walk you through when and how to use the JavaScript regex through the function split(). 

## Summary of split() and Regex

split() takes a string and divides each character in it into an order list. These characters (or substrings) can then be searched for and manipulated like an array of characters of the original string. In fact, if you were to return the entire string after it has been split, you would get an array of the string. Regex are then used in conjunction with split in order to manipulate where and how strings will be split! Regex are a bit strange looking, but getting to know their components and how to use them will turn them into powerful tools to employ!

Note: Regex can be used in many other JavaScript methods, such as: exec(), test(), match(), matchAll(), replace(), replaceAll(), and search(). For the purposes of supplying examples through one method, I have chosen to focus on split rather than introducing a variety of methods to exemplify regex patterns and uses. 

## Table of Contents

- [Regex Components](#regex-components)
- [split() Components](#split()-components)
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

### Regex Components
Regex help you define a search pattern in a text or a string. It helps hone in on a specific part of that string. The regex helps you find various patterns based on specific characteristics. Check out the following for possibilities!

Sample string: 'Clay is really happy today!'

Firstly, regex can be broken into two categories: 
- Literal Character: looks for exact combo of characters (casing, spelling, etc.)
    - Example: regex of 'really' would only look for that word in the sample.
- Meta Character: a character that indicates a generalized pattern

Meta Characters  | Use          
------------- | -------------
 / | Used to wrap the regex at the start and end 
Anchors  | Look at what is attached to the start (^) and end ($) of a word 
Quantifiers  | Set a number to the regex, such as a min or max of characters
OR Operators  | Using the symbol (|) between letters in parentheses allows what can be done in bracket expressions happen outside of them, which is useful for grouping constructors (example \[abc] = (a|b|c)).
Character Classes  | These define a set of characters or values in a string.
Flags | Placed at the end of regex outside of closing slash (/); seven in total defined below
Grouping and Capturing | Group multiple patters as a whole; capturing groups give extra submatch information
Bracket Expressions  | Whatever is inside brackets ([]) is a range of characters to be matched
Greedy and Lazy Match | This will work in conjunction with other searches to work with as many matches as possible (greedy) or as few as possible (lazy)
Boundaries | Work with the begginings and endings of lines, words, and/or patterns
Back-references | Refer to a previously captured group in the same regex
Look-ahead and Look-behind | These look for matches either before (ahead) or after (behind) a desired string/character.

Throughout this tutorial, I'm going to try and isolate the regex expressions as much as possible for ease of seeing what is expected when you use only one. Please note that you can combine many of these characteristics to get a more complex regex that will really filter and assist your search in being as precise as possible!

### split() Components

Note: Feel free to skip this if you only came for regex!

Before you're able to work with regex and the split() method, you need to identify a string. You can put the string in quotes directly before split, but working with a constant simplifies the process. The first works directly with the string, the second stores the string to be put used with the function later:

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
Anchors specify the parts at the beginning (^) or the end ($) of a string. With a singular string, you can only start with what is present. For example: 

const str = 'Clay is really happy today!';
const anchorEx = /^C/;
const newStr = str.split(anchorEx);
console.log(newStr);
returns: ["","lay is really happy today!"]

In this case, only the C is removed as that is what's specified after the anchor. The more I add after the C, the more that will be cut off. It does, however, need an exact match. So, adding "lay is" after the "C" returns [""," really happy today!"]. The same happens with the $ as the end: 

const str = 'Clay is really happy today!';
const anchorEx = /!$/;
const newStr = str.split(anchorEx);
console.log(newStr);
returns: ["Clay is really happy today",""]

const str = 'Clay is really happy today!';
const anchorEx = / today!$/;
const newStr = str.split(anchorEx);
console.log(newStr);
returns: ["Clay is really happy",""]

    Note: The ^ goes before the desired search, while the $ goes after the desired search.

### Quantifiers
Quantifiers are inherently greedy, which means they look for as many occurences as possible that match the patterns. Here are some possible symbols used for quantifiers in regex:

- * : matches zero or more times
- + : matches one or more times
- ? : Matches zero or one time
- {} : various uses:
    - {n} : matches exactly "n" times
    - {n, } : matches at least "n" times
    - {n, x} : matches a minimum "n" times to a max of "x" times

In the same string as above, if I wanted to remove any word with a double "p", I could use a quantifier: 

const string = 'Clay is really happy today!';
const quantifierEx = /hap{2,}y/;
const newStr = string.split(quantifierEx);
console.log(newStr);
returns: ["Clay is really "," today!"]

### OR Operator
As mentioned above, the OR Operator (|) allows another way to write the bracket expressions. See this example with here and below in bracket expressions to see the difference. 

const string = 'Clay is really happy today!';
const operatorEx = /(a|y)/;
const newStr = string.split(operatorEx);
console.log(newStr);
returns: ["Cl","a","","y"," is re","a","ll","y"," h","a","pp","y"," tod","a","","y","!"]

You'll notice that in the above return, you are actually not removing the "a" or the "y", but you are splitting and maintaining it in the array. Remember that when looking at the bracket expression below for how that works with the split() method. While split() does slightly alter the use of OR Operators vs. Bracket Expressions, it is important to note that their search ability is similar. 

### Character Classes
Various character classes can be used as separators. Here is a list of possible options: 
Character Class  | Meaning
------------- | -------------
. | Matches any character except a newline
\d  | Matches any Arabic numeral
\D  | Matches any non Arabic numeral
\s  | Matches any spaces (space, tab, etc.)
\S  | Matches a single character other than a space
\t  | Matches a tab
\r  | Matches a return
\w | Matches any alphanumeric character from the Latin alphabet

This is very useful if I want to split a string up based on the words without any spaces whatsoever. I can use the \s in my regex to achieve that! For example: 

const string = 'Clay is really happy today!';
const quantifierEx = /\s/;
const newStr = string.split(quantifierEx);
console.log(newStr);
returns: \["Clay","is","really","happy","today!"]

### Flags
The seven flags used in regex are as follows: 
- d : stands for indices and generates indices for substring matches
- g : stands for global search and tests for all possible matches 
- i : stands for case-insensitve search and means that case is ignored when searching
- m : stands for multi-line search and means that a string should be treated as multiple lines
- s : stands for dot all and allows "." to match newline characters
- u : stands for Unicode and treats a pattern as a sequence of Unicode code points (see below example)
- y : stands for sticky search and looks for matches starting at the current position in the string

The below example uses the "u" flag to split apart two emojis. Its position reflects where all flags would be placed in a regex.

console.log("😄😄".split(/(?:)/u));
returns: [ "😄", "😄" ]

<!-- ### Grouping and Capturing
Grouping and capturing are only used when splitting with a regex to include parts of the separator in the result. Capturing parentheses can be used to group together the character class. For example:

const str = '1, Clay is really happy today! 2, it is nice outside';
const splits = str.split(/(\d)/);
console.log(splits);
returns: ["","1",", Clay is really happy today! ","2",", it is nice outside"]

In what is returned, all letters and spaces are grouped together, while all numbers are split apart from the rest of the characters. This is becuase the separator is using numerical digits (through the character class \d) as the separator in the capturing parentheses. A similar thing was done in the above example under flags.  -->

### Bracket Expressions
 Bracket expressions can represent a range of characters or a list of characters that you want to search for in a string. \[abc], for example, looks for "a", "b", or "c" in the string at any point. You could also write it as a range, \[a-c]. You can also use bracket expressions with numbers. In the below example, you will see how you can use a list of looking for two letters that are not near eachother in the alphabet without making it a range from a to z. 

const string = 'Clay is really happy today!';
const bracketEx = /[a, y]/;
const newStr = string.split(bracketEx);
console.log(newStr);
returns: \["Cl","","","is","re","ll","","h","pp","","tod","","!"]

You'll notice that in the return with bracket expressions (unlike with OR Operators) when using split(), the "a" and the "y" are completely removed array, but the splits still occur at the same places for the other characters. 

### Greedy and Lazy Match
Greedy and lazy match both function in this method to eliminate exact or semi-exact matches. As mentioned above, the g flag looks for all possible matches, making it greedy. For example:

let regexp = /".+"/g;
let str = '"Clay" is "happy" today';
console.log( str.split(regexp));
returns: [""," today"]

The two components of the array include everything that is not in quotes as the regexp above being used as a separator removes it from the string (it is split at the start and end quote). Because the above is greedy, it will do it every time it sees quotation marks and even eliminates the "is" because it falls between quotation marks (technically). If we make it lazy—like in the following example—it only cuts where a word is surrounded by quotations marks (so only "Clay" and "happy" are taken out). 

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
FINISH

### Look-ahead and Look-behind
Look-ahead and look-behind look for patterns that follow (ahead) or precede (behind) another pattern. The syntax for lookahead is X(?=Y), or, in other words, look for X if followed by Y. Check out this example of how it works in split:

let lookahead = /today(?=!)/;
let str = 'Clay is happy today!';
console.log( str.split(lookahead)); 
returns: ["Clay is happy ","!"]

Because I am splitting the sentence at "today" if it precedes the exclamation point, the array returns without the string "today". To complete a look-behind, you use (?<=Y)X—in other words, lok for matches of X if Y precedes it. Rather than using a string in the first example, I will combine the look-behind with a character class:

let lookahead = /(?<=\s)\S/;
let str = 'Clay is happy today!';
console.log( str.split(lookahead)); 
returns:["Clay ","s ","appy ","oday!"]

The above regex asks the string to be split at every consonant (\S) that is preceded by a space (\s), so the "i", "h", and "t" are all removed from the string; the rest of the characters are then grouped accordingly. 

## Author

Clayton McKee is currently completing a bootcamp with UCLA Extension. He is a rising fullstack developer. For some of his projects, please take a look at [his GitHub profile](https://github.com/cmckee120993). You can also email him at [cmckee120993@gmail.com](mailto:cmckee120993@gmail.com).
