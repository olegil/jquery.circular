jquery.circular
===============

— *No! Not yet another fraking carousel library!*

— But it's a dead-simple, modern one! It even has promises in it!

— *Oh? All right then.*

Default settings
----------------

* 4s display per slide
* 1s transition between slides
* starts on first slide (id == 0)
* responsive-friendly DOM convention for slides and controls

Usage
-----

``` jquery
$('.wannabe-carousel').circular()
```

with `.wannabe-carousel` a container for slides and slide's controls. By
default, it would be of the following shape:

``` haml
%div.wannabe-carousel
  %ul.slides
    %li.slide(data-id: 0)
      -# first slide's content
    %li.slide(data-id: 1)
      -# second slide's content
  %ul.controls
    %li.control(data-id: 0)
      -# first slide's control
    %li.control(data-id: 1)
      -# second slide's control
```

Events
------

### circular:fading

Triggered when the active slide is about to become unactive and "fade" out.

``` jquery
$('.wannabe-carousel').on('circular:fading', function(event, prevSlide, nextSlide) {
  // prevSlide is the "fading" slide
  // nextSlide is the slide about to become the selected one
});
```

### circular:selected

Triggered when a slide has been selected, either when a automated transition
occurs or when a manual selection was performed/triggered.

This event fires in between the transition's animation (typically, before the
selected slide "fades" in, and after the previously active slide has "fade"
out).

``` jquery
$('.wannabe-carousel').on('circular:selected', function(event, slide) {
  // slide is the selected slide
});
```

### circular:faded

Triggered when a slide has been selected and has been made visible, after the
transition's animation.

``` jquery
$('.wannabe-carousel').on('circular:faded', function(event, newSlide, prevSlide) {
  // newSlide is the new active, visible slide
  // prevSlide is the former active slide
});
```

API
---

### init

Inits the carousel. It should not be called more than once, and will be ran
automatically when calling `.circular` on a jQuery matcher.

### currentSlide

Returns the current slide's DOM element.

``` jquery
$('.wannabe-carousel').circular('currentSlide')
```

### currentControl

Returns the DOM element for the current slide's control.

``` jquery
$('.wannabe-carousel').circular('currentControl')
```

### current

Returns both slide and slide's control DOM elements as an object, under the
`slide` and `control` properties.

``` jquery
$('.wannabe-carousel').circular('current')
```

### jumpTo

* arguments: `event, [id]`

This is an event handler implementing the business logic involved when jumping
to a slide. By default, it relies on a default implementation that can be
overriden.

Bind events to the `jumpTo` handler to add custom interactions support. It
expects the DOM element you bind to to provide an `id` data-attribute matching
the slide's id you want to jump to, but in case this is not possible, an
explicit id can be passed as the second argument in the default implementation.

``` jquery
// Why not enabling transitioning to the fourth slide by hovering its control?
$('.slide-control[data-id="3"]').on('hover', $('.wannabe-carousel').circular('jumpTo'))

// let's say we are able to pick a random number among the slides indexes
id = randomInt(nbSlides)
$('body').on('click', 'a', $('.wannabe-carousel').circular('jumpTo', id))
```

About this plugin
-----------------

### What it is trying *not* to do

* Make unfair assumptions about your DOM tree
* Be overall complicated
* Provide styles, pictures…

"Trying" means those are my goals. For instance, it *does* make some unfair
assumptions about your DOM tree at the moment. Oh my!

### What it is trying to do

* [KISS](http://en.wikipedia.org/wiki/KISS_principle)
* Simple code so that one can hack on
* Use a convention over configuration approach, but remain fully tweakable
* Modern patterns ([proper jQuery Plugin's API](http://kaibun.net/blog/2013/04/19/a-fully-fledged-coffeescript-boilerplate-for-jquery-plugins/),
  Deferred-based architecture…)

### Maybe one day?

* Overridable transition effect/logic
* Allow the slides and the controls to be anywhere in the DOM (fully
  data-\* based), removing any unfair assumption about your DOM tree
* Extend the API with prev/next/pause/resume and provide default binding
  to matching event handlers, as been done for `jumpTo`
* Some more events (started, stopped, maybe paused/resumed)
* Some hooks (beforeStart, beforeStop, things like that)
* A demo page with examples and a nice design!

License
-------

MIT (see circular.coffee for details and credits/authorship).
