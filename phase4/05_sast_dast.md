# Methodologies

Two security testing methodologies are worth covering at this point, and have
some association with the possible tools we've just looked at.

While you're reading through some details on SAST and DAST, think about whether
anything in there sounds familiar!

## Static Application Security Testing

Static Application Security Testing (SAST) is a testing approach that is driven
by knowledge of the code. By inspecting the code, one can look for errors and
security vulnerabilities.

SAST tools exist but given this is a course aimed at software testers rather
than developers, we haven't listed them on the previous page. Developers might
consider adding SAST tools into build pipelines, for example.

The term "static" applies to the fact that the code doesn't need to be run in
order for the testing to occur - that's where DAST comes in.

## Dynamic Application Security Testing

Dynamic Application Security Testing (DAST) is a testing approach that looks at
the application while it is running, and uses its behaviour, the information it
reveals, etc. as the way to look for errors and security vulnerabilities.

DAST tools include the ones listed in the previous section, including inspecting
requests and responses as you did earlier - when you found that header, you were
doing DAST.

Because you're more likely to be doing "dynamic" security testing, where the
application is running, our focus is on tools that support DAST.

## Sounds familiar?

If you thought those test activities sounded a lot like white box and black box
testing, then you're right - SAST is a white box method and DAST is a black box
method of testing.

It's worth noting that like other black box testing activities, DAST tends to
naturally occur later in the cycle, as it requires more
code/integration/systems/etc. than SAST with its code inspection.

[Next Challenge](06_threat_modelling.md)

<!-- BEGIN GENERATED SECTION DO NOT EDIT -->

---

**How was this resource?**  
[😫](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F05_sast_dast.md&prefill_Sentiment=😫) [😕](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F05_sast_dast.md&prefill_Sentiment=😕) [😐](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F05_sast_dast.md&prefill_Sentiment=😐) [🙂](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F05_sast_dast.md&prefill_Sentiment=🙂) [😀](https://airtable.com/shrUJ3t7KLMqVRFKR?prefill_Repository=makersacademy%2Fextending-testing&prefill_File=phase4%2F05_sast_dast.md&prefill_Sentiment=😀)  
Click an emoji to tell us.

<!-- END GENERATED SECTION DO NOT EDIT -->
