# CSS Training Path - Notes
<!-- order:10 -->

## SASS
- Sass vs Scss
	- The difference is syntax. Underneath the textual exterior they are identical.
	- ![image](Attachments/CleanShot%202023-07-28%20at%2010.40.37%402x.png)
- Is a preprocessor
	- Once you start tinkering with Sass, it will take your preprocessed Sass file and save it as a normal CSS file that you can use in your website.
	- Running `sass input.scss output.css` from your terminal would take a single Sass file, `input.scss`, and compile that file to `output.css`.
- You can also watch individual files or directories with the --watch flag. The watch flag tells Sass to watch your source files for changes, and re-compile CSS each time you save your Sass.
	- Sass would watch all files in the `app/sass` folder for changes, and compile CSS to the `public/stylesheets` folder.
- Variables
	- When the Sass is processed, it takes the variables we define for the `$font-stack` and `$primary-color` and outputs normal CSS with our variable values placed in the CSS.
- Nesting
	- CSS not support it, SCSS does
	- ![image](Attachments/CleanShot%202023-07-28%20at%2010.43.54%402x.png)
- Partials
	- `_partial.scss`
	- The underscore lets Sass know that the file is only a partial file and that it should not be generated into a CSS file. Sass partials are used with the `@use` rule.
		- This rule loads another Sass file as a _module_, which means you can refer to its variables, [mixins](https://sass-lang.com/guide/#mixins), and [functions](https://sass-lang.com/documentation/at-rules/function) in your Sass file with a namespace based on the filename.
		- ![image](Attachments/CleanShot%202023-07-28%20at%2010.56.28%402x.png)
- Import
	- The `@import` directive allows you to include the content of one file in another.
	- It's different from the `@use`, as `@use` is more like use the `PARTIALS` only
- Mixins
	- A mixin lets you make groups of CSS declarations that you want to reuse throughout your site.
		- You can even pass in values to make your mixin more flexible.
		- ![image](Attachments/CleanShot%202023-07-28%20at%2010.57.09%402x.png)
- Extends
	- ![image](Attachments/CleanShot%202023-07-28%20at%2011.14.36%402x.png)
- Mixins vs Extends vs Placeholders
	- Mixins when dynamic variables
	- Extends and Placeholders **does** combine selectors while Mixins not(the generated css is not grouped):
		- Extends
			- ![image](Attachments/CleanShot%202023-08-02%20at%2013.15.27%402x.png)
		- Mixins
			- ![image](Attachments/CleanShot%202023-08-02%20at%2013.15.50%402x.png)
		- Placeholders
			- Like extends, **do** regroups, but the genarated css not include the placholder:
				- ![image](Attachments/CleanShot%202023-08-02%20at%2013.17.47%402x.png)
	- ![image](Attachments/CleanShot%202023-08-02%20at%2013.18.24%402x.png)
	- When in doubt, use **mixins**. They generate more CSS lines and are less elegant than extend/placeholders, but they are straightforward.
- Nested Properties
	- Many CSS properties have the same prefix, like font-family, font-size and font-weight or text-align, text-transform and text-overflow.
	- With Sass you can write them as nested properties:
		- ![image](Attachments/CleanShot%202023-07-28%20at%2011.21.06%402x.png)

## Tailwind
- Tailwind CSS works by scanning all of your HTML files, JavaScript components, and any other templates for class names, generating the corresponding styles and then writing them to a static CSS file.
- Ways to use Tailwind
	- Use CLI
	- PostCSS
	- Framework Guides(like, how to use it in Next.js)
	- Play CDN
- Since Tailwind is a PostCSS plugin, there’s nothing stopping you from using it with Sass, Less, Stylus, or other preprocessors, just like you can with other PostCSS plugins like Autoprefixer.
- Performance
	- Tailwind CSS is incredibly performance focused and aims to produce the smallest CSS file possible by only generating the CSS you are _actually using_ in your project.
	- Combined with minification and network compression, this usually leads to CSS files that are less than 10kB, even for large projects.
	- For example, Netflix uses Tailwind for Netflix Top 10 and the entire website delivers only 6.5kB of CSS over the network.
- Compare
	- ![image](Attachments/CleanShot%202023-07-28%20at%2011.55.30%402x.png)
	- The traditional
		- ![image](Attachments/CleanShot%202023-07-28%20at%2011.56.02%402x.png)
	- The TW way
		- ![image](Attachments/CleanShot%202023-07-28%20at%2011.56.10%402x.png)
- Now I know what you’re thinking, “this is an atrocity, what a horrible mess!” and you’re right, it’s kind of ugly. In fact it’s just about impossible to think this is a good idea the first time you see it — you have to actually try it.
	- **You aren’t wasting energy inventing class names**
	- **Your CSS stops growing**
	- **Making changes feels safer**
		- CSS is global and you never know what you’re breaking when you make a change.
- Why not just use inline styles? Yes, but diff
	- **Designing with constraints**.
		- Using inline styles, every value is a magic number.
	- **Responsive design**
		- You can’t use media queries in inline styles
	- **Hover, focus, and other states**
- Manage commonly repeated utility combinations.
	- This is easily solved by extracting components and partials.
		- ![image](Attachments/CleanShot%202023-07-28%20at%2013.33.39%402x.png)
	- Maintaining a utility-first CSS project turns out to be a lot easier than maintaining a large CSS codebase
		- If you can quickly edit all of the duplicated class lists simultaneously, there’s no benefit to introducing any additional abstraction.
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.09.06%402x.png)
	- A lot of the time a design element that shows up more than once in the rendered page is only actually authored once because the actual markup is rendered in a loop.
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.14.56%402x.png)
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.16.07%402x.png)
	- Even if you create classes for the different elements in a component like this, you still have to duplicate the HTML every time you want to use a component.
		- Components and template partials solve this problem much better than CSS-only abstractions because a component can encapsulate the HTML _and_ the styles.
	- Use `@apply`
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.25.20%402x.png)
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.25.26%402x.png)
		- Whatever you do, **don’t use `@apply` just to make things look “cleaner”**.
			- If you start using `@apply` for everything, you are basically just writing CSS again and throwing away all of the workflow and maintainability advantages Tailwind gives you, for example:
				- **You have to think up class names all the time**
				- **You have to jump between multiple files to make changes**
				- **Changing styles is scarier**
				- **Your CSS bundle will be bigger**
