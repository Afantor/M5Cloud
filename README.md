# M5Stack Web IDE

## ���ٿ�ʼ

### 1. ��¼�̼�
#### Windows��¼
Windowsʹ��Espressif�ṩFlash Download Tools������¼([�������](http://espressif.com/sites/default/files/tools/flash_download_tools_v3.6.2.2_0.rar))����������(�Ȳ�������¼)��
  ![image](docs/img/windows_esptool.png) 


#### MacOS/Linux��¼
- ʹ��pip��װesptool��

    ```pip install esptool```

- ��¼bin�ļ�:

    ``` esptool.py --chip esp32 --port /dev/tty.SLAB_USBtoUART write_flash -z 0x1000 firmware.bin ```

### 2. ���豸WiFi��������
- **����1:** ʹ���ȵ���룬ͨ��Web��������
  - �ֻ����������M5Stack Core��Ļ��ʾ��WiFi�ȵ�
  ![image](docs/img/img_startup_ap.JPG)

    ����M5Stack Core WiFi��

    ![image](docs/img/wificonnect.png)
  - ���������½ 192.168.4.1����WiFi��SSID������
  ![image](docs/img/wifisetup.jpg)
  
- **����2:** ͨ����������WiFi����

    ͨ������REPL�����ϴ��������豸��Ŀ¼�´���һ������Ϊ��config.json���ļ����ļ���wifi�����ò���JSON��ʽ���£�
    ```
    {
        "wifi":{
            "ssid":"MasterHax_2.4G",
            "password":"12345678"
        }
    }
    ```
- **����3:** ͨ��΢��ɨ���ά��Airkiss����

  TODO

### 3. ���豸
  ��½ http://io.m5cloud.com ע���˺�,����豸��

  ![image](docs/img/add.jpg)

  ��M5Stack Core��Ļ��ʾ��Check Code������豸��Check Code��һ��������ģ�60���ˢ��һ�Σ����������豸����֤��

  ![image](docs/img/img_conncet-suc.JPG)
  
  ![image](docs/img/checkcode.jpg)



### 4. ��ʼ���
![image](docs/img/ide_uploads.jpg)

# **M5Stack** Micropython

Micropython ��������

## **LCD**

---

��ʹ��LCDǰ���ȵ���LCD����:

```python
from m5stack import lcd
lcd.print('hello world!')
```

Ҳ����ֱ��������

```python
import m5stack
m5stack.lcd.print('hello world!')
```

����������

```python
import m5stack
lcd = m5stack.lcd
lcd.print('hello world!')
```


#### ��ɫ

LCD��**Color** ��ɫʹ�� **24bit** �������ͱ�ʾ��RGB��Ӧ��8bit��

����: **0xFF0000** ��������ȫ��ɫ��**0x00FF00** ������ԭ��ɫ��ɫ��

���õ���ɫ����ֱ���ö��嵽�Ĳ���: 

**BLACK, NAVY, DARKGREEN, DARKCYAN, MAROON, PURPLE, OLIVE, LIGHTGREY, DARKGREY, BLUE, GREEN, CYAN, RED, MAGENTA, YELLOW, WHITE, ORANGE, GREENYELLOW, PINK**

��������LCD��ӡһ����ɫ��hello world����������
```python
lcd.print('hello world', color=lcd.GREEN)
```

Ҳ����������
```python
lcd.print('hello world', color=0X00FF00)
```

### lcd.setColor(color [,bcolor])
����Ĭ�ϵĻ滭��ɫ�ͱ���ɫ��bcolorһ����������������ʾ�ı���ɫ��


### lcd.print(text, [x, y, color])

��ʾ�ַ��� *text* �� *(x, y)* ָ����λ�ã����� *color* Ϊ��ɫ������ 

��ע������������[x, y, color]�ڵ���ʾΪ��ѡ������

* **x**: ָ��ˮƽ�����λ����ʾ, �������������:
  * LASTX(Ĭ��), ֱ����һ���������ֽ�����ʾ
  * CENTER, ������ʾ�ı�
  * RIGHT, �Ҷ����ı�

* **y**: ָ����ֱ�����λ����ʾ, �������������:
  * LASTX(Ĭ��), ֱ����һ���������ֽ�����ʾ
  * CENTER, ������ʾ�ı�
  * BOTTOM, ���ֿ��ײ���ʾ

* **color**:����ò���δ���ã�Ĭ��Ϊ *lcd.setColor* ���õ���ɫ��



### lcd.println(text, [x, y, color])

lcd.println���������� *lcd.print* �������ܻ���һ����ֻ�ǻ�������Զ����С�

```python
lcd.print('hello world\n')
lcd.println('hello world') #��ʾЧ��һ��
```


### lcd.font(font)

��������.

����ʹ�����õ������Ѷ���õĲ���: 

**FONT_Default, FONT_DefaultSmall, FONT_DejaVu18, FONT_Dejavu24, FONT_Ubuntu, FONT_Comic, FONT_Minya, FONT_Tooney, FONT_Small, FONT_7seg**

```python
lcd.font(lcd.FONT_Dejavu24) #����ΪFONT_Dejavu24����
```

### lcd.textWidth(text)

�����ַ��� *text* ������ʾռ�õĿ�ȡ�


### lcd.fontSize()

������ǰ����� *width* �� *heigh*��


Example:

```python
from m5stack import lcd

 #����Ļ��hello world
lcd.print('hello world')

#����Ļx=10,y=100���ط���ʾhello world
lcd.print('hello world', 10, 100)

#��ʾ��������ɫΪ��ɫ��hello world
lcd.print('hello wrold', color=0xFF0000) 

#����Ļx=10,y=100���ط���ʾ��ɫ��hello world����
lcd.print('hello world', 10, 200, 0xFF0000) 

#��������ΪFONT_Dejavu24
lcd.font(lcd.FONT_Dejavu24)
lcd.println('hello world')
```


### lcd.pixel(x, y [,color])

��һ�����ص���ָ��λ�� (x,y). ��� *color* ����δ����, ��Ĭ��ʹ�� *lcd.setColor* ���õ�ǰ��ɫ.

### lcd.line(x, y, x1, y1 [,color])

��һ��ֱ�ߴ�����(x,y) �� (x1,y1). ��һ�����ص���ָ��λ�� (x,y). ��� *color* ����δ����, ��Ĭ��ʹ�� *lcd.setColor* ���õ�ǰ��ɫ.


### lcd.rect(x, y, width, height, [color, fillcolor])

��һ�����Σ�(x,y)Ϊ�������Ͻǵ���ʼ���꣬���� *width* �� *height* Ϊ���þ��εĿ�Ⱥ͸߶ȡ�

��� *color* �� ����δ����, ��Ĭ��ʹ�� *lcd.setColor* ���õ�ǰ��ɫ.

��ѡ���� *fillcolor* Ϊ���ε����ɫ��

```python
lcd.rect(10, 100, 100, 200, 0xFF0000) #�������ɫ
lcd.rect(10, 100, 100, 200, 0xFF0000, 0x00FF00) #�������ڲ�Ϊ��ɫ
```

### lcd.triangle(x, y, x1, y1, x2, y2 [,color, fillcolor])

��һ�������θ���ָ���������� (x,y), (x1,y1) and (x2,y2).


### lcd.circle(x, y, r [,color, fillcolor])

��һ��Բ�� ����(x,y)ΪԲ��ԭ�㣬*r* Ϊ�뾶.


### lcd.ellipse(x, y, rx, ry [opt, color, fillcolor])

��һ����Բ (x,y)�� (rx, ry) Ϊ��Բ����������.

**opt* ����������ʾ����, Ĭ���� 15, ��ʾ������Բ.

Multiple segments can drawn, combine (logical or) the values.
* 1 - upper left segment
* 2 - upper right segment
* 4 - lower left segment
* 8 - lower right segment

If *fillcolor* is given, filled elipse will be drawn.


### lcd.arc(x, y, r, thick, start, end [color, fillcolor])

��һ��Բ�����ĵ� (x,y)�� *r* Ϊ�뾶��*thick* Ϊ�ߵĺ�ȣ���ʼ�Ƕ� *start* �� *end* �Ƕȣ�0~360�ȣ���


### lcd.poly(x, y, r, sides, thick, [color, fillcolor, rotate])

��һ����������ĵ� (x,y)�� *r* Ϊ�뾶, ���� *sides* Ϊ����ε�������*thick* Ϊ�ߵĺ�ȡ�

��������� *rotate* ����, ������ת����εĽǶ� (0~359)


### lcd.roundrect(x, y, width, height, r [color, fillcolor])

Բ�Ǿ��β��� *r* ΪԲ�ǵİ뾶.


### lcd.clear([color]) 

�ȼ���lcd.fill([color])

Clear the screen with default background color or specific color if given.

�����Ļ��ʾ�����ݣ����ָ������ɫ��Ĭ���� *lcd.setColor* ���õı���ɫ��


### lcd.image(x, y, file [,scale, type])

��ʾͼƬ*file*��(x,y)Ϊ��ʼλ�� 
* ֧�� **JPG** and **BMP** ͼƬ��ʽ.
* Constants **lcd.CENTER**, **lcd.BOTTOM**, **lcd.RIGHT** can be used for x&y
* **x** and **y** values can be negative

**scale**: ͼƬ���ű���

**type**: ͼƬ������ *lcd.JPG* �� *lcd.BMP* 

## **Button**

---
```python
import m5stack as m5

def press_cb(pin):
    m5.lcd.println('button_press A')
    print('button_press A')
    
m5.BtnA.set_callback(press_cb)
```

���ߣ�

```python
import m5stack as m5

while True:    
  if m5.BtnA.press():
    m5.lcd.println('button_press A')
  time.sleep_ms(10)

```


## **SD Card**

---

```python
import uos

uos.mountsd()
uos.listdir('/sd')
```


## **Beep**

---

```python
import m5stack as m5

m5.beep.tone(freq=1800)
m5.beep.tone(freq=1800, timeout=200)
```

## **GPIO**

---

```python
import machine

pinout = machine.Pin(0, machine.Pin.OUT)
pinout.value(1)

pinin = machine.Pin(2, machine.Pin.IN)
val = pinin.value()
```

## **PWM**

---

```python
import machine

pwm = machine.PWM(machine.Pin(3))
pwm.freq(5000)
pwm.duty(666)
```


## **ADC**

---
```python
import machine

adc = machine.ADC(35)
adc.read()
```
