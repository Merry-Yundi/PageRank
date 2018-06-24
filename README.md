# Simple Python Search Spider, Page Ranker, and Visualizer

This is a set of programs that emulate some of the functions of a search engine.

We store their data in a SQLITE3 database named 'spider.sqlite'.

This file can be removed at any time to restart the process.

First install the SQLite browser to view and modify the databases from: http://sqlitebrowser.org/

This program crawls a web site and pulls a series of pages into the database, recording the links between pages.

Note: Windows has difficulty in displaying UTF-8 characters in the console so for each console window you open, you may need to type the following command before running this code: chcp 65001

http://stackoverflow.com/questions/388490/unicode-characters-in-windows-command-line-how

Mac: rm spider.sqlite

Mac: python3 spider.py

Win: del spider.sqlite

Win: spider.py

Enter web url or enter: http://www.xuetangx.com/

['http://www.xuetangx.com/']

How many pages:100

1 http://www.xuetangx.com (32958) 27
13 http://www.xuetangx.com/courses?cid=119 (77145) 96
57 http://www.xuetangx.com/courses?credential=0&page_type=0&cid=119&process=0&org=33&course_mode=0 (35240) 58
31 http://www.xuetangx.com/courses?credential=0&page_type=0&cid=120&process=0&org=0&course_mode=0 (73505) 96
...
How many pages:

In this sample run, we told it to crawl a website and retrieve 100 pages.

If you restart the program again and tell it to crawl more pages, it will not re-crawl any pages already in the database.

Upon restart it goes to a random non-crawled page and starts there.

So each successive run of spider.py is additive.

You can have multiple starting points in the same database - within the program these are called "webs".

The spider chooses randomly amongst all non-visited links across all the webs.

If you want to dump the contents of the spider.sqlite file, you can run spdump.py as follows:

Mac: python3 spdump.py

Win: spdump.py

(198, 20.006653638381028, 20.006653638381028, 1, 'http://www.xuetangx.com')
(143, 18.18786694398275, 18.18786694398275, 13, 'http://www.xuetangx.com/courses?cid=119')
(12, 3.420377887206523, 3.420377887206523, 63, 'http://www.xuetangx.com/courses?credential=0&page_type=0&cid=119&process=0&org=51&course_mode=0')
...
100 rows.

This shows the number of incoming links, the old page rank, the new page rank, the id of the page, and the url of the page.

The spdump.py program only shows pages that have at least one incoming link to them.

Once you have a few pages in the database, you can run Page Rank on the pages using the sprank.py program.

You simply tell it how many Page Rank iterations to run.

Mac: python3 sprank.py
Win: sprank.py

How many iterations:100
1 0.00040304240606917193
2 0.000202882239109336
3 0.00010140982372411931
4 5.383817683170076e-05
5 3.170151772656087e-05
6 1.886542562824157e-05
7 1.0479046819882412e-05
8 6.194637833348996e-06
9 3.4951065966985913e-06
10 2.085839157584034e-06
...
[(1, 20.006653638381028), (24, 5.001663409595257),(13, 18.18786694398275), (63, 3.420377887206523), (33, 1.6672211365317524)]


You can run sprank.py as many times as you like and it will simply refine the page rank the more times you run it.

You can even run sprank.py a few times and then go spider a few more pages sith spider.py and then run sprank.py to converge the page ranks.

If you want to restart the Page Rank calculations without re-spidering the web pages, you can use spreset.py

Mac: python3 spreset.py

Win: spreset.py

All pages set to a rank of 1.0

Mac: python3 sprank.py

Win: sprank.py

How many iterations:50
1 0.546848992536
2 0.226714939664
3 0.0659516187242
4 0.0244199333
5 0.0102096489546
6 0.00610244329379
...
42 0.000109076928206
43 9.91987599002e-05
44 9.02151706798e-05
45 8.20451504471e-05
46 7.46150183837e-05
47 6.7857770908e-05
48 6.17124694224e-05
49 5.61236959327e-05
50 5.10410499467e-05

[(512, 0.02963718031139026), (1, 12.790786721866658),(2, 28.939418898678284), (3, 6.808468390725946), (4, 13.469889092397006)]

For each iteration of the page rank algorithm it prints the average change per page of the page rank

The network initially is quite unbalanced and so the individual page ranks are changing wildly.

But in a few short iterations, the page rank converges.

You should run prank.py long enough that the page ranks converge.

If you want to visualize the current top pages in terms of page rank, run spjson.py to write the pages out in JSON format to be viewed in a web browser.

Mac: python3 spjson.py
Win: spjson.py

Creating JSON output on spider.js...

How many nodes? 100

Open force.html in a browser to view the visualization

You can view this data by opening the file force.html in your web browser.

This shows an automatic layout of the nodes and links.

You can click and drag any node and you can also double click on a node to find the URL that is represented by the node.

This visualization is provided using the force layout from:

http://mbostock.github.com/d3/

If you rerun the other utilities and then re-run spjson.py -you merely have to press refresh in the browser to get the new data from spider.js.
