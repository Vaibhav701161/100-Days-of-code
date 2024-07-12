# Blockchain Daily notes

- DAY-1 : Basics of solidity revision
    1. First , we are writing a smart contract that maintains a count
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract counter {
     uint count;
    
     constructor()public { // it is a special function for each smart contract that runs ones and only once!
      count = 0;
     }
    
     function getCount() public view returns(uint) {
       return count;
     }
    
     function incrementCount( ) public {
        count = count +1 ;
     }
    }
    ```
    
    1. next let’s see the variables in solidity:
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract MyContract{
        // solidity is statically typed language
        // variables
        string public myString =  "my string";  // -- type of variable, that define it's visiblity than the name of the variable..
        bool public boolean1 = true;
        uint public case1 = 1;
        int public case2 = 1;
        address public myAddress = 0x5B38Da6a701c568545dCfcB03FcB875f56beddC4;
    
    }
    ```
    
    1. next we have functions in solidity: 
    
    IT basically have two types: write functions and view functions
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract MyContract{
        string name = "example1";
    
        function setName (string memory _name) public { // this is a write function
            name = _name;
        }
    
    // This function, setName, takes a single argument _name of type 
    // string. The memory keyword indicates that this string is a temporary 
    // variable, stored in memory rather than on the blockchain. 
    // The public keyword means this function can be called from 
    // outside the contract, like a public method in a JavaScript class.
      
      
        function getName () public view returns (string memory) { // this is a view function
              return name;
        }
    
        function resetName () public {
            name = "example1";
        }
        
        }
     
    
    ```
    
    1. next we have the visibility types
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract contract1 {
    
        string name1 = "name 1"; // string with no visiblity
    
        string private name2 = "name 2";
        // it can only be accessed inside and can be inhereted
        string internal name3 = "name 3";
        // it can only be accessed inside and can not be inherited
        string public name4 = "name 4";
        // it can be accessed both inside and outside and can be inherited
         
    }
    ```
    
    1. Modifiers : a. View : it means that the blockchain can not modify the state of the blockchain but can read the state of blockchain.
    
    b. Pure : it means that can not modify the state  as well as cannot read the state of the blockchain.
    
    c. Payable : they are allowed to receive the payment.
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract contract1 {
    
      string public name = "example 5";
      uint public balance ;
    
      function getName() public view returns (string memory){
        return name;
      }
    
      function add (uint a, uint b) public pure returns (uint){
        return a+b;
      }
    
     function pay() public payable {
        balance = msg.value;
     }
    }
    ```
    
    1. Custom modifiers :
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract contract1 {
    
      address private owner;
      string public name = "";
    
      modifier onlyOwner {
        require(msg.sender == owner, 'caller must be owner');
        _;
      }
    
      function setName(string memory _name) onlyOwner public {
        name = _name;
      }
    }
    
    ```
    
    Code explanation :
    
    - `address private owner;`: This declares a state variable `owner` of type `address` and makes it private, meaning it can only be accessed within the contract.
    - `string public name = "";`: This declares a state variable `name` of type `string`, initializes it to an empty string, and makes it public, meaning there is an automatically generated getter function for it.
    
    Modifiers in Solidity are used to change the behavior of functions. The `onlyOwner` modifier checks if the caller (the person who sent the transaction) is the owner of the contract. If not, it reverts the transaction with an error message.
    
    - `require(msg.sender == owner, 'caller must be owner');`: This is similar to an `if` statement in JavaScript that throws an error if the condition is not met.
    - `_;`: This is a placeholder for the function body. When a function uses this modifier, its code is inserted at this point.
    - `function setName(string memory _name) onlyOwner public {`: Declares the function `setName` which takes a single argument `_name` of type `string`. The `onlyOwner` modifier ensures only the owner can call this function. `public` means it can be called externally.
    - `name = _name;`: This sets the state variable `name` to the value of `_name`.
    1. Constructor function: a constructor is an optional function that is only executed once when the contract is deployed. It is typically used to initialize the contract's state, such as setting initial values for state variables or performing any setup tasks required when the contract is deployed.
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract contract1 {
    
      address private owner;
      string public name = "";
    
      modifier onlyOwner {
        require(msg.sender == owner, 'caller must be owner');
        _;
      }
    
      // Constructor
      constructor(string memory _name) {
        owner = msg.sender; // Sets the deployer of the contract as the owner
        name = _name; // Initializes the name variable
      }
    
      function setName(string memory _name) onlyOwner public {
        name = _name;
      }
    }
    
    ```
    
    1. Global variables:
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract contract1 {
    address public contractAddress;
    address public payer;
    address public origin;
    uint public amount;
    
    constructor () {
    contractAddress = address(this); // this corresponds to the address of the current smart contract
    
    }
    function pay() public payable {
    payer = msg.sender;//  Used to set the contract owner and to check the sender of the function calls.
    origin = tx.origin;// to get the origin of the transaction
    amount = msg.value;// Used to check the amount of Ether sent with the deposit function.
    }
    
    function getBlockInfo() public view returns(uint,uint,uint){
    return(
    block.number;
    block.timestamp;
    block.chainid
    );
    }
    }
    ```
    
    1. **Operators:** 
    
    ```solidity
    // SPDX-License-Identifier: MIT
    pragma solidity ^0.8.0;
    
    contract OperatorsExample {
        // State variables for demonstration
        uint256 public result;
        bool public isTrue;
        uint8 public bitwiseResult;
        
        // Function demonstrating arithmetic operators
        function arithmeticOperators(uint256 a, uint256 b) public {
            result = a + b; // Addition
            result = a - b; // Subtraction
            result = a * b; // Multiplication
            result = a / b; // Division
            result = a % b; // Modulus
        }
        
        // Function demonstrating comparison operators
        function comparisonOperators(uint256 a, uint256 b) public {
            isTrue = (a == b); // Equal to
            isTrue = (a != b); // Not equal to
            isTrue = (a > b);  // Greater than
            isTrue = (a < b);  // Less than
            isTrue = (a >= b); // Greater than or equal to
            isTrue = (a <= b); // Less than or equal to
        }
        
        // Function demonstrating logical operators
        function logicalOperators(bool a, bool b) public {
            isTrue = a && b; // Logical AND
            isTrue = a || b; // Logical OR
            isTrue = !a;     // Logical NOT
        }
        
        // Function demonstrating bitwise operators
        function bitwiseOperators(uint8 a, uint8 b) public {
            bitwiseResult = a & b; // Bitwise AND
            bitwiseResult = a | b; // Bitwise OR
            bitwiseResult = a ^ b; // Bitwise XOR
            bitwiseResult = ~a;    // Bitwise NOT
            bitwiseResult = a << 1; // Left shift
            bitwiseResult = a >> 1; // Right shift
        }
        
        // Function demonstrating assignment operators
        function assignmentOperators(uint256 a, uint256 b) public {
            result = a;   // Assign
            result += b;  // Add and assign
            result -= b;  // Subtract and assign
            result *= b;  // Multiply and assign
            result /= b;  // Divide and assign
            result %= b;  // Modulus and assign
        }
    }
    
    ```
    
