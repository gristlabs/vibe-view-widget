# Vibe View - Grist Custom Widget

This repository contains the "Vibe View" widget for [Grist](https://www.getgrist.com).

## Description

The Vibe View widget allows creating a read-only view of some Grist data using a single
[LiquidJS](https://liquidjs.com/tutorials/intro-to-liquid.html) HTML template. This template has
access to certain dynamic variables to easily access Grist data. This makes it easy to use AI to
generate nice-looking templates.

The goodies include:
- Simple access to referenced data (i.e. records pointed to by Reference columns).
- Simple access to attachments.
- Filters for formatting dates or currencies, and options to override defauults.
- Support for `<style>` and `<script>` tags, or external stylesheets and scripts.

In fact, the widget includes a detailed prompt to use with AI, so that it can get things right
quickly. There is no plumbing: you can copy-paste the prompt from the widget to a chatbot of your
choice, and copy-paste the template it writes for you back into the widget. You can also edit the
template code by hand if you like.

Switch between editing the template and previewing its result using the 'Edit' / 'Preview' buttons.

Other tools are:
- 'Info': shows instructions for using the widget, for you or to copy to AI of your choice.
- 'Print': tells the browser to print the content of the widget.
- 'Hide': hides the toolbar. A hidden toolbar leaves a pill on the right which you can hover over
  to show the toolbar again, or for quick access to the 'Print' button.

When you click "Save" above the widget, its code and toolbar status get saved into the widget's
configuration, and become available to other users of this document.

Note that Vibe View needs access level "Full document access" rather than "Read selected table".
Even though it's only suitable for read-only views, it needs the higher access level to be able to
access metadata.

Vibe View can access data outside of the current table via Reference and Reference List columns.
It can't do lookups. If you have relevant data in other tables, you can create references to it
using [lookup formulas](https://support.getgrist.com/references-lookups/#lookuprecords) or
[two-way references](https://support.getgrist.com/col-refs/#two-way-references).

⚠️  Note about reactivity: the widget will react to changes in the main table it is rendering.
To have it update automatically when referenced data changes, set up formulas in the main table
that will react to such updates. For example, if the widget renders and invoice, a formula for
"total" in the main table will cause the widget to update whenever the total changes, but a change
to an item that doesn't affect the total will not cause it to update. You can switch to
another page and come back to force the widget re-render.


## Developer notes

This repo is included into the [grist-widget](https://github.com/gristlabs/grist-widget) repo as a
submodule.

To preview during development, follow the usual recommendations for `grist-widget`. If you don't
see `vibe-view`, make sure submodules are initialized: `git submodule update --init --recursive`.

To commit changes, commit in the `vibe-view` subdirectory. You can make PRs directly from there.

To deploy changes to production for use in Grist, you need to:

1. Commit and push changes to this repo.
2. In the `grist-widget` repo, run `git submodule update --remote --init` to update the submodule
   to the latest commit in the `main` branch.
3. Commit this update in the `grist-widget` repo, push, and make a PR. The deploy preview URL can
   be used to test the changes.




