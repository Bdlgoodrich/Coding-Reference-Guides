JavaScript Basics Reference Guide


Concepts:
JavaScript can execute not only in the browser, but also on the server, or actually on any device that has a special program called the JavaScript engine.
Javascript is written and executed as plain text


The browser has an embedded engine sometimes called a “JavaScript virtual machine”.
Different engines have different “codenames”. For example:
V8 – in Chrome, Opera and Edge.
SpiderMonkey – in Firefox.
…There are other codenames like “Chakra” for IE, “JavaScriptCore”, “Nitro” and “SquirrelFish” for Safari, etc.
Node.js supports functions that allow JavaScript to read/write arbitrary files, perform network requests, etc.
In-browser JavaScript can do everything related to webpage manipulation, interaction with the user, and the webserver.
JavaScript from one page may not access the other page if they come from different sites (from a different domain, protocol or port).
This is called the “Same Origin Policy”. To work around that, both pages must agree for data exchange and must contain special JavaScript code that handles it. 
NOTE: js run in the server does not have this problem
***Google MDN "term" to find official documentation/info on code concept


Developer tool "Console" shows any errors on page and has command prompt which can run js
         To insert multiple lines, press Shift+Enter. This way one can enter long fragments of JavaScript code.


**Node.js is non-browser-based JavaScript


the <script tag in html designates code to run as js with imbedded setup


Statements (like "alert") can be separated by ; or a line break
        implicit semicolons exist -> automatic semicolon insertion
        **not perfect, so safer to use them


Comments are //single line OR  /*multiple lines*/
******In most editors, a line of code can be commented out by pressing the Ctrl+/ hotkey for a single-line comment and something like Ctrl+Shift+/ – for multiline comments


Please make sure that "use strict"; is at the top of your scripts, otherwise strict mode may not be enabled.  //This is permanent for the whole script
        Use Shift+Enter after line for use in console


Variables use keyword "let"
variable names can contain letters, numbers, and/or '$' or  '_'
        first character must not be a number (digit)
        variable names are case sensitive and cannot be keywords
         *** “dynamically typed” ***
Constants use keyword "const"
        UPPERCASE_AND_UNDERSCORE constants are used for values known before execution (like hex color codes) ie aliases for hardcoded values




Data Types:
* number
   * represents both integers and floating points
   * include Infinity, -Infinity, and NaN
   * script will not stop ("die") if maths are wrong
* bigInt
* string
   * can use single or double quotes
   * backticks allow for ${varName} insertions
      * eg  alert( `Hello, ${name}!` ); 
      * expression inside { } is evaluated separately, then added into the string
   * a string can have 0 (empty), 1, or more characters
* boolean
   * can be the result of comparison operators
* null
   * not any other data type
   * represents “nothing”, “empty” or “value unknown”
* undefined
   * not any other data type
   * represents “value is not assigned”
   * assigned by default with variable is created
* symbol
   * used for unique identifiers for objects
* object
   * NOT a primitive data type
   * used to store collections of data and complex entities


** keyword (operator) "typeof" returns string with the type of the operand**
        note: null returns typeof "object" and is wrong
        ex:         typeof x
                typeof(x+y)


Interactions: functions that interact with the user
* alert
   * creates modal window with parameter as message
      * "modal" means the user can't interact with anything else until they deal with it
   * ex: alert("Hello");
* prompt
   * creates modal window with title as message to user, and input field for user
   * includes buttons OK/Cancel
   * ex: result = prompt(title, [defaultValue]);  //[ ] denotes optional initial value
   * ex: test = prompt("Test", ' ');  //
   * returns input if OK is clicked
   * returns null if input is canceled (with button or esc key)
Note: returns null even if an initial value is present
****[ ] denote optional parameters *****
* confirm
   * creates modal window with parameter as message
   * includes OK and Cancel buttons
   * returns boolean result
      * true if OK
      * otherwise, false
   * ex: result = confirm(question);
NOTE: the position and appearance of a modal window is determined by the browser and cannot be modified


Explicit type conversions
strings:
        ex:         let value = true;
                value = String(value);
numbers:
        conversion for mathematical functions and expressions happens automatically
        can be done explicitly esp when reading values from string-based source
        ex:        let str = "123";
                num = Number(str);
                num = +str;
        results in NaN if argument contains non-number characters
        true and false become 1 and 0
        undefined becomes NaN
        null becomes 0
        note: white spaces are automatically removed
boolean:
        ex: Boolean(value);
        intuitively "empty" values (0, null, undefined, NaN, false, empty string) become "false"
        everything else becomes "true"
        note: the string "0" is true, but the number 0 is false
                likewise, " " is true


