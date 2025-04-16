.. _bioamp-exg-pill:

BioAmp EXG Pill
##################

:bdg-danger:`v1.0`

Overview
*********

BioAmp EXG Pill is a small, powerful analog-front-end (AFE) biopotential signal-acquisition board that can be paired 
with any microcontroller unit (MCU) or single-board computer (SBC) with an analog-to-digital converter (ADC) such as 
Arduino UNO & Nano, Adafruit QtPy, STM32 Blue Pill, BeagleBone Black, and Raspberry Pi Pico, to name 
just a few. It also works with any dedicated ADC, like the Texas Instruments ADS1115 and ADS131M0x, among others.

.. note:: It is recommended to use Arduino UNO R4 while recording biopotential signals since it has 14-bit ADC and can record the signals much accurately.

.. figure:: ../../../media/bioamp-exg-pill.*
    :align: center

What makes it different?
**************************

1. Record publication-quality biopotential signals like ECG, EMG, EOG, or EEG.
2. Small size (25.4 x 10.0mm) allows easy integration into mobile and space-constrained projects.
3. Powerful noise rejection makes it usable even when the device is close to the AC mains supply.
4. Any 1.5 mm diameter wire can be used as a strain-relieving electrode cable, making it very cost-effective.
5. Configure the gain, band pass filter and electrode count according to your requirements.

Features & Specifications
**************************

+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Operating Voltage                   | 3.3/5 V                                                                                                                                                                                               |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Input Impedance                     | 10^12 ohm                                                                                                                                                                                             |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Compatible Hardware                 | Any development board with an ADC (Arduino UNO & Nano, Adafruit QtPy, STM32 Blue Pill, BeagleBone Black, Raspberry Pi Pico, to name just a few) or any standalone ADC of your choice                  |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| BioPotentials                       | EMG, ECG, EOG, EEG (configurable band-pass, by default configured for EEG & EOG)                                                                                                                      |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| No. of channels                     | 1                                                                                                                                                                                                     |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Electrodes                          | 2 or 3 (By default configured for 3 electrodes)                                                                                                                                                       |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Dimensions                          | 25.4 x 10 mm                                                                                                                                                                                          |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Open Source                         | Hardware + Software                                                                                                                                                                                   |
+-------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Board layout
*************

BioAmp EXG Pill’s elegant design allows it to be used in 3 ways:

1. Pin-header holes allow you to solder (berg strip) pin headers for easy use with a breadboard.
2. Castellated holes allow you to solder BioAmp EXG Pill directly onto a custom PCB that requires biopotential-amplification capabilities.
3. Electrode holes allow you to use any 1.5 mm diameter wire as an electrode cable with minimal strain.

.. figure:: media/Front_Specifications.*
    :align: center

.. figure:: media/Back_Specifications.*
    :align: center

BioAmp EXG Pill is fully configurable
=============================================

1. Increase the gain of the instrumentation amplifier by using a 0603 resistor at ``R6``. Decrease gain and configure the bandpass filter by using 0603 parts at ``R12`` and ``C5``. Band limiting is very useful for EOG and EEG recording. Also, the signal sometimes clips while recording an ECG with electrodes very close to the heart. Creating a solder jumper for a band-pass filter helps with that. By default, BioAmp EXG Pill is configured to record EEG and EOG but you can bridge the pads (below bandpass) with solder to make it configurable for EMG and ECG.
2. The normal method of operation for best-quality signal amplification is to use 3 electrodes by default but you can bridge the pads (below electrodes) to make it configurable for 2 electrodes. The 2-electrode mode is specifically included for projects like heart (ECG) patches for HRV. It’s only supposed to be used with a battery-operated setup and is quite prone to high interference noise due to a lack of proper reference on the body (This option is not recommended for most operations)

Software requirements
**********************

To use BioAmp EXG Pill, you will need the softwares mentioned below. Instructions on how to use them are provided later in the guide.

- `Arduino IDE <https://www.arduino.cc/en/software>`_ (Download this to upload Chords arduino firmware to your development board)

- `Chords Web <https://chords.upsidedownlabs.tech/>`_ (Use this open-source web application to visualize your biopotential signals)

