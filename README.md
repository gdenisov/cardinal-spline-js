Cardinal spline / Catmull-Rom
=============================

A Cardinal spline (Cubic Hermite spline interpolation, Catmull-Rom with a tension option)
implementation for JavaScript/HTML5 which creates an interpolated smooth curve through each
point pair in the given array. There is no need to specify control points.

![Demo snapshot](http://i.imgur.com/5e69T5C.png)

The archive comes with three separate versions for the sake of convenience:

    curve.js      - Canvas 2D context extension. Call curve() on the context (ctx.curve(...))
    curve_func.js - if you get sweaty palms with the idea of using extensions: this is a pure
                    function that takes the context as an argument instead of extending it.
    curve_calc.js - just the function that calculates the points. Does not draw anything.

As well as their minified equivalent. There are no dependencies between these implementations.


Usage
=====

curve.js or curve.min.js:
-------------------------

Make sure the script is loaded before a 2D context is obtained from the canvas element.

Then use `curve()` as any other method/function on the context -

**Examples**

    ctx.moveTo(points[0], points[1]);  // optionally move to first point
    ctx.curve(points);                 // add cardinal spline to path
    ctx.stroke();                      // stroke path

will draw the points in the array which are arranged in the following manner:

    var points = [x1, y1,  x2, y2, ... xn, yn];

Optionally a tension value can be given *(default: 0.5)*:

    ctx.curve(points, 0.5);            // sets tension [0.0, 1.0] +/-

as well as a segment resolution value *(default: 25)*:

    ctx.curve(points, 0.5, 25);        // points in each segment

The curve can be drawn closed. All arguments must be given in this
case *(default: false (open))*:

    ctx.curve(points, 0.5, 20, true);  // make a closed loop

The function returns a new (typed) array with the spline points which can be used for
tracking, calculate length and so forth. The values are in floating points:

    var splinePoints = ctx.curve(points);


curve_func.js or curve_func.min.js:
-----------------------------------

If you use the function file instead, the arguments are the same as above
except that the context is passed in as the first argument and then the
function is instead called as:

    ctx.moveTo(points[0], points[1]);  // optionally move to first point
    curve(ctx, points);                // add cardinal spline to path
    ctx.stroke();                      // stroke path

Also this variant returns a spline point array.


curve_calc.js or curve_calc.min.js:
-----------------------------------

If you just want the calculated points without drawing anything, then use
the `curve_calc.js` file and call (please observe that the name has been
changed to better reflect its purpose):

    var splinePoints = getCurvePoints(points, ...);

Context is not required with this function.


Requirements
============

A modern HTML5 compliant browser with support for Typed Arrays and
JavaScript enabled. Except from `curve_calc.js` the canvas element and
a 2D context is required as well.


License
=======

Released under [MIT license](http://choosealicense.com/licenses/mit/). You can use this class in both commercial and non-commercial projects provided that full header (minified and developer versions) is included.

*&copy; 2013-2014 Epistemex*

![Epistemex](http://i.imgur.com/YxO8CtB.png)