Basic operators
        An operand – is what operators are applied to. For instance, in the multiplication of 5 * 2, there are two operands: the left operand is 5 and the right operand is 2. Sometimes, people call these “arguments” instead of “operands”.
An operator is unary if it has a single operand.
        An operator is binary if it has two operands.
Operators include:
* Addition +
* Subtraction -
* Multiplication *
* Division /
* Remainder %
* Exponentiation **
   * a ** b is a to the power of b
   * 2 ** (1/2)


+ will also concat strings
        if any operand for + is a string, the whole result is converted to string
        ex: 2+2+'1'; returns 41
ALL other arithmetic operators will convert operand into numbers


+value converts value into a number


Operator Precedence:
        Every operator is assigned a number and higher numbers execute first, equal numbers execute from right to left
        Parenthesis always override precedence
Assignment ( = ) has a low precedence of 2


a+=b, a-=b, a*=b, a/=b   //now, a = a+b, a = a-b, a = a*b, a = a/b
++a  //increment up  **variables only
--a  //increment down  **variables only
NOTE: a++ and ++a are both valid. The former returns a, then increments it, the later increments a, then returns it


commas can be used to separate different operations performed on the same line


Comparisons are straightforward
<, >, <=, >=, ==, !=
note: all comparisons return a boolean


The algorithm to compare two strings is simple:
1. Compare the first character of both strings.
2. If the first character from the first string is greater (or less) than the other string’s, then the first string is greater (or less) than the second. We’re done.
3. Otherwise, if both strings’ first characters are the same, compare the second characters the same way.
4. Repeat until the end of either string.
5. If both strings end at the same length, then they are equal. Otherwise, the longer string is greater.
NOTE: this is case-sensitive and lowercase letters are greater


When comparing values of different types, Javascript converts the values to numbers
NOTE: this means == cannot differentiate between 0 (or "") and false


Strict equality is === and will not convert different types of values
        Likewise with !==
ex:         null == undefined //true
        null === undefined //false


**Don’t use comparisons >=, >, <, <= with a variable which may be null/undefined, unless you’re really sure of what you’re doing. If a variable can have these values, check for them separately.


If statements
if (booleanExpression) {
        //code to execute if true
}
A number 0, an empty string "", null, undefined, and NaN all become false. Because of that they are called “falsy” values.
Other values become true, so they are called “truthy”.
else {  } blocks are optional
else if (booleanExpression2) {  } blocks are also optional


ternary or conditional operator: basically a single if/else pair
ex: let result = (condition) ? value1 : value2;
        returns value 1 if condition is truthy
        returns value 2 if condition is falsy


Logical Operators
* || (or)
   * boolean: if any operand is true, returns true
   * non-boolean operands are converted to booleans, then evaluated
   * useful in if statements
   * ex: if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'The office is closed.' ); // it is the weekend
}
   * operands are evaluated from left to right
      * stops after first truthy value, returns that value in original form
      * if all falsy, returns final value in original form
      * ex: firstName, lastName, nickName are all optional inputs
alert( firstName || lastName || nickName || "Anonymous");
ex:         true || alert("not printed");
false || alert("printed");
* && (and)
   * boolean: returns true if ALL operands are true
   * non-boolean operands are converted to booleans, then evaluated
   * operands are evaluated from left to right
      * stops after first falsy value, returns that value in original form
      * if all truthy, returns final operand in original form
   * has higher precedence than ||
      * eg a && b || c && d => (a && b) || (c && d) 
* ! (not)
   * non-boolean operands are converted to booleans
   * returns inverse boolean value
   * has highest precedence
   * !! can be used to convert to boolean
* ?? (nullish coalescing)
   * read operands from left to right
   * if first operand is defined, returns it  //defined is anything not null or undefined
   * if first operand is not defined, returns second operand
   * ex:        let height = 0;
alert(height || 100); // 100
alert(height ?? 100);  //0
   * has the same precedence as ||
      * this may necessitate parentheses 


While and For Loops
while (condition) { 
        //loop body 
}
while (i) => while (i != 0) when i is a number


do {
        //loop body
} while (condition);  //executes body once, then checks condition


for (begin; condition; step) {
        //loop body
}
Any part of the loop can be skipped if unnecessary
let i = 0;
for (; i < 3;) {
  alert( i++ );
}
directive "break" will automatically end a loop
        will only break the inner-most loop if nested
