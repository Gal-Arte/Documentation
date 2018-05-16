---
PG_TITLE: Reduce memory footprint
---

# How To reduce memory footprint

Babylon.js offers multiple options to reduce the memory usage of a scene:

## Turning off IndexedDB

By default, all assets are saved in the local indexedDB to reduce network calls when loading multiple time the same files.
This feature uses memory so you can turn it off at engine level with:

```
 engine.enableOfflineSupport = false;
```

## Turning off support for context lost / contest restore

Babylon.js will automatically recreate everything in a transparent way if the [WebGL context is lost](http://doc.babylonjs.com/how_to/optimizing_your_scene#handling-webgl-context-lost).
While being handy, this feature consumes a lot of memory so you may want to turn if off when creating the engine with:

```
var engine = new BABYLON.Engine(canvas, true, {doNotHandleContextLost: true});
```

You can also turn it off after engine creation (but before creating any resources) with:

```
engine.doNotHandleContextLost = true;
```

## Removing cached vertex data

All vertex buffers keep a copy of their data on CPU memory to support collisions, picking, geometry edition or physics.
If you don't need to use these features, you can call this function to free associated memory:

```
scene.clearCachedVertexData();
```

You can find a demo [here](https://www.babylonjs-playground.com/#AS54U8)