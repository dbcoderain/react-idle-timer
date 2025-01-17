### 4.2.10
- Fixes a bug where onIdle was not triggered consistently on iOS. (see #94)
- Refactor of toggleIdle function to prevent race conditions. (see #93)

### 4.2.9
- Fixes a bug where HMR systems would prevent events from unbinding. (see #87)

### 4.2.8
- Fixes a bug where a paused timer would return the wrong remaining time when resumed.

### 4.2.7
- Fixes a regression introduced in v4.2.6.  If you rely on `getRemainingTime()` you should update to this patch.

### 4.2.6
- Update dependencies
- Fix a bug where `reset()` was not resetting `getRemainingTime()`
- `componentWillMount` is deprecated. Moved logic to `componentDidMount`

### 4.2.5
- Remove ref from typedef as it's included in the React Component interface (see #76)

### 4.2.4
- Fixes typescript definition for evented methods
- Fixes a bug where throttled and debounced actions would not take new props

### 4.2.3
- Fixes an issue importing module with typescript (see #72)

### 4.2.2
- Fixes an issue updating state from inside onIdle (see #71)

### 4.2.1

- Added a typescript definition that will now be maintained along with this library. It expects that you have the react type definitions installed.
- Fixed a documentation error

# 4.2.0

Version `4.2.0` will now dynamically bind and unbind events.

Events are unbound when:
- `stopOnIdle` is set to `true` and the user goes idle
- `pause()` is called

Events are bound when:
- component is mounted
- `reset()` is called
- `resume()` is called

### 4.1.3
- `stopOnIdle` will now keep `IdleTimer` in idle state until `reset()` is called

### 4.1.2
- Fixes a bug where `stopOnIdle` logic was being applied to active state

### 4.1.1
- Fixes a bug where initial `onIdle` event was not firing when `stopOnIdle` is set

# 4.1.0

Version `4.1.0` adds support for some commonly requested features:

## Features

- Added property `stopOnIdle` defaults to `false`. Setting to `true` will prevent user activity from restarting the `IdleTimer` once it has gone idle.  This useful if you want to do some custom async stuff before the `IdleTimer` gets restarted.  In order to restart the `IdleTimer` call `reset()` on your ref.
- Added event handler `onActive` which enables reporting of all user activity from `IdleTimer`.  The built in `debounce` or `throttle` properties will help increase performance if you are using the `onActive` event. By default `debounce` and `throttle` are off.  Only one can be enabled at a time.
- Added property `debounce` defaults to 0.  Set the `onActive` debounce delay in milliseconds. The `throttle` property cannot be set if this property is set.
- Added property `throttle` defaults to 0.  Set the `onActive` throttle delay in milliseconds.  The `debounce` property cannot be set if this property is set.

### 4.0.9

- Fixes a memory leak when IdleTimer is unmounted.  Events need to be removed exactly the same way they are added. See [here](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/removeEventListener#Matching_event_listeners_for_removal)

### 4.0.8
- Fixed a bug where passive and capture were not being passed to the event listener.  The function has been reformated so it reads better.

### 4.0.7
- Fixed some inconsistencies in the README
- Added default prop values to documentation

### 4.0.5 - 4.0.6
- Fixes a bug where setting `startOnMount` to `false` starts IdleTimer in the wrong state

### 4.0.4
- Fixes a bug where the module could not be imported

### 4.0.1 - 4.0.3
- Minor documentation updates
- Continuous integration bugfixes

# 4.0.0
Version 4.0 contains a rewrite of the build system and a refactor of the source code for IdleTimer.  After accepting many pull requests, the projects code style was destroyed.  We added in some forced styling and will not be accepting PRs that don't respect this style. Contribution guide now on the README.  

## Breaking Changes
- The property `startOnLoad` has been renamed to `startOnMount` to make more sense in a react context.
- The property `activeAction` has been renamed to `onActive`.
- The property `idleAction` has been renamed to `onIdle`.

## Enhancements
- Added [passive](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) property.  Defaults to `true`, bind events with passive mode enabled
- Added [capture](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) property.  Defaults to `true`, bind events with capture mode enabled
- Pass event through to `idle` and `active` handler functions

## Bugfixes
- Fixed installation bug on windows machines. This was due to the use of environment variables in the build scripts. The new build system does not rely on environment variables defined at the cli level

# 3.0.0
We dropped support for date formatting in version 3.  React idle timer returns raw date objects and you can use which ever library you like to format it. If you would like to continue using the built in formatter, stick with version 2.

## Breaking Changes
- Removed built in date formatter.

# 2.0.0
Added support for isomorphic react!

# 1.0.0
Initial release
