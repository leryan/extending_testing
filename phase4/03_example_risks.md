# Example Risks & OWASP

The Open Web Application Security Project (OWASP) Foundation is a non-profit,
community-led foundation that works to improve the quality of software for web
applications.

The OWASP Foundation regularly discusses the latest security risks, provides
tools to help security testing, and provides things like networking, training
and conferences.

## Top 10

Periodically, the foundation publishes a new "[OWASP Top
10](https://owasp.org/www-project-top-ten/)", listing the ten most critical
security concerns at the time of writing, for web applications.

At the time of writing, the most recent Top 10 was produced in 2021 (the
previous being 2017, if you want an idea of cadence) and was compiled from
various different organisations and groups. It's designed to both give insight
and raise awareness, but isn't (and can't!) be an exhaustive list. Reviewing
your application against the Top 10 is a very worthwhile activity, but it's not
the end of the story.

Along with the ten listed security risks and potential exploits, the Top 10 also
includes remediation strategies in order to help developers prevent or lessen
the dangers. While it's less likely that remediation will be the tester's duty,
being aware of how the exploits are being addressed can be just as useful as
understanding the exploits in the first place.

We'll look at number one on the list first, then leave you to read through
another example on your own.

### Broken Access Control

Up from 6th place in 2017, the number one security risk for web applications in
2021 was determined to be "Broken Access Control".

Let's start by thinking about an example. Say you had a website such as
`https://some-company-site.co.xyz` where a user could look at their own
*private* details on a URL such as
`https://some-company-site.co.xyz/users/myusername`. If by just changing the URL
to something else such as `https://some-company-site.co.xyz/users/someoneelse`
one user could immediately view another user's *private* details, that would
show that the **access control** of the web application was broken.

Access control is designed to do what it says: control access. If the
application allows one or more users - malicious or otherwise - to access
content which they shouldn't be allowed to access, the controls are failing.

The recommendation is that applications should be striving towards something
which is called the "[Principle of Least
Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege)". This
principle, often called "PoLP", states that users should only have access to
information and resources for which there is legitimate need. In the example
scenario above, we've clearly violated that as users can see other users'
private details.

The Broken Access Control security risk is a lot more than just hand-crafting
URLs - situations where users can make themselves administrators ("elevation of
privilege") or where users can make or modify requests to do things without
authenticating, also come under that same security risk.

From a testing point of view, we now have at least these three simple takeaways
which we could consider trying next time we're testing a web application:

* Does the URL contain anything specific to this user and, if so, can I change
  it myself and browse to a URL I shouldn't be able to see?
* Am I able to change my permissions to that of a user with a higher level of
  control, like an administrator?
* Is there anything in the request or response data that looks like it could be
  modified, in order to trick something into thinking I'm someone else or have
  different levels of permissions?

You can read more about Broken Access Control
[here](https://owasp.org/Top10/A01_2021-Broken_Access_Control/), along with
other examples and mitigation strategies.

### Another Example

Review the OWASP Top 10 yourself - pick a number (from 2 to 10 inclusive) and
spend no more than half an hour reading up on what OWASP says about that
security risk, and doing some researching and reading of your own from other
sites you can find. Ask yourself questions such as:

* What is the vulnerability?
* What is the risk i.e. what's the potential fallout?
* What are the mitigation strategies?
* What news articles or other pieces of information exist relating to that
  security risk or real world examples of that vulnerability being exploited?
* Do I have an improved understanding of the sorts of things to look for, to keep
  in mind or to try to do, when testing a web application?

Share your findings with your pair or someone else in your peer group/cohort and
see what their research on another one of the OWASP Top 10 has uncovered.

## Disclaimer

It's not the case that OWASP and its security risks, tools and resources is
*everything* there is to security testing. However, it is a really good starting
point on your journey to being better equipped and having a better understanding
of what risks are out there.

[Next Challenge](04_testing_tools.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F03_example_risks.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F03_example_risks.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F03_example_risks.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F03_example_risks.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F03_example_risks.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
