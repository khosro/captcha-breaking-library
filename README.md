# CAPTCHA Breaking Scripting Language #

## Introduction ##

The CAPTCHA Breaking Library and Scripting Language provides the necessary tools for quickly creating a program capable of reading text out of an image. 
The actual job of determining which letter is in a given image is done with the help of **Neural Networks**, **Contour Analysis**, and **Bitmap Vector Subtraction**.

CAPTCHAs that are able to be segmented by color (i.e., each letter is a different color) may first be converted to a **perceptive color space** where 
distances between colors are mathematically determined based on how the human eyes perceive color, not how colors are different in the RGB color-space. 
This allows most multicolor CAPTCHAs to be solved quite trivially.

## Documentation ##

To get started, check out the 
[hello world tutorial](https://github.com/skotz/captcha-breaking-library/blob/wiki/HelloWorld.md),
the [language syntax](https://github.com/skotz/captcha-breaking-library/blob/wiki/Syntax.md),
and the [solver walkthrough](https://github.com/skotz/captcha-breaking-library/tree/master/Examples/Color%20CAPTCHA/readme.md).

## Example ##

Here is a code snippet written in CBL that breaks a CAPTCHA originally from [here](http://www.codeproject.com/Articles/5947/CAPTCHA-Imag).

![CAPTCHA](https://github.com/skotz/captcha-breaking-library/blob/master/ART/42028351.png)

```
**********************************************************
* Scott Clayton                           April 14, 2012 *
**********************************************************
* This script is part of the CBL interpreter:            *
* http://code.google.com/p/captcha-breaking-library/     *
**********************************************************
* The CAPTCHA that this script breaks came from:         *
* http://www.codeproject.com/Articles/5947/CAPTCHA-Image *
**********************************************************

SetMode,        all
SetupSegmenter, BLOB, 4, 14, 8
SetupSolver,    MNN, "0123456789", 20, 20, 8, 150, 0.95
Load,           "mnn.solver.db"

DefinePreconditions
   Resize,           400, 100
   Subtract,         "merge3.bmp"
   Invert
   Median,           1
   MeanShift,        1, 2, 5
   Binarize,         150
   ColorFillBlobs,   80, 52
   RemoveSmallBlobs, 90, 4, 14
   HistogramRotate
   Binarize,         200
   ColorFillBlobs
EndPreconditions

Solve, %IMAGE%
```

Here's the CBL GUI running the script you see above on a CAPTCHA:

![Example 1](https://github.com/skotz/captcha-breaking-library/blob/wiki/main-example-01.png)

![Example 2](https://github.com/skotz/captcha-breaking-library/blob/wiki/main-example-02.png)


## Notepad++ Plugin ##

Be sure to install the [Notepad++](http://notepad-plus-plus.org/) syntax highlighting plugin on the downloads page to get syntax highlighting for CBL. 
Installation instructions are included in the Readme.txt file in the download.


_Scott_

Exported from my old [Google Code](https://code.google.com/p/captcha-breaking-library/) repository.
