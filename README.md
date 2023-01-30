# cmd 
## A collection of random shell commands to make my life easier


### ImageMagick Shenanigans

#### Convert all EXR files in current folder to JPG

`parallel convert -quality 100 -scale 2000000@ '{}' '{.}.jpg' ::: *.exr`

##### Bonus round:
- Add `-profile profile_name.icc` to specify an ICC profile
- The scale parameter with @ at the end specifies the image size in megapixels. For example, a 2:1 image wil automatically be scaled to 2000x1000px

#### Resize all JPG images in current folder to fit 1920x1080 frame and fill the background with black

`parallel convert -resize 1920x1080 -extent 1920x1080 -gravity Center -background black '{}' '{.}.png' ::: *.jpg`

#### Convert all TIF files to EXR (raw exr that is, not linear or AcesCG because I'm a weirdo)

`find /path/to/folder/ -name '*.tif' | parallel mogrify {} -format exr -compress DWAB {}`

***

### FFMPEG Fun

#### Convert JPG image sequence to mp4

`ffmpeg -framerate 30 -pattern_type glob -i '*.jpg' -r 30 -crf 25 -preset veryslow -pix_fmt yuv420p -c:v libx264 ../000-out.mp4`

#### Convert video to JPG image sequence

`ffmpeg -i video.mov -q:v 2 %04d.jpg`

***

### Raw Conversion

#### dcraw "one size fits all" raw to linear 16-bit tif

`parallel dcraw -v -w -o 7 -4 -T -q 0 -p embed '{}' ::: *`

- -v = verbose
- -w = respect cam color temp
- -o = ouptut colorspace
- -4 = linearize
- -q = debayer quality, fastest
- -p = embed cam profile
