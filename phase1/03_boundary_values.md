# Boundary Value Analysis

While there's obviously a *lot* more to test in the real world that just sign-up
and login forms, our password validation example is going to be useful for us
again here!

Let's briefly remind ourselves of the validation checks:

* At least 8 characters
* Must contain at least one uppercase and one lowercase letter
* Must contain at least one number

There are a lot of "at least" phrases in the above. Throughout your coding
journey, you'll have used or seen operators of `>`, `<`, `>=` and `<=` and may
at some point have tripped over using something like `>` when you meant `>=`.

(Human) errors such as these have a habit of cropping up in code, thereby making
it a risky area and one worth testing "around".

If we look at just the first condition for now:

* At least 8 characters

we can think of "8" as being our **boundary** and the thing around which we're
going to test. If we assume all the other conditions are met, the boundary
divides our password lengths into two partitions:

* Passwords with 8 or more characters => should be valid
* Passwords with 7 or fewer characters => should be invalid

so we already have two partitions and so we might consider checking passwords of
length 5 (too short) and 10 (sufficiently long).

This is good, and should catch bugs where the developer wrote completely the
wrong character limit into the code, but if they've written `> 8` rather than
`>= 8` those lengths of 5 and 10 wouldn't catch it. So, we make sure to include
values on and around the boundary.

For our password length checking piece of code, passwords of length 7, 8 and 9
would be really good ones to include.

## Other Boundaries

Any time there's some sort of "boundary", interesting test cases can show up. In
our password length checking piece of code, there's at least one other "edge
case" that's interesting and that's passwords of length zero - an empty field,
in the form.

Perhaps the developer didn't expect the password field to ever be left empty and
so either hasn't written code to handle it or wrote code that generates an error
when it is empty.

Similarly, as mentioned in the previous section, larger passwords can be of
interest too and it's likely that there's some upper limit on the password
length that can be entered.

Testing at the extremes, as well as interesting boundaries, can often be
valuable and a source of interesting bugs.

## Exercise

A developer has written a function in Python which can be used by different
sites popular to **teenagers**, to check whether a user is old enough to access
the content. The check is deliberately a simple one, just based on the user's
birthdate.

You can find the code in the accompanying [03_resources](./03_resources/)
folder.

You can run the code in the Python REPL and try out different birthdates and age
restrictions by steps like:

```
% python3 -i age_checker.py
>>> is_old_enough(2023, 1, 5, 13)
False
```

noting that the inputs to `is_old_enough()` are the *birth* year, month and day
(i.e. 2023 January 5th in the example above), then the age restriction - "13" in
the small example above, where a True response would mean the user was at least
13 years old and allowed to view the content, and False would mean they were
denied access.

As this is a boundary value analysis test - what might be interesting tests to
run, for the different age restriction use cases? First plan what tests you want
to run, then when you're happy with the plan, try them out.

Does the code work correctly, from what you can tell? If not, under what
conditions is it going wrong? What might your bug report say and/or reproduction
steps need to be, for it to be clear when it is going wrong?

Don't look at the Python code! (Even if you do, it might not help you much!) If
you are stuck, reach out to someone else in your cohort or your coach(es).

<details>
  <summary>Not at all sure where to start?</summary>

  The age restriction checker is designed for teenage websites, so we're looking
  at age restriction values of 13, 14, ..., 18, 19.
</details>

## Optional Extension

Cast your mind back to the wrap_it program from a few weeks back. Were there any
interesting boundary values that you happened to have tested during that
challenge? Did you find any interesting behaviour at those boundaries?

Feel free to get wrap_it running again and run some more tests if you'd like.

Can you identify any boundaries and, if so, what might the tests around those
boundaries be like?

<details>
  <summary>Once you've taken some time to think about boundaries and possibly run some new tests, click here to see boundaries we think are interesting.</summary>

Two boundaries of interest are as follows:

* Where the defined word wrap limit causes a break around the end of one word
  and the start of another word.
* Where the defined word wrap limit is around the total length of the input text
  that's provided.
</details>

[Next Challenge](04_decision_tables.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F03_boundary_values.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F03_boundary_values.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F03_boundary_values.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F03_boundary_values.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F03_boundary_values.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
