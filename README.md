# Introduction
jQuery.html5Loader can preload <b>images</b>, html5 <b>video</b> and <b>audio</b> sources, <b>css</b>, <b>scripts</b> and <b>text</b> files.
This plugin needs a <b>JSON</b> file to get the files that must be preloaded (you can use also use a javascript object as well), and it provides an easy API to give you the the amount of file loaded in percentage.

All the javascript and css files will be automatically loaded and injected into the DOM


## Features
* <b>smart</b>: it loads just the sources supported by the client running the script.
* <b>flexible</b>: it returns the current percentage and the object loaded, so you could be free to show this info as you like
* <b>fun</b>: inside the package you could find some preloading animation examples, customizable and ready to use




## Demos
 - [nprogress preloader](http://gianlucaguarini.github.io/jquery.html5loader/examples/demo-append-sources.html) by [Rico Sta. Cruz](https://github.com/rstacruz/nprogress)
 - [Append the files loaded on the fly](http://gianlucaguarini.github.io/jquery.html5loader/examples/demo-append-sources.html)
 - [Big counter animation](http://gianlucaguarini.github.io/jquery.html5loader/examples/demo-big-counter.html)
 - [Circular preloader](http://gianlucaguarini.github.io/jquery.html5loader/examples/demo-circular.html)
 - [Line preloader](http://gianlucaguarini.github.io/jquery.html5loader/examples/demo-line.html)

## Production websites using jQuery.html5loader
 - http://www.mobi-myhome.ch
 - http://lindberghallee.ch

# USAGE

### 1 Create a JSON file like this, containing all the files you need to preload ( size in bytes ):

<pre lang="json">
{
    "files": [
      {
        "type":"SCRIPT",
        "source":"../path/to/your/script.js",
        "size":4.096,
        "stopExecution":true
      },
      {
        "type":"SCRIPT",
        "source":"../path/to/your/script.js",
        "size":4.096,
        "stopExecution":false
      },
      {
        "type":"IMAGE",
        "source":"../path/to/your/image.jpg",
        "size":620
      },
      {
        "type": "CSS",
        "source": "../files/test.css",
        "size": 16.819
      },
      {
        "type":"TEXT",
        "source":"../path/to/your/text.txt",
        "size":44
      },
      {
        "type":"VIDEO",
        "sources": {
          "webm":{
            "source":"../path/to/your/video.webm",
            "size":5054.976
          },
          "ogg":{
            "source":"../path/to/your/video.ogg",
            "size":2932.736
          },
          "h264":{
            "source":"../path/to/your/video.mp4",
            "size":9285.632
          },
          "vp9": {
              "source":"../path/to/your/video.webm",
              "size":9285.632
            }
          }
        }
      },
      {
        "type":"AUDIO",
        "sources": {
          "mp3":{
            "source":"../path/to/your/audio.mp3",
            "size":9285.632
          },
          "ogg":{
            "source":"../path/to/your/audio.ogg",
            "size":2089.688
          },
          "opus": {
            "source": "../path/to/your/audio.opus",
            "size":2000.20
          },
          "wav": {
            "source": "../path/to/your/audio.wav",
            "size":2000.20
          },
          "m4a": {
            "source": "../path/to/your/audio.m4a",
            "size":2000.20
          }
        }
      }
    ]
  }
</pre>

### 2 Import the plugin into your page:

<pre lang="html">
&lt;script src=&quot;http://code.jquery.com/jquery-latest.min.js&quot;&gt;&lt;/script&gt;
&lt;script src=&quot;../js/jQuery.html5Loader.js&quot;&gt;&lt;/script&gt;
</pre>

### 3 Initialize the plugin setting the callback functions:

<pre lang="javascript">
$.html5Loader({
      filesToLoad:    '../js/files.json', // this could be a JSON or simply a javascript object
      onBeforeLoad:       function () {},
      onComplete:         function () {},
      onElementLoaded:    function ( obj, elm) { },
      onUpdate:           function ( percentage ) {}
});
</pre>


# API
## Methods
- <code>onBeforeLoad</code> It is triggered right before the plugin starts loading all the files
- <code>onComplete</code> It is triggered when the plugin finishes to load all the sources
- <code>onMediaError</code> This function is called in case there's an error during the preloading
  - <code>obj</code> original object passed to the plugin
  - <code>elm</code> html output (for type "SCRIPT" and "TEXT" this value is just a string)
- <code>stopExecution</code> (false by default) : default behavior for all the script files, they won't execute when loaded. This behavior can be changed by each script object passed to the plugin
- <code>onElementLoaded</code> It is triggered anytime a new element of your files list gets loaded, (ATTENTION IF AN ELEMENT IS NOT SUPPORTED IT WILL NEVER PASS TROUGH THIS FUNCTION).
  - <code>obj</code> original object passed to the plugin
  - <code>elm</code> html output (for type "SCRIPT" and "TEXT" this value is just a string)
- <code>onUpdate</code> it is triggered anytime new bytes are loaded
  - <code>percentage</code> the percentage currently loaded

# KNOWN ISSUES
- Internet Explorer 9 and 10 do not return any value using the method <code>canPlayType</code> on a video or audio element ( http://modernizr.com/docs/#audio ). For these browsers we don't preload any HTML5 media format
- on mobile devices and on the iPad we cannot load any video or audio element because these devices can't preload those kind of elements until the user start dealing with them

# CHANGELOG

## v1.6.8

- small refactor
- added: new media file codecs tests
 - video: vp9
 - audio: opus, wav, m4a
- added: stopExecution option
- added: stopExecution option via json
- added: nprogress demo

