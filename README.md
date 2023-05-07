Download Link: https://assignmentchef.com/product/solved-oop345-workshop-2-move-and-copy-semantics
<br>
In this workshop, you work with a large dynamically allocated array of C++ Standard Library strings and compare the performance of copy and move operations on that collection.

## *In-Lab*

This workshop consists of three modules:– `w2` (supplied)– `TimedEvents`– `Text`

Enclose all your source code within the `sdds` namespace and include the necessary guards in each header file.

### `w2` Module (supplied)

**Do not modify this module!**  Look at the code and make sure you understand it.

### `TimedEvents` Module

Design and code a class named `TimedEvents` that manages a **statically** allocated array of record objects.  Your class predefines the maximum number of record objects at 7. The **instance variables** for your class should include:– the number of records currently stored– the start time for the current event (an object of type `std::chrono::steady_clock::time_point`; see documentation [here](https://en.cppreference.com/w/cpp/chrono/time_point))– the end time for the current event (an object of type `std::chrono::steady_clock::time_point`)– an array of records of anonymous structure type (the structure has no name). The structure should contain the following fields:– a string with the event name.– a string with the predefined units of time– the duration of the recorded event (an object of type `std::chrono::steady_clock::duration`; see documentation [here](https://en.cppreference.com/w/cpp/chrono/duration))

Your class includes the following member functions:– a default constructor– `startClock()`: a modifier that starts the timer for an event– `stopClock()`: a modifier that stops the timer for an event– `recordEvent()`: a modifier that receives the address of a C-style null terminated string that holds the name of the event.  This function will update the next time-record in the array:– stores the parameter into the name attribute– stores `”nanoseconds”` as the units of time– calculates and stores the duration of the event (use `std::chrono::duration_cast&lt;std::chrono::nanoseconds&gt;()`, see documentation [here](https://en.cppreference.com/w/cpp/chrono/duration/duration_cast))– a **friend insertion operator** that receives a reference to an `std::ostream` object and a `TimedEvents` object. This operator should insert in the first parameter the records from the array in the following format:

“`Execution Times:————————–EVENT_NAME DURATION UNITSEVENT_NAME DURATION UNITS…————————–“`

The **name** of the event should be a field of size 20, alligned on the left; the **duration** should be a field of size 12, alligned on the right.

Starting and stopping the timer means getting the current time (use `std::chrono::steady_clock::now()`; see documentation [here](https://en.cppreference.com/w/cpp/chrono/steady_clock/now)).

### `Text` Module

Design and code a class named `Text` that manages a **dynamically** allocated array of `std::string`s. Your class keeps track of the number of strings currently stored and defines the following member functions:– a no-argument default constructor– a 1-argument constructor that receives the address of a C-style null terminated string containing the name of a file from which this member function populates the current object. This function1. reads the file to count the number of records present (the record delimiter should be a single space `’ ‘`)2. allocates memory for that number records in the array3. re-reads the file and loads the records into the array.– a copy constructor– a copy assignment operator– a destructor– `size_t size() const`: a query that returns the number of records stored in the current object.

To review the syntax for reading from a text file using an `std::ifstream` object see the chapter in your notes entitled [Custom File Operators](https://scs.senecac.on.ca/~BTP200/pages/content/files.html).

### Sample Output

When the program is started with the command:“`w2.exe gutenberg_shakespeare“`the output should look like:“`Command Line:————————–1: w2.exe2: gutenberg_shakespeare————————–

0-arg Constructor – a.size =       0 records1-arg Constructor – b.size = 1293934 recordsCopy Constructor  – c.size = 1293934 recordsCopy Assignment   – a.size = 1293934 records

————————–Execution Times:————————–0-arg Constructor           790 nanoseconds1-arg Constructor    4377977955 nanosecondsCopy Constructor     1976590065 nanosecondsCopy Assignment      2004531426 nanosecondsDestructor           3478640044 nanoseconds————————–“`

**Note:** The execution times will be different every time you run the program! Everything else should match.

## *At-Home*

For this part of the workshop, upgrade the `Text` class to include a **move constructor** and a **move assignment operator**.  No other modules need to be changed.

### Sample Output

When the program is started with the command:“`w2.exe gutenberg_shakespeare“`the output should look like:“`Command Line:————————–1: w2.exe2: gutenberg_shakespeare————————–

0-arg Constructor – a.size =       0 records1-arg Constructor – b.size = 1293934 recordsCopy Constructor  – c.size = 1293934 recordsCopy Assignment   – a.size = 1293934 recordsMove Constructor  – d.size = 1293934 recordsMove Assignment   – a.size = 1293934 records

————————–Execution Times:————————–0-arg Constructor           790 nanoseconds1-arg Constructor    4010433846 nanosecondsCopy Constructor     2002725409 nanosecondsCopy Assignment      1926967415 nanosecondsMove Constructor            790 nanosecondsMove Assignment             394 nanosecondsDestructor           3538222832 nanoseconds