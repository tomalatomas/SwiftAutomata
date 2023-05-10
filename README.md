# SwiftAutomata

School project for course IZA (Programming Apple Devices) at FIT BUT.

## Task

Implement a program in the Swift language that simulates the transition between states necessary to accept an input string and a nondeterministic finite automaton. If the string is accepted by the finite automaton, the sequence of states will be printed to stdout. If the string is not accepted, the program ends with an error. Tested automata will contain at most one sequence of states for input acceptance.
### Running the program

The program can be run using the `swift run proj1 <input_string> <file_name>` command in the program's home directory (the directory containing the *Package.swift* file). 
- `<input_string>` - contains individual symbols separated by `,` (comma), for example: 
- `swift run proj1 a,b,c automata.json`: the input string contains three symbols, 
- `swift run proj1 "First,Second,Third,+1š_,Symbol with space" automata.json`: the input string contains five symbols, 
- `swift run proj1 "" automata.json`: the input string does not contain any symbols. 
- `<file_name>` - the path to the file containing the representation of the finite automaton stored in JSON format.
### JSON attributes
- states - an array of strings containing individual states,
- symbols - an array of strings containing individual symbols, 
- transitions - an array of transitions, where each transition ($`pa \rightarrow q`$) contains the attributes: 
- from - the current state $`q`$, 
- with - the current symbol $`a`$, 
- to - the new state $`q`$,
- initialState - initial state,
- finalStates - an array of final states.
#### Finite automaton no. 1 
- Language of the automaton: $`L=a^*`$

```javascript

{
  "states" : [
    "A"
  ],
  "symbols" : [
    "a"
  ],
  "transitions" : [
    {
      "with" : "a",
      "to" : "A",
      "from" : "A"
    }
  ],
  "initialState" : "A",
  "finalStates" : [
    "A"
  ]
}
```


#### Finite automaton no. 2 
- Language of the automaton: $`L=(ab)^+c^+`$

```javascript

{
  "states" : [
    "S",
    "AB",
    "C",
    "D"
  ],
  "symbols" : [
    "a",
    "b",
    "c"
  ],
  "transitions" : [
    {
    "with" : "a",
    "to" : "AB",
    "from" : "S"
    },
    {
    "with" : "a",
    "to" : "D",
    "from" : "S"
    },
    {
      "with" : "b",
      "to" : "AB",
      "from" : "S"
    }, {
      "with" : "a",
      "to" : "AB",
      "from" : "AB"
    },
    {
      "with" : "b",
      "to" : "AB",
      "from" : "AB"
    },
    {
      "with" : "c",
      "to" : "C",
      "from" : "AB"
    },
    {
      "with" : "c",
      "to" : "C",
      "from" : "C"
    }
  ],
  "initialState" : "S",
  "finalStates" : [
    "C"
  ]
```
