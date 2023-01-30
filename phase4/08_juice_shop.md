# Extension Exercise - Juice Shop

This exercise is optional and not assessed. You should work on this if you have
time during the first week of the module and have completed all the other,
non-extension sections.

## Juice Shop

The OWASP Foundation and its many collaborators have done more than produce a
Top 10 and ZAP application - they have also produced a well-maintained
application that's ideal for learning about security. We can't improve on their
own introduction to their application, so here it is:

> OWASP Juice Shop is probably the most modern and sophisticated insecure web
> application!

The Juice Shop is an actively maintained application riddled with security
concerns and vulnerabilities, including multiple examples of the OWASP Top 10
along with many, many other problems. The problems are also graded in terms of
difficulty, from introduction/tutorial level problems through to extremely
well-hidden and obscure vulnerabilities.

There's certainly no expectation that you will "complete" the Juice Shop! It's a
difficult challenge for specialist security testers who have been in their
industry for years, but it does provide a place for you to explore, try out some
of the tools, and learn more about the sorts of vulnerabilities you can find.

We'll give you some details on how to get the Juice Shop installed and running
locally, a few suggestions of where to begin, including a **warning if you
decide to try running OWASP ZAP** at the bottom of this page, and then leave you
to explore.

## Installation

> Note that by default, Juice Shop also runs on localhost:3000, just like
> app.js, so now is a good time to stop that one from running.

The most up-to-date details on installation are going to come from OWASP
themselves, so take a look at the [Juice
Shop](https://owasp.org/www-project-juice-shop/) project and look for
"Installation" on the right-hand side.

You can choose your own way (e.g. Docker if you want) but if you want a
suggestion, https://github.com/juice-shop/juice-shop#from-sources on a Makers
Mac laptop has been shown to be quick and successful.

## Exploration

Once installed, you should be able to browse to http://localhost:3000 and see
the OWASP Juice Shop running.

Feel free to take a look around at the site. It might help to remember that
you're not supposed to be testing the functionality of the site, accessibility,
usability and so on - it has a lot of bugs in those sorts of areas! - and
instead the focus here is on security testing.

## Where to start?

OWASP suggest that you start off by looking for some sort of associated score
board on which your progress in finding security problems is recorded. Like
before, the OWASP documentation is the place to read more.

You can start with a general overview and some introductions to the architecture
and what the site does by reading https://pwning.owasp-juice.shop.
Alternatively, you could jump ahead to
https://pwning.owasp-juice.shop/part2/score-board.html and read through the
steps at the bottom. Can you use some simple browser-based tools to find the
score board?

## Tools

OWASP claim that you could find most, if not all, of the vulnerabilities with
just a browser (and lots of knowledge and effort, of course!) rather than
needing to rely upon specific tools.

Our advice therefore would be to use the following:

* Inspection of page source
* Dev tools like the Network tab showing HTTP communication
* Modification of HTTP requests

### Modification of HTTP requests

In an earlier part of this phase, you learnt that Firefox had the ability to
inspect requests so that you can resend them, optionally with your own edits.
The following are some quick example steps you can use, to see that in action
for yourself so you know how to do it:

* In Firefox, open a new tab
* Press F12, or go to Tools -> Browser Tools -> Web Developer Tools
* In the new panel that appears, switch to the Network tab
* Browse to https://apply.makers.tech/are-you-ready-to-be-a-software-developer
* Left-click on one of the first few rows - it'll have a Status of "200" (the
  "response code" meaning success) and be for File
  "are-you-ready-to-be-a-software-developer"
* Note a new panel is shown with things like the request headers and response
  headers
* Right-click on the same row, choose "Edit and Resend"
* Note a different new panel is shown, called "New Request"
* Change it from a GET request to a POST request - this is something you
  couldn't normally *just do* in the page itself...
* Click "Send"
* Inspect either the latest in the Network tab of the panel showing the request
  and response data - note this request got back a Status of "403" (Forbidden!)

> Note: please don't now go and start "attacking" Makers' website! A POST
> request is one thing, a full-on attack is something different, and that's what
> Juice Shop is for.

### ZAP

Firstly, the warning:

> If you decide to use ZAP to **actively** attack the Juice Shop, be aware that
> you will need to create some boundaries for it, otherwise you'll likely find
> yourself penetration testing a site you weren't intending to attack. If you're
> unsure, **stop**, then ask.

You *can* choose to point ZAP at your Juice Shop install and run an active scan
to see what it'll find. One of the things an active scan does is it discovers
other things it can test, such as URLs and entry points.

For what it's worth, by doing an active scan you'll find some vulnerabilities,
but maybe not as many as you might hope. If you still decide to go ahead, the
steps you should follow are:

* From ZAP's list of passively scanned Sites, right-click on
  http://localhost:3000 and choose "Include in Context" -> "New Context", then
  close the dialog
* Above Sites, you should see Contexts - right-click on your new context and
  choose "Active Scan..." then start the scan

ZAP uses Contexts as its boundaries - if you set a boundary/context, it won't go
outside that. Were you to Active Scan a URL from the Sites instead, you may find
ZAP runs a scan, discovers a set of URLs that aren't related to the Juice Shop
and don't start "http://localhost:3000", and quickly runs off actively scanning
something like "https://www.mozilla.org" as well - in case it needs saying
again: do not do that!

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F08_juice_shop.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F08_juice_shop.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F08_juice_shop.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F08_juice_shop.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F08_juice_shop.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
