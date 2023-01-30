# Decision Table Testing

In situations where we have different inputs and those inputs can have different
values, or at least groups of values we could consider, we can rapidly get a
combinatorial explosion of possible test cases.

Even with our old friend, the email and password scenario, the login page for
confirming whether a given email and password are correct can become complicated
quite quickly.

While we might have started off thinking about just two cases, for a given
user's email address:

* invalid password
* valid password

(and the interesting test cases that make up "valid" and "invalid" groups to
test), when we add into the mix whether the email address has already been used
to sign up, we're already at these combinations on the *login page*:

* invalid password + signed-up email address
* invalid password + unknown email address
* valid password + signed-up email address
* valid password + unknown email address (?)

(The fourth is an interesting one - valid password in what sense? Is it that
it's valid for some email address, but just not the one that's specified?)

If we then consider that the fields on the login page could be valid, invalid or
blank... well, we're now at nine different combinations and they might not all
be valuable to test separately from each other. You might notice that there's
some overlap here with equivalence partitioning.

If we start to write out the full table, we can also include our expectations
and probably a blank column for what we later actually observe:

| Email address | Password | Expected Outcome | Observed Behaviour |
|-|-|-|-|
| Signed-up | Valid | Log in |  |
| Signed-up | Invalid | Invalid password |  |
| Signed-up | Blank | Invalid password |  |
| Unknown | Valid | Failed to log in |  |
| Unknown | Invalid | Failed to log in |  |
| Unknown | Blank | Failed to log in |  |
| Blank | Valid | "Email must be specified" error |  |
| Blank | Invalid | "Email must be specified" error |  |
| Blank | Blank | "Email must be specified" error |  |

By thinking through the combinations and writing them out, we're less likely to
miss combinations that might have been valuable to consider and potentially
test. If we know the number of combinations, we can quickly count the table's
rows. When the combinations (and columns) increase, the planning becomes even
more important.

The tabular format above is also helpful both for the tester (planning and
noting down observed behaviours as they test) but can also form part of a
report, perhaps to stakeholders reviewing the outcomes from a test activity.

## Refining

Continuing with our table above, we might consider that some of the rows aren't
worth testing separately. For example, the last two rows are highly likely to be
the same sort of test, as invalid and blank passwords when there's no email
address specified are likely to produce the same outcome and use the same logic
in the code. So, we would probably only test one of those cases.

Although it would depend on the product, stakeholders and users' needs, it might
be preferable not to give any hints to users logging in as to whether they've
specified a valid email address. For example, whether or not an email has
previously been used to sign up for a site is often considered private
information! Our table might start to change, both from us removing rows we
don't consider interesting to test, and based on different outcomes. Perhaps we
might end up with something like the following:

| Email address | Password | Expected Outcome | Observed Behaviour |
|-|-|-|-|
| Signed-up | Valid | Log in |  |
| Signed-up | Invalid | "Invalid email and/or password" error |  |
| Unknown | Valid | "Invalid email and/or password" error |  |
| Unknown | Invalid | "Invalid email and/or password" error |  |
| *any* | Blank | "Password cannot be blank" error |  |
| Blank | *any* | "Email must be specified" error |  |

Whether we'd want to drop one of the third and fourth, "Unknown" email address
cases, might be a tricky decision. Sometimes, if the test is cheap (cost/time),
it's probably worth doing, and quicker to do than debating the pros and cons of
taking it out.

[Next Challenge](05_state_transitions.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F04_decision_tables.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F04_decision_tables.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F04_decision_tables.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F04_decision_tables.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F04_decision_tables.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