directive "continue" ends the current iteration and rechecks the condition to begin a new iteration
note: directives cannot be used to the right of ternary operators
        (i > 5) ? alert(i) : continue; //doesn't work


Labels can be given to a loop with "labelName:" before for( ) on either the same or a new line
"break labelName;" will break out of the specified loop and all by default, all loops within it


Switch statement:
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]
  case 'value2':  // if (x === 'value2')
    ...
    [break]
  case 'value3': 
  case 'value4': // if (x === 'value3' OR 'value4')
    ...
    [break]
  default:  //not required if no default action is needed
    ...
    [break]
}
NOTE: this is a strict equality, so type matters!!


Functions:
Function Declaration:
defined with "function name(parameter1, parameter2, etc) { //function body }
variables declared inside a function exist only within that function
note: if a variable of the same name is declared inside the function, only the inside variable is used and outside (global) variables remain unchanged
        global variables are not often used in JavaScript
Parameters not passed into the function are set as undefined, unless a default value is specified
        ex:         function name(parameter=defaultValue)
                function name(parameter=anotherFunction() )
        note: the variable can be assigned a default value later in the function with
                parameter = parameter || defaultValue;  OR
                parameter = parameter ?? defaultValue;  OR
                if (parameter === undefined) { parameter = defaultValue; }
Return values are specified with the directive "return"
This also acts as a "break" in the function and can be used without an actual return value 
(if the "return" is caught, it is undefined)
note: if not return is specified, function also "returns" undefined
NOTE: functions are usually named with a verbal prefix such as "show" "get" "calc" "check" "create"
Additional functions can be created to "self-describe" actions, even when they are only called once
Function Expression:
ex: let name = function() {  //function body };
***In both cases, a function is simply a value for a variable***
        if you call the function name without parentheses, you get the code of the function without executing the function
        likewise, "let newFunct = oldFunct;" copies the code from the old function and stores it under the variable newFunct


function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}
function showOk() {
  alert( "You agreed." );
}
function showCancel() {
  alert( "You canceled the execution." );
}
// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
**showOk and showCancel are referred to as callback functions or just callbacks
        meaning functions passed as arguments into another function to be called as needed
OR
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}
ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
//creates "anonymous" callback functions within the ask() call


NOTE: function declarations can be made anywhere in the code, before or after the function's use because js first finds all declarations and processes them BUT it's only visible within the block of code where it's declared
        function expressions are only processed when the code reaches them, so the expression must come before any use of the function
** function declarations are easier to find in code, but function expressions allow for conditional declarations


Arrow Functions:
let functionName = (argument1, argument2, etc) => expression;
        parentheses will be empty, but present, if no arguments are needed
ex: 
let age = prompt("What is your age?", 18);
let welcome = (age < 18) ?
  () => alert('Hello!') :
  () => alert("Greetings!");
welcome();
** if you want to include a multi-line expression, use { }; and include a return








________________




Code:
**F12 opens developer tools
<script>
        js to run in browser
</script>
OR
<script src="/path/to/script.js"></script>  //path can be relative or absolute
//multiple <script> tags are used for multiple files
        a tag containing a file cannot also contain code
"use strict";  //enables only modern use of code functions when not using modern classes


Variables:
let variableName = 'value';  //strings are single quotes
const constantName = 'value';  //value cannot be changed


typeof x
typeof(x+y)  //returns string of operand type


alert("Hello");
test = prompt("Test", ' ');  //returns input or null
result = confirm(question);  //returns true only with OK


String(value);
Number(string);
        +string;  //does same thing
Boolean(value);
        !!value;  //does same thing


if (booleanExpression1) {
        //code to execute if expression 1 is true
}
if else (booleanExpression2){
        //code to execute if expression 2 is true
        //optional block
}
else {
        //code to execute if both expressions 1 and 2 are false
        //optional block
}


let result = (condition) ? valueTrue : valueElse;
let value = (condition1) ? 'value1' :
  (condition2) ? 'value2' :
  (condition3) ? 'value3' :
  'valueElse';


//firstName, lastName, nickName are all optional inputs
alert( firstName || lastName || nickName || "Anonymous");  //returns first truthy value
alert( firstName ?? lastName ?? nickName ?? "Anonymous");  //returns first defined value


true || alert("not printed");
false || alert("printed");


//finding prime numbers less than or equal to n
let n = 10;
nextPrime:
for (let i = 2; i <= n; i++) { // for each i...
  for (let j = 2; j < i; j++) { // look for a divisor..
    if (i % j == 0) continue nextPrime; // not a prime, go next i
  }
  alert( i ); // a prime
}


Math.round(n) != n  //check for whole number