- Apply classes conditionally `hover:bg-sky-700`
	- These modifiers can even be [stacked](https://tailwindcss.com/docs/hover-focus-and-other-states#ordering-stacked-modifiers) to target more specific situations `dark:md:hover:bg-fuchsia-600`
- Responsive
	- ![image](Attachments/CleanShot%202023-07-28%20at%2014.02.01%402x.png)
	- Customize breakpoints
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.03.19%402x.png)
	- Arbitrary values
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.03.38%402x.png)
- Dark mode
	- `dark:bg-slate-800`
	- If you want to support toggling dark mode manually
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.04.38%402x.png)
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.04.54%402x.png)
- Customizing your theme
	- If you want to change things like your color palette, spacing scale, typography scale, or breakpoints
		- ![image](Attachments/CleanShot%202023-07-28%20at%2014.28.44%402x.png)
- Using arbitrary values
	- ![image](Attachments/CleanShot%202023-07-28%20at%2014.29.23%402x.png)
- Use the components layer for any more complicated classes you want to add to your project that you’d still like to be able to override with utility classes.
	- ![image](Attachments/CleanShot%202023-07-28%20at%2014.30.30%402x.png)

## Bootstrap
- Main go is to make responsive webs
- Bootstrap vs Tailwind
	- Bootstrap is a great choice if you're looking for a ready-made and consistent solution that covers most web design scenarios and saves time
	- _Bootstrap is used for creating responsive web and mobile applications_ whereas Tailwind CSS is used to create customized user interfaces.
	-  **If your project contains more of backend work and requires common layouts, then Bootstrap will be better**.
- Support css classses to style like Tailwind
- Support css for components
- Not need to use JS
	- Not even when use the interactive components like carousels or offcanvas. Just HTML attributes or CSS classes
	- But some components, well, still need a bit
		- To initialize the components
- The default style of classes is gud, not need custom much
- Have a grid system that's very easy to use. It's like the flexbox + grid of basic css have a child.
- In Nimble
	- Use frameworks styles in CSS instead of using the framework helper classes in the HTML 
	- Re-use the underlying implementation of the framework e.g. Bootstrap grid `row-` and `col-` classes use the utilities `make-row()` and `make-col()`.
		```css
		.users.show {
		  main {
			@include make-container();
		  }
		
		  .user-profile {
			@include make-row();
		
			&__header {
			  @include make-col(6);
			}
		  }
		}
		```

- Flexbox vs Bootstrap
	- Flexbox does the opposite by staying flexible to the items’ size and contents; which is similar to using pixels vs em/rem, or like controlling your divs only using margins and padding and never setting a pre-defined size.
	- As Bootstrap uses floats, it needs clearfix after each row; otherwise, we will get misaligned divs of different height.
		- Flexbox doesn’t use floats; instead, it checks for the tallest div in the container and sticks to its height.
	- Flexbox layout is most appropriate to an application’s components and small-scale layouts, while Bootstrap is intended for smaller or larger scale layouts.
	- Flexbox is not an alternative to Bootstrap

## Responsive web design
- 3 things
	- A Fluid Foundation
	- Flexible Content
	- Media Queries
- A Fluid Foundation
	- ![image](Attachments/CleanShot%202023-08-01%20at%2011.09.23%402x.png)
	- Should also percentage the main container
		- ![image](Attachments/CleanShot%202023-08-01%20at%2011.14.27%402x.png)
	- Old browsers used to round up or down the percentages, which make it look weird. But now they are gud.
