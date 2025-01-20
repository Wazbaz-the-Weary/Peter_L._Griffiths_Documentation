# Peter_L._Griffiths_Documentation
## [Assignment 1 - Build your own binary (byob)](https://github.com/charlieroberts/imgd-5010-s24/blob/main/assignment1-binary.md)

The premise of this speculative binary programming language is to embed a texture image with per-pixel physically-based lighting properties, expanding onto 8-bit SDR 256^4 bit RGBA with DEST, an additional 256^4 bit spectral register: 
- D: Depth (of material until transition to next material) (none/clear to opaque).
- E: Emissivity (reflective to black-body), 
- S: Specularity (specular/glossy reflection/transmission to diffuse/scattered reflection/transmission), and
- T: Tropism (isotropic scattering to anisotropic scattering), 
