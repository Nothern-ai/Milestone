# Project Goal: Mimic several weather/natural phenomena in Genshin Impact through shaders

## Team Members: Nothern, Jaxon Zeng, Kingsley Situ, Mengjun Wen

### Implement the daytime fog
- Fog algorithm (depth based)
- Different color mixed
- Add parameters for fog start and end distance
- Defined fog intensity parameter and fog density curve

### Implement the nighttime fog
- Defined the nighttime fog effect
- Tuned the parameters for nighttime fog
- Implemented the environment illumination detection
- Nighttime light source effect: we want to mimic the nighttime light source diffusion effect in real life in the game fog effect

### Add day-to-night shift
- Implement the light source detection
- Adjust the light source luminance
- Adjust the environment lighting effect
- Add light diffusion around the light source to mimic the glowing effect
- Add moon texture into the game
- Allow fine-tuning of sun position, size, opacity, and depth range
- Enable real-time preview of sun effect changes
- Enhance the moon's visual appearance
- Implement moon color inversion effect
- Add a bloom effect around the sun to simulate glowing
- Bind bloom intensity and color inversion to simulate a lunar eclipse in terms of light effects

### Implement color filters for the whole picture
- Bind the color gradient process to the moon change
- Dimming of light under lunar eclipse
- The red atmosphere under a blood moon

For this milestone, we’ve done a lot of work and made great progress on the final project. From our final project team formed to the date of the milestone, we had several meetings and decided that the goal of our project was to mimic several weather/natural phenomena in Genshin Impact including fog, lunar eclipse/blood moon, lighting, and perhaps raining or thunderstorm.

We first luckily found a great tool called Genshin Stella Mod. This tool can provide a platform to implement custom shaders. It embedded the ReShade post-processing injector for Genshin Impact which uses a custom shader language called ReShade FX.

The first type of effect we decided to implement was fog. After researching several fog effect implementations, we decided to create a depth-based fog shader. This algorithm will blend the color of the fog with the original color based on the depth of that pixel. The further the pixel, the intenser the fog color in the blending. After having the algorithm working, we decided to have more control over the fog. So we first created a UI control to control different fog colors. When we are running the game, we can change the fog color on the flight. Moreover, we also added the controls for the fog start and end distance based on the depth. Furthermore, fog intensity and fog density curve were also added to give further control to the fog. Based on that, we have a great framework to control the fog effect.

When we changed the time to the night, we found out that the fog effect that satisfied us during the daytime behaved horribly during the night. The nighttime fog color should be much deeper while the fog could be denser. So we first defined the nighttime fog effect and tuned the parameters to achieve this effect. We also wanted to create a shift of the fog effect from daytime to nighttime but we found out that we could not access the game time since ReShade is a post-processing graphic tool. So we implemented the day-to-night detection based on the environment luminance detection.

For the next step to further achieve a realistic fog effect, we also want to mimic the nighttime light source diffusion effect. We want the light source to look glowing in the fog. So here are several things we can do. First, we can implement the light source detection. Then we adjust the luminance effect of the light source and the environment during the nighttime. Then we can add the light diffusion around the light source to intimate the glowing effect. At last, we also want to add a smooth shift for the fog from the daytime to the nighttime.

When it comes to the moon, to put the moon texture into the game and make it adjustable, we load the moon texture, create a sampler, define uniform variables for position, size, opacity, and depth range, calculate the moon's texture coordinates based on screen position and aspect ratio, and blends the sun with the original image using depth testing and user-specified parameters. To control the depth and hide the moon based on the distance from the player, we retrieve the depth value of each pixel and then calculate the moon's depth using the adjustable z value of the moon's position. By comparing the pixel's depth with the moon's depth range, the shader determines whether the moon should be visible or hidden for objects at different distances from the player. For example, if there is a mountain in the player's immediate vicinity, this mountain will block the entire moon.

To simulate a lunar eclipse using bloom and color inversion, we first apply a bloom effect around the moon by generating a bloom mask based on the moon's alpha value and a color threshold. The bloom mask is then used to intensify the moon's glow. Next, the shader applies color inversion to the moon using the adjustable parameter, allowing the user to gradually darken the moon until it appears completely black, mimicking the appearance of a lunar eclipse. The halo should become more pronounced as the eclipse progresses.

So far, we have only implemented the color inversion process of the moon, we would like to use a mask to simulate the process of the moon slowly being covered up. In addition, the lunar eclipse will inevitably have an impact on the overall picture, how to achieve the brightness and color regulation of the game is also our next step.
