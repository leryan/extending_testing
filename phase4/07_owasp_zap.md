# OWASP ZAP

The OWASP Foundation also provide a tool which can be used during security
testing called OWASP ZAP, standing for "Zed Attack Proxy".

## Proxies

You may or may not have encountered proxies or proxy servers before - if you
know what a proxy is, such as used in HTTP communication, feel free to skip
through this section on Proxies, straight through to talking about ZAP.

A proxy or proxy server is an intermediary between a client making a *request*
and a server which receives that request and sends a *response* back to the
client. You'll have seen these client and server entities in the Web
Applications module, where your browser acted as the client and there were
various servers sending data back to your browser, depending on what you'd
clicked on or entered.

A proxy therefore sits somewhere between the client and server directly along
the line of communication. A client-side proxy would be something configured on
the client's side - configured in the browser, for example. A server-side proxy
is the other way around, configured on the server's side.

Client-side proxies can be configured to do a number of different things, from
keeping you safe to preventing you from visiting certain sites.

## ZAP is a Proxy

The "Zed Attack Proxy" (ZAP) is indeed just that - a proxy - and your browser
can be configured to use ZAP for some or all outgoing requests. We'll run
through the following steps:

* Download and install ZAP
* Configure your browser to use ZAP as its proxy
* Visit some sites and see the requests/responses in ZAP

### Download & Install ZAP

