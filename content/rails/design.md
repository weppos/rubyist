---
title: Design Conventions / Rails
---

# Rails Design Conventions


## Layout & Page Namespace

Sometimes, CSS definitions apply to one page or all pages in a specific layout. The convention is to scope these definitions under the page namespace or layout namespace.

Each template can have a layout namespace and a page namespace attached to the `body` HTML element.

    <body class="layout-boxed page-login">

The `layout-NAME` CSS class identifies the layout, the `page-NAME` identifies the page. Multiple actions can have the same layout namespace and, sometimes, the same page namespace.

If a CSS class should apply only to boxed layouts use

    .layout-boxed .the-class {
      /* only for boxed */
    }

Likewise, use the page namespace to define page-wide classes.

    .page-account .the-class {
      /* only for boxed */
    }

Here's the code for the `page_id` helper.

    # Sets/Gets a page id for a view.
    #
    # If called with an argument, appends the argument to the existing page id.
    #
    #   page_id "page-users"
    #   # => "page-users"
    #   page_id
    #   # => "page-users"
    #   page_id "hidden"
    #   # => "page-users hidden"
    #   page_id
    #   # => "page-users hidden"
    #
    # Returns a String with the current page id.
    def page_id(*args)
      (@_page_id ||= []).concat(args).compact.join(" ")
    end

### How to change the `layout-NAME` namespace

Each layout should have its own layout namespace attached to the layout file itself.

### How to change the `page-NAME` namespace

Use the `page_id` Ruby helper at the top of your action file.
For example, to assign the page namespace `page-account` to the `/accounts/index.html.erb` view file, place the following string at the top of the view file.

    <% page_id "page-account" %>

      ... your HTML view goes here
