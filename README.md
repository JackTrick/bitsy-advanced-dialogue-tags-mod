
# bitsy-advanced-dialogue-tags mod

A modified version of [Adam Le Doux](https://twitter.com/adamledoux)'s [Bitsy Game Maker](https://ledoux.itch.io/bitsy) (v5.1)

Borrowing HEAVILY and offering full credit to [Sean LeBlanc](https://github.com/seleb), @mildmojo, @ducklingsmith, and the [bitsy hacks page](https://github.com/seleb/bitsy-hacks).

## Overview

This modifies the Bitsy Game Maker to automatically include the following hacks:

* :paintbrush: [edit-image-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/edit%20image%20from%20dialog.js): edit sprites, items, and tiles from dialog 
* :end: [end-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/end-from-dialog.js): trigger an ending from dialog, including narration text
* :door: [exit-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/exit-from-dialog.js): exit to another room from dialog, including conditionals
* :page_with_curl: [paragraph-break](https://github.com/seleb/bitsy-hacks/blob/master/dist/paragraph-break.js): Adds paragraph breaks to the dialogue parser

### How To Use

* For now, download editor.zip and unpack it into a folder of your choosing.
* Open the folder, and run index.html in Firefox.
* Use it as you would standard Bitsy.

```
NOTE: THIS EDITOR MAY NOT WORK IN CHROME/EXPLORER. RUNNING IN FIREFOX IS RECOMMENDED.

EXPORTED GAMES SHOULD STILL RUN IN ANY BROWSER
```

### Warning

I tried to be fairly limited with my changes to avoid the possibility of bugs that could leave your bitsy game file in a bad state. I'm *pretty* sure you should be fine, but use at your own risk and save a backup copy.

### Difference From the Hacks

* You can choose to either use parentheses "()" or curly braces "{}" in dialogue to call the hack functions. Note that you may want to use parentheses to maintain compatibility with standard hack editing conventions.
* You should not need to add anything to the exported HTML file to support the above hacks. However, if you want to use any of the other bitsy hacks, you should be able to add them to the bottom of the HTML file as you have in the past.

```
Note, loading and running your HTML in the non-modified Bitsy should still function, 
but you will need to manually add the hacks to your HTML file for them to work.
```

## Specific Hacks

### Edit Image From Dialog
You can use this to edit the image data of sprites (including the player avatar), items, and tiles through dialog.
Image data can be replaced with data from another image, and the palette index can be set.
(image "map, target, source")
Parameters:
  map:    Type of image (SPR, TIL, or ITM)
  target: id/name of image to edit
  source: id/name of image to copy
(imageNow "map, target, source")
Same as (image), but applied immediately instead of after dialog is closed.
(imagePal "map, target, palette")
Parameters:
  map:    Type of image (SPR, TIL, or ITM)
  target: id/name of image to edit
  source: palette index (0 is bg, 1 is tiles, 2 is sprites/items, anything higher requires editing your game data to include more)
(imagePalNow "map, target, palette")
Same as (imagePal), but applied immediately instead of after dialog is closed.
Examples:
  (image "SPR, A, a")
  (imageNow "TIL, a, floor")
  (image "ITM, a, b")
  (imagePal "SPR, A, 1")
  (imagePalNow "TIL, floor, 2")
HOW TO USE:
  1. Copy-paste this script into a new script tag after the Bitsy source code.
     It should appear *before* any other mods that handle loading your game
     data so it executes *after* them (last-in first-out).
TIPS:
  - The player avatar is always a sprite with id "A"; you can edit your gamedata to give them a name for clarity
  - You can use the full names or shorthand of image types (e.g. "SPR" and "sprite" will both work)
  - The "source" images don't have to be placed anywhere; so long as they exist in the gamedata they'll work
  - This is a destructive operation! Unless you have a copy of an overwritten image, you won't be able to get it back during that run

### End From Dialog
Blah

### Exit From Dialog
Blah

### Paragraph Break
Blah

## Example File
An example level can be downloaded [here](https://github.com/JackTrick/bitsyhack/tree/master/example). You can load it into the editor for an example of most of the new functionality.

## Additional Information

My 'hack' is not particularly artful, it just places the hack code directly into bitsy rather than having a developer add them to the html post-export and letting kitsy inject them where appropriate.

I figured the dialogue tags were relatively safe to add to the bitsy maker, as the tags could just exist 'under the hood' unless someone actually wanted to use them.

If I've stepped on anyone's toes (particularly Adam Le Doux), do let me know. Bitsy is a marvelous thing, and ultimately I just want to be helpful to its community <3

Parts of the code I changed can be found accompanied by a comment of:
```
// bitsy-advanced-dialogue-tags -jacktrick
```

Note that this is not me trying to claim total credit for the code there. I just wanted to tag it so it could easily be found to edit/update/remove as people saw fit.

### Acknowledgements

Once again, big thanks to [Sean LeBlanc](https://github.com/seleb), @mildmojo, @ducklingsmith, and the [bitsy hacks page](https://github.com/seleb/bitsy-hacks).

Also, thank you to Von_Bednar and the other lovely folks of the bitsy discord channel for their help <3