- `Visual Studio Code <https://code.visualstudio.com/download>`_ (or any other Code editor of your choice)

- `Python <https://www.python.org/downloads/>`_ (To run Chords-Python script)

- `Chords Python <https://github.com/upsidedownlabs/Chords-Python>`_ (Use this open-source python script designed to record and visualize biopotential signals)

.. note::

    1. The Chords Arduino firmware is identical for both Chords Web and Chords Python, so you only need to upload the code once, and you're all set.
    2. You can choose either Chords Web or Chords Python to record and visualize your biopotential signals based on your needs. If you're curious, you can try both one at a time.

Using the Hardware
*********************

If you have received the assembled BioAmp EXG Pill then you can skip the step 1 and move on to step 2.

Step 1: Solder Connectors
===========================

Insert the provided BioAmp cable's JST PH connector and header pins from top as shown in the image and solder them from below.

.. figure:: media/assembly-step1.*
    :align: center

    `Soldering the connector & header pins on BioAmp EXG Pill`

.. figure:: media/bioamp-exg-pill-soldered.*
    :align: center

    `After soldering, BioAmp EXG Pill should look like this`

Step 2 (optional): Configure for ECG/EMG
==========================================

BioAmp EXG Pill is by default configured for recording EEG or EOG but if you want to record good quality ECG or EMG, then it is recommended to configure it by making a solder joint as shown in the image.

.. figure:: media/assembly-step2.*
    :align: center

.. note:: Even without making the solder joint the BioAmp EXG Pill is capable of recording ECG or EMG but the signals would be more accurate if you configure it.

Step 3: Connect MCU/ADC
=========================

Connect your BioAmp EXG Pill to your MCU/ADC as per the connection table shown below:

.. table:: BioAmp to MCU/ADC connection

    +--------+-----------+
    | BioAmp | MCU/ADC   |
    +========+===========+
    | VCC    | 3.3/5V    |
    +--------+-----------+
    | GND    | GND       |
    +--------+-----------+
    | OUT    | ADC Input |
    +--------+-----------+

If you are connecting ``OUT`` pin of BioAmp to any other analog pin of your development board, then you will have to change the INPUT PIN in the Arduino sketch accordingly.

.. figure:: media/connections-with-arduino.*
    :align: center

    `Connections with a development board`

.. warning:: Take precautions while connecting to power, if power pins (VCC/GND) are to be swapped, your BioAmp EXG Pill will be fried and it’ll become unusable (DIE).

Step 4: Connecting electrode cable
==================================

Connect the BioAmp cable to BioAmp EXG Pill by inserting the cable end in the JST PH connector as shown in the graphic below.

.. figure:: media/connection-with-cable.*
    :align: center

    `Connections with BioAmp Cable v3`

Step 5: Skin Preparation
=========================

Determine the target area and apply Nuprep Skin Preparation Gel on the skin surface where electrodes would be placed to remove dead skin cells and clean the skin from dirt. After rubbing the skin surface thoroughly, clean it with an alcohol wipe or a wet wipe.

For more information, please check out detailed step by step :ref:`skin-preparation`.

Step 5: Electrode placement
===========================

We have 2 options to measure the signals, either using the gel electrodes or using dry electrode based BioAmp Bands. You can try both of them one by one.

1. :ref:`Using Gel electrodes guide <steps-for-gel-electrodes>`
2. :ref:`Assembling & using BioAmp Bands guide <using-bioamp-bands>`

Once you have made the connections, return here to proceed to the next steps.

Step 6: Uploading the code
===========================

1. Connect the development board to your laptop using it's USB cable. Go to Chords Arduino Firmware github repository, scroll down to see a list of development boards compatible with Chords Software Suite. Copy the arduino sketch corresponding to your development board and paste it in Arduino IDE that you downloaded earlier.

    Link for the Github repo: :fab:`github;pst-color-primary` `Chords Arduino Firmware <https://github.com/upsidedownlabs/Chords-Arduino-Firmware/>`_

