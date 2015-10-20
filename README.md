# Rhythm

Rhythm is an extraction of Compass's vertical rhythm module, removing all dependencies on Compass,
removing pixel-fallback and removing all mixins and functions unrelated to typography. I've made some changes, and added a few bits, but all credit to the original author: Eric M. Suzanne.

Rhythm is based on a simple idea drawn from typo(graphic) design; that a page should be structured around a grid. There are many excellent grid systems out there and most deal with horizontal units which are arranged either in explicit or implicit rows. Rhythm complements these systems by setting
up a vertical rythm running down the page based on a repeated unit - a line. You can use this rhythm to lock your page layout to. Rythm will take a font-size and maintain the rythm by setting the line-height of the element to the smallest multiple of those lines that it can. For example a smaller 14px equivalent font-size used for body copy might only need a single line, while an h1 title font-size of 32px equivilant might require three.

By ensuring each element on your page vertically takes up a multiple of the line unit, all the items sit on a vertical rhythm.

Rhythm supports three units; rems, ems and pixels.

Though you can use it on its own, this library is primarily built for use with its companion libraries; [box](https://github.com/Undistraction/box) and [position](https://github.com/Undistraction/position). By using a single conistant unit of rhythm shared between them, you can ensure this rhythm can be applied across all box-model properties and offsets.

## Docs

You can view the docs online [here](http://undistraction.github.io/rhythm/docs/) or locally in Chrome by running:

```
$ grunt docs
```

There is also a Grunt task to build the docs:

```
$ grunt sassdoc
```

## Tests

Tests are available from the excellent [Bootcamp](https://github.com/thejameskyle/bootcamp) and can
be run using:

```
$ grunt test
```

## API

### Configuration

Configure rhythm using the following variables.

The base font-size is the default font-size of your document. By default, browsers set a default
font-size of 16px, however you can change this if you wish.

```
$rhythm-base-font-size: 16px !default;
```

The base line-height is your unit of rhythm. You must set both this and `$base-line-height` to a pixel value, but don't worry. You can set the output to rems.

```
$rhythm-base-line-height: 21px !default;
```

The unit in which to output rhythm values (px | rem | em)

```
$rhythm-render-unit: rem !default;
```

If you want to allow rythm to lock everything to half rather than whole lines, set this to true.

```
$rhythm-round-to-nearest-half-line: false !default;
```

Ensure minimum leading above / below text. If necessary rhythm will increase the number of lines to ensure this minimum is met.

```
$rhythm-min-line-leading: 2px !default;
```

### Mixins

To set up the rhythm through your document use:

```
@include rhythm-establish();
```

This will render a selector targeting the `html` element which will set the desired `font-size` and `line-height`.

Your most used mixin will be `rhythm` itself. Pass it in a font-size and it will output the `font-size` and a `line-height` set to the necessary number of lines to accommodate the `font-size`:

```
@include rhythm(22px);
```

To set a specific number of lines, pass a second unitless number:

```
@include rhythm(22px, 4);
```

You can set a localised rhythm for a block of content by using a combination of `rhythm` and another mixin; `scoped-rhythm` which will temporarily set the base `font-size` and `line-height` to new values. This is powerful when used in a media-query;

```
@include rhythm-context(18px, 44px) {
  @include rhythm(24px);
}
```
