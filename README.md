# A-Frame: Image Target Stickers

I made AR Pins for my friends' birthday - happy birthday Chanel & Diana!

### Make it your own

1. Create a design or logo digitally.
2. Upload the design as an image target.
3. Create a transparent version of the design.

![transparent image target design](./src/assets/transparent.png)

4. Use the transparent image as a texture on `<a-plane>`.

```

```

5. Animate the plane's rotation, apply a holographic shader.

```
<script src="https://unpkg.com/aframe-hologram-shader"></script>
```

```
<xrextras-named-image-target name="image">
  <!-- black circle to cover up the real pin -->
  <a-circle color="black" radius="0.46"></a-circle>

  <!-- transparent design -->
  <a-plane src="#img"
    material="transparent: true; shader: hologram; numGlitchBars: 20"
    position="0 0 0.5"
    animation__spin="property: rotation; from: 0 0 0; to: 0 0 360; loop: true; easing: linear; dur: 10000"
  ></a-plane>
</xrextras-named-image-target>
```

### Try the experience yourself

![image target design](./src/assets/demo.png)

## What I learned

- pins should be matte, the reflections caused issues with tracking
- use black on white, the contrast of the green was not enough
- "it worked once and that was enough"

---

### Your Exported Project
This zip contains your project source code, assets, image targets, and configuration needed to build and publish your 8th Wall project. It does not connect to any 8th Wall services, so will work even after the 8th Wall servers are shut down.

### Setup
If node/npm are not installed, install using https://github.com/nvm-sh/nvm or https://nodejs.org/en/download.

Run `npm install` in this folder.

### Development
Run `npm run serve` to run the development server.

#### Testing on Mobile
To test your project on mobile devices, especially for AR experiences that require camera access, you'll need to serve your development server over HTTPS. We recommend using [ngrok](https://ngrok.com/) to create a secure tunnel to your local server. After setting up ngrok, add the following configuration to `config/webpack.config.js` under the `devServer` section:

```javascript
devServer: {
  // ... existing config
  allowedHosts: ['.ngrok-free.dev']
}
```

### Publishing
Run `npm run build` to generate a production build. The resulting build will be in `dist/`. You can host this bundle on any web server you want.

### Project Overview
- `src/`: Contains all your original project code and assets.
    - References to asset bundles will need to be updated. Asset bundles are now plain folders. For example,
      - GLTF bundles need to be updated to the `.gltf` file in the folder, i.e., if your model is at `assets/mymodel.gltf/`, update your code to reference `assets/mymodel.gltf/mymodel_file.gltf`.
- `image-targets/`: Contains your project's image targets (if any).
  - The image target with the `_target` suffix is the image target loaded by the engine. The others are used for various display purposes, but are exported for your convenience.
  - To enable image targets, call this in `app.js` or `app.ts` file. (Note: `app.js` or `app.ts` may not be created by default; you will need to create this file yourself.) The autoload targets will have a `"loadAutomatically": true` property in their json file.
```javascript
const onxrloaded = () => {
  XR8.XrController.configure({
    imageTargetData: [
      require('../image-targets/target1.json'),
      require('../image-targets/target2.json'),
    ],
  })
}
window.XR8 ? onxrloaded() : window.addEventListener('xrloaded', onxrloaded)
```
- `config/`: Contains the necessary webpack configuration and typescript definitions to support project development.
- `external/`: Contains dependencies used by your project, loaded in `index.html`.
  - If you are not using the XR Engine, you can remove the xr.js script tag from `index.html` and delete the `external/xr/` folder to save bandwidth.
  - You can also customize whether `face`, `slam`, or both, are loaded on the `data-preload-chunks` attribute.

### Final Notes
Please reach out to support@8thwall.com with any questions not yet answered in the docs. Thank you for being part of 8th Wall's story!