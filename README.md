Heroku buildpack: FFMpeg
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
    https://github.com/shunjikonishi/heroku-buildpack-ffmpeg
    https://github.com/heroku/heroku-buildpack-play

    $ heroku create --buildpack https://github.com/ddollar/heroku-buildpack-multi

    $ git push heroku master
    ...

You can verify installing ffmpeg by following command.

    $ heroku run "ffmpeg -version"


Building the Binary
-----

The ffmpeg binary was built using the [ffmpeg-static](https://github.com/stvs/ffmpeg-static) build scripts on a heroku [stack-image](https://github.com/heroku/stack-images) VM.

To build it yourself

- clone the stack-image heroku repository to your local machine via `git clone https://github.com/stvs/ffmpeg-static`, then `cd` into it
- run `vagrant up`
- run `vagrant ssh`
- now clone the ffmpeg-static repo into the virtual machine: `git clone https://github.com/stvs/ffmpeg-static`
- `cd ffmpeg-static`
- `./build-ubuntu.sh`

if the final ffmpeg compilation step fails due to a missing library (such as libopus):

- manually copy the ffmpeg `./configure` command, remove the `--enable-opus` line, and then run it again
- run `make` manually

I had to disable libopus and one other library if I remember correctly.

