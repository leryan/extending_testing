# Selecting Test Cases

As you already know, it's not possible to test **everything** in a product, but
even once you've chosen a subset of areas to test, it's not always pragmatic or
possible (e.g. due to time) to run **every test** either.

> Say you were staring at a few million possible values for input X and a few
> more million for input Y, and you can test them in combination... how do you
> start to hone in on the more important values for X and Y to test them in
> combination?

We need some tactics when designing test cases in order to be efficient, but
also to make sure we're testing effectively and covering the important cases.

For example - if you were testing a sign-up web form which had an email and
password fields with some validation checks, you probably wouldn't just do:

* password: "a"
* password: "b"
* password: "c"
* ...

and so on. Not only are there too many possible inputs for email and password,
but you've got those in combination with each other as well. On top of that,
there are probably some interesting "special cases" we might want to consider,
like one or both fields being empty. Then, after we've signed up, there's
probably going to be some testing around logging in again with that same email
and password, logging out, and so on.

What we'd like to be able to do, is come up with a set of test cases which gives
us broad coverage of the functionality, includes the most risky
areas/inputs/etc., but that isn't too long and doesn't contain tests we could -
with some level of confidence - skip and not run at all.

The next sections will give you some guidance on how to achieve that.

[Next Challenge](02_equivalence_partitioning.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F01_selecting_tests.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F01_selecting_tests.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F01_selecting_tests.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F01_selecting_tests.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase1%2F01_selecting_tests.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
