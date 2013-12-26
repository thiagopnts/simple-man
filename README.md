#Simple Man

Jekyll is pretty rad and figured releasing a cleaned up version of [Balzac](http://jekyll.gtat.me/about/) and [Minimal Mistakes](https://twitter.com/mmistakes) as a theme to hack up and use would be cool.

## Simple Man features:

* Responsive templates. Looking good on mobile, tablet, and desktop.
* Gracefully degrading in older browsers. Compatible with Internet Explorer 8+ and all modern browsers. 
* Content first.
* Large feature images for posts and pages.
* Simple and clear permalink structure *(ie: domain.com/category/post-title)*

![screenshot of Simple Man theme]()

General notes and suggestions for customizing Simple Man.

## Basic Setup

1. [Install Jekyll](http://jekyllrb.com) if you haven't already.
2. Fork the [Simple man repo](http://github.com/thiagopnts/simple-man/)
3. Make it your own and customize, customize, customize.

## [Preview the Theme](http://mmistakes.github.io/minimal-mistakes)

``` bash
simple-man/
├── _includes
|    ├── author-bio.html  //bio stuff goes here
|    ├── chrome-frame.html  //displays on IE8 and less
|    ├── footer.html  //site footer
|    ├── head.html  //site head
|    ├── navigation.html //site top nav
|    └── scripts.html  //jQuery, plugins, GA, etc.
├── _layouts
|    ├── home.html  //homepage layout
|    ├── page.html  //page layout
|    ├── post-index.html  //post listing layout
|    └── post.html  //post layout
├── _posts
├── assets
|    ├── css  //preprocessed less styles. good idea to minify
|    ├── img  //images and graphics used in css and js
|    ├── js
|    |   ├── main.js  //jQuery plugins and settings
|    |   └── vendor  //all 3rd party scripts
|    └── less 
├── images  //images for posts and pages
├── about.md  //about page
├── articles.md  //lists all posts from latest to oldest
└── index.md  //homepage. lists 5 most recent posts
```

## Customization

### _config.yml

Most of the variables found here are used in the .html files found in `_includes` if you need to add or remove anything. A good place to start would be to change the title, tagline, description, and url of your site. When working locally comment out `url` or else you will get a bunch of broken links because they are absolute and prefixed with `{{ site.url }}` in the various `_includes` and `_layouts`. Just remember to uncomment `url` when building for deployment or pushing to **gh-pages**...

#### Owner/Author Information

Change your name, bio, and avatar photo (100x100 pixels or larger), Twitter url, email, and Google+ url. If you want to link to an external image on Gravatar or something similiar you'll need to edit the path in `author-bio.html` since it assumes it is located in `\images`.

Including a link to your Google+ profile has the added benefit of displaying [Google Authorship](https://plus.google.com/authorship) in Google search results if you've went ahead and applied for it. Don't have a Google+ account? Just leave it blank and/or remove `<link rel="author" href="{{ site.owner.google_plus }}">` from `head.html`.

#### Google Analytics and Webmaster Tools

Your Google Analytics ID goes here along with meta tags for [Google Webmaster Tools](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=35179) and [Bing Webmaster Tools](https://ssl.bing.com/webmaster/configure/verify/ownershi) site verification.

#### Top Navigation Links

Edit page/post titles and URLs to include in the site's navigation. For external links add `external: true`.

``` yaml
# sample top navigation links
links:
  - title: About Page
    url: /about
  - title: Articles
    url: /articles
  - title: Other Page
    url: /other-page
  - title: External Page
    url: http://mademistakes.com
    external: true
```

#### Other Stuff

The rest is just your average Jekyll config settings. Nothing too crazy here...

### _includes

For the most part you can leave these as is since the author/owner details are pulled from `_config.yml`. That said you'll probably want to customize the copyright stuff in `footer.html` to your liking.

### Adding Posts and Pages

There are two main content layouts: `post.html` (for posts) and `page.html` (for pages). Both have large **feature images** that span the full-width of the screen, and both are meant for text heavy blog posts (or articles). 

#### Feature Images

A good rule of thumb is to keep feature images nice and wide so you don't push the body text too far down. An image cropped around around 1024 x 256 pixels will keep file size down with an acceptable resolution for most devices. If you want to serve these images responsively I'd suggest looking at [Picturefill](https://github.com/scottjehl/picturefill) or [Adaptive Images](http://adaptive-images.com/).

The two layouts make the assumption that the feature images live in the *images* folder. To add a feature image to a post or page just include the filename in the front matter like so. 

``` yaml
image:
  feature: feature-image-filename.jpg
  thumb: thumbnail-image.jpg #keep it square 200x200 px is good
```

The large texture images used in *Minimal Mistakes* are from [Love Textures](http://lovetextures.com), probably a good idea to swap these out with your own photos...

#### Categories

In the sample `_posts` folder you may have noticed `category: articles` in the front matter. I like keeping all posts grouped in the same folder. If you decide to rename or add categories you will need to modify the permalink in `articles.md` along with the filename (if renaming).

For example. Say you want to group all your posts under `blog/` instead of `articles/`. In your post add `category: blog` to the front matter, rename or duplicate `articles.md` to `blog.md` and change the permalink in that file to `permalink: /blog/index.html`.

If done correctly `/blog` should be a page listing all the site's posts.

#### Thumbnails for OG and Twitter Cards

Post and page thumbnails work the same way. These are used by [Open Graph](https://developers.facebook.com/docs/opengraph/) and [Twitter Cards](https://dev.twitter.com/docs/cards) meta tags found in `head.html`. If you don't assign a thumbnail the default graphic *(default-thumb.png)* is used. I'd suggest changing this to something more meaningful -- your logo or avatar are good options.

#### Table of Contents

Insert the following HTML in post or page content that you want a *table of contents* to render. [Kramdown will take care of the rest](http://kramdown.rubyforge.org/converter/html.html#toc) and convert all headlines into a contents list.

**PS:** The TOC is hidden on small devices because I haven't gotten around to optimizing it. For now it only shows on tablet and desktop breakpoints...

``` html
<section id="table-of-contents" class="toc">
  <header>
    <h3 class="delta">Contents</h3>
  </header>
<div id="drawer" markdown="1">
*  Auto generated table of contents
{:toc}
</div>
</section><!-- /#table-of-contents -->
```

#### Videos

Video embeds are responsive and scale with the width of the main content block with the help of [FitVids](http://fitvidsjs.com/).

Not sure if this only effects Kramdown or if it's an issue with Markdown in general. But adding YouTube video embeds causes errors when building your Jekyll site. To fix add a space between the `<iframe>` tags and remove `allowfullscreen`. Example below:

``` html
<iframe width="560" height="315" src="http://www.youtube.com/embed/PWf4WUoMXwg" frameborder="0"> </iframe>
```

#### Twitter Cards

Twitter cards make it possible to attach images and post summaries to Tweets that link to your content. Summary Card meta tags have been added to `head.html` to support this, you just need to [validate and apply your domain](https://dev.twitter.com/docs/cards) to turn it on.

## Further Customization

To make things easier I use SASS to build Simple Man's stylesheets. If you want to make some minor cosmetic alterations, take a look at `variables.scss` in `assets/sass/`. Changing some of the following variables can help make the theme your own.

``` css
// TYPOGRAPHY ================================================
@basefont: 'Open Sans', serif;
@baseheadingfont: 'Droid Sans', sans-serif;
@codefont: Monaco, Courier New, monospace;
```

## License

This is [MIT](LICENSE) with no added caveats, so feel free to use this Jekyll theme on your site without linking back to me or using a disclaimer.

