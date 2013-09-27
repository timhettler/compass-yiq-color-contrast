# Compass YIQ Color Contrast

The default color contrast function that Compass provides determines if a color is "light" or "dark" by checking its lightness in the HSL color space. Occassionally this function will produce color pairings that - while functionally correct - just look a little "off". The reason for this is that the eye is more sensitive to changes in the orange-blue range than in the purple-green range, so the percieved lightness of a color can change depending its wavelength.

The YIQ color space is designed to take this bias into account. It weighs the different parts of the color according to their impact on our perpection of the color's brightness. By utilizing this color space when doing contrast comparison, the result is a color pairing that appears more natural.

This code is bundled as a Compass extension simply for ease of installation. It actually has no Compass dependencies, so you can use this library in a non-Compass-based project.

For information on color contrast and the YIQ color space:

* [24 Ways: Calculating Color Contrast](http://24ways.org/2010/calculating-color-contrast/)
* [W3C: Ensure that foreground and background color combinations provide sufficient contrast when viewed by someone having color deficits or when viewed on a black and white screen](http://www.w3.org/TR/AERT#color-contrast)
* [Wikipedia: YIQ](http://en.wikipedia.org/wiki/YIQ)

## Compass Extension Installation

### Install the Ruby Gem.

  ```
  gem install compass-yiq-color-contrast
  ```

#### Install into an existing project:

Edit the project configuration file (`config.rb`) and add:

  ```ruby
  require 'compass-yiq-color-contrast'
  ```

Then run this command from the root of your project:

  ```
  compass install compass-yiq-color-contrast
  ```

#### When creating a new project:

  ```
  compass create my_project -r compass-yiq-color-contrast --using compass-yiq-color-contrast
  ```

By default, the extension doesn't add any files to your project. An example scss and html file can be imported by installing the "example" pattern:

  ```
  compass install compass-yiq-color-contrast/example
  ```

## Usage

  ```scss
  @import 'yiq-color-contrast'
  ```
### Configurable Variables

All configuration variables are assigned with the `!default` flag, so they may be overriden in your project stylesheet.

  ```scss
  $yiq-contrasted-dark-default: #000;
  ```

The text color to be used when a background is determiend to be "light"

  ```scss
  $yiq-contrasted-light-default: #fff;
  ```

The text color to be used when a background is determiend to be "dark"

  ```scss
  $yiq-contrasted-threshold: 128;
  ```

A a value between 0 and 255. It determines when the lightness of color changes from "dark" to "light".

  ```scss
  $yiq-debug: false;
  ```

Toggles diagnostic messages.

### Functions

  ```scss
  yiq-contrast-color($color, $dark, $light, $threshold)
  ```

Returns the `$light` color when the `$color` is dark and the `$dark` color when the `$color` is light. The `$threshold` is a value between 0 and 255 and it determines when the lightness of `$color` changes from "dark" to "light".

### Mixins

  ```scss
  @include yiq-contrasted($background-color, $dark, $light, $threshold)
  ```

Sets the specified background color and calculates a dark or light contrasted text color. The arguments are passed through to the `yiq-contrast-color function`.

### Demo

Check out how the YIQ color contrast compares to the default Compass color contrast: http://timhettler.github.io/compass-yiq-color-contrast/
