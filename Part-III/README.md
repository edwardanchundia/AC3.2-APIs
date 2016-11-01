# AC3.2-APIs: Part III
### Storing Requests
---
### Readings

1. [Swift Guide to Map, Filter, Reduce - Use Your Loaf](http://useyourloaf.com/blog/swift-guide-to-map-filter-reduce/)
  - Nice brief explanation of each
2. [Higher Order Functions - We </3 Swift](https://www.weheartswift.com/higher-order-functions-map-filter-reduce-and-more/)
  - An excellent, and longer, example of each with accompanying for-in loop for comparison
3. [Demo Map, Filter, Reduce - Global Nerdy](http://www.globalnerdy.com/2016/06/26/demonstrating-map-filter-and-reduce-in-swift-using-food-emoji/)
  - Really cute example of these functions! Highly recommended if you're more of a visual learner. 
4. [NSUserDefaults - Coding Explorer](http://www.codingexplorer.com/nsuserdefaults-a-swift-introduction/)

---
### Quick, Persistant Storage using `UserDefaults`

What is `UserDefaults`? Well officially it is intended to store a user's settings for your app. For example, if you had a weather, location-based app you may decide you'd like to store the user's preferred zip code, their preferred temperature scale (C/F), and if they choose to receive push notifications from your app. 

In practice, `UserDefaults` tends to be used as a lightweight persistant storage container. The data stored in `UserDefaults` is in the form of a __property list__, or plist for short. You've seen property lists already: one gets generated for your project in Xcode automatically (`Info.plist`). Plists are essentially dictionaries at their core, and to store something in a plist you do so in a dictionary-like manner: setting a key/value pair. 

In looking at `UserDefaults`, we're going to store our `SettingsManager`s settings for `results`, `nationality` and `gender` so that any change we make in our `SettingsTableViewController` persists between runs of our app. 

---
### 
