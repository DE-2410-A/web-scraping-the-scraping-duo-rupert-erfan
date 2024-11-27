# ![Digital Futures](https://github.com/digital-futures-academy/DataScienceMasterResources/blob/main/Resources/datascience-notebook-header.png?raw=true)

## Python For Extracting

### Introduction

This is a practical activity to create a set of Python scripts to perform web scraping.  Data will be scraped from the a website that is intended for such a purpose called [Books to Scrape](http://books.toscrape.com/). The data scraped includes the book title, price, rating, and availability.  Once the data has been scraped, the activities will show how to extract the data from the HTML ready for cleansing and transformation.

The activities include the production Python scripts required and also the unit tests to ensure that all scripts are reliable and working correcty.

---

## Webscraping with Python - Learner Stories

In completing this activity, you will be working on the following user stories from the Data Engineering SKU backlog:

```txt
As a DATA PROFESSIONAL,  
I want to be able to SCRAPE data from websites,  
so that I can COLLECT data from them ready for TRANSFORMATION and INTEGRATION into my DATA PIPELINE

As a DATA PROFESSIONAL,  
I want to be able to write UNIT TESTS using the unittest and/or pytest module,  
so that I can ENSURE my CODE is RELIABLE and WORKS correctly
```

### Definitions of Done

#### Webscraping

- [ ] The data professional has completed a tutorial or training session on web scraping techniques, including the use of libraries such as Beautiful Soup, Scrapy, or Requests-HTML.

- [ ] The data professional can explain the ethical considerations and legal implications of web scraping, including terms of service and robots.txt files.

- The data professional has written scripts demonstrating:
  - [ ] Sending HTTP requests to websites and handling responses.

  - [ ] Parsing HTML or XML content to extract relevant data elements.

  - [ ] Storing scraped data in a suitable format (e.g., CSV, JSON, or a database).

- [ ] The data professional has successfully scraped data from multiple websites, ensuring that the data is accurate and relevant.

- [ ] All scripts are formatted according to PEP 8 guidelines and adhere to Python best practices.

- [ ] The data professional has documented examples of web scraping projects in a shared knowledge repository or personal learning journal.

- [ ] Feedback from peers or mentors on web scraping practices has been reviewed, and any suggested improvements have been implemented.

- [ ] The data professional has created a plan for handling potential changes in website structure or scraping obstacles (e.g., CAPTCHA, pagination).  

---

#### Unit Tests

- [ ] The data professional has completed a tutorial or training session on writing unit tests in Python using unittest and/or pytest, focusing on their syntax and features.

- [ ] The data professional can explain the purpose of unit testing, the differences between unittest and pytest, and how to write effective test cases.

- The data professional has written unit tests demonstrating:
  - [ ] Creating and organising test cases using unittest with TestCase classes, and using assertions to validate code behaviour.

  - [ ] Writing tests using pytest with simple function-based test cases and fixtures for setup and teardown.

  - [ ] Running and interpreting test results from both unittest and pytest.

  - [ ] Implementing parameterised tests and mocking dependencies where needed.

- The data professional has completed exercises that demonstrate:
  - [ ] Writing comprehensive test cases for different types of functions and scenarios (e.g., edge cases, expected failures).

  - [ ] Integrating unit tests into a development workflow, including running tests automatically during development or deployment.

- [ ] Code reviews have been conducted for these tests, confirming that tests are comprehensive, correctly implemented, and follow best practices.

- [ ] The data professional has created a set of unit tests for a script or module, demonstrating thorough testing and validation of the code’s functionality.

- [ ] All tests are organised and documented according to best practices for unittest and pytest.

---

## What is Web Scraping? - ***IMPORTANT

Read this information page on [Web Scraping](./info/webscraping.pdf) ***before continuing with the activity***.

Here are some further resources to help you understand the concepts of web scraping:

- [Web Scraping](https://en.wikipedia.org/wiki/Web_scraping) - Wikipedia
- [Web Scraping](https://www.datacamp.com/community/tutorials/web-scraping-using-python) - DataCamp
- [Web Scraping](https://realpython.com/beautiful-soup-web-scraper-python/) - Real Python
- [Web Scraping](https://www.scrapingbee.com/blog/web-scraping-101-with-python/) - Scraping Bee
- [Web Scraping](https://www.geeksforgeeks.org/implementing-web-scraping-python-beautiful-soup/) - Geeks for Geeks

---

## Getting Started

1. After accepting the assignment from GitHub Classroom, both you and your partner should `clone` the repository to your local machines.

2. One of the pair should then do the following locally:

- Make sure that you are on the `main` branch and then create and switch to a new branch for your work

```bash
# Replace <YOUR-BRANCH-NAME> with anything suitable - e.g. feature/webscraping
git checkout -b feature/<YOUR-BRANCH-NAME>
```

- Create a Python environment ready for running Jupyter Notebook by executing the following commands in the root of the project:

```bash
# Create a new Python environment
python3 -m venv .venv

# Activate the Python environment
source .venv/bin/activate

# Install the required Python packages
pip install ipykernel

# Create a requirements.txt file
pip freeze > requirements.txt

```
  
- Add and commit the changes to the repository
  - **Note:** The `.venv` directory is included in the `.gitignore` file - this will need to be created by the other person and then the `requirements.txt` file used to install the required packages

```bash
git add .
git commit -m "CHORE: set up Python environment"
```

- Push the new branch to your remote GitHub repository

```bash
git push -u origin feature/<YOUR-BRANCH-NAME>
```

3. The other person should then pull the new branch to their local machine and switch to it

```bash
git pull
git switch feature/<YOUR-BRANCH-NAME>
cd /path/to/your/project/root

# Create a new Python environment
python3 -m venv .venv
# Activate the Python environment
source .venv/bin/activate
pip install -r requirements.txt
```

4. Both of you should then ensure that you select the correct Python Interpreter for the Jupyter Notebook
   - In VSCode, set the Kernel from the top right of the Notebook window and choose the `.venv` environment

|---> Next ---> [Understanding the Problem](./activities/01-understanding-the-problem.md)
