# Peter_L._Griffiths_Documentation
## [Assignment 1 - Build your own binary (byob)](https://github.com/charlieroberts/imgd-5010-s24/blob/main/assignment1-binary.md)

The premise of this speculative binary programming language is to render a texture image with per-pixel physically-based properties, expanding onto 8-bit SDR 4*256 bit RGBA with spectral material data: 
- E:Emissivity/Albedo (reflective to black-body), 
- S:Specularity (specular/glossy reflection/transmission to diffuse/scattered reflection/transmission), 
- T:Tropism (isotropic scattering to anisotropic scattering), and 
- D:Depth (until transition to next material) (none/clear to infinite/black-body).

