# OWASP Maryam - Project Proposal

## Personal information

### Contact Information

* Student name: Prakhar Jain
* Email(s): prakharalt@gmail.com
* Personal Website/Blog: https://www.prakharj.me/
* Slack: Prakhar Jain
* GitHub: https://github.com/prakhar-ai
* Twitter: https://twitter.com/prakharj2000
* LinkedIn: https://www.linkedin.com/in/prakhar-j/

### Student affiliation

**Institute of Technology, Nirma University**

*Computer Science and Engineering (Bachelor’s)*

6th semester, 2022 (expected graduation)

### Brief bio

I am hooked to open-source software development, an ambitious outgrowth of my
personal interests to create [free](https://www.gnu.org/philosophy/free-sw.html) and
[open-source](http://c2.com/cgi/wiki?OpenSource) content.

* I like to write [technical blogs](https://www.prakharj.me/posts/) and [projects](https://www.prakharj.me/projects/).
* I love to participate in Hackathons. Two of my Projects have won Hackathons - [JASPER](https://devpost.com/software/jasper) and [InstantMD](https://github.com/prakhar-ai/InstantMD).
* I enjoy making [open-source projects](https://github.com/prakhar-ai/npa) for my university.

I use [GNU/Linux](https://www.debian.org/releases/squeeze/i386/ch01s02.html.en)
(Ubuntu 20.04.2), keep files under [version control](https://git-scm.com/), and edit using
[VSCode](https://code.visualstudio.com/).

Further information and details of my general interests can be found on my
[blog](https://www.prakharj.me/).


## Background

I'm a Python Developer and use it to develop most of my [projects](https://github.com/prakhar-ai?tab=repositories). I also have knowledge of OS, Object-Oriented Programming and Web Programming as listed in the Knowledge Prerequisites of the project.

### Prior Contributions
* Contributed to the [Maryam](https://github.com/saeeddhqan/Maryam) project by [updating](https://github.com/saeeddhqan/Maryam/pull/104) new search modules
* Contributed to OWASP projects like [Threat Dragon](https://github.com/OWASP/threat-dragon) by adding a [ZAP Scan](https://github.com/OWASP/threat-dragon/pull/48)
* An extensive list of my contributions can be found on my [GitHub](https://github.com/prakhar-ai) profile.

I've always found OSINT projects very interesting and I chose this project since I believe that I perfectly match the requirements for the project. I have a development environment set up for the project and have studied all the modules in detail. I have also contributed to it leading up to the Application Period.

## My Proposal

### Current State
<p align="center">
	<img width="600" height="600" src="https://svgshare.com/i/VX4.svg">
</p>
<p align="center"><i>Fig 1. All modules in Maryam currently</i></p>


OWASP Maryam is a modular/optional open source framework based on OSINT and data gathering. Maryam is written in Python programming language and it’s designed to provide a powerful environment to harvest data from open sources and search engines and collect data quickly and thoroughly.<sup>[[1]](https://github.com/saeeddhqan/Maryam#owasp-maryam)</sup>


### Project proposal

Essentially, the different objectives (or components) are as follows:

-----

#### Adding and Updating Modules

* **New util classes**: As mentioned in issue [#105](https://github.com/saeeddhqan/Maryam/issues/105), 
    the program currently lacks several important util classes (`core/util`)
    for websites like Facebook, Twitter, Instagram, LinkedIn etc. These classes
    would be useful in the search modules as well as other OSINT modules. 
  
Here is an example util class taken from the project [wiki](https://github.com/saeeddhqan/Maryam/wiki/Development-Guide#make-a-util-class)
which can be used as reference.

```python
class main:

	def __init__(self, q, limit=2):
		""" ask.com search engine

			q 		  : query for search
			limit	  : count of pages
		"""
		self.framework = main.framework
		self.q = self.framework.urlib(q).quote
		self.limit = limit
		self._pages = ''
		self.ask = 'www.ask.com'

	def run_crawl(self):
		urls = [f"https://{self.ask}/web?q={self.q}&page={i}" for i in range(1, self.limit+1)]
		max_attempt = len(urls)
		for url in range(len(urls)):
			self.framework.verbose(f"[ASK] Searching in {url} page...")
			try:
				req = self.framework.request(url=urls[url])
			except:
				self.framework.error('[ASK] ConnectionError')
				max_attempt -= 1
				if max_attempt == 0:
					self.framework.error('Ask is missed!')
					break
			else:
				page = req.text
				if '>Next</li>' not in page:
					self._pages += page
					break
				self._pages += page

	@property
	def pages(self):
		return self._pages

	@property
	def dns(self):
		return self.framework.page_parse(self._pages).get_dns(self.q)

	@property
	def emails(self):
		return self.framework.page_parse(self._pages).get_emails(self.q)

	@property
	def docs(self):
		return self.framework.page_parse(self._pages).get_docs(self.q)
 ```
For **Twitter**, the [twint](https://github.com/twintproject/twint) library can be used, which works without using the official Twitter API

```python
import twint

# Configure
c = twint.Config()
c.Username = "realDonaldTrump"
c.Search = "great"

# Run
twint.run.Search(c)

```

<p align="center">
	<img width="400" height="400" src="https://svgshare.com/i/VXb.svg">
</p>

<p align="center"><i>Fig 2. Features in the Twitter util class</i></p>

an extensive guide for using the twint module for OSINT can be found [here](https://pielco11.ovh/posts/twint-osint/)

Similarly util classes can be built for **Facebook** and **LinkedIn** 


-----


* **Updating search modules**: Search modules need to be updated by adding source sites directly along with search engines. (Refer PR [#104](https://github.com/saeeddhqan/Maryam/pull/104))

Many modules like the **StackOverflow** module(`modules/search/stackoverflow.py`) are outdated and do not display usernames and tags. I intend to update them
as part of my proposal.

Sources can also be queried directly using

```
https://stackoverflow.com/search?q='query'
```

Similarly for the TikTok (`modules/search/tiktok.py`) module,

```
https://www.tiktok.com/search?q='query'
```
New Search modules can be added,

<p align="center">
	<img width="350" height="350" src="https://svgshare.com/i/VWF.svg">
</p>
<p align="center"><i>Fig 3. Additional Search modules that can be added</i></p>


----


* **Testing and Fixing Bugs**: Leading up to the application period, I found some bugs in the search modules, some of which I have fixed. I plan to continue testing other modules and fixing bugs throughout the program.

----

* **Adding ML and NLP Modules**: We can use NLP and keyword extraction from a Twitter Profile, accounts most interacted with. This can be done on Reddit, Twitter etc. We could use the [yake](https://github.com/LIAAD/yake) library to extract keywords. 

```python

import yake

text = "Sample text for keyword extraction in the NLP Module"

kw_extractor = yake.KeywordExtractor()
keywords = kw_extractor.extract_keywords(text)

for kw in keywords:
	print(kw)
```
----

#### Working on Web Interface

* **Improving Frontend UI**: UI Frameworks like [Semantic UI](https://semantic-ui.com/) can be used to improve the UI/UX of the web application. Semantic UI 
			     provides us with built-in classes like `ui inverted table` and `ui selection dropdown` which can be integrated into our Web 
			     framework. A sidebar can be created using the `sidebar menu` class as seen in Fig 3

```python
        <table class="ui selectable inverted table">
            <thead>
              <tr>
                <th class="ten wide">Type</th>
                <th class="ten wide">Modules</th>
                <th class="ten wide">Target</th>
                <th class="right aligned ten wide">Results</th>
              </tr>
            </thead>
	    .....
                <td><div class="ui selection dropdown">
                    <input type="hidden">
                    <i class="dropdown icon"></i>
                    <div class="default text">Select Target</div>
                  </div></td>
                <td></td>
              </tr>
            </tbody>
          </table>
```


* **Adding Animated Graphs**: Using the [amcharts](https://www.amcharts.com/) library, we can add better looking visualisations to our web interface


<p align="center">
	<img src="https://s4.gifyu.com/images/web-interface.gif">
</p>
<p align="center"><i>Fig 4. Web Interface using Semantic UI and amcharts</i></p>

### SAT Questions

`What makes you suited to carry the project?`

I have a lot of experience with Python, Web Scraping and building Web Applications using Flask. This skills would be required in expanding the project which makes me suited for the project. I've also previously contributed to it and understand all underlying modules

`If you have chosen an idea from our list, why did you choose this specific idea?`

I've always found OSINT projects very interesting and I chose this project since I believe that I perfectly match the requirements for the project.

`How much time do you plan to invest in the project before, during and after the Summer of Code?`

I plan to invest 4-5 hours everyday during the coding period. I will also interact and discuss ideas during the Community bonding period for a few hours everyday. I intend to continue contributing to the project after Summer of Code, since I'm truly passionate about it.

### Timeline (tentative)



*Through the coding period, emphasis is on creating well documented and tested
code. For this, one may commit frequently (with verbose messages), follow
a test-driven development style and use continuous integration services.*

**Community bonding period**

Spend time interacting with community members and learn more about Maryam and
its broader vision. The period can also be used to further refine, discuss and
plan the components of proposal which are not very clear.

Also, help plan out roadmap, create/fix minor issues and familiarize myself with
the codebase.

**Week 1 - Week 2**

* Discuss the design of the new util and search modules
* Start work on the additional util classes
* Bi-weekly summary

**Week 3 - Week 4**

* Work on building the new modules
* Discuss and design ML and NLP implementation in the project
* Start designing the Web UI
* Bi-weekly summary

**Week 5 - Week 6**

* Work on the Web UI and charts
* Thoroughly test the new modules, see if the implemented with good accuracy.
* Bi-weekly summary

*Mid term evaluations*

**Week 7 - Week 8**

* Test all the changes so far. If something is not working properly, fix it
    before moving on to other parts.
* Complete the Web UI
* Bi-weekly summary


**Week 9 - Week 10**

*Week to scrub code, write tests, focus on documentation.*

*End term evaluations*


## Mentors

[Saeed Dehqan](https://github.com/saeeddhqan)

