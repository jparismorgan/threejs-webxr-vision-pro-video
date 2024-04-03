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

https://github.com/jparismorgan/threejs-webxr-vision-pro-video/assets/1396242/745be62e-0fa9-4417-bbf4-1a1ae8d97c62

### Context
This code was copied from https://threejs.org/examples/?q=webxr#webxr_vr_video / https://github.com/mrdoob/three.js/blob/master/examples/webxr_vr_video.html

The only change I made was https://github.com/jparismorgan/threejs-webxr-vision-pro-video/blob/main/index.html#L113-L123, which will try to play the video when the session starts:
```
renderer.xr.addEventListener('sessionstart', () => {
                    console.log('[index@sessionStart] video.paused:', video.paused);

                    const handlePaused = () => {
                        console.log('[index@sessionStart@handlePaused] video.paused:', video.paused);
                        video.removeEventListener("pause", handlePaused);
                        video.play();
                        console.log('[index@sessionStart@handlePaused] after we called play() video.paused:', video.paused);
                    };
                    video.addEventListener("pause", handlePaused);
                })
```
I can see it is hit and plays the video, but it doesn't show as playing.
