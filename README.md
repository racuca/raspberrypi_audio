# Raspberry Pi MEMS Mic audio Test
# reference 
https://github.com/makerportal/rpi_i2s

https://www.pythonguis.com/widgets/equalizerbar/

chatgpt


# setup process
#### 0. install OS

Rasbian Bullseye 32bit OS with Python 3.9.2


#### 1. update OS

sudo apt-get -y update

sudo apt-get -y upgrade

sudo reboot

#### 2. update python (Optional)

wget https://www.python.org/ftp/python/3.xx.xx/Python-3.xx.xx.tgz

tar zxvf Python-3.xx.xx.tgz

cd Python-3.xx.xx

./configure --enable-optimizations --with-openssl=/usr/bin/openssl --with-openssl-rpath=auto

sudo make altinstall

cd /usr/bin

sudo rm python

sudo ln -s /usr/local/bin/python3.xx python

sudo rm python3

sudo ln -s /usr/local/bin/python3.xx python3

python --version



#### 3. install PyQt5 for equalizer function

sudo apt-get install python3-pyqt5

sudo apt-get install qttools5-dev-tools

sudo apt-get install pyside2-tools

sudo apt-get install pyside2.*

sudo apt-get install python3-pyside2.*

####  **** run for DRI2 error message, but after this, screen may be unstable. this command is just optional. ****
sudo raspi-config

Advanced Options -> GL Driver -> GL (Full KMS) OpenGL ...

reboot


#### 4. install packages for pyaudio 

sudo pip3 install --upgrade adafruit-python-shell

sudo wget https://raw.githubusercontent.com/adafruit/Raspberry-Pi-Installer-Scripts/master/i2smic.py

    # modify source
    run editor as root. for example, sudo thonny
    modify Raspberry-Pi-Installer-Scripts/i2s_mic_module/snd-i2smic-rpi.c
    simple_card_info to asoc_simple_card_info
    
sudo python3 i2smic.py</br>

reboot

sudo apt-get install libportaudio0 libportaudio2 libportaudiocpp0 portaudio19-dev</br>

sudo pip install pyaudio matplotlib scipy</br>

sudo apt-get install libopenblas-dev

#### 5. check audio devices with input channels

    import pyaudio
    audio = pyaudio.PyAudio() # start pyaudio
    for ii in range(0,audio.get_device_count()):
        # print out device info
        print(audio.get_device_info_by_index(ii))

You should see this snd_rpi_i2s_card device.

(1, 'snd_rpi_i2s_card: simple-card_codec_link snd-soc-dummy-dai-0 (hw:1,0)', 2)

#### 6. connect raspberry pi and mems mic

refer to images


#### 7. record speech and analyze wave file using fft.
python i2s_mono.py  ( specify dev_index variable value as your device indexes )

python fft_pysimplegui.py

python fft_prompt.py
