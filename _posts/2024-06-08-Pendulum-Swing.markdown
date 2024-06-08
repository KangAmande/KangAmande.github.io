---
layout: post
title:  "2024-06-08 - Creating Pendulum Swing"
date:   2024-06-08 00:00:00 -0400
---

- Pendulum swing is mainly affected by the length of bob and angle of the pendulum swing origin.

- TransformOrigin CSS property can be used to set up a part of the pendulum to be fixed at one spot. If TransformOrigin is set to top, the top of the pendulum is fixed and the rest of the body will move. This means that when the pendulum is rotated, it will rotate around the top.
```javascript
pendulum.style.transformOrigin = "top";
```

- Transition CSS property helps in setting up the pendulum's fixed motion. This means that when the transform property is changed, instead of the change happening instantly, it will smoothly transition over 1 second.
```javascript
pendulum.style.transition = "transform 1s";
```

- Transform property helps in setting the rotation angle of the pendulum. This also rotates it based transformOrigin and transition properties setup in there.
```javascript
pendulum.style.transform = `rotate(${angle}deg)`;
setTimeout(function() {
    pendulum.style.transform = `rotate(${-angle}deg)`;
}, interval/2);
angle -= 10;
```

- I was able to implement the two swings of the pendulum by using angle and -angle rotations. But then I had to look into building multiple swings up until the pendulum comes to a stopping point. I tried muliple setTimeout functions one after the other but since they all had same multi seconds value, they ran at once and the simulation could not be built. Then tried setInterval but this function would swing the bob only once. Hence, I used a combination of setInterval and setTimeout which would lead perfect flow of the swings. The clearInterval can be used to clear stop the swinging.
```javascript
var swingInterval = setInterval(function() {
        pendulum.style.transform = `rotate(${angle}deg)`;
        setTimeout(function() {
            pendulum.style.transform = `rotate(${-angle}deg)`;
        }, interval/2);
        angle -= 10;
        if (angle <= 0) {
            clearInterval(swingInterval);
        }
    }, interval);
```