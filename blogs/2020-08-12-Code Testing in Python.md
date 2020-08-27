How can you perform testing in Python?

## unittest
Python packages a unit testing framework called <Unittest>. It supports the following features:
- Automation testing.
- Sharing of setup and shutdown code for tests.
- Aggregation of tests into collections.
- Independence of the tests from the reporting framework.

Below are some coding examples for unittest:

```Python
import unittest
def func(x):
    return x+1

class MyTest(unittest.TestCase):
    def test(self):
        self.assertEqual(fun(3), 4)
```

```Python
# unittest in production
import pandas as pd
import unittest
import validator as v

class ValidatorValidator(unittest.TestCase):
    """ Tests the validation functions in the validator"""

    @classmethod # optional
    def setUpClass(cls):
        cls.test_df = pd.read_csv('test_data.csv')

    def test_nulls(self):
        with self.subTest():
            self.assertEqual(v.check_for_nulls(self.test_df['a'])[0], 1)
        with self.subTest():
            self.assertEqual(v.check_for_nulls(self.test_df['b'])[0], 0)
        with self.subTest():
            self.assertEqual(v.check_for_nulls(self.test_df['c'])[0], 0.4)

if __name__ == '__main__':
    unittest.main()
```

## Test case in coding interview

Procedure for coding interview:
- talk out loud about your thoughts
- write down the code and explain along the way
- go over your code line by line as this is the first time you see it to check for grammar or syntax errors
- come up with test cases to make sure the code runs as expected

The goal is to see
- if the programmer knows how to program
- if the programmer knows how to test his program
- (advanced) if the programmer knows how make an automatic test

Possible questions from an interviewer regarding a test case:
- Can you come up some test cases and test your code?
- How do you know your code works?
- How to test your program?

You would test your program first with simple test cases to ensure that it actually works and then with various stress, volume, range, etc tests to improve coverage (in production, not interview), as many combinations as you can think of which might traverse different control paths in the code. 

Sample test in an interview usually include the following categories:
- Edge cases
- Cases where there's no solution (i.e., none, -1, empty results)
- Non-trivial functional tests (normal cases)

You can ask some clarification questions during a coding interview to help you better answer the coding question:
- How big is the size of the input?
- How big is the range of values?
- What kind of values are there? Are there negative numbers? Floating points? Will there be empty inputs?
- Are there duplicates within the input?
- What are some extreme cases of the input?
- How is the input stored? If you are given a dictionary of words, is it a list of strings or a trie?

Below are some code examples to use during a coding interview:

```Python
# code test in interview
case1 = xxx
case2 = xxx
case3 = xxx
print(func(case1))
print(func(case2))
print(func(case3))
```

```Python
# code test in interview
assert func(case1) == a
assert func(case2) == b
assert func(case3) == c
```

```Python
# code test in interview
def main():
    assert func(case1) == a
    assert func(case2) == b
    assert func(case3) == c
    assert func(case4) == d

if __name__ == "__main__":
    main()
```

References:
1. https://docs.python-guide.org/writing/tests/