Heroku buildpack: FFMpeg with prebuilt x264 and fdk_acc
=======================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for using [ffmpeg](http://www.ffmpeg.org/) in your project.  
It doesn't do anything else, so to actually compile your app you should use [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) to combine it with a real buildpack.

Usage
-----
To use this buildpack, you should prepare .buildpacks file that contains this buildpack url and your real buildpack url.  

    $ ls
    .buildpacks
    ...
    
    $ cat .buildpacks
    https://github.com/Litterfeldt/heroku-buildpack-ffmpeg-x264-fdk_aac
    https://github.com/heroku/heroku-buildpack-play

    $ heroku create --buildpack https://github.com/ddollar/heroku-buildpack-multi

    $ git push heroku master
    ...

You can verify installing ffmpeg by following command.

    $ heroku run "ffmpeg -version"

Perks
-------
This buildpack comes with ffmpeg configured like so:

```bash
./configure --enable-static \
--disable-shared \
--disable-asm \
--extra-libs="-L$LIBSS/lib" \
--extra-cflags="-I$LIBSS/include" \
--prefix=/app/vendor/ffmpeg \
--enable-libfdk-aac \
--enable-nonfree \
--enable-libx264 \
--enable-gpl
```

It also contains all prebuilt dependencies needed to run ffmpeg with x264 and fdk_acc.

Nothing else is needed.

https://github.com/shunjikonishi/heroku-buildpack-ffmpeg/blob/master/bin/compile#L10
