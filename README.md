# mipgen
I had trouble finding a decent standalone program which converts various image formats to the .ktx or .dds format. Then I stumbled upon [filament](https://github.com/google/filament) and found the [mipgen tool](https://github.com/google/filament/tree/master/tools/mipgen) which seemed to be a good starting point. 

## Differences to [mipgen tool](https://github.com/google/filament/tree/master/tools/mipgen)
- standalone
- no-mipmap option 

## Note
- currently linux only
- input must have png format

## Detailed Info
```
MIPGEN generates mipmaps for an image down to the 1x1 level.

The <output_pattern> argument is a printf-style pattern.
For example, "mip%2d.png" generates mip01.png, mip02.png, etc.
Miplevel 0 is not generated since it is the original image.

If the output format is a container format like KTX, then
<output_pattern> is simply a filename.

Usage:
    MIPGEN [options] <input_file> <output_pattern>

Options:
   --help, -h
       print this message
   --license, -L
       print copyright and license information
   --linear, -l
       assume that image pixels are already linearized
   --page, -p
       generate HTML page for review purposes (mipmap.html)
   --quiet, -q
       suppress console output from the mipgen tool
   --grayscale, -g
       create a single-channel image and do not perform gamma correction
   --format=[exr|hdr|rgbm|psd|png|dds|ktx], -f [exr|hdr|rgbm|psd|png|dds|ktx]
       specify output file format, inferred from output pattern if omitted
   --kernel=[box|nearest|hermite|gaussian|normals|mitchell|lanczos|min], -k [filter]
       specify filter kernel type (defaults to lanczos)
       the "normals" filter may automatically change the compression scheme
   --add-alpha
       if the source image has 3 channels, this adds a fourth channel filled with 1.0
   --strip-alpha
       ignore the alpha component of the input image
   --no-mipmap
       forces a miplevel count of 0, effectively disabling mipmaps
   --compression=COMPRESSION, -c COMPRESSION
       format specific compression:
           KTX:
             astc_[fast|thorough]_[ldr|hdr]_WxH, where WxH is a valid block size
             s3tc_rgb_dxt1, s3tc_rgba_dxt5
             etc_FORMAT_METRIC_EFFORT
               FORMAT is r11, signed_r11, rg11, signed_rg11, rgb8, srgb8, rgb8_alpha
                         srgb8_alpha, rgba8, or srgb8_alpha8
               METRIC is rgba, rgbx, rec709, numeric, or normalxyz
               EFFORT is an integer between 0 and 100
           PNG: Ignored
           Radiance: Ignored
           Photoshop: 16 (default), 32
           OpenEXR: RAW, RLE, ZIPS, ZIP, PIZ (default)
           DDS: 8, 16 (default), 32

Examples:
    MIPGEN -g --kernel=hermite grassland.png mip_%03d.png
    MIPGEN -f ktx --compression=astc_fast_ldr_4x4 grassland.png mips.ktx
    MIPGEN -f ktx --compression=etc_rgb_rgba_40 grassland.png mips.ktx
```

## Examples 
Some more examples from a [filament tutorial](https://google.github.io/filament/webgl/tutorial_suzanne.html)
```
# Create mipmaps for base color and two compressed variants.
mipgen albedo.png albedo.ktx
mipgen --compression=astc_fast_ldr_4x4 albedo.png albedo_astc.ktx
mipgen --compression=s3tc_rgb_dxt1 albedo.png albedo_s3tc.ktx

# Create mipmaps for the normal map and a compressed variant.
mipgen --strip-alpha --kernel=NORMALS --linear normal.png normal.ktx
mipgen --strip-alpha --kernel=NORMALS --linear --compression=etc_rgb8_normalxyz_40 \
    normal.png normal_etc.ktx

# Create mipmaps for the single-component roughness map and a compressed variant.
mipgen --grayscale roughness.png roughness.ktx
mipgen --grayscale --compression=etc_r11_numeric_40 roughness.png roughness_etc.ktx

# Create mipmaps for the single-component metallic map and a compressed variant.
mipgen --grayscale metallic.png metallic.ktx
mipgen --grayscale --compression=etc_r11_numeric_40 metallic.png metallic_etc.ktx

# Create mipmaps for the single-component occlusion map and a compressed variant.
mipgen --grayscale ao.png ao.ktx
mipgen --grayscale --compression=etc_r11_numeric_40 ao.png ao_etc.ktx
```

## Build
Standard cmake procedure. Go to ```build/``` and run
```
cmake .
make
```
