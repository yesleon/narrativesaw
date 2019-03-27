---
date: 2019-03-26T15:15:29+08:00
draft: false
title: On Developing a Universal App
categories: []
---

# On Developing a Universal App

## A Non-linear Process

It's pretty easy to implement a [universal app](https://www.lifewire.com/what-is-universal-app-1994348). Use Interface Builder, Auto Layout, Split View, and Popover, and voila! Now your app is ready to run on both iPad and iPhone with an adaptive layout.

The obstacle, though, lays with the _design_. If you push a View onto a Navigation View on iPhone, should you do the same on iPad? Or should you present it as a popover, a form sheet, a page sheet, or even embed it into a Split View?

Should you use a Table View or a Collection View? How is it supposed to scale?

How about orientations? Which orientations should be supported on both devices, respectively?

Should a view be presented modally?

All questions above are hard questions one must answer when he or she wants to adapt an iPhone app to iPad. Or rather, when one wants to make an iPad app.

An app on iPhone is like a stack of views. Without dedicated tweaking, all views in an iPhone app would be presented fullscreen or embedded in a Navigation View--which is fullscreen too.

![](https://i.imgur.com/5XHw62Wm.png)

Things are different on iPad, though. Compared to iPhone apps, iPad apps are less linear. They often have two main views shown at the same time, like the Split View and the Page View. It's also encouraged to use non-fullscreen presentations, such as popover, form sheet, or page sheet. Therefore, when developing iPad apps, we need to think more thoroughly on how one view is related to another, and how we should structure all the views.

![](https://i.imgur.com/UGC26Vb.png width=400)

Therefore, it is easier to design for iPad first and then move on to the iPhone. All you have to do is to make the views collapse into a single stack.

## iPad-first Design 

When redesigning Storyboards, I dealt with the main view structure on iPad first. I use the new Document Browser from Apple, and I took the advice from the [official docs](https://developer.apple.com/documentation/uikit/view_controllers/adding_a_document_browser_to_your_app) and made it the root main view like this:

![](https://i.imgur.com/bEXtJak.png)

It’s pretty straightforward, and it was the same with Storyboards 1.0. The differences start to show on the second main view, though. Originally, the main view on top of the Document Browser was the Storyboard View, and above it was the Shot View, presented as a modal view.

![](https://i.imgur.com/W1AjNP5.png)

One can see that there are three layers of main view in the structure, and they are all modal, meaning you can’t interact with one layer when you are in another layer. This is typical iPhone-style linear thinking, because iPhone is all about doing one thing at a time. However, there’s no such restriction on iPad. It makes perfect sense to make the Storyboard View and the Shot View show at the same time, just like every video editor out there, and I decided to do so.

I had thought about using a floating panel or a vertical split view, but I found the stock, horizontal Split View meets the needs pretty well already. However, let me describe my thought process here for a bit.

The floating panel pattern is widely used on desktop, but its presence on iOS is limited. It can be seen in apps like Apple Maps and MindNode which have a sort of "canvas" showing the main content. It makes sense for them to use floating panels because moving/hiding/showing panels won’t impact the layout of the canvas. It’s like a non-modal popover, only that it feels more "pinned" than popovers. However, it doesn’t make sense with Storyboards in that the Storyboard View is not a "canvas" with a fixed layout.

Vertical split view seems like a viable solution, but it is even much rarer than the floating panel pattern on iOS. Therefore, there are a lot of things need to establish. For example, which panel should contain the primary view, the upper one or the lower one? The upper panel sounds more suited, but if you think about video editors, the timeline editors are always in the lower panel. There’s no such concern for the horizontal Split View, though. The left panel is the primary one, period. It is also easier for portrait layouts, because all its panels have by default a portrait layout, except for on a landscape-oriented iPhone.

Therefore, I chose to implement a horizontal Split View in the end:

![](https://i.imgur.com/7jyfDJ5h.png)

The beauty of the Split View is that its two panels are equal in the main view hierarchy. It hints multitasking. It gives you a bird’s eye view of everything in the document. It makes you feel in control. This is something the floating panel pattern can’t give you, because the panel and the "canvas" are not equal but hierarchical, and the panel always seems like it’s hiding something underneath. It’s great when you want the user to focus on the canvas, but it’s not for Storyboards.

After establishing the main view structure of the app on iPad, it was quite straightforward to adapt it to the iPhone. The Split View basically acts like a Navigation Controller on iPhone, pushing and popping the Shot View here. 

![](https://i.imgur.com/dgscae6.png width=640)

It was pretty confusing between presenting a main view modally and showing it non-modally on iPhone, because the only visual differences are which direction the new view comes in and if the new view is using the same Navigation Controller. However, after the thought process of designing the structure on iPad, it became much clearer that the modal presentation is a more thorough transition, discouraging the user to switch back and forth. Although I want the user to be able to focus on the Shot View on iPhone, I don’t want it to be a burden for them to go back to the Storyboard View either. After all, ordering shots should also be a part of the creative process, so I want to encourage the user to head back to the Storyboard View when he or she feels like to do so. If I make the presentation of the Shot View modal, even if equipped with a fluid transition like showing a photo in the Photos app, it would be like creating a new view for that specific shot. However, pushing a view only feels like that view has always been there, and it’s only hidden until you call it out.

## Conclusion

To make an app universal is not as simple as what I had thought, but it hugely deepened my understanding of Storyboards. In the process, I also began to appreciate the design of stock objects like the Split View and the Navigation Controller. They might not be able to make the app look as fancy as Snapshot, but they can do a damn good job on enhancing the UX once used correctly.