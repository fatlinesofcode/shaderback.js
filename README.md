# shaderback
Shader-generated backgrounds for the Web.

Shaderback is a really simple javascript library that allows animated backgrounds to be added to HTML5 Web pages. The backgrounds are generated using shaders, and should work on any WebGL compatible device with a suitably powerful GPU.

## Examples

I'm still working on some examples, so there isn't much to see yet. However, there is a live example at http://www.flypig.co.uk/?style=14

## Usage

Simply add the following code inside the header of the webpage you want the background on.

```JavaScript
<script type="text/javascript" src="shaderback.js"></script>
<script type="text/javascript">
window.onload = shaderback_loadURL("shader.txt");
</script>
```
Where `shader.txt` is the URL of the fragment shader file on your webserver.

Alternatively, you can include the shader code in a script element on your page, and tell shaderback to use this instead by passing the ID of the script:

```JavaScript
<script id="shader-id" type="x-shader/x-fragment">
	precision highp float;

	varying vec2 vTextureCoord;
	uniform float time;
	uniform float width;
	uniform float height;

	void main(void) {
		// The actual shader code goes here
		// See the example folder for some examples 
		float line = (width * (0.5 - vTextureCoord.s)) * sin(0.8 + (time / 30000.0));
		line -= (height * (0.5 - vTextureCoord.t)) * cos(0.8 + (time / 30000.0));
		float cycle = (1.0 + sin(line)) / 2.0;

		vec4 colour = (cycle * vec4(0.6, 0.6, 0.6, 1.0)) + ((1.0 - cycle) * vec4(0.9, 0.9, 0.9, 1.0));
		gl_FragColor = colour;
	}
</script>

<script type="text/javascript" src="shaderback.js"></script>
<script type="text/javascript">
window.onload = shaderback_loaddiv("shader-id");
</script>
```
In this second case `shader-id` is the element ID of the script tag containing the fragment shader code.

Finally, if you have your shader code stored as a string, you can use:

```JavaScript
<script type="text/javascript" src="shaderback.js"></script>
<script type="text/javascript">
window.onload = shaderback_loadtext(text);
</script>
```
Where `text` is a string containing the fragment shader code.


## Compatibility
It's been tested on the following browsers, and seems to work fine on all of them:

1. Firefox 36.01 under Linux and Windows
1. Chrome 41.something on Windows
1. Chromium 41.something on Linux
1. IE 11 on Windows
1. Jolla Sailfish browser 1.0 (Mozilla based) 
1. Android 4.4.2 Chrome 40.something

However, it's only been tested in pretty limited circumstances (only on a few Web pages), so don't expect too much of it.

## Licence

Dandelion is released under an MIT License. See the LICENSE file for the full details.

## Contact and Links

More information will eventually be added to: http://www.flypig.co.uk/?to=shaderback

The source code can be obtained from GitHub: https://github.com/llewelld/shaderback.git

I can be contacted via one of the following.

 * Website: http://www.flypig.co.uk
 * Email: david@flypig.co.uk

