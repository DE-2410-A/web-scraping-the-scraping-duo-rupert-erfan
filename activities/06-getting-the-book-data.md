# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Python for Extracting

### Activity 6 - Getting the Book Data

We now have covered off the first part of the customer's requirements by extracting the number of books in each category.  We now need to get the data about the books in each category.

To do this, we'll need to write some more functions, using BeautifulSoup again, so that we can get the data about the books in each category and their price.

However, the execution of this code will start with a call to the `extract_category_data` function as we do not want to make more requests than necessary to get the data we need.

---

## Customer's Requirements

> I would like to understand the market for books in different categories and understand the price point of books in each category.  
> This will help me to make decisions about which categories to focus on when launching a rival business.  
> I have come across a website that has a lot of data about books that I would like to use for this analysis.  
> The website address <http://books.toscrape.com/>.

This is a reminder of the customer's requirements.  In the previous activity, you developed the code to make a request for the category names and links.  
In this activity, you will extract the data by visiting each link and extracting the book data and returning this.  
As we are not sure what the actual HTML looks like, we will need to inspect the HTML to understand the structure before we can do any testing!

---

## User Stories

> DONE:
> *As a BOOK STORE OWNER,*  
> *I want to understand how may books are available in each category from [http://books.toscrape.com/],*  
> *So that I can make decisions about which categories to focus on when launching a rival business*

***AND***

> TO DO:
> As a BOOK STORE OWNER,  
> I want to understand the average price point of books in each category from [http://books.toscrape.com/],  
> So that I can make decisions about the price point of different books for each category

---

## What is the plan?

> Erm...hang on a minute...we've already scraped the data off each category page, haven't we?  We've got the number of books in each category, so we must have the data about the books in each category too, right?
>
> Well, not quite.  We've got the number of books in each category, but we didn't scrape any data about the books on that page, PLUS, some categories had more than one page of books, so we need to scrape the data from each page.
>
> Here's the plan:
>
> 1. Refactor our `extract_category_data` so we scrape the first page of each category IF we supply a `True` value for the `get_book_data` parameter
> 2. Determine if there are more pages of books in the category and use this value to generate other links to scrape
> 3. Write a function to extract the book data from any page
> 4. Visit each of the pages in the category and add the book data to the category dictionary key `books` as a list of book dictionaries containing the title and price of the book
> 5. Return the `categories` list populated with dictionaries category name as a key and a dictionary that contains:
>     - `link` - The link to the first category page
>     - `number_of_books` - The number of books in the category
>     - `books` - A list of dictionaries, each containing the book data (title, price, rating and availability)
>
> Here's where we may need to confer with the Data Analysts to determine how we should structure the data and if they want to be able to make different requests - say just the number of books in each category, just the book data or both at once.  
> However, keeping the functionality separate will allow us to reuse the code in different ways, regardless of how they want it to be presented to them!

---

### Task 22 - Prepare the Execution Code to get the Book Data as well as the Number of Books

1. Comment out the code in the cell `Python Execution Code 3`
2. Create another cell below this with the title `Python Execution Code 4`
3. Make a call to `extract_all_category_data` with `categories` as the first argument and `True` as the second argument
   - Print out the `categories` list
4. Run the cell to see the output

> The output should be the same as before, we now need to do a little refactoring of the `extract_category_data` function to scrape the book data
>
> Initially, we will just scrape the first page of each category, but we will need to determine if there are more pages of books in the category and use this value to generate other links to scrape

---

### Task 23 - Refactor the `extract_category_data` Function and initiate getting the Book Data

1. Just before the return statement in the `extract_category_data` function, add an `if` statement to check if the `get_book_data` parameter is `True`
2. If it is, call the `extract_book_data` function with the `soup` and the `category` dictionary as the arguments
3. Create a Production Code new cell called `extract_book_data` and write the function signature, accepting `category_page` and `category` as arguments
4. In the function, create a variable called `books` and set it to an empty list
5. Return `books` at the end of the function

---

### Task 24 - Scrape the Book Data from the Category Home Page

1. Create a new Production Code cell called `extract_book_data_from_page` and write the function signature, accepting `page` the argument

> A little inspection of the page here will reveal that books are store in an element that has a class of `product_pod`.  We can use this to find all the books on the page

2. Set `book_articles` to be a call to `page.find_all(class_='product_pod)`
3. Create a new `list` called `books` and inside it, use a comprehension call a new function called `extract_book_data_from_article` with each `article` in `book_articles`:

```python
    books = [
        extract_book_data_from_article(article) 
        for article in book_articles
    ]
```

4. Return `books` from the function
5. Create a new Production Code cell called `extract_book_data_from_article` and write the function signature, accepting `article` as the argument
6. Use the `extract_element` function to get a `'h3'` tag from the `article` and set it to `title_element`

> You might be tempted to get the text content of this tag, but that's not a great idea...inspect some pages and work out why we want to get the `title` attribute of the `a` tag inside the `h3` tag!

7. Use a ternary operator to set `title` to `title_element.a['title']` if both `title_element` and `title_element.a` are not `None` otherwise set it to `None`
8. Use the `extract_element` function to get a `'p'` tag with a class of `price_color` from the `article` and set it to `price`
9. Add a call to `get_text(strip=True)` to the `extract_element` call
10. Return a dictionary with keys `'title'` and `'price'` set to the respective obtained values.
11. Modify the `books` variable in the `extract_book_data` function so that it is a call to `extract_book_data_from_page` with the `category_page` as the argument
12. Execute the modified cells and re-run your execution code cell to see the output

> You should see a list of dictionaries with the title and price of the books in each category

```text
Category: Travel
  link: http://books.toscrape.com/catalogue/category/books/travel_2/index.html
  number_of_books: 11
  books: [{'title': "It's Only the Himalayas", 'price': 'Â£45.17'}, ...]
```

> You may notice that the price is not formatted correctly and if we are going to be working out an average price, this needs to be in a number format.
>
> We need to strip the `Â£` characters from the text and then cast it to a `float` type with the correct number of decimal places

13. Rename `price` in the `extract_book_data_from_article` function to `price_str`
14. Define `price` on the next line to slice `price_str` after the second character to the end, casting it to a float rounded to 2 decimal places ***IF*** `price_str` is not `None` otherwise set it to `None`

```python
price = round(float(price_str[2:]), 2) if price_str else None
```

15. Re-run the cells and check the output

```text
Category: Travel
  link: http://books.toscrape.com/catalogue/category/books/travel_2/index.html
  number_of_books: 11
  books: [{'title': "It's Only the Himalayas", 'price': 45.17}, ...]
```

> The price should now be in a number format and mcuh easier to work with - cleaning as we go!

---

### Task 25 - Test the refactored and new functions

Do your existing tests still pass?  If not, why not?  What do you need to do to fix them? (***HINT: THEY SHOULD!***)

However, we have refactored the `extract_category_data` function and added a conditional to it, so we should check that if the condition is met, the`extract_book_data` function is called and that the `books` list is populated with the book data in the category dictionary.

#### `extract_category_data` Function

**Consider:**

- Test that `extract_category_data` correctly adds the number of books in a category and extracts book data when `get_book_data` is `True` and `extract_number_in_category` returns a *valid integer*.
- Test that `extract_category_data` returns 0 books in category and extracts book data when `get_book_data` is `True` and `extract_number_in_category` returns an *invalid integer* value.
- Test that `extract_category_data` handles request_to_scrape failure gracefully and still extracts book data when `get_book_data` is `True`.
- Test that `extract_category_data` handles empty HTML response gracefully and still extracts book data when `get_book_data` is `True`.
- Test that `extract_category_data` returns `0` books when no books are found and still extracts book data when `get_book_data` is `True` (what happens if the number of books value is wrong on the page?)

#### `extract_book_data` Function

**Consider:**

- Verify `extract_book_data` correctly extracts book data from a single page.
- Verify `extract_book_data` returns an empty list when no books are found.
- Verify `extract_book_data` correctly handles invalid data and returns the valid data.

#### `extract_book_data_from_page` Function

**Consider:**

- Verify `extract_book_data_from_page` correctly extracts book data from a page with multiple books.
- Verify `extract_book_data_from_page` returns an empty list when no books are found on the page.
- Verify `extract_book_data_from_page` returns an empty list when the page is empty.
- Verify `extract_book_data_from_page` correctly handles invalid book data and returns the valid data.
- Verify `extract_book_data_from_page` returns an empty list when the page is None.

**HINTS:**

- The code we have written will not pass all of these tests, so you will need to refactor the function to handle the edge and corner cases identified in the test cases.

#### `extract_book_data_from_article` Function

**Consider:**

- Verify `extract_book_data_from_article` correctly extracts book data from an article with valid data.
- Verify `extract_book_data_from_article` correctly extracts book data from an article with a truncated title.
- Verify `extract_book_data_from_article` returns the price str when the price is invalid.
- Verify `extract_book_data_from_article` returns None for price when element is missing from the article.
- Verify `extract_book_data_from_article` returns None for the title when attribute is missing.

**HINTS:**

- The code we have written will not pass all of these tests, so you will need to refactor the function to handle the edge and corner cases identified in the test cases.

---

## Getting the Book Data from Other Pages

We now have a dictionary of categories that has the number of books in each category and the data for the books that are on the category's `index` page.  However, some categories have multiple pages of books and therefore, we'll need to visit each of these pages to scrape the data and add it to the `books` list in the category dictionary.

To do this we will need to:

1. Determine if there are more pages of books in the category and use this value to generate other links to scrape
2. Request the HTML for each additional page and scrape the book data from it

---

### Task 26 - Determine if there are more pages of books in the category

> Examine the HTML of a category page that has multiple pages of books and determine the HTML you need to find to extract that number
>
> You should find that it is in a `li` tag with a class of `current`
>
> Visit additional pages and take a note of the format of the UR
>
> You should find that additional pages replaces `index.html` with `page-2.html`, `page-3.html` etc.

1. Create a new Production Code cell called `extract_number_of_book_pages` and write the function signature, accepting `category_page` as the argument, making it
   - Get the element that holds the *pagination* information
   - Get the text from this element
   - Return an integer that is the second value in the string - **HINT:** use `split()[-1]` and cast to `int`
   - Return `1` if there is no pagination element or an error casting the value obtained

2. Refactor the `extract_book_data` function so it:
   - Sets books to an empty list
   - Calls the `extract_number_of_pages` function and store the result in a variable called `number_of_pages`
   - Calls `extend` on books with the result of calling `extract_book_data_from_page` with the `category_page` as the argument
   - If `number_of_pages` is greater than `1`, iterate from `2` to `number_of_pages + 1` and call `books.extend` with `extract_additional_page_book_data` as the argument and with `category['link']` and `page_number` as arguments
     - You may want to surround this in a `try`/`except` block and `break` on an `Exception` to handle any errors gracefully
   - Return `books` at the end of the function

3. Create a new Production Code cell called `extract_additional_page_book_data` and write the function signature, accepting `category_link` and `page_number` as arguments - this function will return a `list` by:
   - Taking the `category_link` and replacing `index.html` with `page-{page_number}.html`
   - Getting the page data by requesting to scrape the page url
   - Creating a BeautifulSoup object from the page data
   - Returning `extract_book_data_from_page` with the *"page soup"* as the argument
     - Again, you may wish to surround the scraping, soup creation and return in a `try`/`except` block to handle any exceptions gracefully - return an empty list of there is an exception

4. Run the code and check the output (it may take upwards of 30 seconds to scrape the whole site!)

```text
Category: Travel
  link: http://books.toscrape.com/catalogue/category/books/travel_2/index.html
  number_of_books: 11
  books: [{'title': "It's Only the Himalayas", 'price': 45.17}, {'title': 'Full Moon over Noahâ\x80\x99s Ark: An Odyssey to Mount Ararat and Beyond', 'price': 49.43}, {'title': 'See America: A Celebration of Our National Parks & Treasured Sites', 'price': 48.87}, {'title': 'Vagabonding: An Uncommon Guide to the Art of Long-Term World Travel', 'price': 36.94}, {'title': 'Under the Tuscan Sun', 'price': 37.33}, {'title': 'A Summer In Europe', 'price': 44.34}, {'title': 'The Great Railway Bazaar', 'price': 30.54}, {'title': 'A Year in Provence (Provence #1)', 'price': 56.88}, {'title': 'The Road to Little Dribbling: Adventures of an American in Britain (Notes From a Small Island #2)', 'price': 23.21}, {'title': 'Neither Here nor There: Travels in Europe', 'price': 38.95}, {'title': '1,000 Places to See Before You Die', 'price': 26.08}]
Category: Mystery
  link: http://books.toscrape.com/catalogue/category/books/mystery_3/index.html
  number_of_books: 32...
```

5. Run your tests - all 59 should pass!  Have you been keeping an eye on the linting?  Are there any issues that need to be resolved?

---

## And Finally

### Task 27 - Test the refactored and new functions

#### `extract_number_of_book_pages` Function

**Consider:**

- Verify `extract_number_of_book_pages` returns 1 when no pagination is found.
- Verify `extract_number_of_book_pages` correctly extracts the number of pages from valid pagination text.
- Verify `extract_number_of_book_pages` returns 1 when the pagination text is invalid.
- Verify `extract_number_of_book_pages` correctly extracts the number of pages from edge case pagination text 'Page 1 of 400'.
- Verify `extract_number_of_book_pages` correctly extracts the number of pages from edge case pagination text 'Page 1 of 40'.
- Verify `extract_number_of_book_pages` correctly extracts the number of pages from edge case pagination text 'Page 1 of 4'.

#### `extract_additional_page_book_data` Function

**Consider:**

- Verify `extract_additional_page_book_data` correctly extracts book data from a page with multiple books.
- Verify `extract_additional_page_book_data` returns an empty list when the URL is invalid.
- Verify `extract_additional_page_book_data` returns an empty list when the page is empty.
- Verify `extract_additional_page_book_data` returns an empty list when no books are found on the page.
- Verify `extract_additional_page_book_data` returns an empty list when the request to scrape the page fails.
- Verify `extract_additional_page_book_data` correctly handles book data with missing price.
- Verify `extract_additional_page_book_data` correctly handles book data with missing title.
- Verify `extract_additional_page_book_data` correctly handles mixed valid and invalid book data.

#### Refactored `extract_book_data` Function

**Consider:**

- Verify `extract_book_data` correctly extracts book data from multiple pages.
- Verify `extract_book_data` correctly extracts book data from the maximum number of pages.
  - A helper function to generate a large number of books here may be useful!

---

## USER STORY 2 DONE (ALMOST)

We now have extracted the data and have it stored on the machine running the code!

For ***EXTRACTING*** this is ALL we need to achieve.  As a ***Data Engineer***, we will need to consider how we can further ***TRANFORM*** this data into a format that is more useful for the ***Data Analysts*** to work with.  We will should also be considering how we can ***LOAD*** this data into a format that is easily accessible to the ***Data Analysts***.

For now, let's create a JSON file that contains the extracted data.

Don't forget that we can make 2 different calls to the `extract_all_category_data` function to get just the *number of books in each category* or this and the *book price data*

---

### Task 28 - Save the Extracted Data to a JSON File

1. Create a new cell under Execution Code and add the following code:

```python
# Python Execution Code 5
import json
with open('category_data.json', 'w') as file:
    json.dump(category_data, file, indent=2)
```

2. Run the cell to save the data to a JSON file
3. Check the file has been created and that it contains the data you expect

---
