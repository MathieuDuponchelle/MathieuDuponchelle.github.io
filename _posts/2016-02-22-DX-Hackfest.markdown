---
layout: post
title: Back from the DX hackfest
category: social
tags: gnome developer documentation
year: 2016
month: 02
day: 22
published: true
summary: My experience at the developer experience hackfest
---

## Back from the DX hackfest

I had the chance to attend the GNOME developer experience hackfest three weeks ago, I'm ashamed to admit three weeks went by before I took the time to write this post!

A lot of people I met there I already knew, I was happy to meet some people I didn't yet, like James, who's working on [Oh-My-Vagrant](https://github.com/purpleidea/oh-my-vagrant).

Philip Withnall has already done a good job at summarizing the general issues we looked at as a group during this hackfest in [this blogpost](https://tecnocode.co.uk/2016/02/01/dx-hackfest-2016-aftermath/), so this post will revolve around my own experience over there.

I am currently working on [hotdoc](https://github.com/hotdoc/hotdoc) for [collabora](https://www.collabora.com/), and I spent the hackfest presenting it to the documentation team members (Ekaterina Gerasimova, Frédéric Péters, Bastian Ilso and Alexandre Franke), discussing its future use with them and Philip Chimento, and making some improvements to it with the help of Thibault Saunier.

#### Hotdoc improvements

I helped Frédéric with testing porting gtk from gtk-doc to hotdoc, and landed a patch from him in hotdoc-gi-extension, the resulting documentation seemed overall correct.

I worked with Thibault Saunier to implement a [smart include feature](https://people.collabora.com/~meh/hotdoc_hotdoc/html/syntax-extensions.html#smart-file-inclusion-syntax) in hotdoc.

#### GNOME Builder

I discussed how to use hotdoc as a [GNOME Builder](https://wiki.gnome.org/Apps/Builder) plugin with Christian Hergert, but the solution he advised me to follow actually falls short because hotdoc is python2, and it seems libpeas cannot handle both python2 and python3 in the same process. I'm still a bit confused as to why this limitation would exist, as the proposed solution involved exposing a D-Bus service, but I'm sure we'll find a better solution when we need to.

#### GNOME developer portal

I discussed the future of <https://developer.gnome.org/> with the documentation team. They liked the search interface in hotdoc (it does work quite well :), and we all agreed that a tighter integration with actual API references would be nice to have, amongst various other things (online editing for example).

The website is currently implemented as [a series of mallard pages](https://github.com/GNOME/gnome-devel-docs/). Hotdoc does not read mallard pages, and it isn't part of my current plans. A possible way forward would be to drop mallard altogether, and have all the pages be "hotdoc-flavored" markdown pages. I think this could make sense because:

* gnome-devel-docs doesn't make an extensive use of mallard.
* markdown pages present a significantly lower barrier to entry, and most people are familiar with the syntax.
* the developer site and the API references it would link to would share the same format for standalone documentation source files.

I have since then implemented a [simple pandoc reader](https://github.com/jgm/pandoc/pull/2700), and used it to make a very naive port of gnome-devel-docs, the result can be seen [here](https://people.collabora.com/~meh/dgo_hotdoc/html/index.html)

This port is naive because I made absolutely no manual edits to the produced markdown files, which explains why the index page looks pretty ugly, but pages like <https://people.collabora.com/~meh/dgo_hotdoc/html/overview-media.html> are pretty faithful to the source, and it would mostly be a matter of custom CSS and trivial edits to get the thing to really look good.

You can have a look at the generated markdown files [here](https://github.com/MathieuDuponchelle/gnome-devel-docs/tree/hotdoc/markdown_files).

#### Philip Chimento's devdocs work

Philip Chimento has been working on a [fork of devdocs](https://github.com/ptomato/gobject-introspection/commits/wip/ptomato/devdocs), in an effort to create a javascriot developer portal for GNOME. I see some drawbacks with his approach, which we've discussed together and I will not detail here, but overall his current solution has the advantage of code reuse, and lightweightness, as the output is generated stictly from gir files.

My opinion on this is that his work is a nice short-term solution to a clear problem (gathering together the javascript documentation for most (all ?) GNOME libraries, and I suggested linking to it on the current portal.

However I think the design of devdocs and his solution will fall short for the long-term requirements that the GNOME documentation team seems to set, and Philip seemed to agree.

This is still a very open issue, and Philip and I definitely intend to work together to provide the best possible experience for GNOME hackers, newbies and senior alike.
