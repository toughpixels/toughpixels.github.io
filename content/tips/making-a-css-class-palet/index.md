---
title: "Making a Css Class Palet"
date: 2021-03-02T21:15:55-06:00
tags: 
description: "Simplify your life with a CSS Class palat!  Save money by saving in Netlify's 300 minite cap for free build minutes!"
draft: true
---

## The Problem
Tailwinds is awesome, but for some reason (perhaps my error) it's adding tons of build time.  This uses up free processing minutes offered by Netlify and we don't need to constantly be compiling CSS if we get organized and make a plan.

## The Plan
Instead of always compiling tailwinds, I propose being thoughtful in advance about what a site calls for in utility classes and only load those. 

## Getting Started
1. Create a Hugo site
2. Inside your Hugo directory, run `npm install -D tailwindcss@latest postcss@latest autoprefixer@latest` to install Tailwinds and it's dependency "postcss" and "autoprefixer" which repeates some generic styles with their browser-specific equivalent to support those browsers. (source docs: https://tailwindcss.com/docs/installation)
3. run `touch postcss.config.js` to make that file.
4. Inside `postcss.config.js` add the text: 

         module.exports = {
                 plugins: {
                 tailwindcss: {},
                 autoprefixer: {},
           }
         }

5. Run `npx tailwindcss init` to make the tailwinds config file.
6. Open your main *.css file and add this: 

         @import "tailwindcss/base";
         @import "tailwindcss/components";
         @import "tailwindcss/utilities";

7. Open `tailwind.config.js` in your editor.
8. Once you're done editing the `tailwind.config.js` file, you'll run the command `postcss styles.css -o compiled.css` where `styles.css` is the directory/filename of your main *.css file and `compiled.css` is the directory/filename of the css file that you want to load on your site.  For me, this line is `postcss ./assets/css/pre.css -o ./assets/css/compiled.css`
9. A pretty awesome tool called [Windsock](https://github.com/Windsock-Styleguide/tailwind-styleguide) will take a `tailwinds.config.js` file as an imput and output stylguide html, which you can then reference while building your site!  It's also useful as a guide to empower the owner of the site to make their own code tweaks down the road.
10.  Add purge lines to `tailwind.config.js`:

 module.exports = {
   purge: [
     './layouts/**/*.html',
     './assets/**/*.js',
   ],
    darkMode: false, // or 'media' or 'class'
    theme: {
      extend: {},
    },
    variants: {},
    plugins: [],
  }

  This assumes urls you would likely want when creating a Hugo site

11. 

## Some things I change

### screens
Most sites don't need a lot of breakpoints so I broke this up into 'md' and 'lg' options only.  This should also help cut back on the number of generated classes.

### colors
If you want to advertise different theme options to the client, it may be valuable to write these in abstract words like "primary" (versus the color name like "pink").

### spacing
Tailwinds gives a bunch of options out the gate but I feel like pretty much anything I want to do regarding spacing can be done in the 0 - 12 range so I removed options above 12.  Sometimes it's nice to have a big space between two sections, so I also included a 'lg' option so large sections can be spaced apart with a class like `space-y-lg`

### container
If this is not a blank array, Tailwinds will create a container that's max-width at every point is the min-width of that breakpoint, which makes it great for developing because you can more quickly see if anything breaks at 768px screens, etc.  Once you're done with development, you can make your own .container class that only has something like `@apply mx-auto px-4;` applied to it.

### fontFamily
I just make this "body" and "header" because for the most part, that's all you need

### fontSize
Leave as they are but come back to these once you've defined all your type styles so that you can prune them down.

### fontWeight
Prune later


### false stuff
#### Many projects don't involve these at all so I'm making them false by default
* animation
* appearance
* backgroundImage
* backgroundOpacity
* backgroundPosition
* borderOpacity
* gradientColorStops


## Single Default option
#### Generally one option is enough
* backgroundSize
* borderRadius
* borderWidth
* boxShadow

### gridAutoColumns
I'm still learning what kind of grid options there are so I'm leaving all grid-related stuff as it is for now.

