Swift Coding Style Guide
============================

The coding standards adopted by adesso Turkey for the iOS platform.

Table of Contents
-----------------

- [DRY](#dry)
- [Use Early Exit](#use-early-exit)
- [Write Shy Code](#write-shy-code)
- [Minimal Imports](#minimal-imports)
- [Protocol Declarations](#protocol-declarations)
- [Protocol Conformance](#protocol-conformance)
- [Function Declarations](#function-declarations)
- [Memory Management](#memory-management)
- [License](#license)

## DRY (Don't Repeat Yourself)


## Use Early Exit


## Write Shy Code


## Minimal Imports


## Protocol Declarations


## Protocol Conformance

When adding protocol conformance to a model, separate each into an extension and use // MARK: - comment.

* <a id='optional-binding-over-protocol-conformance'></a>(<a href='#optional-binding-over-protocol-conformance'>link</a>)

**Preferred**
```swift
class MyViewController: UIViewController {
  // class stuff
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view data source
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate
}
```

**Not Preferred**
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all
}
```

## Function Declarations


## Memory Management

A memory leak must not be created in the source code. Retain cycles should be prevented by using either `weak` and `unowned` references. In addition, value types (e.g., `struct`, `enum`) can be used instead of reference types (e.g., `class`).

* <a id='optional-binding-over-memory-management'></a>(<a href='#optional-binding-over-memory-management'>link</a>)
Always use `[weak self]` or `[unowned self]` with `guard let self = self else { return }`.

**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self = self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
/// Deallocation of self might occur between `let result = self?.updateResult(someResult)` and `self?.updateUI(with: result)`
someMethod { [weak self] someResult in
  let result = self?.updateResult(someResult)
  self?.updateUI(with: result)
}
```
* <a id='weak-over-unowned'></a>(<a href='#weak-over-unowned'>link</a>)
Use `[unowned self]` where the object can not be nil and 100% sure that object's lifetime is less than or equal to self. However, `[weak self]` should be preferred to `[unowned self]`.


**Preferred**
```swift
someMethod { [weak self] someResult in
  guard let self = self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

**Not Preferred**
```swift
/// self may be deallocated inside closure
someMethod { [unowned self] someResult in
  guard let self = self else { return }
  let result = self.updateResult(someResult)
  self.updateUI(with: result)
}
```

## License

```
Copyright 2020 adesso Turkey

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

[linkedin/jobs]: https://www.linkedin.com/company/adessoturkey/jobs/
