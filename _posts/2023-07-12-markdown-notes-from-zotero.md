---
layout: post
title:  "Markdown notes from Zotero"
description: "Getting Markdown notes for items stored in Zotero"
date: 2023-07-12
author: msleigh
categories: zotero markdown zettelkasten
---

## Context

I keep a 'zettelkasten' or 'second brain' of sorts (although without adhering
to any particular system), consisting of Markdown files. I use VSCode and
[Foam](https://foambubble.github.io/foam/) to manage this, which for the basic
level of functionality I need seems roughly equivalent to using
[Obsidian](https://obsidian.md/). (In fact I use that sometimes, on the same
set of notes - I can switch between between Obsidian, VSCode+Foam, or just
editing in Vim, depending on what I want to do. The notes are plain Markdown
and are stored in a Git repository, so I'm not tied to any particular tool.)

In trying to get as much of the information that I store as possible into
Markdown, I recently started to use [Zotero](https://www.zotero.org/) to manage
bibliographies and reading lists, primarily because there are add-ons for it
that allow Zotero records to be exported as Markdown.

They key one is [Mdnotes](https://github.com/argenos/zotero-mdnotes).

## Installation / configuration

To install any Zotero add-on, the add-on needs to be downloaded as an `.xpi`
file. Then it can be added via the `Tools` -> `Add-ons` ->
`Install Add-on From File...` menu.

Two dependencies are required:

- [Zotfile](http://zotfile.com/) for advanced PDF management
- [Better Bibtex for Zotero](https://retorque.re/zotero-better-bibtex/)

Once these have been added, add Mdnotes itself in the same way, then restart
Zotero.

In Zotero's `Tools` menu, selecting the new `Mdnotes preferences` item allows
the add-on's behaviour to be configured. I set the `File organization` option
to `Single file`, which enables the `Create full export note` function. This
exports the item's metadata, and any Zotero notes that are associated with it,
as a single file. I set the `Export directory` to a location inside my Foam
project. Under the `File names` tab, I set the suffix to `-mdnote` for the
`Mdnotes` type, which is what seems to be created by the `Create full export
note` option. Lastly, I set up the note template files as described
[here](https://github.com/argenos/zotero-mdnotes/blob/master/docs/docs/advanced/templates/single-file.md),
and store them in the same directory as the exported Markdown, so they're
under version control inside my notes repository.

That's all a bit of a faff, but once done, right-clicking on an item in Zotero
and clicking `Create full export note` adds a Markdown file in my Foam project
with all the metadata for the item, with appropriate tags and Wiki links, and
including any notes I made in Zotero about the item. I add a Zotero record, and
export it to a Markdown note in this way, for everything I read online.