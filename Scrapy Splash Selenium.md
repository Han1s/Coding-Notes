# I. Introduction

- libraries:
  - Requests
  - BeautifulSoup
  - Scrapy more complex (1k pages per minute)
- Scrapy
  - Spiders
    - What we want to extract from the page
      - **Scrapy Spider**
      - **Crawl Spider**
      - XML Feel Spider
      - CSV Feed Spider
      - Sitemap Spider
  - Pipelines
    - how to process the data
    - cleaning it
    - remove duplication
    - store data
  - Middlewares
    - request / response
    - e.g. injecting headers
    - proxying
  - Engine
    - Coordinating other components
  - Scheduler
    - Preserving order of operations
    - its a queue

Example:

- Spider sends request to the engine
- Engine transmits it to scheduler
- Request will be send to the engine
- Request is send to the **middleware downloader** responsible for getting the response
- response sent to the engine
- response send to middleware spider responsible for extracting data
- item send to the engine
- then pipeline

- Websites usually include in their directory **Robots.txt**
  - this contains three instructions
    - user agent - identity of the spider
    - allow - pages allowed to scrape
    - disallow - pages forbidden to scrape
  - example.www.facebook.com/robots.txt

 ## 2.Setting up Scrapy Development environment

- Use **Anaconda**
  - Anaconda Navigator
  - Install **scrapy**
    - `conda install -c conda-forge scrapy pylint autopep8 -y` 
  - Install vs code from the anaconda and launch it through anaconda

# II. Scrapy Fundamentals

## 6. Part 1

- open the environment we created 
- open its terminal
- `scrapy` lists all the commands
- `scrapy bench` runs a quick benchmark test - better cpu scrapes faster
- `scrapy fetch`  fetches the markup of the website you specify. E.g. `scrapy fetch http://google.com` 
- `scrapy genspider` generate a spider using pre-defined templates
- `scrapy runspider`runs a self-contained spider (without creating a project)
- `scrapy settings` returns all the settings
- `scrapy shell` allows you to experiment with the website youre trying to scrape before writing actual project
- `scrapy startproject` scaffolds a new project
- `scrapy version` returns a version youre using
- `scrapy view` opens up a website of your choice as seen by Scapy - spider can see the website as a normal user.

## 7. Part 2

- `scrapy startproject projectname` creates a basic project
- `cd projectname` 
- `scrapy genspider spidername www.xxx.com`  creates a spider
  - if you open the spider `spidername` 
    - **allowed domains** can never have http protocol
    - **start_urls** can start with https as scrapy by default starts with http


## 7. Part 3

- `conda install ipython` 
- `scrapy shell` opens scrapy shell
  - this has some useful objects and some useful shortcuts
- `fetch("https://www.worldometers.info/world-population/population-by-country/")` 
  - 404 robots.txt means it could not find the file
- the request way:
  - `r = scrapy.Request(url="https://url.domain/")`
  - `fetch(r)`
  - `response.body` prints body
  - `view(response)` shows the response as bot sees it
  - **note that bots see sites without js**
  - F12 and ctrl+shift+P and `disable javascript` disables javascript

## 9. Part 4

- to test the xpath expression before implementing it in scrapy
  - in console press `ctrl+F` 
  - put there the expression and the chrome will highlight it. So `//h1` will highlight title
- to output the title in scrapy via **xpath**
  - `title = response.xpath("//h1")`
  - `title` outputs title
  - `title = response.xpath("//h1/text()")` saves the text of the element
  - `title.get()` gets the text
- to output the title in scrapy via **css**
  - `title_css = response.css("h1::text")`
  - `title_css` gets the title object. 
  - `title_css.get()` gets the text
  - Be aware that **scrapy transfers the css selectors into xpath**, this means a slight negative impact in performance
- to output array of element via xpath
  - `countries = response.xpath("//td/a/text()").getall()`
  - `countries`
- to ouput array of elements via css
  - `countries_css = response.css("td a::text").getall()`
  - `countries`

## 10. Part 5

- install **python** extension in VS

- to execute the spider:

  ```python
  # countries.py
  
  # -*- coding: utf-8 -*-
  import scrapy
  
  
  class CountriesSpider(scrapy.Spider):
      name = 'countries'
      allowed_domains = ['www.worldometers.info/']
      start_urls = ['https://www.worldometers.info/world-population/population-by-country/']
  
      def parse(self, response):
          title = response.xpath('//h1/text()').get()
          countries = response.xpath('//td/a/text()').getall()
  
          yield {
              'title': title,
              'countries': countries
          }
  ```

