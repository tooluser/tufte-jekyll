---
layout: post
title: "Linking non-sibling libraries in an Xcode 5 workspace"
date: 2014-01-30 17:06:04 -0800
comments: true
categories: 
---

It would be interesting to examine the history of software engineering via solely the history of the process of layering build systems atop each other.
<!--more-->

Like any decent human being, your third-party libraries are in a subdirectory in your project folder.

```
MyProject
	/Model
	/UI
	/Externals
		/SomeLibrary
	/...
```
You've thus configured your project header import paths, library linking paths, and such with references to ```./Externals/```.

right /images/posts/xcode-5-workspaces.png 400 'Xcode 5 workspaces' 'blah'

Now, along comes Xcode 5 with its fancy new-fangled 'workspaces'. If you're not familiar, [Xcode 5 workspaces][Xcode 5 Workspaces] promises what every build system, ever, has promised: by adding another layer of configuration, *we can finally, really, make everything work*.

In theory, it's quite snazzy. Declare your dependencies via the build phase and as long as the library is in your workspace, it will be automatically discovered and built as needed. (Supposedly, it will also properly associate header files and such, but I've found that practically, one ends up needing to declare header search paths anyway.)

The dependency analysis works well (at least as well as ```make```) But it turns out that if your dependencies are anywhere but sibling folders, Xcode doesn't do a very good job putting build intermediates somewhere they're available for linking, leading to linking errors in any configuration but the command-line default one. Your build logs will show the dependencies being built, so this can be an obscure error to track down.

The solution is simple: manually include ```${OBJROOT}/UninstalledProducts``` as a library search path in the necessary schemas and you're golden. 

Hat tip to [Eonil at StackOverflow](http://stackoverflow.com/questions/6400800/managing-static-library-project-as-a-module-like-framework-on-ios-project-in-xco/6400872#comment30133261_6400872) for the reference to a similar problem in an earlier version of Xcode.

[Xcode 5 Workspaces]: https://developer.apple.com/library/ios/featuredarticles/XcodeConcepts/Concept-Workspace.html