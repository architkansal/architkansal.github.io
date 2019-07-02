---
layout: post
title: Taking AXL to Production - Season of Code 2019 at Arcesium
---

<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/post.css" />
Recently, Arcesium organized its global Season of Code (SOC) event for the year 2019. I decided to use this opportunity to make AXL (our [most-creative-hack winner project from Hackathon-2018](https://architkansal.github.io/Arc-Most-Creative-Hack-2018/)) production ready and collaborated with [Ram Chidambaram](https://www.linkedin.com/in/ramachandran-chidambaram-170071141/) and [Dhiraj Bhakta](https://www.linkedin.com/in/dhiraj-bhakta-065529113/) to accomplish this.

First blog in the series : [Introduction to AXL](https://architkansal.github.io/Arc-Most-Creative-Hack-2018/)

## How SOC Works:

SOC provides people the opportunity to work on a project of their choice. It aims at building production-ready, brand-new features into the Arcesium platform offering or projects for efficiency and internal usage. Unlike Hackathons, SOC participants are expected to write production-ready code.

SOC takes off with an Idea Pitching session where each team presents their ideas to judges. Shortlisted teams then get to work on their implementation for 6 weeks, following which they deliver the final presentations.

This year, 11 teams pitched their ideas and 7 were shortlisted for the implementation round.

## The Idea Pitching Session:

Excited by the possibilities that AXL has to offer, we targeted integrating AXL into margin-replication infrastructure at Arcesium where the idea of AXL was born in the first place!


Few other items in our to-do list were error-handling and fully functional minimal online IDE integrated into the Arcesium platform for developing, testing, running and publishing AXL code.

## The SOC Implementation:

## Error Handling in AXL:

We added support for robust, graceful, efficient and useful handling and reporting for both syntactical as well as runtime errors in AXL. Here is a list of a few cases that we handled:

* **Syntax errors with line number information**: We were able to provide correct information in a lot of cases but for few cases the line information was wrong by 1-2 lines. It's not always possible to provide the correct line number with error because the way we look at the code isn’t how system parses it.
* **Reporting conflicting definitions for reusable components**: AXL natively supports defining and re-using (by importing) components or using components from standard library. This brings the possibility of having multiple definitions for the same component, which needs to be resolved by the user.
* **Context/Data does not exist or support the operation**: AXL works on an input context which could be user-specified or inferred. The possibility of unsupported operations, accessing non-existent data in a context needed to be gracefully handled and reported.
* **Gracefully ignore few specific types of errors**: Depending on the use-case, we decide to either exit the execution or continue with a warning.
* **Invalid Input data**: AXL expects input to be valid JSON data and cannot execute otherwise. Similarly, if other optional inputs are provided, then necessary validations are performed on those as well.

## The AXL IDE:

One of the necessary tools for any programming language is a good development and testing framework. We built a web-based Integrated Development Environment (IDE) for AXL on the Arcesium platform for this. 


We implemented the web-based AXL IDE using Java backend and React frontend.

An IDE can provide a lot of different features to users. We kept the features in AXL IDE very minimal because it had to be completed within the contest duration. Here is the list of features we thought were necessary in AXL IDE:

* Code editor - we used ACE editor (React Component) for this
* Input area with placeholder inputs
* Ability to check for syntactical errors
* Ability to execute and navigate through the output (or runtime errors, if any)
* Ability to save AXL code
* Ability to publish AXL code (this is necessary to make the code available for deployment)
* Minimal version control (ability to checkout a previous version of AXL code)

## AXL in Motion - Arcesium Margin-Replication Use-Case:

A few benefits that AXL provides:

* Simple, English-like syntax 
* Codebase size reduced by 80% 
* Time taken to write a new piece of code: 2-3 hours (reduced from several days)
* Gives users a lot more control through a UI
* Reusability - ability to write and import operators and modules written again in AXL

A lot of these features are supported by AXL language and the web-based IDE. Now, we wanted to demo the AXL impact in production. We implemented an adapter in the Arcesium platform infrastructure to bridge the gap between the AXL execution environment and platform. So now a user could write and publish AXL code from IDE and deploy it in production with the help of our adapter in the platform, which was completely transparent to them. With the help of this bridge, we were able to write and execute AXL code for real production margin replication use-cases. 

Here are the high level stats collected from above exercise:

* **Code size in AXL** - ~80 Lines vs. code size in programming language - ~1000 Lines.
* **Execution time** - no impact
* **Execution output** - consistent with expected production output
* **Time to write AXL code** - ~4 hours vs. a few days in programming language
* **Few other parameters** which significantly improved by using AXL but cannot be directly translated into numbers include 
    * End-user accessibility 
    * Logic transparency
    * Ease of maintenance

**Our project stood 2nd place and got us a OnePlus 7 Pro each!**

## Next Steps:

As a next step, we could build support for more operations in AXL, add new features into AXL IDE or explore integrating AXL into other applications and products at Arcesium. I am really excited to see how this project evolves with time! 


