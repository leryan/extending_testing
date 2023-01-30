# Equivalence Partitioning

Continuing with our example from the previous section where we had a sign-up
form and later on a login page, let's think a bit more about the password field
on the sign-up form.

Let's assume that the password field's validation is checking for a few things:

<!-- OMITTED -->

* At least 8 characters
* Must contain at least one uppercase and one lowercase letter
* Must contain at least one number

and for now, let's also just think about what we might test when checking for
valid passwords.

If I started with password of `ABCDabcd1`, which I'd expect to be valid
according to the restrictions above, how valuable would it be to next try
testing with a password of `ABCDabcd2`?

It's accurate to say that it's a different password, but we might question
whether there's much value in testing something with such a small change. If the
developer of the password checker for the sign-up form has made a sufficiently
long, with mixed-case, password work when the number "1" is in it, it's likely
to give the same outcome if there's a "2" in that same place instead.

We'd call those two passwords **equivalent** - they're not identical, but we'd
consider them equivalent and likely only test one of them.

If we had a whole set of many different passwords, we could make equivalence
partitions - groups of passwords which we consider equivalent. If the test
passes (or fails!) for one from a partition or group we've created, we think
it's highly likely that the test would behave the same way for all the others.

## Exercise - Valid Passwords

Partition the password test cases below into groups which are equivalent, and
hence from which you'd only want to test with just one. Note that a group might
only have one password in it, there may well be other groups which would be
valuable to try that aren't covered here, and there isn't only one answer!

* `ABCDabcd1`
* `1ABCDabcd`
* `ABCDabc1`
* `ABCDabcd2`
* `Aa1234567`
* `ABCDabcd0`
* `A1111111a`

<details>
  <summary>Click here once you've created your partitions.</summary>

One partitioning of the above passwords might be as follows:

```
>1 upper, >1 lower, 1 number: ABCDabcd1, ABCDabcd2, ABCDabcd0, ABCDabc1

Same again, but starts with a number not a letter: 1ABCDabcd

1 upper, 1 lower, >1 numbers: Aa1234567, A1111111a
```

Do you agree with the answer above? Maybe you think 0 could be a special case
(perhaps the developer for some reason only accounted for 1-9), or maybe you
think starting with a number and ending with a number are like to give the same
behaviour...

Would you have the password with just 8 characters as its own group...? (More on
this in the next section!)
</details>

Lastly on the valid passwords, ask yourself - is there a group that's missing
for which we've currently got no passwords?

<details>
  <summary>Here's at least one idea we think is missing.</summary>

A longer password would be worth checking as well. If there's nothing in the
form stopping the user from typing a very long value, some user somewhere at
some point in time will try it. If our developer wrote the code to only expect,
say, 32 characters at most then we might be on our way to finding a bug.
</details>

## Exercise - Invalid Passwords

Next, on your own, take a few minutes to think through some password test cases
which we'd expect to be determined to be invalid. Write them down and try to avoid
equivalent passwords - if you write one down that's equivalent, that's OK, just
group it with any others and keep going.

Once you're done, have a look at how many different groups you created. If you
tested just one invalid password from each, how **confident** would you be that
the password checker is correctly identifying invalid passwords? If you're not
that confident, ask yourself why - what might you be missing?

These sorts of questions around confidence and "what else could I check?" are
useful ones to practice asking yourself. Sometimes your gut could be telling you
something... and it's often worth pausing, paying it some attention and having
another moment to think.

<details>
  <summary>Once you've got some equivalence partitionings of invalid passwords put together, you can take a look at our thoughts on the exercise.</summary>

Noting once again that there's no single, correct answer to this, our approach
was as follows:

* Look at and test each of the rules separately:
  * At least 8 characters
  * At least 1 uppercase
  * At least 1 lowercase
  * At least 1 number
* For the first, anything less than 7 should be the same, but 0 characters could
  be worth including as a special case
* For each of the other three, it's when there are 0 of that type of character
  present
* Create passwords that are otherwise valid, satisfying all the other rules
  apart from the one rule we're testing
* Create passwords that don't satisfy >1 of the rules at the same time e.g. too
  short and no numbers

Our suggested partitioning:

```
0 characters: i.e. ""

7 characters: e.g. 12345Aa, ABCDEa0

0 uppercase: e.g. 1234abcd, abcdefghijklm1

0 lowercase: e.g. 1234ABCD, A1234567890

0 numbers: e.g. ABCDabcd, Aabcdefghijklm

Multiple problems: e.g. 1, ?!£$%^&*()-=, ?
```
</details>

[Next Challenge](03_boundary_values.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F02_equivalence_partitioning.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F02_equivalence_partitioning.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F02_equivalence_partitioning.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F02_equivalence_partitioning.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F02_equivalence_partitioning.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
