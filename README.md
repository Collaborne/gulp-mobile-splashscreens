# gulp-mobile-splashscreens [![Build Status](https://travis-ci.org/Collaborne/gulp-mobile-splashscreens.svg?branch=master)](https://travis-ci.org/Collaborne/gulp-mobile-splashscreens)

Gulp plugin that creates PNG splashscreens for iOS and Android based on a SVG image

Please read this [blog post](https://medium.com/collaborne-engineering/the-pain-of-producing-mobile-icons-and-splash-screens-and-how-to-get-rid-off-it-b37372618ea0#.up1ljd9r9) for a detailed explanation of the problem that the plugin solves.

## Usage

To use the the plugin in your gulp process:

```javascript
const gulp = require('gulp');
const mobileSplashscreens = require('gulp-mobile-splashscreens');

gulp.task('default', [], function() {
    gulp.src('splashscreen.svg')
        .pipe(mobileSplashscreens())
        .pipe(gulp.dest('images'));
});
```

This will create all splashscreens in the folder `images/`.


### Cordova / PhoneGap

Add the following to your `config.xml` to use the icons in a Cordova/PhoneGap application:

```html
<platform name="ios">
    <!-- Splashscreens -->
    <splash src="images/ios-1080-portrait.png"       width="1080" height="1920"/>
    <splash src="images/ios-1080-landscape.png"      width="1920" height="1080"/>
    <splash src="images/ios-750-portrait.png"        width="750"  height="1334"/>
    <splash src="images/ios-750-landscape.png"       width="1334" height="750"/>
    <splash src="images/ios-1242-portrait.png"       width="1242" height="2208"/>
    <splash src="images/ios-1242-landscape.png"      width="2208" height="1242"/>
    <splash src="images/ios-640-portrait.png"        width="640"  height="1136"/>
    <splash src="images/ios-640-landscape.png"       width="1136" height="640"/>
    <splash src="images/ios-640-short-portrait.png"  width="640"  height="960"/>
    <splash src="images/ios-640-short-landscape.png" width="960"  height="640"/>
    <splash src="images/ios-320-portrait.png"        width="320"  height="480"/>
    <splash src="images/ios-320-landscape.png"       width="480"  height="320"/>
    <splash src="images/ios-2048-portrait.png"       width="2048" height="2732"/>
    <splash src="images/ios-2048-landscape.png"      width="2732" height="2048"/>
    <splash src="images/ios-1536-portrait.png"       width="1536" height="2048"/>
    <splash src="images/ios-1536-landscape.png"      width="2048" height="1536"/>
    <splash src="images/ios-768-portrait.png"        width="768"  height="1024"/>
    <splash src="images/ios-768-landscape.png"       width="1024" height="768"/>
</platform>

<platform name="android">
    <splash src="images/android-ldpi-portrait.png"     density="port-ldpi"/>
    <splash src="images/android-ldpi-landscape.png"    density="land-ldpi"/>
    <splash src="images/android-mdpi-portrait.png"     density="port-mdpi"/>
    <splash src="images/android-mdpi-landscape.png"    density="land-mdpi"/>
    <splash src="images/android-hdpi-portrait.png"     density="port-hdpi"/>
    <splash src="images/android-hdpi-landscape.png"    density="land-hdpi"/>
    <splash src="images/android-xhdpi-portrait.png"    density="port-xhdpi"/>
    <splash src="images/android-xhdpi-landscape.png"   density="land-xhdpi"/>
    <splash src="images/android-xxhdpi-portrait.png"   density="port-xxhdpi"/>
    <splash src="images/android-xxhdpi-landscape.png"  density="land-xxhdpi"/>
    <splash src="images/android-xxxhdpi-portrait.png"  density="port-xxxhdpi"/>
    <splash src="images/android-xxxhdpi-landscape.png" density="land-xxxhdpi"/>
</platform>
```

## FAQ

### Q: Why does iOS add a black background behind my splashscreen?

If you use a SVG with a transparent background, the `gulp-mobile-splashscreens`
will create splashscreens with transparent background. iOS always adds a black
background to those transparent splashscreens.

You need to add to your SVG a background if you want to have another color. It's important that the background area stretches beyond the image itself because `gulp-mobile-splashscreens` will otherwise add transparent areas around
the image to fill the target size of each splashscreen.

For example, this adds a red background to your splashscreens:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<svg width="375px" height="667px" viewBox="0 0 375 667" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <rect fill="red" width="10000" height="10000" transform="translate(-5000, -5000)"/>
    <!-- Your image -->
</svg>
```

## Credits

Sample icon made by [Freepik](http://www.freepik.com) from [www.flaticon.com](http://www.flaticon.com) is licensed by [Creative Commons BY 3.0](http://creativecommons.org/licenses/by/3.0/)
