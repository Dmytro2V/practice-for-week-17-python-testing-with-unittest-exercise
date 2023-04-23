Unit Testing in Python
exercise doing mostly on video: 
https://my.appacademy.io/lessons/testing-basics/f8d2245d/practices/writing-unit-tests-with-unittest/840de3c6

In this reading, you will learn:

How unit tests are written using the unittest library
How to run tests with unittest
How to interpret test results
Writing unit tests
The unittest library is the built-in testing framework in Python. Similar to how you would set up your unit tests in Node, you also need to set up a test or specs folder. Or alternatively, have a spec file accompany every file you have.

For example, if you decide to have a testing folder:

your-project
├── Pipfile
├── Pipfile.lock
├── app
│   ├── __init__.py
│   └── app code...
└── test
    ├── __init__.py
    └── tests...
Or if you have specs accompanying each file:

your-project
├── Pipfile
├── Pipfile.lock
├── app
│   ├── __init__.py
│   └── app code...
└── test
    ├── __init__.py
    ├── module1
    │   ├── __init__.py
    │   └── test_with_same_name.py
    └── module2
        ├── __init__.py
        └── test_with_same_name.py
Using unittest
Python's built-in unittest package is class-based. You must define classes, the methods of which are your unit tests. Your class must inherit from unittest.TestCase. Here's what that looks like. (There are more things you can do in your test cases. Please see TestCase documentation if you want to learn more.)

import unittest


class TestSomeStuff(unittest.TestCase):
    """
    This is a test case, something run by both unittest
    and pytest.
    """

    def setUp(self):
        """The setUp method runs before each test."""
        pass

    def tearDown(self):
        """The tearDown method runs after each test."""
        pass

    def test_some_thing(self):
        """
        All methods that begin with "test_" are run as
        unit tests. Do your assertions in here so that
        the test runner will capture them.
        """
        pass
This is the only way that unittest works.

Writing assertions
Each of your test classes in unittest get a variety of assertions built in as instance methods to your class, inherited from unittest.TestCase. Here's an example of a test making an assertion.

class TestDoubleFunction(unittest.TestCase):
    def test_returns_twice_passed_in(self):
        result = double(3)
        self.assertEqual(result, 6)
This table shows the assertions available to you by using unittest.TestCase as the base class for you unit tests.

METHOD	CHECK THAT
assertEqual(a, b)	a == b
assertNotEqual(a, b)	a != b
assertTrue(x)	bool(x) is True
assertFalse(x)	bool(x) is False
assertIs(a, b)	a is b
assertIsNot(a, b)	a is not b
assertIsNone(x)	x is None
assertIsNotNone(x)	x is not None
assertIn(a, b)	a in b
assertNotIn(a, b)	a not in b
assertIsInstance(a, b)	isinstance(a, b)
assertNotIsInstance(a, b)	not isinstance(a, b)
The assertEqual method does some smart stuff when used with lists or dictionaries (or tuples or sets). Instead of determining if the collection points to the same memory location, it checks entries to make sure they exist in both objects. So, for example, the following assertEqual does not raise an error because both lists contain 1, 2, and 3.

class TestDoubleFunction(unittest.TestCase):
    def test_returns_twice_passed_in(self):
        lst1 = [1, 2, 3]
        lst2 = [1, 1 + 1, 1 + 1 + 1]
        self.assertEqual(lst1, lst2)
It compares them, pairwise, index by index.

The same kind of comparison is true for dictionaries, but it will check that both dictionaries have the same keys and values.

Running tests
Once you've set up your test folder and written some tests, you can run your tests using the following command:

> python -m unittest
This will run all the tests within your test library. Alternatively, you can run specific test scripts by appending the path to the test file you want to run like so:

> python -m unittest <path-to-file>
Running the unittest command with the -v flag will provide more helpful outputs that list each test and their results. The output will be separated into three categories. Those beginning with "." indicate a passing test. Those with "E" indicate an error running the test. Those with "F" indicate a failed test.

Interpreting test results
Passing tests
A passing test will be indicated with a "." and/or an "OK". This means that your code passed all assertions in the corresponding tests and did not encounter any errors in the process.

Failing tests
The failing test will be indicated with an "F" and a "FAIL" block that includes the test method name, the location of the test, and a stack trace indicating where the failure occurred while running the test.

A failing test indicates that your code failed an assertion in the corresponding test.

Errored tests
An errored test will be indicated with an "E" and an "ERROR" block that includes the test method name, the location of the test, and a stack trace indicating where the exception arose while running the test.

This means that an exception was encountered in the process of running your code through the corresponding test. This is considered another type of test failure, but it happens because of an error rather than a failed assertion.

What you learned
In this reading, you learned how unit tests are written using the unittest library, how to run the tests, and how to interpret them.