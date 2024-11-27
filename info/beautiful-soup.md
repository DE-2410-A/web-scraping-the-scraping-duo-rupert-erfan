# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Libraries for Webscraping - Beautiful Soup

### Overview

Once you have made a request for the HTML of a webpage, how do you actually extract the data that is contained within it.  Parsing libraries make it simpler to extract the data you need from the HTML.  One of the most popular libraries for this is Beautiful Soup.

---

### What is Beautiful Soup?

- Beautiful Soup is a Python library for pulling data out of HTML and XML files.
- It creates a parse tree from page source code that can be used to extract data easily.
- It is a powerful library that makes it easy to scrape information from web pages.
- Other libraries exist and may be used dependent on the preferences of teams, but Beautiful Soup is a popular choice.

---

### How does Beautiful Soup work?

1. It takes the HTML content returned by a web server and creates a parse tree from it.
   - it basically converts the HTML document into a tree of Python objects.
2. To work with the data, you need to understand the structure of the HTML document and find where the data you need is located.
3. You can then navigate the parse tree to extract the data you need.
   - There are 4 major kind of objects in the parse tree:
     - Tag,
     - NavigableString,
     - BeautifulSoup,
     - Comment

#### Tag

- A Tag object corresponds to an XML or HTML tag in the original document.
- It has a name and attributes.
- It can be navigated through the tree and has methods and attributes that allow you to navigate and search the parse tree.
- You can access the tag's name using the `.name` attribute.
- You can access the tag's attributes using the `.attrs` attribute.
- You can access the tag's content using the `.string` attribute.
- You can access the tag's children using the `.contents` attribute.
- You can access the tag's parent using the `.parent` attribute.
- You can access the tag's siblings using the `.next_sibling` and `.previous_sibling` attributes.
- You can access the tag's descendants using the `.descendants` attribute.
- You can access the tag's descendants using the `.find_all()` method.
- You can access the tag's descendants using the `.find()` method.
- You can access the tag's descendants using the `.select()` method.
- You can access the tag's descendants using the `.get_text()` method.
- You can access the tag's descendants using the `.get()` method.

Using these methods and attributes, you can navigate the parse tree to extract the data you need and are often safer than trying to access data and attributes directly.  BeautifulSoup will not throw an error if the tag or attribute does not exist, it will return `None`.
