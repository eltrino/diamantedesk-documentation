Javascript Date() on steroids
=============

Javascript's native Date object on steroids by adding .format() as an output method.
Wrapped [@slevithan](https://github.com/slevithan)'s [source](http://blog.stevenlevithan.com/archives/date-time-format) in a bower installable, GitHub maintainable package.

### Installation

Dead simple. 

```sh
bower install date-steroids
```

### Usage 
Straight from http://blog.stevenlevithan.com/archives/date-time-format

```js
var now = new Date();

now.format("m/dd/yy");
// Returns, e.g., 6/09/07

// Can also be used as a standalone function
dateFormat(now, "dddd, mmmm dS, yyyy, h:MM:ss TT");
// Saturday, June 9th, 2007, 5:46:21 PM

// You can use one of several named masks
now.format("isoDateTime");
// 2007-06-09T17:46:21

// ...Or add your own
dateFormat.masks.hammerTime = 'HH:MM! "Can\'t touch this!"';
now.format("hammerTime");
// 17:46! Can't touch this!

// When using the standalone dateFormat function,
// you can also provide the date as a string
dateFormat("Jun 9 2007", "fullDate");
// Saturday, June 9, 2007

// Note that if you don't include the mask argument,
// dateFormat.masks.default is used
now.format();
// Sat Jun 09 2007 17:46:21

// And if you don't include the date argument,
// the current date and time is used
dateFormat();
// Sat Jun 09 2007 17:46:22

// You can also skip the date argument (as long as your mask doesn't
// contain any numbers), in which case the current date/time is used
dateFormat("longTime");
// 5:46:22 PM EST

// And finally, you can convert local time to UTC time. Either pass in
// true as an additional argument (no argument skipping allowed in this case):
dateFormat(now, "longTime", true);
now.format("longTime", true);
// Both lines return, e.g., 10:46:21 PM UTC

// ...Or add the prefix "UTC:" to your mask.
now.format("UTC:h:MM:ss TT Z");
```
