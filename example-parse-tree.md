# CS 3270: Programming Languages
## Brief Introduction to the DOT Language

The DOT language is a language used to describe graphs. An example DOT file named [example-parse-tree.txt](example-parse-tree.txt) is provided. Let's at a look at this example.

The graph definition starts with the keyword `graph` and the name of the graph, which in this case is `ParseTree`.

```text
graph ParseTree {
```

## Node properties

The next line provides two properties for the nodes in the graph. Setting `shape` to `none` will suppress the drawing of shapes that are usually drawn around the nodes. Setting `ordering` to `out` specifies that the ordering of nodes should be from left-to-right based on how they are defined in the graph definition. By default, the rendering of the graph may change the ordering of a parent node's child node. In a parse tree, the order is important. Leave this line as-is.

```text
node [shape = none, ordering = out];
```

## Text labels

When there are multiple nodes with the same identical name, Graphviz will only generate a single node of that name and all edges going to a node with the same name will point to that single generated node. This is not how a parse tree should be drawn, because each terminal in a parse tree must have its own node even if the node names are the same.

Hence, each node in the graph definition must have a unique name or label. In the example parse tree, there are two nodes with the name `<term>` and three nodes with the name `<var>`. Also, there are two nodes with name `A`. In order to allow nodes with identical names to be rendered separatedly, *text labels* will need to be defined. In the graph definition, each a different node name is used (i.e., `var1` and `var2`). However, both node names can use the same label. Simply separate the node names by a comma and then specify the label after the list of names. For example:

```text
var1, var2 [label = "<var>"];
```

Note that such text labels are only required when multiple nodes use the same name. If a node has a unique name (i.e., not found anywhere else in the parse tree), the name can simply be written in the graph definition.

## Graph definition

Each element on the right hand side of a production rule should be connected to the nonterminal on the left hand side of the production rule using `--` (i.e., two dashes). For example:

```text
"<program>" -- "<stmts>";
```

The nodes representing the `<program>` and `<stmts>` nonterminals are placed inside double quotes, because some of the characters in the node name are special characters in the DOT language.

When a parent node has multiple child nodes, list each child node separated by a comma. For example, the production rule `<stmt> -> <var> = <expr>` is represented by the following:

```text
stmt -- var1, "=", "<expr>";
```

The node named `var1` is the first `<var>` nonterminal in the parse tree. The node representing the equal sign is named `"="`. The equal sign is placed inside double quotes as some non-alphanumeric characters are special characters in the DOT language.

**Note: for readability purposes, each line in the graph definition should only contain one `--` symbol.**