- Flexible Content
	- `max-width`
		- ![image](Attachments/CleanShot%202023-08-01%20at%2011.28.38%402x.png)
			- => means: show an image as its native size when it's smaller than its container(100%). It will never be larger than its native resolusion
			- Before
				- ![image](Attachments/CleanShot%202023-08-01%20at%2011.33.26%402x.png)
				- ![image](Attachments/CleanShot%202023-08-01%20at%2011.33.33%402x.png)
			- After
				- ![image](Attachments/CleanShot%202023-08-01%20at%2011.32.51%402x.png)
				- ![image](Attachments/CleanShot%202023-08-01%20at%2011.33.09%402x.png)
			- If we set the height, things go weird
	- `object-fit`(not really in this course but yeah)
		- The CSS object-fit property is used to specify how an <img> or `<video>` should be resized to fit its container.
		- original image, 400 x 300
			- ![image](Pasted image 20230801113646.png)
		- if set fixed, 200 x 300, it break
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.37.13%402x.png)
		- `object-fit: cover`: keep aspect, still 200 x 300 but cut the part of the image that overflow
		- `object-fit: contain;`: keep aspect, but resize to smaller image
			- or do this
				- ![image](Attachments/CleanShot%202023-08-01%20at%2017.25.53%402x.png)
		- `object-fit: fill;`: resized to fill, maybe strech or squished, not keep aspect
	- Ratio
		- a trick to make it maintains 2:1 ratio:
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.43.39%402x.png)
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.44.43%402x.png)
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.44.34%402x.png)
		- 4:1 ratio:
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.44.09%402x.png)
			- ![image](Attachments/CleanShot%202023-08-01%20at%2011.44.22%402x.png)
		- although it's `padding-bottom` percentage, it's actually calculated on the width, not height. Weird.
	- units
		- `em` vs `rem`
			- `rem` relative to root element("root em")
				- 1 `rem` equals the font size of the html element, which default `16px`
			- `em` relative to parent element
				- They can cascade and cause unexpected results
		- check `flexi` project:
			- no `em`, all `rem`, like `rem(16px)`, seems like a custom rem function
			- no `px`
- Media Queries
	- We should use these tricks to keep the content as flexible as we are, but there will still be a point that we need to make a large shift to layout. Time for media queries.
	- check `flexi` project:
		- not very much media queries, maybe because it's a dashboard, so only web?
	- large first
		- use `max-width`:
		- ![image](Attachments/CleanShot%202023-08-01%20at%2012.16.17%402x.png)
		- if small devices can't see all, they will still download all assets first, which is bad
	- small first
		- is mobile-first
		- use`min-width`
		- ![image](Attachments/CleanShot%202023-08-01%20at%2012.16.59%402x.png)
	- the common way to choose breakpoints
		- is not based on popular devices
		- but based on just when the content and layout need to change. that's it
	- `width` vs `device-width`
		- `width` is like the current width, it can be smaller or equal of the width of the device
		- `device-width`is something fixed because, well, physically fixed
	- `@media print`
		- => target printers
	- `@media screen`
		- => target screen devices
- Other considerations
	- Touch Target Area
		- Apple recommends minimum `44px × 44px`
		- Using padding instead of margin
			- Paddings increase touching area
	- Hover
		- Don't hide content behind :hover
		- Require the users to click to show sub-categories is beter than hover
			- ![image](Attachments/CleanShot%202023-08-01%20at%2012.35.15%402x.png)
	- Constrast
		- Laptops? Maybe in a fixed area
		- Mobiles? Bring everywhere, even in the sun
		* Try your site outside in the sun
		* Try your site in bed when it's dark
	* Readability
		* Small screen != small type
		* Consider increasing font size
* Ways to optimize an image
	* Create many versions of one when upload to servers
	* Detect and change versions of images with each APIs called
		* Still this, but use other services. Calls to their domain instead of our domain to get an image.
		* Not optimal
* `box-sizing: border-box;`
	* to ignore the padding and border, the width is still the same(not `120px`(`padding` `10px`), but `100px`)
	* many developers want all elements on their pages to work this way.
* `background-image`
	* when not need to load images from servers, lke in a small media query, can use `display: none`
* Polyfill
	* A polyfill is a piece of code (usually JavaScript) used to provide modern functionality on older browsers.
		* Since it use JS, it may have some performance concerns
	* For example, a polyfill could be used to mimic the functionality of a text-shadow in IE7
	- Or the polyfill to support media queries on old browsers
	- Very easy to use, just include it
- `ajax-include-pattern`
	```html
	<a href="..." data-append="articles/latest/fragment" data-media="(min-width: 30em)">Latest Articles</a>
	```
	- only calls some additional apis when on desktop
- `eSSential`
	- ![image](Attachments/CleanShot%202023-08-01%20at%2015.46.22%402x.png)
	- conditionally loads css files
- Cost when do the responsive(back then, in their processes)
	- ![image](Attachments/CleanShot%202023-08-01%20at%2015.48.55%402x.png)
	- On first sites, 2 3 times

