# Building on Arch Linux and It's Derivatives

The following builds RebbleOS on Arch Linux and Parabola once the Pebble SDK is installed:

Note: You will need to aquire the FPGA blobs from the [discord](discord.gg/aRUAYFN) before building.
```sh
    git clone https://github.com/ginge/FreeRTOS-Pebble.git
    cd FreeRTOS-Pebble
    git submodule update --init --recursive
    virtualenv --no-site-packages .env
    souce .env/bin/activate
    make
    deactivate
```
   
The Pebble SDK is a prerequisite for portions of RebbleOS. The
SDK is available [here](https://developer.rebble.io/developer.pebble.com/sdk/download/index.html).
As an example, on Arch, one may create an installation
directory for the SDK using the following.

```sh
    mkdir ~/pebble-dev/
    cd ~/pebble-dev/
    wget https://s3.amazonaws.com/assets.getpebble.com/pebble-tool/pebble-sdk-4.5-linux64.tar.bz2
    tar -jxf pebble-sdk-4.5-linux64.tar.bz2
    echo 'export PATH=~/pebble-dev/pebble-sdk-4.5-linux64/bin:$PATH' >> ~/.bash_profile
    . ~/.bash_profile
    sudo pacman -Syyu
    sudo pacman -S python2 python2-pip  python2-gevent sdl dtc pixman git arm-none-eabi-gcc arm-none-eabi-newlib npm
    pip2 install virtualenv --user
    pip2 install --upgrade pip --user
    cd ~/pebble-dev/pebble-sdk-4.5-linux64
    virtualenv --no-site-packages .env
    source .env/bin/activate
    pip2 install -r requirements.txt
    deactivate
    mkdir ~/.pebble-sdk/
    touch ~/.pebble-sdk/NO_TRACKING
    pebble sdk install https://github.com/aveao/PebbleArchive/raw/master/SDKCores/sdk-core-4.3.tar.bz2
    pebble ping --emulator aplite
```

As the SDK is no longer available from an official source, this example uses an archived version from [this](https://github.com/aveao/PebbleArchive/) GitHub repository
