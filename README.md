[![Download](https://api.bintray.com/packages/davideas/maven/flipview/images/download.svg) ](https://bintray.com/davideas/maven/flipview/_latestVersion)

# FlipView

###### Gmail like View & beyond - Master branch: v1.1 of 2015.11.05

#### Concept
FlipView is a ViewGroup (FrameLayout) that is designed to display 2 views/layouts by flipping
the front one in favor of the back one, and vice versa. Optionally more views can be
displayed in series one after another or can cycle with a interval.

Usage is very simple. You just need to add this View to any layout and you customize the behaviours
by assigning values to the optional properties in the layout or programmatically.
Please, refer to those attributes documentation for more details.

Not less, FlipView extends `android.widget.ViewFlipper` that extends `android.widget.ViewAnimator`,
which means you can call all public functions of these two Android views.

#### Main functionalities
- Visible during design time ;-)
- Custom In/Out animation + Entry animation + Rear ImageView animation
- Custom layout, ImageView & TextView for front layout.
- Custom layout, ImageView for rear layout.
- Custom background Drawable & color.
- Autostart cycle animation with custom interval.
- PictureDrawable for SVG resources.

# Showcase
![Showcase1](/showcase/showcase1.gif) ![Showcase2](/showcase/showcase2.gif)

#Setup
Import the library into your project using Gradle with JCenter
```
dependencies {
	compile 'eu.davidea:flipview:1.1.0'
}
```
Using bintray.com
```
repositories {
	maven { url "http://dl.bintray.com/davideas/maven" }
}
dependencies {
	compile 'eu.davidea:flipview:1.1.0@aar'
}
```
#### Pull requests / Issues / Improvement requests
Feel free to contribute and ask!

#Usage
Supported attributes with _default_ values:
``` xml
<eu.davidea.flipview.FlipView
	xmlns:app="http://schemas.android.com/apk/res-auto"
	android usual attrs
	(see below).../>
```
**ViewAnimator**
- `android:inAnimation="@anim/grow_from_middle_x_axis"` - Identifier for the animation to use when a view is shown.
- `android:outAnimation="@anim/shrink_to_middle_x_axis"` - Identifier for the animation to use when a view is hidden.
- `android:animateFirstView="true"` - Defines whether to animate the current View when the ViewAnimation is first displayed.

**ViewFlipper**
- `android:autoStart="false"` - When true, automatically start animating.
- `android:flipInterval="3000"` - Time before next animation.

**FlipView**
- `android:clickable="false"` - (!!) Set this if you want view react to the taps and animate it.
- `app:checked="false"` - Whether or not this component is flipped at startup
- `app:animateDesignLayoutOnly="false"` - false, if main animation should be applied only to the child views from design layout; true, to use inner layout.
- `app:animationDuration="100"` - Set the main animation duration.
- `app:anticipateInAnimationTime="0"` - Anticipate the beginning of the InAnimation.
- `app:enableInitialAnimation="false"` - Whether or not the initial animation should start at the beginning.
- `app:initialLayoutAnimation="@anim/scale_up"` - Starting animation.
- `app:initialLayoutAnimationDuration="250"` - Starting animation duration.
- `app:animateRearImage="true"` - Use default rear image animation.
- `app:frontLayout="@layout/flipview_front"` - Front view layout resource (for checked state -> false).
- `app:frontBackground="<OvalShape Drawable generated programmatically>"` - Front drawable resource (for checked state -> false).
- `app:frontBackgroundColor="<Color.GRAY set programmatically>"` - Front view color resource (for checked state -> false).
- `app:frontImage="@null"` - Front image resource (for checked state -> false).
- `app:frontImagePadding="0dp"` - Front image padding.
- `app:rearLayout="@layout/flipview_rear"` - Rear view layout resource (for checked state -> true).
- `app:rearBackground="<OvalShape Drawable generated programmatically>"` - Rear drawable resource (for checked state -> true).
- `app:reartBackgroundColor="Color.GRAY set programmatically"` - Rear view color resource (for checked state -> true).
- `app:rearImage="@drawable/ic_action_done"` - Rear accept image resource.
- `app:rearImagePadding="0dp"` - Rear image padding.
- `app:rearImageAnimation="@anim/scale_up"` - Rear image animation.
- `app:rearImageAnimationDuration="150"` - Rear image animation duration.
- `app:rearImageAnimationDelay="duration"` - Rear image animation delay (depends the animation/duration it can be smart setting a custom delay).

**Not changeable values** (in ms)
- `DEFAULT_INITIAL_DELAY = 500` - This gives time to the activity to load.
- `SCALE_STEP_DELAY = 35` - This gives an acceptable nice loading effect.
- `STOP_LAYOUT_ANIMATION_DELAY = 1500` - This gives the time to perform all entry animations but to stop further animations when screen is fully rendered.

# Limitations
- Transparency has a little glitch when used with elevation, you could see shadow In the shape: more transparent the color is more visible the shadow is.
- Using layer type _software_ on the entire layout it removes the shadow/elevation.
- Stroke and background color on custom Drawable should be preset by the user: too complex to determine the type of the Drawable used in order to change its color.

# Change Log
###### v1.1.0 - 2015.11.05
- New attribute `app:rearImageAnimationDelay`.
- Fixed bugs #4 #5 #6.
- Overridden `showNext()` & `showPrevious()` methods from `ViewAnimator`: now they perform the flip accordingly with the existing
  settings and register its state.
- Since the FlipView uses shapes to define its border and shadows, one can use `app:frontBackground` & `app:rearBackground`
  for the custom Drawable with the desired shape, color and stroke, which always override inner Drawables.
  Alternatively you can do this also by assigning the resource to `android:background` of the _custom_ layout.
  Because of that, for runtime, the method `setChildBackgroundDrawable(child, drawable)` has been reviewed (#2 #3).
- Instead, if you want to use the inner Drawable (OvalShape) and only change color with alpha value, you can do it
  at design time with `app:frontBackgroundColor` & `app:rearBackgroundColor` and at runtime with the new method
  `setChildBackgroundColor(child, color)`: it always creates an OvalShape with the custom color (#2 #3).
  **Note:** setBackgroundColor is the method of `android.view.View`, so it does the default job!
- First version of ShapeDrawables static methods (Oval, Arc, RoundRect).
- Added new static methods to enable/disable logs at runtime (call them once in the app!).
- Added methods to retrieve ImageViews and front TextView objects.
- Automatic layer type _software_ when setting PictureDrawable for SVG (applied on ImageView reference only!).
- Adapted example to show Autostart and how 2 entire layouts can be animated ;-)

###### Old releases
See [releases](https://github.com/davideas/FlipView/releases) for old versions.

v1.0.0 - 2015.11.01

# License

    Copyright 2015 Davide Steduto

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
