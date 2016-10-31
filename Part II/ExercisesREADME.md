# AC3.2-APIs: Part II Exercises
---

### Part I Discussion
In task 1, you were asked to build out the `SegementedCell` using the `SliderCell` as a template. You will have different answers, but what your `UITableViewCell` subclass must accomplish is: 

1. Define a `static let` constant for it's `cellIdentifier` property to be used in `cellForRow` in `SettingsTableViewController`
2. Contain both an outlet and action that links the `UISegmentedControl` object that is in your cell in storyboard
  - You may have named them differently; I went with `genderSegmentControl` and `selectedSegmentDidChange(_:)` where the `sender` is `UISegmentedControl`
3. A way to parse between the currently selected segment and the segment's index. Here's how I did it: 

```swift 
  // *** In SegmentedTableViewCell ***
  
  // 1. I decided I wanted two helpers to assist me in switching between segment index and the corresponding UserGender
  internal func genderFor(segment: Int) -> UserGender {
     switch segment {
     case 0: return .both
     case 1: return .male
     default: return .female
     }
  }
    
  internal func segmentFor(gender: UserGender) -> Int {
     switch gender {
     case .both: return 0
     case .male: return 1
     default: return 2
     }
  }
    
  // 2. Next, I wanted to have functions to update my selections: one using Int as a parameter and the other UserGender
  internal func updateSelectedSegment(index: Int) {
     genderSegmentedControl.selectedSegmentIndex = index
  }
    
  internal func updateSelectedSegment(gender: UserGender) {
     genderSegmentedControl.selectedSegmentIndex = segmentFor(gender: gender)
  }
```

Then for my protocol, `SegmentedCellDelegate`: 

```swift
protocol SegmentedCellDelegate: class {
  func segmentedValueChanged(_ gender: UserGender)
}
```

Next, for the implementation of `SegmentedCellDelegate` in `SettingsManager`

```swift
    // MARK: - Segmented Cell Delegate
    func segmentedValueChanged(_ gender: UserGender) {
        self.gender = gender
    }
```

And lastly, in `cellForRow` in `SettingsTableViewController`

```swift
   cell = tableView.dequeueReusableCell(withIdentifier: SegmentedTableViewCell.cellIdentifier, for: indexPath)
            
   if let segmentedCell: SegmentedTableViewCell = cell as? SegmentedTableViewCell {
      segmentedCell.updateSelectedSegment(gender: SettingsManager.manager.gender)
      segmentedCell.delegate = SettingsManager.manager
   }
```
