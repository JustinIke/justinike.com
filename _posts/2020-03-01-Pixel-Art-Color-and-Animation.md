---
layout: post
title: "Pixel Art: Color and Graphical Projection"
date: 2020-03-05 10:00:01
tags: Hobby
image: 2020-03-01-Pixel-Art-Color-and-Graphical-Projection/House.gif

---

I was told by a few people that my first pixel art post was their favorite post of mine, which gives me all the more confidence to continue with pixel art! So today I'll be talking about my latest progressions with making a color palette and then using it to make a top down scene. To learn about these topics, I once again referred to the ever-talented [SLYNYRD's](https://raymond-schlitter.squarespace.com/) tutorials.

## Color  Palette

My first few drawings' colors were chosen fairly arbitrarily. This worked for a while, but, being a programmer, I like to make sure my techniques are scalable and future proof. Switching to a color palette speeds up the workflow and makes your scenes look much more harmonious. A palette is essentially a bunch of predetermined colors that you use within your drawing. This way, you just pick colors from the palette instead of finding a color from the whole spectrum.

The technique for creating palettes that reliable [SLYNYRD](https://raymond-schlitter.squarespace.com/) uses is called hue shifting. Here, in each "ramp" of colors the brightness increases, while the saturation peaks in the middle and the hue is shifted by a predetermined amount. This is done through the HSB color system.

{% include image.html url="\assets\images\2020-03-01-Pixel-Art-Color-and-Graphical-Projection\ExampleRamp.png" description="A color ramp" %}

Through a lot of trial and error, I managed to make a ramp that I'm fairly happy with. I tried to not totally copy [SLYNYRD](https://raymond-schlitter.squarespace.com/) as to get a palette that is more my own by shifting different values for the different stages of the ramp. Some of my changes may end up being problematic in the future as my eye isn't that great for this stuff, but for now I think they are okay.

After creating a ramp, you simply hue shift the whole thing to get more. There are 360 hues in HSB, so just divide that number by however many ramps you want and that's the value by which you hue shift. I decided on 10 ramps so I shifted each ramp's hue by 36 from the previous. Then, with all the colors now accounted for, I copied those ramps to the bottom of the palette and desaturated them. [SLYNYRD](https://raymond-schlitter.squarespace.com/) suggests this so that you have more natural colors to work with. I tend to go for darker colors, so I made a my less saturated colors less bright than he does in the tutorial. Finally, I figured I could use a greyscale ramp. With that final change my palette was complete. 

{% include image.html url="\assets\images\2020-03-01-Pixel-Art-Color-and-Graphical-Projection\colorPalette2.png" %}

To actually use it, you just pick the colors you want and go across the ramp to get different shades and complementing colors. I'm still practicing this, but as I continue to work with it, I think it'll be very advantageous. 

## Graphical Projection

Creating believable depth with a few pixels is where things really start to get exciting. A 3/4 top-down view is one you're likely to see in indie games. Here, the perspective is 45 degrees from the top, with sunlight coming from the top right.  Being the most exposed to light, the top right of an object will be the lightest, then each side further from the light gets gradually darker, with shadows for overhangs and highlights for things that jut out. This is where the color ramps come in. It's easy to find the color you want and then pick the proper adjacent color that is lighter or darker.

With these ideas in mind, I got this little farm scene.

{% include image.html url="\assets\images\2020-03-01-Pixel-Art-Color-and-Graphical-Projection\Farm.gif" %}

All of the colors used were from the palette I made. I think they look pretty good together, except the red of the barn pops out a bit much for my liking. This could be a sign that I need some lighter versions of my desaturated colors, as my dark, desaturated reds are essentially browns. I think the power of the palette really shined with my truck in particular. I was able to find a few nice colors super quickly, allowing me to focus on organizing them into the form you see. It's small, but I love the look of it.

You may have also noticed that this image moves! I dipped into animation a bit for this scene, using 4 different frames for the smoke from the house and 20 frames for the curious chicks in the barn. For only having 4 frames, the smoke actually looks quite smooth without trying to be too realistic. Pixel artists are pretty big into minimal animations like this one, and I can see why.

I could've gone into a lot more detail with other structures, trees, or whatever else, but I was decided I was happy with the result and done with the farm theme for now. I plan to continue with these fun [SLYNYRD](https://raymond-schlitter.squarespace.com/) tutorials and make more updates of my progress. Onward and upward!

