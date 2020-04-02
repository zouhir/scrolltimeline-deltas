# Quirks

### Creating a ScrollTimeline driven animation

##### Native Chromium Version 83

- Only works via `new Animation` constructor for now, `Element.prototype.animate` is not yet implemented
- Requires invoking `animation.play()` method

##### Polyfill

- Only works via `Element.animate()` method, integration with `Animation` constructor function is not implemented yet.
- Using `new Animation` and passing the polyfill's `ScrollTimeline` results in an error as the polyfill's ScrollTimeline is not of type `AnimationTineline`
    - Fix: Add a small `Animation` constructor polyfill
- Calling `Element.animate().play()` will play the entire keyframe animation without scrolling, while users likely won't do that, animation should not autoplay if they did.

### ScrollTimeline options: orientation

##### Native Chromium Version 83

- `inline` , `block` , `horizontal` and `vertical` working as expected

##### Polyfill

- The `inline` orientation is not implemented yet and it defaults to `block` and `vertical`
- Consider adding a `console.warn` if you see `orientation: inline | horizontal` in options until that is implemented

### TimeRange: 0

##### Native

- You will only see the first frame, animation won't play

##### Polyfill

- Animation plays as if `timeRange` === `duration`


### TimeRange: auto

##### Native

- Not yet implemented (as Majid https://github.com/flackr/scroll-timeline/issues/4)

##### Polyfill

- Animation plays as if `timeRange` === `duration`, same behaviour as `timeRange: 0`


# Consistent parts

### ScrollSource as arbitrary element

##### Native

- works as expected

##### Polyfill

- works as expected

### Element position if a scrollable element cannot scroll

##### Native

- element is at the last frame

##### Polyfill

- element is at the last frame


### TimeRange: <number> (where number > 0 and obviously not `auto`) 

##### Native

- Works as expected

##### Polyfill

- Works as expected
