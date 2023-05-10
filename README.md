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

### Program output

The program will print on stdout the individual states that the input string went through during the simulation on the finite automaton. There will be a new line LF (\n) symbol after each state, including the last one. Sample output for the input string *aaa* and the sample automaton #1 is:

```swift
A
A
A
A
```

<!--There is a space on the last line for proper rendering-->

For the string abc and automaton #2, the expected output is:

```swift
S
AB
AB
C
```

<!--There is a space on the last line for proper rendering-->
### Error states

If an error is detected, the program will terminate correctly, print error information on stderr and return an error code according to the following table:Error typeReturn codeInput string is not accepted by the automaton6Incorrect arguments11Error while working with a file12Error while decoding the automaton20Automaton contains an undefined state21Automaton contains an undefined symbol22Other error99
## Program structure

Use the program structure with the recommended module structure to solve the task. Each module has a separate folder prepared in the *Sources* folder.
### Modules

To be implemented: 
- *FiniteAutomata* - library for representation and decoding of finite automaton 
- *proj1* - module containing main code for program execution 
- *Simulator* - library for simulation of finite automaton

Pre-implemented module: 
- *MyFiniteAutomatas* - Examples of finite automata, inputs, and outputs used in tests
### Testing

Four test sets are prepared in the structure that can be executed using the command `swift test` in the project's home directory. The sets are located in the *Tests/proj1Tests* folder: 
- *FiniteAutomataTests* - two test sets for the simulator 
- *proj1Tests* - two test sets for the resulting binary.

It is recommended to also add your own tests.
### GitLab CI/CD

The structure also includes the *.gitlab-ci.yml* file, which automatically runs tests after each push to the repository on GitLab. If you use the GitLab service, it can help you detect errors as soon as they occur.
### Mac Xcode

To create an Xcode project *.xcodeproj* on a MacOS system, you can use the command `swift package generate-xcodeproj` in the project's home directory or open the Package.swift file.
## Submission

Submit *xlogin00.zip* with your login, which will contain: 
- *Package.swift* 
- *Sources/* 
- *Tests/*

