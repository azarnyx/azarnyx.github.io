---
layout: post
title:  "Web of Science data parser"
categories: scripts python
tags: python scholar script
---
{% include JB/setup %}
Back in 2011 I have started my PhD in Technical University of Munich. During my first years lots of my acquaintances asked me for an advice in searching PhD positions in EU and US as well as what are the best chairs to apply. Though I learned about the best chairs and Universities in Aerodynamics and related fields, I had no idea what to recommend to people who wanted to apply for a PhD position, say, in Chemistry. Still, I wanted to help. I searched for a ranking, which gives you the best people to supervise PhD in the choosen field and did not find any. 

So together with my friend, we thought how to create such a ranking. The best idea which came to our minds is to sort people by the number of publications for the last 10-15 years in the chosen field. Such a criterion was imposed due to the idea, that if somebody is so highly productive and publishes a large amount of papers, then it would be easier for new PhD students to publish and to graduate with a PhD degree in the field of their interest. In this sense the number of publications might be more representative, rather than h-index. The criteria of the most numbers of publications might not be accurate to define the true ranking who is the best in the field. After all, they have Nobel prize, Fields medal, Abel prize for such purposes. But the ranking based on the number of publications gives top 10-30 people in the field to supervise PhD thesis. Usually such highly productive people are heads of chairs, where the graduate student can apply. 

We used the [web-of-science database][ws] and wrote a small [script in Python][ga]. On the [web-of-science search tool][ws] one can set different types of filters, such as choosing location, field and years of publications.

![](https://azarnyx.github.io/pic/wos.png )


The search results could be downlowded in txt files. The inconvinience
is due to WoS allow to download up to 500 records at once, so to search through
10000 different publications one needs to press download button 20
times.

![](https://azarnyx.github.io/pic/wos_save.png)

After results are stored in the folder `FOLDER`, just simply type in command line:

{% highlight shell %}
:~$ git clone https://github.com/azarnyx/parse.py
:~$ cd parse.py
:~$ python parse.py -d /Path/To/FOLDER
{% endhighlight %}

So I use the script to estimate top-20 people published the most papers that satisfies query "Machine Learning" for 2000-2016 years. I searched through 10000 most cited papers from Web of Science search tool. Here is the result:


| Place 	| Name 	| # Publications 	|
| :------: | :---------: | :---------:|
|1. | Herrera, Francisco | 35|
|2. | Huang, Guang-Bin | 28|
|3. | Mueller, Klaus-Robert | 24|
|4. | Zhou, Zhi-Hua | 20|
|5. | Wang, Ji-Bo | 17|
|6. | Fernandez, Alberto | 17|
|7. | Scholkopf, B | 17|
|8. | Jennings, NR | 17|
|9. | Staab, S | 17|
|10. | Bruzzone, Lorenzo | 16|
|11. | Pedrycz, Witold | 16|
|12. | Herrera, F | 16|
|13. | Blankertz, Benjamin | 15|
|14. | Polat, Kemal | 15|
|15. | Hu, Qinghua | 14|
|16. | Suykens, JAK | 14|
|17. | Fan, BT | 14|
|18. | Han, JW | 14|
|19. | Wooldridge, M | 14|
|20. | Hu, ZD | 13|

The alternative to [Web Of Science database][ws] is to use
[Google Scholar][gs] database or [PubMed][pm]. Pubmed is mostly
related with medical science publications and is not suitable for the
wide range of disciplines. Google Scholar search does not provide a
convinient way to download database of publications. However, it is
possible to use Google Scholar search to get database with the
[other parsing script][gp] after some modifications. Script with
modifications will be available soon at
[`https://github.com/azarnyx/parse.py`][ga]. Though, Google Scholar
search output is restricted to 1000 articles, which might not be
representative.

Interestingly, that nowadays such a search available directly on the
Web Of Science search with `Analyze Results` button, however it
searches through all results rather than through 10000 most cited
results as was used so it gave somehow different output:

![alt text](https://azarnyx.github.io/pic/wos_ml.png "Logo Title Text 1")

The WoS output still could be modified by accurate setting of filters.

[gp]: https://github.com/ckreibich/scholar.py
[gs]: http://scholar.google.com/
[pm]: https://www.ncbi.nlm.nih.gov/
[ws]: http://apps.webofknowledge.com/WOS_GeneralSearch_input.do?product=WOS&search_mode=GeneralSearch&SID=N16nzS1stow8xb3y9A4&preferencesSaved=
[ga]: https://github.com/azarnyx/parse.py
