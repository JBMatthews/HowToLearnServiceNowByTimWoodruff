# How to Learn ServiceNow
This comes from the incredible article provided by Tim Woodruff on The SN Guys website. I decided to go through it myself, to see what I could learn and how I might put it into better bit-sized pieces. 

Link: [How to Learn ServiceNow](https://snprotips.com/blog/2018/10/20/how-to-learn-servicenow)
[Tim Woodruff](https://snprotips.com/?author=56709603dc5cb4b3239718bb)

Hello, future ServiceNow developer! - I'm [**Tim Woodruff**](https://timothywoodruff.com/); founder of [**The SN Guys**](https://snprotips.com/contact-us). I write most of the articles on this site ([**SN Pro Tips**](https://snprotips.com/archive)), and I’m the author of a few [**books**](https://books.snc.guru/) on ServiceNow development, architecture, and administration, including [**Learning ServiceNow**](https://lsn.snc.guru/), and [**The ServiceNow Development Handbook**](https://handbook.snc.guru/).  
I've put together this **quick-start guide to learning ServiceNow development**, as a sort of map or check-list for going “from zero to credible” when you’re starting out your career as a ServiceNow developer.

> Speaking of careers, don’t forget to check out my article on [**ServiceNow development as a career**](https://career.snc.guru/), which will help you get a sense of what to expect, how to build your resume, and how to market yourself as a ServiceNow developer (among other things).

This article is not meant to actually teach you to be a ServiceNow developer (it’s far too short for that). Instead, it's meant to be something you can reference when you find yourself thinking "Okay, what next?" on your journey to becoming a credible expert. In each section, I outline a few **key points** that you should look for, and pay special attention to. These are tidbits of knowledge that will help you out in your ServiceNow development career, or help you understand some concept about how SN works more deeply and intuitively. **I don't recommend skipping around to learn those specific topics**, but once you've done a bit of research (such as reading a book) on one of the topics mentioned, go back and review the list of concepts for anything you may have missed, and _then_ research those points specifically.

> **_Note_**_: If you want to keep up-to-date on my articles and books, you can_ [**_subscribe to SN Pro Tips_**](https://snprotips.com/subscribe/)_.  
> You can also follow me on Twitter at_ [**_@TheTimWoodruff_**](https://twitter.com/TheTimWoodruff)_, and connect with me on_ [**_LinkedIn_**](https://www.linkedin.com/in/sn-timw/)_._ 

---

# **Relational databases**

Understanding relational databases _fully_ is not necessary to get started (it's not _too_ tough to pick up along the way), but I **_strongly_** recommend that you acquire a solid understanding of the basic **data-structures**, types of **relationships**, and **data-types** you'll run into in relational databases. This will help you understand how ServiceNow stores and correlates data (including **database records** like Incident tickets or [attachment](http://attachments.snc.guru/) files).

Having a vague, surface-level understanding of the SQL query language syntax under your belt would also be helpful in understanding some of the high-level _and_ low-level functionality in ServiceNow, since it is - at its core - largely a big relational database with functional “sugar” on top.

## **What to know**

Here are some basic concepts that would be helpful to be aware of: 

- What is the difference between a field or table **label**, and a field/table **name**
    
- What is a **primary key** (PK)
    
    - In ServiceNow, the PK for (_almost_) _all records in all tables_, is a column (or "field") labeled **Sys ID** with the column _name_ "**sys_id**"
        
- What is a **foreign key** (FK)
    
    - “Foreign key” fields in ServiceNow, are usually called **Reference** fields - though there are other "types" of fields (aside from reference fields) which can hold one or multiple FKs
        
- How are records related to one another
    
    (hint: Using an FK is one way to relate records to one another, but not the only way!) 
    
    - **One-to-many** relationships
        
        (This typically uses an FK column)
        
        - Understand what constitutes "parent" versus "child" in these relationship types
            
    - **Many-to-many** relationships
        
        - Using an **m2m** table, versus using a FK field which supports multiple FKs on two tables (or on the same table - records can reference other records in the same table)
            
    - **One-to-one** relationships (How can these be enforced?)
        
        (Note: These are not easy to enforce without some kind of logical underpinning, but it's a good idea to think about them and how they could be maintained.)
        
        - When are one-to-one relationships necessary?
            
            (Hint: _rarely_. Often if you have a 1-to-1 relationship, data from both records in the relationship should be in a single record rather than split across two - but not always. One example of an exception would be the CMDB and Asset tables which have a one-to-one relationship enforced by multiple “Business Rules”, but you’ll learn about that much later!)
            
- Queries (Don't worry too much about _syntax_, but think about how they _work_.)
    
    - **Dot-walking** - querying based on data in an FK (reference) field
        
    - Query **efficiency** - If querying a table with a few million records, what are some basic things you can do to make your queries not make the database cry? 
        
        - Again, think about _functionality_, not _syntax_.
            
    - "AND" vs "OR" and logical operators: (=, !=, IN, LIKE, etc.)
        
    - "Join" queries (though you can pick this up later if it seems a bit arcane for right now)
        

## **Resources**

- [This video](https://www.youtube.com/watch?v=NvrpuBAMddw) introduces the basics of relational databases. 
    
- Here's a super-brief [crash course](https://www.webucator.com/tutorial/learn-sql/relational-database-basics.cfm) for a bit of light reading
    
- To learn a bit more in-depth, [Database Design for Mere Mortals](https://amzn.to/2M3HBP1) is a great book.



| TOPIC                                                                                                          | LEARNINGS                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Attachments<br>[GlideAttachment](https://snprotips.com/blog/2016/2/25/understanding-and-using-glideattachment) | There are two table in ServiceNow that control attachments. <br>1. Attachments (sys_attachment) <br>2. Attachments Documents (sys_attachment_doc). <br><br>Attachments is the Parent table where the record of the attachment itself is stored. But, the binary data is split of and stored on the Attachments Documents table. <br>Fields on the doc table include: <br>- Data (ID to the data chunk itself)<br>- Length (The length of the data)<br>- Position (The positioning of the chunk for when the attachment is recalled and SN must reconfigure the file.)<br>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| What is the difference between a field or table label, and a field/table name?                                 | Think about a jar full of pennies. On the outside of the jar you have a "Label" that reads "pennies." You don't tape a penny to the outside of the penny jar, you place a label on it. Maybe sometime later you decide to change the label to "piggy bank," but the pennies don't change. Table in a Relational DB use this same functionality.<br>LABEL ---> "Piggy Bank"<br>NAME  ---> "coin_penny"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| What is a **primary key** (PK)?                                                                                | In a Relational Database a PK doesn't stand for "pastor's kids," it stands for Primary Key, and it serves as a unique identifier for each record in a table.<br>ServiceNow:<br>Primary Key (PK) ---> Sys ID (GUIDs)<br><br>Something cool to note: <br>Why does SN use strings instead of numbers?<br>ServiceNow runs on Oracle, and supports global data replication (multi-instances, cloned environment, etc.). If every table simply used numbers 1, 2, 3..., dups would constantly appear across systems. <br>So, SN utilizes GUIDs (Globally Unique Identifiers) - long strings of numbers and letters, that guarantee unique identify across different instances.<br>Compare the license plate number for a car, versus a number ticketing dispenser at a Bakery.<br>License Plate System:<br>Car, Make, Color, State, Number<br>You can drive not only around town but also around other states and by assured you have a unique ID that identifies just you. <br>The numbering ticket dispenser works well for a day, a week, or maybe even the month, but once that role is replaced, theoretically, you could go back in with the same ticket you go two months ago and find yourself waiting in line with another #41. <br>Imagine being pulled over in NYC, suspected of a crime you didn't commit, because your ticket reads simply #41... nobody is going home with cupcakes! <br><br>PS. "GUID" is most commonly pronounced "gwid." Think squid, but gwid. Ok, that's just a gwid reminder...                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| What is a Foreign Key (FK)?                                                                                    | Visual: Two tables in a traditional relational database<br>Table 1: `employees`<br>\|id (PK)\|name\|department\|<br>\|---\|---\|---\|<br>\|**1**\|John Doe\|HR\|<br>\|**2**\|Sarah Kim\|IT\|<br><br>Table 2: `tickets`<br>\|ticket_id (PK)\|description\|**employee_id (FK)**\|<br>\|---\|---\|---\|<br>\|100\|Forgot password\|**1**\|<br>\|101\|Computer not booting\|**2**\|<br>\|102\|VPN access issue\|**2**\|<br><br>So, essentially, a FK is when a PK is used on a different table.<br><br>In SN, FK are stores in Reference Field types:<br>Visual example in ServiceNow data<br>Table 1: `sys_user`<br>\|sys_id (PK)\|name\|<br>\|---\|---\|<br>\|`a87b3e9087321100c9f0d7d3ccbb3589`\|John Doe\|<br>\|`b93f2a5087321100c9f0d7d3ccbb358f`\|Sarah Kim\|<br><br>#### Table 2: `incident`<br>\|sys_id (PK)\|number\|short_description\|**caller_id (FK → sys_user)**\|<br>\|---\|---\|---\|---\|<br>\|`c03d4b1087321100c9f0d7d3ccbb3592`\|INC0010001\|Forgot password\|`a87b3e9087321100c9f0d7d3ccbb3589`\|<br>\|`d09f2b5087321100c9f0d7d3ccbb3594`\|INC0010002\|Computer not booting\|`b93f2a5087321100c9f0d7d3ccbb358f`\|### Visual example in ServiceNow data<br><br>I didn't know this but the reference field "caller_id" on the Incident table is the same sys_id as that user's record on the sys_user table. <br>- `inc.caller_id` is the **Foreign Key** value.<br>- `inc.caller_id.name` uses **dot-walking** to grab a field from the referenced record.<br><br>One-to-many Relationships<br>This is where we get one-to-many relationships!<br>One User ---> Many Incidents<br><br>Quick metaphor:<br>If the **Primary Key** is a person’s License Play Number,  <br>the **Foreign Key** is a Policeman with a badge number writing that plate number down on a citation.<br><br>So to summarize:<br>\|Concept\|Role\|Example in ServiceNow\|<br>\|---\|---\|---\|<br>\|**Primary Key (PK)**\|Uniquely identifies a record\|`sys_id`\|<br>\|**Foreign Key (FK)**\|Points to a PK in another table\|`caller_id`, `assigned_to`, `cmdb_ci`\|<br>\|**Relationship**\|Connects two tables\|One User → Many Incidents\|<br><br>![[Screenshot 2025-11-12 at 11.10.44 AM.png]] |
|                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|                                                                                                                |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |





---

# **ITIL V3/V4**

> **_Note_**_: ITIL stands for “Information Technology Infrastructure Library”_

First, you’ll want to learn basic ITIL terminology. Maybe take an "ITIL Foundations" course.   
The ITIL Foundations certification isn't _always_ necessary but it's good to be able to say that you have it. Lots of (especially entry-level) job **will require it**, and it's a pretty cheap cert to get.

I've worked with too many developers who, when asked to solve a problem, build really off-the-wall solutions because they don't understand the context they're working in (specifically, **ITIL**). It's difficult to explain how important it is to understand ITIL when you're building functionality that equates or relates to IT processes.

ITIL is _very_ important to understand. It's also _very dry_, especially if you don't have a lot of context for what you're learning (such as prior IT experience). Don't let this discourage you, and don't be afraid to learn only the basics about ITIL at first - but **do come back to it**, and make sure you understand it early-on in your career! 

## **What to know**

- What is the difference between a "problem" and an "incident"?
    
- What is a "CI"?
    
- What is a "service catalog" and "catalog item"? 
    
- What is a "Change request"? 
    
    - If you want to work closely with Change Management (see [**ServiceNow as a Career**](http://career.snc.guru/) article for info on _specialization_), also learn about the different types of change (normal, standard, emergency).
        

## **Resources**

You can find loads of ~100 to 150-page books on Amazon, but make sure you get one with more than 10 reviews and a 4-star minimum rating.   
_Short + high rating = information dense and won't waste your time._ 

You can even find them on audiobook, if you're able to learn that way. I personally love audiobooks, but it requires a lot of focus to learn something technical and completely new from an audiobook. 

[This book](https://amzn.to/2Lnof7d) is a good bet, and it has audiobook and Kindle versions. [This book](https://amzn.to/2swr1jO) also looks great. 

---

# **JavaScript**

JavaScript is the language you'll use to do all of your development within ServiceNow - both client-side, **and** **server-side**. This is because ServiceNow's application servers run a _Java-based_ implementation of JavaScript, called Mozilla Rhino. This has a few minor implications but until you get fairly advanced with SN development, you won't likely have to worry about them. 

> Remember: **Java** is to **JavaScript**, as **Car** is to **Carpet**. In other words, the two are effectively **unrelated**. _Don't learn Java_ - I mean, unless you feel like it. But it won't help you. Instead, learn Java**Script**. 

## **What to know**

Next, I recommend studying JS until you understand the following concepts: 

1. **Variables**, variables **types** (despite JS being “loosely typed” — and learn what “loosely typed” means as well)
    
2. How to create and interact with **arrays** and **objects**
    
3. Condition statements (**boolean expressions**), **conditional** code blocks (“if” and maybe “switch/case” blocks), and **loops** (aka “flow control”).
    
4. **Functions** in JavaScript
    
    1. How to write functions with proper syntax (specifically in JavaScript ES5; so don’t worry about “arrow functions” if you come across those).
        
    2. Function **parameters** (AKA function “arguments”) - how to define the arguments a function accepts when writing the function, and how to **call** a function (with or without arguments)
        
        1. Pro-tip: Typically, “_parameters_” are what you call them when you’re _writing_ a function, and “_arguments_” are what you call them when you’re _calling_ (executing) the function. However, if you use these terms interchangeably, everyone will know what you mean. Very few people are pedantic about that term.
            
    3. **Returning** a value from a function in JavaScript
        
5. **JSON formatting**, objects, reference types, and primitives (and the differences between them) 
    
6. **Pass-by-reference** (and how cool _and_ annoying it can be)
    
7. **Truthiness**, **falsiness**, and strict vs. coercive/loose boolean expressions
    
8. Understand JS's **coercive** loosely-typed nature, and how to use and avoid it  
    (I recommend avoiding it using strict expressions because I think coercion leads to lazy and error-prone programming personally, but the important thing is to _understand_ it)
    
9. **Asynchronicity**, and **higher-order**/**callback** functions
    
    _(You can probably move on and pick this one up later, but make sure it's in your toolkit eventually)_
    

Without studying SPECIFICALLY those topics (as in, not just skipping over everything else to get to specifically those), once you know enough JS that you've incorporated those topics into your knowledgebase by osmosis, you'll be ready to start focusing on the ServiceNow platform.

Focus on **ES5** (ES6 is _unsupported_ on the JS implementation used by the platform back-end (which is based on this old thing called Mozilla Rhino)). Client-side code (such as Client Scripts and Catalog Client Scripts) _can_ use ES6, but don’t worry about that. Anything you write using ES5 syntax will be just fine in client- _or_ server-side code.

You don't need to be a JS super-pro before you jump into ServiceNow, but it's important to be able to read and write simple 10-20 line scripts in basic syntax without getting confused.

You can try using JavaScript IN your ServiceNow instance, and even using basic ServiceNow APIs at this point, but don't get frustrated if you can't figure that part out yet. You can find both the API documentation, and a way to request your own **free** personal developer instance, at [http://developer.servicenow.com/](http://developer.servicenow.com/). 

## **Resources**

For learning JS, I recommend the "You Don't Know JS" book series for this; specifically [Up and Going](https://amzn.to/2HjnVnQ), [Types and Grammar](https://amzn.to/2J9GnVQ), and [this & Object Prototypes](https://amzn.to/2LnOQkJ). The whole series appears to be available **for free** as a Github repository, [here](https://github.com/getify/You-Dont-Know-JS). 

If you’re more of a visual/hands-on learner, which I know a lot of you are, check out Chuck Tomasi’s [**guide to JavaScript**](https://nowjs.snc.guru/) **specifically** in the context of ServiceNow. Go give him a thumbs-up, because this is a **fantastic video series**! The only caveat is that if you use this guide, it can be extremely helpful to already have learned a fair bit about the ServiceNow platform, (such as by reading [**Learning ServiceNow**](http://lsn.snc.guru/) **😉)**.

> **Note**: If you enjoy games, there’s a great resource for learning JavaScript called [**Code Combat**](https://codecombat.com/). If you’re in the US, you can join my “class” on CodeCombat and potentially send me JavaScript questions, by clicking [**here**](https://codecombat.com/students?_cc=FalsePlaceHeavy)!

One great resource for learning JavaScript without too much “clutter” from ES6 that you’ll have to separate out in your mind, is [Learn JS](http://learn-js.org/).  
This is a great resource if you’re the sort of person who can easily learn by the sort of “read about it, then try it” methodology, and is the first place I tell people to check out when they’re thinking about learning JS, just to get the super-basics. More advanced concepts are more difficult to learn from a resource like this, but it’s a great place to start!

If you prefer a “watch and follow along” methodology, there is a wonderful YouTube channel by a big huge dork of a guy, called [The Coding Train](https://www.youtube.com/user/shiffman). This channel focuses a lot on JavaScript, but it definitely covers a lot of libraries, APIs, and tools that you don’t need for ServiceNow. If you want to learn JavaScript more generally, and build a knowledgebase that’s more generally applicable than _just_ ServiceNow development from the beginning, this is a great channel to learn with. [This playlist](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6Zy51Q-x9tMWIv9cueOFTFA) for example, teaches you JavaScript using the “P5.js” library. This library is completely irrelevant to ServiceNow, but you learn the language pretty thoroughly along the way.

A lot of people also find [codecademy](https://www.codecademy.com/learn/introduction-to-javascript) to be useful as a bit more of a "hands-on", almost bootcamp-style guide to the very basics - though I’m not personally fond of their recent changes. Just remember that you should focus on **ES5**, _not_ ES6 (even though codecademy will teach you some ES6 concepts, it's important to try to sort of compartmentalize them). 

My biggest bit of advice for learning JS… **do not pay for a “boot camp”**. Boot camps, for _most_ people, are just not a good way to learn and retain a large amount of information long-term.

> **_Note_**_: Keywords like_ **_let_**_,_ **_const_** _and_ **_class_** _are all_ **_unsupported_** _in ES5, and therefore in ServiceNow's server-side scripts (with rare exceptions such as scoped apps in post-Tokyo ServiceNow instances). You can use them in client-scripts, but it's best to focus mainly on ES5, especially at first, to avoid confusion._ 

---

# **ServiceNow**

Once you have at least a passing understanding of relational databases, ITIL, and JavaScript, you can begin your journey into the ServiceNow ITSM platform! This is the specific learning path that I recommend for this, but in the interest of full disclosure, I wrote a couple (but not all) of the books I recommend below. 

1. Set up your [Personal Development Instance](http://developer.servicenow.com/) (PDI).
    
2. Read [Learning ServiceNow](http://lsn.snc.guru/) (**second edition**). 
    
3. Brush up on and reaffirm your JavaScript knowledge.
    
4. After reading [LSN](http://lsn.snc.guru/) and following the examples therein, do you feel like you're missing anything?
    
    1. Now is the time to study JS _in the context_ of ServiceNow.
        
5. Use ServiceNow for a while. Read the community forums and try to answer questions yourself, even if they've already been answered. Researching these answers will help you learn, and reinforce what you've already learned. 
    
6. At this point, you're ready to start looking for an entry-level “Jr. ServiceNow developer” job!  
    Don't stop studying though, just cause you're looking for a job! Keep your skills sharp, and read on! 
    
    1. **_Note_**_: You may want to get the ServiceNow Administrator certification, but having a job as a junior ServiceNow developer will help expose you to more knowledge more quickly than anything else._ 
        
    2. Don’t forget to check out [my other article on **ServiceNow as a career**](http://career.snc.guru/), including choosing a career path, how to build a “ServiceNow resume”, interviewing for a ServiceNow job, negotiating your salary, and so on.
        
7. Read [The ServiceNow Development Handbook](http://handbook.snc.guru/), and keep it around. You may want to reference it often to make sure that you're writing robust, best-practice code, building future-mindful functionality, tables, and so on. 
    
8. Read [Mastering ServiceNow](https://amzn.to/2Jpg4KD). It contains a lot of module-specific and deeper info that can definitely be helpful as you look to move your career forward into a more lucrative salary range.
    
9. Read the [handbook](http://handbook.snc.guru/) again. 😛 
    
10. Peruse [Jace Benson’s news site](https://news.jace.pro/?relatedSort=ItemClick%3A30), which aggregates some of the best sources of ServiceNow news, information, and articles.
    
    1. This can be a great resource for finding out what the community is asking and saying about the ServiceNow platform. The link above points directly to the most clicked resources over the last 30 days which are aggregated by [news.jace.pro](https://news.jace.pro/).
        

**Congrats**! Once you've got through all of the above, and with a couple of years of hands-on experience, you're likely to be a really solid, perhaps even senior-level developer or architect!

Never stop learning. 🙂
