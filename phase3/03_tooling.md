# Tooling

In this section we'll introduce some tools that you can use to perform
accessibility testing but these tools will not automate everything for you.
You'll need to do some manual testing too.

## Task: Choose Some Sites to Test

You'll need a small selection of sites to play with and, ideally, some will have
critical accessibility flaws. Your task is pick 5 sites that you'd like to test,
but don't spend ages deciding :)

* Every now and then, someone produces a list of the least accessible sites but,
  thankfully, this often prompts companies to improve. So, those lists go stale
  but if you search for "list of least accessible sites" you'll find one of them
  and, if you're lucky, it'll be very recent. Pick one or two from there.

* Pick one or two sites that you use frequently.

* [This site was created to demonstrate accessibility
  flaws](https://www.w3.org/WAI/demos/bad/before/home.html) - we saw images of
  it earlier on. There are two versions, accessible and inaccessible, of the
  same pages. You can toggle between those versions at the top of the page, just
  underneath the tabs. The defects can all be revealed by selecting to "Show
  Annotations", so you don't _need_ to test these pages but the inaccessible
  version does guarantee some positive results. So, if you like, include this
  site to ensure you find some defects.

## Web Accessibility Evaluation (WAVE) Tool

WAVE is actually a suite of tools - we'll use the free browser extension here
but there is also a paid version that could be integrated as part of your
automated checking process.

### Setup

[Download the browser extension](https://wave.webaim.org/extension/).

### Usage

Using the WAVE browser extension is really simple. You should see an icon, like
the one below, next to the address bar of your browser or listed among other
extensions (if you already have a few). Click on it and you'll immediately see
some results, summarised. Select 'Details' and, as you might expect, you'll see
more detailed results.

![Wave extension icon](../images/wave_icon.png)

You'll be using WAVE to do some analysis in a bit, so don't worry about getting
into what it has found in too much detail, just yet.

## Lighthouse

Google Chrome has its own Dev Tools built-in tool called Lighthouse, which can
also be used for inspecting accessibility. Like WAVE, it is only an automated
tool and can't replace manual, human thinking and analysis, but it's another aid
which you could consider using.

### Usage

Using Lighthouse is also really simple. In Google Chrome, open Dev Tools and
find the "Lighthouse" tab - you might need to expand `>>` to find it, if it's
not already shown alongside "Elements", "Console", and the others. Choose the
following settings:

* Navigation (Default)
* Desktop
* Just "Accessibility" from the checkboxes

and then `Analyze page load`. Like before, don't worry too much about what it
finds - just make sure you can run it and generate a report. You'll be using it,
and WAVE, next.

## Exercise: WAVE & Lighthouse

Use WAVE and Lighthouse to evaluate some pages from some or all of the 5 sites
that you chose earlier, then pick one to focus on when answering the following
questions...

* Who might struggle to use this site?
* What would the consequences be for both the users and company?
* Which defects would you prioritise fixing?
* Are the tools finding the same things, is one finding all the other found and
  more, or are they both finding unique problems and adding value?

## Colorblindly

There are some tools out there for designers who want their sites to work for
colour blind users (like [Color
Blind](https://www.figma.com/community/plugin/733343906244951586/Color-Blind) as
a tool in Figma when designing a site or application). There are also some
browser plugins which you could consider as a tester analysing a site.

One such plugin is
[Colorblindly](https://chrome.google.com/webstore/detail/colorblindly/floniaahmccleoclneebhhmnjgdfijgg/related)
which allows you to view the site as it could look to users with a decreased
ability to see certain colours or differences between colours.

Install the plugin now and try it out on a few of the 5 sites you originally
chose, so you can experience some of the things your future users could be
dealing with.

> If you'd like to learn more about the different names and what they mean, and
> enjoy decision tables(!),
> [Wikipedia](https://en.wikipedia.org/wiki/Color_blindness#Summary_of_cone_complements)
> represents them nicely.

## VoiceOver

VoiceOver is Apple's built in Text to Speech program. It allows visually
impaired users to navigate their computer, and the web.

### Setup

If you're using a Mac, there is no setup! It's already installed.

If you're on another device please either pair up with someone who is using a
Mac or reach out to your coach and they'll pair you up.

### Usage

VoiceOver is going to take some getting used to, but it's a great way to put
yourselves in the shoes of your potential users, so your persistence will pay
off.

#### Getting Started

Macs also have a built in VoiceOver tutorial that is an excellent way to get
started.

* Open System Settings (or System Preferences on some older versions of MacOS)
* Go to Accessibility > VoiceOver
* Click on 'Open VoiceOver Training'

The tutorial will take 15 - 20 mins. Be sure to take notes! 

#### Video Demonstration

This video, by Google, gives a nice demon of [how to get started with
VoiceOver](https://www.youtube.com/watch?v=5R-6WvAihms&t=600s&ab_channel=GoogleChromeDevelopers).

#### Cheat Sheet

You'll get a long way using a handful of VoiceOver commands, which we'll give to
you in these next sections - starting with the basics.

##### Basics

Go to one of your chosen sites, start VoiceOver and try these commands:

* `VO + right arrow` - moves you along the page, **left to right**, and **then
down** to the next row and so on
* `VO + right arrow` - moves you along the page, **right to left**, and **then
  up** to the next row and so on
* `VO + space` - clicks on things, like buttons, links, checkboxes and so on
* `VO + shift + down arrow` - interact an element, such as a dropdown menu`

##### Advanced

Now, try these commands:

* `VO + command + H` - will jump you from heading to heading, which is commonly
used to get an overview of new pages
* `VO + U` - opens the 'rotor', which is a set of lists, containing things like
headings and tables, that can be used to navigate, quickly and efficiently,
around the page

##### Voice Controls and Settings

These might be useful too:

* `control` - interrupt VoiceOver
* `VO + command + up arrow / down arrow` - turns VoiceOver speed up / down

## Challenge: VoiceOver

This is a process feedback challenge. For this challenge, you will be submitting
a video, but not of your "live" testing and usage of VoiceOver. You'll be
creating a recording you make after you've finished testing.

* Use VoiceOver to navigate both the inaccessible and accessible versions of the
  [City Lights site](https://www.w3.org/WAI/demos/bad/before/home.html).
* Make notes on your experience of both.
* Now, start a video recording and talk through your findings and reflections on
  the testing you've just done. Use the questions below to guide your
  reflections, making sure to talk about each of them. N.B. your coaches are not
  expecting you to need to make a very long, in-depth video! As a guide, spend
  no more than 5 minutes on each of the questions.

1. What makes the inaccessible version of the site more difficult to use?
2. Could you have predicted the outcome based on the appearance of each version?
3. Did you notice any defects that were not identified by WAVE/Lighthouse?
4. What are the differences and similarities between "accessibility testing" and
   "usability testing"?

[After you're done, submit your
recording](https://airtable.com/shrNFgNkPWr3d63Db?prefill_Item=et_as03).

[Next Challenge](04_extensions.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase3%2F03_tooling.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase3%2F03_tooling.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase3%2F03_tooling.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase3%2F03_tooling.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase3%2F03_tooling.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
