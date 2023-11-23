# Big Impressive Title
## Subtitles Are Nice

This is a little cheat sheet of Markdown syntax I wrote for myself while making this project. I'm getting rusty...

### Section 1: General Formatting
To **bold** or *italicize* words is pretty easy.
And (by the way newlines mean nothing if they aren't BREAK newlines)
* bullets can be
    * super duper. (automatically a gap was created above)
* as simple

1. or as
    1. complicated
        1. (so this has to be in number order to be recognized as a bullet
        * but you can mix and match
        - with plenty of styles...
        8. as well as other things
        6. but also some will automatically change (this is actually bullet 6)
    - and NEVER add parentheses around the bullet icon because that's not syntax!)
2. as these ones
3. can be

### Section 2: Special Formatting
First off, 

> Side note: This is one. 

However, way cooler is the `bubble words` you can do or even bubble boxes:
```
This bubble box is a standard one, but you can also
```
``` bash
$ runAProgram ./onArg1 ../andArg2
```
and also if I add a newline after this and then

        confusingly this also works as a way to make
            a bubble box
                even with indents
        so that you can write pseudocode things

I think I prefer the other way to be clearer.

    Also just a a single indent will work for this too as long as you add that newline!! 
        so the extra indent in the previous box actually gets added inside the box :0 (but make sure you don't let it spill over to next line because it's not preserved)

### Section 3: Links
You can do regular links like this:
[Link name](www.theLink.com)

Or, for an image that is saved elsewhere in your repository:
![Indexer data flow](media/indexer/data-model.png)

Or, for **[:arrow_forward: Video demo](https://dartmouth.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=a36d11ab-5263-4904-9520-ad16017c24fa)**

### Section 4: Math
Inline, you can easily use $\sqrt{3x-1}+(1+x)^2$ to show math equations.

Alternately, you can use
$$\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)$$
or take out the `$$` with

```math
    x = {-b \pm \sqrt{b^2-4ac} \over 2a} 
```
```math
\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
```


### Section 3: Icons
This section has icons like
:arrow_forward:








### Sources

The querier's only interface with the user is on the command-line; it must always have two arguments.

```
querier pageDirectory indexFilename
```

For example, if `letters` is a pageDirectory in `../data`,

``` bash
$ querier ../data/letters ../data/letters.index
```


### Inputs and outputs

**Input**: the querier reads files from a directory by constructing file pathnames from the `pageDirectory` parameter followed by a numeric document ID (as described in the Requirements). It loads an inverted index of words from `indexFilename`, which have corresponding word frequencies in a list of documents. It also takes in a query from standard input, which a sequence of words with optional boolean operators, which will be searched for in the index.

**Output**: We print the ranked list of documents which match the query provided by the user. 

### Functional decomposition into modules

We anticipate the following modules or functions:

 1. *main* and *parseQrgs*, which parse arguments and initialize other modules;
 2. *parseQuery*, calls on the next 4 helper functions to process the query and print results.
 3. *tokenizeQuery*, which reads the input character by character and validates it as a query.
4. *validateQuery*, which reads the input word by word to validate it.
5. *matchQuery*, which compiles the list of documents which contain the words in the query
6. and *printMatches*, which prints the list of documents in order of their "score"

And some helper modules that provide data structures:

 1. *index*, a module providing the data structure to represent the in-memory index, and functions to read and write index files;
 2. *pagedir*, a module providing functions to load webpages from files in the pageDirectory;

### Pseudo code for logic/algorithmic flow

The querier will run as follows:

    parse the command line, validate parameters, initialize other modules with parseArgs
    call parseQuery, with an empty pointer to an array of words, a number of words, a words index, a document counters set, and the pageDirectory

where *parseQuery:*

      takes each line of input and
        tokenizes the query character by character
          validates the word syntax of the query
            mathces the query to a set of documents
              and prints that set of documents in decreasing order by score
      making sure to free the index and lines afterwards


### Major data structures

The key data structure is the *index*, mapping from *word* to *(docID, #occurrences)* pairs.
The *index* is a *hashtable* keyed by *word* and storing *counters* as items.
The *counters* is keyed by *docID* and stores a count of the number of occurrences of that word in the document with that ID. 

### Testing plan

*Unit testing*.  We test the parseArgs module using basic calls on querier with error parameters. 

*Integration testing*.  The *querier*, as a complete program, will be tested by building an index from a pageDirectory, parsing a query given by the user, creating a new set of "matched" documents, and printing that list in order. We will not only test using our own input/outputs from our crawler & indexer modules, but also using a side program called fuzzquery provided by the CS50 curriculum.

1. Test `querier` with various invalid arguments.
	2. no arguments
	3. one argument
	4. three or more arguments
	5. invalid `pageDirectory` (non-existent path)
	5. invalid `pageDirectory` (not a crawler directory)
	6. invalid `indexFile` (non-existent path)
	7. invalid `indexFile` (existing, read-only file)
2. Run *querier* on a variety of pageDirectories with indexes and examine the output documents listed. Run with *valgrind* to ensure no memory leaks or errors.
3. Run *fuzzyquery* with *querier* to see if the random words are able to reveal any other bugs. 
