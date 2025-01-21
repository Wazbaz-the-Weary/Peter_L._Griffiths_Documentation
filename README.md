# RGBADEST (and CMYKDAST)
## [Assignment 1 - Build your own binary (byob)](https://github.com/charlieroberts/imgd-5010-s24/blob/main/assignment1-binary.md)

The premise of this speculative binary programming language is to embed rendered color/texture images with additional per-pixel physically-based lighting properties, expanding onto 4x8-bit/32-bit RGBA/CMYK color with DEST/DAST, an additional 4x8-bit/32-bit spectral register: 
- D: Depth (of material until transition to next material): clear/none to opaque/black-body, 0-255(00000000-11111111)/00-ff
- E/A: Emissivity/Albedo: reflective/white to absorbant/black-body, 0-255(00000000-11111111)/00-ff
- S: Specularity: specular/glossy reflection to diffuse/scattered transmission, 0-255(00000000-11111111)/00-ff
- T: Tropism: isotropic diffusion/scattering to anisotropic diffusion/scattering, 0-255(00000000-11111111)/00-ff

  *NB: These material lighting properties are typically mapped in layers onto 3D meshes following the Pixar openUSD or Khronos glTF PBR pipelines. Expanding color space to include some of these features has been fun to think and write about, but represents fewer possible material variations than layered maps with properties of light represented in separate RGBA color-spaces.*

  *I'm not sure this impacts utility unless this format was expressly more efficient or performant, challenging as glTF and openUSD are already more theoretically capable and are being actively refined.*

Recognizing how complex an extended SDR 8x8/64-bit, 18,446,744,000,000,000,000 (18.446744 e+19/quintillion) value image format is, I'm not even going to think about representing every possible value. HDR extended to 8x12/96-bit, for simplicity (hah!) only considering 12-bit density and not 10-bit, expands the possible range of values to 7.9228163 e+28, so I'm ignoring that it exists. 

With the exception of varied brightness to simulate spectral phenomena the pixels of modern XY-plane screens can't directly emulate material physical lighting properties, and so cannot display this proposed format at native resolution and aspect ratio. Rather, by providing a light source and shifting into 3D space these material properties can be simulated, displayed, and/or observed even when projected onto a visual XY-plane. 
