NOTES
"Measure First, THEN Optimize"

- added media query to print.css link tag
- rearranged order of javascript link tags to bottom of doc
- moved css link tags above title tag....prolly not necessary
- dropped the webfont link tag below the css link tags
- added async value to custom js link tag
- remove comments in html...minify?
- inline style.css?
- inline scripts always block UNLESS js link is ABOVE CSS...
- inline css font declaration for Open Sans 400,700
- minify?
- add a scroll handler that temporarily disables hover effects while scrolling

- web fonts: EOT is IE8 only...fuckit. Woff is most universal, serve that with a Arial/Verdana fallback?

- scale images and set css size rules ... esp pizzeria img gets a couple smaller sizes..
	- can also work in device width specific img requests

- modify resizePizzas:
	- line 406: cache doc.querySelector result
	- why is ChangeSliderLabel a declared function when it gets called immediately after definition?

	- line 452: cache changePizzaSizes
	- Line 473 ... cache querySelector used in loop
	- Line 507: doc.body.scrollTop needs to be cached?

	- Line 536: cache querySelector

	- Mover elements: too many? Seems I only ever see as many as the viewport is high...how can I control number of movers based on viewport height? See ~line 480
		- For Movers, each has a height of 100px and an offset top of 256px * row they are in...
		- ...each has width 73px and are spread btwn 200-300 px apart...
		- Therefore, with 8 Movers per row, 5 rows would equal height of 1780px (each takes ~356px)
		- Get viewport size...divide height by 356, width by 300...generate Movers accordingly
		- Also what if I applied the Layer hack to the Mover css class?
		- Batch append mover elements using createDocumentFragment
		- Apply left position adjustment one time only on element creation

	- modify updatePositions: precompute phase values, cache DOM query, change to use translateX

	- meta viewport tag inserted to ensure proper device wide display

	Observation: enabling "gpu acceleration" via the layer hack had two interesting results...
		- In Timeline, paints went WAY down but white bar activity (gpu time?) went WAY up
		- According to User Timing API, measuring time to generate last 10 frames, actually INCREASED slightly

## Website Performance Optimization portfolio project

Your challenge, if you wish to accept it (and we sure hope you will), is to optimize this online portfolio for speed! In particular, optimize the critical rendering path and make this page render as quickly as possible by applying the techniques you've picked up in the [Critical Rendering Path course](https://www.udacity.com/course/ud884).

To get started, check out the repository, inspect the code,

### Getting started

Some useful tips to help you get started:

1. Check out the repository
1. To inspect the site on your phone, you can run a local server

	```bash
	$> cd /path/to/your-project-folder
	$> python -m SimpleHTTPServer 8080
	```

1. Open a browser and visit localhost:8080
1. Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

	``` bash
	$> cd /path/to/your-project-folder
	$> ngrok 8080
	```

1. Copy the public URL ngrok gives you and try running it through PageSpeed Insights! [More on integrating ngrok, Grunt and PageSpeed.](http://www.jamescryer.com/2014/06/12/grunt-pagespeed-and-ngrok-locally-testing/)

Profile, optimize, measure... and then lather, rinse, and repeat. Good luck!

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

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
