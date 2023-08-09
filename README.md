# Hackathon: openOCT - Full-field Incoherent Interferemeter for better optical sectioning with remote control capabilities

Welcome to the openOCT Hackathon! In this hackathon, we will be addressing the crucial need for an open-source optical coherence tomography system that can help students learning more about setting up a low-coherence interferemoter. To keep the budget low, we aim for a full-field time domain OCT using an SLD (super luminescent diode) - alternatively one could also try an LED to lower the costs even more




![](./IMAGES/Bildschirmaufnahme.gif)



## Motivation

Optical coherence tomography (OCT) is a non-invasive optical method that allows for deep imaging within tissues. It is primarily based on a Michelson-type interferometer, where the light source is generated by a low-coherence light source, such as a superluminescent diode (SLD). The coherence volume, which represents the volume where constructive interference is observed, is inversely proportional to the spectral bandwidth of the light source.

However, adjusting a Michelson interferometer is not a straightforward process, as the lengths of the reference and sample arms need to match by approximately 10 µm. To address this challenge, a common-path-type full-field OCT is employed, where both arms are illuminated by an SLD, and the sample or mirror is imaged using a long-working distance objective or a simple lens. This alignment method simplifies the process since the "sample" or mirror is brought into focus, ensuring that the path lengths are nearly equal.

![](IMAGES/OCt.png)


Such a system enables the estimation of depth in applications like fingertip imaging or visualization of the rods in the retina. Currently available OCT systems are expensive and not accessible to all, and thus there is a need for a more affordable and open system, which our system aims to provide.

In addition to the challenges related to alignment, adjusting such a system becomes even more complex due to the influence of touch, which can change the path lengths. To overcome this, we also intend to automate certain mechanical elements and enable remote access using the TwinLab developed by the Lichtwerkstatt, which provides WebRTC-based access to labware.

