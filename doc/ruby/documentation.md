# Documentation


## Documenting Ruby code

Ruby libraries intended to be distributed or packaged as Gem MUST be documented using [YARD][1].

YARD is a powerful Ruby documentation tool for generating API documentation from Ruby source code. While the base syntax is compatible with RDoc, YARD provides a set of [Javadoc-inspired tags][4] the developer can use to enrich the documentation with details that cannot be extracted from the source code.

Compared to RDoc, YARD is able to generate a more detailed API documentation. It also offers some very handy tools, such as `yard server --reload`, that generates and reloads the documentation on-the-fly.


## Documenting Rails code

Rails code MUST be documented using [TomDoc][3].

TomDoc is a code documentation specification that helps you write precise documentation that is nice to read in plain text, yet structured enough to be automatically extracted and processed by a machine.

Rails code usually doesn't need the same level of details of a Ruby Gem or distributable library. Using YARD adds too much overhead, since nobody ever generates API documentation for a Rails project. Conversely, a Rails documentation needs to be easy to read but structured enough to provide a common specification for all the developers. TomDoc perfectly fits this requirement.


## List of Documentation Tools/Formats

* [RDoc][2]
* [YARD][1]
* [TomDoc][3]


  [1]: http://yardoc.org/
  [2]: http://rdoc.rubyforge.org/
  [3]: http://tomdoc.org/
  [4]: http://rubydoc.info/docs/yard/file/docs/Tags.md#List_of_Available_Tags