You can either visit https://www.zaproxy.org/download/ to download and install
an appropriate version of ZAP, or if you're using brew you can just run `brew
install --cask owasp-zap` in a terminal.

After installation on a Mac, you may need to go into the System Settings to
permit ZAP to be considered safe to run.

Once you're able to start ZAP, do so. You will be asked a question about whether
you want to "persist the ZAP session" - just check "No" and move on. ZAP is now
running, but not doing anything useful just yet as there's more to configure.

We will need to generate a CA (Certification Authority) certificate so that our
browser trusts ZAP as a proxy later on, and also check a particular setting.

* Go to Tools -> Options -> Network -> Local Servers/Proxies
* Check/set the Address to `localhost` and port to `8080` - if you choose a
  different port, perhaps because 8080 is in use by something else, make a note
  of it and use your chosen port later on when configuring the browser
* Go to Tools -> Options -> Network -> Server Certificates
* Click `Save` to save the Root CA Certificate somewhere you can find it later
  on

### Browser Configuration

Next, we'll be configuring a browser to use a proxy. There's a small "gotcha" we
need to explain first:

> Many modern browsers don't have their own settings for configuring a proxy,
> instead relying upon an operating system-level configuration. Changing that
> setting would change all outgoing requests, to all sites, to go via that
> proxy!

For testers, this is not necessarily the most helpful situation as you may want
to treat your `browser -> proxy -> server` test setup separately to your
recording of tests and normal work like web browsing or responding to emails.
Given that, we suggest using Firefox at this stage, since Firefox has its own
proxy configuration setting rather than using the operating system's one.

If you don't already have it installed, go and [install
Firefox](https://www.mozilla.org/en-GB/firefox/new/) now.

In Firefox's settings, find Network Settings to "*configure how Firefox connects
to the internet*". Open that up and set:

* `Manual proxy configuration` radio button
* HTTP proxy to `127.0.0.1` and Port to `8080`
* Then check `Also use this proxy for HTTPS`
* Finally, `OK` to save the settings

Next, we'll need to configure Firefox to trust the certificate from ZAP which we
saved earlier. In Firefox's settings, find Certificates and the View
Certificates button to open the Certificate Manager. Import the `.cer`
certificate file you saved earlier on, checking both `Trust this CA...`
checkboxes and finally `OK`.

Lastly, we will need to convince Firefox that we want to use a proxy to
connections to our own machine i.e. localhost or 127.0.0.1. This is a setting
that's hidden away with various warnings about changing it - if you're concerned
or use Firefox as your main browser, it's OK to go with it for now, you can just
reset the configuration later on. We have a note further down the page about
that, to remind you.

* In Firefox, enter `about:config` into the URL and open that page
* Click to accept the risks and continue
* Search for `network.proxy.allow_hijacking_localhost`
* Double-click on it to change it to `true`

### Using ZAP

You're now all set to use ZAP as a proxy in Firefox!

In Firefox, browse to any website of your choosing. You may find a "Welcome to
the ZAP HUD" page displayed - if so, click to "Continue to your target". You
should now be on the site you wanted to see - so far, so normal.

Switch back to look at ZAP and you should see one or more "Sites" listed on the
left hand side, and a bunch of timestamped things in the panel at the bottom. If
so, that's ZAP noting all the traffic that is going through it as a proxy
(outgoing requests from Firefox, incoming responses) and displaying it to you.

If you don't see this information, recheck you've done the steps above, then
consult with others on your cohort or contact your coach(es) for help.

## app.js

In a previous section, we looked at `app.js` with its vulnerable header which
was revealing more information than we needed to reveal.

We'll now use ZAP in order to show us what we already know - that the header in
app.js is a security risk and needs mitigation!

* Close all your tabs in Firefox so that you just have a "New Tab" tab open.
* In ZAP, go to the File menu -> New Session - there's no need to save anything
  and like before, check "No" to persisting the session.
* In the bottom panel, switch to show "History". There won't be anything there
  yet, as this is a new session and Firefox isn't making any requests yet.
* If app.js isn't still running from before, run `node app.js` again so that it
  is now running.
* In Firefox, browse to http://localhost:3000 - you should see "Hello World!"
  displayed again, with no difference to what the browser shows compared to
  before.

Now take a look around in ZAP - under "Sites" you should find that same
http://localhost:3000 URL and under "History" should be a single GET request to
that URL. If so, congratulations! Not only is everything configured correctly...
but ZAP has identified some problems - take a look at the "Highest Alert" column
at the bottom, which should say something like "Medium".

ZAP is telling you that the request and response that it observed going through
it when you visited that page contains at least a Medium-level concern according
to its own rules and what it looks for. We haven't done anything particularly
extensive here, just browsed to a page, and ZAP is automatically *scanning*
what's going on and giving feedback that there are problems we could/should/must
investigate. If you look along the toolbar at the very bottom of ZAP, you should
see "Alerts" and some flags with numbers - this is the total number of
alerts/problems ZAP has found from just that one event.

Let's take a look at what ZAP found.

### Reporting

From ZAP's menus choose Report -> Generate Report ... -> then leave all the
settings as they are and Generate Report. A new page should be opened in a
browser (your default one, not necessarily Firefox) showing a "ZAP Scanning
Report".

Take some time to read through the report. Can you see anything in here that
looks familiar?

<details>
  <summary>Click here once you've read through the report, particularly if you can't see anything that looks familiar</summary>

In the ZAP Scanning Report, ZAP has listed at least one Low-level issue called
"Server Leaks Information via "X-Powered-By" HTTP Response Header Field(s)" -
that's the same header we looked at earlier!

Clicking through from that issue takes us to
https://www.zaproxy.org/docs/alerts/10037/ which mentions:

* A summary about why it's a problem, i.e. information that might help attackers
* A solution about how to prevent it by suppressing that header, which is
  exactly what we did earlier on
</details>

> There are other ways to view the Alerts ZAP has identified, like the Alerts
> tab in the bottom panel. In this section, we're using Reports as they're more
> convenient.

If you're interested, feel free to read around any other interesting issues ZAP
found in that one application and request, that seemed like it should be so
simple and hence so secure when it was first written.

### Passive vs Active

What you've done above is to use ZAP in a **passive** scanning manner, simply
inspecting data that passes through, without modification nor ZAP doing any
requests of its own.

ZAP also allows for **active** scanning - attacking - where ZAP will make its
own requests and decisions, based on rules you give it and its own knowledge of
potential security vulnerabilities and exploits it may be able to use.

**It's the active mode that requires the utmost caution, so tread carefully and
don't attack something you shouldn't.**

### Exercise

You've now used ZAP once to scan some HTTP communications and have found a
number of issues. In this exercise, you'll go back through some of the steps to
re-run the test but on a patched version of app.js with the `X-Powered-By`
header suppressed.

Feel free to work through that on your own but if you want some guidance, here
are our suggested steps:

* Stop NodeJS
* "Fix" app.js for the `X-Powered-By` vulnerability (either method)
* Start NodeJS
* New ZAP session
* Re-run the test
* Generate a new scan report
* Verify your fix from earlier

> Note: if you see an error such as "Exception evaluating `OGNL` expression" when
> generating the scan report, try deleting all unrelated "Sites" in ZAP
> (right-click and Delete) before attempting to regenerate the report.

### Exercise - Extension

If you're comfortable with the steps above and making modifications to app.js,
and *if you have time*, you can try to keep fixing app.js to see if you can get
it to have zero alerts of any level. There are links from each report you
generate that explain the problems and mitigations, which might give you enough
information to make fixes.

<details>
  <summary>Need a hand with the other issues you've already seen in the first report?</summary>

Along with `removeHeader()` you can also use `setHeader()` to set/add headers to
requests.
</details>

Don't spend more than an hour working on this extension though - set yourself a
time box and stick to it, before moving on to the next section where you'll get
to use ZAP and do even more security testing, on a much more complicated program
than app.js.

## Resetting Firefox

If you want to restore Firefox's configuration for any reason, there are the
things below to revert. Note that you might want to consider delaying making all
of these changes, since you will be using Firefox & ZAP more later on.

If you want to undo the settings made earlier:

* Revisit `about:config`, accept the risks, search for
  `network.proxy.allow_hijacking_localhost` and double-click to change it back
  to `false`
* In Network Settings, select the `No proxy` radio button
* In Certificate Manager, delete the accepted "OWASP Root CA" certificate

[Next Challenge](08_juice_shop.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F07_owasp_zap.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F07_owasp_zap.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F07_owasp_zap.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F07_owasp_zap.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F07_owasp_zap.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
