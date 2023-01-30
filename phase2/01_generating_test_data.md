# Generating Test Data

In the software development modules at Makers, unit tests are written as part of
test-driven development. Given the use cases, examples and other ideas a
developer may have, a selection of tests are crafted and unit tests implemented
(one by one) to *check* core pieces of code functionality, such as a method's
output.

It's OK crafting a few test cases by hand such as one might do during TDD. When
the number of test cases you might want to try means creating the test data will
take a long period of *time*, or even the type of data starts to become
*complex*, we need to turn to more automated solutions.

## Time

### Problems

Hand-crafting data works up to a point - when there are specific inputs or small
numbers of combinations of inputs to try, it can be tractable to manually create
the test data.

When the size of the input or combinations increase, test data creation can
quickly get out of hand.

For example, let's say you had Makers' postcode of `EC2A 4HJ`. If you were asked
to create a list of postcodes with the same "outward code" (`EC2A`) for some
reason, hand-crafting all of these wouldn't be a good use of your time and
effort:

* `EC2A 0AA`
* `EC2A 0AB`
* `EC2A 0AC`
* ...
* `EC2A 9ZZ`

> Number of postcodes: 10 * 26 * 26 = 6760

### Solutions

Using scripts to generate test data can be incredibly powerful and save you a
lot of manual effort. For the problem above, it's not too much effort to
generate those postcodes - here's one possible way:

```python
alphabet_upper = list(map(chr, range(65, 91)))
for n in range(0, 10):
    for c1 in alphabet_upper:
        for c2 in alphabet_upper:
            print("EC2A " + str(n) + c1 + c2)
```

### Exercise

In this scenario, imagine you're a malicious person who has hacked into a
company and stolen a bunch of details, including some source code used for
checking whether an entered password is correct for a given user, and a bunch of
data relating to those passwords that had been stored in a database.

> Doing the above would be against the law and you should **never** break the
> law. Hacking into systems, theft, and attempting to acquire passwords is
> unlawful and unethical.
> 
> We're going to demonstrate how to use automation to brute force a situation
> which we could've done by hand, but very slowly. We're using this
> hypothetical, malicious user example both because it illustrates the point,
> but also hopefully reminds you of the importance of keeping password-related
> data safe.

