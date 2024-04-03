### What
This is a repro of a bug where on Vision Pro using three.js and WebXR, a video element will be paused when you enter the immersive session. It's also discussed here: https://discourse.threejs.org/t/videotexture-playback-html5-videoelement-apple-vision-pro-simulator-in-vr-mode-not-playing/53374

### How to run
- Clone the repo
- Run `npm install`
- Run `npm run dev`
- Find the URL the server is available, i.e. `http://127.0.0.1:8080`
- Open up the Vision Pro and enable the WebXR feature flags
- Open Safari on Vision Pro and paste it in
- See that the video plays normally
- Click the "Enter VR" button
- See that the video will be paused

Here is what the bug looks like:

![repro](repro.mp4)