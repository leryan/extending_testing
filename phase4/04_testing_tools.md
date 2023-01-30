# Security Testing Tools

There's no one single tool for web application security testing and even the
list below can't be exhaustive, but the following are some tools you may find
useful, a number of which we'll be using in later exercises.

## Browsers

Browsers are the first tool to have on your list when you're thinking about web
application security testing. Sure, they're the thing that displays the
application, but modern browsers have so much more power than just displaying
pages.

Firstly, browsers allow you to inspect the page source. The ability to gain
access to some of what's going on behind the scenes, and perhaps view links,
scripts or even comments left in by the developers can start to reveal
information which you can use to further progress your testing.

More powerfully, browsers such as Firefox and Chromium-based ones offer a set of
"Dev Tools" ranging from network traffic monitoring to consoles allowing you to
see errors, logs, cookies, and other local storage data, all of which can reveal
to you more information and/or vulnerabilities.

Dev Tools can usually be accessed via F12, from context menus or from some sort
of browser "Tools" menu.

## Clients for HTTP Requests

When dealing with web applications and/or APIs, the ability to inspect HTTP
requests - like we can do with browser Dev Tools above - is just one part of the
story. The ability to create our own requests or even tweak ones that our
browser might make, opens up a new world of testing to us.

Naturally, wherever we are empowered, attackers may flourish too and so as
crafting clever or evil requests is something they're likely to do, we need to
test for and then help defend against those types of attacks.

There are many, many ways of sending your own hand-crafted HTTP requests to
mimic a user with a browser (or a hacker with a mission) and so these are just
some we would recommend:

* [Postman](https://www.postman.com): a popular application that will allow you
  to send HTTP requests, inspect the responses, and a lot more including
  managing projects, preserving previous requests and running a series of tests.
* [cURL](https://curl.se): a ubiquitous command line utility that has far less
  gloss and no front-end UI compared with Postman, but the advantage of being
  very "raw" - if you want to send a nonsense, malformed, ridiculous request
  then cURL will just do that for you with no hand-holding
* Browsers (again): specifically Firefox, which will allow you not only to see
  the request and response, but will allow you to not only send the request
  against but optionally modify parts of the request, like adding or removing
  headers, changing the URL, methods, etc.

## Scripts & Automation

If you're comfortable putting together a quick script Python or Bash, you
can easily change your slow manual HTTP requests, let's say, into a torrent of
identical requests sent every millisecond.

Similarly, you could mimic many users accessing a site at the same time, send
lots of different requests, or even work through a large number of malicious
request body contents by wrapping something like cURL (see above) up into a
script.

Like all the other tools, automation isn't the full story, but having the
ability to automate away some of the manual element can open up new security
testing ideas you couldn't do otherwise.

## Penetration Testing Tools

At the more advanced end of the security testing tools are applications designed
specifically to attack applications on your behalf. There are expensive and open
source options, with a huge variety of features and attack vectors.

It's probably most useful at this stage to know that they exist and that they
are an option if and when you need them, rather than devoting hours of time into
learning a specific one. However, we will be covering one - "ZAP" - in a later
section so that you've seen some of the power those tools can offer.

[Next Challenge](05_sast_dast.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F04_testing_tools.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F04_testing_tools.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F04_testing_tools.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F04_testing_tools.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F04_testing_tools.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
