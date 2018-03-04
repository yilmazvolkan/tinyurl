# TinyURL Project
<p align="center">
<a href = "https://github.com/yilmazvolkan/tinyurl/projects"><img 
<img src="https://github.com/yilmazvolkan/tinyurl/blob/master/Res/tinyURL_logo.png" width="320" height="160"></a>
</p>

<p align="center">
    <a href="https://github.com/yilmazvolkan/tinyurl/blob/master/README.md">
        <img src="https://img.shields.io/badge/DESCRIPTION-ONLINE-46dbdb.svg"
             alt="Description">
    </a>
    <a href="https://github.com/bounswe/bounswe2018group1/issues">
        <img src="https://img.shields.io/badge/ISSUES 4-CLOSED-8de9e9.svg"
             alt="Issues">
    </a>
</p>


## :tophat: Introduction


This is a companion problem to the System Design problem. TinyURL is a URL shortening service where you enter a URL such as https://github.com/yilmazvolkan/tinyurl/tree/master/Res  and it returns a short URL such as http://tinyurl.com/4e9iAk. It is also called friendly URL.

A friendly URL (Uniform Resource Locator) may be desired for messaging technologies that limit the number of characters in a message (for example SMS, Twitter), for reducing the amount of typing required if the reader is copying a URL from a print source, for making it easier for a person to remember, or for the intention of a permalink (unchanged for many years). In Twitter, this service is supplied automatically, it shortens links using its own URL shortening service.
Other uses of URL shortening are to "beautify" a link, track clicks, or hide the underlying address. Although hiding of the underlying address may be desired for legitimate business or personal reasons, it is open to abuse. Some URL shortening service providers have found themselves on spam blacklists, because of the use of their redirect services by sites trying to bypass those very same blacklists. Some websites prevent short, redirected URLs from being posted.


## :blue_book: Basic Questions

* **How many unique identifiers possible? Will you run out of unique URLs?**
The answer depends on how many character will be used. With 26 low-case + 26 upper case letters + 10 digits (the choice of reasonable sites), using one character gives you 62 positions (i.e. 62 shortened URLs), then each additional char multiplies the position number by 62. For example, in our case, if you use 6 character you can have 62 over 6 different urls. It satisfies for every person on earth can take 7 different URLs.

* **Should the identifier be increment or not? Which is easier to design? Pros and cons?**
Actually, for Google URL shortener it seems to enough. Few people are creating short URLs, and each person creates few URLs. Original URLs are enough in most cases. Moreover, using random string as IDs may sacrifice performance a little bit. More specifically, when you already have millions of records, insertion can be costly. Since IDs are not sequential, so every time a new record is inserted, the database needs to go look at the correct page for this ID. However, when using incremental IDs, insertion can be much easier 

* **How should we design the database in order to store above a million URLs?**
If you want to store a huge amount of key-value pairs across multiple instances, you need to design a look up algorithm that allows you to find the corresponding machine for a given look up key. For example, if the incoming short alias is http://tinyurl.com/abcd123, based on key “abcd123” the system should know which machine stores the database that contains entry for this key. This is exactly the same idea of database sharding where each shard is held on a separate database server instance, to spread load. Problems are; replication, resharding, and concurrency.

   * Replication. Data stores can crash for various random reasons, therefore a common solution is having multiple replicas for each database. There can be many problems here: how to replicate instances? How to recover fast? How to keep read/write consistent? 
   * Resharding. When the system scales to another level, the original sharding algorithm might not work well. We may need to use a new hash algorithm to reshard the system. How to reshard the database while keeping the system running can be an extremely difficult problem.
   * Concurrency. There can be multiple users inserting the same URL or editing the same alias at the same time. With a single machine, you can control this with a lock. However, things become much more complicated when you scale to multiple instances.



## :beers: Contributers


<p align="left">
<a href = "https://github.com/yilmazvolkan"><img 
<img src="https://avatars2.githubusercontent.com/u/28186366?s=400&v=4" width="120" height="120"></a>
</p>
[Volkan Yılmaz](https://github.com/yilmazvolkan)