- DAY-2: Basics of solidity revision
    1. Conditionals:
    - Operators are most commonly used inside conditionals in if-else statements.
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    
    contract MyContract{
      function evenOrOdd(uint x) public pure returns (string memory){
         if (x%2 == 0){
            return "even";
         }else{
            return "odd";
         }
      }
    }
    ```
    
    1. Arrays:  sorted lists of information which can be declared by giving it a datatype and declare it inline.
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    contract myContract {
       uint [] public array1 = [1,2,3];
       string [] public array2;
    
    // we can do a bunch of things like read an array and manipulate them from inside a function
    uint[] public array;
    
    function get(uint i) public view returns (uint){
         return array[i];// this gives the value out of a given index
         
      }
      function length() public view returns (uint){
          return array.length;
       
       }
       
       function push(uint i) public {
        array.push(i);
       }
       
       function pop() public {
       array.pop();
       } 
       
       function remove(uint index) public {
         delete array[index];
       }
    }
    ```
    
    1. Mapping: Most common way to store information in smart contracts is with mapping. 
    - These are key value pairs that works like associative arrays or hash tables where you have a key with a value pair!
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    
    contract studentGrades{
    // define a mapping where the key is the student id (uint) and the valueis their grade also uint
    mapping (uint=> uint) public grades;
    
     // function to set a student's grade
         function setGrade(uint studentId, uint grade) public {
          grades[studentId] = grade;
         }
         //mfunction to get student's grade
             function getGrade(uint 
    }
    ```
    
    1. Structs:  Solidity lets us create our own types with something called as structs.
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    
    contract MyContract{
      sttruct books {
       string title;
       string autor;
       bool completed;
      }
      
      // Array of books
      books[] public books;
      
      function add(string memory _title, string memory _author) public {
        books.push(books(_title, _author,false));
      }
      
      function get (uint _index)
      public
      view
      returns(string memory title, string memory author, bool completed)
      {
      books storage books =  books [_index];
      return (book.title, book.author, book.completed); 
      }
      // update completed
      function complete(uint _index) public {
         books storage books = books[_index];
         books.completed = true;
      }
    }
    ```
    
    1. Events:  Solidity lets us subscribe to events  from an external consumer to find if anytime a function or anything inside of a function is called.  we trigger events with the emit keyword.
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    contract contract2{
    string public message = "hello world";
    event messageUpdated(
      address indexed _user,
      string _message
    );
    
    function updateMessage(string memory _message) public {
       message = _message;
       emit messageUpdated(msg.sender,_message);
    }
    }
    ```
    
    1. ETHERS :  WE can receive ethers directly in the smart contract by using the receive function.   
    
                                  
    
    ```solidity
    recieve() external payable{}
    ```
    
    `fallback` function is like a catch-all mechanism for a smart contract. It’s used when the contract receives Ether or when someone tries to call a function that doesn't exist in the contract.
    
    ```solidity
    fallback() external payable {}
    ```
    
    We can check the balance of any wallet inside a smart contract 
    
    ```solidity
    function checkBalance() public view returnsc(uint){
      function checkBalance () public view returns (uint){
       return address(this).balance;
      }
    }
    ```
    
    We can send ether to a different address using call 
    
    ```solidity
    function transfer (addrss payable _to) public payable {
      (bool sent, ) = _to.call{value: msg.value}("");
         require(sent, "failed!");
    }
    ```
    
    1. Inheritance:  we can create smart contracts which inherit  behaviors from other smart contracts
    
    ```solidity
    //SPDX-License-Identifier: Unlicense
    pragma solidity ^0.8.0;
    
    contract ownable{
    address owner;
    
    constructor(){
      owner = msg.sender;
    }
    modifier oonlyOwner{
    require(msg.sender == owner, 'caller must be owner');
      _;
    }
    }
    
    contract Mycontract is ownable {
      string public name = "example 1";
        function setName(string memory _name) public onlyOwner {
        
        name = _name;
        }
    }
    ```