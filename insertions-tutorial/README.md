
# Tutorial
This system is OS X-only and was tested in a OS X 10.11.6. Let me know if you ever test this in another version/distribution, I'd love to know!

## Dependencies
To start, we need to install the following software:
- [webInsertion software](https://www.dropbox.com/sh/iiwf8gqqzjp75fn/AAB8OtNXv44U7p0Vcwti85aOa?dl=0): Software that allows you to modify the incoming video using a friendly programming languages, as if it was a webcam. Make sure you download the right version for you platform (i.e. 32 or 64 bits). In addition, because this software is not Apple certified, there’s a chance you might have a security-related problem (*"this application is damaged and cannot be opened"* or something like that). In this case, follow [this link](http://osxdaily.com/2016/09/27/allow-apps-from-anywhere-macos-gatekeeper/) to solve the problem;
- [Youtube-dl](https://github.com/rg3/youtube-dl/): Command line tool that allows you to extract an m3u8 file from several resources, such as Youtube Live and others;
- [Open-broadcast software (OBS)](https://obsproject.com/): Software tool that allows you to broadcast videos to several services such as Youtube and Facebook Live;
- [Soundflower](https://soundflower.en.softonic.com/mac): Software tool that allows you to route whatever you're hearing in your speakers as a "virtual michrophone" to feed external software.


## Process
The image below summarizes the process. After selecting your video target (**step 1**, picture (a)), you will process it locally on openFrameworks and OBS (**step 2**, picture (b)). The result is going to be streamed back to whatever service you'd like, such as the youtube (**step 3**, picture (c)).

![Setup](assets/setup.png)

## Step 1: From the internet to your computer
In the beginning, you need to choose the live video stream you want to target. This video is represented in the picture above by (a). For example, you can go to the [Youtube Live](https://www.youtube.com/live), open the video you want to modify, and copy its URL.

Once you copied this URL, you only need paste it inside a text file called "video.txt". This file is placed inside the folder "data" that comes along with the webInsertion software you downloaded. As follows:

![Screenshot](assets/modify-video-txt.png)

When you're done, you can open the webInsertion software you just downloaded. If you see the video playing, everything should be OK!

![Screenshot](assets/webInsertion-screenshot.png)

At any time, you can change the target video by modifying the "video.txt" and by clicking on "reload URL from file" inside the application. You can hide the debug info by unselecting "Show debug info".

If you're having problems, make sure you have picked a valid video, and that its link is correctly pasted into the "video.txt" file.

## Step 2: Modify it!
For this step, you'll need first to configure both *video* and *audio*. Then, you will be able to insert basic media on the video such as overlaying images and sound. This step is represented by picture (b).

### Configuring video
Here, we are going to use the Open-broadcast software (OBS). A full explanation of OBS is beyond the scope of this tutorial, you can find [several on youtube](https://www.youtube.com/watch?v=LX04mw_xG6A). It's enough to say here that it is:
1. **Open source** (i.e. free, and community driven);
2. **Powerful** (i.e. allows you to easily add images, sound, and other things to your video); and
3. **Easy to use** (you can learn how to use only by trying it out).

Roughly, the more familiar you are with it, the more sophisticated are the insertions you can do with it. In this tutorial, we'll stick to very the basics.

This is how OBS should look like:

![obs-part-0](assets/obs-part-0.png)

To import your video inside OBS you'll need first to go to *"Sources"*, and click in *"+"*:

![obs-part-1](assets/obs-part-1.png)

Then, click on *"Game Capture Syphon"*, and then on *"Create new"*:

![obs-part-2](assets/obs-part-2.png)

Go in *"Source"* and choose *"[webInsertion] Insertion output"*. It's **essential** that the webInsertion app is up and running before this options is available to you (see Step 1 if it's not):

![obs-part-3](assets/obs-part-3.png)

By now, you should be seeing the video output inside OBS. That's great! You only need to adjust the size according to the output window provided by OBS.

![obs-part-4](assets/obs-part-4.png)

### Configuring audio
To import your audio inside OBS you'll need to:

1. Go to *System preferences* > *Sound* > *Output*;
2. Select Soundflower as default output.

Don't forget to set your speakers as default when you're done!

By them you should notice that you can (should?) no longer hear your speakers. Everything now is being routed by default to Soundflower. This allows you to import the routed audio inside external applications as if your speakers were a microphone. Actually, this is exactly what want to do inside OBS by:

3. Clicking on *Desktop Audio settings* (i.e. the wheels) > *Properties;*
4. Choose *Soundflower (2ch)* as device.

If everything is fine, you should be able to see the green volume line moving in your Desktop Audio options. You should also make sure the Mix/Aux is properly muted. As follows:

![configuring-audio](assets/configuring-audio.png)

### Basic overlaying!

It's time to make some modifications in our video!

We won't cover this substep in details, we leave this to you. As we already said, the more familiar you are with OBS, the more sophisticated are the insertions you can do with it.

In summary: all you can do is available by clicking on  *"Sources"*, and then on *"+"*. As follows:

![obs-part-1](assets/obs-fake-news.png)

Each options you see offer some element you can add to the video. For instance, **Image** allows you to overlay multiple images (as in the image above). **Media source** allows you to overlay another video, or yet an audio file to the stream. And so on. Take your time to explore these possibilities. If you want to go advanced, you might want to explore the **Scenes**, that gives you the possibility of transitions between different setups (e.g. when it's commercial time, you might want an overlay to disappear).

## Step 3: From your computer to the internet
Finally, you need to configure OBS to stream your inserted video to the target stream service (e.g. Youtube Live, Facebook like, etc). You can do this by:

1. Going to **Settings**;
2. When the window opens, go to **Stream**;

This window will give you the options available for outputing your insertion, as follows:

![obs-part-1](assets/obs-stream.png)

Again, we won't go in details here. Each service uses its own way to authenticate the stream. After choosing yours (e.g. Facebook Live), you need to google for the details. As an example, in the particular case of choosing the Youtube, you just need to select "Youtube" as service, and update the individual stream key provided to you in your [Youtube Live page](https://www.youtube.com/live_dashboard).

Thats it! Now, you just need to click on **start streaming** to start your insertion!

# Advanced insertions (for developers)
If you are familiar with C++/Openframeworks, you can play around with the video before sending it to OBS by modifying the source code. This gives you the possibility of doing things way more complex and sophisticated than basic overlaying.

In this case, you'll also need as dependencies:
- openFrameworks ([version 0.9.8](http://openframeworks.cc/download/));
- xCode (get started on using xCode with openFrameworks [here](http://openframeworks.cc/setup/xcode/));
- The [webInsertion's source](https://github.com/jeraman/insertions/tree/master/osx/webInsertion).

You'll also need to install the following oF addons:
- https://github.com/jvcleave/ofxAvFoundationHLSPlayer
- https://github.com/astellato/ofxSyphon

A major thing here to keep in mind is that whatever you draw in the screen before the command *"mainOutputSyphonServer.publishScreen()"* is going to get sent to OBS. Thus, for example:

```cpp
ofDrawCircle(150,150,100);
mainOutputSyphonServer.publishScreen();
```
In this first case, the circle *will* be sent to OBS. However, here:

```cpp
mainOutputSyphonServer.publishScreen();
ofDrawCircle(150,150,100);
```
The circle *won't* be sent to OBS.

Have fun! And don't forget to share your results around here! ;)

--

[Jeraman](https://jeraman.info), 2017.
