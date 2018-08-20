
# bitsy-advanced-dialogue-tags mod

A modified version of [Adam Le Doux](https://twitter.com/adamledoux)'s [Bitsy Game Maker](https://ledoux.itch.io/bitsy) (v5.1)

Borrowing HEAVILY and offering full credit to [Sean LeBlanc](https://github.com/seleb), [mildmojo](https://github.com/mildmojo), [ducklingsmith](https://github.com/ducklingsmith), and the [bitsy hacks page](https://github.com/seleb/bitsy-hacks).

## Overview

This modifies the Bitsy Game Maker to automatically include the following hacks:

* :paintbrush: [edit-image-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/edit%20image%20from%20dialog.js): edit sprites, items, and tiles from dialog 
* :end: [end-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/end-from-dialog.js): trigger an ending from dialog, including narration text
* :door: [exit-from-dialog](https://github.com/seleb/bitsy-hacks/blob/master/dist/exit-from-dialog.js): exit to another room from dialog, including conditionals
* :page_with_curl: [paragraph-break](https://github.com/seleb/bitsy-hacks/blob/master/dist/paragraph-break.js): Adds paragraph breaks to the dialogue parser
* :rainbow: edit-current-room-palette: edit the current room's palette index
* :alarm_clock: timer-variant-dialog-hacks: adds a set of functions that are variants of the above hacks with a timer that determines when they execute

### How To Use

* For now, download editor.zip and unpack it into a folder of your choosing.
* Open the folder, and run index.html in Firefox.
* Use it as you would standard Bitsy.

```
THIS EDITOR MAY NOT WORK IN CHROME/EXPLORER. RUNNING IN FIREFOX IS RECOMMENDED.

EXPORTED GAMES SHOULD STILL RUN IN ANY BROWSER
```

### :smiley_cat: Example File :tea:
An example level showcasing the changes is playable [here](https://jacktrick.itch.io/bitsy-advanced-dialog-tag-mods-example).

The level can be downloaded [here](https://github.com/JackTrick/bitsyhack/tree/master/example). You can load it into the editor for an example of most of the new functionality.

### :warning: Warning

I tried to be fairly limited with my changes to avoid the possibility of bugs that could leave your bitsy game file in a bad state. I'm *pretty* sure you should be fine, but use at your own risk and save a backup copy.

### Difference From the Hacks

* You can choose to either use parentheses "()" or curly braces "{}" in dialogue to call the hack functions. My preference is parentheses for compatibility with other hacked editors, and to better differentiate the unofficial hacks.
* You should not need to add anything to the exported HTML file to support the above hacks. However, if you want to use any of the other bitsy hacks, you should be able to add them to the bottom of the HTML file as you have in the past.

```
Note, loading and running your HTML in the non-modified Bitsy should still function, 
but you will need to manually add the hacks to your HTML file for them to work.
```

## Using the Specific Hacks

### :paintbrush: Edit Image From Dialog
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
       (imagePal "<map>, <target>, <palette>")

       (imageNow "<map>, <target>, <source>")
       (imagePalNow "<map>, <target>, <palette>")

Example: (image "SPR, A, a")
         (imageNow "TIL, a, floor")
         (image "ITM, a, b")
         (imagePal "SPR, A, 1")
         (imagePalNow "TIL, floor, 2")
```

### :end: End From Dialog
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

### :door: Exit From Dialog
Lets you exit to another room from dialog (including inside conditionals). 

Use it to make an invisible sprite that acts as a conditional exit, use it to warp somewhere after a conversation, use it to put a guard at your gate who only lets you in once you're disguised, use it to require payment before the ferryman will take you across the river.

Using the (exit) function in any part of a series of dialog will make the game exit to the new room after the dialog is finished. 

Using (exitNow) will immediately warp to the new room, but the current dialog will continue.

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

### :page_with_curl:  Paragraph Break
Adds a (p) tag to the dialogue parser that forces the following text to start on a fresh dialogue screen, eliminating the need to spend hours testing line lengths or adding multiple line breaks that then have to be reviewed when you make edits or change the font size.
```
Usage: (p)
       
Example: I am a cat(p)and my dialogue contains multitudes
```

### :rainbow: Edit Current Room Palette From Dialog

Lets you edit the current room's palette index from dialog (including inside conditionals).

Use it change the overall emotional tone of a room, or to signify a certain condition. Consider the timer variant of it to create 'effects' of lightning or being hit.

Using the (curRoomPal) function in any part of a series of dialog will change the current room palette to the provided index after the dialog is finished.

Using (curRoomPalNow) will immediately change the current room's palette, but the current dialog will continue.
```
       palette:    should be the index of the palette (can be found in the game data).
                   You can try palette names, but I've found that buggy so far. 
                   Will try to fix that in a future update.

Usage: (curRoomPal "<palette>")

       (curRoomPalNow "<palette>")

Example: (curRoomPal "1")
         (curRoomPalNow "2")
```

### :alarm_clock: Timer Variant Dialog Hacks

These are variants of the above hacks where you provide a duration (in milliseconds) and an optional condition (simple logic check)

Once the timer starts, it will wait until its duration has passed and then try to execute its dialog function. If a condition has been defined, it will be checked first to see if the dialog function should be executed.

:warning: Conditions ONLY support variable/number single operations. It does NOT support strings NOR multiple operations.
* :white_check_mark: a == 1 
* :white_check_mark: a < 42
* :white_check_mark: a != 3
* :white_check_mark: a = a + 1
* :white_check_mark: a = a + b
* :x: a == "cat fed"
* :x: a < 42 & a > 10

Using the normal variant function in any part of a series of dialog will start the timer after the dialog is finished.

Using the (Now) variant function will immediately start the timer, but the current dialog will continue. 

:heavy_exclamation_mark: If you define in a dialog a series of Now timers with a condition, and the condition evaluates to false, all following Now timers in that dialog will be ignored. Standard timers will evaluate individually regardless of any of their conditions.

#### :paintbrush: Edit Image From Dialog, :alarm_clock: Timer Variant
![Edit Image Timer Example|50%](https://github.com/JackTrick/bitsy-advanced-dialogue-tags-mod/blob/master/example/ex-changeimage-timer.gif?raw=true)

```
Usage: (imageTimer "<duration>, <map>, <target>, <source>")
       (imageTimer "<duration>, <map>, <target>, <source>, <condition>")
       (imageTimerPal "<duration>, <map>, <target>, <palette>")
       (imageTimerPal "<duration>, <map>, <target>, <palette>")
       
       (imageTimerNow "<duration>, <map>, <target>, <source>")
       (imageTimerNow "<duration>, <map>, <target>, <source>, <condition>")
       (imageTimerPalNow "<duration>, <map>, <target>, <palette>")
       (imageTimerPalNow "<duration>, <map>, <target>, <palette>, <condition>")

Example: (imageTimer "3000, SPR, A, a") // 3000 = 3 seconds
         (imageTimerNow "1000, TIL, a, floor, lava == 1")
         (imageTimer "3000, ITM, a, b")
         (imageTimerPal "1500, SPR, A, 1, a = a + 1")
         (imageTimerPalNow "1000, TIL, floor, 2, b != a")
```

#### :door: End From Dialog, :alarm_clock: Timer Variant

A specific (Narrate) version of the dialog function is used for specifying end narration.

```
Usage: (endTimer "<duration>")
       (endTimer "<duration>, <condition>")
       (endTimerNarrate "<duration>, <ending narration>")
       (endTimerNarrate "<duration>, <ending narration>, <condition>")

       (endTimerNow "<duration>")
       (endTimerNow "<duration>, <condition>")       
       (endTimerNarrateNow "<duration>, <ending narration>")
       (endTimerNarrateNow "<duration>, <ending narration>, <condition>")

Example: (endTimer "5000")
         (endTimerNarrate "10000", You ran out of time..., lava = 1")
         (endTimerNarrateNow "3000, The computer is still online! The chamber floods with neurotoxin.")
```

#### :door: Exit From Dialog, :alarm_clock: Timer Variant

Note, the Timer Variant of Exit From Dialog does NOT support sprite coordinate positioning at this time.
```
WARNING: In exit coordinates, the TOP LEFT tile is (0,0). 

Usage: (exitTimer "<duration>, <room name>, <x>, <y>")
       (exitTimer "<duration>, <room name>, <x>, <y>, <condition>")

       (exitTimerNow "<duration>, <room name>, <x>, <y>")
       (exitTimerNow "<duration>, <room name>, <x>, <y>, <condition>")

Example: (exitTimer "3000, FinalRoom, 8, 4")
         (exitTimerNow "5000, FinalRoom, 8, 11, a >= 42)
```

#### :rainbow: Edit Current Room Palette From Dialog, :alarm_clock: Timer Variant

```
Usage: (curRoomPalTimer "<duration>, <palette index>")
       (curRoomPalTimer "<duration>, <palette index>, <condition>")

       (curRoomPalTimerNow "<duration>, <palette index>")
       (curRoomPalTimerNow "<duration>, <palette index>, <condition>")

Example: (curRoomPal "4000, 1, a == 0")
         (curRoomPalNow "3000, 5")
```

## Additional Information

This 'hack' is not particularly artful, it just places the hack code directly into bitsy rather than having a developer add them to the html post-export and letting kitsy inject them where appropriate.

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