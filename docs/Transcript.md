https://www.youtube.com/watch?v=ldxFjLJ3rVY

# How (and why) to take the logarithm of a picture

Chapter 1: The print gallery
0:00Whenever I'm making one of these videos, there's sometimes a special moment where the act of animating involves solving a whole bunch of little technical puzzlers,
0:077 secondsand then the underlying math I'm trying to explain clicks for me in a way that it hadn't before once I see it alive on screen.
0:1414 secondsThe best versions of those moments often tell me when a video is going to be one of my favorites, and putting together the end of this piece right here was one such time when I got that feeling.
0:2727 secondsOur story doesn't actually start in the math classroom today. We begin in the art room. Imagine standing in a gallery, looking at a picture of a boat in a harbour,
0:3636 secondsand the whole world warps as your gaze shifts upwards and to the right, where you see a village on this waterfront.
0:4343 secondsAmong the tightly clustered buildings, the world warps even more as your gaze shifts downwards to the entrance of one building, leading to a hallway full of artwork.
0:5353 secondsAnd at the end of this hall, here you are again, staring at a picture of a boat. This is M.C.
0:5959 secondsEscher's 1956 lithograph, the Print Gallery, or in Dutch, Prentendentunstelling.
1:051 minute, 5 secondsIn a letter that he wrote to his son, describing his creation of a young man looking with interest at a print that features himself,
1:131 minute, 13 secondsEscher called this the most peculiar thing I have ever done, which for him is saying a lot. Escher's art is widely loved around the world,
1:211 minute, 21 secondsfrequently featuring paradoxical themes or uniquely satisfying geometric patterns with some kind of character. This love is especially pronounced among mathematicians,
1:301 minute, 30 secondssince his art often touches on surprisingly deep concepts within math, despite the fact that Escher himself had no formal training in the field.
1:391 minute, 39 secondsThe Print Gallery offers a perfect example of this unexpected depth.
1:431 minute, 43 secondsIn 2003, the mathematicians De Smit and Lenstra offered a delightful analysis of what's really going on in this piece and the mind-bending self-contained loop that Escher managed to achieve.
1:541 minute, 54 secondsOne of my main goals with this video is to offer a visual unpacking of their analysis, aiming as always to give you a feeling that you could have rediscovered this yourself.
2:052 minutes, 5 secondsSomething that unexpectedly pops out of this analysis is an answer to the question of what exactly should go in the middle of this picture.
2:122 minutes, 12 secondsAt first, that might sound like an incoherent question.
2:152 minutes, 15 secondsIf you come at it from the upper right, it feels like it should be featuring buildings in the village, but coming at it from the left, it looks more like part of the picture frame.
2:232 minutes, 23 secondsCome at it from below, though, and it feels more fitting to be part of the gallery itself.
2:282 minutes, 28 secondsSomehow all of the ambiguity about where exactly you are in this whole scene is compressed into that blank circle in the middle.
2:362 minutes, 36 secondsAnd just for fun, since we're in the 2020s, I let a diffusion model take a stab at filling this in. Unsurprisingly, it struggles immensely.
2:432 minutes, 43 secondsIt just doesn't get it at all. And giving the poor machine some credit, of course it struggles. This feels like an intrinsically ambiguous and ill-defined part of the scene.
2:522 minutes, 52 secondsBut nevertheless, by the end, I hope you'll agree there is one, and really only one, completion that feels like the right puzzle piece you can slot in.
3:023 minutes, 2 secondsBefore diving into the math, I want to give you a purely intuitive description for how Escher actually made this piece, which breaks up into three different steps.
3:103 minutes, 10 secondsStep one is to start out with a straightened out version of the same general concept, where a man is looking at a picture.
3:173 minutes, 17 secondsThat picture contains a harbor, which contains a town, that contains a print gallery, that contains that same man, and so on and so forth.
3:263 minutes, 26 secondsYou could zoom in forever to your heart's content. This idea of a self-similar image, where the picture is contained inside itself,
3:343 minutes, 34 secondshas a special name to graphic designers.
3:373 minutes, 37 secondsIt's known as the Drosta effect, named after a cocoa company that featured it in its branding.
3:423 minutes, 42 secondsIn fact, this seems to have been a somewhat common marketing gimmick for all kinds of early 20th century products. The self-similar Drosta image that Escher was using, though,
3:523 minutes, 52 secondsinvolves a much, much deeper zoom than any of these, where the self-similar copy is 256 times smaller than the original.
4:004 minutesYou'll see where that number comes from in just a minute. The genius of Escher is that he somehow intuitively realized there must be a way to
4:084 minutes, 8 secondstake this concept of a picture nested inside itself and turn it into this warped loop where the zooming in happens implicitly as a viewer's gaze wanders around the circle.
4:214 minutes, 21 secondsBy the way, you might be wondering where I got this straightened out version, and the answer is that those two mathematicians I referenced generously let us use it.
4:284 minutes, 28 secondsThis is something they actually reverse engineered from the original Escher piece using the help of two Dutch artists, Hans Richter and Jacqueline Hofstra.
4:374 minutes, 37 secondsThe way they reverse engineered it is actually super interesting. In a certain manner of speaking, it involves taking the logarithm of the original piece.
4:444 minutes, 44 secondsI recognize that sentence probably sounds like nonsense right now, but later on in this video, I promise that will make abundant sense.
4:524 minutes, 52 secondsTo outline the basic idea for how Escher made this loop, I want to use an example that's simpler than the one he was working with,
4:594 minutes, 59 secondsso we'll pull up this custom self-similar Drasta image which has a pie creature looking at a framed picture of a house where that same pie creature lives.
5:085 minutes, 8 secondsIn this example, the self-similar copy is only 16 times smaller than the original, and this just makes everything much easier to see all at once.
5:155 minutes, 15 secondsWhat I'll do is keep a separate workspace on the right here to sketch out the general goal we have in mind, where the way you might think about it is that you want to distribute that 16-fold zoom-in factor across the four corners of the square.
5:305 minutes, 30 secondsFor example, let's say you want the pie creature itself to appear about at the same size in the lower left corner. Then if you zoom in by a factor of 2 in the original,
5:395 minutes, 39 secondswe'll take what would be in the upper left of that zoomed version and then place it in the upper left of our workspace.
5:475 minutes, 47 secondsSimilarly, zoom in by another factor of 2 and then take the upper right of that zoomed-in version and now place an expanded version of that in the upper right of our workspace.
5:585 minutes, 58 secondsFinally, one more step, zoom in by another factor of 2, take what's in the lower right of that zoomed-in version, blow it up, and place it in the lower right of our workspace.
6:086 minutes, 8 secondsThese four cut-out corners give a rough idea of what we want to create here. As long as you can find a smooth way to fill in the gaps between them,
6:176 minutes, 17 secondsthen as the onlooker's gaze wanders around a circle on this image,
6:216 minutes, 21 secondswhat they're seeing will zoom in and in and in until it elegantly joins up with the self-similar part of the image 16 times smaller.
6:296 minutes, 29 secondsWe could just try joining it all up naively, something like this, but frankly that doesn't really look very good,
6:356 minutes, 35 secondsand it's certainly not as smooth and as elegant as what Escher managed to achieve, so we still have some work ahead of us.
6:426 minutes, 42 secondsThis book that I've been pawing through by the way, The Magic of M.C. Escher, is something that I got on a delightful visit to the Escher Museum in The Hague,
6:506 minutes, 50 secondswhich, if you're ever in the Netherlands, I would highly recommend, and when we turn to the section about the print gallery, it offers us a little peek into what Escher's process actually was.
6:596 minutes, 59 secondsFor him, step two was to create this warped grid.
7:037 minutes, 3 secondsFor the animations here, I'm going to pull up a slight modification of that grid that is basically just a little nicer mathematically to generate, but it illustrates the same key point.
7:117 minutes, 11 secondsIn his case, the self-similar Drosta image he was working with has a scaling factor of 256, so to distribute that across the four corners,
7:207 minutes, 20 secondsfor him it would involve scaling by a factor of four as you walk from one corner to the next.
7:267 minutes, 26 secondsAnd if you look closely at his grid, say at one of the squares on the lower right,
7:307 minutes, 30 secondsnotice how if you follow the top and bottom lines bounding that square over to the lower left of the image, those same lines end up enclosing a square that is now four times as big.
7:407 minutes, 40 secondsAnd then similarly, if you look at the lines bounding the left and right of a small square from that region, and you follow them upward,
7:477 minutes, 47 secondsthey end up nestled around a square that's nicely four times as big. So the grid kind of encodes the scaling from one corner to the next that we want.
7:557 minutes, 55 secondsNow for our pet project, where we only need to scale up by a factor of two from each corner to the next, we're going to use a modified version of this, but it'll be the same general idea.
8:058 minutes, 5 secondsYou might naturally wonder where on earth does this grid come from, but I actually want to postpone that question and skip ahead to step three,
8:128 minutes, 12 secondswhich is how you can actually use this grid together with the self- similar Drosse image to create Escher's final effect.
8:198 minutes, 19 secondsThe way this works is to first lay down an ordinary square grid on the original image,
8:238 minutes, 23 secondsand then let's say you want this portion here to end up in this corner of our final version.
8:298 minutes, 29 secondsWhat you would do is take each tiny square inside it and then copy over its contents to the corresponding tiny square in the warped version of the grid.
8:388 minutes, 38 secondsFrom there, each neighboring square in our original grid is forced to go to the corresponding neighboring square in the warped version,
8:468 minutes, 46 secondsso you can kind of just keep following where the image must go by following the grid.
8:528 minutes, 52 secondsAnd the fact that the grid lines on the warped version space out by a factor of two as you go from the lower left to the upper left means that the scale of our scene automatically gets scaled up by that factor of two as you walk up that line.
9:069 minutes, 6 secondsThe idea of this process is that as an artist, it's relatively straightforward to go piece by piece, copying over what's inside one tiny square to another tiny square,
9:159 minutes, 15 secondsbecause at this small scale things are undistorted.
9:199 minutes, 19 secondsIt's certainly way, way easier than trying to dream up and draw the appropriate warped final image starting with nothing but a blank page in front of you.
9:289 minutes, 28 secondsSo basically with this warped grid in hand, the process of copying over each little square is pleasantly automatic, and if we let this automatic process run all the way around, it nicely closes up with the initial position, and for that to happen,
9:439 minutes, 43 secondsit requires that our original image had this self-similarity when you zoom in by a factor of 16. I hope you'll agree the final result we have is pretty nice,
9:529 minutes, 52 secondsit recreates the same general effect, but more than anything I think it gives Kaz to more deeply appreciate Escher's own composition.
9:599 minutes, 59 secondsHe was actually very deliberate about the choice of imagery at all of the distinct scales. To quote, I quite intentionally chose serial types of objects,
10:0710 minutes, 7 secondssuch for instance as a row of prints along the wall, or blocks of houses in a town.
10:1310 minutes, 13 secondsWithout the cyclic elements, it would be all the more difficult to get my meaning over to the random viewer. This idea where you have a straight reference image and then a warped grid,
10:2310 minutes, 23 secondsand you use the two together to create a warped scene, is a common process in graphic design. It's known as a mesh warp, and Escher didn't invent it for this case,
10:3210 minutes, 32 secondsit's something that he had used multiple times before for other pieces.
10:3610 minutes, 36 secondsFor our story, the point is that all of the logic for turning a Drasta zoom into a loop is abstracted and purified into this grid,
10:4410 minutes, 44 secondsraising the natural question, where does it come from? How do you make this?
10:4910 minutes, 49 secondsYou can kind of imagine as an initial naive approach you might try linearly scaling everything from one corner to the next, but if you did that right away you would see a conflict.
11:0111 minutes, 1 secondThese two scaling processes are placing distinct pressures on the individual squares,
11:0511 minutes, 5 secondswhere for example this square wants to get flared out in this direction based on the zooming in from the right, but it also wants to get flared in this direction based on the zooming out as you go up.
11:1611 minutes, 16 secondsEscher was evidently pulled to resolve this by curving all of the lines to relieve this tension. But there's one other crucial constraint that it seems he was guided by,
11:2611 minutes, 26 secondsone that presumably made the image transfer process easier, which made the final result look more natural,
11:3211 minutes, 32 secondsand which will make the ears of any mathematician immersed in complex analysis immediately perk up. In his final warped grid, the tiny squares are, well, squares.
11:4311 minutes, 43 secondsTo be clear, this is not at all true for most mesh warps.
11:4611 minutes, 46 secondsIn most cases, the warped grid lines that you draw don't necessarily intersect at right angles, and the little regions that they bound will in general be little parallelograms.
11:5611 minutes, 56 secondsThis can still be workable for an artist, you can still kind of do the transfer,
12:0012 minutesbut presumably the act of copying over from the original to the warped version is more awkward when you have that distortion,
12:0712 minutes, 7 secondsso it would be much nicer if in the warped grid, little squares remained at least approximately square. And when you look closely at the grid that Escher used for his print gallery,
12:1712 minutes, 17 secondsit has this property. All the lines are intersecting at right angles, and at a small enough scale, the regions they bound really are approximately squares.
12:2512 minutes, 25 secondsArtistically, this has the nice effect that even though the whole scene is dramatically warped and distorted at a global scale,
12:3212 minutes, 32 secondszoomed in at a local scale, everything is relatively undistorted. This is what makes each local part of Escher's image easily recognizable.
12:4112 minutes, 41 secondsAnd mathematically, this is where the story really gets interesting. You see, this idea of a function from two dimensional space to two dimensional space,
12:4912 minutes, 49 secondswhere tiny squares remain approximately square, plays a special role and has a special name in math.
12:5512 minutes, 55 secondsIt's called a conformal map, and one area where it comes up all the time is in the study of functions with complex number inputs and complex number outputs.
Chapter 2: Conformal maps from complex analysis
13:0413 minutes, 4 secondsAt this point, we're going to step back and walk out of the art classroom and wander over into the math department, where I want to offer you a mini lesson on some of the core ideas from this field.
13:1613 minutes, 16 secondsThe basic game plan from here is that I want to first do a little refresher, go over some of the basics of complex numbers and complex functions,
13:2313 minutes, 23 secondsand then I want to spend some meaningful time building up an intuition for what logarithms look like in this context of complex numbers.
13:3013 minutes, 30 secondsAnd then once you have that in hand, we're going to step through a completely different way that you can think about recreating this effect that Escher had in his print gallery.
13:3813 minutes, 38 secondsLet's warm up with a review of the basics. We typically think about real numbers as living on a one dimensional line, the real number line, and complex numbers are two dimensional.
13:4813 minutes, 48 secondsSpecifically, we think of the imaginary constant i,
13:5213 minutes, 52 secondsdefined to be the square root of And every other point on this plane represents some combination of a real number with some real multiple of i.
14:0314 minutes, 3 secondsIt's typical to use the variable z in referring to a general complex number, and the game we want to play is to understand various functions of z.
14:1114 minutes, 11 secondsA very simple but important example is to multiply z by some constant.
14:1614 minutes, 16 secondsThe function f of z equals two times z has the effect of scaling everything up by a factor of two. But what about multiplying by something imaginary,
14:2514 minutes, 25 secondslike i, the square root of negative one? Well you know that multiplying one by i gives you i, and by definition, i times i is negative one.
14:3414 minutes, 34 secondsBoth of these you'll notice are in 90 degree rotation, and more generally, multiplying any value z by i has the effect of a 90 degree rotation.
14:4214 minutes, 42 secondsAnd more general than that, when you multiply by any complex constant, the effect is some combination of scaling and rotating.
14:5014 minutes, 50 secondsAnd there's a nice way to think about exactly how much it should scale and rotate. Zero times anything is zero, so the origin has to stay fixed in place,
14:5814 minutes, 58 secondsand then one times any constant c is that same constant c.
15:0215 minutes, 2 secondsSo that means this point at one has to be dragged over to land on whatever that constant c is that we're talking about, and that fully determines the amount of scaling and rotating.
15:1215 minutes, 12 secondsFrom there, the rest of the grid stays as rigid as it can.
15:1515 minutes, 15 secondsA key point to emphasize for our story is that if all you're doing is multiplying by some constant, shapes are always preserved.
15:2215 minutes, 22 secondsAnything you might want to draw, like a square, can get scaled or rotated, but beyond that, there are no distortions. Now things get more interesting for more complicated functions.
15:3215 minutes, 32 secondsA simple but non-trivial example would be mapping each number z to z squared. So the input two is going to have to move to two squared, which is four.
15:4115 minutes, 41 secondsThe input i is going to have to move to i squared, which is negative one. Negative one itself would have to get mapped to positive one.
15:4815 minutes, 48 secondsAnd in its fullness, here's what it looks like if I let every point among the grid lines of this input space move over to their corresponding outputs.
15:5715 minutes, 57 secondsIt's a pretty nice effect, and unlike multiplying by a constant, shape is absolutely no longer preserved. The grid lines get curved and warped.
16:0516 minutes, 5 secondsHowever, and this is a key point, pay attention to what happens at a small scale. For example, just focusing on this little square from the input space.
16:1216 minutes, 12 secondsAs you watch the transformation happen again, you can see that shape is approximately preserved, at least at a small enough scale.
16:2016 minutes, 20 secondsLittle squares from our original grid remain approximately square even after getting processed by the function. To use the lingo, the function z squared gives a conformal math.
16:3016 minutes, 30 secondsAnd the choice of z squared is really not special here. Here's what it looks like if you transform each point z over to z cubed. Squares remain approximately square.
16:4016 minutes, 40 secondsOkay, maybe this example square that I'm highlighting doesn't exactly look square in the output, but really it's just because it started off too big.
16:4616 minutes, 46 secondsTo be clear, this conformal property that I'm talking about is a limiting one. A particular square might not exactly become square, but the idea is that as you zoom in more and more,
16:5516 minutes, 55 secondschoosing square regions from the input space that are smaller and smaller, the resulting output will indeed be better and better approximated by a square.
17:0417 minutes, 4 secondsAnd there's also nothing all that special about the choice of polynomials like z squared or z cubed. For just about any function of complex numbers you could think to write down,
17:1217 minutes, 12 secondsthis property holds. Shape is preserved at a small enough scale. It's almost like magic. The use of complex numbers is very relevant here.
17:2017 minutes, 20 secondsIf instead you were thinking of points in 2D space simply as a pair of real numbers with some xy coordinates, and you write down some arbitrary function of x and y to get a
17:2917 minutes, 29 secondsnew pair of numbers, what is way, way more typical as you let points in that input space get transformed is that the outputs of those tiny squares get squished and distorted.
17:3917 minutes, 39 secondsEven as you zoom in more and more, the resulting limiting shape typically looks like a parallelogram, not necessarily a square.
17:4617 minutes, 46 secondsSo, complex functions really are special in this way. And the basic reason that tiny squares remain square comes down to calculus.
17:5417 minutes, 54 secondsWhat you're looking at is what it means for these functions to have derivatives.
17:5917 minutes, 59 secondsThat might sound a little strange, but the analogy you can think of is that for most functions of real numbers, if you visualize them the ordinary way,
18:0718 minutes, 7 secondsjust with a graph of inputs on the x-axis, outputs on the y-axis, as you zoom in more and more to any particular point on that graph,
18:1418 minutes, 14 secondsit looks more and more like a straight line. That is, the rate of change, how much delta f you get for a given delta x,
18:2118 minutes, 21 secondsapproaches a constant. This is literally what it means for a function to have a derivative, but it's not the only way to visualize it.
18:2918 minutes, 29 secondsHere's a different way to see the same concept. Instead of looking at the graph of a function, let's think of the same function but as a transformation.
18:3718 minutes, 37 secondsThat is, you're going to let each of these points on the real number line move over to their corresponding outputs on this other number line.
18:4518 minutes, 45 secondsWhat you'll notice is that evenly spaced dots from the input space can get warped in the output space, meaning the rate of change of the function in general is not constant.
18:5518 minutes, 55 secondsThis spacing between our dots can change from one part of the image to the next. But we know that as you zoom in more and more to a particular output,
19:0319 minutes, 3 secondsthe rate of change approaches a constant. The dots look more and more evenly spaced.
19:0919 minutes, 9 secondsSpecifically, if you take a tiny patch of dots around a particular input and you copy them over to the output space around the corresponding output,
19:1719 minutes, 17 secondsyou can approximately line up all the dots just by scaling everything by a certain constant factor.
19:2319 minutes, 23 secondsThis is the same analytical fact as what the slope of a graph is telling you, it's just in a different visual context.
19:3019 minutes, 30 secondsBut this context carries over much more easily to thinking about complex valued functions as transformations in the complex plane.
19:3819 minutes, 38 secondsThere we're going to think of the neighborhood around a given input as a tiny little grid of points, like we were before,
19:4419 minutes, 44 secondsand we let each point on that grid move over to its corresponding output.
19:4919 minutes, 49 secondsIn this case, what it means for the rate of change to approach a constant is basically the exact same equation.
19:5619 minutes, 56 secondsThe visual to have in your head is that if you take that tiny patch of squares around the input and copy it over to the corresponding output,
20:0420 minutes, 4 secondsyou can approximately match this up with the output grid lines by multiplying by a certain constant, which remember, in the setting of complex numbers,
20:1220 minutes, 12 secondsmeans rotating and scaling it in some way, depending on the value of that complex constant.
20:1720 minutes, 17 secondsSince rotation and scaling preserve shape, it means that all the tiny squares from the input space remain at least approximately square under this transformation.
20:2720 minutes, 27 secondsSo, stepping back, here's the key point, the reason for talking about any of this at all.
20:3120 minutes, 31 secondsEven though conformal maps like the one that Escher was using for his print gallery are incredibly constrained and highly unusual among the general ways that you could continuously squish about two-dimensional space, nevertheless,
20:4320 minutes, 43 secondsas if by magic, simply by speaking a language of complex numbers,
20:4720 minutes, 47 secondsyou can somehow create entire families of these conformal maps without even really trying. All you do is mix and match standard functions of complex numbers.
20:5620 minutes, 56 secondsThe one constraint is that these functions have to have derivatives, but this will be true for most of the functions you think to write down.
21:0321 minutes, 3 secondsFor our story, decoding what's happening with the print gallery, this means that we have an entirely new way to reframe the key question.
21:1021 minutes, 10 secondsCan you construct some deliberately tailored complex function so that the act of zooming in around the inputs looks like walking around a loop among the outputs?
21:2121 minutes, 21 secondsNow, at this point, with only the bare minimum crash course of complex analysis under our belts, it's hard to know where to start without
21:2821 minutes, 28 secondsfirst building up a larger palette of functions to work with and gaining some familiarity with how they actually behave for complex numbers.
21:3521 minutes, 35 secondsIn this case, there are really only two functions that you need to understand, e to the z and the natural log.
Chapter 3: The complex exponential
21:4221 minutes, 42 secondsI want to settle in and spend some meaningful time understanding both of these, and I think you'll agree that it's time well spent.
21:4821 minutes, 48 secondsEverybody deserves, in my opinion, at least one time in their life to experience the joy of understanding a complex logarithm.
21:5521 minutes, 55 secondsFirst though, a necessary prerequisite is to understand the complex exponential.
22:0022 minutesRegular viewers will be familiar with what it looks like to raise e to the power of a complex number, but a review just never hurts.
22:0722 minutes, 7 secondsWe can start scaffolding the transformation just by focusing on the more familiar examples of real number inputs and the real number outputs they correspond to.
22:1622 minutes, 16 secondsFor example, e to the 0 is 1, so this point at 0 maps over to this point at 1. And then every time you let that input increase by 1,
22:2522 minutes, 25 secondsthe output grows by a factor of e, meaning it runs away from us actually quite quickly. And then on the flip side, as you decrease that input,
22:3422 minutes, 34 secondsletting it get into the negative numbers, every step to the left corresponds to shrinking the output, again by a factor of e.
22:4022 minutes, 40 secondsIn particular, you'll notice in this case that output is always a positive number.
22:4422 minutes, 44 secondsThis of course gets much more interesting when we let the inputs and the outputs both be complex numbers.
22:5022 minutes, 50 secondsAnd here, everything you need to know comes down to what happens as you let the imaginary part of that input increase.
22:5622 minutes, 56 secondsAnd what happens there is that the corresponding output walks around a circle.
23:0223 minutes, 2 secondsIf you're wondering why imaginary inputs to an exponential walk you around a circle like this, we have discussed it many, many other times on this channel.
23:1023 minutes, 10 secondsSee some of the links on screen and in the description.
23:1323 minutes, 13 secondsA key point that I'll reiterate here is that what makes the function e to the z very nice, as opposed to exponentials with other bases,
23:2123 minutes, 21 secondsis that as your input walks up at a rate of 1 unit per second, the output walks around its circle at a rate of exactly 1 radian per second.
23:3023 minutes, 30 secondsSo in particular, increasing the imaginary part by exactly 2 pi causes one full rotation in the output.
23:3723 minutes, 37 secondsPhrased another way, these vertical line segments that I've been drawing with heights of exactly 2 pi each get mapped neatly onto one complete circle when you apply the function.
23:4823 minutes, 48 secondsYou'll notice how I've drawn these particular vertical line segments to be spaced out evenly in the real direction, where the real part from 1 to the next increases by 1.
23:5723 minutes, 57 secondsThe corresponding circles on the right each differ by a constant scaling factor, specifically the scaling factor e.
24:0424 minutes, 4 secondsEarlier for the simpler function z squared, I showed it as a transformation, moving all of the inputs to the outputs.
24:1124 minutes, 11 secondsAnd in this case, for e to the z, if you're curious how that same idea looks, it's easiest to take a subset of the grid, like this one here from the input space,
24:1924 minutes, 19 secondsand here's what it looks like to move each square over to the corresponding output. As we actually use this function for our print gallery goals,
24:2724 minutes, 27 secondsit'll be very helpful to anchor your mind by thinking of these vertical lines and the circles they turn into.
24:3324 minutes, 33 secondsIn fact, there's a very playful way that I like to think about how these vertical lines turn into concentric circles and how they can carry the full input space along with them.
24:4124 minutes, 41 secondsWhat I like to imagine is sort of rolling up that entire z-plane into a tube, such that all of those vertical lines end up as circles.
24:5024 minutes, 50 secondsSpecifically, each circle would have a circumference of 2 pi. Next, imagine taking this tube, lining it up above the origin of the output space,
24:5824 minutes, 58 secondsand then kind of squishing it down onto that output space,
25:0225 minutes, 2 secondsturning all the circles from that tube into these concentric rings of exponentially growing size. That's just what I like, but however you choose to think about it,
25:1125 minutes, 11 secondswhat I want to be etched into your brain is the idea of vertical lines turning into circles.
25:1625 minutes, 16 secondsNow, the other very important point to emphasize here is that multiple different inputs can land on the same output.
25:2325 minutes, 23 secondsFor example, e to the zero is one, but e to the 2 pi i is also one. So is e to the negative 2 pi i and e to the 4 pi i and so on.
25:3425 minutes, 34 secondsIn fact, the infinite sequence along any given vertical line spaced out by 2 pi will all get collapsed together as that vertical line gets kind of rolled up into a circle.
25:4525 minutes, 45 secondsWe say that the exponential map is many to one,
25:4725 minutes, 47 secondsalthough it might not be obvious how this repetition in the vertical direction is going to be key to our final recreation of the print gallery effect.
Chapter 4: The complex logarithm
25:5625 minutes, 56 secondsOkay, so exponentials give us the first ingredient,
25:5925 minutes, 59 secondscharacterized by turning lines into circles, and the second ingredient we need is the inverse of such an exponential, known as the natural log,
26:0726 minutes, 7 secondswhere basically the idea is that it unravels those circles back into lines.
26:1126 minutes, 11 secondsNow, this will be especially fun to visualize and especially relevant to our story if we imagine painting this complex plane on the right with a Drosta image,
26:2026 minutes, 20 secondssay the example we were working with earlier with the pi creature looking at a picture of a house where that same pi creature lives.
26:2826 minutes, 28 secondsIn other words, it is finally time for you and me to answer that question of what it means to take the natural log of a picture.
26:3626 minutes, 36 secondsOkay, so think about this for a second.
26:3826 minutes, 38 secondsYou already know that a vertical line segment like this one on the left with a height of 2 pi gets turned into a circle when you apply the map e to the z.
26:4726 minutes, 47 secondsSo the natural log is going to take a circle of points on this image and then straighten them out into one of those lines.
26:5526 minutes, 55 secondsSimilarly, if you looked at a circle which was exactly e times smaller,
26:5926 minutes, 59 secondsthat would also get straightened out into a line with the same height positioned one unit to the left.
27:0527 minutes, 5 secondsAnd then similarly, every circle in between these two is going to get unwrapped into one of these vertical lines between those last two, and more generally,
27:1427 minutes, 14 secondssmaller and smaller rings from the picture will all get unwrapped into these vertical line segments, each one with a height of 2 pi,
27:2127 minutes, 21 secondsfarther and farther to the left in the image. The result we get is a bit trippy, but it's pretty cool when you think about it, and there's a number of important things that I want you to notice.
27:3027 minutes, 30 secondsYou've probably noticed that it repeats as you move to the left,
27:3327 minutes, 33 secondsand I'll invite you to ponder why that might be the case in the back of your mind for a minute, but before that repetition, I want to talk about a different direction in which it repeats.
27:4227 minutes, 42 secondsThe way I've drawn it so far, the imaginary part for the values on the left are ranging from 0 up to 2 pi, but that's actually kind of an arbitrary choice.
27:5127 minutes, 51 secondsRemember, if you keep letting that value z on the left walk up by another 2 pi units,
27:5627 minutes, 56 secondsthe corresponding value e to the z on the right would just keep walking around that same circle again, so I hope you'll agree it feels at least enticing to let our image repeat in this vertical direction along every one of those vertical lines.
28:1228 minutes, 12 secondsAnd it goes the other way too, as you let the imaginary part on the left get smaller going down, the corresponding value on that right just keeps walking around that same circle, so the pattern that you see should perhaps repeat in that way too.
28:2628 minutes, 26 secondsTo be more explicit, the rule that I'm using to draw this image on the left is that for every point z in that plane on the left,
28:3328 minutes, 33 secondsyou look at the corresponding value e to the z on the right, and then you assign it a matching color.
28:4028 minutes, 40 secondsSo for example, this warped pi creature and this one and this one all really correspond to the same part of the image on the right, the big pi creature in the lower left.
28:5128 minutes, 51 secondsAnother way to think about this is that because the function e to the z is many to one, the feeling we get is that the natural logarithm, its inverse,
28:5928 minutes, 59 secondswants to be a multi-valued function, something where one input maps to multiple different outputs.
29:0629 minutes, 6 secondsNow in practice, many times you don't want a function to have multiple outputs, sometimes that even defies the definition of a function in your context,
29:1429 minutes, 14 secondsso people will often just choose a band of this plane on the left to be the outputs of the natural log. In complex analysis, this is called choosing a branch cut for the function.
29:2429 minutes, 24 secondsFor our purposes though, where we want to recreate and understand Escher's piece, it's actually nice as to think of the log as a multi-valued function,
29:3229 minutes, 32 secondswhere each point on the right corresponds to a repeating sequence of points on the left, spaced out two pi vertically, going infinitely in both directions.
29:4129 minutes, 41 secondsNow in our special case, you also see this repeating pattern as you move to the left, but that is something different entirely. You would not see this for most images.
29:5129 minutes, 51 secondsIt arises specifically because we're working with a self-similar Drosta image, one that looks identical as you zoom in by a certain factor.
29:5929 minutes, 59 secondsThis falls straight out of a core property of logarithms and exponentials. Exponentials turn addition into multiplication,
30:0830 minutes, 8 secondsand logarithms turn multiplication back into addition. For example, imagine taking some small value w on this plane on the right,
30:1730 minutes, 17 secondsand also considering 16 times that value, which is scaled up 16 times farther away from the origin.
30:2430 minutes, 24 secondsNow if we look at the corresponding value, log of w on the left, that act of multiplying by 16 now looks like addition,
30:3230 minutes, 32 secondsspecifically shifting to the right by the natural log of 16, which is just some real number.
30:3930 minutes, 39 secondsIn fact, this rectangle here in our bizarre warped log image that has a width of log 16 and a height of 2 pi contains all the information about the image on the right.
30:5030 minutes, 50 secondsIt corresponds to this annulus of the Drosta image, and if you were to shift that rectangle exactly log of 16 units to the left,
30:5830 minutes, 58 secondsyou would get a scaled-down version of that annulus exactly 16 times smaller that nestles in perfectly like a puzzle piece.
31:0731 minutes, 7 secondsAnd if you repeat that infinitely many times, it gives you this infinite nesting that characterizes the Drosta zoom.
31:1431 minutes, 14 secondsThe way I've drawn things so far, we have this cutoff to the log image on the right side,
31:1931 minutes, 19 secondsand at this point you know well that vertical lines on the left correspond to circles on the right, so you can probably guess that this corresponds to the fact that I gave a maximum radius to that Drosta image, but of course you don't need to do that.
31:3131 minutes, 31 secondsIn principle, it can extend out infinitely far in all directions, following the same self-similar pattern as you scale up,
31:3831 minutes, 38 secondsand the result for the log image on the left would be to extend as far rightward as you want, again with a repeated tiling pattern.
31:4731 minutes, 47 secondsSo to conclude, the logarithm image on the left is periodic vertically, basically because rotation on the right is periodic.
31:5431 minutes, 54 secondsThis would happen for any image. And then in this special case of a Drosta image, it's also periodic horizontally, because the Drosta image repeats as you zoom in.
32:0432 minutes, 4 secondsThis doubly periodic property is what we'll ultimately take advantage of for the final result. And we now have all the foundation we need.
32:1332 minutes, 13 secondsI can now finally describe for you the function that turns the Drosta zoom into this Escher-style self-contained loop.
32:2032 minutes, 20 secondsBefore just jumping right into it, we have been kind of covering a lot, so it might be worth giving some space to let this digest.
32:2632 minutes, 26 secondsAnd I was meaning to take 30 quick seconds at some point in this video to talk about 3b1b talent, so now might be as good a time as any.
Chapter 5: 3b1b Talent
32:3232 minutes, 32 secondsThis is the virtual career fair that I'm experimenting with this year,
32:3632 minutes, 36 secondsand the basic idea is that you, a person who spends their free time learning about things like complex logarithms, are probably interested in working with like-minded,
32:4432 minutes, 44 secondscurious, and technical teams. So if you're seeking or open to a new job, check out the organizations at 3b1b.co/talent When you explore that page, you'll find interviews between me and the relevant teams,
32:5632 minutes, 56 secondstechnical puzzles and challenges that they've chosen to feature for you, and various other things aimed at giving you a feel for the technical team culture.
33:0433 minutes, 4 secondsAnd I just kind of like the idea of exposing this audience to aligned career opportunities, so whenever you are looking for a job, whether that's now or later, be sure to check it out.
Chapter 6: Constructing the key function
33:1433 minutes, 14 secondsOkay, so back to our main goal.
33:1633 minutes, 16 secondsHow is it that we can use everything that we've built up about complex functions and transformations that give conformal maps and everything like that to construct some kind of function that recreates Escher's print gallery effect?
33:2833 minutes, 28 secondsMaybe it's easiest if I just throw down the whole outline of the function, and then we can go through each step in more detail. First, take a logarithm, giving this bizarre doubly periodic tiling pattern,
33:3833 minutes, 38 secondsand then you rotate and scale that tiling pattern in just the right way, and then from there you take an exponential, which unworps it,
33:4733 minutes, 47 secondsbut this time with a certain twist.
33:5033 minutes, 50 secondsThis might seem a little bizarre, but there's actually a really nice way to motivate and to understand what's really going on here. Take a look back at that original Drosta image,
33:5933 minutes, 59 secondsand remember how we want to take this big pie creature and somehow identify it with the smaller self-similar copy, 16 times zoomed in.
34:0734 minutes, 7 secondsI want you to think about a line connecting both of those.
34:1134 minutes, 11 secondsOne way to frame the goal that we have is that we want the final function to transform such a line into a closed loop in the final space.
34:1934 minutes, 19 secondsThe endpoints of the line on the top represent the big and the small pie creatures, so whatever function identifies those creatures should, at the very least,
34:2834 minutes, 28 secondsclose up this line. Now think about what this line looks like in the logarithm of the image.
34:3334 minutes, 33 secondsThe big pie creature corresponds to all these multiple copies here next to the imaginary line. As we talked about, when you scale down the image,
34:4234 minutes, 42 secondsit corresponds to shifting to the left in the log, so these copies in the log image represent that small pie creature.
34:5034 minutes, 50 secondsAnd actually, instead of using this horizontal line,
34:5234 minutes, 52 secondswe're going to want to take advantage of the fact that this log image is periodic in two separate directions.
34:5834 minutes, 58 secondsSo instead, what we'll work with is a diagonal line that connects this copy of the big character to this lower left copy of the small one.
35:0735 minutes, 7 secondsThat might seem unmotivated at the moment, and it is, but the best way to explain why is just to show you how this plays out,
35:1335 minutes, 13 secondsand afterwards, if you want, we can contrast with what would have happened if you tried using the horizontal line.
35:1935 minutes, 19 secondsNow this new downward component in the log image corresponds to adding some clockwise rotation to the path in the original image.
35:2635 minutes, 26 secondsRemember, our goal is to turn this into a loop in the final image,
35:3035 minutes, 30 secondsbut you and I just spent like 10 minutes talking extensively about a function that turns line segments into circles, namely e to the z.
35:3935 minutes, 39 secondsWhat you need to do is get that line segment to end up perfectly vertical with a height of 2 pi, and doing this basically comes down to rotating and scaling it in just the right way to give it that length and direction.
35:5235 minutes, 52 secondsNow if you remember, as we were warming up with complex numbers,
35:5635 minutes, 56 secondswe talked about how multiplication by a constant gives you some combination of rotation and scaling, and in this case, one artistic feature we might like is for our big pi creature on the lower left to stay fixed in that position,
36:0836 minutes, 8 secondsand that would mean that this point in our log image needs to stay fixed in place,
36:1236 minutes, 12 secondsso instead of pivoting around the origin, we really want everything to pivot about that point. Let's say we label that point something like z naught,
36:2136 minutes, 21 secondsthen here's how the updated formula would look for that rotation and scaling,
36:2536 minutes, 25 secondsbut really most of the content comes down to choosing this constant c that you're going to multiply by, and if you like exercises,
36:3236 minutes, 32 secondsyou might enjoy actually taking a moment to work out what specific value that constant should take on. But right here, since we're being very visual and I want to have a little fun,
36:4236 minutes, 42 secondslet me show you that constant in its own little complex plane, and then also show what happens if I kind of grab it and move it around a little bit.
36:5036 minutes, 50 secondsDifferent choices give you different scaling and rotation, which after exponentiating gives you all these completely bizarre kaleidoscopic images.
36:5836 minutes, 58 secondsOne way you could think about the whole operation is as a game where you're trying to find just the right value that corresponds everything to line up as you need them to in that image of the lower right.
37:0937 minutes, 9 secondsWhen it is set to that appropriate value and we get this recreated Escher effect, in that final image on the lower right, I've been showing this hole in the middle,
37:1637 minutes, 16 secondsanalogous to the hole that Escher had in his original piece. But that's actually entirely artificial.
37:2237 minutes, 22 secondsThe output image of the function naturally fills that in with its own repeating spiral inward.
37:2837 minutes, 28 secondsAfter all, the rotated tiling pattern on the left extends infinitely through the whole plane, so when you take its exponential,
37:3537 minutes, 35 secondsit also fills in everything, except for the point at zero. And that's it! That is the basic operation.
37:4237 minutes, 42 secondsTranslate to this bizarre looking log space, rotate and scale to realign things, and then translate back with an exponential.
37:5137 minutes, 51 secondsAt this point, having recreated our own variation on Escher,
37:5437 minutes, 54 secondsit might be nice to step through what that same process looks like for Escher's specific example, that seaside Maltese town containing a print gallery with a person looking at a picture of the town.
38:0638 minutes, 6 secondsAs before, step number one is to place this scene on its own little complex plane, where the infinite limiting point about which everything scales is positioned at zero.
38:1638 minutes, 16 secondsStep two, take a logarithm of this, which in this case gives us a similarly bizarre transformation of the whole scene, but there is a little difference this time.
38:2438 minutes, 24 secondsBecause Escher was working with a much deeper zoom, with a scale factor of 256, the repeating tiles in this new example actually span a wider part of the complex plane.
38:3638 minutes, 36 secondsStep three, again, is to rotate and scale this, which depends on multiplying by the appropriate choice of a complex constant.
38:4338 minutes, 43 secondsThe constraint is to ensure that this rotated image still repeats every 2 pi units vertically, but along a part of the image that was previously diagonal.
38:5338 minutes, 53 secondsAnd then step four, plug this all through e to the z, and what you get is something very similar to Escher's final picture,
39:0039 minutesan image where walking around a loop corresponds to zooming in by a factor of 256. And again, when we frame it this way with complex functions,
39:1039 minutes, 10 secondsthere is no hole in the middle. That final result is itself a Drosta image, albeit this time with a twist,
39:1639 minutes, 16 secondswhere there's a kind of self-similarity spiraling down infinitely far as much as you want to zoom in.
39:2439 minutes, 24 secondsThere are a couple things worth noticing about this whole process. First off, if you write this idea down as a formula, where you take a log,
39:3139 minutes, 31 secondsmultiply it by a constant, and then exponentiate,
39:3339 minutes, 33 secondsthat can actually be simplified to simply look like raising your input to the power of some complex constant. And if you reintroduce that offset factor, it just introduces another constant.
39:4339 minutes, 43 secondsOn the one hand, it's very pleasing that this entire complicated process can be boiled down to so few symbols on the page, but I do think this risks kind of obscuring what's actually going on.
39:5339 minutes, 53 secondsAnd then, I had mentioned things would not work if you only tried using those horizontal lines. If you're curious, here's what it looks like if you try that,
40:0040 minuteswhich would mean rotating everything by 90 degrees and scaling it the appropriate amount. You do get something kind of interesting, but it's just not what we're going for.
40:0940 minutes, 9 secondsAnd if you think about it, what's basically going on is that you are swapping the roles of rotation and of scaling.
Chapter 7: The deeper math behind Escher
40:1640 minutes, 16 secondsStepping back from all this, this second perspective where the piece is all about rotating in a log space feels completely different from Escher's more intuitive approach using his distorted grid and the mesh warp.
40:2840 minutes, 28 secondsBut there is a through line connecting both perspectives.
40:3140 minutes, 31 secondsFor one thing, you can now understand how exactly we've been recreating and modifying the grid that Escher had. You basically take that same function that we've built up,
40:4040 minutes, 40 secondsbut instead of applying it to an image, you apply it to an ordinary square grid. Well, actually not quite an ordinary square grid.
40:4840 minutes, 48 secondsIt's nicest to work with one that gets more dense as you zoom in so that it looks the same at all scales. When you do this, the logarithm gives you this very beautiful curved tiling pattern.
40:5840 minutes, 58 secondsAnd then from there, you do the same trick of rotating things in just the right way and then taking an exponential with the result of something quite close to what Escher spent many arduous hours constructing.
41:0941 minutes, 9 secondsAnd remember, the entire reason that we're using the language of complex numbers is the motivation for me having you jump through those hoops is that this conformal property falls out as a byproduct.
41:2041 minutes, 20 secondsTiny squares from the original grid remain, at least approximately, square in the final result. Escher said that making this piece gave him some almighty headaches,
41:2941 minutes, 29 secondsand though maybe you and I had to endure a few headaches ourselves for very different reasons, the payoff is that this property is one that we get with no added effort.
41:3941 minutes, 39 secondsNow to be clear, you certainly don't need to understand complex derivatives or logarithms to enjoy Escher's work, and I wouldn't want to imply that you do.
41:4641 minutes, 46 secondsHowever, when you understand that more mathematical side,
41:4941 minutes, 49 secondsit gives you the capacity for a very different kind of appreciation for what Escher was really doing. And this is what I find fascinating about all of this,
41:5741 minutes, 57 secondsthe real connection I want to give between the two storylines. If you look at Escher's career, throughout it he was drawn to certain concepts,
42:0542 minutes, 5 secondsthings like representing infinity in a finite space. And at the same time, he seemed to be guided by a certain aesthetic,
42:1142 minutes, 11 secondsoften some implicit rigid rule like the idea of little squares remaining little squares for this mesh.
42:1742 minutes, 17 secondsThe end result when concept and aesthetic are combined like this is that a given piece from Escher often feels like a solution to a puzzle,
42:2542 minutes, 25 secondsbut one where it's not even obvious that a solution should exist.
42:2942 minutes, 29 secondsNow what I find so thought-provoking is that these visual puzzles that he landed on are not merely analogous to the act of doing math.
42:3642 minutes, 36 secondsThe specific structures that he was intuitively drawn to often hide within them very real and very deep mathematics.
42:4442 minutes, 44 secondsIn our example, the deeper structure is not just that the piece can be described with complex functions.
42:5042 minutes, 50 secondsThe ideas that we've touched on in this storyline are actually a lot closer than you might expect to the research frontiers. If you look back at our approach in the second half,
42:5942 minutes, 59 secondsremember how it relied on using this doubly periodic pattern in the complex plane, something that repeats in two separate directions.
43:0743 minutes, 7 secondsThere's actually a special name for functions of complex numbers that are doubly periodic like this. They're known as elliptic functions.
43:1443 minutes, 14 secondsIt would be way too much to explain right here exactly why these functions are so useful,
43:1943 minutes, 19 secondsbut one thing I want to highlight is that those two mathematicians I referenced at the start, the ones who provided the analysis of this piece, De Smit and Lenstra,
43:2743 minutes, 27 secondsare both number theorists, and elliptic functions play a very prominent role in modern number theory, providing a kind of bridge to other parts of mathematics.
43:3643 minutes, 36 secondsThis may at least partially explain how it is that they could look at this piece and think to construct that function that we laid out here.
43:4443 minutes, 44 secondsWhen I look at Escher's work, whether it's the print gallery or many other favorites,
43:4843 minutes, 48 secondsthe reason I love these pieces so much is that they awaken within me a very specific feeling that's hard to find elsewhere. It's a feeling of things perfectly fitting into place.
43:5843 minutes, 58 secondsBut that's not exactly it. It's something more than just the pleasure of seeing a puzzle solved.
44:0244 minutes, 2 secondsIt's an appreciation for the creative genius required to even dream up the puzzle in the first place. The only other place where I get that feeling is in doing math.
44:1144 minutes, 11 secondsSo the fact that an artist and a mathematician can be drawn to the same structures,
44:1644 minutes, 16 secondsbut for completely different reasons, suggests to me that there's something universal in what exactly it is that both of them seem to be drawn to.

Sync to video time