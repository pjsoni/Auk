# Auk, an image slideshow for iOS / Swift

[![Carthage compatible](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)][carthage]
[![CocoaPods Version](https://img.shields.io/cocoapods/v/Auk.svg?style=flat)][cocoadocs]
[![License](https://img.shields.io/cocoapods/l/Auk.svg?style=flat)](LICENSE)
[![Platform](https://img.shields.io/cocoapods/p/Auk.svg?style=flat)][cocoadocs]
[cocoadocs]: http://cocoadocs.org/docsets/Auk
[carthage]: https://github.com/Carthage/Carthage

This is an iOS library that shows an image carousel with a page indicator. Users can scroll through local and remote images or watch them scroll automatically.

* Allows to specify placeholder and error images for remote sources.
* Includes ability to simulate and verify image download in unit tests.
* Supports animated transition during screen orientation change.
* Includes image caching.

> This code is dedicated to the [great auk](https://en.wikipedia.org/wiki/Great_auk), a flightless bird that became extinct in the mid-19th century.

<img src='https://raw.githubusercontent.com/evgenyneu/Auk/master/Graphics/Screenshots/auk_paged_image_scroller_ios.jpg' alt='Great Auks by John Gerrard Keulemans' width='382'>

*Drawing of the great auk by John Gerrard Keulemans, circa 1900. Source: [Wikimedia Commons](https://en.wikipedia.org/wiki/Great_auk).*


## Setup

There are three ways you can add Auk to your Xcode project.

**Add source (iOS 7+)**

Simply add two files to your project:

1. Moa image downloader [MoaDistrib.swift](https://github.com/evgenyneu/moa/blob/1.0.50/Distrib/MoaDistrib.swift).
2. Auk image slideshow [AukDistrib.swift](https://github.com/evgenyneu/Auk/blob/master/Distrib/AukDistrib.swift).

**Setup with Carthage (iOS 8+)**

1. Add `github "evgenyneu/Auk" ~> 1.0` to your Cartfile.
2. Run `carthage update`.
3. Add `moa` and `Auk` frameworks into your project.

**Setup with CocoaPods (iOS 8+)**

If you are using CocoaPods add this text to your Podfile and run `pod install`.

    use_frameworks!
    pod 'Auk', '~> 1.0'


## Usage

import Auk

Add `import Auk` to your source code if you used Carthage or CocoaPods setup methods. Auk extends UIScrollView class by creating the `auk` property that you can use for showing images.

```Swift
// Show remote image
scrollView.auk.show(url: "http://site.com/bird.jpg")

// Show local image
scrollView.auk.show(image: UIImage(named: "bird"))

// Remove all images
scrollView.auk.removeAll()

// Return the number of pages in the scroll view
scrollView.auk.numberOfPages

// Get the index of the current page
scrollView.auk.currentPageIndex
```

#### Scrolling from code

```Swift
// Scroll to page
scrollView.auk.scrollTo(2, animated: true)

// Scroll to the next page
scrollView.auk.scrollToNextPage()

// Scroll to the previous page
scrollView.auk.scrollToPreviousPage()
```

#### Auto scrolling

```Swift
// Scroll images automatically with the interval of 3 seconds
scrollView.auk.startAutoScroll(delaySeconds: 3)

// Stop auto-scrolling of the images
scrollView.auk.stopAutoScroll()
```

## Configuration

Use the `auk.settings` property to configure behavior and appearance of the scroll view. See the [configuration manual](https://github.com/evgenyneu/Auk/wiki/Auk-configuration) for the complete list of configuration options.

```Swift
// Make the images fill entire page
scrollView.auk.settings.contentMode = UIViewContentMode.ScaleAspectFill

// Set background color of page indicator
scrollView.auk.settings.pageControl.backgroundColor = UIColor.grayColor().colorWithAlphaComponent(0.3)

// Show placeholder image while remote image is being downloaded.
scrollView.auk.settings.placeholderImage = UIImage(named: "placeholder.jpg")
```

## Size change animation

Read [animate size change](https://github.com/evgenyneu/Auk/wiki/Animate-size-change) manual if you need to animate the scroll view during device orientation change.


## Image caching

Auk uses [moa image downloader](https://github.com/evgenyneu/moa) for getting remote images. You can configure its caching settings by settings the `Moa.settings.cache.requestCachePolicy` property.


```Swift
// By default images are cached according to their response HTTP headers.
Moa.settings.cache.requestCachePolicy = .UseProtocolCachePolicy

// Use local cache regardless of response HTTP headers.
Moa.settings.cache.requestCachePolicy = .ReturnCacheDataElseLoad
```

## Remote image unit testing

One can simulate and verify remote image download in your unit tests. Please refer to the [moa unit testing manual](https://github.com/evgenyneu/moa/wiki/Unit-testing-with-Moa) for more information.


```Swift
// Autorespond with the given image to all image requests
MoaSimulator.autorespondWithImage("www.site.com", image: UIImage(named: "35px.jpg")!)
```

## Demo app

The project includes a demo iOS app.

<img src='https://raw.githubusercontent.com/evgenyneu/Auk/master/Graphics/Screenshots/auk_demo_app.gif' width='300' alt='Auk pages scroll view demo iOS app'>

## Alternative solutions

Here is a list of other image slideshow libraries for iOS.

* [kimar/KIImagePager](https://github.com/kimar/KIImagePager)
* [kirualex/KASlideShow](https://github.com/kirualex/KASlideShow)
* [nicklockwood/iCarousel](https://github.com/nicklockwood/iCarousel)
* [nicklockwood/SwipeView](https://github.com/nicklockwood/SwipeView)
* [paritsohraval100/PJR-ScrollView-Slider](https://github.com/paritsohraval100/PJR-ScrollView-Slider)

## Credits

* The Great Auk drawing by John James Audubon, 1827-1838. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:341_Great_Auk.jpg).
* Great Auks drawing by John Gerrard Keulemans, circa 1900. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Great_auk_with_juvenile.jpg).
* The Great Auk drawing from Popular Science Monthly Volume 62, 1902-1903. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:PSM_V62_D510_The_great_auk.png).
* Great Auk egg, U. S. National Museum, in a book by Arthur Cleveland Bent, 1919. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Great_Auk_Egg_Bent.jpg).
* Only known illustration of a Great Auk frawn from life by Olaus Wormius, 1655. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Wormius%27_Great_Auk.jpg).
* The Great Auks at Home, oil on canvas by John Gerrard Keulemans. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Pinguinus.jpg).
* Alca impennis by John Gould: The Birds of Europe, vol. 5 pl. 55, 19th century. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Alca_Impennis_by_John_Gould.jpg).
* Great Auks (extinct) in summer and winter plumage by John Gerrard Keulemans, before 1912. Source: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Keulemans-GreatAuk.jpg).



## License

Auk is released under the [MIT License](LICENSE).
