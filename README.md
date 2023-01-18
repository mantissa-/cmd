# cmd
## A collection of random shell commands to make my life easier


### Convert all EXR files in folder to JPG

`parallel convert -quality 100 -scale 2000000@ '{}' '{.}.jpg' ::: *.exr`

#### Bonus round:
- Add `-profile profile_name.icc` to specify an ICC profile
- The scale parameter with @ at the end specifies the image size in megapixels. For example, a 2:1 image wil automatically be scaled to 2000x1000px

### Convert all TIF files to EXR (raw exr that is, not linear or AcesCG because I'm a weirdo)

`find /path/to/folder/ -name '*.tif' | parallel mogrify {} -format exr -compress DWAB {}`



### FFMPEG Fun

#### Convert image sequence to mp4

`ffmpeg -framerate 30 -pattern_type glob -i '*.jpg' -r 30 -crf 25 -preset veryslow -pix_fmt yuv420p -c:v libx264 ../000-out.mp4`

#### Convert video to image sequence

`ffmpeg -i video.mov -q:v 2 037/%04d.jpg`
