## DEVEINER

* made for twin veins (proxoxie + t3chnofairy)

<img width="1392" height="944" alt="Screenshot 2026-11-12 at 8 22 09 PM" src="https://github.com/user-attachments/assets/8395808e-7bb8-497c-876e-077255cf2c8c" />
  

I built an app for you that will allow you to upload code with existing inline comments, have them stripped out, then output a special "backup" reference file along with the new code in a ZIP file. The idea is to use this right before you upload the code to be pushed and deployed to the live website and upload the "deveined" code. Then when you need to edit it offline, load the deveined into the app, and then load in the backup file, which will restore your code to the way it was before with all the comments.

## SUGGESTIONS FOR SITE STYLES/EFFECTS

# 1. prevent text/object-selection when holding/dragging with finger (mobile) or mouse (desktop)

adding this to your CSS code should prevent that from happening and make it so only like normal text get selected (not like the images and the whole page; this was happening to me on mobile)

```body,
body * {
-webkit-user-select: none;
user-select: none;
-webkit-touch-callout: none;
-webkit-tap-highlight-color: transparent;
}
img,
svg,
video {
-webkit-user-drag: none;
}
input,
textarea,
select,
[contenteditable="true"],
.allow-selection,
.allow-selection * {
-webkit-user-select: text;
user-select: text;
-webkit-touch-callout: default;
```

# 2.  over-riding mobile video player auto-fullscreen 

this will allow the video to play at the scale it's intended to be, within the frame like you have it laid out currently. right now when youre on a phone and try to play the video, it automatically changes to full-screen mode (its a mobile browser default setting that you have to use some work around on 

On your index.html; find this:

<video id="video" preload="metadata" src="videos/twins.mov">
    Your browser does not support video.
</video>

Replace it with this:

```<video
    id="video"
    preload="metadata"
    src="videos/twins.mov"
    playsinline
    webkit-playsinline
    draggable="false"
>
    Your browser does not support video.
</video>
```

In your main.js; add this to the bottom, right before the closing </script> tag:

```document.addEventListener("dragstart", function(event) {
  if (event.target.closest("img, svg, video")) {
    event.preventDefault();
  }
});
```

# One last suggestion too!
- Right now, your "jam1" audio file is a .WAV. This is a hugeee file that a lot of browsers and mobile data plans might have trouble loading easily/quickly. Generally with audio streams on websites, you'd wanna convert the audio to .MP3. Imo the easiest/most intuitive converter for Mac is XLD [[link to download]](https://sourceforge.net/projects/xld/files/xld-20250302.dmg/download), you basically just set the output file to be MP3; drag the file onto the icon, and it spits it out converted. 
- You've got a similar issue here with the "twins.mov" file for the video in the player. It's almost 1.0 Gb large; that's like; the size of an average 720p feature-length movie file, and a total nightmare for almost any cellular data plan. My personal favorite video converter is Shutter Encoder [[link to download]](https://www.shutterencoder.com/). Here's a basic step-by-step for how to convert the video:

* 1. launch the program, drag and drop the video into the queue, and select "Output: H.264" from the dropdown menu:
 
<img width="378" height="777" alt="Screenshot 2026-11-12 at 2 56 05 PM" src="https://github.com/user-attachments/assets/b3de97e5-9aaf-425b-a051-5498e7cc815d" />

<img width="337" height="840" alt="Screenshot 2026-11-12 at 2 56 19 PM" src="https://github.com/user-attachments/assets/fdab277f-23aa-4159-bb53-093f570a5277" />

* 2. In the upper right under the source section, click the drop-down, and select a smaller video size (720x1280, 50% [at bottom], etc), then click "Start Function" and you should hear a little ring sound when it's done!
   
<img width="1356" height="737" alt="Screenshot 2026-11-12 at 2 56 41 PM" src="https://github.com/user-attachments/assets/b71f2c02-1d95-49cd-a5fe-2a99853c59ab" />

* 3. Make sure to update the code to so the new file extensions match (.mov -> .mp4, .wav > .mp3)
