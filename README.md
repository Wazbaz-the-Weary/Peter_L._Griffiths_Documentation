# RGBADEST (and CMYKDAST)
## [Assignment 1 - Build your own binary (byob)](https://github.com/charlieroberts/imgd-5010-s24/blob/main/assignment1-binary.md)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The premise of this speculative binary programming thingy is to embed color/texture images with additional per-texel physically-based lighting properties, expanding onto 4x8-bit/32-bit RGBA/CMYK color with DEST/DAST, an additional 4x8-bit/32-bit spectral register: 
- D: Depth (of material or until transition to next material): opaque/black-body to transparent
- E/A: Emissivity/Albedo: absorbant/black-body to reflective/white
- S: Specularity: diffuse/scattered reflection and transmission to specular/glossy reflection and transmission
- T: Tropism: isotropic diffusion/scattering to anisotropic diffusion/scattering
  
*NB: These material lighting properties are typically mapped in layers onto 3D meshes following the Pixar openUSD or Khronos glTF PBR pipelines. Expanding color space to include some of these features has been fun to think and write about, but represents fewer possible material variations than layered maps with properties of light represented in separate RGBA color-spaces.*

*I'm not sure this impacts utility unless this format was expressly more efficient or performant, challenging as glTF and openUSD are already more theoretically capable and are being actively refined.*

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Recognizing how complex an extended SDR 8x8/64-bit, 18,446,744,000,000,000,000 (18.446744 e+19/quintillion) value image format is, I'm not even going to think about representing every possible value. HDR extended to 8x12/96-bit, for simplicity (hah!) only considering 12-bit density and not 10-bit, expands the range of values to 7.9228163 e+28, so I'm ignoring that it exists. 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;With the exception of varied brightness to simulate spectral phenomena in increasingly granular LCD backlighting zones or the individually addressable LED sub-pixels of more modern displays, XY-plane screens can't directly emulate physical lighting properties, and so cannot display this proposed format at native resolution and aspect ratio. Rather, by directing a light source and shifting off-axis into 3-space these material properties can be simulated, displayed, and/or observed projected onto a visual XY-plane. 

### Step 1

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For this exercise I've created a rough 4x4 texel demonstration, (re)photographed 3 times using the sun for light instead of a lamp for better contrast to amalgamate RGB values. Only the 2 glass texels display transparency, so I've not included it in this; all others retain a value of 255/opaque.
  
*NB: The glass in the photos is shown as close to the color of the surface below it, for accuracy I should have taken a photo of the surface under the demo and used the difference in values. I'm leaving the wood-color values from the photos in place, but note that these soda-glass slides are just a little green and should be assumed to approach a color value of (167,199,203) as Alpha increases*

Top-down:
![Top-Down](https://github.com/Wazbaz-the-Weary/Peter_L._Griffiths_Documentation/blob/main/PXL_20250121_190302056.RAW-01.COVER.jpg?raw=true)

| RGB(A ignored) |             |             |             | Top-Down    |
|----------------|-------------|-------------|-------------|-------------|
| Metallic       | 156,144,133 | 178,174,169 | 180,175,172 | 229,230,232 |
| Oak Veneer     | 188,129,82  | 187,141,121 | 192,121,80  | 221,178,148 |
| Fabric         | 14,12,17    | 15,13,16    | 29,28,24    | 38,36,37    |
| Glass vs Paper | 38,36,37    | 61,47,43    | 200,200,200 | 205,205,205 |

Tilted camera:
![Tilted Camera](https://github.com/Wazbaz-the-Weary/Peter_L._Griffiths_Documentation/blob/main/PXL_20250121_190306477.RAW-01.COVER.jpg?raw=true)

| RGB            |             |             |             | Tilted camera|
|----------------|-------------|-------------|-------------|-------------|
| Metallic       | 157,148,137 | 166,160,153 | 166,162,154 | 169,168,162 |
| Oak Veneer     | 188,127,83  | 189,138,112 | 202,130,85  | 203,154,115 |
| Fabric         | 20,18,23    | 36,34,35    | 33,28,27    | 35,33,34    |
| Glass vs Paper | 65,76,71    | 70,59,53    | 208,209,211 | 210,211,213 |

Sun incident:
![Sun Incident](https://github.com/Wazbaz-the-Weary/Peter_L._Griffiths_Documentation/blob/main/PXL_20250121_190440025.RAW-01.COVER.jpg?raw=true)

| RGB            |             |             |             | Sun incident |
|----------------|-------------|-------------|-------------|--------------|
| Metallic       | 255,255,255 | 183,188,189 | 206,208,205 | 227,233,237  |
| Oak Veneer     | 206,173,141 | 188,153,140 | 208,164,141 | 205,171,145  |
| Fabric         | 25,27,35    | 28,29,33    | 42,43,47    | 67,71,77     |
| Glass vs Paper | 87,94,92    | 129,124,123 | 195,206,214 | 199,210,218  |

