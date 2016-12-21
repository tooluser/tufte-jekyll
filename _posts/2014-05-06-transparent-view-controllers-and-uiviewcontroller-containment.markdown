---
layout: post
title: "'Transparent' view controllers and UIViewController containment"
date: 2014-05-06 09:43:47 -0700
comments: true
categories: 
published: false
---

A common desire and one that can be used to great effect is for a ‘transparent’ modal or view controller. This could be phrased as having a consistent image in the background of a navigation controller, or of having successive view controllers slide onto a stack while leaving others 'showing through' their transparent or translucent areas.

Say for example you want to use a standard ‘navigation’ style view controller paradigm, but have each successive view slide over a shared background. 

No problem, you may think. Just set a background on your `UINavigationController`, then push on a `UIViewController` with its view’s `backgroundColor` set to `[UIColor clearColor]`.

(code)

(image)

No dice. What's going on? A hint is provided by what happens when another view controller is pushed atop that one:

(code)

At first it looks promising, but the awful flash of black says something unexpected is happening. What gives?

(spark video)

Dumping the view hierarchy shows clearly that while your new view controller’s view is present, the background view you thought you'd added to the navigation controller is nowhere to be seen; neither is the view that was visible '. Why is that?

To perform its function, `UINavigationController` maintains an array of view controllers, accessible via its `viewControllers` property. This array is used as a stack; the topmost item’s `view` is displayed. 

When a standard-issue UINavigationController executes your `pushViewController:animated:`, it inserts the new view controller onto this stack and animates it into place. It uses some cleverness to make animation smoother and lower-cost; namely, rather than animating a live version of your view, it renders the view offscreen and slides an image into place. Then, once it's in place, the view below it is entirely removed from the view hierarchy so it need not even be considered for drawing or interaction. Pushing a transparent view makes these optimizations more visible. 

But what if you want views 'below' the new one to receive touches or simply display their content? You're going to have to roll your own. 

One way to accomplish this would be to use only one view controller, and to slide on successive custom `UIView` subclasses to accomplish the visual effect. This is undesirable for several reasons: all the controller code would need to live in the single view controller, eradicating any potential for encapsulation or testing, and you'd need to duplicate most of the behavior of navigation controller to get the navigation bar to function at all similarly. Device rotation would have to manually notify and reconfigure all the subviews. . . . owls would kill hawks, sea levels would rise, and android apps would acquire reasonable security practices.

No, clearly you want to encapsulate your view controllers into, well, view controllers. You want something as much like UINavigationController as possible. The mechanism employed is called [view controller containment](https://developer.apple.com/library/ios/featuredarticles/ViewControllerPGforiPhoneOS/CreatingCustomContainerViewControllers/CreatingCustomContainerViewControllers.html).

View Controller Containment
===========================
(basic intro)

In this case we wanted to build an interface where a navigation-controller like view controller maintained a map in the background that could be shared by successive view controllers as they were pushed on for our taxi-hailing app, [Flywheel](https://itunes.apple.com/us/app/flywheel-the-taxi-app/id584165682?mt=8). One view controller would handle selection of the user's pickup place, another would show taxis being hailed and a taxi approaching their location, and so on, all sliding into place over a shared map. The map should be available from any contained view controller, in the same way that the `navigationController` method on UIViewController returns the appropriate containing view controller, no matter how many levels deep it is nested. (Try it!)

As we've seen, simply inserting a MKMapView into the 'background' via a UINavigationController doesn't fly. Instead we had to make our own. 

BackgroundMapViewController
-----------

To begin with, we made the root view controller, `BackgroundMapViewController`. 

(code, simplified)

Here are the salient bits. 