- now in terminal with activated wirtual environment

  - `scrapy crawl countries`

- **To activate the environment in the VS Code**

  - Just open vs code and switch python interpreter to conda virtual env
  
- **alternative activation**

  - `source activate workspace_name`

# III. Xpath expressions & CSS Selectors

## 11. Xpath & CSS selectors

- **Xpath** is XML path language to query XML path
- **CSS** - cascading style sheet selectors
- Xpath has the ability to go up and down, but CSS sometimes looks cleaner

## 12. Css selectors fundamentals

- by tag - `h1` 
- by class name - `.intro` 
- by id - `#location`
- only an element that has a certain class - `div.intro`
- select element that has two or more classes - `.bold.italic`
- select element by an attribute - `li[data-identifier='7']` - we can ommit the `li` element
- conditions in css selectors - e.g. only a elements where href starts with https - `a[href^='https']`
- element where attribute ends - `a[href$='fr']`
- element where attribute is in the middle = `a[href*='google']`
- element that are inside -  `div.intro p` - nested elements are not selected though.
- element that are inside including the elements that are inside them - `div.intro p, #location` 
- select all the children - `div.intro > p` 
- select all the p elements that are placed **immediately** after an element - `div.intro + p`
- select first li of unorderer list - `li:nth-child(1)`
- select first and third li of unorderer list - `li:nth-child(1), li:nth-child(3)`
- select all odd / even elements of the list - `li:nth-child(odd)` / `li:nth-child(even)`

## 15. XPath fundamentals

- by tag name - `//h1` 
- element based on the class names - `//div[@class='intro' or @class='outro']/p/text()`
- get href attribute value - `//a/@href`
- get href starting with https - `//a[starts-with(@href, 'https')]`
- get href ending with something - `//a[ends-with(@href, 'fr')]`
  - supporting only in version 2.0 (might not work in chrome)
- search for text in between - `//a[contains(@href, 'google')]` or `//a[contains(text(), 'France')]`
- based on position - `//ul[@id='items']/li[1]`  or `//ul[@id='items']/li/[position() = 1 or position() = last()]` or `//ul[@id='items']/li/[position() > 1]`

## 16. Navigating Up using Xpath

- `//div[@class='intro']/p`
- `//p[@id='unique']/parent::div` - search for parent that is a div
- `//p[@id='unique']/parent::div` - search for any parent
- `//p[@id='unique']/ancestor::node()`- ancestor includes all the ancestors generations
- `//p[@id='unique']/ancestor-or-self::node()` - get self as well
- `//p[@id='unique']/preceding::node()` - all the elements preceding the child excluding the ancestors
- `//p[@id='unique']/preceding::h1` - get h1 preceding the element
- `//p[@id='outside']/preceding-sibling::node()` - get sibling

## 17. Navigating Down using Xpath

- `//div[@class='intro']/p`  or `//div[@class='intro']/child::p`  or `//div[@class='intro']/child:node()` for non specific children.
- `//div[@class='intro']/following::node()` - get all elements after the elements
- `//div[@class='intro']/following-sibling::node()` - get elements with same parent that are siblings after
- `//div[@class='intro']/descendant:node()` - get all descendant elements (opposite of ancestors)    

## 19. Worldometers

- when executing xpath against an object (not a response, we need to have a dot at the beginning)

```python
# -*- coding: utf-8 -*-
import scrapy


class CountriesSpider(scrapy.Spider):
    name = 'countries'
    allowed_domains = ['www.worldometers.info/']
    start_urls = ['https://www.worldometers.info/world-population/population-by-country/']

    def parse(self, response):
        countries = response.xpath("//td/a")

        for country in countries:
            name = country.xpath(".//text()").get()
            link = country.xpath(".//@href").get()
        
            yield {
                'country_name': name,
                'country_link': link
            }
```

## 20. Following Links

```python
# -*- coding: utf-8 -*-
import scrapy


class CountriesSpider(scrapy.Spider):
    name = 'countries'
    allowed_domains = ['www.worldometers.info']
    start_urls = ['https://www.worldometers.info/world-population/population-by-country/']

    def parse(self, response):
        countries = response.xpath("//td/a")

        for country in countries:
            name = country.xpath(".//text()").get()
            link = country.xpath(".//@href").get()
        
            # absolute_url = f"https://www.worldometers.info{link}"
            # absolute_url = response.urljoin(link)

            # yield scrapy.Request(url=absolute_url)

            yield response.follow(url=link)
```

