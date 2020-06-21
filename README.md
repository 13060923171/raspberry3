# raspberry3
树莓派温湿度传感器模块

**读取传感器数据**

树莓派最大的特点是它的40pin引脚可以提供丰富的扩展性能，而读取各种传感器的数值就是其中之一。下面我们将通过树莓派的GPIO脚来读取DHT22温湿度传感器的值。

DHT22温湿度传感器介绍：低成本的DHT温度和湿度传感器具有一般的基础功能、速度不快，但对于进行基本数据记录的爱好者来说非常适合。DHT传感器由两部分组成，即电容式湿度传感器和热敏电阻。 内部还有一个非常基本的芯片，它可以进行一些模数转换，并能读取温度和湿度的数字信号。 数字信号很容易用任何微控制器读取。

DHT22主要特点：

§ 3至5V电源和I/O

§ 转换期间最大电流为2.5mA

§ 适用于0-100％湿度读数，精度为2-5％

§ 适用于-40至125°C温度读数，精度为±0.5°C

§ 不超过0.5 Hz的采样率（每2秒一次）

§ 尺寸15.1mm x 25mm x 7.7mm

一般情况下，我们会在数据引脚和VCC引脚之间连接一个4.7K欧姆的上拉电阻。DHT22输出数据引脚将连接到树莓派的GPIO16。检查传感器连接到树莓派引脚的电路表，如下                                                                             
1、引脚1 – Vcc ==> 3.3V                                                            
2、引脚2 – 数据 ==> GPIO 16                                                        
3、引脚3 – 未连接                                                                  
4、引脚4 – Gnd ==> Gnd 

![](https://s1.ax1x.com/2020/06/21/N3an9U.png)

# 安装DHT库：

Adafruit 公司已经为旗下的数字式温湿度传感器提供了DHT 库。

**在树莓派终端输入以下命令：**

sudo git clone https://github.com/adafruit/Adafruit_Python_DHT.git

cd Adafruit_Python_DHT

**给 Python 2 和 Python 3 安装该库：**

sudo python setup.py install

sudo python3 setup.py install

源代码：

```python
import Adafruit_DHT
 
# Set sensor type : Options are DHT11,DHT22 or AM2302
DHT22Sensor = Adafruit_DHT.DHT22
 
# Set GPIO sensor is connected to
DHTpin = 16
 
# Use read_retry method. This will retry up to 15 times to
# get a sensor reading (waiting 2 seconds between each retry).
humidity, temperature = Adafruit_DHT.read_retry(DHT22Sensor, DHTpin)
 
#Reading the DHT11 is very sensitive to timings and occasionally
# the Pi might fail to get a valid reading. So check if readings are valid.
if humidity is not None and temperature is not None:
    print('Temp={0:0.1f}*C  Humidity={1:0.1f}%'.format(temperature, humidity))
else:
    print('Failed to get reading. Try again!')
```

最后运行结果应该是：

```python
Temp=25.0*C Humidity=46.0%
```