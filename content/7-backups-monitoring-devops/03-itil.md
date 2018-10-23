---
title: "ITIL"
weight: 15
pre: "3. "
---

{{< youtube df5VhDPq3ig >}}

#### Resources

* **[Slides]({{< relref "/7-backups-monitoring-devops/03-itil-slides.md" >}})**
* [ITIL](https://en.wikipedia.org/wiki/ITIL) on Wikipedia
* [ITIL](https://www.axelos.com/best-practice-solutions/itil) from Axelos
* [ISO/IEC 20000](https://en.wikipedia.org/wiki/ISO/IEC_20000) on Wikipedia
* [ISO/IEC 20000-1:2018](https://www.iso.org/standard/70636.html) from ISO

#### Video Transcript

In this video, I'll be taking a detour from all of the technical topics in this class to discuss a more philosophical topic: the art of system administration. Specifically, this video will introduce you to ITIL, one of the core resources for many IT organizations worldwide.

First, you might be wondering what ITIL is. Originally, it was an acronym for the "Information Technology Infrastructure Library," but it has since been officially shortened to just ITIL. ITIL is a comprehensive set of standards and best practices for all aspects of an IT infrastructure. Many organizations refer to this as "IT Service Management" or "ITSM" for short. By making use of the information found in the ITIL resources, you should be able to keep your IT systems running and make your customers happy.

This slide gives a brief history of ITIL. It was originally a set of recommendations developed by the UK Central Computer & Telecommunications Agency in the 1980s. That information was shared with many government and private entities, and they found it to be a very useful resource. By the 1990s, it was expanded to include over 30 volumes of information on a number of IT processes and services. As the technology matured, those volumes were collected into 9 sets of guidelines in the early 2000s, and by 2007, a complete rework was released, consisting of just 5 volumes encompassing 26 processes in all. This version is known as ITIL Version 3.

In 2011, a small update to version 3 was released by the UK Office of Government Commerce, the maintainers of ITIL at that time. However, starting in 2013, the licensing and maintenance of ITIL was handed over to Axelos. They also handle ITIL certifications. Recently, Axelos announced that they are working on ITIL 4, which should be released sometime in the next year.

As mentioned before, the current version of ITIL consists of 5 volumes: Service Strategy, Service Design, Service Transition, Service Operation, and Continual Service Improvement.

These volumes are interrelated, forming the backbone of any IT organization. This diagram shows how they all fit together. At the core is strategy, which defines the overall goals and expectations of the IT organization. Next, design, transition, and operation deal with how to put those strategies into practice and how to keep them running smoothly. Finally, Continual Service Improvement is all about performing an introspective look at the organization to help it stay ahead of trends in technology, while predicting and responding to upcoming threats or issues.

To break it down even further, this diagram lists most of the 26 processes included in ITIL. "Supplier Management" under "Design" is omitted for some reason. As you can see, there are quite a variety of processes and related items contained in each volume of ITIL.

However, I've found one of the easiest ways to discuss ITIL is to relate it to a restaurant. This analogy is very commonly found on the internet, but the version I am using can be most closely attributed to Paul Solis. So, let's say you want to open a restaurant, but you'd like to follow the ITIL principles to make sure it is the best, most successful restaurant ever. So, first you'll work on your strategy. That includes the genre of food you'd like to serve, the location, and an analysis of future trends in the restaurant business. You don't want to enter a market that is already saturated, or serve a food genre that is becoming less popular.

Next, you'll discuss details in the design. This includes determining specific menu items, the hours of operation, staffing needs, and how you'll go about hiring and training the people you need.

Once you have everything figured out, its time to enter the transition phase. During this phase, you'll test the menu items, maybe have a soft open to make sure the equipment and staff are all functioning properly, and validating any last-minute details of your design before the grand opening.

Once the restaurant is open for business, it's time to enter the operational phase. In this phase, you'll be looking at the details in the day-to-day operations of the restaurant, such as how customers are greeted and seated when they enter, how your wait staff enters the food orders, how the kitchen prepares the food, and finally how your clients are able to pay and be on their way. You'll always be looking for issues in any of these areas, and work diligently to correct them as quickly as possible.

In addition, great restaurants will undergo continual service improvement, always looking for ways to be better and bring in more business. This includes surveys, market research, testing new recipes, and even undergoing full menu changes to keep things fresh and exciting.

Overall, if you follow these steps, you should be able to build a great restaurant. If you'd like a great exercise applying this in practice, I encourage you to watch an episode or two of a TV show that focuses on fixing a failing restaurant, such as "Restaurant Impossible" or "Kitchen Nightmares," and see if you can spot exactly where in this process the restaurant started to fail. Was the menu too large and confusing? Were the staff not trained properly? Did they fail to react to customer suggestions? Did the market change, leaving them behind? I've seen all of those issues, and more, appear during episodes of these TV shows, but each one always links directly back to one of the volumes and processes in ITIL. My hope is that you can see how these same issues could affect any IT organization as well.

ITIL also proposes a maturity model, allowing organizations to rate themselves based on how well they are conforming to ITIL best practices. Level 0 represents the total absence of a plan, or just outright chaos. At Level 1, the organization is starting to formulate a plan, but at best it is just a reactive one. I like to call this the "putting out fires" phase, but the fires are starting as fast as they can be put out. At Level 2, the organization is starting to be a bit more active in planning, so at this point they aren't just putting out fires, but they are getting to the fires as fast as they develop.

By Level 3, the organization is becoming much more defined in its approach, and is working proactively to prevent fires before they occur. There are still fires once in a while, but many of them are either predicted or easily mitigated. At Level 4, most risks are managed, and fires are minimal and rare. Instead, they are preemptively fixing problems before they occur, and always working to provide the best service possible. Lastly, at Level 5, everything is fully optimized and automated, and any error that is unexpected is easily dealt with, usually without the customers even noticing. I'd say that Netflix is one of the few organizations that I can say is very comfortably at Level 5, based on the case-study from Module 5. Most organizations are typically in the range of Level 3 or 4.

There are a variety of factors that can limit and organization's ITIL maturity level, but in my opinion, they usually come down to cost. For an organization to be at level 5, it requires a large investment in IT infrastructure, staff, and resources. However, for many large organizations, IT is always seen as a "red line" on the budget, meaning that it costs the organization more money than it brings in. So, when the budget gets tight, often IT is one of the groups to be downsized, only to lead to major issues down the line. Many companies simply don't figure the cost of an IT failure into their budget until after it happens, and by then it is too late.

Consider the recent events at K-State with the Hale Library fire. If K-State was truly operating at Level 5, there would most likely have to be a backup site or distributed recovery center, such that all systems could be back online in a matter of hours or minutes after a failure. However, that would be an astronomical cost to the university, and often it is still cheaper to deal with a few days of downtime instead of paying the additional cost to maintain such a system.

So, in summary, why should an IT organization use ITIL? First, IT is a very complex area, and it is constantly changing. At the same time, user satisfaction is very important, and IT organizations must do their best to keep customers happy. Even though it is a very technical field, IT can easily be seen as a service organization, just like any restaurant. Because of that, many IT organizations can adopt some of the same techniques and processes that come from those more mature fields, and ITIL is a great reference that brings all of that industry knowledge and experience to one place. Lastly, poor management can be very expensive, so even though it may be expensive to maintain your IT systems at a high ITIL maturity level, that expense may end up saving money in the long run by preventing catastrophic errors. If you'd like to know more, feel free to check out some of the resources linked below the video in the resources section. Unfortunately, the ITIL volumes are not freely available, but many additional resources are.