## 21. Pass the response from the link

```python
# -*- coding: utf-8 -*-
import logging
import scrapy


class CountriesSpider(scrapy.Spider):
    name = 'countries'
    allowed_domains = ['www.worldometers.info']
    start_urls = ['https://www.worldometers.info/world-population/population-by-country/']

    def parse(self, response):
        countries = response.xpath("//td/a")

        for country in countries:
            name = country.xpath(".//text()").get()
            link = country.xpath(".//@href").get()

            yield response.follow(url=link, callback=self.parse_country)

    def parse_country(self, response):
        rows = response.xpath('//table[@class="table table-striped table-bordered table-hover table-condensed table-list"][1]/tbody/tr')
        for row in rows:
            year = row.xpath('.//td[1]/text()').get()
            population = row.xpath('.//td[2]/strong/text()').get()
            yield {
                'year': year,
                'population': population
            }
```

## 22. Sync the data between two request methods

```python
# -*- coding: utf-8 -*-
import logging
import scrapy


class CountriesSpider(scrapy.Spider):
    name = 'countries'
    allowed_domains = ['www.worldometers.info']
    start_urls = ['https://www.worldometers.info/world-population/population-by-country/']

    def parse(self, response):
        countries = response.xpath("//td/a")

        for country in countries:
            name = country.xpath(".//text()").get()
            link = country.xpath(".//@href").get()

            yield response.follow(
                url=link, 
                callback=self.parse_country, 
                meta={
                    'country_name': name
                }
            )

    def parse_country(self, response):
        name = response.request.meta['country_name']
        rows = response.xpath('//table[@class="table table-striped table-bordered table-hover table-condensed table-list"][1]/tbody/tr')
        for row in rows:
            year = row.xpath('.//td[1]/text()').get()
            population = row.xpath('.//td[2]/strong/text()').get()
            yield {
                'country_name': name,
                'year': year,
                'population': population
            }
```





# V. Building datasets

- `scrapy crawl countries -o population_dataset.json` 
  - `Alt + Shift + F` - converts the json to more readable format inside VS code
- `scrapy crawl countries -o population_dataset.csv` 
- `scrapy crawl countries -o population_dataset.xml` 

# VI. Dealing With Multiple Pages

- we will use https://web.archive.org/
  - https://web.archive.org/web/20190225123327/https://www.tinydeal.com/specials.html
- before you start a project check robots.txt and make sure the endpoint you're scraping is not listed
- disable javascript to check the website

- to make relative url into absolute

  - ```python
    url = response.urljoin(product.xpath(".//a[@class='p_box_title']/@href").get())
    ```

- to fix encoding problems 

  - go to **settings.py** and add

    ```python
    FEED_EXPORT_ENCODING = 'utf-8'
    ```

## Dealing with pagination

- usually the best way is to check whether next button exists, if it does you can move to the next URL

```python
class SpecialOffersSpider(scrapy.Spider):
    name = 'special_offers'
    allowed_domains = ['www.web.archive.org']
    start_urls = ['https://www.web.archive.org/web/20190225123327/https://www.tinydeal.com/specials.html']

    def parse(self, response):
        for product in response.xpath("//ul[@class='productlisting-ul']/div/li"):
            yield {
                'title': product.xpath(".//a[@class='p_box_title']/text()").get(), 
                'url': response.urljoin(product.xpath(".//a[@class='p_box_title']/@href").get()), 
                'discounted_price': product.xpath(".//div[@class='p_box_price']/span[1]/text()").get(),
                'oritinal_price': product.xpath(".//div[@class='p_box_price']/span[2]/text()").get(), 
            }

        next_page = response.xpath("//a[@class='nextPage']/@href").get()

        if next_page:
            # dont_filter is optional in case of error
            yield scrapy.Request(url=next_page, callback=self.parse, dont_filter=True) 
```

## Spoofing request headers

- use `scrapy shell "https:....html"`

- we have **request** object available

- `request.headers` outputs headers

- `response.request.headers` does the same

  - we get a python dict with **user-agent** property
  - user agent is 'Scrapy' - not a good practice

