```python
import numpy as np
import matplotlib.pyplot as plt
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    <ipython-input-209-bd177e4be8d7> in <module>
          1 import numpy as np
          2 import matplotlib.pyplot as plt
    ----> 3 import napari


    ModuleNotFoundError: No module named 'napari'



```python
import napari
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    <ipython-input-211-1e1049a33073> in <module>
    ----> 1 import napari


    ModuleNotFoundError: No module named 'napari'



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
