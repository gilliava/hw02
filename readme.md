> **The Academic Honesty Policy (see Brightspace) is applicable to all work you do in CS 3270/5270.**

# CS 3270: Programming Languages

## Homework 2

Exercises with the Backus-Naur Form.

## GitHub notes

This homework does not include C++ coding and hence, does not need CLion. However, it requires interaction with Git and GitHub. You have two options for this interaction. You can clone your homework repository just as you cloned Homework 0 (if you did it) in CLion. The repository would open as a project in CLion without any connection with C++. You can then use CLion's version control system interface to interact with Git/GitHub (i.e., perform commits and pushes).

You can also perform the necessary interactions with Git/GitHub via a *Bash* window on Windows or the terminal on MacOS. The process is very simple with only a few commands that you need to type in. If you would like to go this route, please see [GitHub notes](github-notes.md) for more information on cloning, committing, and pushing, on the command line. If you have any problems, please let the instructor know.

## Assignment

### Exercise 1

Consider the following BNF grammar with `<program>` as the start symbol:

```text
    <program> -> begin <stmts> end

      <stmts> -> <stmt>
              |  <stmt> <stmts>

       <stmt> -> <decl_stmt>
              |  <assign_stmt>
              |  <if_stmt>
              |  <while_loop>

  <decl_stmt> -> <type> <var> = <num>

<assign_stmt> -> <var> = <expr>

    <if_stmt> -> if ( <condition> ) <stmt>

 <while_loop> -> while ( <condition> ) <stmt>

       <type> -> byte | int | short

        <var> -> x | y

        <num> -> 0 | 1 | 2 | 3 | 4 | 5

       <expr> -> <term> + <term>
              |  <term> - <term>
              |  <term>

       <term> -> <var> | <num>

  <condition> -> <term> <rel_op> <term>

     <rel_op> -> == | != | < | > | <= | >=
```

In `exercise-1.txt`, write the ***rightmost derivation*** for the following snippet of code based on the BNF grammar above.

```text
begin
  int y = 5
  
  if ( y == 5 )
    while ( y > 0 )
      y = y - 2
end
```

**The derivation should follow the same layout as the examples in class, i.e.:**

* **Only the first expansion** should have the nonterminal start symbol listed on the LHS (i.e., before the `->` symbol). All remaining expansions should have an empty LHS (i.e., nothing before the `->` symbol).

* Expand only **one nonterminal at a time** (i.e., each line in the derivation should represent the expansion of a single nonterminal).

* Each expansion of the derivation should be **in a single line**. That is, an expansion should not be in multiple lines based on the layout of the original code. All terminals and nonterminals should be in a one line for a particular expansion.

### Exercise 2

In `exercise-2.txt`, use the DOT graph description language to represent the parse tree for the derivation in **Exercise 1**. An example DOT code that will *render* a parse tree that you saw in class can be found at [example-parse-tree.txt](example-parse-tree.txt). An explanation of this file can be found at [example-parse-tree.md](example-parse-tree.md).

You can use the website [dreampuf.github.io/GraphvizOnline](https://dreampuf.github.io/GraphvizOnline) to *render* DOT code. For example, to see the rendered parse tree from the example above, delete any DOT code that is displayed when you open the website and copy-and-paste the code in [example-parse-tree.txt](example-parse-tree.txt). You can use the website to develop your DOT code for this exercise. Start by copying the starter template in `exercise-2.txt` to the website.

### Exercise 3

BNF can be used to specify the syntax of languages other than programming languages. For example, we can define a BNF grammar that specifies the syntax of HTML, XML, YAML, and even BNF itself.

Consider the following (very simplified) production rules in BNF that describes the syntax of BNF itself. The start symbol is `<syntax>`. Unlike the production rules in the previous exercises, the terminals are enclosed by double quotes. This is to distinguish the terminals from the actual "code" portion of the production rules.

```text
       <syntax> -> <rule>
                |  <rule> <syntax>

         <rule> ->  <non_term> "->" <option>

     <non_term> -> "<" <non_term_name> ">"

<non_term_name> -> "factor"
                |  "ident"
                |  "expr"
 
       <option> -> <unit>
                |  <unit> "|" <option>
 
         <unit> -> "const"
                |  <non_term>
                |  "(" <unit> ")"
```

In `exercise-3.txt`, write the ***leftmost derivation*** for the following production rule:

```text
< factor > -> < ident > | const | ( < expr > )
```

Note that in this exercise, you are trying to see if the *sentence* consisting of (in this order): the less than symbol `<`, the rule name `factor`, the greater than symbol `>`, the arrow symbol pair `->`, the less than symbol `<`, the rule name `ident`, the greater than symbol `>`, the vertical line `|`, the literal name `const`, the vertical line `|`, the left parenthesis `(`, the less than symbol `<`, the rule name `expr`, the greater than symbol `>`, and the right parenthesis `)`, representing a valid sentence in the BNF language. That is, there is a derivation starting from the `<syntax>` start symbol all the way to this sentence.

As stated above, all terminals in the sentential forms should be placed inside double quotes, hence the sentence that you are expected to reach at the end of your derivation is the following:

```
"<" "factor" ">" "->" "<" "ident" ">" "|" "const" "|" "(" "<" "expr" ">" ")"
```

Just as Exercise 1, **expand only one nonterminal at a time** (i.e., each line in the derivation should represent the expansion of a single nonterminal). Also, **a single expansion should be all in one line**.

### Exercise 4

In `exercise-4.txt`, use the DOT graph description language to represent the parse tree for the derivation in **Exercise 3**. In the parse tree, you **don't need to include double quotes** for the terminal values.

## Final notes

* Ensure that your name, VUnetID, email address, and the honor code statement appear in the header comments of files you altered. The honor statement that you are to type in is "I have neither given nor received unauthorized help on this assignment", or something to that extent. The statement must be a complete statement. Don't just say "I agree".

* In a parse tree, once a terminal has been reached, there is no need to "expand" it any more. That is, a terminal in a parse tree should be represented by a leaf node.
