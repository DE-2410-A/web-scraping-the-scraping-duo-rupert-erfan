# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Python for Extracting

### Customer Requirements Breakdown

In case you aren't sure, the 2 main requirements from the customer's requirements are:

> As a BOOK STORE OWNER,  
> I want to understand how may books are available in each category from [http://books.toscrape.com/](http://books.toscrape.com/),  
> So that I can make decisions about which categories to focus on when launching a rival business

***AND***

> As a BOOK STORE OWNER,
> I want to understand the average price point of books in each category from [http://books.toscrape.com/](http://books.toscrape.com/),  
> So that I can make decisions about the price point of different books for each category

### Making a Request

From this, it is clear to see that we need to make at least 1 request to a website to get the data we need.  As it is probable that we will need to make multiple requests, it is a good idea to create a function that can handle this for us.

In this activity, you will learn how to test-drive the creation of a function to make a request to a website and handle the various responses it returns.

[TDD?](../info/test-driven-development.md)

---

## HTTP Request Task

Hopefully, you have broken this down into something similar to:

### Functional Requirements

1. [ ] The function should accept a URL as an input parameter.
2. [ ] The function should send an HTTP GET request to the provided URL using the `requests` library.
3. The function should handle the response:
   - [ ] If the response status code is `200`, the function should return the HTML content of the page.
   - [ ] If the response status code is not `200`, the function should return an error message indicating the status code and that the request was unsuccessful.
4. [ ] The function should catch any exceptions that occur during the request and return an appropriate error message.

### Testing Requirements

1. **Successful Request:**
   - [ ] The function should receive a URL and make a GET request to that URL.
   - [ ] The function should return the HTML content if the response status code is `200`.

2. **Unsuccessful Request:**
   - [ ] The function should return an error message if the response status code is not `200`.
   - [ ] The error message should include the status code and indicate that the request was unsuccessful.

3. **Exception Handling:**
   - [ ] The function should catch any exceptions that occur during the request.
   - [ ] The function should return an error message indicating that an exception occurred.

### Definition of Done

- [ ] The function is implemented according to the functional requirements.
- [ ] Unit tests are written to cover all testing requirements.
- [ ] The function and tests are reviewed and approved by at least one peer.
- [ ] The function is documented with clear and concise comments.
- [ ] The code adheres to PEP 8 guidelines and Python best practices.

---

## Activity 2 - Use TDD to Develop the Request Function

**Uncle Bob's Three Laws of TDD:**

1. You are not allowed to write any production code unless it is to make a failing unit test pass.
2. You are not allowed to write any more of a unit test than is sufficient to fail, and not compiling is failing.
3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

---

### Activity 2.1 - Write a Test for the Request Function

1. Locate the cell with the comment `# Test request_to_scrape` in the Jupyter notebook
2. Write a test to make sure that the production function actually makes a GET request to the URL supplied, the test should:
   - **Arrange**
     - Set a variable URL to use for the request (this can be a dummy URL)
     - Set `mock_get` to have a `return_value` with `status_code` set to `200` - you will need to call `patch` on the `requests.get` function, importing this from the `unittest.mock` module
   - **Act**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Call the production function with the URL set up in the `Arrange` step
   - **Assert**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Check that the `mock_get` function was called with the URL set up in the `Arrange` step
     - Hint: use the `assert_called_once_with` method on the `mock_get` object
3. Run the test to make sure it fails

> If you have done this properly, then you should get an output similar to this:
>
```bash

F                                                                                            [100%]
============================================= FAILURES =============================================
___________________________ test_request_to_scrape_makes_correct_request ___________________________

    def test_request_to_scrape_makes_correct_request():
        # Arrange
        url = "https://www.example.com"
    
        with patch('requests.get') as mock_get:
            mock_get.return_value.status_code = 200
    
            # Act
>           request_to_scrape(url)
E           NameError: name 'request_to_scrape' is not defined

/var/folders/jf/3t017l9948jgt5frxgh1sqjm0000gn/T/ipykernel_49108/2446753150.py:13: NameError
===================================== short test summary info ======================================
FAILED t_d6b87f72ff1d45608ccaf98f5060f27c.py::test_request_to_scrape_makes_correct_request - NameError: name 'request_to_scrape' is not defined
1 failed in 0.47s
<ExitCode.TESTS_FAILED: 1>

```

> This is GOOD!!!  We now have fulfilled the first law of TDD - we have a failing test!
> Now we can move on to the next step.

---

### Activity 2.2 - Write the Production Code

> Remember, we are not allowed to write any more code than is necessary to make this test pass.

**Why is the test failing?**

The test is failing because we don not have the function `request_to_scrape` defined yet.

To pass clear this error:

1. Locate the cell with the comment `# request_to_scrape Production Code` in the Jupyter notebook
2. Write a function called `request_to_scrape` that accepts a URL as an input parameter (for the time being, make it return `None`)
3. Run the test again...

> And we get a different error:

```bash
F                                                                                            [100%]
============================================= FAILURES =============================================
___________________________ test_request_to_scrape_makes_correct_request ___________________________

    def test_request_to_scrape_makes_correct_request():
        # Arrange
        url = "https://www.example.com"
    
        with patch('requests.get') as mock_get:
            mock_get.return_value.status_code = 200
    
            # Act
            request_to_scrape(url)
    
            # Assert
>           mock_get.assert_called_with(url)

/var/folders/jf/3t017l9948jgt5frxgh1sqjm0000gn/T/ipykernel_49108/2446753150.py:16: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

self = <MagicMock name='get' id='4427404288'>, args = ('https://www.example.com',), kwargs = {}
expected = "get('https://www.example.com')", actual = 'not called.'
error_message = "expected call not found.\nExpected: get('https://www.example.com')\n  Actual: not called."

    def assert_called_with(self, /, *args, **kwargs):
        """assert that the last call was made with the specified arguments.
    
        Raises an AssertionError if the args and keyword args passed in are
        different to the last call to the mock."""
        if self.call_args is None:
            expected = self._format_mock_call_signature(args, kwargs)
            actual = 'not called.'
            error_message = ('expected call not found.\nExpected: %s\n  Actual: %s'
                    % (expected, actual))
>           raise AssertionError(error_message)
E           AssertionError: expected call not found.
E           Expected: get('https://www.example.com')
E             Actual: not called.

/opt/homebrew/Cellar/python@3.13/3.13.0_1/Frameworks/Python.framework/Versions/3.13/lib/python3.13/unittest/mock.py:968: AssertionError
===================================== short test summary info ======================================
FAILED t_d6b87f72ff1d45608ccaf98f5060f27c.py::test_request_to_scrape_makes_correct_request - AssertionError: expected call not found.
1 failed in 0.04s
<ExitCode.TESTS_FAILED: 1>
```

> We are still in the realms of Rule 1 of TDD - we are still failing the test, but we are failing in a different way.  
> This is STILL GOOD!  
> We can write more production code to make this test pass.
>
> **If you didn't get this error, make sure you have run the code in the `request_to_scrape Production Code` cell.**

---

**Why is the test failing?**

The test is failing because we are not calling the `requests.get` function with the URL parameter.

1. Add a call to the `requests.get` function in the `request_to_scrape` function with the URL parameter using the `url` parameter passed to the function
2. Run the test again...

> This time...

```bash
F                                                                                            [100%]
============================================= FAILURES =============================================
___________________________ test_request_to_scrape_makes_correct_request ___________________________

    def test_request_to_scrape_makes_correct_request():
        # Arrange
        url = "https://www.example.com"
    
        with patch('requests.get') as mock_get:
            mock_get.return_value.status_code = 200
    
            # Act
>           request_to_scrape(url)

/var/folders/jf/3t017l9948jgt5frxgh1sqjm0000gn/T/ipykernel_49108/2446753150.py:13: 
_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 

url = 'https://www.example.com'

    def request_to_scrape(url):
>       response = requests.get(url)
E       NameError: name 'requests' is not defined

/var/folders/jf/3t017l9948jgt5frxgh1sqjm0000gn/T/ipykernel_49108/1708649239.py:3: NameError
===================================== short test summary info ======================================
FAILED t_d6b87f72ff1d45608ccaf98f5060f27c.py::test_request_to_scrape_makes_correct_request - NameError: name 'requests' is not defined
1 failed in 0.01s
<ExitCode.TESTS_FAILED: 1>
```

> You might have forgotten to import the `requests` module!  Well done if you didn't!

- You know the drill here... import the `requests` module, re-run the cell and run the test again...

> ...and finally...

```bash
.                                                                                            [100%]
1 passed in 0.01s
<ExitCode.OK: 0>
```

> So we're done, right...?
> Well, we have passed the test, but we have not fulfilled the requirements of the task.
> We need to make sure that the function returns the HTML content of the page if the response status code is `200`.
> So we can move to Rule 2 of TDD - we can write a test to make sure that this requirement is met.

---

### Activity 2.3 - Write a Test for the Successful Request

> Leave the existing test in place here, add to the end of the `# Test request_to_scrape` cell.

1. Write a ***NEW*** test to make sure that the production function returns the HTML content of the page if the response status code is `200`, the test should:
   - **Arrange**
     - Set a variable URL to use for the request (this can be a dummy URL)
     - Set `mock_get` to have a `return_value` with `status_code` set to `200` and a `text` attribute set to some dummy HTML content (e.g. `<html><body><h1>Hello, World!</h1></body></html>`)
   - **Act**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Call the production function with the URL set up in the `Arrange` step
   - **Assert**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Check that the production function returns the dummy HTML content set up in the `Arrange` step

> We should expect an error, right?
> On to Rule 3 of TDD...

---

### Activity 2.4 - Write the Production Code to ensure a 200 status code returns the HTML content

1. Add a conditional statement to the `request_to_scrape` function that checks if the response status code is `200` and returns the HTML content of the page if it is
2. Run the test again...

> And we should get...

```bash
..                                                                                           [100%]
2 passed in 0.01s
<ExitCode.OK: 0>
```

> We have passed the test, but we have not fulfilled the requirements of the task.  
> What about a non-200 status code?

---

### Activity 2.5 - Write a Test for a non-200 status code

> Leave the existing tests in place here, add to the end of the `# Test request_to_scrape` cell.

1. Write a ***NEW*** test to make sure that the production function returns an error message if the response status code is not `200`, the test should:
   - **Arrange**
     - Set a variable URL to use for the request (this can be a dummy URL)
     - Set `mock_get` to have a `return_value` with `status_code` set to `404`
   - **Act**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Call the production function with the URL set up in the `Arrange` step
   - **Assert**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Check that the production function returns an error message indicating that the request was unsuccessful

---

### Activity 2.6 - Write the Production Code to ensure a non-200 status code returns an error message

1. Add a conditional statement to the `request_to_scrape` function that checks if the response status code is not `200` and returns an error message indicating that the request was unsuccessful

---

### Activity 2.7 - Write a Test for Exception Handling

> Leave the existing tests in place here, add to the end of the `# Test request_to_scrape` cell.

1. Write a ***NEW*** test to make sure that the production function catches any exceptions that occur during the request and returns an appropriate error message, the test should:
   - **Arrange**
     - Set a variable URL to use for the request (this can be a dummy URL)
     - Set `mock_get` to raise an exception when called
   - **Act**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Call the production function with the URL set up in the `Arrange` step
   - **Assert**
     - *Its important that this code is indented within the `with patch('requests.get') as mock_get:` block*
     - Check that the production function returns an error message indicating that an exception occurred

---

### Activity 2.8 - Write the Production Code to ensure that exceptions are caught and an appropriate error message is returned

1. Add a `try`/`except` block to the `request_to_scrape` function that catches any exceptions that occur during the request and returns an appropriate error message
2. Run the test again...

---

## Documenting the Code

This is often seen as the most pointless and laborious part of the process, but it is important to document your code!

However, this is seen as one of the top uses cases for AI in the development process.

Paste your function into your favourite AI tool and ask it to generate a docstring for you.

---

## Code Review

At this point, you are probably not feeling experienced enough to do a code review - and it's difficult to review code you have had a hand in writing.

For the purposes of this exercise, you will use AI to help review your code.

Here are some prompts that you can give to the AI to help review your code (remember to copy your production function and tests to the AI):

1. Does the code adhere to PEP 8 guidelines?
2. Are there any test cases that have not been considered?
3. Are there any opportunities to make the code more efficient?
4. Are there any opportunities to make the code more readable?
5. Are there any improvements that could be made to the return of the function?
6. Can the code be made more robust?

**Remember to:**

- Refactor in small steps making sure tests still pass at each stage.
- Update your tests to reflect any changes you make.
- Update your documentation to reflect any changes you make.

### Improve the Code

AI may suggest that you:

- Add functionality that checks to see if the URL returns HTML content and handles this appropriately
- Change the return from a string to a dictionary with the status code and a more explicit message
- Handle exceptions more explicitly

Make these changes to your code to make it more robust and reliable!

#### Bonus Activity - Using a Linter

Linting tools are a great way to ensure that your code is following best practice and adhering to PEP 8 guidelines.

Jupyter Notebooks can be a bit tricky to lint, but there are some tools that can help.

1. Add a code cell to your Notebook as a Shell and run the following installs:

```bash
!pip install nbqa flake8
```

2. Add a code cell to your Notebook as a Shell and run the following command:

```bash
!nbqa flake8 webscraping.ipynb
```

> Have a look at the output and see if there are any improvements that can be made to your code.  You can link each of the suggestions to PEP8 guidelines to see why they are being suggested.

Sometimes, the suggestions may not be in-line with how the team has agreed to write code.  In this instance, you can add a configuration file to 'skip' certain rules.

3. In the root of your folder, create a file called `.flake8` and add the following content:

```bash
[flake8]
ignore = E402, W291, F811
```

> Be careful when ignoring rules as they may mask potential issues in your code.
>
> A full list of the rule codes can be found in the documentation for [Flake8](https://flake8.pycqa.org/en/latest/).

4. Re-run the cell with the `nbqa` command in it.  You should notice that the rules above are now not shown.

> Try and fix the issues that were previously shown and re-run the `nbqa` command to see if you have fixed them.

---

## DONE?

Have you checked off all the tasks in your list? No? Do so before moving on to the next activity!

---

## STUCK?

If you are having trouble with what the code should look like, you can switch to the solution branch to see the completed code.

```bash
git switch solutions
```

Then find checkout the ***tag*** for the **task** you are working on

```bash
git log --oneline
```

```text
# Reveals:
91f5768 (HEAD -> solutions, tag: user-story-2-done, tag: task-28, tag: activity-6) TASK 28 - Create JSON file
0a35c02 (tag: task-27) TASK 27 - All Tested
8daa28b (tag: task-26) TASK 26 - All books from all pages scraped
08a1c08 (tag: task-25) TASK 25 - Test Get all books from category index page
2bfeb55 (tag: task-24) TASK 24 - Get all books from category index page
e8227e3 (tag: task-23) TASK 23 - Refactor extract_category_data
2f0eade (tag: task-22) TASK 22 - Prepare to get book data
542d611 (tag: user-story-1-done, tag: task-21, tag: activity-5) TASK 21 - Number of books in each category obtained
e6cf531 (tag: task-20) TASK 20 - Add tests for extract_category_data
a139fbd TASK 20 - Number in Category Tested
172846a (tag: task-19) TASK 19 - Number in Category added to Category dictionary
bb52933 (tag: task-18) TASK 18 - Number in Category obtained
72203b3 (tag: task-17) TASK 17 - Category Page Obtained
99f1034 (tag: task-16) TASK 16 - Pass in single category to extract_category_data
61ca30a (tag: activity-4) TASK 13, 14, 15 - Extract Category Complete
477f65c (tag: task-12, tag: activity-3) TASK 12 - Category dictionary printed
44ecde9 (tag: task-11) TASK 11 - Isolate the Categories
dc6bdcc (tag: task-10) TASK 10 - Find the Category List
a61d878 (tag: task-9) TASK 9 - Obtain the HTML
7da47e2 (tag: activity-2) Activity 2 - Making a Request complete
ce71c0e (tag: task-8) TASK 8 - Fourth Test passing for request_to_scrape
a160569 (tag: task-7) TASK 7 - Fourth Failing Test for request_to_scrape
57d0381 (tag: task-6) TASK 6 - Third Test passing for request_to_scrape
fcb4c08 (tag: task-5) TASK 5 - Third Failing Test for request_to_scrape
24373d5 (tag: task-4) TASK 4 - Second Test passing for request_to_scrape
9623fa7 (tag: task-3) TASK 3 - Second Failing Test for request_to_scrape
f8a99da (tag: task-2) TASK 2 - First request_to_scrape test passes
9106a4d (tag: task-1) TASK 1 - Failing Test for request_to_scrape
17fbd88 (tag: starting-point, start, main) Starting Point
```

You can switch to the commit that has the completed code for the task using the `tag` value, e.g.:

```bash
git switch "task-8"
```

> Remember, if you have any work in progress, you will need to commit or stash it before you can switch branches (or commits).
>
> In this instance, `git stash` will store any changes since your last commit temporarily, "cleaning" your working directory.
>
> Once you return to your feature branch, you can use `git stash pop` to reapply your changes.
>
> Alternatively, visit the repository on GitHub to see the completed code for the task.

[Understanding the Problem](01-understanding-the-problem.md) <--- Previous <---|---> Next ---> [Extracting the Category List from HTML](03-extracting-category-list-from-html.md)
