# YARD

YARD is a powerful Ruby documentation tool for generating API documentation from Ruby source code.

## Tag Conventions

YARD provides a [set of Javadoc-inspired tags](http://rubydoc.info/docs/yard/file/docs/Tags.md) the developer can use to enrich the documentation with additional 
metadata.

### Order of Tags

Whilst YARD does not enforce a particular order, a common convention makes the source code more readable, especially when the documentation block contains more than 5 tags.

Include tags in the following order:

    Description block.

    @example

    @note
    @todo

    @param
    @return
    @raise

    @see

    @author
    @version
    @since

    @abstract
    @api
    @deprecated


### Ordering Multiple Tags

We employ the following conventions when a tag appears more than once in a documentation block.

* Multiple `@author` tags should be listed in chronological order, with the creator of the class/method listed at the top.
* Multiple `@param` tags should be listed in argument-declaration order. This makes it easier to visually match the list to the declaration.
* Multiple `@raise` tags should be listed alphabetically by the exception names.  

### Required Tags 

A `@param` tag is "required" (by convention) for every parameter. The description can be omitted if the meaning of the parameter is obvious.

    # Opens a socket connection and returns the TCPSocket instance.
    #
    # @param  [String] host
    # @param  [Integer] port
    # @return [TCPSocket]
    def connect(host, port)
    end

The `@return` tag is required for every method that returns something other than void. The description can be omitted if the meaning of the parameter is obvious. Whenever possible, find something non-redundant (ideally, more specific) to use for the tag comment.

    # Opens a socket connection and returns the TCPSocket instance.
    #
    # @param  [String] host
    # @param  [Integer] port
    # @return [TCPSocket] The socket connection,
    #         preconfigured with the default set of options.
    def connect(host, port)
    end