2. If you are using Arduino UNO R3/Arduino Nano/Arduino Mega/Maker Uno, you will have to uncomment the corresponding macro (eg. uncomment ``#define BOARD_MAKER_UNO`` when using Maker Uno) at the start of the code.

3. If you are using any other development board then skip step 2.

4. Now go to ``tools`` > ``board`` and select you board name. If the name doesn't appear, install the required libraries. In the same menu, select the COM port on which your board is connected. To find out the right COM port, disconnect your board and reopen the menu. The entry that disappears should be the right COM port. Now click on the upload button.

.. warning:: Make sure your laptop is not connected to a charger and sit 5m away from any AC appliances for best signal acquisition.

Step 7: Setting up Chords Web
==============================

1. Visit `chords.upsidedownlabs.tech <https://chords.upsidedownlabs.tech>`_.
2. Click on "Visualize now" button.

.. figure:: ../../../software/chords/chords-web/media/chords_landing_page.*
    :align: center
    :alt: Chords-Web landing page

3. At the bottom, you can see buttons to access various applications:
    a. :ref:`Chords Visualizer <chords-visualizer>`: Use this application for real-time data visualization, recording and data management, filter options, and multi-channel support.
    b. :ref:`FFT Visualizer <fft-visualizer>`: Use this app to visualize filtered EEG signals in real-time, FFT graph, EEG frequency bands, and a beta candle to determine your focus.
    c. :ref:`Serial Wizard <serial-wizard>`: This interface provides real-time serial data visualization using serial plotter and monitor, optimised data rendering, baud rate selection and options to toggle between different modes.

4. Click on any of the button according to your requirement, select the COM port and click OK. You will be able to visualize your signals on the screen.

Step 8: Setting up Chords Python
=================================

Since you have uploaded the firmware already to your board, use our python script and follow the steps given in the :ref:`Chords-Python documentation <using-chords-python>` for lsl streaming, CSV data logging, verbose output with detailed statistics and error reporting. Not only that, you get a complete web interface to access various applications (like ECG with heart rate, EMG with envelope, GUI of channels, CSV plotter, etc.) that you can use to further analyse your signals and create HCI/BCI projects.

.. figure:: ../../../software/chords/chords-python/media/webinterface.*
    :align: center
    :alt: Web Interface

Glimpses of previous versions
*******************************

The BioAmp EXG Pill can be used in a variety of ways, the YouTube video below shows a potential way of using ``v0.7`` of 
BioAmp EXG Pill.

.. youtube:: -G3z9fvQnuw
    :align: center
    :width: 100%

A lot has improved in terms of interference rejection and flexibility from ``v0.7`` to ``v1.0`` of the BioAmp EXG Pill. The YouTube video 
below shows the ECG, EMG, EOG, and EEG recording using ``v1.0b`` of device.

.. youtube:: z9-B9bHWuhg
    :align: center
    :width: 100%

Real-world Applications
************************

BioAmp EXG Pill is perfect for researchers, makers, and hobbyists looking for novel ways to sample biopotential data. It can 
be used for a wide variety of interesting biosensing projects, including:

- AI-assisted detection of congestive heart failure using CNN (ECG)
- Heart-rate variability calculation to detect heart ailments (ECG)
- Prosthetic arm (servo) control (EMG)
- Controlling a 3DOF robotic arm (EMG)
- Real-time game controllers (EOG)
- Blink detection (EOG)
- Capturing photos with a blink of an eye (EOG) and many more examples. 

Project ideas & tutorials
*************************

.. only:: html

    .. article-info::
        :avatar: ../../../kits/diy-neuroscience/basic/media/instructables.svg
        :avatar-link: https://www.instructables.com/member/Upside+Down+Labs/
        :avatar-outline: muted
        :author: Projects on Instructables
        :class-container: sd-p-2 sd-rounded-1

    Below are some projects made by students using the BioAmp EXG Pill.

    .. grid:: 2 2 2 2
        :margin: 4 4 0 0 
        :gutter: 2

        .. grid-item-card:: Controlling video game using brainwaves (EEG)
            :text-align: center
            :link: https://www.instructables.com/Controlling-Video-Game-Using-Brainwaves-EEG/

        .. grid-item-card:: Visualising electrical impulses from eyes (EOG)
            :text-align: center
            :link: https://www.instructables.com/Visualizing-Electrical-Impulses-of-Eyes-EOG-Using-/

        .. grid-item-card:: Recording EEG from visual cortex
            :text-align: center
            :link: https://www.instructables.com/Recording-EEG-From-Visual-Cortex-of-Brain-Using-Bi/

        .. grid-item-card:: Recording EEG from prefrontal cortex
            :text-align: center
            :link: https://www.instructables.com/Recording-EEG-From-Pre-Frontal-Cortex-of-Brain-Usi/

        .. grid-item-card:: Eye blink detection
            :text-align: center
            :link: https://www.instructables.com/Eye-Blink-Detection-by-Recording-EOG-Using-BioAmp-/

        .. grid-item-card:: Creating a drowsiness detector
            :text-align: center
            :link: https://www.instructables.com/Drowsiness-Detector-by-Detecting-EOG-Signals-Using/

        .. grid-item-card:: Record publication-grade ECG
            :text-align: center
            :link: https://www.instructables.com/Record-Publication-Grade-ECG-at-Your-Home-Using-Bi/

        .. grid-item-card:: Measuring heart rate
            :text-align: center
            :link: https://www.instructables.com/Measuring-Heart-Rate-Using-BioAmp-EXG-Pill/

        .. grid-item-card:: Detecting heart beats
            :text-align: center
            :link: https://www.instructables.com/Detecting-Heart-Beats-Using-BioAmp-EXG-Pill/

        .. grid-item-card:: Record publication-grade EMG
            :text-align: center
            :link: https://www.instructables.com/Recording-Publication-Grade-Muscle-Signals-Using-B/

        .. grid-item-card:: Detecting up and down movement of eyes
            :text-align: center
            :link: https://www.instructables.com/Tracking-UP-and-DOWN-Movements-of-Eyes-Using-EOG/

    These are some of the project ideas but the possibilities are endless. So create your own Human Computer Interface (HCI) and 
    Brain Computer Interface (BCI) projects and share them with us at contact@upsidedownlabs.tech.

.. only:: latex

    You can find step-by-step tutorials for various HCI/BCI projects on our `Instructables <https://www.instructables.com/member/Upside+Down+Labs/>`_.

    Below are some project ideas that you can try making at your home.

    1. `Controlling video game using brainwaves (EEG) <https://www.instructables.com/Controlling-Video-Game-Using-Brainwaves-EEG/>`_
    2. `Visualising electrical impulses from eyes (EOG) <https://www.instructables.com/Visualizing-Electrical-Impulses-of-Eyes-EOG-Using-/>`_
    3. `Recording EEG from visual cortex part of brain <https://www.instructables.com/Recording-EEG-From-Visual-Cortex-of-Brain-Using-Bi/>`_
    4. `Recording EEG from prefrontal cortex part of brain <https://www.instructables.com/Recording-EEG-From-Pre-Frontal-Cortex-of-Brain-Usi/>`_
    5. `Eye blink detection <https://www.instructables.com/Eye-Blink-Detection-by-Recording-EOG-Using-BioAmp-/>`_
    6. `Creating a drowsiness detector <https://www.instructables.com/Drowsiness-Detector-by-Detecting-EOG-Signals-Using/>`_
    7. `Record publication-grade ECG <https://www.instructables.com/Record-Publication-Grade-ECG-at-Your-Home-Using-Bi/>`_
    8. `Measuring heart rate <https://www.instructables.com/Measuring-Heart-Rate-Using-BioAmp-EXG-Pill/>`_
    9. `Detecting heart beats <https://www.instructables.com/Detecting-Heart-Beats-Using-BioAmp-EXG-Pill/>`_
    10. `Record publication-grade EMG <https://www.instructables.com/Recording-Publication-Grade-Muscle-Signals-Using-B/>`_
    11. `Detecting up and down movement of eyes <https://www.instructables.com/Tracking-UP-and-DOWN-Movements-of-Eyes-Using-EOG/>`_

    These are some of the project ideas but the possibilities are endless. So create your own Human Computer Interface (HCI) and 
    Brain Computer Interface (BCI) projects and share them with us at contact@upsidedownlabs.tech.