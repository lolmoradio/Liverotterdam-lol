<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Webcam Switcher</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: black;
            color: white;
        }
        iframe {
            border: none;
            width: 80%;
            height: 50%;
        }
        button {
            margin-top: 10px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<iframe id="videoPlayer" src=""></iframe>

<audio id="radioPlayer" controls>
    <source src="https://icecast.omroep.nl/radio2-bb-mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>

<div>
    <button id="skipButton">Skip Video</button>
    <button id="playRadioButton">Play Radio</button>
</div>

<script>
    const videoPlayer = document.getElementById('videoPlayer');
    const radioPlayer = document.getElementById('radioPlayer');
    const skipButton = document.getElementById('skipButton');
    const playRadioButton = document.getElementById('playRadioButton');

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

    // Play the first video on load
    videoPlayer.src = videoSources[currentSourceIndex];

    // Function to switch to the next video
    function switchVideo() {
        currentSourceIndex = (currentSourceIndex + 1) % videoSources.length;
        videoPlayer.src = videoSources[currentSourceIndex];
    }

    // Add event listener to skip button
    skipButton.addEventListener('click', switchVideo);

    // Automatically switch videos every 20 seconds
    setInterval(switchVideo, 20000);

    // Ensure radio can be played
    playRadioButton.addEventListener('click', () => {
        if (radioPlayer.paused) {
            radioPlayer.play();
        } else {
            radioPlayer.pause();
        }
    });

    // Attempt to play the radio when the page loads
    radioPlayer.play().catch(() => {
        console.log("Autoplay blocked, user interaction required to play the radio.");
    });
</script>

</body>
</html>

