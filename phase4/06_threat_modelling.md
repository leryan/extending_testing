# Threat Modelling

Threat Modelling is the process by which a system or application is
systematically analysed to identify potential vulnerabilities and assets that
might be valuable to attackers, followed by the prioritisation of mitigation
strategies.

It should be obvious by now why threat modelling is a potentially valuable
activity - any time we can reveal more information about how our application is
behaving (or misbehaving!) that empowers us and our stakeholders to make
better-informed decisions about what to do about the risks and how to improve
quality.

If you read more around threat modelling, you may see references to a
four-question framework which suggests following these four questions:

* What is it we're modelling? (scope)
* What are the vulnerabilities? (see Methodologies, below)
* What can we do about them? (mitigations)
* How well did we do? (retrospection / validation)

Much like testing, threat modelling can be done at any time and there are
benefits from including the process earlier in the SDLC, and doing it
continuously throughout.

## Methodologies

The process of threat modelling comes from particular methodologies, of which
there are quite a few. One of the more famous ones was introduced back in 1999
by Microsoft, called **STRIDE**.

STRIDE is a mnemonic:

* **S**poofing (pretending to be someone else)
* **T**ampering (modifying in a harmful way)
* **R**epudiation (authenticity)
* **I**nformation disclosure
* **D**enial of service
* **E**levation of privilege

At least one of these will be familiar as we've just covered "E", for elevation
of privilege, but you're probably also heard of denial of service ("DoS")
attacks in the news or maybe popular culture and can guess what information
disclosure might be about. The mnemonic is designed to help you think about and
identify threats in a system - it's much like the test heuristics cheat sheets
you were given in an earlier module, where you could choose to think about each
of them in turn.

As before, STRIDE is just one methodology and there are others such as VAST and
PASTA which have different uses and approaches. The methodologies tend to have a
particular focus from these:

* `asset-centric`
* `attacker-centric`
* `software-centric`
* `value` and `stakeholder-centric`
* hybrid (of the above)

For example, PASTA takes an `attacker-centric` view of the application, and
attempts to do `asset-centric` mitigation.

## Terminology

You might be thinking this "what could go wrong?" type of question sounds
familiar, and perhaps are wondering whether "threat" is another term for "risk"
and how "modelling" differs from "assessment". Put simply: is threat modelling
just risk assessment?

The quick answer is that it's part of risk assessment but is its own specific
thing. Threat modelling is a process which looks at *threats to data* at a
system or application level, and that activity does involve similar sorts of
questions around the dangers or risks.

You may also hear the term "security risk assessment" as well, and while that is
part of the more general "risk assessment", it's still a separate activity to
threat modelling. For example, threat modelling could/should be done at any
time, but certain things need to exist before a security risk assessment can be
carried out (e.g. understanding of assets, how risks should be evaluated).

# Example Application

We're going to look at a very simple application with around 10 lines of code.
With it being so short, *surely* nothing could go wrong?!

## Setup

In a terminal, with a clone of this repository, navigate to this phase's
[resources folder](./resources/) and firstly run:

```
npm install express
```

(if express isn't yet installed - you'll soon find out), then run:

```
node app.js
```

to start the app.js application.

You can now browse to http://localhost:3000 in something like Firefox or Chrome
and you should see "Hello World!" displayed. This is the first of our 4 Threat
Modelling questions above - we're just working on app.js, which is a very simple
web application.

Let's now move on to the next question - what could go wrong? With something so
simple, it might be tempting to conclude that there aren't any issues but even
this application illustrates an unfortunate vulnerability.

Using your browser's Dev Tools, find the HTTP GET request that was made when you
browsed to the page the application is serving. Take a few minutes to do that,
and look through the request headers, response headers and response body.

Once you've done that - read on!

## Investigation

In the response headers you're able to inspect through the browser's Dev Tools,
you may have noticed this header:

```
X-Powered-By: express
```

This single header tells us what server we're using - express - which **we**
already know from looking at the code. The problem is that it reveals the same
information to a hacker who doesn't have access to the source code. We don't
know how they might use that information and the potential damage that knowledge
could cause.

The rule we've seen before is the Principle of Least Privilege and it applies
here. There is no legitimate reason for users to have this information, so it's
something we should not be revealing and a risk we should not be taking.

## Mitigation

We have at least two possible mitigation strategies here, focusing on making
sure that response header is not sent, revealing information about our server.

We could add the following line, just before `res.send()`:

```
res.removeHeader('X-Powered-By')
```

This would mean that the X-Powered-By response header is removed from `res`
before we send the response, which would fix our immediate issue.

The problem with this simple approach is that as soon as we create a different
route within our application, we might forget to remove that header on a
response that's built and sent there as well.

Alternatively, we could add the following line, after we have defined `app`:

```
app.disable('x-powered-by')
```

This would mean that the `app` object has the whole concept of X-Powered-By
headers disabled from the start, and so would be a more general fix and probably
a safer one in our situation.

Make one of those changes now to app.js, remembering to restart `node` after you
make a change. Refresh the page in the browser and check - has that header, and
that vulnerability, now been resolved?

## Wrap Up

Stop running `node` and revert any changes you made to app.js. We'll shortly
want to reuse our same vulnerable application to demonstrate another security
testing tool, so we want the X-Powered-By header to be included once again.

[Next Challenge](07_owasp_zap.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F06_threat_modelling.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F06_threat_modelling.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F06_threat_modelling.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F06_threat_modelling.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F06_threat_modelling.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
