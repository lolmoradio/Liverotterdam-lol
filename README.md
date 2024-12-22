<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Webcam Switcher</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
    </style>
</head>
<body>

<iframe id="videoPlayer" width="640" height="360" src="" frameborder="0" allowfullscreen></iframe>

<audio id="radioPlayer" controls autoplay>
    <source src="https://icecast.omroep.nl/radio2-bb-mp3" type="audio/mpeg">
    Your browser does not support the audio element.
</audio>

<script>
    const videoPlayer = document.getElementById('videoPlayer');
    const radioPlayer = document.getElementById('radioPlayer');
    
    const videoSources = [
        "https://www.youtube.com/embed/gsViKzj7nuQ?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/_KVWehizoNU?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/nFozEhYTEMo?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/5BfSKKTtOqM?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/M09NaBVPjAI?autoplay=1&mute=1&loop=1",
        "https://www.youtube.com/embed/qYy_7AJ4DKo?autoplay=1&mute=1&loop=1"
        https://www.youtube.com/live/1wWlJyopdN4?si=SX5RVaBbOoCKJjIK
    ];
    
    let currentSourceIndex = 0;
    
    function switchVideo() {
        currentSourceIndex = (currentSourceIndex + 1) % videoSources.length;
        videoPlayer.src = videoSources[currentSourceIndex];
    }
    
    setInterval(switchVideo, 20000); // Switch video every 20 seconds
</script>

</body>
</html>
