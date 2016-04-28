# Media Elements JS

- [mediaelementsjs](http://mediaelementjs.com)

## .srt Closed Captioning

```srt
0
00:00:00,1 --> 00:00:04
In the last two lessons, you learned about blah blah blah

1
00:00:04 --> 00:00:07
But browser vendors couldn't agree on a codec
```

Caption files using the _.srt_ file extension must be made executable:

```shell
chmod +x captions.srt
```

### Possible .srt Generators

- [Aegisub](http://www.aegisub.org)
- [Subs Factory](http://www.macupdate.com/app/mac/25826/subs-factory)

## Full Screen Video Media

The following `css` class applied to the `video` element will stretch the video media to fill the full window: 

```css
.video-class {
    position: fixed;
    top: 50%;
    left: 50%;
    min-width: 100%;
    min-height: 100%;
    width: auto;
    height: auto;
    z-index: -100;
    -ms-transform: translateX(-50%) translate(-50%);
    -moz-transform: translateX(-50%) translateY(-50%);
    -webkit-transform: translateX(-50%) translateY(-50%);
    transform: translateX(-50%) translateY(-50%);
    background-size: cover;
  }
```

Additional adjustments may be needed to accommodate full window video. 

### Captions

```css
  /* Increase the width to the full window to allow CC to be centered */
  .mejs-captions-layer { width: 100% !important; }

  .mejs-captions-position {
    /* Center the CC text */
    text-align: center !important;
    /* Adjust font size of CC text */
    font-size: 200%;
    /** 
     * Move captions further from the bottom of the screen.
     * default: 35px;
    */
    bottom: 70px;
  }

  .mejs-captions-position span {
    /* Adjust the span element that holds the CC text. */
    padding: 2em;
  }
```

## Controls

```css
/* Permanently remove the video conrol bar */
  .mejs-controls { display: none !important; }
```

### Custom CC Control

```javascript
// Includes jQuery for mediaelementjs plugin
$('audio,video').mediaelementplayer({
// auto-select this language (instead of starting with "None")
startLanguage:'en'
});

var v  = document.getElementById('video'),
btnCC  = document.getElementById('btn-cc'),
cc     = document.querySelector(".mejs-captions-position");
cc.style.display = 'none'; // hide captions

var ccMode = cc.style.display;

var toggleCaptions = function() {
  ccMode = ccMode === 'block' ? 'none' : 'block';
  cc.style.display = ccMode;
  console.log('CC should be ' + ccMode);
};

v.play();

btnCC.addEventListener('click', toggleCaptions, false);
```
