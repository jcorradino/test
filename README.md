# CrowdSurfing Fullscreen
CrowdSurfing supporters fullscreen functionality when configured.  Follow the instructions below to implement this functionality into your application.

## CrowdSurfing configurations - Under the `Fullscreen Settings` box
 * `Allow fullscreen` option should be checked in CrowdSurfing event config
 * `Outer wrapper containing player and widget DOM selector` should be set to the css selector of the parent element of player and widget. If none exist, set to either `null` or `body` (see below).
 * `CrowdSurfing widget's wrapper DOM selector` should contain the css selector of the widget's wrapper
 * `Video player's wrapper DOM selector` should contain css selector of video player's wrapper
 * `Player` - Optional, videoplayer name. This is used to activate some player-specific scripts. Only `twitch` is currently supported.

You can set these parameters in admin panel or in embedded code.  You can find an example of these settings within the embed code below.

Example: 
```HTML
<script id="crowdsurfing-script"
    src="https://s3.amazonaws.com/liveone-static/events/53d7937fdbc2a9867e8b4569.js"
    type="text/javascript">({
        fullscreen: true,
        wrapper: document.body,
        csWrapper: '#wrapper',
        playerWrapper: '#player'
    })</script>
```

## Usage guide
Depending on page layout, there are three ways to use this script:

 * When the player and widget are children of a common wrapper element, fullscreen will work perfectly.

 * Setting the wrapper setting to `body` will cause the entire page to go full-screen. This may cause elements with large z-indexes or other special elements on the page to sit above the CrowdSurfing widget, potentially requiring special handling. (class `full-screen` is added to body tag, so modification can be made targeting that class)

 * Setting the wrapper as `null` will cause the player to be moved under the widget`s parent element on enter into full screen, and moved back when fullscreen is closed. This may cause the player to stop.

## Notices

* Video player should be configured to hide the fullscreen button.

* When the page is switched to fullscreen mode, the class `full-screen` is added to the body element. This can be used for additional styling, if needed.


## Tablets
Tablets, such as the iPad, need to be kept from zooming in and out, either by "pinching" the screen, or by double clicking. By setting a meta tag with "viewport" set to "user-scalable=no", the layout of the page will be kept to the size designated by the web page.

## Example
```HTML
<!DOCTYPE html>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
    <title>CS Fullscreen Demo</title>
    <link rel="stylesheet" type="text/css" href="style.css" />
    <meta name="viewport" content="width=device-width,user-scalable=no">
</head>
<body>
    <div id="header-wrapper">
        <div id="header">
            <div class="outer-left"></div>
            <div class="outer-right"></div>
            <div class="inner-right"></div>
            <div class="inner-left"></div>
        </div>
    </div>
    <div id="fs">
        <div id="player-wrapper">
            <iframe width="100%" height="100%" src="//www.youtube.com/embed/nXGh7aVHqHo?fs=0" frameborder="0"  scrolling="no" allowtransparency="true"></iframe>
        </div>
        <div id="crowdsurfing-wrapper">
            <script id="crowdsurfing_event" src="https://s3.amazonaws.com/liveone-static/events/53882407dbc2a9af018b4567.js" type="text/javascript">({
/*
                player: 'twitch',    //player-specific, only used for Twitch player currently
*/
                wrapper: '#fs',  //css selector
                csWrapper: document.getElementById('crowdsurfing-wrapper'),  //DOM node
                playerWrapper: '#player-wrapper',
            })</script>
        </div>
    </div>
</body>
</html>
```
