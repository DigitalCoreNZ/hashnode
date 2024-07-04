---
title: "2 of 5: Learning the Scrapy Basics."
datePublished: Tue Apr 09 2024 10:00:27 GMT+0000 (Coordinated Universal Time)
cuid: clus7nlye000q08l01c7xgol6
slug: 2-of-5-learning-the-scrapy-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716790930117/d296b3da-c299-4396-9bd6-0cd08853b423.png
tags: python, scrapy, web-scraping, web-crawling, python-programming, miniconda, programming-tips, virtual-environment, data-extraction, tech-insights, tech-tutorial, scrapy-tutorial, scrapy-spiders

---

JavaScript Scraping | Scrapy | ScrapeGraphAI | Nomic | Embeddings & LLMs

Originally published: Tuesday 9<sup>th</sup> April 2024.

# TL;DR.

This post is a comprehensive guide to using Scrapy for web scraping, starting with setting up a Miniconda environment to creating Scrapy spiders for data extraction. I cover the basics of web scraping, navigating through the target pages, extracting detailed information, and exporting scraped data. My aim is to equip myself with the skills needed to create web scraping projects, while highlighting Scrapy's capabilities as a fast, open-source, and powerful scraping framework.

> **Attributions:**
> 
> [https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***
> 
> [https://docs.scrapy.org/en/latest/intro/tutorial.html](https://docs.scrapy.org/en/latest/intro/tutorial.html)***↗.***

# An Introduction.

Scrapy is the perfect tool for collecting data from the web. It is a fast and adaptable tool but comes with a relatively steep learning curve. However, experienced coders should be able to integrate this framework into their workflows with little trouble:

> The purpose of this post is to introduce the basics of scraping with Scrapy.

# The Big Picture.

Single-page tutorials are fantastic. This [coaching document for Scrapy](https://docs.scrapy.org/en/latest/intro/tutorial.html) is no exception. I just want to know how to use a tool and I don't have time for nuance. The official Scrapy tutorial shows me what I need to get the job done by giving me the information to build my own spider. By the end of the official single-page tutelage, I have a clear idea of how Scrapy works and how to achieve my goal.

This post is nothing more than a over-commented version [of the original](https://docs.scrapy.org/en/latest/intro/tutorial.html). As a new user/n00b/newbie, I add comments to example code so I can understand the syntax of new (to me) programming languages and frameworks.

# Prerequisites.

* A Debian-based Linux distro (I use Ubuntu),
    
* [Miniconda](https://solodev.app/installing-miniconda).
    

# Updating my Base System.

* From the (base) terminal, I update my (base) system:
    

```python
sudo apt clean && \
sudo apt update && \
sudo apt dist-upgrade -y && \
sudo apt --fix-broken install && \
sudo apt autoclean && \
sudo apt autoremove -y
```

# What is Anaconda and Miniconda?

Python projects can run in virtual environments. These isolated spaces are used to manage project dependencies. Different versions of the same package can run in different environments while avoiding version conflicts.

venv is a built-in Python 3.3+ module that runs virtual environments. Anaconda is a Python and R distribution for scientific computing that includes the `conda` package manager. Miniconda is a small, free, bootstrap version of Anaconda that also includes the `conda` package manager, Python, and other packages that are required or useful (like pip and zlib).

[http://www.anaconda.com/](http://www.anaconda.com/)***↗,***

[https://docs.anaconda.com/free/miniconda/index.html](https://docs.anaconda.com/free/miniconda/index.html)***↗, and***

[https://solodev.app/installing-miniconda](https://solodev.app/installing-miniconda).

I ensure [Miniconda is installed](https://solodev.app/installing-miniconda) (`conda -V`) before continuing with this post.

## Creating a Miniconda Environment.

* I use the `conda` command to display a `list` of Miniconda `env`ironments:
    

```bash
conda env list
```

* I use `conda` to `create`, and `activate`, a new environment named (-n) (Scrapy):
    

```bash
conda create -n Scrapy python=3.11 -y && conda activate Scrapy
```

> NOTE: This command creates the (Scrapy) environment, then activates the (Scrapy) environment.

## Creating the Scrapy Home Directory.

> NOTE: I will now define the home directory in the environment directory.

* I create the `Scrapy` home directory:
    

```bash
mkdir ~/Scrapy
```

* I make new directories within the (Scrapy) environment:
    

```bash
mkdir -p ~/miniconda3/envs/Scrapy/etc/conda/activate.d
```

* I use the Nano text editor to create the `set_working_directory.sh` shell script:
    

```bash
sudo nano ~/miniconda3/envs/Scrapy/etc/conda/activate.d/set_working_directory.sh
```

* I copy the following, paste (CTRL + SHIFT + V) it to the `set_working_directory.sh` script, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```bash
cd ~/Scrapy
```

* I activate the (base) environment:
    

```bash
conda activate
```

* I activate the (`Scrapy`) environment:
    

```bash
conda activate Scrapy
```

> NOTE: I should now, by default, be in the `~/Scrapy` home directory.

# What is Ollama?

Ollama is a tool for downloading, setting up, and running LLMs (large language models). It lets me access powerful models like Llama 2 and Mistral and helps me run them on my local Linux, macOS, and Windows systems.

[https://ollama.com](https://ollama.com)↗.

Ollama must be installed (`ollama -v`) before continuing with this post.

## Installing Ollama.

> NOTE: When learning a new (to me) programming language or framework, I would take example code and add comments to every line. Thanks to LLMs (Large Language Models), this laborious and time-consuming task has been relegated to easy-to-use tools that don't complain.

I install Ollama within the Scrapy environment:

```python
curl https://ollama.ai/install.sh | sh
```

I list the LLMs downloaded by Ollama:

```python
ollama list
```

If the above command fails, I run Ollama as a background service:

```python
ollama serve &
```

If the following error shows when running the previous command, that means Ollama is already running as a background service:

```python
Error: listen tcp 127.0.0.1:11434: bind: address already in use
```

## Pulling the CodeLlama Model.

> NOTE: There are many models that support software development. CodeLlama is one such model.

* I use `Ollama` to `pull` down the `CodeLlama` model to the Scrapy environment:
    

```python
ollama pull codellama
```

> NOTE: Later, I will use CodeLlama to add comments to the code examples.

# What is Scrapy?

Scrapy is a fast, open-source, extensible, and powerful Python-based scraping framework that is used to extract website data. Although it was originally designed for web scraping, Scrapy can also use APIs to extract data, or even as a general purpose web crawler. Like other frameworks, there is a steep learning curve, however experienced systems operators and software developers should be able to understand the documents, install this utility, and comfortably use Scrapy without too much effort.

[https://scrapy.org](https://scrapy.org)↗.

## Installing the Dependencies.

* From the (Scrapy) terminal, I use APT (Advanced Packaging Tool) to install the dependencies for Scrapy:
    

```bash
sudo apt install -y python3 python3-dev python3-pip libxml2-dev libxslt1-dev zlib1g-dev libffi-dev libssl-dev
```

> NOTE: Python3 has already been installed so it may be skipped during this process.

## Installing the Scrapy Tool.

* I use `pip` to `install` the `Scrapy` tool:
    

```bash
pip install Scrapy twisted[tls]
```

> NOTE: [Twisted](https://twisted.org/) is an event-driven, Python-based networking engine.

## Starting a Scrapy Project.

* I start a Scrapy project called tutorial:
    

```bash
scrapy startproject tutorial
```

## Creating a Spider.

* I use the Nano text editor to create a file called `quotes_spider01.py`:
    

```bash
nano ~/Scrapy/tutorial/tutorial/spiders/quotes_spider01.py
```

* I copy the following, add it (CTRL + SHIFT + V) to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```python
# Import the Path class from the pathlib module, which is used
# to work with file paths in Python.
from pathlib import Path
# Import the scrapy module, which provides a framework for building
# web scrapers in Python.
import scrapy

# Define a class called QuotesSpider, which inherits from the
# scrapy.Spider class. The QuotesSpider class is used to define
# the behavior of the web scraper, such as how it should handle
# requests and parse responses.
class QuotesSpider(scrapy.Spider):
    # Set the name of the web scraper to "quotes01". This name
    # will be used to identify this spider in Scrapy's built-in
    # scheduler and in logs.
    name = "quotes01"
    # Define a method called start_requests that is called when
    # the spider starts running. It returns a sequence of requests
    # that are used to start the crawl. In this case, I am generating
    # two requests to retrieve quotes from these web pages:
    #    "https://quotes.toscrape.com/page/1/"
    #    "https://quotes.toscrape.com/page/2/".
    def start_requests(self):
        # Define a list of URLs that will be used as the start requests
        # for our spider. In this case, we are generating two URLs by
        # concatenating the base URL "https://quotes.toscrape.com/"
        # with the page numbers "1" and "2".
        urls = [
            "https://quotes.toscrape.com/page/1/",
            "https://quotes.toscrape.com/page/2/",
        ]
        # Generate a new request for each URL in my list of URLs.
        # The url parameter specifies the URL to retrieve, and the
        # callback parameter specifies which method will be called
        # to handle the response. In this case, I am using the
        # self.parse method to handle the response.
        for url in urls:
            yield scrapy.Request(url=url, callback=self.parse)
    # Define a method called parse that is called for each response
    # received from my requests. It takes a response object as an
    # argument, which contains the HTML content of the page
    # being parsed.
    def parse(self, response):
        # Extract the page number from the URL of the response using
        # string manipulation techniques. I split the URL on the "/"
        # character, and then use negative indexing to get the last
        # element (i.e., the page number).
        page = response.url.split("/")[-2]
        # Generate a filename for the HTML content of the page. I
        # concatenate the word "quotes-" with the page number to
        # generate the filename.
        filename = f"quotes-{page}.html"
        # Use the Path class from the pathlib module to write the
        # response body (i.e., the HTML content of the page) to a
        # file on my local system. The write_bytes method takes a
        # binary string as an argument, which is the content of the
        # file I want to save.
        Path(filename).write_bytes(response.body)
        # Log a message to the console indicating that a file has been
        # saved using Scrapy's built-in logging facilities. The log
        # method takes a string argument, which is the message I want
        # to log. I am using the f string notation to include
        # variables in the log message (i.e., the filename).
        self.log(f"Saved file {filename}")
```

> NOTE: This Scrapy script performs a web scraping task to retrieve quotes from the website "[https://quotes.toscrape.com/](https://quotes.toscrape.com/)". It will save each page of quotes as a separate HTML file on my local system.

## Adding Comments.

[The original source code](https://docs.scrapy.org/en/latest/intro/tutorial.html#our-first-spider)↗ did not have any comments. Scrapy (and Python in general) are new technologies to me, so adding comments helps me understand the syntax of the framework and language.

* I use `Ollama` to `run` the `CodeLlama` model:
    

```python
ollama run codellama
```

* At the CodeLlama prompt (&gt;&gt;&gt;), I prepare it for multi-line input with a set of three double quotes and a simple prompt:
    

```python
"""
Add comments for the following Scrapy module:
```

* I copy (CTRL + C) [the original source code](https://docs.scrapy.org/en/latest/intro/tutorial.html#our-first-spider)↗.
    
* I paste (CTRL + SHIFT + V) the code into the CodeLlama prompt.
    
* I end multi-line input with another set of three double quotes:
    

```python
"""
Add comments for the following Scrapy module:
[Scrapy source code goes here.]
"""
```

* After adding the second set of three double quotes, I hit the ENTER key to have CodeLlama generate the comments.
    
* I add the comments to [the original source code](https://docs.scrapy.org/en/latest/intro/tutorial.html#our-first-spider)↗ (as shown above).
    

> NOTE: This is the process I will use to add comments throughout the rest of this post. Comments begin with (#) so the compiler or runtime knows to ignore everything after the hash for the rest of that line. The comments above span multiple lines for easy reading.

## Running the Spider.

* I change into the tutorial directory:
    

```bash
cd ~/Scrapy/tutorial/tutorial
```

* I run the spider:
    

```bash
scrapy crawl quotes01
```

> This command uses the name `quotes01` that is defined in the `quotes_spider01.py` module.

* I list the contents of the current directory (`~/Scrapy/tutorial/tutorial`):
    

```python
ls
```

> NOTE: There are now two new files that have been created: `quotes-1.html` and `quotes-2.html`*.*

## Scrapy Shell 1 of 2: An Introduction.

* I start the Scrapy shell:
    

```python
# I start a Scrapy shell session where I can execute Scrapy commands.
scrapy shell 'https://quotes.toscrape.com/page/1/'
```

> NOTE: Pay attention to the single quotes.

* I select a CSS element called the `title` tag using the `response.css()` method:
    

```python
# The `response.css()` method is used to select elements
# on a web page based on their CSS selector. In this case, the 
# selector `title` is used to select all elements with the tag
# name `title` in the HTML document of the response.
response.css('title')
```

> NOTE 1/2: The response should look like the following:

\[&lt;Selector query='descendant-or-self::title' data='&lt;title&gt;Quotes to Scrape&lt;/title&gt;'&gt;\]

> NOTE 2/2: There is a list-like object called [`SelectorList`](https://docs.scrapy.org/en/latest/topics/selectors.html#scrapy.selector.SelectorList), which represents a list of `Selector` objects that wrap around XML/HTML elements.

* I extract all the text from the `title` tag using the `::text` pseudo-class and `getall()` method:
    

```python
# The `::text` pseudo-class specifies that only the
# text content of the selected elements should be extracted.
# The `getall()` method is used to extract the data
# from the selected elements and return it as a list.
response.css("title::text").getall()
```

> NOTE 1/3: The result:

\['Quotes to Scrape'\]

> NOTE 2/3: The `::text` is used to select only the text directly inside `<title>` tag. Remove it to get the full title element, including its tags.

> NOTE 3/3: It is possible that a selector returns more than one result, so we use `getall()` to extract all of the results.

* I use the `get()` method when I only want the first result:
    

```python
# The `get()` method is used to extract the data from the selected
# elements and return it as a single value. In this case, it returns
# the first text node within the `<title>` element on the page.
response.css("title::text").get()
```

* This alternative has the same result:
    

```python
# The `[0]` at the end of the selector indicates that we want to
# extract only the first match, if there are multiple matches.
response.css("title::text")[0].get()
```

* The following will raise an `IndexError` exception:
    

```python
# This line of code is using the `CSS` selector to extract an element
# with the tag name "noelement". However, since there is no such element
# on the page, the result will be an empty list. In Scrapy, it is not
# possible to use a CSS selector to retrieve an element that does not
# exist on the page.
response.css("noelement")[0].get()
```

* I can use `.get()` directly on the `SelectorList` instance:
    

```python
response.css("noelement").get()
```

> NOTE: This time, there was no error raised. For scraping code, I want resilience against errors due to things not being found on a page. A better solution is to use a \`try\` block.

* I can use the `re()` method to scrape using regular expressions:
    

```python
# This line of code is using the `CSS` selector to extract the text
# content of an HTML element with the tag name "title" and then using
# the `re` method to perform a regular expression match on the extracted
# text. The regular expression pattern used in this case is `"Quotes.*"`
# which matches any string that starts with "Quotes".
response.css("title::text").re(r"Quotes.*")
```

```python
# The `re` method performs a regular expression match on the extracted
# text. The regular expression pattern used in this case is `"Q\w+"`
# which matches any string that starts with "Q" and has one or more
# word characters following it (letters, digits, or underscores).
response.css("title::text").re(r"Q\w+")
```

```python
# The `re` method performs a regular expression match on the extracted
# text. The regular expression pattern used in this case is `"(\w+)
# to (\w+)"` which matches any string that contains two words
# separated by the phrase "to".
response.css("title::text").re(r"(\w+) to (\w+)")
```

* Scrapy selectors also support using XPath expressions:
    

```python
# The `XPath` selector extracts all HTML elements with the tag name
# "title" from the page being scraped. The `//` at the beginning of
# the XPath expression indicates that I want to search for an element
# in the entire document, rather than just in the current node.
response.xpath("//title")
```

```python
# The `XPath` selector extracts the text content of all HTML elements
# with the tag name "title" from the page being scraped and then using
# the `get()` method to retrieve the actual text value. The `//` at the
# beginning of the XPath expression indicates that I want to search for
# an element in the entire document, rather than just in the current
# node.
response.xpath("//title/text()").get()
```

> NOTE: XPath expressions are the foundation of Scrapy Selectors. In fact, CSS selectors are converted to XPath under-the-hood.

* I quit the Scrapy shell:
    

```python
quit()
```

## Scrapy Shell 2 of 2: Extracting Data.

* I start the Scrapy shell:
    

```python
scrapy shell 'https://quotes.toscrape.com'
```

* I get a list of selectors:
    

```python
# This line is trying to extract all div elements with
# class `quote` from the HTML document using the css()
# method of a Response object.
response.css("div.quote")
```

* I assign the first selector to a variable called `quote`:
    

```python
# This line is trying to extract the first div element with
# class `quote` from the HTML document using the css() method
# of a Response object, then assigning (=) the result to the
# `quote` variable.
quote = response.css("div.quote")[0]
```

* I use the quote object to extract `text`, `author` and the `tags`:
    

```python
# This line is trying to extract the text from a span element
# with class `text` inside the quote element using the css()
# method of a Selector object, then assigning (=) the results
# to the `text` variable.
text = quote.css("span.text::text").get()
```

```python
text
```

```python
# This line is trying to extract the author name from
# a small element with class `author` inside the quote
# element using the css() method of a Selector object,
# then assigning (=) the results to the `author` variable.
author = quote.css("small.author::text").get()
```

```python
author
```

```python
# This line is trying to extract all anchor elements with class
# `tag` inside the div element with class `tags` inside the quote
# element using the css() method of a Selector object, then
# assigning (=) the results to the `tags` variable. The getall()
# method is used because there may be multiple results.
tags = quote.css("div.tags a.tag::text").getall()
```

```python
tags
```

* I can now iterate over the quotes' elements and put them together into a Python dictionary:
    

```python
# This is an example of how to iterate over all div elements
# with class "quote" in the HTML document using the css() method
# of a Response object.
for quote in response.css("div.quote"):
    text = quote.css("span.text::text").get()
    author = quote.css("small.author::text").get()
    tags = quote.css("div.tags a.tag::text").getall()
    print(dict(text=text, author=author, tags=tags))
```

* I quit the shell:
    

```python
quit()
```

## Exporting the Scraped Data.

> With my new insights that were provided by the shell exercises above, I can now understand, and follow, the code below.

* I use the Nano text editor to create a file called `quotes_spider02.py`:
    

```bash
nano ~/Scrapy/tutorial/tutorial/spiders/quotes_spider02.py
```

* I copy the following, add it (CTRL + SHIFT + V) to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes02"
    start_urls = [
        "https://quotes.toscrape.com/page/1/",
        "https://quotes.toscrape.com/page/2/",
    ]

    def parse(self, response):
        for quote in response.css("div.quote"):
            yield {
                "text": quote.css("span.text::text").get(),
                "author": quote.css("small.author::text").get(),
                "tags": quote.css("div.tags a.tag::text").getall(),
            }
```

This is a method called `parse` that takes a `response` object as an argument, and it iterates over the quotes on the page using CSS selectors. For each quote, it extracts the text, author, and tags using CSS selectors and returns them in a dictionary format.

Here are some comments on what each line of code is doing:

* `for quote in response.css("div.quote"):`: This line iterates over all the quotes on the page using the `response.css` method, which takes a CSS selector as an argument and returns a list of elements that match the selector. The CSS selector `"div.quote"` matches all elements with the class `quote` within the `div` element.
    
* `yield {`: This line uses the `yield` keyword to return a dictionary object for each quote. The dictionary contains three keys: "text", "author", and "tags".
    
* `text": quote.css("span.text::text").get(),`: This line extracts the text of the quote using CSS selectors. We use the `quote.css` method to find all elements with the class `text` within the current quote element, and then we use the `get` method to get the first match as a string.
    
* `author": quote.css("`[`small.author`](http://small.author)`::text").get(),`: This line extracts the author of the quote using CSS selectors. We use the `quote.css` method to find all elements with the class `author` within the current quote element, and then we use the `get` method to get the first match as a string.
    
* `tags": quote.css("div.tags a.tag::text").getall(),`: This line extracts the tags of the quote using CSS selectors. We use the `quote.css` method to find all elements with the class `tags` within the current quote element, and then we use the `getall` method to get all matches as a list of strings.
    
* `}`: This line ends the dictionary object for each quote.
    

Overall, this code extracts text, author, and tags from each quote on the page using CSS selectors and returns them in a dictionary format.

* I run the spider:
    

```bash
scrapy crawl quotes02
```

* I modify the command to save the results to a JSON file:
    

```python
scrapy crawl quotes02 -O quotes.json
```

> NOTE: There is now a new file that has been created: `quotes.json`*.* The `-O` flag overwrites the existing file. When appending to a file, consider using a different serialization format, such as [JSON Lines](http://jsonlines.org): `scrapy crawl quotes -o quotes.jsonl`. The `-o` flag (small 'o') appends any content to the `quotes.jsonl` file.

## Recursively Following Links.

* This is the markup that creates a link to the next page:
    

```xml
<ul class="pager">
    <li class="next">
        <a href="/page/2/">Next <span aria-hidden="true">&rarr;</span></a>
    </li>
</ul>
```

* I run the shell:
    

```python
scrapy shell 'https://quotes.toscrape.com'
```

* I try to extract the link:
    

```python
response.css('li.next a').get()
```

> NOTE: Here is the result:

'&lt;a href="/page/2/"&gt;Next &lt;span aria-hidden="true"&gt;→&lt;/span&gt;&lt;/a&gt;'

> What I really want is the `href` attribute of the `<a>` tag.

* I modify my command:
    

```python
response.css("li.next a::attr(href)").get()
```

* I can also use an `attrib` property to shorten the command:
    

```python
response.css("li.next a").attrib["href"]
```

> NOTE: The `attrib` property is, in my opinion, easier to understand.

* I quit the shell:
    

```python
quit()
```

* I use the Nano text editor to create a file called `quotes_spider03.py`:
    

```bash
nano ~/Scrapy/tutorial/tutorial/spiders/quotes_spider03.py
```

* I copy the following, add it (CTRL + SHIFT + V) to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes03"
    start_urls = [
        "https://quotes.toscrape.com/page/1/",
    ]

    def parse(self, response):
        for quote in response.css("div.quote"):
            yield {
                "text": quote.css("span.text::text").get(),
                "author": quote.css("small.author::text").get(),
                "tags": quote.css("div.tags a.tag::text").getall(),
            }

        next_page = response.css("li.next a::attr(href)").get()
        if next_page is not None:
            next_page = response.urljoin(next_page)
            yield scrapy.Request(next_page, callback=self.parse)
```

> NOTE: Since the links can be relative, the `parse()` method looks for the link to the `next_page`, builds an absolute URL using the `urljoin()` method, and uses `yield` to make a new `.Request` to the `next_page`. It also registers itself as a `callback` to handle the data extraction for the next page, and to keep the crawling going through all the pages.

* I run the module and save the results to the `quotes.json` file:
    

```python
scrapy crawl quotes03 -O quotes.json
```

## Creating Shortcuts for Requests.

* I use the Nano text editor to create a file called `quotes_spider04.py`:
    

```bash
nano ~/Scrapy/tutorial/tutorial/spiders/quotes_spider04.py
```

* I copy the following, add it (CTRL + SHIFT + V) to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```python
import scrapy


class QuotesSpider(scrapy.Spider):
    name = "quotes04"
    start_urls = [
        "https://quotes.toscrape.com/page/1/",
    ]

    def parse(self, response):
        for quote in response.css("div.quote"):
            yield {
                "text": quote.css("span.text::text").get(),
                "author": quote.css("span small::text").get(),
                "tags": quote.css("div.tags a.tag::text").getall(),
            }

        next_page = response.css("li.next a::attr(href)").get()
        if next_page is not None:
            yield response.follow(next_page, callback=self.parse)
```

> NOTE: `response.follow` supports relative URLs directly but it just returns a `Request` instance; I still have to `yield` the Request.

* I run the spider:
    

```bash
scrapy crawl quotes04
```

* I can pass a selector to `response.follow` instead of a string:
    

```python
for href in response.css("ul.pager a::attr(href)"):
    yield response.follow(href, callback=self.parse)
```

* With `response.follow`, I can automatically access the `href` attribute of `<a>` tags:
    

```python
for a in response.css("ul.pager a"):
    yield response.follow(a, callback=self.parse)
```

* I can make multiple Requests with `response.follow_all`:
    

```python
anchors = response.css("ul.pager a")
yield from response.follow_all(anchors, callback=self.parse)
```

* I can even use a shortened version of the command:
    

```python
yield from response.follow_all(css="ul.pager a", callback=self.parse)
```

## Scraping Info about the Authors.

* I use the Nano text editor to create a file called `author_spider01.py`:
    

```bash
nano ~/Scrapy/tutorial/tutorial/spiders/author_spider01.py
```

* I copy the following, add it (CTRL + SHIFT + V) to the module, save (CTRL + S) the changes, and exit (CTRL + X) Nano:
    

```python
import scrapy


class AuthorSpider(scrapy.Spider):
    name = "author01"

    # The `start_urls` attribute is used to define the starting URLs
    # for the scraper, which in this case is a single URL that returns
    # a list of author pages. The `parse` method is called when I
    # receive a response from one of the starting URLs, and it
    # iterates over the links to each author page and yields a
    # request for each link. The response from each request is
    # then passed to the `parse_author` method.
    start_urls = ["https://quotes.toscrape.com/"]

    # The `parse` method iterates over the links to each author
    # page and yields a request for each link. The response from
    # each request is then passed to the `parse_author` method.
    def parse(self, response):
        author_page_links = response.css(".author + a")
        yield from response.follow_all(author_page_links,
        self.parse_author)

        pagination_links = response.css("li.next a")
        yield from response.follow_all(pagination_links, self.parse)

    # The `parse_author` method extracts data from each author page,
    # including the author's name, birthdate, and bio. It uses CSS
    # selectors to find these elements on the page and returns a
    # dictionary with the extracted data.
    def parse_author(self, response):
        def extract_with_css(query):
            return response.css(query).get(default="").strip()

        yield {
            "name": extract_with_css("h3.author-title::text"),
            "birthdate": extract_with_css(".author-born-date::text"),
            "bio": extract_with_css(".author-description::text"),
        }
```

* I run the spider:
    

```bash
scrapy crawl author01
```

## Examining Spider Arguments.

* Consider this command line argument with an `-a` flag:
    

```bash
scrapy crawl quotes05 -O quotes-humor.json -a tag=humor
```

> NOTE: The `-a` option above is used to specify an `argument` for the spider which, in this case, is `tag`.

* Now let's look at the file that will process this tag:
    

```bash
import scrapy
# This Scrapy module is for scraping quotes from the website
# "quotes.toscrape.com". It uses the `scrapy.Spider` class to
# define a spider that will crawl the website and extract the
# quotes. The spider has two methods: `start_requests`, which
# defines the starting URL of the crawl, and `parse`, which is
# called for each response returned by the crawl.

class QuotesSpider(scrapy.Spider):
    name = "quotes05"

    # The `start_requests` method uses the `yield` keyword to return
    # a request object that will be used to start the crawl. The request
    # object specifies the URL of the website to be scraped and the
    # callback function that will be executed when the response is
    # received. In this case, the callback function is the `parse`
    # method.
    def start_requests(self):
        url = "https://quotes.toscrape.com/"
        # The `getattr()` method 
        tag = getattr(self, "tag", None)
        # This module defines a `tag` attribute that can be set to
        # specify a specific tag for which quotes should be scraped.
        # For example, if the user sets `tag="funny"`, the spider will
        # only scrape quotes with the "funny" tag.
        if tag is not None:
            url = url + "tag/" + tag
        yield scrapy.Request(url, self.parse)

    # The `parse` method uses CSS selectors to extract the quotes from
    # the HTML content of the response. It first selects all elements
    # with the class "quote" and then iterates over each quote element
    # to extract the text and author information. The text is extracted
    # using the `::text` pseudo-class, which returns the text content of
    # an element. The author is extracted using the `::text`
    #  pseudo-class as well, but it is wrapped in a small
    # element with the class "author".
    def parse(self, response):
        for quote in response.css("div.quote"):
            yield {
                "text": quote.css("span.text::text").get(),
                "author": quote.css("small.author::text").get(),
            }

        # After extracting the quotes, the method checks if there are
        # more pages to be scraped by checking if the next page link
        # exists. If it does, the method returns another request object
        # that will be used to follow the next page link and continue
        # the crawl. The `response.follow` method is used to create a
        # new request object that will be used to follow the next page
        # link.
        next_page = response.css("li.next a::attr(href)").get()
        if next_page is not None:
            yield response.follow(next_page, self.parse)
```

> NOTE: If I pass the `tag=humor` argument to this spider, then I will only visit URLs from the `humor` tag, such as [`https://quotes.toscrape.com/tag/humor`](https://quotes.toscrape.com/tag/humor):
> 
> [https://docs.scrapy.org/en/latest/topics/spiders.html#spider-arguments](https://docs.scrapy.org/en/latest/topics/spiders.html#spider-arguments)

# Following Up.

Now that I have a *very basic* understanding of how Scrapy works, it is time to follow up, and reinforce what I have learned, with other tutorials. Choosing the right tutorials can be problematic but it does *not* have to be complicated. I tend to start with learning materials that cover very specific points, especially if they are short.

A quick search for Scrapy tutorials should work a treat.

# The Results.

In this post, I've covered the basics of using Scrapy for web scraping. From setting up my environment with Miniconda, understanding the essentials of Python virtual environments, and diving into the creation of Scrapy spiders for data extraction, I've covered a broad spectrum of knowledge. I demonstrated how to scrape quotes, navigate through pages, and even extract detailed information about authors. The [original tutorial](https://docs.scrapy.org/en/latest/intro/tutorial.html) (of which this is but pale copy) helped me get familiar with Scrapy's capabilities and also led to acquiring the practical skills needed to undertake my own web scraping projects. With this knowledge, I'm better prepared to use web scraping for opening up a world of analysis, insight, and innovation. My interest lies in creating large language model embeddings for web development and Scrapy will help me collect processes and procedures for the latest WebDev and AppDev technologies and best practices.

# In Conclusion.

I just dove into the world of web scraping with Scrapy and I'm looking forward using it in my workflow. I've always been interested in converting raw data into knowledge, then sharing my insights through practical implementations. That's why I decided to take a closer look at Scrapy, a leading tool in the web scraping arena. My journey led me to understanding its mechanics and appreciating its capabilities.

Here's what I discovered: Scrapy is more than just a tool; it's a gateway to efficiently harvesting web data. It's a comprehensive framework that caters to all levels of expertise.

🔹 Scrapy is fast, open-source, incredibly versatile, and makes data extraction a breeze. It's designed for scraping and for crawling web applications using APIs. The learning curve is definitely there, but absolutely worth the climb.

🔹 I began with setting up my Miniconda environment, ensuring I had all the tools and dependencies I needed. The simplicity of creating virtual environments with Miniconda always streamlines my processes.

🔹 With everything set, I embarked on creating my first Scrapy spider. Writing scripts that navigates through web pages, extracts data, and saves it locally was satisfying, enlightening, and empowering.

🔹Leveraging Scrapy for more complex tasks, like recursively following links and extracting detailed information shows the potential of this framework.

Through this exploration, I've gained invaluable insights into the world of web scraping. Scrapy has opened up new possibilities for data analysis and innovation, making it an indispensable tool in my tech arsenal.

Now, I'm curious to hear from you! Have you used Scrapy or any other web scraping tools in your projects? What has been your experience? Let's share insights and learn from each other's journeys!

Until next time: Be safe, be kind, be awesome.

#Scrapy #ScrapyTutorial #ScrapySpiders #WebScraping #WebCrawling #DataExtraction #Python #PythonProgramming #Miniconda #VirtualEnvironments #ProgrammingTips #TechTutorial #TechInsights

[Scraping URLs](https://solodev.app/1-of-5-scraping-website-urls) | [Scraping Tutorial](https://solodev.app/2-of-5-scraping-tutorial-for-the-scrapy-tool) | Scraping Data | Making Embeddings | Using Embeddings