# cmd
A collection of random shell commands to make my life easier


## Convert all EXR files in folder to jpg

`parallel convert -quality 100 -scale 2000000@ '{}' '{.}.jpg' ::: *.exr`

Bonus: add `-profile profile_name.icc` to specify an ICC profile