For further reading on this topic, please refer to the following sources:
- [Article 1](https://ieeexplore.ieee.org/document/8957575)
- [Article 2](https://pubs.aip.org/aapt/ajp/article-abstract/88/12/1132/859670/Full-field-optical-coherence-tomography-An?redirectedFrom=fulltext)


This will be our main guide star publication:

![](IMAGES/Detailed-optical-design-and-schematic-top-view-of-the-compact-and-mobile-FF-OCT_W640.jpg)


Further reading https://ieeexplore.ieee.org/document/8957575
https://pubs.aip.org/aapt/ajp/article-abstract/88/12/1132/859670/Full-field-optical-coherence-tomography-An?redirectedFrom=fulltext


## Goal


Our primary goal is to set up an optical coherence tomography (OCT) system based on the optical scheme depicted in the diagram. The first step is to ensure that the system is adjusted to observe interference fringes. This involves aligning the components to achieve constructive interference.

![](IMAGES/OCTSetup.png)

Once we have successfully obtained interference fringes, our next objective is to acquire a stack of fringes from two mirrors with varying positions. To achieve this, we plan to integrate low-cost stepper motors into one of the mirrors, allowing us to control its movement. The integration of these motors will be done in conjunction with the TwinLab, a versatile platform developed by the Lichtwerkstatt that provides remote access to labware via WebRTC.


![](IMAGES/Newvideo-2.gif)

Alternatively, we aim to develop a Jupyter notebook program that integrates the UC2-ESP32/UC2-REST framework with the low-cost stepper motors, enabling automation of the OCT system. This program will facilitate precise control over the motion of the mirrors.

To further enhance the capabilities of our OCT system, we are exploring methods to move the reference mirror along the optical axis. This can be achieved by employing a stepper motor, voice coil motor, or similar mechanism. By varying the position of the reference mirror, we can capture the typical oscillation of the interference over the Z-axis.

In order to process and analyze the acquired data, we plan to develop Python code that can reconstruct the OCT scan. This code will extract the mirror location and reflection information from the data. Additionally, we will investigate techniques to compensate for any potential non-linearity in the motion of the mirrors or stages, ensuring accurate positioning.

Finally, we intend to incorporate a sample, such as layers of coverslips, into the setup and acquire an OCT scan. This will allow us to visualize and analyze the internal structure of the sample using the OCT system.

By accomplishing these goals, we aim to create a functional and cost-effective OCT system that provides valuable imaging capabilities for various applications.


## Background

### Interference

- A phenomenon where two waves interact with each other, resulting in a visible pattern.
- Two wave trains must have a fixed phase relationship to each other.
- Temporal coherence: A light source is split and brought into interference at different times by extending the optical path accordingly.
- Spatial coherence measures the interference capability of two wavelengths from a source originating from different locations.

### OCT

OCT relies on having as small a temporal coherence as possible to increase optical sectioning. This is achieved by using a typical source such as an SLD or LED that has a broad spectrum. Multiple wavelength components interfere simultaneously. Constructive interference of all wavelengths is only visible in a range inversely proportional to the spectrum. The broader the spectrum, the smaller the range where interference can be observed. This makes alignment challenging. Our design overcomes this challenge by ensuring that as soon as we see a sharp image of the reference mirror and the sample on the detector, we are within the same optical path length and thus within the coherence volume.

## Current State: Building the Prototype and Optical Setup

We are currently in the process of building a prototype for the simplified OCT system. The setup eliminates the need for an optical table and instead is mounted on a foam mat, allowing for easier operation and portability.

### TwinLAB Integration

Johannes will tell you more about it. Here you can find some links and thoughts:

https://www.asp.uni-jena.de/digital-teaching/xr-twinlab


![](./IMAGES/grafik_gesamt.png)

Sources:
https://github.com/Lichtwerkstatt/XRTL_SPA

The idea would be to integrate the UC2 system into this framework

### CAD

The Inventor DEsign Files can be found in the folder [INVENTOR](./INVENTOR)
The STL printing files can be found in the folder [STL](./STL)

![OPU Lower](./INVENTOR/InventorScreen.png)

![OPU Lower](./INVENTOR/IMG_20230712_125434.jpg)


### Reference Mirror

The optical setup consists of a minimal number of optical components. The reference mirror (M2) is mounted on a linear stage, enabling forward and backward movement to scan the coherence volume. It is also kinematically held to align the beam with respect to the sample. The entire scanning process will be motorized to minimize vibrations caused by manual movements.

### Light Source

Currently, we are using a Superlum SLD (Superluminescent Diode) as the light source. However, it would be interesting to explore the use of an LED due to their lower cost. For spatial incoherence, a LED with a small emitter could be considered to minimize the visible interference range. The SLD is collimated using lens L1 to illuminate the mirrors and the sample.

### Imaging Optics

The beam splitter cube or the 50% reflective mirror (approximately 1mm thick) divides and recombines the beam paths of the Michelson interferometer before passing through the 100mm objective lens (L2) and the 50mm tube lens, which takes the form of a CCTV lens. The resulting image is captured by a CMOS camera (Deheng IMX 226).

### Sample

In its simplest form, the sample is represented by a mirror mounted on a micrometer XYZ stage, allowing for controlled movement in space. To facilitate interference, it is advisable to kinematically mount the sample as well, ensuring precise alignment and stability during scanning.
### Setting up and Adapting

To disassemble the OPU, you can remove the metal plate at the back and the detection lens using Philips screwdrivers.

The back of the OPU features a complex and precisely adjusted "confocal" microscope:

![OPU Lower](./IMAGES/OPU_Lower.png)
*Bottom View*

To attach this unit to a 3D printed assembly, we will enlarge the holes where the lens used to be, making them M3-sized, and then incorporate the assembly into a UC2 insert:

![3D Printed Assembly](./IMAGES/AF_6.jpg)

The Xiao camera module can be adapted using another 3D printed mechanism (customizable to your needs). It's worth noting that the astigmatism is not parallel to the case of the OPU, so it may be necessary to adjust the angle by rotating the camera. Additionally, the focus may be slightly closer than the plastic cap (black) of the camera module allows.

![Xiao Camera Module](./IMAGES/AF_7.jpg)

We create an initial prototype as follows:

![Prototype](./IMAGES/AF_8.jpg)

It is advisable to mount the XIAO camera securely to prevent damage to the flatband cable:

![Secure Mounting](./IMAGES/AF_9.jpg)

The laser diode can be directly powered by the 3V3 supply voltage or controlled using a transistor for on/off switching in the code.

![Laser Diode Setup](./IMAGES/AF_12.jpg)


## Current State: Building the Prototype

We are currently in the advanced stages of constructing the prototype for our simplified OCT system, and several significant milestones have been accomplished:

### Achievements

1. **System Alignment:** We have successfully achieved a satisfactory level of system alignment, ensuring that all the optical components are properly positioned for optimal performance.

2. **Mirror Focusing:** Precise focusing of the mirrors has been achieved, contributing to enhanced imaging quality and accurate interference patterns.

3. **Tip Tilt Optimization:** We have effectively optimized the tip and tilt of the mirrors. This meticulous adjustment has resulted in improved beam steering, critical for obtaining clear interference fringes.

4. **Interference Fringe Generation:** By meticulously aligning the reference mirror and the sample arm, we have managed to generate distinct interference fringes, a pivotal step towards achieving high-resolution OCT imaging.

5. **Motor Control Script:** We have developed a custom script, OCT_motor_movement, which facilitates the control of the motor. Parameters such as speed and the number of steps per second (nSteps) can be adjusted through this script.

6. **Dephasing Control:** The motor movement script allows precise control over dephasing. With a duration of approximately 4 seconds, it covers a range from -nSteps//2 to +nSteps//2, contributing to comprehensive data collection.

7. **Camera Image Acquisition:** We have successfully acquired images using the camera software, Galaxy View. Utilizing the plugin for videos and image saving, we convert the images into TIFF stacks for further processing.

8. **Post-Processing Script:** We have developed the OCT_post_process script, designed to demodulate the stack of acquired images. This script aids in extracting meaningful information from the raw data.

### Upcoming Tasks

1. **Demodulation Testing:** The demodulation script, designed to process the collected data, is poised for testing. Initial results indicate its potential effectiveness, and we are eager to refine it further.

2. **Sample Demodulation Testing:** We intend to initiate testing with a sample, evaluating the demodulation script's performance under practical conditions.

Through these achievements and ongoing efforts, our prototype OCT system is progressing towards its full operational potential, offering simplified setup and enhanced imaging capabilities.

### Code

Luckily we don't need a lot of code. Essentially we will have 3 steppers rotating the thumbscrews of the kinematic mirror mount. Then there is a non-captive stepper motor translating the linear stage.

#### Kinematic mirror mount

These are 28byj-48  stepper motors and will be driven using a ULN2003 board hooked up to our UC2-ESP firmware. The **FIRMWARE**: https://github.com/youseetoo/uc2-esp32/tree/main/main

*Three steppers mounted to the insert*
![](./IMAGES/IMG_20230706_132532.jpg)

*All motor drivers hooked up the ESP32 controlled by UC2-ESP*
![](./IMAGES/IMG_20230706_132516.jpg)

*Module in Action*
![](./IMAGES/IMG_20230630_154302.jpg)

You can access them using the `Rotataor` class: https://github.com/youseetoo/uc2-esp32/blob/main/main/src/rotator/Rotator.cpp

**The pincofiguration** is determined here:
https://github.com/youseetoo/uc2-esp32/blob/main/main/PinConfig.h#L427
You can download the code, import it into Visual Studio's Platform.io, compile and upload it to the ESP32 board and connect the 3 ULN2003 boards to the following pins:

```cpp
    // ESP32-WEMOS D1 R32
    int ROTATOR_X_0 = GPIO_NUM_13;
    int ROTATOR_X_1 = GPIO_NUM_14;
    int ROTATOR_X_2 = GPIO_NUM_12;
    int ROTATOR_X_3 = GPIO_NUM_27;
    int ROTATOR_Y_0 = GPIO_NUM_26;
    int ROTATOR_Y_1 = GPIO_NUM_33;
    int ROTATOR_Y_2 = GPIO_NUM_25;
    int ROTATOR_Y_3 = GPIO_NUM_32;    
    int ROTATOR_Z_0 = GPIO_NUM_5;
    int ROTATOR_Z_1 = GPIO_NUM_19;
    int ROTATOR_Z_2 = GPIO_NUM_18;
    int ROTATOR_Z_3 = GPIO_NUM_21;  
```

If everything goes right, you can control the motors using our web-gui that is available here: https://youseetoo.github.io/indexWebSerialTest.html

You can control the steppers using the following python code:

In Python code that means (after `pip install UC2-REST`):

```py
import uc2rest
import numpy as np
import time

port = "unknown"

ESP32 = uc2rest.UC2Client(serialport=port, DEBUG=True)
# setting debug output of the serial to true - all message will be printed
ESP32.serial.DEBUG=True

#%%
# test Rotators
ESP32.rotator.move_x(steps=10000, speed=10000, is_blocking=True)
ESP32.rotator.move_y(steps=1000, speed=1000, is_blocking=True, is_enabled=False)
ESP32.rotator.move_z(steps=1000, speed=1000, is_blocking=True)
ESP32.rotator.move_y(steps=1000, speed=1000, is_blocking=True, is_enabled=False)
ESP32.rotator.move_t(steps=1000, speed=1000)
```


#### XYZ Stage

This video should describe some of the details for the stage's operation:

![](https://img.youtube.com/vi/E_hhclFqx5g/sddefault.jpg)

Depending how you will connect the stepper to the ESP you can simply use the flashing tool and upload the latest firmware (https://youseetoo.githu.io)

You can also use the web-tool to move the motor (https://youseetoo.github.io/indexWebSerialTest.html).


In Python code that means (after `pip install UC2-REST`):

```py
import uc2rest
import numpy as np
import time

port = "unknown"

ESP32 = uc2rest.UC2Client(serialport=port, DEBUG=True)
# setting debug output of the serial to true - all message will be printed
ESP32.serial.DEBUG=True

#%%
# test motor
ESP32.motor.move_x(steps=10000, speed=10000, is_blocking=True)
ESP32.motor.move_y(steps=1000, speed=1000, is_blocking=True, is_enabled=False)
ESP32.motor.move_z(steps=1000, speed=1000, is_blocking=True)
```

#### Camera

We use a Daheng camera. For this we would need to download the drivers:
https://dahengimaging.com/downloads/Galaxy_Windows_EN_32bits%2064bits_1.23.2305.9161.zip

After installation, you will have access to the Galaxy Viewer to get the image stream.

We can also read out frames in Python. For this we have the option to use the camera in ImSwitch. Alternatively, you can simply use the UC2-REST library shown above and some simple python lines (see also [the python SDK](Python SDK))


```py
# version:1.0.1905.9051
import gxipy as gx
from PIL import Image


def main():
    # print the demo information
    print("")
    print("-------------------------------------------------------------")
    print("Sample to show how to acquire mono image continuously and show acquired image.")
    print("-------------------------------------------------------------")
    print("")
    print("Initializing......")
    print("")

    # create a device manager
    device_manager = gx.DeviceManager()
    dev_num, dev_info_list = device_manager.update_device_list()
    if dev_num is 0:
        print("Number of enumerated devices is 0")
        return

    # open the first device
    cam = device_manager.open_device_by_index(1)

    # exit when the camera is a color camera
    if cam.PixelColorFilter.is_implemented() is True:
        print("This sample does not support color camera.")
        cam.close_device()
        return

    # set continuous acquisition
    cam.TriggerMode.set(gx.GxSwitchEntry.OFF)

    # set exposure
    cam.ExposureTime.set(10000)

    # set gain
    cam.Gain.set(10.0)

    # start data acquisition
    cam.stream_on()

    # acquire image: num is the image number
    num = 1
    for i in range(num):
        # get raw image
        raw_image = cam.data_stream[0].get_image()
        if raw_image is None:
            print("Getting image failed.")
            continue

        # create numpy array with data from raw image
        numpy_image = raw_image.get_numpy_array()
        if numpy_image is None:
            continue

        # show acquired image
        img = Image.fromarray(numpy_image, 'L')
        img.show()

        # print height, width, and frame ID of the acquisition image
        print("Frame ID: %d   Height: %d   Width: %d"
              % (raw_image.get_frame_id(), raw_image.get_height(), raw_image.get_width()))

    # stop data acquisition
    cam.stream_off()

    # close device
    cam.close_device()

if __name__ == "__main__":
    main()

```



#### Image Processing

Ultimatively, the goal is to capture a stack of images while the refernce arm is moving alon ghte optical path difference. Then image processing will help you to recover the reflection map of your sample.



## Safety

**LASER Safety/Radition** Never watch into the source directly. You may hurt your eye. Always be careful!

**Risk of Squeezing fingers** Don't hurt your fingers!



## When Goal is met?

- Control the setup using your computer
- Think about an integration into the TWINLab https://www.asp.uni-jena.de/digital-teaching/xr-twinlab
- get interference fringes
- align the system to get an OCT signal
- acquire a image stack and process it

## Ressources
- https://hackaday.com/2021/02/02/dvd-optics-power-this-scanning-laser-microscope/


## Future and outlook

In conclusion, the development of the "common-path" OCT prototype has marked a significant step forward, though it has also revealed critical areas for improvement. The initial design, hindered by a vulnerability to vibrations due to the lengthy reference and sample arms and the tuning fork-like mounting of mirrors and samples, needed rethinking. The recommendation to miniaturize the setup into a single cube, eliminating potential sources of reduced mechanical stiffness, has proven to be a wise direction.

![](IMAGES/IMG_20230730_151609.jpg)


The innovative one-cube design, featuring a reference arm with z-only positioning and kinematically mounted other arm, cleverly couples a non-captive motor with a TMC stepper motor. This approach has helped to overcome the vibrational challenges associated with previous A4988 stepper drivers. Although the mounting of real samples remains an open question and subject for future experimentation, the current setup is undoubtedly more stable and more straightforward to realize.

The openOCT project's future looks promising, with a newfound focus on robustness and precision. By continuing to address the challenges identified and adapting the prototype accordingly, there is immense potential for achieving a state-of-the-art system that could redefine OCT technology. The pathway towards miniaturization and stability has already begun to be paved, opening exciting possibilities for research and applications.
In the future we definitely want to replace the SLD with an LED due to supply chain issues

### Results

First results on in-cube OCT with the TMC motor controller and the Superlum SLD:

![](IMAGES/incubeOCT_TMC.gif)

![](IMAGES/incubeOCT_TMC_highcontrast.gif)


## Results

Raw-data can be found here:
10.5281/zenodo.8196533

```python
import numpy as np
import matplotlib.pyplot as plt
```

```python
from skimage import io
im = io.imread('stack140.tif')
```


```python
plt.imshow(im[20,:,:])
```




    <matplotlib.image.AxesImage at 0x22e77248848>




![png](IMAGES/results/output_3_1.png)



```python
im_cut=im[:,120:1050,700:1500]
```


```python
plt.plot(im_cut[:,300,700])
```




    [<matplotlib.lines.Line2D at 0x22e774f3608>]




![png](IMAGES/results/output_5_1.png)



```python
ans=[]
stack0=im_cut[:,300,500]*1.0
for i in range(0,stack0.shape[0]-5):
    valTemp=np.power(stack0[i+1]-stack0[i+3],2)-np.multiply((stack0[i]-stack0[i+2]),(stack0[i+2]-stack0[i+4]))
    ans.append(valTemp)
```


```python
plt.plot(ans)
```




    [<matplotlib.lines.Line2D at 0x22e770c1b88>]




![png](IMAGES/results/output_7_1.png)



```python
plt.imshow(im_cut[31,:,:])
```




    <matplotlib.image.AxesImage at 0x22e77564fc8>




![png](IMAGES/results/output_8_1.png)



```python
size = im_cut.shape
im_stack=im_cut.reshape((size[0],size[1]*size[2]))


```


```python
size
```




    (35, 930, 800)




```python
plt.plot(im_stack[2,:])
```




    [<matplotlib.lines.Line2D at 0x22e7717de08>]




![png](IMAGES/results/output_11_1.png)



```python
stack0 = im_stack
```


```python
im_ft = np.fft.fft(im_cut,None,0)
```


```python
plt.imshow(np.abs(im_ft[17,:,:]))
```




    <matplotlib.image.AxesImage at 0x22e8908c248>




![png](IMAGES/results/output_14_1.png)



```python
ans=[]
stack0=im_cut[:,:,:]*1.0
for i in range(0,size[0]-5):
# i = 0
    valTemp=np.power(stack0[i+1,:]-stack0[i+3,:],2)-np.multiply((stack0[i,:]-stack0[i+2,:]),(stack0[i+2,:]-stack0[i+4,:]))
    ans.append(valTemp)
    #print(pixel[i+2])
# print('Distance:')
#print(q)

```


```python
ans=[]
stack0=im_cut[:,:,:]*1.0
for i in range(0,size[0]-5):
# i = 0
    valTemp=np.power(stack0[i+1,:]-stack0[i+3,:],2)-np.power((stack0[i,:]-stack0[i+2,:]),2)
    ans.append(valTemp)
    #print(pixel[i+2])
# print('Distance:')
#print(q)
```


```python
stack0.shape
```




    (35, 930, 800)




```python
out = np.vstack(ans)
size2=out.shape
size2[0]
```




    27900




```python
out.shape
out2 = out.reshape((35-5,930,800))
plt.imshow(out2[0,:,:])
```




    <matplotlib.image.AxesImage at 0x22e771e9f88>




![png](IMAGES/results/output_19_1.png)



```python
out.shape
```




    (27900, 800)




```python
for q in range (1,37):
    pixel2=pixel0[::q]

    #plt.plot(pixel2)

    ans=[]
    pixel=pixel2*1.0
    for i in range(1,len(pixel)-5):
        valTemp=np.power(pixel[i+2]-pixel[i+4],2)-np.multiply((pixel[i-1]-pixel[i+3]),(pixel[i+3]-pixel[i+5]))
        ans.append(valTemp)
        #print(pixel[i+2])
    print('Distance:')
    print(q)
    plt.figure()
    plt.plot(ans)
    plt.show()
```


```python
stack0.shape
```




    (660, 40000)




```python
pixel0=im[:,553,933]
#
print(pixel0.shape)
plt.plot(pixel0)
```

    (660,)





    [<matplotlib.lines.Line2D at 0x2ac8a71f7c8>]




![png](IMAGES/results/output_23_2.png)



```python

for q in range (1,37):
    pixel2=pixel0[::q]

    #plt.plot(pixel2)

    ans=[]
    pixel=pixel2*1.0
    for i in range(1,len(pixel)-5):
        valTemp=np.power(pixel[i+2]-pixel[i+4],2)-np.multiply((pixel[i-1]-pixel[i+3]),(pixel[i+3]-pixel[i+5]))
        ans.append(valTemp)
        #print(pixel[i+2])
    print('Distance:')
    print(q)
    plt.figure()
    plt.plot(ans)
    plt.show()
```

    Distance:
    1



![png](IMAGES/results/output_24_1.png)


    Distance:
    2



![png](IMAGES/results/output_24_3.png)


    Distance:
    3



![png](IMAGES/results/output_24_5.png)


    Distance:
    4



![png](IMAGES/results/output_24_7.png)


    Distance:
    5



![png](IMAGES/results/output_24_9.png)


    Distance:
    6



![png](IMAGES/results/output_24_11.png)


    Distance:
    7



![png](IMAGES/results/output_24_13.png)


    Distance:
    8



![png](IMAGES/results/output_24_15.png)


    Distance:
    9



![png](IMAGES/results/output_24_17.png)


    Distance:
    10



![png](IMAGES/results/output_24_19.png)


    Distance:
    11



![png](IMAGES/results/output_24_21.png)


    Distance:
    12



![png](IMAGES/results/output_24_23.png)


    Distance:
    13



![png](IMAGES/results/output_24_25.png)


    Distance:
    14



![png](IMAGES/results/output_24_27.png)


    Distance:
    15



![png](IMAGES/results/output_24_29.png)


    Distance:
    16



![png](IMAGES/results/output_24_31.png)


    Distance:
    17



![png](IMAGES/results/output_24_33.png)


    Distance:
    18



![png](IMAGES/results/output_24_35.png)


    Distance:
    19



![png](IMAGES/results/output_24_37.png)


    Distance:
    20



![png](IMAGES/results/output_24_39.png)


    Distance:
    21



![png](IMAGES/results/output_24_41.png)


    Distance:
    22



![png](IMAGES/results/output_24_43.png)


    Distance:
    23



![png](IMAGES/results/output_24_45.png)


    Distance:
    24



![png](IMAGES/results/output_24_47.png)


    Distance:
    25



![png](IMAGES/results/output_24_49.png)


    Distance:
    26



![png](IMAGES/results/output_24_51.png)


    Distance:
    27



![png](IMAGES/results/output_24_53.png)


    Distance:
    28



![png](IMAGES/results/output_24_55.png)


    Distance:
    29



![png](IMAGES/results/output_24_57.png)


    Distance:
    30



![png](IMAGES/results/output_24_59.png)


    Distance:
    31



![png](IMAGES/results/output_24_61.png)


    Distance:
    32



![png](IMAGES/results/output_24_63.png)


    Distance:
    33



![png](IMAGES/results/output_24_65.png)


    Distance:
    34



![png](IMAGES/results/output_24_67.png)


    Distance:
    35



![png](IMAGES/results/output_24_69.png)


    Distance:
    36



![png](IMAGES/results/output_24_71.png)



```python
plt.plot(pixel2)
```




    [<matplotlib.lines.Line2D at 0x2ac52d46648>]




![png](IMAGES/results/output_25_1.png)



```python
ans=[]
pixel=pixel2*1.0
for i in range(1,len(pixel)-5):
    valTemp=np.power(pixel[i+2]-pixel[i+4],2)-np.multiply((pixel[i-1]-pixel[i+3]),(pixel[i+3]-pixel[i+5]))
    ans.append(valTemp)
    #print(pixel[i+2])

plt.plot(ans)
```




    [<matplotlib.lines.Line2D at 0x2ac52e1bf48>]




![png](IMAGES/results/output_26_1.png)



```python

```




    [<matplotlib.lines.Line2D at 0x2ac52c12388>]




![png](IMAGES/results/output_27_1.png)



```python
import os
os.getcwd()
```




    'C:\\ProgramData\\Galaxy\\userdata\\ImagesAndVideos\\hackaday\\MER2-230-168U3M(FDG22050153)'



## License
