# Design Conventions

## Layout & Page Namespace

Sometimes, CSS definitions apply to one page or all pages in a specific layout. The convention is to scope these definitions under the page namespace or layout namespace.

Each template can have a layout namespace and a page namespace attached to the `body` HTML element.

```html
<body class="layout-boxed page-login">
```

The `layout-NAME` CSS class identifies the layout, the `page-NAME` identifies the page. Multiple actions can have the same layout namespace and, sometimes, the same page namespace.

If a CSS class should apply only to boxed layouts use

```css
.layout-boxed .the-class {
  /* only for boxed */
}
```

Likewise, use the page namespace to define page-wide classes.

```css
.page-account .the-class {
  /* only for boxed */
}
```

## How to change the @layout-NAME@ namespace

Each layout should have its own layout namespace attached to the layout file itself.

## How to change the @page-NAME@ namespace

Use the `pagid` Ruby helper at the top of your action file.
For example, to assign the page namespace `page-account` to the `/accounts/index.html.erb` view file, place the following string at the top of the view file.

```html
<% pagid "account" %>

... here your HTML view
```
