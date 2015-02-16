---
layout: post
title: Dev Tip of the week - OSX Spotlight search from terminal
date: 2014-02-23 22:37:00.000000000 -08:00
categories:
- OSX
- software
- Spotlight
- Terminal
- tip
tags: []
status: publish
type: post
published: true

---
This is a really cool tip that I came across that allows you to perform OSX Spotlight search from the Mac Terminal. Add following to your __.bashrc__ or __.zshrc__ on the Mac to do Spotlight-indexed searches from the command line.

	function spotlight() {
 		mdfind "kMDItemDisplayName == '$@'wc";
	}

###Example
	 $> spotlight main.py  
 	