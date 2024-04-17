# Mimic several weather/natural phenomena in Genshin Impact through shaders

## Team Members: Nothern, Jaxon Zeng, Kingsley Situ, Mengjun Wen

Vedio && Slides: https://drive.google.com/drive/folders/1Uk5cjVnPMUhYInYM2YtSKTEXuUUhH2s_?usp=drive_link

For this milestone, we’ve done a lot of work and made great progress on the final project. From our final project team formed to the date of the milestone, we had several meetings and decided that the goal of our project was to mimic several weather/natural phenomena in Genshin Impact including fog, lunar eclipse/blood moon, lighting, and perhaps raining or thunderstorm.

We found a great tool called Genshin Stella Mod. This tool can provide a platform to implement custom shaders. It embedded the ReShade post-processing injector for Genshin Impact which uses a custom shader language called ReShade FX.

## The Fog

### Completed
The first effect achieved is fog. Our algorithm mixes the fog color with the original color based on the pixel's depth. The further the pixel, the greater the intensity of the fog color in the mix. We have created a user interface control to adjust the properties of the fog, such as the starting and ending distances of the fog boundaries, and the intensity and density curve of the fog.

### Preliminary Results
We now have a good framework to simulate the effect of fog and can control it within the game's UI interface. It performs well during the day. However, the fog effect does not perform well at night or early morning. The color of the fog at night should be darker and denser. Although the fog can be adjusted, it defaults to white, which does not match other environmental settings.

### Reflect on Progress
We have segmented the simulation process of environmental fog, first implementing the fog at night and then the transition from day to night. However, since ReShade is a post-processing graphics tool and cannot access game time, we will implement time change detection based on environmental brightness detection. To further achieve a realistic fog effect, we also hope to mimic the diffusion effect of night light sources. We want the light sources to appear blurry and diffused in the fog. There are several things to do here. First, implement light source detection. Then, adjust the brightness effects of the night light sources and the environment. Next, I will add blurriness to the light around the light sources to mimic the glowing effect in the fog. Finally, we also hope to add a smooth transition for the fog from day to night.

## The Lunar Eclipse

### Completed
A sampler was created, and uniform variables for position, size, opacity, and depth range were defined. The moon's texture coordinates were then calculated based on screen position and aspect ratio, and the sun was blended with the original image using depth testing and user-specified parameters. Additionally, the depth value of each pixel was retrieved, and the moon's depth was calculated using the adjustable z-value of the moon's position. By comparing the pixel's depth with the moon's depth range, the shader determines whether the moon should be visible or hidden for objects at different distances.

To simulate a lunar eclipse using bloom and color inversion, a bloom mask was first generated based on the moon's alpha value and a color threshold, which was then used to intensify the moon's glow. Next, the shader applied color inversion to the moon using adjustable parameters, allowing the user to gradually darken the moon until it appeared completely black, thus mimicking the appearance of a lunar eclipse. The halo should become more pronounced as the eclipse progresses.

### Preliminary Results
The moon texture was loaded, and the occlusion effect of closer objects on the moon was rendered. The color inversion process for the moon was implemented.

### Reflect on Progress
We aim to use a mask to simulate the process of the moon gradually being covered up. Moreover, a spectacle like a lunar eclipse will undoubtedly impact the overall scene; thus, how to achieve brightness and color adjustment in the game is our next step.
