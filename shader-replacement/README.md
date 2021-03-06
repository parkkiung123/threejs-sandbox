
# Shader Replacement

![](./docs/image.png)

Utility for rendering a scene with a replacement shader. Similar to `Scene.overrideMaterial` but the uniforms of the original material uniforms are maintained.

[Demo Here](https://gkjohnson.github.io/threejs-sandbox/shader-replacement/)

# Use

```js
import { ShaderReplacement } from './src/ShaderReplacement.js';

// ...

const shader = ShaderLib.normal;
shader.defines.USE_NORMALMAP = '';
shader.defines.TANGENTSPACE_NORMALMAP = '';
shader.defines.USE_UV = '';

const shaderReplacement = new ShaderReplacement( ShaderLib.normal );
shaderReplacement.reploace( scene, true );
renderer.render( scene, camera );
shaderReplacement.reset( scene, true );
```

# API

## ShaderReplacement

### .constructor

```js
constructor( shader : Shader )
```

Takes the shader to use on all materials when rendering the scene.

### .replace

```js
replace(
	scene : Scene | Array< Object3D >,
	recursive = false : Boolean,
	cacheMaterial = true : Boolean
) : void
```

Replaces the material on all objects in the given scene. Recurses to all children if `recursive` is true. If `cacheMaterial` is true then all current materials are saved so they can be replaced on [reset](#reset).

### .reset

```js
reset(
	scene : Scene | Array< Object3D >,
	recursive = false : Boolean
) : void
```

Resets all materials to the originally cached one. Recurses to all children if `recursive` is true.

### updateUniforms

_overrideable_

```js
updateUniforms( object : Object3D, material : Material, target : ShaderMaterial ) : void
```

Overrideable function intended to update the uniforms on the `target` material to match those on `material` for the given `object`. This can be overriden if special defines need to be set for a given material such as `USE_NORMALMAP` for a normal shader. 