- to find headers the browser sends

  -  go to the webpage in chrome and open inspector
  - go to **networks** and press `ctrl+R`
  - check the first request you sent and user agent in it
    - `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.90 Safari/537.36`

- **To change headers:**

  - go to **settings.py**
  - there is variable **USER_AGENT**
    - copy the one from the browser and paste it there
  - this might not be the best option if you wanna overwrite multiple headers

- **To overwrite multiple headers**

  - **DEFAULT_REQUEST_HEADERS** dict in **settimgs.py**

- Third way

  - ```python
    # -*- coding: utf-8 -*-
    import scrapy
    
    
    class SpecialOffersSpider(scrapy.Spider):
        name = 'special_offers'
        allowed_domains = ['www.web.archive.org']
    
        def start_requests(self):
            yield scrapy.Request(url="https://www.web.archive.org/web/20190225123327/https://www.tinydeal.com/specials.html", callback=self.parse, headers={
                'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.90 Safari/537.36'
            })
    
        def parse(self, response):
            for product in response.xpath("//ul[@class='productlisting-ul']/div/li"):
                yield {
                    'title': product.xpath(".//a[@class='p_box_title']/text()").get(), 
                    'url': response.urljoin(product.xpath(".//a[@class='p_box_title']/@href").get()), 
                    'discounted_price': product.xpath(".//div[@class='p_box_price']/span[1]/text()").get(),
                    'oritinal_price': product.xpath(".//div[@class='p_box_price']/span[2]/text()").get(), 
                    'User-Agent': response.request.headers['User-Agent']
                }
    
            next_page = response.xpath("//a[@class='nextPage']/@href").get()
    
            if next_page:
                yield scrapy.Request(url=next_page, callback=self.parse, dont_filter=True, headers={
                'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.90 Safari/537.36'
            })
    
    ```



# Debugging Spiders

- bugs can be **logical** or **syntactical**

## Parse Command

- checks the output of the spider 

- `scrapy parse spider_name callbck_method depth item_url` 
  
- **depth** 1 is first website, 2 second website etc
  
- **Scrapy parse**

  - example of an command
    - `scrapy parse --spider=countries -c parse_country --meta='{\"country_name\":\"China\"}' https://www.worldometers.info/world-population/china-population/`

- **Scrapy shell** and **inspect response**

- call with `scrapy crawl countries`

  ```python
  # -*- coding: utf-8 -*-
  import scrapy
  import logging
  from scrapy.shell import inspect_response # ADD IMPORT HERE
  
  class CountriesSpider(scrapy.Spider):
      name = 'countries'
      allowed_domains = ['www.worldometers.info']
      start_urls = ['https://www.worldometers.info/world-population/population-by-country/']
  
      def parse(self, response):
          countries = response.xpath('//td/a')
          for country in countries:
              name = country.xpath('.//text()').get()
              link = country.xpath('.//@href').get()
  
              # absolute_url = f'https://www.worldometers.info{link}' 1. way of using full urls
              # absolute_url = response.urljoin(link) 2. way of using full urls
  
              yield response.follow(url=link, callback=self.parse_country, meta={'country_name': name}) # 3. way of using full urls
  
      def parse_country(self, response):
          inspect_response(response, self)  # COMMENT OUT THE LOGIC. THE SPIDER HAS TO BE SET AS A SECOND ARGUMENT
          # name = response.request.meta['country_name']
          # rows = response.xpath("(//table[@class='table table-striped table-bordered table-hover table-condensed table-list'])[1]/tbody/tr")
          # for row in rows:
          #     year = row.xpath('.//td[1]/text()').get()
          #     population = row.xpath('.//td[2]/strong/text()').get()
          #     yield {
          #         'country_name':name,
          #         'year': year,
          #         'population': population
          #     }
  
          #     # scrapy parse --spider=countries -c parse_country --meta='{\"country_name\":\"China\"}' https://www.worldometers.info/world-population/china-population/
  ```

  - `request.headers` checks headers
  - `response.body` checks body
  - `view(response)` opens the response in the browser

- **To open in browser**

- call with `scrapy crawl countries`