The [stolen script](./01_resources/password_handler.py) is available for you to
use (and read, if you want to - it won't really help you with this exercise).

Given you have the script, it appears that you can generate strings, e.g.:

```python
>>> output = hide_password("password1")
>>> output
b'\xd5\xf9\xdf0I\xde\tg\xb1m\x8e\xf9\x03\xdd1\xc0<\x1a\xba\xf7\xbd7\xe0t:N\xe1\xd3@\xbdS\xd7'
```

and also check whether you've given a password that, when "hidden", matches
another value:

```python
[...]
>>> check_password(output, "password1")
True
>>> check_password(output, "myguess")
False
```

You also know that the requirement the company imposed was for simple,
4-character passwords made up of lower case letters or numbers (e.g. `foo0` or
`9yz1`).

> N.B. This is not a good situation, choice of secret key (see inside the
> script), password restriction, nor a way of encrypting a password, so please
> don't use this approach to writing password handling scripts in the real
> world!
> 
> If you wanted a more secure method, something like
> https://cryptography.io/en/latest/ would be safer, but you should always fully
> check and understand any requirements of systems where you're asked to e.g.
> encrypt data. Don't use this example for anything serious - it's intentionally
> poor.

Along with the stolen script, you have also acquire values that were stored in a
database which are those "hidden" passwords, like this particular one:

```python
b'$\xed\xb8v\x10\x1f\xe2\xa6\xc2\x0f\xaf[\x98|\xc7\x84l\xe1H\x02"\xed\xbf\xde\xd7>/;.\x9bI\xdf'
```

While you *could* spend a few hours guessing the password that was originally
used, got "hidden" and stored in the database with the value shown above, by
manually typing things like:

```python
>>> check_password(b'$\xed\xb8v\x10\x1f\xe2\xa6\xc2\x0f\xaf[\x98|\xc7\x84l\xe1H\x02"\xed\xbf\xde\xd7>/;.\x9bI\xdf', "0000")
False
```

try generating your own data to determine what the original, user-entered string
was which got stored in the database in this way.

If you're not sure whether you've got the correct answer, check with someone
else in your cohort/peer group who has already done the exercise, your coach if
you're the first one through it!

<!-- OMITTED -->

## Complexity

### Problems

Similar to the time problem above, it's also possible that the input data is
either exceptionally large or doesn't have a finite number - for example, there
are a massive number of possible addresses in the UK, and an infinite number of
possible contents a text file could contain. While it could be possible to
generate the former - and impossible to generate the latter - attempting to do
so might produce so much data that it wouldn't be tractable or pragmatic to test
with all of them, anyway.

Sometimes, randomly generating a sample set of test data can be useful. For
example, perhaps you're looking to seed (set up) a database with thousands of
names and addresses to create something closer to a real world scenario, so that
you can test with this rather than an empty database. Alternatively, perhaps you
want to generate a range of different possible addresses to check whether a
system which validates UK addresses is returning appropriate answers, and a
randomly generated set of test data helps give you more coverage than what you
could craft by hand.

### Solutions

Using scripts to generate suitable, usable test data comes in again here. Like
before, when we were considering all of the combinations of a particular
postcode, we could fairly easily generate some random postcodes, albeit here in
only one of the [possible
formats](https://en.wikipedia.org/wiki/Postcodes_in_the_United_Kingdom#Validation):

```python
>>> import random
>>> alpha = list(map(chr, range(65, 91)))
>>> def make_postcode():
...     random.choice(alpha) + str(random.randint(0,9)) + " " + str(random.randint(0,9)) + random.choice(alpha) + random.choice(alpha)
... 
>>> make_postcode()
'K6 1JD'
>>> make_postcode()
'P1 8JH'
```

Generating - and then using - all of these postcodes would produce more data
than would be tractable and pragmatic to test with. By generating some
acceptable quantity of postcodes, probably in each of the possible formats
linked above, we could use that sample set of postcodes to give us:

* coverage across the different possible postcode formats,
* and some increased confidence that postcodes matching those formats are
  acceptable/etc. in the program we're testing.

Whether the postcodes are valid and apply to real addresses or not, is another
question, but it's not too tricky to find out that `Z0 0ZZ` isn't a real UK
postcode. We'll look more into the "fakeness" of this data in the next section.

### Exercise

In this scenario, imagine you've been tasked with checking [National Insurance
Numbers](https://en.wikipedia.org/wiki/National_Insurance_number#Format) against
some UK Government system that's doing a look-up for whatever a user types in.

You need to create a text file of 1000 randomly generated, valid National
Insurance Numbers. For the purpose of this exercise, they should either match a
format such as `QQ 12 34 56 C` or `QQ123456C`. A random selection of both might
be advisable, since both formats should be acceptable by the system.

Notes:
* There will be a few special cases you need to handle, including what the
  letters at the start and end can't be.
* There is no need to generate things like Temporary Numbers or Administrative
  Numbers (see other sections in the above link) - just generate ones meeting
  the standard format.
* You don't need to consider invalid National Insurance Numbers (e.g. `12 AA BB
  CC`) in this exercise, just valid ones.
* It should be clear by now that you'll be scripting the production of the test
  data, not manually creating it! We'd advise using Python again here, but it is
  up to you. Your script should also be writing that data to a text file rather
  than, let's say, you copying it from what's printed to a terminal. If you
  don't know how to write to a file, now is the time to learn that and to get it
  working - you'll need to do it again, later.

We'll look at some more solutions for the problem of complex test data in the
next section.

[Next Challenge](02_fake_data.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F01_generating_test_data.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F01_generating_test_data.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F01_generating_test_data.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F01_generating_test_data.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F01_generating_test_data.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
