<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        .slider-container {
            position: relative;
            width: 100%;
            max-width: 600px;
        }
        .before-image, .after-image {
            width: 100%;
            display: block;
        }
        .after-image {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            clip: rect(0, 50%, 100%, 0);
        }
        .slider {
            position: absolute;
            top: 0;
            left: 50%;
            width: 3px;
            height: 100%;
            background: #fff;
            cursor: ew-resize;
        }
    </style>
</head>
<body>
    <div class="slider-container">
        <img src="before-image-url.jpg" alt="Before" class="before-image">
        <img src="after-image-url.jpg" alt="After" class="after-image">
        <div class="slider"></div>
    </div>
    <script>
        const slider = document.querySelector('.slider');
        const afterImage = document.querySelector('.after-image');
        const container = document.querySelector('.slider-container');
        
        function slide(event) {
            const containerRect = container.getBoundingClientRect();
            const offsetX = event.clientX - containerRect.left;
            const sliderPosition = (offsetX / containerRect.width) * 100;
            slider.style.left = `${sliderPosition}%`;
            afterImage.style.clip = `rect(0, ${sliderPosition}%, 100%, 0)`;
        }
        
        slider.addEventListener('mousedown', () => {
            window.addEventListener('mousemove', slide);
        });
        
        window.addEventListener('mouseup', () => {
            window.removeEventListener('mousemove', slide);
        });
    </script>
</body>
</html>