```python
# -*- coding: utf-8 -*-
import scrapy
import logging
from scrapy.utils.response import open_in_browser # IMPORT THE OBJECT

class CountriesSpider(scrapy.Spider):
    name = 'countries'
    allowed_domains = ['www.worldometers.info']
    start_urls = ['https://www.worldometers.info/world-population/population-by-country/']

    def parse(self, response):  # Adjust here
        # countries = response.xpath('//td/a')
        # for country in countries:
        #     name = country.xpath('.//text()').get()
        #     link = country.xpath('.//@href').get()

            # absolute_url = f'https://www.worldometers.info{link}' 1. way of using full urls
            # absolute_url = response.urljoin(link) 2. way of using full urls

        yield response.follow(url="https://www.worldometers.info/world-population/china-population/", callback=self.parse_country, meta={'country_name': "China"}) # 3. way of using full urls

    def parse_country(self, response):
        open_in_browser(response)
        # name = response.request.meta['country_name']
        # rows = response.xpath("(//table[@class='table table-striped table-bordered table-hover table-condensed table-list'])[1]/tbody/tr")
        # for row in rows:
        #     year = row.xpath('.//td[1]/text()').get()
        #     population = row.xpath('.//td[2]/strong/text()').get()
        #     yield {
        #         'country_name':name,
        #         'year': year,
        #         'population': population
        #     }

        #     # scrapy parse --spider=countries -c parse_country --meta='{\"country_name\":\"China\"}' https://www.worldometers.info/world-population/china-population/
```

- response gets open in browser

- **Using logging module**

  ```python
  # -*- coding: utf-8 -*-
  import scrapy
  import logging
  
  class CountriesSpider(scrapy.Spider):
      name = 'countries'
      allowed_domains = ['www.worldometers.info']
      start_urls = ['https://www.worldometers.info/world-population/population-by-country/']
  
      def parse(self, response):
          # countries = response.xpath('//td/a')
          # for country in countries:
          #     name = country.xpath('.//text()').get()
          #     link = country.xpath('.//@href').get()
  
              # absolute_url = f'https://www.worldometers.info{link}' 1. way of using full urls
              # absolute_url = response.urljoin(link) 2. way of using full urls
  
          yield response.follow(url="https://www.worldometers.info/world-population/china-population/", callback=self.parse_country, meta={'country_name': "China"}) # 3. way of using full urls
  
      def parse_country(self, response):
          logging.warning(response.status)
          # name = response.request.meta['country_name']
          # rows = response.xpath("(//table[@class='table table-striped table-bordered table-hover table-condensed table-list'])[1]/tbody/tr")
          # for row in rows:
          #     year = row.xpath('.//td[1]/text()').get()
          #     population = row.xpath('.//td[2]/strong/text()').get()
          #     yield {
          #         'country_name':name,
          #         'year': year,
          #         'population': population
          #     }
  
          #     # scrapy parse --spider=countries -c parse_country --meta='{\"country_name\":\"China\"}' https://www.worldometers.info/world-population/china-population/
  ```

  

## Debugging with debug

- within a root directory create a **runner.py** file

  ```python
  import scrapy
  from scrapy.crawler import CrawlerProcess
  from scrapy.utils.project import get_project_settings
  from worldometers.spiders.countries import CountriesSpider
  
  process = CrawlerProcess(settings=get_project_settings())
  process.crawl(CountriesSpider)
  process.start()
  ```

- place the stop in the spider

- debug **runner.py** as a python file

  - can place watcher variables if you want

# Taking a break

## whys and whens

- scraping usually used for data analysis or machine learning
- lead generation
- real estate listings
- price monitoring
- stock market tracking
- drop shipping - **this is super interesting!** - you basically scrape amazon and put a markup and resel
- when to use/not use web scraping
  - **robots.txt**
  - **does the website have a public API?**
    - some websites limit the nunber of requests
  - **does the API have any limitations?**
  - **is the API free/paid?**

## Web scraping challenges

- **stability and maintanence of the spider**
  - if website changes UI you can break selectors - e.g. adding javascript
  - the spider might not work tomorrow

# Crawl Spider Structure

- the basic template is the default when creating a spider
- `scrapy genspider -l` puts out all the available templates
  - **basic**
  - **crawl**
  - **csvfeed** - no that common. used to scrape csv files
  - **xmlfeed** - used to scrape xml documents
- `scrapy genspider -t crawl best_movies imdb.com` generates the spider

## The rule object

