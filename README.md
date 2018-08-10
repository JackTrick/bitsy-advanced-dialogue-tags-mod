
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
```

### Difference From the Hacks

* Rather than using parentheses "()" you should be able to use curly braces "{}" in dialogue to call the hack functions.
* You should not need to add anything to the exported HTML file to support the above hacks. However, if you want to use any of the other bitsy hacks, you should be able to add them to the bottom of the HTML file as you have in the past.

Note, loading and running your HTML in the non-modified Bitsy should still function, but you will need to manually add the hacks to your HTML file for them to work.

## Specific Hacks

### Edit Image From Dialog
Blah

### End From Dialog
Blah

### Exit From Dialog
Blah

### Paragraph Break
Blah

## Example File
An example file has been provided.

## Additional Information

My 'hack' is not particularly artful, it just places the hack code directly into bitsy rather than having a
developer add them to the html post-export and letting kitsy inject them where appropriate.

I figured the dialogue tags were relatively safe to add to the bitsy maker, as the tags
could just exist 'under the hood' unless someone actually wanted to use them.

If I've stepped on anyone's toes (particularly Adam Le Doux), do let me know.
Bitsy is a marvelous thing, and ultimately I just want to be helpful to its community <3

================

I chose to separate from kitsy, as what I mostly use is just dialogFunctions and deferredDialogFunctions.

Parts of the code I changed can be found accompanied by a comment of:
  // bitsy-advanced-dialogue-tags -jacktrick
  Note that this is not me trying to claim total credit for the code there 
  (again, that goes to Adam, Sean, and @mildmojo). 
  I just wanted to tag it so it could easily be found to edit/update/remove as people saw fit.

### Acknowledgements

Once again, big thanks to [Sean LeBlanc](https://github.com/seleb), @mildmojo, @ducklingsmith, and the [bitsy hacks page](https://github.com/seleb/bitsy-hacks).

Also, thank you to Von_Bednar and the other lovely folks of the bitsy discord channel <3