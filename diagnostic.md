# Problem Solving Diagnostic

Directions: Please the diagnostic in its entirety before beginning. There may be information throughout that will help you to complete this successfully.

## Question 1

Write a `biggestNum` function so that given an array of numbers >= 0, will
arrange them such that they form the biggest number.

Example:

```javascript
biggestNum([1, 2, 3]) === '321'
biggestNum([3, 30, 34, 5, 9]) === '9534330'
```

Place your code within the following code block:

```javascript
const biggest = nums =>
  nums
    .map(String)
    .sort((a, b) => (b + a) - (a + b))
    .join('')
    .replace(/^0+(.)/, '$1');
```

> _From [codewars.com](http://www.codewars.com/)_

## Question 2

Write a function that will solve a 9x9 Sudoku puzzle. The function will take
one argument consisting of the 2D puzzle array, with the value 0 representing
an unknown square.

There will be no need to assume and test possibilities on unknowns and this can
be solved with a brute-force approach.

Example:

```javascript
var puzzle = [
            [5,3,0,0,7,0,0,0,0],
            [6,0,0,1,9,5,0,0,0],
            [0,9,8,0,0,0,0,6,0],
            [8,0,0,0,6,0,0,0,3],
            [4,0,0,8,0,3,0,0,1],
            [7,0,0,0,2,0,0,0,6],
            [0,6,0,0,0,0,2,8,0],
            [0,0,0,4,1,9,0,0,5],
            [0,0,0,0,8,0,0,7,9]];

sudoku(puzzle);
/* Should return
[[5,3,4,6,7,8,9,1,2],
[6,7,2,1,9,5,3,4,8],
[1,9,8,3,4,2,5,6,7],
[8,5,9,7,6,1,4,2,3],
[4,2,6,8,5,3,7,9,1],
[7,1,3,9,2,4,8,5,6],
[9,6,1,5,3,7,2,8,4],
[2,8,7,4,1,9,6,3,5],
[3,4,5,2,8,6,1,7,9]]
*/
```

Place your code within the following code block:

```javascript
  //code in here
```

> _From [codewars.com](http://www.codewars.com/)_

## Question 3

Extend the String object to create a function that converts the value of the
String to and from Base64 using the ASCII character set.

Example:

```javascript
// should return 'dGhpcyBpcyBhIHN0cmluZyEh'
'this is a string!!'.toBase64();

// should return 'this is a string!!'
'dGhpcyBpcyBhIHN0cmluZyEh'.fromBase64();
```

Place your code within the following code block:

```javascript
//Extend the String object with toBase64() and fromBase64() functions
String.prototype.toBase64 = function(){

  var asci = function(b){
    var a =  "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    return a[parseInt('00'+b,2)];
  }
  var txt = ''
  for(var i = 0;i<this.length;i=i+3){
    var s = this.byteAt(i)+this.byteAt(i+1)+this.byteAt(i+2)+this.byteAt(i+2);
    txt += asci(s.substr(0,6))+asci(s.substr(6,6))+asci(s.substr(12,6))+asci(s.substr(18,6));
  }
  if(this.length%3===1){
    var s = this.byteAt(this.length-1)+'0000000000000000';
    txt += asci(s.substr(0,6))+asci(s.substr(6,6));
  }
  if(this.length%3===2){
    var s = this.byteAt(this.length-2)+this.byteAt(this.length-1)+'00000000';
    txt += asci(s.substr(0,6))+asci(s.substr(6,6))+asci(s.substr(12,6));
  }

  return txt;
}
String.prototype.fromBase64 = function(){
    var dec2Bin = function (dec){
       var ret = (dec >>> 0).toString(2);
      return ('00000000'.substr(0,8-ret.length)+ret).substr(2);
    }
    var a =  "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    var txt = '';
    for(var i = 0;i<this.length;i=i+1){
      txt += dec2Bin(a.indexOf(this[i]));
    }

    var ret = '';
    for(var i = 0;i<txt.length;i=i+8){
      ret += String.fromCharCode(parseInt(txt.substr(i,8),2));
    }
    return ret;
}

String.prototype.byteAt = function(idx){
  var dec2Bin = function (dec){
    var ret = (dec >>> 0).toString(2);
    ret =  '00000000'.substr(0,8-ret.length)+ret;
     return ret;
  }
  var v = this.charCodeAt(idx);
  return dec2Bin(v);
}
```

> _From [codewars.com](http://www.codewars.com/)_

## Question 4

Explain the benefits and drawbacks of prefix / post fix notation using the Lisp
and Forth we have gone over thus far. Give an example of both.

```bash
Both pre- and postfix have basically the same advantages over infix notation. The most important of these are:

much easier to translate to a format that is suitable for direct execution. Either format can trivially be turned into a tree for further processing, and postfix can be directly translated to code if you use a stack-based processor or virtual machine

entirely unambiguous. Infix notation requires precedence and associativity rules to disambiguate it, or addition of extra parentheses that are not usually considered part of the notation. As long as the number of arguments to each operator are known in advance, both prefix and postfix notation are entirely unambiguous: "* + 5 6 3" is (5+6)*3, and cannot be interpreted as 5+(6*3), whereas parenthesis is required to achieve with infix.

supports operators with different numbers of arguments without variation of syntax. "unary-op 5" and "ternary-op 1 2 3" both work fine, but need special syntax to make them work in infix.

Notice that LISP languages (e.g. Common Lisp, Scheme, Clojure and many specific dialects inspired by them like AutoLISP, Emacs-LISP, MELT, etc...) are all using a prefix-syntax: every expression starts with a left parenthesis, then the operator, then the operands, then the right parenthesis. These expressions are called S-expressions. For example 1+2*3 is typed as (+ 1 (* 2 3)) and there is no need for operator precedence.

The advantages of such a simple syntax (probably the simplest possible one for ASTs, outside of stack languages à la Forth) include:

easy to remember syntax rule for human developers
easy and quick to parse for language implementations
easy to emit when generating code in s-expressions (from some AST representation)
ability to easily make homoiconic languages above them
ability to handle many operands (e.g. have variadic operators or functions, or functions with many formal arguments)
simple to read, once you can match a left parenthesis with its right one
The disadvantage of such syntax is a pun on the language: Lots of Insipid Stupid Parenthesis. However (believe it or not) any Lisp coder don't see the parenthesis as agressive, and uses the ability (provided by any good editor) to match parenthesis when reading code on the screen.

BTW, what is important is not to convert textual representation from e.g. infix to prefix, but to parse expressions into AST (abstract syntax trees). Very often, an AST is a tree-like structure in memory, keeping more information that the simple syntactical shape (e.g. the source location, as a file name, line number, column number, or some type information, etc...).
```

## Question 5

Given the following markup, how would you go about using CSS to style
`div`s 1-3 into a simple emoticon conveying your comfort with positioning in CSS
(e.g. `-_-` or `= ]`)?

```html
<body>
  <div class="first">

  </div>
  <div class="second">

  </div>
  <div class="third">

  </div>
</body>
```

```CSS
<!-- Your CSS here -->
```

## Question 6

Please read the following:

> There are 256 possible shades each of red, green and blue (0 through 255). If we wanted to produce white (the brightest levels of all three colors combined), we’d need to write #255255255. That’s nine digits long.

> Hex codes use the hexadecimal number system to make it possible for 256 numbers to be represented with only two digits. Instead of counting 0 through 10 like our regular decimal number system, it counts 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F and then 10, followed by 11, 12, 13, 14, 15, 16, 17, 18, 19, 1A, 1B, 1C, 1D, 1E, 1F and then 20. Make sense?

> This means that 256 numbers can be represented using only two digits, instead of the 100 that are possible with our decimal number system (0 through 99). So the highest possible two digit number is not 99 but FF (equal to 255). This is why white is #FFFFFF, pure red is #FF0000, pure green #00FF00 and pure blue #0000FF.

> _From [codeconquest.com](http://www.codeconquest.com/hex-color-codes/)_

Given this understanding of how hex codes are generated, please build a JavaScript function that takes a hex code as an argument and returns complimentary colors of the given color from the color wheel in the form of their hex codes.

```javascript
// your code here
```


<!--
Thanks for reading the diagnostic in its entirety.  If you're reading this,
happy April Fool's Day.  Delete this entire file and write a short explanation
of why it's important to read things carefully and in their entirety.

Bonus: Tell me how upset you are with me becuase you had to do this

Shhhh, don't tell your classmates...
 -->
