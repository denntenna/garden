---
title: shaders
tags:
  - cheatsheet
---

# Shaders

## Mental Model

Shader is a function that takes position of a pixel (amongst other inputs) and returns the color of that pixel.

You have mathematical functions to emulate imperative programming. for instance, think of `step` function as a comparator that compares two inputs. Very much like an if condition. It returns a 0 or 1 (like the if condition). You can use `smoothstep`, if instead of a boolean you want a smooth transition between 0 and 1.

## glslviewer

This is the best way to work on shaders because it provides you with almost a live coding environment for making shaders.

Lets say you are working on a fragment shader and need to work with a texture, run glslviewer with `../build/glslViewer shader.frag texture.png`. This will open up a window where the shader can be previewed. Now, you can also open up shader.frag in a text editor. As you make changes to it, glsviewer live-reloads the new shader and you get instantaneous previews.

## Simple Shaders

### Slide between two images with mouse

```glsl
#version 100

#ifdef GL_ES
precision mediump float;
#endif

uniform sampler2D   u_tex0;
uniform sampler2D   u_tex1;

uniform vec2        u_mouse;
uniform vec2        u_resolution;
uniform float       u_time;

void main (void) {
    vec3 color = vec3(0.0);
    vec3 color2 = vec3(0.0);
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec2 mn = u_mouse/u_resolution;

    color = texture2D(u_tex1, st).rgb;
    color2 = texture2D(u_tex0, st).rgb;

    float scale = step(mn.x, st.x);

    gl_FragColor = vec4(color*scale+color2*(1.0-scale), 1.0);
}
```

### Circular Mask

```glsl
#version 100

#ifdef GL_ES
precision mediump float;
#endif

uniform sampler2D   u_tex0;
uniform sampler2D   u_tex1;

uniform vec2        u_mouse;
uniform vec2        u_resolution;
uniform float       u_time;

float circle(in vec2 _st, vec2 _mn, in float _radius){
    vec2 dist = _st-_mn;
	return 1.-smoothstep(_radius-(_radius*0.01),
                         _radius+(_radius*0.01),
                         dot(dist,dist)*4.0);
}

void main (void) {
    vec3 color = vec3(0.0);
    vec3 color2 = vec3(0.0);
    vec2 st = gl_FragCoord.xy/u_resolution.xy;
    vec2 mn = u_mouse/u_resolution;

    color2 = texture2D(u_tex1, st).rgb;
    color = texture2D(u_tex0, st).rgb;

    vec3 scale = vec3(circle(st,mn, 0.05));

    gl_FragColor = vec4(color*scale+color2*(1.0-scale), 1.0);

}
```
