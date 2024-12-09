# Snapshot testing
Inspired by the nice snapshot diff review tool that Charlie Marsh uses in uv
I want to see if we could use something similar in Python.
https://x.com/charliermarsh/status/1853623858458443957
> uv is almost entirely snapshot tested... We have 1,394 snapshot tests that exercise various resolution and installation scenarios. I love it -- I find snapshot testing to be such good "value" 📸
Insta a snapshot testing library in rust, looks like it would enable really ergonomic reviews and updates of snapshot tests.

## Motivation
Easy to review.
We can review a diff in function outputs when tests change.
Instaed of running tests and manually verifying the output.
And if no outputs change we can know that we're just reviewing a refactor that
changes style.

A PR text can just be the before and after of the snapshot test.

## Plan
This would either replace or supplement the workflow tests.

Nice to test:
- Works well with dataframes?
  - A lot of our code takes a dataframe as input and output 

## Python tools
### Syrup
Syrupey 

### Pytest insta
https://asciinema.org/a/369462
Pytest insta (inspired by insta). Written this year.

https://pypi.org/project/pytest-insta/
insta (from rust) alternative for python?
