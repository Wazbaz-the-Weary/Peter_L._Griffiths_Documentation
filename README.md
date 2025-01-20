# RGBADEST, or Colorfuller
## [Assignment 1 - Build your own binary (byob)](https://github.com/charlieroberts/imgd-5010-s24/blob/main/assignment1-binary.md)

The premise of this speculative binary programming language is to embed rendered color/texture images with additional per-pixel physically-based lighting properties, expanding onto 4x8-bit RGBA color with DEST, an additional 4x8-bit bit spectral register: 
- D: Depth (of material until transition to next material) (none/clear to opaque),
- E: Emissivity (reflective to black-body), 
- S: Specularity (specular/glossy reflection/transmission to diffuse/scattered reflection/transmission), and
- T: Tropism (isotropic scattering to anisotropic scattering). 

Recognizing how uneccessarily complex a 64-bit SDR
