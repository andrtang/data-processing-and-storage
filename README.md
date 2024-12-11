# InMemoryDB

## Overview
`InMemoryDB` is a Python implementation of an in-memory key-value database with support for transactions. It allows for "all-or-nothing" updates to maintain consistency, inspired by scenarios such as managing financial transfers where partial updates can lead to invalid states.

## Features
- **Key-Value Storage**: Supports string keys and integer values.
- **Transactions**: Begin, commit, and rollback transactions.
- **Isolation**: Changes made within a transaction are not visible until committed.
- **Error Handling**: Ensures operations like `put` are only valid within active transactions.

## Prerequisites
- Python 3.7 or later.

## Installation
1. Clone and open this repository:
   ```bash
   git clone https://github.com/andrtang/data-processing-and-storage.git
   cd data-processing-and-storage
   ```
2. Ensure Python is installed:
   ```bash
   python --version
   ```

## How to Run (and a note about input)
- Create a file with a main function (or write a main function inside the InMemoryDB.py file)
- If you are creating a main function in a separate file, be sure to include `import InMemoryDB` at the top of your file.
- The functions in the class do not print anything. If you are expecting an output for .get(), be sure to print it in a print statement.

### Example Interaction
Below is an example of a main function to demonstrate how the `InMemoryDB` behaves, which is taken from Fig 2 in the assignment:

```python
if __name__ == "__main__":

    inmemoryDB = InMemoryDB()

    print(inmemoryDB.get("A")) # Should print None

    # inmemoryDB.put("A", 5)  # Should throw an error because a transaction is not in progress

    inmemoryDB.begin_transaction()

    inmemoryDB.put("A", 5)

    print(inmemoryDB.get("A"))  # Should print None

    inmemoryDB.put("A", 6)

    inmemoryDB.commit()

    print(inmemoryDB.get("A"))  # Should print 6

    # inmemoryDB.commit()  # Should throw an error

    # inmemoryDB.rollback()  # Should throw an error

    print(inmemoryDB.get("B"))  # Should print None

    inmemoryDB.begin_transaction()

    inmemoryDB.put("B", 10)

    inmemoryDB.rollback()

    print(inmemoryDB.get("B"))  # Should print None

```

## Assignment Modification Suggestions
1. **Clarifications to Instructions**:
   - Include specific requirements for error messages when invalid operations (e.g., `put` without a transaction) are performed.
   - Clarify what inputs are possible.
   - Fig 2 does not include print statements, but the instructions say that methods should return elements, not print them, which makes it a little confusing.

2. **Additional Methods**:
   - Support for deleting keys.
   - Methods to retrieve all keys or list changes made within a transaction.

3. **Improved Grading**:
   - Include a suite of automated tests for common edge cases (e.g., rollback after multiple changes).
   - Implement an autograder like how OS or PLC implement autograders.
   - Explain how automated graders would work (specify file structure, language, etc.)
