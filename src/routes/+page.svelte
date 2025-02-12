<script lang="ts">
    import { onMount } from 'svelte';
    
    let lat: string, long: string, acc: string, height: number;
    const width:number = 320;
    let streaming:boolean = false;
    
    let video = null;
    let canvas = null;
    let photo = null;
    let startButton = null;
    
    const options = {
        enableHighAccuracy: true,
        timeout: 5000,
        maximumAge: 0,
    };
    
    function success(pos) {
        lat = pos.coords.latitude;
        long = pos.coords.longitude;
        acc = pos.coords.accuracy;
    }
    
    function error(err) {
        console.warn(`ERROR(${err.code}): ${err.message}`);
    }
    
    function findLoc() {
        navigator.geolocation.getCurrentPosition(success, error, options);
        document.getElementById('geo-detail').hidden = false;
    }
    
    function showViewLiveResultButton() {
        if (window.self !== window.top) {
            // Ensure that if our document is in a frame, we get the user
            // to first open it in its own tab or window. Otherwise, it
            // won't be able to request permission for camera access.
            document.querySelector(".content-area").remove();
            const button = document.createElement("button");
            button.textContent = "View live result of the example code above";
            document.body.append(button);
            button.addEventListener("click", () => window.open(location.href));
            return true;
        }
        return false;
    }
    
    function startup() {
        if (showViewLiveResultButton()) {
            return;
        }
        video = document.getElementById("video");
        canvas = document.getElementById("canvas");
        photo = document.getElementById("photo");
        startButton = document.getElementById("start-button");
        
        navigator.mediaDevices
        .getUserMedia({ video: true, audio: false })
        .then((stream) => {
            video.srcObject = stream;
            video.play();
        })
        .catch((err) => {
            console.error(`An error occurred: ${err}`);
        });
        
        video.addEventListener(
        "canplay",
        (ev) => {
            if (!streaming) {
                height = video.videoHeight / (video.videoWidth / width);
                
                // Firefox currently has a bug where the height can't be read from
                // the video, so we will make assumptions if this happens.
                
                if (isNaN(height)) {
                    height = width / (4 / 3);
                }
                
                video.setAttribute("width", width);
                video.setAttribute("height", height);
                canvas.setAttribute("width", width);
                canvas.setAttribute("height", height);
                streaming = true;
            }
        },
        false,
        );
        
        startButton.addEventListener(
        "click",
        (ev) => {
            takePicture();
            ev.preventDefault();
        },
        false,
        );
        
        clearPhoto();
    }
    
    // Fill the photo with an indication that none has been
    // captured.
    
    function clearPhoto() {
        const context = canvas.getContext("2d");
        context.fillStyle = "#AAA";
        context.fillRect(0, 0, canvas.width, canvas.height);
        
        const data = canvas.toDataURL("image/png");
        photo.setAttribute("src", data);
    }
    
    // Capture a photo by fetching the current contents of the video
    // and drawing it into a canvas, then converting that to a PNG
    // format data URL. By drawing it on an offscreen canvas and then
    // drawing that to the screen, we can change its size and/or apply
    // other changes before drawing it.
    
    function takePicture() {
        const context = canvas.getContext("2d");
        if (width && height) {
            canvas.width = width;
            canvas.height = height;
            context.drawImage(video, 0, 0, width, height);
            context.font = "bold 15pt Calibri";
            context.fillStyle = "white";
            context.fillText(`${lat} | ${long} | ${acc}`, 20, 20);
            
            const data = canvas.toDataURL("image/png");
            photo.setAttribute("src", data);
        } else {
            clearPhoto();
        }
    }
    
    onMount(() => {
        navigator.geolocation.getCurrentPosition(success, error, options);
        window.addEventListener("load", startup, false);
    })
</script>

<button onclick={findLoc}>Debug geo details</button>

<div id="geo-detail" hidden>
    <h1>Your position is: </h1>
    <span>Latitute: {lat}</span><br>
    <span>Longitude: {long}</span><br>
    <span>More or less {acc} meters</span><br>
</div>

<div class="content-area">
    <div class="camera">
        <video id="video">Video stream not available.
            <track kind="captions">
        </video>
        <button id="start-button">Take photo</button>
    </div>
    <canvas id="canvas"> </canvas>
    <div class="output">
        <img id="photo" alt="The screen capture will appear in this box." />
    </div>
</div>

<style>
    #video {
        border: 1px solid black;
        box-shadow: 2px 2px 3px black;
        width: 320px;
        height: 240px;
    }
    
    #photo {
        border: 1px solid black;
        box-shadow: 2px 2px 3px black;
        width: 320px;
        height: 240px;
    }
    
    #canvas {
        display: none;
    }
    
    .camera {
        width: 340px;
        display: inline-block;
    }
    
    .output {
        width: 340px;
        display: inline-block;
        vertical-align: top;
    }
    
    #start-button {
        display: block;
        position: relative;
        margin-left: auto;
        margin-right: auto;
        bottom: 32px;
        background-color: rgb(0 150 0 / 50%);
        border: 1px solid rgb(255 255 255 / 70%);
        box-shadow: 0px 0px 1px 2px rgb(0 0 0 / 20%);
        font-size: 14px;
        font-family: "Lucida Grande", "Arial", sans-serif;
        color: rgb(255 255 255 / 100%);
    }
    
    .content-area {
        font-size: 16px;
        font-family: "Lucida Grande", "Arial", sans-serif;
        width: 760px;
    }
</style>