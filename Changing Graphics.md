## Step 1 - Creating gritflags.

Before making graphics changes, you need to understand what gritflags are and how to create them. Grit is the image compiler in the CFRU engine. Gritflags contain instructions on how an image should be compiled by Grit, such as whether the palette has 16 or 256 colors, whether the tileset, tilemap or palette are compressed, specify what you want to be generated during compilation, etc. This allows us to have a better customization.

I will teach you how to create custom gritflags for your images. I recommend seeing all the Grit commands [here](https://www.coranac.com/man/grit/html/grit.htm) before proceeding, so you can understand what each command does.  Also i'll just highlight the most important commands.

The syntax for gritflags is pretty simple, you just have to separate all commands by whitespace, like the example below:

```-gB4 -gu8 -ah256 -aw256 -m -mR4 -mu8```

So, lets start. Here's a list of commands that I consider important, and when you should use them according to the characteristics of your image:

### Graphics Options

`-g!` : By default a tileset is generated during compilation. If you don't want a tileset to be generated, add this command. If you added this command, you can ignore all the other commands in this section.

`-gBx` : In this command, replace `x` with the bit depth of your image. If your image has 16 colors, add `-gB4`. If your image has 256 colors, add `-gB8`. (16 colors = 4, 256 colors = 8).

`-gu8` : This is a required command, you must always add it, otherwise you'll have problems.

`-gzl` : Add this command if you want the generated tileset to be compressed.

### Area Options

`-ahY` : This command is used to determine the height of the image. Replace `Y` with the height of the image.

`-awX` : This works like the command `-ahY`, but this one is used to determine the image weight. you just have to change `X` with the image weight. `-awX` and `-ahY` are used to determine the image size. It's a good practice to always add these two commands in your gritflags.

### Tilemap Options

`-m` : By default a tilemap isn't generated during compilation. Add this command if you want a tilemap to be generated. Note that if you don't add this command, the tileset will become a sprite. If you didn't add this command, you can ignore the other commands in this section.

`-mRx` : This command enables tiles reduction for tilemaps. If the image have 16 colors, add `-mR4`. If the image have 256 colors, add `-mR8`. This command isn't required, but it's recommended.

`-mu8` : This is a required command, you must always add it, otherwise you'll have problems.

`-mzl` : Add this command if you want the generated tilemap to be compressed.

