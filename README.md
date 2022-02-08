# jquery-same-height

jQuery function can be used to make selected elements the same height.


```javascript
jQuery(document).ready(function ($) {
    $(window).load(function () {
        mam_set_auto_height();
    });
    $(window).resize(function () {
        mam_set_auto_height();
    });
    mam_set_auto_height();
});
```

```javascript
function mam_set_auto_height() {
    // reset sh-active class
    $('.sh-active').css('height', 'auto');
    $('.sh-active').removeClass('sh-active');

    // get all elemets with same height data
    $ashElements = $("[data-same-height]");
    // loop through the elements 
    $ashElements.each(function () {
        $element = $(this);

        // skip if it's been configured already or not
        if ($element.hasClass('sh-active')) {
            return true;
        }
        // get group to set same height
        var _group = $element.attr('data-same-height');

        // get group elements
        $groupElements = $('[data-same-height="' + _group + '"]');

        // Cache the highest
        var highestBox = 0;

        // loop throgh the group elements
        $groupElements.each(function () {
            // If this box is higher than the cached highest then store it
            if ($(this).height() > highestBox) {
                highestBox = $(this).height();
            }
        });
        // Set the height of all those children to whichever was highest 
        $groupElements.addClass('sh-active').height(highestBox);
    });
}
```

Usage

```html
<!-- Example 1 -->
<div class="col-md-4" data-same-height="group-1"></div>
<div class="col-md-4" data-same-height="group-1"></div>
<div class="col-md-4" data-same-height="group-1"></div>

<!-- Example 2 -->
<div class="somediv">
    <div data-same-height="group-2"></div>
</div>
<div class="someotherdiv">
    <div data-same-height="group-2"></div>
</div>
```
