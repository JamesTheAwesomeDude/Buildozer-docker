What
====

A simple docker image to build kivy projects without pain (hopefully)

How to use
==========

Buildozer.spec
--------------

If you don't have a buildozer.spec you can create one using

    sudo docker -v $PWD:/buildozer tshirtman/buildozer buildozer init .

Then customize it in your favorite editor.

Building
--------

Simply run the docker image with the directory containing buildozer.spec mounted as /buildozer/, the result apk will be in your directory/bin

    sudo docker run -v $PWD:/buildozer/ tshirtman/buildozer

The first build, or any build that changed your requirements in buildozer.spec will be slower, since the distribution has to be rebuilt (it's cached in your project's directory, so it'll be reused when possible). Builds that can reuse your distribution will be a lot faster.

Installing
----------

Sadly the docker doesn't see the android device for me, so you'll need adb another way to deploy

- adb

   If you have adb installed on your machine, you can use

       adb install bin/yourapp.apk

- webserver

   You can run a local webserver and open your application from the browser

       python -m SimpleHTTPServer 8000 bin

   and open it on your phone

   http://your-ip:8000/bin

   Of course, don't do that in an untrusted network if you care about the secrecy of your project, or the security of your computer :).

- MTP

  This is a bit less nice, but you can open the phone in your filebrowser, drop it on the phone, and open it with a file browser on the phone, to install it.


Debugging
---------

Ideally debugging should be done through adb logcat, but if you can't do it for some reason, I advise configuring kivy to output to a file on your phone memory, this can be achieved by setting the Config before any other kivy import in your main.py

    from kivy.config import Config
    Config.set('kivy', 'log_dir', '/mnt/sdcard/kivy_logs'

So you can open them from your file browser with your phone plugged to your computer.
