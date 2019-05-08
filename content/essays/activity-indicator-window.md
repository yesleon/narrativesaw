---
date: 2019-05-08T14:55:08+08:00
draft: false
title: Activity Indicator Window
categories: []
---

# Activity Indicator Window

## How to block user interaction in your iOS app

Firstly, add a constructor method like this to your `UIWindow` extension:

```swift
import UIKit

extension UIWindow {
    
    static func makeActivityIndicatorWindow() -> UIWindow {
        
        // Create a window
        let window = UIWindow()
        window.backgroundColor = UIColor(white: 0, alpha: 0.3)
        
        // Create an activity indicator
        let activityIndicator = UIActivityIndicatorView(style: .white)
        activityIndicator.translatesAutoresizingMaskIntoConstraints = false
        activityIndicator.startAnimating()
        window.addSubview(activityIndicator)
        
        // Layout
        [
            activityIndicator.centerXAnchor.constraint(equalTo: window.centerXAnchor),
            activityIndicator.centerYAnchor.constraint(equalTo: window.centerYAnchor)
        ].forEach({ $0.isActive = true })
        
        return window
    }
    
}
```

And then, when you want to block user interaction:

```swift
func someFunction() {

    // Create a window
    let window = UIWindow.makeActivityIndicatorWindow()

    // Show the window (and start blocking)
    window.isHidden = false

    // Start the time-consuming task
    someOtherFunctionThatTakesTime(completion: {

        // Hide the window when the task is done
        window.isHidden = true
    })
}
```

Because the window is not retained outside of this function and the completion closure, as long as they’re done the window will be deallocated and unblock user interaction.

Actually you don’t even need to call `window.isHidden = true` in the completion handler. All you need is to retain the window in it, so it won’t be deallocated when `someFunction()` returns:

```swift
func someFunction() {

    let window = UIWindow.makeActivityIndicatorWindow()
    window.isHidden = false

    someOtherFunctionThatTakesTime(completion: {

        // This works too
        _ = window
    })
}
```

I still prefer `window.isHidden = true` though. It’s way more meaningful.

Why using a window instead of a view controller, you ask? Well if you use a view controller then you can only present it from the top presented view controller, but with window, you can show it directly in any place, including `AppDelegate`.