This is a tiny compiler based written completely in python and can compile to C code
Our language will allow a variety of the basic operations that you'd expect from a programming language. In particular, it will support:

    1.Numerical variables
    2.Basic arithmetic
    3.If statements
    4.While loops
    5.Print text and numbers
    6.Input numbers
    7.Labels and goto
    8.Comments
There are no functions, no arrays, no way to read/write from a file, and not even an else statement. But with just this small set of 
constructs, you can actually do a lot. 
but it will also setup the compiler in such a way that many other features will be straight forward to add later.
Our compiler will follow a three step process that is illustrated above. First, given the inputted source code, it 
will break the code up into tokens. These are like words and punctuation in English. Second, it will parse the tokens 
to make sure they are in an order that is allowed in our language. Just like English sentences follow specific structures 
of verbs and nouns. Third, it will emit the C code that our language will translate to compiler



**Lexer**: The lexer consists of the following functions:
1.nextChar(self)
2.peek(self)
3.abort(self, message)
4.skipWhitespace(self)
5.getToken(self)
6.skipComment(self)
7.checkIfKeyword(tokenText):
8.class TokenType(enum.Enum)    
                        
In order to paint a clear picture of how the compiler actually works,lets start from the beginning in the main function,where the lexer is 
called at the beginning(along with the others).
The compiler takes in a input file,and the first thing it does,is pass it to an instace of the Lexer class
Here's are the steps that follow for each this happens:
1.The lexer's constructer will take in the input file,initialize the current character and the position of the character to be processed,
along with a call to the next nextChar
2.nextChar is used to check if it's the end the file and exit
3.curChar is what the lexer will constantly check to decide what kind of token it is
3.peek(self) is used for special conditions to check the character AFTER the character being processed. This is called in special cases,
like when the code(being given) is ==
4. The getToken() Return the next token.It will be called each time the compiler is ready for the next token and it will do the 
work of classifying tokens. nextChar and peek are helper functions for looking at the next character. skipWhitespace consumes
the spaces and tabs that we don't care about. abort is what we will use to report an invalid token.


**Parser**:
The parser is the component that will make sure the code follows the correct syntax. It does this by looking at the tokens, 
one at a time, and deciding if the ordering is legal as defined by our language.
In this case, parser object keeps track of current token, checks if the code matches the grammar, and emits code along the way.
The following functions make up most of the parser:
class Parser()- called in the main function to initialize the parser
Other major functions include:
1.def checkToken(self, kind) returns true if the current token matches.
2.def checkPeek(self, kind): returns true if the next token matches.  
3.self.nextToken() is called twice to initialize current and peek.
4.def match(self, kind) matches current token. If not, error. Advances the current token.
5.def nextToken(self) advances the current token.
6.def isComparisonOperator(self) return true if the current token is a comparison operator.
7.def statement(self) checks the first token to see what kind of statement(if,while,goto) this is.


**Emittor**:
The emitter is the component that will produce the compiled code. In this case,it'll be carried out by 3 major functions(along with the others):
1.def __init__(self, fullPath): the constructer used to initialize the other two functions.
2.def emit(self, code): to generate code on demand
3.def headerLine(self, code):headerLine(along with writeFile) is used to output information about the code being generated.
The following steps take place:
1.The __init__ function sets up some basic variables that will be used by the other functions.
2. First, it sets up a variable called fullPath which stores the path to the source file that will be analyzed.
3.Next it sets up a variable called header which stores an empty string initially and sets up a variable called code which stores an empty string initially as well.
4.The emit(self,code) function takes one argument: code which is an empty string initially.It uses this argument to generate a block of code that will be outputted onto stdout .
This block of code consists of one line of text followed by a newline character (\n).
5.The headerLine and writeFile functions are identical in terms of their functionality; they both simply store an empty string into their respective variables respectively.
However, because they are defined within the same function as emit , they are executed before any actual code is generated by emit
The code will create an Emitter object and initialize it with the full path to the file where the code should be written.
6. The emit() method will take in a string of code and will append it to the current code string.
7. The emitLine() method will do the same, but for each line of code.
8. Finally, the headerLine() method will add a line of text at the beginning of 
 the generated code, and writeFile() will write all of the generated code to the outputFile .

 The Emitter object will also keep track of the generated code and output it to the outputFile .











