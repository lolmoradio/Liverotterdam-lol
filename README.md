<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fullscreen Video Player</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: black;
            color: white;
        }
        iframe {
            border: none;
            width: 100%;
            height: 60%;
            max-width: 1200px;
        }
        .controls {
            display: flex;
            gap: 10px;
            margin-top: 20px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            border-radius: 5px;
            background-color: #007bff;
            color: white;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

<iframe id="videoPlayer" src="" allowfullscreen></iframe>

<div class="controls">
    <button id="fullscreenButton">Fullscreen</button>
    <button id="skipButton">Skip Video</button>
    <button id="radioToggleButton">Radio Uit</button>
</div>

<audio id="radioPlayer">
    <source src="https://icecast.omroep.nl/radio2-bb-mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>

<script>
    const videoPlayer = document.getElementById('videoPlayer');
    const skipButton = document.getElementById('skipButton');
    const fullscreenButton = document.getElementById('fullscreenButton');
    const radioPlayer = document.getElementById('radioPlayer');
    const radioToggleButton = document.getElementById('radioToggleButton');

    const videoSources = [
        "https://www.youtube.com/embed/gsViKzj7nuQ?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/_KVWehizoNU?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/nFozEhYTEMo?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/5BfSKKTtOqM?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/M09NaBVPjAI?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/qYy_7AJ4DKo?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/1wWlJyopdN4?autoplay=1&mute=1&loop=1"
    ];

    let currentSourceIndex = 0;

    // Load the first video
    videoPlayer.src = videoSources[currentSourceIndex];

    // Function to switch to the next video
    function switchVideo() {
        currentSourceIndex = (currentSourceIndex + 1) % videoSources.length;
        videoPlayer.src = videoSources[currentSourceIndex];
    }

    // Event listener for skip button
    skipButton.addEventListener('click', switchVideo);

    // Automatically switch videos every 20 seconds
    setInterval(switchVideo, 20000);

    // Fullscreen functionality
    fullscreenButton.addEventListener('click', () => {
        if (videoPlayer.requestFullscreen) {
            videoPlayer.requestFullscreen();
        } else if (videoPlayer.webkitRequestFullscreen) { // For Safari
            videoPlayer.webkitRequestFullscreen();
        } else if (videoPlayer.msRequestFullscreen) { // For IE/Edge
            videoPlayer.msRequestFullscreen();
        } else {
            alert('Fullscreen is not supported by your browser.');
        }
    });

    // Radio on/off toggle functionality
    radioToggleButton.addEventListener('click', () => {
        if (radioPlayer.paused) {
            radioPlayer.play();
            radioToggleButton.textContent = "Radio Aan";
        } else {
            radioPlayer.pause();
            radioToggleButton.textContent = "Radio Uit";
        }
    });

    // Attempt to play the radio when the page loads
    radioPlayer.play().catch(() => {
        console.log("Autoplay blocked, user interaction required to play the radio.");
    });
</script>

</body>
</html>


