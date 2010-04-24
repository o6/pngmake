## Purpose ##

*pngmake* is a simple bash script created to help developers that want to keep their resources in fully editable, layered PSD format. Although PSD files can be great for keeping edibility, they aren't the kind of files that you'd want to actually distribute in an application. This script takes a directory of PSD files and converts each one to a PNG file. And as if that wasn't enough, it then runs the fabulous [OptiPNG](http://optipng.sourceforge.net/) on each PNG file, so that you can distribute the PNG files on the web or in an application without worrying about bandwidth or storage.  

## Compatibility ##

At this time, *pngmake* is only compatible with Mac OS X. It has been tested on Mac OS 10.6.3, but I believe it will work on all versions of Snow Leopard. It may or may not work on Leopard, I haven't tested it.  

You may be wondering why it doesn't support other UNIX operating systems. The simple answer is that ImageMagick sucks. I tried to write the script to use ImageMagick, which would have been cross-platform, but it doesn't play nicely with Photoshop layer styles. As layer styles are a necessity to many designers/developers, I decided to use a OS X-only utility to run the image conversions:  *sips*. SIPS stands for Scriptable Image Processing Suite. Some developers may be familiar with it, either directly or from using it indirectly through the Image Events AppleScript library. It handles PSD files beautifully, so I decided to use it.  

If anyone can find a cross-platform tool for converting PSD files that handles layer styles properly, please let me know and I'll try and integrate it with the script.  

## Usage ##

*pngmake* is currently only a command line utility, but I do have plans to make a UI soon. For now, here is how to use it via Terminal:  

    $ ./pngmake.sh  

Though it seems almost too good to be true, that command may be enough for you! When passed no arguments, *pngmake* looks in the working directory for PSD files and converts/optimizes each one. There are a few catches though. The main difficulty is that you will need to have an optipng binary somewhere on your $PATH. There is a binary included in the *pngmake* repository, so you should just be able to drop it into /usr/local/bin and use the script. If you would like to store optipng somewhere else, or have your own copy you'd like to use, just use the following command:  

    $ ./pngmake.sh --optipng /path/to/optipng  

Or, if you prefer short arguments, you can use the following:  

    $ ./pngmake.sh -p /path/to/optipng  

You can also point *pngmake* to a custom input directory and a custom output directory. Both default to "./", but they are easily customized like so:  

    $ ./pngmake.sh --input /directory/full/of/psd/files --output /directory/soon/to/be/full/of/png/files  

And again, if you prefer short arguments, they work too:  

    $ ./pngmake.sh -i /directory/full/of/psd/files -o /directory/soon/to/be/full/of/png/files  

Pretty cool, right? I know. But the awesomeness doesn't stop there! You can also tweak the compression level used for optipng. The default is to use the maximum compression level (7), but that may be slow for large images. OptiPNG accepts an integer value from 1 to 7 for the compression ratio, with 1 being the fastest with the worst compression ratio, and 7 being the slowest with the best compression ratio. Keep in mind that no matter what, OptiPNG will not degrade the *quality* of your images. If you want to customize it, use the following flag:  

    $ ./pngmake.sh --compression-level 2  

And again, with shorter arguments:  

    $ ./pngmake.sh -c 2  

That pretty much covers it! If you, for some strange reason, would like to customize the path to the SIPS binary that is used, you can use the `--sips` or `-s` flag, but you really shouldn't need to do that. Oh, and you can turn on verbose mode with the `--verbose` or `-v` flags. That will give you status information about your conversions.  

## License ##

See the License.md file for extended license info, but in short, use it for anything you want, however you want!