---
title: Documentation / Rails
---

# Rails Documentation

Rails code SHOULD be documented using [TomDoc](http://tomdoc.org/).

TomDoc is a code documentation specification that helps you write precise documentation that is nice to read in plain text, yet structured enough to be automatically extracted and processed by a machine.

Rails code usually doesn't need the same level of details of a Ruby Gem or distributable library. Using YARD adds too much overhead, since nobody ever generates API documentation for a Rails project. Conversely, a Rails documentation needs to be easy to read but structured enough to provide a common specification for all the developers. TomDoc perfectly fits this requirement.
