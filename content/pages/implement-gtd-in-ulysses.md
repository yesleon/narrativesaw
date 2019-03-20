---
date: 2019-03-20T18:05:23+08:00
draft: false
title: Implement GTD in Ulysses
categories: []
---

# Implement GTD in Ulysses

I use Ulysses for all serious writings, paid or unpaid. Since the range of my interests is quite wide -- I write essays, short stories, and technical articles -- my Ulysses library was complicated enough to set me back from opening the app. There were such things like how I should archive the completed articles, and how the sheets should be organized, that added up to my anxiety.

It’s not supposed to be like this. Ulysses should give me liberty of creativity, not anxiety on organizing sheets.

I realized that the library approach Ulysses takes is not necessarily better than the document approach most word processors take. Yes, you’ll have to manage the file system and it’s a pain too, but once you’ve done with a project you can always archive it into some compressed filetype and/or just throw it into a hidden folder. Not for a library system though, at least not obvious in Ulysses at the beginning. You cannot mark a sheet or a group as readonly, and you cannot compress them into zip files. Well, it’s possible, but you’ll have to do it manually in Finder, and that beats the purpose of using a library system.

After all, a library system is just another organization paradigm. You still have to make it work for you, and it requires effort to design as in using a file system. The best library system I’ve used is from Things, a GTD to-do list app, but that’s because it follows GTD quite strictly and there’s like only one way to use it. Ulysses is not like that. Its library is just like Finder that it doesn’t tell you how to organize things. Therefore, we’re going to have _options_ when we want to implement some functions, for example archiving. 

Archiving is the one thing that immensely boosts my productivity. I’m the kind of person that worries about everything in front of me, so putting completed articles away really helps me focus on the ones I should work on at the time. However, I couldn’t decide if I should use a keyword for archiving sheets, or just create archive groups for those sheets. And if I’m going to create archive groups, which level should I put them in? In the project group? What about a finished project?

I was stuck here for a long time. Fortunately, not long ago, an idea struck me.

## How Things Handles It

I was studying the structure of Things’ library and I realized that the Inbox, the Areas, and the Projects work like folders, while the Today list, the Anytime list, the Sometime list, and the Logbook all work as smart lists. 

| Folder   | Smart List |
|----------|------------|
| Inbox    | Today      |
| Areas    | Anytime    |
| Projects | Upcoming   |
|          | Someday    |
|          | Logbook    |

It is very clear that folders are for static categorization and smart lists for dynamic action grouping here. In other words, when you put something in a folder, it should stay there for its entire life; but if you assign a thing to, say, the Anytime list, it would be prone to changes. It might be finished very soon and then it would be re-assigned to the Logbook.

So there it is. Static folder structure versus dynamic tag assignment.

## Meanwhile, In Ulysses…

The equivalencies in Ulysses of folders and smart lists are _groups_ and _filters_, and it’s actually quite simple to set up a GTD-like system here according to the Things approach.

![](DraggedImage.png)

Guess which are groups and which are filters? I hope it’s not that obvious… yes, _Anytime_, _Someday_, and the _Logbook_, under the _iCloud_ section, are all filters. All groups are put inside a base group called, uncreatively, _Groups_, except for the _Inbox_.

I use keywords like _completed_ and _someday_ to assign sheets into the filters, and when there’s no such keywords, the sheets are going to show up in _Anytime_. All the filters work upon the base group _Groups_ since they can’t just work on the entire _iCloud_ section. They need a group to work on. Fortunately, I don’t need them to include sheets in the _Inbox_. Actually, smart lists in Things don’t include items in the Inbox, either.

You might’ve noticed that there’s no _Today_ list. There is, in fact, but it’s called _Favorites_.

Not sure it’s by design or accidentally, but there are icons look exactly the same as in Things. The stack for _Anytime_, the star for _Favorites_, and the book with a check for the _Logbook_ are just like those in Things. I can’t find the covered box icon for _Someday_ in Ulysses, but there are plenty of alternatives that work as great.

With this organizing structure, I act mostly on the filters, which includes finding some sheets to work on and… well that’s about it. When I want to focus on a specific project though, I can always dive into the _Groups_ and work in the one group I’m interested in.

Although Ulysses provides us the ability to mix groups and filters together, I find it best to separate the two paradigm like this, just to prevent complexity.

## Wishlist and Workarounds

It is still irritating that we can’t add filters that apply to the entire library. There’re built-in filters that work this way, i.e. _All_, _Last 7 Days_, and _Favorites_, but there’s no way to add custom ones. 

The types of filter condition are also very limited. You can only search for keywords, dates, and contents. You can’t search for sheets that have a deadline, and you can’t exclude sheets which reside in a specific group. 

Also, the search system is somehow totally unrelated to the filter system. I know it’s the same with Things, but Finder has saved search, so why not integrate the two into one?

The keyword management on iOS is cumbersome too. There was no way to show all keywords in one place, therefore if you wanted to show all sheets that have a specific tag, **you had to create a filter for that**. And no, it doesn’t provide the option to search for tags only when searching in Ulysses. Yet another reason to integrate filters and searching. The whole keyword design on Ulysses for iOS just feels so basic that it can be easily replaced by hashtags. (I just tried. It works great. Might worth another research someday.)

Finally, although we can make it look _really like_ Things in Ulysses, there’s no way to add a start date to a sheet. It might not make much sense for Ulysses though, since it is ultimately a writing app not a scheduling app. Luckily, Ulysses supports sheet links, so we can copy the sheet links and paste them to our actual GTD apps. We can also assign them to the _Someday_ list or create a _Upcoming_ list just for them.