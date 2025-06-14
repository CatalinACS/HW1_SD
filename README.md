# Text Editor Implementation

## Project Overview
This assignment involved implementing a text editor with advanced features, including undo/redo functionality, text manipulation commands, and file operations. The project was completed over a 3-week development period.

## Implementation Timeline

### Week 1: Foundation and Basic Structure
**Focus**: Core architecture and basic functionality

**Achievements**:
- Designed and implemented the fundamental data structures
- Established the overall program logic and control flow
- Implemented file I/O using `while(1)` loop and `fgets()` for data reading
- Created basic commands:
  - `save`: Save current state to file
  - `quit`: Exit the program

**Key Decisions**:
- Chose doubly linked list structure for efficient text manipulation
- Established command parsing framework

---

### Week 2: Core Operations and Debugging
**Focus**: Text manipulation commands and major debugging phase

**Implemented Commands**:
- `da`: Delete all
- `d`: Delete operation
- `b`: Basic operation
- `gl`: Go to line
- `gc`: Go to character

**Major Challenges**:
- **Delete Operations**: Generated numerous errors due to complex list traversal
- **Debugging Phase**: 2-3 days dedicated to error resolution
- **Memory Management**: Extensive use of debugging tools

**Debugging Tools Used**:
- **Valgrind**: Primary tool for memory error detection
- **GDB**: Used for runtime debugging
- Valgrind reported the majority of memory-related issues

**Navigation Operations**:
- Move operations (`gl`, `gc`) were implemented successfully
- These proved to be more straightforward than deletion operations

## Data Structure Design

### Main Architecture
The program uses a "large list" structure - a doubly linked list of doubly linked lists:

```
      NULL
       ^
       |
 NULL<-a-><-a-><-a-><-a-><-a->NULL
       ^
       |
       v
 NULL<-b-><-b-><-b-><-b-><-b->NULL
       ^
       |
       v
 NULL<-c-><-c-><-c-><-c-><-c->NULL
       |
       v
      NULL
```

**Text Representation**:
```
aaaaa
bbbbb
ccccc
```

### Node Structure Fields
- **`next`**: Move one character forward (horizontal navigation)
- **`prev`**: Move one character backward (horizontal navigation)
- **`nextlist`**: Move to the beginning of the next line (vertical navigation)
- **`prevlist`**: Move to the beginning of the previous line (vertical navigation)

### List Management
- **`LIST->HEAD`**: Points to the first line
- **`LIST->TAIL`**: Points to the last line
- **Boundary conditions**:
  - `LIST->HEAD->prevlist == NULL`
  - `LIST->TAIL->nextlist == NULL`
- **`LIST2`**: Separate list structure for command management

---

### Week 3: Advanced Features and Completion
**Focus**: Remaining commands and undo/redo functionality

**Implemented Commands**:
- `undo`: Reverse previous operation
- `redo`: Reapply undone operation
- `re`: Replace operation
- `ra`: Replace all operation
- `dl`: Delete line
- Additional text manipulation commands

## Advanced Features Implementation

### Undo/Redo System
**Architecture**: Stack-based implementation (as required)

**Undo Operations**:
- **Text Insertion**: Used auxiliary list for state preservation
- **Text Deletion**: Straightforward reversal using stored state
- **Replace Operations**: Implemented argument reversal technique
- **Complex Operations**: Handled all edge cases for each command type

**Redo Operations**:
- **General Approach**: Pop from stack and use `goto` statement
- **Text Insertion**: Called `add` function with stored list data
- **Efficiency**: Trivial implementation for most operations

### Specific Command Challenges

#### Replace All (`ra`) Operation
- **Development Time**: Full day of implementation
- **Approach**: Used two auxiliary lists for argument storage
- **Process**: Complete traversal of the large list structure

#### Replace (`re`) Operation
- **Development Time**: 2 hours of design
- **Implementation**: Pattern matching and replacement logic

#### Undo System Design
- **Development Time**: 5 days for comprehensive undo operations
- **Coverage**: All commands (`re`, `ra`, `d`, etc.)
- **Complexity**: Handled all possible edge cases

## Technical Implementation Details

### Memory Management
- **Variables**: Used multiple `char*` variables (`s1`, `s2`, `s6`, etc.)
- **Purpose**: Proper memory deallocation to satisfy Valgrind requirements
- **Approach**: Systematic cleanup of dynamically allocated memory

### Error Handling
- Comprehensive error checking for all operations
- Robust handling of edge cases and boundary conditions
- Memory leak prevention through careful resource management

### Performance Considerations
- Efficient list traversal algorithms
- Optimized memory usage patterns
- Minimal redundant operations

## Development Insights

### Lessons Learned
1. **Debugging Tools**: Valgrind proved invaluable for memory management
2. **Data Structure Choice**: Doubly linked lists provided necessary flexibility
3. **Incremental Development**: Week-by-week approach managed complexity effectively
4. **Error Prevention**: Week 2 debugging experience prevented similar issues in Week 3

### Project Complexity
- **Assessment**: Non-trivial assignment requiring significant algorithmic thinking
- **Challenge Areas**: Memory management, complex data structure manipulation
- **Success Factors**: Systematic approach, thorough debugging, comprehensive testing

## Final Architecture

### Core Components
1. **Text Storage**: Doubly linked list of lines
2. **Command Processing**: Stack-based undo/redo system
3. **File Operations**: Robust save/load functionality
4. **Navigation System**: Efficient cursor movement
5. **Text Manipulation**: Complete set of editing operations

### Supported Operations
- File I/O (save, load, quit)
- Text insertion and deletion
- Line-based operations
- Character-based navigation
- Search and replace functionality
- Complete undo/redo system

## Conclusion
This text editor implementation demonstrates advanced data structure usage, comprehensive error handling, and sophisticated undo/redo functionality. The 3-week development cycle provided valuable experience in debugging complex pointer-based data structures and implementing robust text manipulation algorithms.
