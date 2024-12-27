# Integration using iFrame 

```html
   <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Iframe Communication Example</title>
    </head>
    <body>
        <iframe
            id="myIframe"
            src="https://video.streamplay.dev"
            width="100%"
            height="100%"
            allow="camera; microphone; clipboard-write; clipboard-read; compute-pressure; geolocation; display-capture"
        ></iframe>
        <script>
            const username = "put your username here" //replace this string with your username
            const baseUrl = 'https://video.streamplay.dev';
            const width = window.innerWidth;
            const height = window.innerHeight;
            const url = encodeURIComponent(window.location.href)
            const dynamicSrc = `${baseUrl}${window.location.pathname}?username=${encodeURIComponent(username)}&width=${width}&height=${height}&url=${url}`;
            const iframe = document.getElementById('video');
            iframe.src = dynamicSrc;
        </script>
    </body>
    </html>
   ```

## Url mapping
In our integration, you need to map our URLs so that multiple players can play their own games and have conversions on the same time.

For example, Player A is playing Game 1 and has created Room 1. Player A shares this link http://your_domain/streamplay/game1/room1?player1 with Player B. Player B opens the link and is redirected to the main page http://your_domain/streamplay/room1 Then, Player B chooses Game 2 and goes to http://your_domain/streamplay/game2/room1?player2

## Additional Info

For any questions or support, please contact us at:

- **Email:** tech@streamplay.dev

Feel free to reach out for any inquiries or feedback regarding the iframeCommunication library!
***
***
***
***
***

# Section below is deprecated

# Iframe Communication Example

This project demonstrates how to use the `iframeCommunication` library for seamless communication between your main application and iframes using vanilla JavaScript.

## Overview

The `iframeCommunication` library allows for easy communication between your main application and iframes. This README provides instructions on how to include and use the library in a vanilla JavaScript application using both npm and a script tag.

## Installation Methods

### Method 1: Using npm

1. **Install the Library**

   ```bash
   npm install @streamplay-dev/iframecommunication
   ```
   
2. **Use the Library in Your JavaScript File**   
   
   ```javascript
    import IframeCommunication from '@streamplay-dev/iframecommunication';

    document.addEventListener('DOMContentLoaded', () => {
       const url = 'https://video.streamplay.dev"';
       const iframe = document.getElementById('myIframe');
       const iframeCommunication = new IframeCommunication('#myIframe', `${url}${window.location.pathname}`, username);
       iframeCommunication.init();

       // Cleanup on window unload
       window.addEventListener('unload', () => {
          iframeCommunication.cleanup();
       });
    });
   ```

### Method 2: Using a Script Tag

1. **Add the Script Tag to Your HTML**
   ```html
    <script src="https://unpkg.com/@streamplay-dev/iframecommunication@0.9.0/dist/iframeCommunication.min.js"></script>
   ```
   
   ```html
   <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Iframe Communication Example</title>
        <script src="https://unpkg.com/@streamplay-dev/iframecommunication@0.9.0/dist/iframeCommunication.min.js"></script>
    </head>
    <body>
        <iframe
            id="myIframe"
            src="https://video.streamplay.dev"
            width="100%"
            height="100%"
            allow="camera; microphone; clipboard-write; clipboard-read; compute-pressure; geolocation"
        ></iframe>
        <script>
            document.addEventListener('DOMContentLoaded', () => {
                const username = "put your username here" //replace this string with your username
                const url = 'https://video.streamplay.dev"';
                const dynamicSrc = `${url}${window.location.pathname}`;
                const iframe = document.getElementById('myIframe');
                iframe.src = dynamicSrc;
    
                iframe.onload = () => {
                    const iframeCommunication = new IframeCommunication('#myIframe', dynamicSrc, username);
                    iframeCommunication.init();
                };
            });
        </script>
    </body>
    </html>
   ```
   
### Example how to toggle video chat
```html
   <head>
      <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
      <style>
         #mainContainer {
            width: 80%;
            height: 100%;
            transition: width 0.3s;
            position: relative;
         }
         #toggleButton {
            position: absolute;
            top: 10px;
            right: 20px;
            z-index: 1000;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 24px;
            color: white;
         }
      </style>
      <script src="https://unpkg.com/@streamplay-dev/iframecommunication@0.9.0/dist/iframeCommunication.min.js"></script>
   </head>
    <body>
       <button id="toggleButton"><i class="fas fa-bars"></i></button>
       <div id="mainContainer">
          ...
       </div>
    </body>
```
`javascript`

```javascript
   const mainContainer = document.getElementById('mainContainer');
   const toggleButton = document.getElementById('toggleButton');
   toggleButton.addEventListener('click', () => {
      iframe.classList.toggle('collapsed');
   
      if (iframe.classList.contains('collapsed')) {
         mainContainer.style.width = '100%';
   
      } else {
         mainContainer.style.width = '80%';
      }
   });
```
   
