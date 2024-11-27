# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Python for Extracting

### Activity 4 - Testing the Category List Extraction Functions

We know that the functions return the correct data for the current version of the home page.  Websites have a tendency to be updated, so we need the function to be able to return without an error if the links are no longer found in the HTML as we have identified it.

---

## Customer's Requirements

> I would like to understand the market for books in different categories and understand the price point of books in each category.  
> This will help me to make decisions about which categories to focus on when launching a rival business.  
> I have come across a website that has a lot of data about books that I would like to use for this analysis.  
> The website address <http://books.toscrape.com/>.

This is a reminder of the customer's requirements.  In the previous activity, you developed the code to make a request for a URL and check that it returns a valid response.  
In this activity, you will extract the data from the HTML that is returned.  
As we are not sure what the actual HTML looks like, we will need to inspect the HTML to understand the structure before we can do any testing!

---

## User Stories

> As a BOOK STORE OWNER,  
> I want to understand how may books are available in each category from [http://books.toscrape.com/],  
> So that I can make decisions about which categories to focus on when launching a rival business

***AND***

> As a BOOK STORE OWNER,  
> I want to understand the average price point of books in each category from [http://books.toscrape.com/],  
> So that I can make decisions about the price point of different books for each category

---

### Task 13 - Test the `extract_element` Function

Here are a list of tests that you could write to test that the function `extract_element` will work with good data and handle exceptions correctly.

1. **Valid HTML with the specified tag and class:** Ensure the function correctly extracts the element.
2. **Valid HTML with the specified tag but without the class:** Ensure the function correctly extracts the element without considering the class.
3. **HTML without the specified tag:** Ensure the function returns None when the tag is not present.
4. **HTML with the specified tag but different class:** Ensure the function returns None when the class does not match.
5. **Empty HTML:** Ensure the function handles empty HTML gracefully.
6. **Invalid HTML:** Ensure the function handles invalid HTML gracefully.

***HINTS:***

- There is no need to do any mocking for this function as it is not making any external requests.
- Put the new tests in a cell with the comment (and a markdown header) `# Test extract_element,` at the top of the cell under the `# Test request_to_scrape` cell.
- You may need to updates the function to handle the edge and corner cases - this is absolutely fine!

---

### Activity 14 - Test the `extract_categories_and_links` Function

Here are a list of tests that you could write to test that the function `extract_categories_and_lists` will work with good data and handle exceptions correctly.

1. **Valid HTML with multiple categories:** Ensure the function correctly extracts all categories and their links.
2. **HTML without any categories:** Ensure the function handles HTML without any `<a>` tags gracefully.
3. **Empty HTML:** Ensure the function handles empty HTML gracefully.
4. **Invalid HTML:** Ensure the function handles invalid HTML gracefully.
5. **HTML with nested categories:** Ensure the function correctly extracts nested categories if applicable.

***HINTS:***

- There is no need to do any mocking for this function as it is not making any external requests.
- You might find that you need to update the function to handle when a category has no HTML in it!
- Put the new tests the cell with the comment `# extract_categories_and_lists` under the recently added tests.

---

### Activity 15 - Test the `extract_book_categories` Function

Here are a list of tests that you could write to test that the function `extract_book_categories` will work with good data and handle exceptions correctly.

1. **The function correctly integrates the helper functions:** Ensure that `extract_element` and `extract_categories_and_links` are called correctly and their results are used properly.
2. **The function handles different HTML structures:** Ensure that the function can handle valid HTML, HTML without the expected structure, empty HTML, and invalid HTML.
3. **The function returns the expected results:** Ensure that the function returns the correct categories and links.

***HINTS:***

- There is no need to do any mocking for this function as it is not making any external requests.
- You might find that you need to update this function and/or helpers to handle `None` values.
- Put the new tests the cell with the comment `# Test extract_book_categories` under the recently added tests.
- The solution has 5 tests for this function.

---

### BONUS

The solution for this activity has additional tests that cover edge and corner cases.  You could add more tests to ensure that the functions are robust and handle all possible scenarios.

It also contains some very *funky* Python code that you might want to research, such as the `**` operator and the `next(iter())` function.  You could research these and see if you can understand how they work.

The solutions show that some test code has been extracted to a constants cell - this is to make sure that the test cells are easy to read and data can be reused across tests.  This is common practice.  Remember to run the constants cell each time you make a change in it.  You will also need to make sure that you import the required values when you create .py files from the notebook.

For linting, remember to SAVE the notebook before running the linting command or it will not recognise the changes you have made!

---

[Extracting the Category List from HTML](03-extracting-category-list-from-html.md) <--- Previous <---|---> Next ---> [Compiling the Category Data](05-compiling-the-category-data.md)