```python
# -*- coding: utf-8 -*-
import scrapy
from scrapy.linkextractors import LinkExtractor
from scrapy.spiders import CrawlSpider, Rule


class BestMoviesSpider(CrawlSpider):
    name = 'best_movies'
    allowed_domains = ['imdb.com']
    start_urls = ['http://imdb.com/']

    rules = (
        Rule(LinkExtractor(restrict_css=('//a[@class="active"]')), callback='parse_item', follow=True),
    )

    def parse_item(self, response):
        item = {}
        #item['domain_id'] = response.xpath('//input[@id="sid"]/@value').get()
        #item['name'] = response.xpath('//div[@id="name"]').get()
        #item['description'] = response.xpath('//div[@id="description"]').get()
        return item
```

- If you need to  **normalize space** around the element text just use 

  ```python
  'duration': response.xpath("normalize-space((//time)[1]/text())").get(),
  ```

## Following links in pagination

```python
# -*- coding: utf-8 -*-
import scrapy
from scrapy.linkextractors import LinkExtractor
from scrapy.spiders import CrawlSpider, Rule


class BestMoviesSpider(CrawlSpider):
    name = 'best_movies'
    allowed_domains = ['imdb.com']
    start_urls = ['https://www.imdb.com/chart/top/']

    rules = (
        Rule(LinkExtractor(restrict_xpaths="//td[@class='titleColumn']/a"), callback='parse_item', follow=True),
        Rule(LinkExtractor(restrict_xpaths="(//a[@class-'lister-page-next next-page'])[2]"))
    )

    def parse_item(self, response):
        yield {
            'title': response.xpath("//div[@class='title_wrapper']/h1/text()").get(),
            'year': response.xpath("//span[@id='titleYear']/a/text()").get(),
            'duration': response.xpath("normalize-space((//time)[1]/text())").get(),
            'genre': response.xpath("//div[@class='subtext']/a/text()").get(),
            'rating': response.xpath("//span[@itemprop='ratingValue']/text()").get(),
            'movie_url': response.url
        }
```

# Spoofing request headers with Crawl spider

- in **settings**

  - assigning **USER_AGENT** variable

- for multiple headers in **settings**

  - assigning **DEFAULT_REQUEST_HEADERS** variable

- in the **spider itself**

  - in google you can enter *My user agent* and youll get *Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36*

  - we need to overwrite **start_requests** method

    ```python
    # -*- coding: utf-8 -*-
    import scrapy
    from scrapy.linkextractors import LinkExtractor
    from scrapy.spiders import CrawlSpider, Rule
    
    
    class BestMoviesSpider(CrawlSpider):
        name = 'best_movies'
        allowed_domains = ['imdb.com']
    
        user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/89.0.4389.114 Safari/537.36"
    
        def start_request(self):
            yield scrapy.Request(
                url='https://www.imdb.com/chart/top/', 
                headers={'User-Agent': self.user_agent}
            )
    
        rules = (
            Rule(LinkExtractor(restrict_xpaths="//td[@class='titleColumn']/a"), callback='parse_item', follow=True, process_request='set_user_agent'),
            Rule(LinkExtractor(restrict_xpaths="(//a[@class-'lister-page-next next-page'])[2]"), process_request='set_user_agent')
        )
    
        def set_user_agent(self, request):
            request.headers['User-Agent'] = self.user_agent
            return request
    
        def parse_item(self, response):
            yield {
                'title': response.xpath("//div[@class='title_wrapper']/h1/text()").get(),
                'year': response.xpath("//span[@id='titleYear']/a/text()").get(),
                'duration': response.xpath("normalize-space((//time)[1]/text())").get(),
                'genre': response.xpath("//div[@class='subtext']/a/text()").get(),
                'rating': response.xpath("//span[@itemprop='ratingValue']/text()").get(),
                'movie_url': response.url,
                'user-agent': response.request.header['User-Agent']
            }
    ```

# Splash Crash Course

## What does Splash solve?

- websites using JavaScript
- its meant to be used with scrapy
- What about selenium?
  - not development for webscraping
  - more beginner friendly
- **Engines**
  - Chrome has V8 engine
  - FF has spiderMonkey
  - Safari has Apple Webkit
  - MS has Chakra

## Setting up Splash 

- has video for pro / enterprise, skipping ig
- **windows home edition**
  - has to be 64-bit
  - search for `windows features on / off`
  - disable **hyper-v** and reboot
- install **docker toolbox**
  - https://hub.docker.com/editions/community/docker-ce-desktop-windows/
  - follow instructions to install splash
  - run at `http://localhost:8050/` 


​    

  