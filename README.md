
# bitsy-advanced-dialogue-tags mod

A modified version of [Adam Le Doux](https://twitter.com/adamledoux)'s [Bitsy Game Maker](https://ledoux.itch.io/bitsy) (v5.1)

Borrowing HEAVILY and offering full credit to [Sean LeBlanc](https://github.com/seleb), [mildmojo](https://github.com/mildmojo), [ducklingsmith](https://github.com/ducklingsmith), and the [bitsy hacks page](https://github.com/seleb/bitsy-hacks).

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

## Example File
An example level can be downloaded [here](https://github.com/JackTrick/bitsyhack/tree/master/example). You can load it into the editor for an example of most of the new functionality.

You can also play the level [here](https://jacktrick.itch.io/bitsy-advanced-dialog-tag-mods-example).

### Warning

I tried to be fairly limited with my changes to avoid the possibility of bugs that could leave your bitsy game file in a bad state. I'm *pretty* sure you should be fine, but use at your own risk and save a backup copy.

### Difference From the Hacks

* You can choose to either use parentheses "()" or curly braces "{}" in dialogue to call the hack functions. Note that you may want to use parentheses to maintain compatibility with standard hack editing conventions.
* You should not need to add anything to the exported HTML file to support the above hacks. However, if you want to use any of the other bitsy hacks, you should be able to add them to the bottom of the HTML file as you have in the past.

```
Note, loading and running your HTML in the non-modified Bitsy should still function, 
but you will need to manually add the hacks to your HTML file for them to work.
```

## Using the Specific Hacks

### Edit Image From Dialog
You can use this to edit the image data of sprites (including the player avatar), items, and tiles through dialog.

Image data can be replaced with data from another image with (image) and (imageNow), or the palette index can be set with (imagePal) and (imagePalNow).

Using the (image) or (imagePal) functions in any part of a series of dialog will edit the image after the dialog is finished.

Using (imageNow) or (imagePalNow) will immediately edit the image.

TIPS:
  - The player avatar is always a sprite with id "A"; you can edit your gamedata to give them a name for clarity
  - You can use the full names or shorthand of image types (e.g. "SPR" and "sprite" will both work)
  - The "source" images don't have to be placed anywhere; so long as they exist in the gamedata they'll work
  - This is a destructive operation! Unless you have a copy of an overwritten image, you won't be able to get it back during that run

```
Parameters:
  (for image and imageNow)
     map:    Type of the images (SPR, TIL, or ITM)
     target: id/name of image to edit
     source: id/name of image to copy

  (for imagePal and imagePalNow)
     map:    Type of the images (SPR, TIL, or ITM)
     target: id/name of image to edit
     source: palette index (0 is bg, 1 is tiles, 2 is sprites/items, 
                           higher requires editing your game data to include more)

Usage: (image "<map>, <target>, <source>")
       (imageNow "<map>, <target>, <source>")
       (imagePal "<map>, <target>, <palette>")
       (imagePalNow "<map>, <target>, <palette>")

Example: (image "SPR, A, a")
         (imageNow "TIL, a, floor")
         (image "ITM, a, b")
         (imagePal "SPR, A, 1")
         (imagePalNow "TIL, floor, 2")
```

### End From Dialog
Lets you end the game from dialog (including inside conditionals).

Using the (end) function in any part of a series of dialog will make the game end after the dialog is finished. Ending the game resets it back to the intro.

Using (endNow) at the end of a sentence will display the whole sentence and immediately clear the background. No further dialog from that passage will display, and the game will reset when you proceed. 

Using (endNow) with narration text will immediately exit the dialog, clear the background, and show the ending narration in an ending-style centered dialog box.
```
Usage: (end)
       (end "<ending narration>")
       (endNow)
       (endNow "<ending narration>")

Example: (end)
         (end "Five friars bid you goodbye. You leave the temple, hopeful.")
         (endNow "The computer is still online! The chamber floods with neurotoxin.")
```

### Exit From Dialog
Lets you exit to another room from dialog (including inside conditionals). 

Use it to make an invisible sprite that acts as a conditional exit, use it to warp somewhere after a conversation, use it to put a guard at your gate who only lets you in once you're disguised, use it to require payment before the ferryman will take you across the river.

Using the (exit) function in any part of a series of dialog will make the game exit to the new room after the dialog is finished. 

Using (exitNow) will immediately warp to the new room, but the current dialog will continue

```
WARNING: In exit coordinates, the TOP LEFT tile is (0,0). In sprite coordinates,
         the BOTTOM LEFT tile is (0,0). If you'd like to use sprite coordinates,
         add the word "sprite" as the fourth parameter to the exit function.

Usage: (exit "<room name>,<x>,<y>")
       (exit "<room name>,<x>,<y>,sprite")
       (exitNow "<room name>,<x>,<y>")
       (exitNow "<room name>,<x>,<y>,sprite")

Example: (exit "FinalRoom,8,4")
         (exitNow "FinalRoom,8,11,sprite")
```

### Paragraph Break
Adds a (p) tag to the dialogue parser that forces the following text to start on a fresh dialogue screen, eliminating the need to spend hours testing line lengths or adding multiple line breaks that then have to be reviewed when you make edits or change the font size.
```
Usage: (p)
       
Example: I am a cat(p)and my dialogue contains multitudes
```

## Additional Information

My 'hack' is not particularly artful, it just places the hack code directly into bitsy rather than having a developer add them to the html post-export and letting kitsy inject them where appropriate.

I figured the dialogue tags were relatively safe to add to the bitsy maker, as the tags could just exist 'under the hood' unless someone actually wanted to use them.

If I've stepped on anyone's toes (particularly Adam Le Doux), do let me know. Bitsy is a marvelous thing, and ultimately I just want to be helpful to its community <3

Parts of the code I changed can be found accompanied by a comment of:
```
// bitsy-advanced-dialogue-tags -jacktrick
```

Note that this is not me trying to claim total credit for the code there. I just wanted to tag it so it could easily be found to edit/update/remove as people saw fit.

## Other Useful Links

* [Bitsy Tutorial](https://www.clairemorleyart.com/a-bitsy-tutorial)
* [Bitsy FAQ](https://docs.google.com/document/d/1jRz3wgkQU3kZN_LGChw4UlMWhVoc145J-euBtkr7NeE/edit#)
* [Bitsy Wiki](http://bitsy.wikia.com/wiki/Bitsy_Wiki)
* [Bitsy Hacks](https://github.com/seleb/bitsy-hacks)
* [Bitsy Discord](https://discord.gg/NYh43Xr)