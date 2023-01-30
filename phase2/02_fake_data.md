# Fake Data

Fake data can be useful in a number of scenarios as a tester. Perhaps you want
to populate a database with thousands of realistic-looking data about users,
from names to addresses to phone numbers so that you're not testing a system
with an empty database. Perhaps you're testing a [text
mining](https://en.wikipedia.org/wiki/Text_mining) system that accepts large
documents of text, extracting pieces of information based on some other given
criteria.

While it's possible to write your own scripts to generate random, fake data, (as
we saw in the previous section) there are many existing ways out there which you
could more quickly use.

## Lorem Ipsum

A famous piece of text which can be used in documents is [Lorem
Ipsum)(https://en.wikipedia.org/wiki/Lorem_ipsum), sometimes used by printing
and typesetting industries, but also sometimes by testers who just need some
sort of valid-looking text.

There are many generators of Lorem Ipsum out there, producing content such as
the section below - take a few moments to find one and try it out.

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis
nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore
eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt
in culpa qui officia deserunt mollit anim id est laborum.
```

### Caution

Some generators of Lorem Ipsum try to be funny, inserting "real" words in
amongst the text, sometimes rude ones. While it's certainly not all of them and
the words might not be offensive to you, it's a useful moment in which to take a
step back and think about test data you're generating or using.

Much like cautionary tales of accidental Reply All email clicks or Forwards to
other people at later stages in a chain, meaning you should be sure what you're
writing in emails is professional at all times, it's possible for test data to
escape "into the wild". Inappropriately named vehicle registrations might be
funny internally, but when that data gets used to populate a live demo database
and presented to a customer who wants to track their fleet of hire cars, these
sorts of things can put a valuable deal at risk.

Similarly, before just jumping in and using some tool you've found out there
that randomly generates data you're going to use for testing, it's worth
checking that what it says it's doing is what you're getting. It's no good
adopting a UK postcode generating tool that misses out some of the valid formats
because it's become out of date or was badly written, especially if that means
you're missing some cases and aren't getting as much test coverage as you
thought... and claimed to stakeholders.

## Fakers

Tools called "fakers" are commonly available, including one for Python called
[Faker](https://github.com/joke2k/faker).

Install Faker, activate the environment and enter the Python REPL:

```python
% cd faker_example
% pip install Faker
Collecting Faker
  Downloading Faker-15.3.4-py3-none-any.whl (1.6 MB)
[...]
% pipenv shell
[...]
(faker_example) % python3
>>> 
```

You can now use Faker to create a Faker object and generate things like fake
names:

```python
>>> from faker import Faker
>>> fake = Faker()
>>> fake.name()
'Raymond Carrillo'
>>> fake.name()
'Rose Hood'
```

Make sure you're following those same steps, although you're highly likely to
see different names printed, then try out generating some "address" values
rather than "name" values for yourself. Do you notice anything about the
outputs?

By default, Faker has US-like output. Sure, the two-letter states are mostly
invalid, but the "fake" data is sufficiently close to the real thing that it
could be useful in some cases. Maybe you want to test an envelope printer just
to see what the quality of the print out is like?

Faker allows us to switch "locale". Try switching to something more relevant for
the UK, print some new names, then see how the output for addresses changes:

```python
>>> fake = Faker('en_UK')
>>> fake.name()
'Charles Holt'
>>> fake.name()
'Maria Wright-Rees'
>>> [...]
```

Generate a few more UK addresses and inspect them. Can you see any patterns in
the address data Faker is generating for UK addresses?

<details>
  <summary>If you don't know much about UK addresses, formats, etc. then click here for some help.</summary>

  Addresses in the UK can be different lengths - sometimes they can be as short
  as just three lines like:

```
DVLA
Swansea
SA99 1BN
```

  and sometimes they can be six, seven or maybe more! Faker is generating either
  three or four lines - along with the recipient's name like `Maria Wright-Rees`
  were we to add that in to our test data, that would mean addresses you might
  be testing with would all have either four or five lines... and that might not
  be sufficient. What if there was a problem with printing addresses longer than
  five lines?
</details>

### Seeds

While not something you necessarily need for the challenge later in this phase,
it's a good moment to look at "seeds" and the "randomness" that Faker provides.

Pseudo-random number generators can be initialised with a "seed" value. This
seed value determines the starting points for the generation of random data and
if the same value is used again as a seed, the same sequence of random data will
be generated.

Python's `random` library can be given a seed - let's take a look at that now:

```python
>>> import random
>>> random.random()
0.3553105192680218
```

Try this yourself - go into the Python REPL and type the two lines above. You're
very likely to see a different random number, because the starting seed will be
different to that of the author of this page.

Let's now give it a particular seed value - a starting point for the
pseudo-randomness - instead:

```python
>>> random.seed(1)
>>> random.random()
0.13436424411240122
>>> random.random()
0.8474337369372327
>>> random.seed(1)
>>> random.random()
0.13436424411240122
```

Try those same lines yourself. This time, you should see the same "random"
numbers as above, because the seed has been set to the same value: `1`. You
could try with any seed and, so long as you re-seed with that same seed value
before generating the next random number, you'll get the same number back.

Faker also uses a seed. Try Faker's seeding out now, referring to the Faker
documentation to see how to set the seed. Make sure you're able to run
fake.name() more than once, seeing the same name each time.

#### Usefulness

Given this power to generate the same "randomness" over and over again, this
seeding of the generators can now be used to do things like:

* Hard-coding expectations - when the test data is used as an input to the
  system, it produced (what we hope will be!) consistent outputs so that we can
  *check* those against some hard-coded expectations in subsequent runs.
* Regenerating the data - perhaps the first time the randomly generated test
  data was used, it produced an error in a system, and we now want to preserve
  that test data for future tests.

#### Exercise

With a seed value of `123456789`, the author of this content has found the first
en_UK fake name generated by Faker is `Dr Mathew Ellis`.

> Different versions of the Faker library might result in different names being
> generated, despite the same seed being used. Find out now if you see the same
> name as the author, but if you get a different one with seed `123456789`, use
> that name for the rest of this exercise.

Answer these two questions:

1. Are there other seeds that also generate `Dr Mathew Ellis` as the first name,
   and if so, can you find one of those seed values? Note that there's not an
   infinite list of first and last names available to the library...
2. For the seeds that give `Dr Mathew Ellis` as the first name out after setting
   the seed, what do you think the second names will be in relation to each
   other - will they be the same, or different? Think about it first and come up
   with an answer, then check for yourself.

[Next Challenge](03_challenge.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F02_fake_data.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F02_fake_data.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F02_fake_data.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F02_fake_data.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase2%2F02_fake_data.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
