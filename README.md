## Website Performance Optimization portfolio project
My challenge, that I accepted (and they sure hoped I would), was to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

The project repo is here: https://github.com/uncleoptimus/udacityP4
The project lives at: http://uncleoptimus.github.io/udacityP4/

MY NOTES

Catchphrase: "Measure First, THEN Optimize"

I. PageSpeed of index.html:
- added media query to print.css link tag
- rearranged order of javascript link tags to bottom of doc
- moved css link tags above title tag....prolly not necessary
- dropped the webfont link tag below the css link tags...ultimately inlined in css (see below)
- added async value to custom js link tag
- scale images and set css size rules ... esp pizzeria img gets a couple smaller sizes..
- can also work in device width specific img requests
- inline style.css, eliminate link tag
- note: inline scripts always block UNLESS js link is ABOVE CSS...
- inline css font declaration for Open Sans 400,700, eliminate link tag
	- there is a devtools hack for obtaining desired font format download link from google fonts
- web fonts: EOT is IE8 only...fukit. Woff is most universal, serve that with a Arial/Verdana fallback
- did not bother to minify HTML
- achieved Mobile PageSpeed of over 90

II. Optimize main.js of pizzeria.html:
- modify resizePizzas (line numbers refer to og file):
	- line 406: cache doc.querySelector result
	- why is ChangeSliderLabel a declared function when it gets called immediately after definition?
	- line 452: cache changePizzaSizes
	- Line 473: cache querySelector used in loop
	- Line 507: cache doc.body.scrollTop
	- Line 536: cache querySelector
	- Move recurrent value computation out of loops

- modify updatePositions: precompute phase values, cache DOM query, change to use translateX
	- Mover elements: too many? Seems I only ever see as many as the viewport is high...See ~line 480
	- For Movers, each has a height of 100px and an offset top of 256px * row they are in...
	- ...each has width 73px and are spread btwn 200-300 px apart...
	- Therefore, with 8 Movers per row, 5 rows would equal height of 1780px (each takes ~356px)
	- Get viewport size...divide height by ~256, width by ~256...generate Movers accordingly
	- Limit DOM reflows by taking 'style.left' references out
	- GPU Accel: I applied the Layer hack to the Mover css class by using 3d transforms "translateZ(0)"
	- Batch append mover elements using createDocumentFragment (one time operation)
	- Apply left position adjustment on movers one time only on element creation

- meta viewport tag inserted to ensure proper device wide display

- Observation: enabling "gpu acceleration" via the layer hack had two interesting results...
		- In Timeline, paints went WAY down but white bar activity (gpu time?) went WAY up
		- According to User Timing API, measuring time to generate last 10 frames, actually INCREASED slightly
		- Googling led to http://stackoverflow.com/questions/18257206/extra-render-time-in-chrome-dev-tools-timeline-frames
			which links to a video by Paul Irish explaining white bar 'phenomena' as chrome likely waiting on gpu

III. Build Tools:
	- Process as outlined at http://blog.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/
		and http://substack.net/task_automation_with_npm_run
	- Installed node/npm
	- Installed browserify to concat (and resolve dependencies) js files...result: one js file, one http request
	- OK turns out that is unneeded in this project
	- Installed uglify to aggressively shrink down 'production' js file
	- Installed watchify to auto build using browserify upon file edits...speed up dev time
	- Installed auto-prefixer for css files
	- Installed cleancss for minification
	- Grokked CLI command 'cat' to concat files
	- Added a build script to 'scripts' object in npm package.json file to automate build process
	NOTE: using Brackets editor extension also will auto-minify files
	- Using npm build script I now concat, minify and autoprefix the css for pizza.html; save 1 request
	- Using npm build script I now uglify the main.js file, shaving 10Kb...

REDACTED! Uglifying necessarily mangles function defnition names, thereby breaking any event handling declared in the dom. Switched pizza.html to use main.min.js instead of the uglified build.js 


### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>
