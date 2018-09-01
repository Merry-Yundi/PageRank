# Simple Python Search Spider, Page Ranker, and Visualizer
Environment:  
MacOS 10.13    
Python 3.6.4   
[SQLite browser](http://sqlitebrowser.org/)

**Introduction**

This is a set of programs that emulate some of the functions of a search engine. I crawl a main website and sepcific number of websites linked in this main website and calculates the page ranks for each website.

**Page Rank Diagram:**

![Page Rank Diagram](https://github.com/Merry-Yundi/PageRank/blob/master/Pagerank.jpg 'Page Rank Diagram')



+ Crawl a certain number of pages as you want from [an example web site](http://www.xuetangx.com/) and store data in SQLite databse by running `spider.py`.  

+ Dump the contents of the spider.sqlite file by running `spdump.py` if you want.   

+ Calculate page rank of each page you have crawled by running `sprank.py` as many times as you like and increasing iterations to refine the page rank.  

+ Use `spreset.py` to restart the Page Rank calculations without re-spidering the web pages. 

+ Visualize the current top pages in terms of page rank by running `spjson.py` to write the pages out in JSON format to be viewed in a web browser.  

+ Open `force.html` in a browser to view the [visualization](http://marui.space/e63q), showing an automatic layout of the nodes and links. 

+ Click and drag any node as you like and double click on a node to find the URL that is represented by the node.  

+ This visualization is provided using the [force layout](http://mbostock.github.com/d3/). 

**Final Visualized Result:**

![Visualization](https://github.com/Merry-Yundi/PageRank/blob/master/PageRank_Visualization.png 'visualization')

[**Algorithms from Wikipedia**](https://en.wikipedia.org/wiki/PageRank)


