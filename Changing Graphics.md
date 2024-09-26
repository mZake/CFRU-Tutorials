## Step 1 - Creating gritflags.

Before making graphics changes, you need to understand what gritflags are and how to create them. Grit is the image compiler in the CFRU engine. Gritflags contain instructions on how an image should be compiled by Grit, such as whether the palette has 16 or 256 colors, whether the tileset, tilemap or palette are compressed, specify what you want to be generated during compilation, etc. This allows us to have a better customization.

I will teach you how to create custom gritflags for your images. I recommend seeing all the Grit commands [here](https://www.coranac.com/man/grit/html/grit.htm) before proceeding, so you can understand what each command does.  Also i'll just highlight the most important commands.

The syntax for gritflags is pretty simple, you just have to separate all commands by whitespace, like the example below:

```-gB4 -gu8 -ah256 -aw256 -m -mR4 -mu8```

So, lets start. Here's a list of commands that I consider important, and when you should use them according to the characteristics of your image:

### Graphics Options

`-g!` - By default a tileset is generated during compilation. If you don't want a tileset to be generated, add this command. If you added this command, you can ignore all the other commands in this section.

`-gBx` - In this command, replace `x` with the bit depth of your image. If your image has 16 colors, add `-gB4`. If your image has 256 colors, add `-gB8`. (16 colors = 4, 256 colors = 8).

`-gu8` - This is a required command, you must always add it, otherwise you'll have problems.

`-gzl` - Add this command if you want the generated tileset to be compressed.

### Area Options

`-ahY` - This command is used to determine the height of the image. Replace `Y` with the height of the image.

`-awX` - This works like the command `-ahY`, but this one is used to determine the image weight. you just have to change `X` with the image weight. `-awX` and `-ahY` are used to determine the image size. It's a good practice to always add these two commands in your gritflags.

### Tilemap Options

`-m` - By default a tilemap isn't generated during compilation. Add this command if you want a tilemap to be generated. Note that if you don't add this command, the tileset will become a sprite. If you didn't add this command, you can ignore the other commands in this section.

`-mRx` - This command enables tiles reduction for tilemaps. If the image have 16 colors, add `-mR4`. If the image have 256 colors, add `-mR8`. This command isn't required, but it's recommended.

`-mu8` - This is a required command, you must always add it, otherwise you'll have problems.

`-mzl` - Add this command if you want the generated tilemap to be compressed.

### Palette Options

`-p!` - By default, a palette is generated. If you don't want a palette to be generated, add this command. If you added this command, you can ignore all other commands in this section.

`-pu8` - Only add this command if your palette is compressed. Otherwise you can ignore it.

`-pzl` - Add this command if you want the generated palette to be compressed.

### Output Options

`-fh` - Always add this command to your gritflags.

`-fts` - Always add this command to your gritflags.

The list of commands ends here. Using gritflags is very simple, all you need to do is create a file called **gritflags.txt**, and add all the commands you want inside it.

Note that you shouldn't put two gritflags in the same folder, otherwise you will have problems.

## Step 2 - Getting the Image info.

This is all the image info you need to get:

- Tileset compression
- Tilemap compression
- Palette compression
- Tileset pointer
- Tilemap pointer
- Palette pointer

If that wasn't clear, you don't need to look for tilemap pointer if the image is a sprite, since sprites don't have tilemaps. Fortunately, it's possible to get all this info just using HMA (Hex Maniac Advance)!

Let's start by getting the compression of the tileset, sprite, tilemap and palette. In HMA, navigate to the image you want to change, It is possible to find out information about compression and the palette by looking for some keywords at the image's anchor. Here is a list of these keywords:

### Tileset

`lzt4` - Compressed tileset with 16 colors.

`lzt8` - Compressed tileset with 256 colors.

`uct4` - Uncompressed tileset with 16 colors.

`uct8` - Uncompressed tileset with 256 colors.

### Sprite

`lzs4` - Compressed sprite with 16 colors.

`lzs8` - Compressed sprite with 256 colors.

`ucs4` - Uncompressed sprite with 16 colors.

`ucs8` - Uncompressed sprite with 256 colors.

### Tilemap

`lzm4` - Compressed tilemap with 16 colors.

`lzm8` - Compressed tilemap with 256 colors.

`ucm4` - Uncompressed tilemap with 16 colors.

`ucm8` - Uncompressed tilemap with 256 colors.

### Palette

`lzp4` - Compressed 16 colors palette.

`lzp8` - Compressed 256 colors palette.

`ucp4` - Uncompressed 16 colors palette.

`ucp8` - Uncompressed 256 colors palette.

Here's an example with the title screen charizard tileset:

![Capturar](https://github.com/user-attachments/assets/80fa91df-8fcb-498a-bf28-38e1a9e6383a)

In this case I got the keyword `lzt4`, which means this is a compressed tileset with 16 colors. You apply this same procedure to sprites, palettes and tilemaps too.

Getting the tileset, sprite, tilemap and palette pointers is very simple, All you have to do is get the offset where they are located and then search for the obtained offset using the find function. Here's an example:

![Capturar](https://github.com/user-attachments/assets/6f04ffad-50e8-4013-bc2e-44131a946ba0)

When you press Enter, something like this should appear:

![Capturar2](https://github.com/user-attachments/assets/5bad3fdb-0b47-41fd-812d-3b1f784c67c2)
