# HTML/CSS

## HTML (HyperText Markup Language)

It's all about Semantic, which leads to better SEO purpose.

Becoming a super hero is a fairly straight forward process:

* `em` > `i` **** (_example_)/ **** `strong` **** > **** `b` (**example**)&#x20;
* `<img alt="" />`should put the content in alt for better to be search. Of course, the content should be highly related to the description of the image.
* `tbody` has the benefit to show the content when your view can see the content. Previous work may show all the contents at the beginning.

{% hint style="warning" %}
Log-in validation or financial related validation is better to construct in backend than frontend. In case of some hackers may take a detour instead of your frontend validation.
{% endhint %}

## CSS (Cascading Style Sheets)

* `article > p` **>** `p`more specific more to be select.
*   `box-sizing: border-box` box-sizing define the width and height to which scope. If `box-sizing: content-box` the scope will  be in blue box. If `box-sizing: border-box` the scope will  be in yellow box. You can have `padding-box` and `margin-box`. Then you try to set padding over `box-sizing: border-box` . The padding will start from border into the element, except outer of it.

    ![https://ithelp.ithome.com.tw/upload/images/20201013/20112550MWKjlQlrdq.png](https://ithelp.ithome.com.tw/upload/images/20201013/20112550MWKjlQlrdq.png)
* You can not set height and width to inline element, unless you change it to `display: block`. `a` tag can be set to be `display: inline-block` to better implement in **nav bar**.
* css reset will clean all style from all default tag. But css normalized only reset the some of it, depending on the file you import. `Link` tag in HTML should be in higher hierarchy  than your custom css file. [https://necolas.github.io/normalize.css/](https://necolas.github.io/normalize.css/)
* `float: left` which needs to add with `clear: both` at the end of tag with class or its parent class. Although we can use Flexbox and Grid to solved, you may need to deal with some tech stack.
* `list-style: none` and `text-decoration: none` to cancel the default style from some html tag.
*   [https://caniuse.com/flexbox](https://caniuse.com/flexbox) & [https://flexboxfroggy.com/](https://flexboxfroggy.com)\
    `display: flex` go with`flex-direction` ,

    `flex-wrap` , `justify-contnet` and `align-items`and&#x20;

    `align-content` (with wrapped item and multiple lines).&#x20;

    `flex-grow`to fill the rest of extra space.`flex-shrink` to shrink target element for other brother elements. `order`d to make target element to be head, origin and tail.
* When user click or tap the button or something, use rwd in tailwind with another css value for hover state (hover sticky)