## CSS: Specificity, the Box Model, and Best Practices
- float
	- do ppl still use it?
		- "No! Well, mostly. I’d only use it today for wrapping text around images, though and I’d avoid using `float` entirely for layouts."
		- "Wrapping text around an image (an exceedingly rare case); nothing more."
		- [ref](https://css-tricks.com/is-css-float-deprecated/)
- yet another way to center blocks: `margin: auto`
- margin collapse
	- ![image](Attachments/CleanShot%202023-08-01%20at%2017.18.22%402x.png)
	- it get the bigger margin, not the sum
	- You can consider an element’s margin as the **minimum space** it want to stay _away_ from other elements.
	- but will not occure when 1 or 2 block element:
		- Padding or border
		- Relative or absolute positioning
		- A float left or right
- clearfixes
	- ![image](Attachments/CleanShot%202023-08-02%20at%2009.50.35%402x.png)
	- we can add `overflow: auto;` to the containing element to fix this problem
	- the `overflow:auto` clearfix works well as long as you are able to keep control of your margins and padding (else you might see scrollbars).
	- the new, modern clearfix hack however, is safer to use, and the following code is used for most webpages:
		- ![image](Attachments/CleanShot%202023-08-02%20at%2009.51.33%402x.png)
- images
	- Content should be marked up as inline images
	- Layout elements should be defined as background images
	- When hover to change image, prefer using same image, to reduce another http call to get the second image(called sprite)
		- ![image](Attachments/CleanShot%202023-08-01%20at%2017.29.07%402x.png)
		- or use base64
			- ![image](Attachments/CleanShot%202023-08-01%20at%2017.30.38%402x.png)

## BEM
- A node may be an element within one block and (at the same time) a container for another block.
- A DOM node being reused to host more than one BEM entity is called a “BEM mixin.”
- We are abusing the CSS inheritance model. There, I said it. I know that the “C” of CSS stands for “Cascading”, but that doesn’t mean we need to cascade from the simplest selector all the way down to a complex component.
	- ![image](Pasted image 20230802101449.png)
	- Cascading in CSS is like Multiple Inheritance
- “For me, a larger total CSS codebase, made up of components that are in many respects insulated from one another, is preferential to a smaller CSS codebase made up of inter-dependent and intrinsically related styles.”
- "The reason I choose BEM over other methodologies comes down to this: it is less confusing than the other methods (i.e. SMACSS) but still provides us the good architecture we want (i.e. OOCSS) and with a recognizable terminology. - Mark McDonnell, Maintainable CSS with BEM"
- Blocks, Elements and Modifiers
	- Block
		- Standalone entity that is meaningful on its own.
		- Examples
			- header, container, menu, checkbox, input
	- Element
		- A part of a block that has no standalone meaning and is semantically tied to its block.
		- Examples
			- menu item, list item, checkbox caption, header title
	- Modifier
		- A flag on a block or element. Use them to change appearance or behavior.
		- Examples
			- disabled, highlighted, checked, fixed, size big, color yellow
	- ![image](Pasted image 20230801174850.png)
	```html
	<button class="button">
		Normal button
	</button>
	<button class="button button--state-success">
		Success button
	</button>
	<button class="button button--state-danger">
		Danger button
	</button>
	```
- Benefits
	- Modularity
		- Block styles are never dependent on other elements on a page, so you will never experience problems from cascading.
		- BEM tries to get the best out of today’s CSS concerning modularity
			- Avoids inheritance
				- CSS Inheritance is infinite.
				- There’s no function scope or closure like in programming.
			- Provides some sort of scope
			- Reduces style conflicts of CSS **specificity**
	- Reusability
		- Composing independent blocks in different ways, and reusing them intelligently, reduces the amount of CSS code that you will have to maintain.
	- Structure
		- BEM methodology gives your CSS code a solid structure that remains simple and easy to understand.
- Arguments
	- "My HTML looks all bloated and messy with BEM!"
		- There is no way to get around inheritance other than sticking unique CSS classes
		- Even if the context doesn’t exist yet, it may be expanded until someone adds another module or component to your HTML.  — Think of modularity as any module may contain further modules!
	- "Why not use element type selectors with child or sibling combinators (like ul > li + li) to avoid inheritance issues?"
		- Nested selectors raise CSS specificity.
		- Your CSS would be sort of tight coupled with the HTML.
		- Modular contexts require low specificity!

## Marksheet guide
### Web
- Protocols
	- Each of them serves a different purpose:
		- FTP: File transfer
		- SMTP: Sending Emails
		- IMAP: Receiving Emails
		- IRC: Chat
		- HTTP: Browsing HTML documents (Webpages)
- On your computer, you probably have different types of files
	- Each of these types of files can be opened by a specific program. Some of these programs can only open these files, while others can both open and create files.
	- iTunes can open .mp3 files but can not create them.
	- Microsoft Word can however both open and create .doc files.

### HTML
- A browser is a document viewer. What kind of document? Webpages.
	- The program used to open HTML documents is a browser, like Firefox or Google Chrome.
	- The program used to create HTML documents is a text editor, like Notepad++ or Sublime Text.
- Remember that an HTML document can be opened in 2 ways:
	- by a text editor who sees the source code
	- by a browser who interprets the source code
- HTML code is purely semantic: you provide meaning to your text.
	- Like any language, HTML comes with a set of rules. These rules are relatively simple. It comes down to defining boundaries, to know where something starts and where something ends.
	- There are 16 HTML attributes that can be used on any HTML element. All of them are optional.
- HTML has 2 main types of elements
	 - block elements like: `<p>`
		 - **Block** elements are meant to **structure** the main parts of your page, by dividing your content in _coherent_ blocks.
		 - Only have opening and closing tags, NOT self-enclosing tags
	 - inline elements like: `<a>`
		 - **Inline** elements are meant to differentiate _part_ of a text, to give it a particular function or meaning. Inline elements usually comprise a single or few words.
		 - Have opening and closing tags AND self-enclosing tags
- The purpose of HTML tags is to deliver meaning to a document. Don’t be concerned about how your webpage looks like. Focus on the significance of each tag you’ll use.
- When apparently no semantic element seems suited for your content but you still want to insert an HTML element (either for grouping or styling purposes), you can settle for one of the two generic elements:
	- `<div>` for block-level elements
	- `<span>` for inline elements
- There are about [100 semantic HTML elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Element) to choose from.
- When inserting an image in HTML, you **don’t need to specify its dimensions**: the browser will automatically display it in **full size**.
	- An image is not an HTML block element but actually an inline element.
- Just like a webpage can have a header and a footer, a table can have a head, a body, and a foot. As anything in HTML, this is purely for semantic reasons: providing more structure to your table.
- While navigating the Web, a user’s interaction is mostly only to click on **links** in order to navigate through webpages.
	- But the Web understands that a user is sometimes required to provide his own **input**.
	- To accomodate for these needs, HTML provides interactive **form controls**

### CSS
- Basics
	- The word _“Style”_ can be deceiving. You might think CSS is only used to change the text’s color, size, and font. But CSS is able to define an HTML document’s **layout**, by defining heights, widths, inner and outer margins, positions, columns…
	- who { what: how; }
	- Only a few CSS properties can be inherited from ancestors. They are mainly text properties:
		- text color
		- font (family, size, style, weight)
		- line-height
	- There is no such thing as an _unstyled_ HTML element. Every webpage uses at least one CSS: the **User agent Stylesheet**.
		- A browser’s _default_ styles can **interfere** with the styles we _actually_ want to apply. That’s why a **CSS reset** has been devised to provide a **consistent base** across all browsers.
			- `<link rel="stylesheet" type="text/css" href="reset.css">`
- Font
	- Fonts are grouped in 5 **generic** families:
		- `serif` fonts have small lines attached to the end of each character
		- `sans-serif`
		- `monospace`
		- `cursive`
		- `fantasy` 
	- Specific font
		- `body{ font-family: Arial;}`
		- Your webpage will use Arial **provided it is installed on the user’s computer**.
		- If the Arial font is not available on the user’s computer, it will use the browser’s default serif font (which is usually Times).
		- Arial is a safe choice though, because it is installed on all Windows and Mac computers, and on most Linux systems.
			- Arial is considered a **web-safe** font
	- It is possible to **include a font** in a webpage. That way, they make sure the font is available even if it’s not present on the user’s computer, simply because the website provides the font.
	- Bear in mind that setting a font size of `16px` won’t make each letter `16px` high. The _actual_ size of each letter depends on the font-family used.
	- The `line-height` property, when applied to block-level element, defines, as its name literally suggests, the **height of each line**.
		- It is **not** to be confused with the line spacing which determines the amount of space _between_ lines in a paragraph.
		- Although they both carry the same purpose (spacing lines of text), they do so in different ways.
		- ![image](Pasted image 20230802115505.png)
		- Because readibility is dependent upon the size of the text, it is recommended to use a **dynamic** value that is relative to the size of the text.
		- Because using `%` or `em` values can have unexpected values, the recommended method is **unitless numbers**: `body{ font-size: 16px; line-height: 1.5;}`
- Box models
	- By default, every HTML element is rendered in the browser as a **rectangle**.
		- The dimensions of that rectangle are **dynamic**: they vary according to the _content_ of that element.
		- A block-level element, like a paragraph, will **horizontally** take up all the space it can
	- Backgrounds are only applied on the targeted element. But considering most HTML elements have a transparent background
	- The difference between HTML images <img> and CSS background images
		- The HTML `<img>` element is for images that are part of the **content**, while CSS background images are purely **decorative**.
			- The logo of a company, the thumbnail of a gallery, the picture of a product… These are all considered **content** and should use the HTML `<img>` element.
			- A diagonal pattern, a beautiful landscape, a cart icon… These can be considered as **decorative**, as they _support_ the content but are not _part_ of it. If they were to disappear, the webpage would still make sense.
	- By default, a background image will repeat itself indefinitely. You can specify its **original position**, by choosing a horizontal `x` value, and a vertical `y` one.
	- `p{ display: inline;}`
		- Why not use an HTML inline element, like `<span>` then?
		- Because you choose an HTML element for its **meaning**, not its rendering.
		- We must not change the tag _only for styling purposes_
	- In short, `display` allows to alter the **type** of an element _without_ changing its **meaning**.
	- The CSS property `visibility` is slightly similar to `display`. Applying `visibility: hidden;` _hides_ an element from your page, but only turns it **invisible**: it still takes up the space it was supposed to.
	- `blockquote { width: 600px; }`
		- The blockquote will not take up the whole width available, but will remain 600px wide in any situation:
			- if the browser window is less wide than 600px, it will show a horizontal scrolling bar
			- if the browser window is wider than 600px, the blockquote will stay 600px wide and not take up the whole space
		- Because we’ve only set the width, the blockquote remains fluid in **height**: the height becomes the variable dimension to fit the blockquote’s content.
		- By setting the dimensions of an element, it will remain fixed no matter the length of its content.
			- What happens if the content is longer than the element can contain?
				- Because we prevent the element to dynamically alter its dimensions, there is a chance the content will be longer than the element accomodates for and will subsequently `overflow`.
	- `padding` vs `margin`
		- This question comes up when no border nor background is applied
			- If a border or a background is set on _either_ element, the visual rendering will be different.
	- When all 4 sides (top, bottom, left and right) are involved in a CSS property, that CSS property also acts as a **shorthand** property.
- The **flow**
	- Even without any CSS applied, an HTML document already has its own rules:
		- fluidity: how the content adapts to browser dimensions
			- All `block` elements are **fluid**. They will naturally adapt their layout to accommodate their inner content:
				- **width: 100%**  
				    a block will take up the whole width available
				- **word wrap**  
				    if a block’s inline content doesn’t fit on a single line, it will continue on a new line
				- **height: auto**  
				    a block’s height varies automatically to match its content’s size
		- ordering: in which order elements appear
		- stacking: how elements appear on top of each other
			- A browser has **3 dimensions**.
			- Each **nested** element appears _on top_ of its parent.
			- The **deeper** in the hierarchy, the _higher_ in the stack.
	- Breaking the flow
		- Several CSS properties allow to **disrupt** the Flow:
		- `height` and `width` can alter an element’s **fluidity**
		- `float` **disrupts** an element’s behavior as well as its surroundings
		- `position` `absolute` and `fixed` **remove** an element from the Flow
		- `z-index` can alter the order in which elements are **stacked**
	- Positions
		- When the `position` is set to **relative**, an element can move according to its **current position**.
		- When the `position` is set to **absolute**, an element can move according to the **first positioned ancestor**.
			- Can set some parent to be **relative** then the **absolute** will move according to it
	- `float`
		- The most unpredictable property
		- The most difficult CSS concept to grasp
		- It is the one that most _influences_ its **surroundings**.
			- In other words, applying a float not only modifies the element it’s applied upon **but also alters its ancestors, siblings, descendants, and following elements**.
		- The purpose of **floating** an element is to **push it to one side** and make the text **wrap around it**.
	- Only **1/3** of CSS properties can be animated
	- Transitions vs animations
		- So CSS transitions are _specific_ kind of animations, where:
			- there’s only 2 states: start and end
			- the animation doesn’t loop
			- the intermediate states are only controlled by the timing function
		- Well what if you want:
			- to have control over the **intermediate** states?
			- to make an animation **loop**?
			- different animations on the _same_ element?
			- to animate a specific property only **halfway** through the animation?
			- to simulate **different timing functions** for different properties?
		- CSS animations allow all of this, and more.
- Responsiveness
	- ![image](Pasted image 20230802130024.png)
	- What options are available to handle mobile devices?
		1. **Not doing anything** and let mobile users zoom in to read your website
		2. Create a **second** website, like [m.facebook.com](https://m.facebook.com/), and redirect mobile devices to that website
		3. Use **responsive web design**
	- The **width** parameter is the most used one in responsive web design. This comes from the fact that **webpages are read vertically**: we scroll to read the hidden content. As a result, the width is fixed and constrained, while the height of the website is variable.

## Others
### HTML
- The reason IE is so reviled and is now deprecated
	- It did not conform to the W3C standards for CSS and certain features of Javascript
	- Had many “quirks” that made writing efficient web sites that relied heavily on CSS and Javascript that would present well on Netscape (the predecessor of Firefox), Opera, Safari, and MSIE was nearly impossible.
- Chromium
	 - Chromium is a free and open-source web browser project, mainly developed and maintained by Google.
	 - Chromium makes it easier for engineers to develop new browser ideas faster.
	 - There is little to no browser-specific development anymore.
		 - For a CSS property to become accepted as a W3C recommendation it has to be implemented in two different browsers and all the people working in the CSS working group have to agree that it’s useful.
- Non-semantic HTML
	- **Poor SEO**
	- **Poor Accessibility**
		- Example, users can not `tab` if all are `div`s
	- **Hard to maintain**
		- Yes, the maintaining devs still can change the `div`s, but it will be harder to differentiate
	- **Incompatible with other intergrations**
		- Like other libs use the standard HTML tags instead of `div`s
- How to use more Semantic HTML(Tags I not use enough)
	- `header` & `footer`
	- `main`
		- The main content area of a document includes content that is unique to that document and excludes content that is repeated across a set of documents such as site navigation links, copyright information, site logos and banners and search forms
	- `<section>`
		- It's basically just a `<div>` with special semantic meaning
		- When an element is needed only for styling purposes or as a convenience for scripting, authors are encouraged to use the `<div>` element instead.
		- A general rule is that the `<section>` element is appropriate only if the element’s contents would be listed explicitly in the document’s outline.
	- `<article>`
	- `<nav>`
- How Google show Q & A?
	- ![image](Attachments/CleanShot%202023-08-02%20at%2011.15.41%402x.png)
	- To make up with [schema.org](https://schema.org/)
	- Properly marked up pages are eligible to have a rich result displayed on the search results page.
	```html
	<div itemscope itemtype="https://schema.org/Event">
	  <div itemprop="name">Spinal Tap</div>
	  <span itemprop="description">One of the loudest bands ever
	  reunites for an unforgettable two-day show.</span>
	  Event date:
	  <time itemprop="startDate" datetime="2011-05-08T19:30">May 8, 7:30pm</time>
	</div>
	```
	- [Ref](https://developers.google.com/search/docs/appearance/structured-data/qapage)

### Others
- Image compression
	- Image compression most often works either by removing bytes of information from the image, or by using an image compression algorithm to rewrite the image file in a way that takes up less storage space.
- postCSS
	- Basically this is a way to help other create plugins for CSS. Like the plugin `Autoprefixer` to automatically adds vendor prefixes to your CSS properties. Or `CSSnano` to focuses on optimizing and minifying your CSS code.
	- PostCSS takes a CSS file and provides an API to analyze and modify its rules (by transforming them into an Abstract Syntax Tree). This API can then be used by plugins to do a lot of useful things, e.g., to find errors automatically, or to insert vendor prefixes.
		- Tailwind uses a mobile-first breakpoint system
- 
## Advanced CSS Layouts
- `calc`
	- scss calc need to have same unit, css does not need
	- css calc can use fallback
		- ![image](Attachments/CleanShot%202023-08-02%20at%2014.22.10%402x.png)
	- make it easier to understand
		- ![image](Attachments/CleanShot%202023-08-02%20at%2014.22.23%402x.png)
	- can use with variables in scss
		- ![image](Attachments/CleanShot%202023-08-02%20at%2014.23.11%402x.png)
- Sass vars vs css custom properties
	- Use Sass for global values that don't typically change: color, font family, etc.
	- Use custom properties for values that will change in the media queries: font size, margin, padding, widths, flex basis, etc.
		- Sass variables are imperative, which means if you use a variable and then change its value, the earlier use will stay the same. CSS variables are declarative, which means if you change the value, it'll affect both earlier uses and later uses.

## A Complete Guide to Flexbox
- Release 2017
- Flexbox layout is most appropriate to the components of an application, and small-scale layouts, while the Grid layout is intended for larger scale layouts.
- align justify content item
	- align-items + justify-items
		- align each item within itself
		- ![image](Attachments/CleanShot%202023-08-02%20at%2016.08.30%402x.png)
	- align-content + justify-content
		- align all the rows and columns on the overall layout
		- ![image](Attachments/CleanShot%202023-08-02%20at%2016.08.38%402x.png)

## CSS Grid & Flexbox for Responsive Layouts, v2
- Before flexbox and grid: Ppl use float or tables
- `<figure>` tag: to mark up a photo in a document, and a `<figcaption>` element to define a caption for the photo:
	```html
	<figure>
	  <img src="pic_trulli.jpg" alt="Trulli" style="width:100%">
	  <figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption>
	</figure>
	```
- Structures like this is more sutiable for flexbox, not possible with grid:
	- ![image](Attachments/CleanShot%202023-08-02%20at%2017.06.18%402x.png)
- When trigger display flex, the element is somewhat a `position: relative` too
- [Types] Flexboxes vs grid
	- [Ref](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Relationship_of_grid_layout_with_other_layout_methods#the_fr_unit_and_flex-basis)
	- Flexbox is starting from max-content and taking space away. Grid starting at min-content and adding space.
	- Do I want to control the item size or the thing there're in?
		- Item: flexbox
		- The cells: grid
	- When you wrap flex items, each new row (or column when working by column) is an independent flex line in the flex container.
		- Space distribution happens across the flex line.
		- A common question then is how to make those items line up. This is where you want a two-dimensional layout method
	- Flexbox works from the content out. An ideal use case for flexbox is when you have a set of items and want to space them out evenly in a container. You let the size of the content decide how much individual space each item takes up.
		- Grid works from the layout in. When you use CSS Grid Layout you create a layout and then you place items into it.
		- If you are using flexbox and find yourself disabling some of the flexibility, you probably need to use CSS Grid Layout.
	- Both use [Box Alignment Module Level 3](https://drafts.csswg.org/css-align/)
	- The fr unit and flex-basis
		- 
	- Grid(when 2 dimentions)
		- CSS Grid is for layout
		- Products grid
		- Cells that not only span horizontal but also vertical
	- Flexboxes(when 1 dimentions, lists)
		- Flexbox is for alignment
		- Any other kinds of lists
			- Nav bars
			- Headers
			- Footers
- Load image variants dynamically:
	- use `<picture>`
		- ![image](Attachments/CleanShot%202023-08-02%20at%2017.49.28%402x.png)
		- ![image](Attachments/CleanShot%202023-08-02%20at%2017.51.28%402x.png)
	- use srcset and sizes: The browser decides which image displays
		- ![image](Attachments/CleanShot%202023-08-03%20at%2009.45.46%402x.png)
		- The browser decides which image to load.
		- The browser may not decide to load the image you expect.
		- Different browsers may make different choices.
		- ![image](Attachments/CleanShot%202023-08-03%20at%2009.46.33%402x.png)
			- ![image](Attachments/CleanShot%202023-08-03%20at%2009.47.00%402x.png)
			- ![image](Attachments/CleanShot%202023-08-03%20at%2009.47.05%402x.png)
			- ![image](Attachments/CleanShot%202023-08-03%20at%2009.47.17%402x.png)
	- ![image](Attachments/CleanShot%202023-08-03%20at%2009.48.14%402x.png)
- Grid rows or columns can oppcupy same space, not like flex

## Learn CSS Grid (Visual Website)
- Ways to define columns/rows
	- Explicit
		- `grid-template-rows: 50px 100px`
	- Minimum and Maximum Grid Track Sizes
		- `grid-template-rows:    minmax(100px, auto);`
	- Repeating Grid Tracks
		- `grid-template-rows:    repeat(4, 100px);`
- Ways to span columns/rows
	- Positioning Items by Grid Lines
		- `grid-column-start: 1;`
		- `grid-column-end:   4;`
	- Positioning Items by Grid Lines Names
		```css
		  grid-template-rows:    [row-1-start] 1fr [row-2-start] 1fr [row-2-end];
		  grid-template-columns: [col-1-start] 1fr [col-2-start] 1fr [col-3-start] 1fr [col-3-end];
		  grid-row-start: row-2-start;
		  grid-row-end: row-end;
		```
	- Naming and Positioning Items by Grid Areas
		```css
		grid-template-areas:   "header header"
		                        "content sidebar"
		                        "footer footer";
		grid-row-start:    header;
		grid-row-end:      header;
		grid-column-start: header;
		grid-column-end:   header;
		```
- Grid lines can generally be named whatever you’d like, but assigning names ending in -start and -end comes with added benefits—they implicitly create named grid areas, which can be referenced for positioning.
	- ![image](Attachments/CleanShot%202023-08-03%20at%2013.10.07%402x.png)
- Implicitly named grid lines work in reverse to implicitly named grid areas—naming grid areas implicitly assigns names to grid lines.
	- ![image](Attachments/CleanShot%202023-08-03%20at%2013.10.21%402x.png)
- Auto-fit Vs Auto-fill
	- ![image](Pasted image 20230803151403.png)
- content sizing
	- normal
		- ![image](Attachments/CleanShot%202023-08-03%20at%2015.29.53%402x.png)
	- `min-content`
		- ![image](Attachments/CleanShot%202023-08-03%20at%2015.29.13%402x.png)
	- `max-content`
		- ![image](Attachments/CleanShot%202023-08-03%20at%2015.29.25%402x.png)
	- `fit-content`
		- without
			- ![image](Attachments/CleanShot%202023-08-03%20at%2014.06.54%402x.png)
		- with
			- ![image](Attachments/CleanShot%202023-08-03%20at%2014.07.08%402x.png)
- Grid is only a replacement for float-based layout, where float-based layout it being used to try and create a two-dimensional grid. If you want to wrap text around an image, I’d suggest floating it.
- Grid is only a replacement for flexbox if you have been trying to make flexbox into a two-dimensional grid. If you want to take a bunch of items and space them out evenly in a single row, use flexbox.

## Other projects
- Font download local, at `app/assets/fonts/MuseoSansRounded-100.otf`
- Have defined media breakpoints , `@include media-breakpoint-up('xl')`
- All use `rem` function
- Good reference, may come back once I do scss