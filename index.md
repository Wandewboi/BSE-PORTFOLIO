# Pet Planter Project
A smart plant pot that can record humidity and temperature and upload that data to io.adafruit.com. It alerts the user when the soil is too dry or moist and the user can adjust the too-low or too-high levels using 5 pre-programmed profiles.

| Andrew B. | Sacred Heart Cathedral Prepratory| Aerospace Engineering | Incoming Sophmore

<!--- **Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.** 

![Headstone Image](logo.svg)-->

  
# Final Milestone
My final milestone for my base project was the completion of a profile system, which allows the user to customize the water alert levels using 5 different pre-programmed profiles. I did this by prompting the user to input an integer 1-5, and based on that changing the alert values. The program also punishes the user with a very loud sound that doesn't stop until unplugged if they input anything other than 1,2,3,4 or 5. 

I initially tried implementing this solution with some touchscreen buttons because I thought my screen had touchscreen functionality. It didn't so now the user selects the setting based on keyboard input. This milestone marks the end of my core project, however, I still plan to add a self-watering system that will use an Arduino and valve.


<iframe width="560" height="315" src="https://www.youtube.com/embed/KSlwN_RVnXo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Second Milestone
My second milestone is getting the planter software to work and interface with adafruit.io. I had to download a few libraries and download them onto the pcb's drive. I encountered quite a few issues in this step that led to almost a full day of troubleshooting. The first thing that I did wrong was updating the pcb to the incorrect version of circuit python. I fixed that by flashing a different version of circuit python. The real issue that I encountered was the default code that was provided in the kit. The first issue was with an argument name. In one of the setup folders, an argument was called aio_username, but in the code, it was called aio_name, something that took me a long time to catch. After I fixed that, I kept getting an issue that caused the pcb to  be unable to read sensor data, which caused the program to crash because ada fruit io was set up in a way where it would kick the user off if new data wasn't being added at least once every 60 seconds. This was solved by deleting a portion of faulty code. I also changed the low water warning to something a bit funnier. My next step is adding a profile system so the user can select what type of plant they have and have the water alerts change based on that.
<iframe width="560" height="315" src="https://www.youtube.com/embed/wMOQiFmWf6o" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# First Milestone
My first milestone is the assembly of my planters pcb, sensor, speaker and body. The first thing I did was assemble my pcb, which entalied plugging in some ribbon cables. My second process was attaching my sensor to a mounting mechanism and plugging in the cable that would attach to the pcb. I then assembled my planters body, which was 3d printed. I first attached the pot to the drip tray, then attached it to the housing. Then, I attached my sensor to the assembled body and attacehd the pcb and screen to the body. I then attached the back part to finish the physical aspect of this project.

The assembly was pretty straight forward and simple, except attaching the speaker cable to the pcb. The cable was exteremly short and was therefore very tense when attaching. It was also a very small and fragile cable, which would be very easy to break. My next step is programing the software for the planter.
<iframe width="560" height="315" src="https://www.youtube.com/embed/bPSWvVxIx5k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Completion Of Starter Project
My first milestone is the completion of my starter project, that being the useless box. The function of the box is essentially to have no function (except perhaps pinching the user), as no items can be taken out or placed inside it. The box does this by contaning a switch that when flipped, causes a mechanical arm to be raised which hits the switch, lowering the arm and closing the box. The basic components of the box are the box itself, a pcb, a motor and a plastic arm. I had an issue while soldering components to the pcb which caused multiple short circuits. After I replaced the pcb, I had an issue with my motor, where it wasn't generationg enough torque to push the switch. I fixed this by replacing the motor. However, after doing this, I found that the motor was too powerful, causing the lid of the box to stay open. I solved this by putting some tape on the sides of the hinge.

<iframe width="560" height="315" src="https://www.youtube.com/embed/WVR7KuA-kq8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>








<!--
# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. --->

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```python
void setup() {
import time
import adafruit_sdcard
import board
import busio
from digitalio import DigitalInOut
import adafruit_esp32spi.adafruit_esp32spi_socket as socket
from adafruit_esp32spi import adafruit_esp32spi, adafruit_esp32spi_wifimanager
import adafruit_imageload
import displayio
import neopixel
from adafruit_bitmap_font import bitmap_font
from adafruit_display_text.label import Label
from adafruit_io.adafruit_io import IO_MQTT
import adafruit_minimqtt.adafruit_minimqtt as MQTT
from adafruit_pyportal import PyPortal
from adafruit_seesaw.seesaw import Seesaw
from simpleio import map_range
import digitalio


#---| User Config |---------------

NUMBER_OF_TIMES_PLANT_HAS_BEEN_ABUSED=0
# How often to poll the soil sensor, in seconds
# Polling every 30 seconds or more may cause connection timeouts
DELAY_SENSOR = 1


# How often to send data to adafruit.io, in minutes
DELAY_PUBLISH = 10



#Maximum Temp
MAX_TEMP=95


#MIN TEMP
MIN_TEMP=38
#---| End User Config |---------------


# Background image
BACKGROUND = "/images/roots.bmp"
# Icons for water level and temperature
ICON_LEVEL = "/images/icon-wetness.bmp"
ICON_TEMP = "/images/icon-temp.bmp"
WATER_COLOR = 0x16549E


# Audio files
wav_water_high = "/sounds/water-high.wav"
wav_water_low = "/sounds/water-low.wav"
PUNISH = "\sounds\you-are-an-idiot.wav"
# the current working directory (where this file is)
cwd = ("/"+__file__).rsplit('/', 1)[0]




# Get wifi details and more from a secrets.py file
try:
    from secrets import secrets
except ImportError:
    print("WiFi secrets are kept in secrets.py, please add them there!")
    raise


# Set up i2c bus
i2c_bus = busio.I2C(board.SCL, board.SDA)


# Initialize soil sensor (s.s)
ss = Seesaw(i2c_bus, addr=0x36)

relay = digitalio.DigitalInOut(board.D4)
relay.direction = digitalio.Direction.OUTPUT



# PyPortal ESP32 AirLift Pins
esp32_cs = DigitalInOut(board.ESP_CS)
esp32_ready = DigitalInOut(board.ESP_BUSY)
esp32_reset = DigitalInOut(board.ESP_RESET)


spi = busio.SPI(board.SCK, board.MOSI, board.MISO)
esp = adafruit_esp32spi.ESP_SPIcontrol(spi, esp32_cs, esp32_ready, esp32_reset)
status_light = neopixel.NeoPixel(board.NEOPIXEL, 1, brightness=0.2)
wifi = adafruit_esp32spi_wifimanager.ESPSPI_WiFiManager(esp, secrets, status_light)


# Initialize PyPortal Display
display = board.DISPLAY


WIDTH = board.DISPLAY.width
HEIGHT = board.DISPLAY.height


# Initialize new PyPortal object
pyportal = PyPortal(esp=esp,
                    external_spi=spi)
# Plant Profile
x=int(input("Please input a number 1-4, 1 indicating your plant doesn't need much water and 5 indicating the opposite"))


if x  == 1:
        SOIL_LEVEL_MIN=100
        SOIL_LEVEL_MAX=350
elif x == 2:
        SOIL_LEVEL_MIN=150
        SOIL_LEVEL_MAX=425
elif x == 3:
        SOIL_LEVEL_MIN=250
        SOIL_LEVEL_MAX=470
elif x==4:
        SOIL_LEVEL_MIN=400
        SOIL_LEVEL_MAX=530

elif x > 5:
        print("Alright, what about the number 1,2,3,4 and 5 do you not understand? I mean did you even graduate pre school? If so, they should really revoke your diploma. I mean the world is wasting it's time and money making sure that your plumbing and internet work. Why you thought you could use a command line is honestly beyond me. Stupid. What is your blood type? A-? Failure. Not even A+. Now suffer the worst sound known to human kind ")
        while True:
             pyportal.play_file(PUNISH)
SOIL_LEVEL_OPTIMAL= (SOIL_LEVEL_MAX+SOIL_LEVEL_MIN)/2
# Set backlight level
pyportal.set_backlight(0.5)


# Create a new DisplayIO group
splash = displayio.Group()


# show splash group
display.show(splash)


# Palette for water bitmap
palette = displayio.Palette(2)
palette[0] = 0x000000
palette[1] = WATER_COLOR
palette.make_transparent(0)


# Create water bitmap
water_bmp = displayio.Bitmap(display.width, display.height, len(palette))
water = displayio.TileGrid(water_bmp, pixel_shader=palette)
splash.append(water)


print("drawing background..")
# Load background image
try:
    bg_bitmap, bg_palette = adafruit_imageload.load(BACKGROUND,
                                                    bitmap=displayio.Bitmap,
                                                    palette=displayio.Palette)
# Or just use solid color
except (OSError, TypeError):
    BACKGROUND = BACKGROUND if isinstance(BACKGROUND, int) else 0x000000
    bg_bitmap = displayio.Bitmap(display.width, display.height, 1)
    bg_palette = displayio.Palette(1)
    bg_palette[0] = BACKGROUND
bg_palette.make_transparent(0)
background = displayio.TileGrid(bg_bitmap, pixel_shader=bg_palette)


# Add background to display
splash.append(background)


print('loading fonts...')
# Fonts within /fonts/ folder
font = cwd+"/fonts/GothamBlack-50.bdf"
font_small = cwd+"/fonts/GothamBlack-25.bdf"


# pylint: disable=syntax-error
data_glyphs = b'0123456789FC-* '
font = bitmap_font.load_font(font)
font.load_glyphs(data_glyphs)


font_small = bitmap_font.load_font(font_small)
full_glyphs = b'0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ-,.: '
font_small.load_glyphs(full_glyphs)


# Label to display Adafruit IO status
label_status = Label(font_small)
label_status.x = 305
label_status.y = 10
splash.append(label_status)


# Create a label to display the temperature
label_temp = Label(font)
label_temp.x = 35
label_temp.y = 300
splash.append(label_temp)


# Create a label to display the water level
label_level = Label(font)
label_level.x = display.width - 130
label_level.y = 300
splash.append(label_level)


print('loading icons...')
# Load temperature icon
icon_tmp_bitmap, icon_palette = adafruit_imageload.load(ICON_TEMP,
                                                        bitmap=displayio.Bitmap,
                                                        palette=displayio.Palette)
icon_palette.make_transparent(0)
icon_tmp_bitmap = displayio.TileGrid(icon_tmp_bitmap,
                                     pixel_shader=icon_palette,
                                     x=0, y=280)
splash.append(icon_tmp_bitmap)


# Load level icon
icon_lvl_bitmap, icon_palette = adafruit_imageload.load(ICON_LEVEL,
                                                        bitmap=displayio.Bitmap,
                                                        palette=displayio.Palette)
icon_palette.make_transparent(0)
icon_lvl_bitmap = displayio.TileGrid(icon_lvl_bitmap,
                                     pixel_shader=icon_palette,
                                     x=315, y=280)
splash.append(icon_lvl_bitmap)


# Connect to WiFi
label_status.text = "Connecting..."
while not esp.is_connected:
    try:
        wifi.connect()
    except (RuntimeError, ConnectionError) as e:
        print("could not connect to AP, retrying: ",e)
        wifi.reset()
        continue
print("Connected to WiFi!")


# Initialize MQTT interface with the esp interface
MQTT.set_socket(socket, esp)


# Initialize a new MQTT Client object
mqtt_client = MQTT.MQTT(broker="io.adafruit.com",
                        username=secrets["aio_username"],
                        password=secrets["aio_key"])


# Adafruit IO Callback Methods
# pylint: disable=unused-argument
def connected(client):
    # Connected function will be called when the client is connected to Adafruit IO.
    print('Connected to Adafruit IO!')


def subscribe(client, userdata, topic, granted_qos):
    # This method is called when the client subscribes to a new feed.
    print('Subscribed to {0} with QOS level {1}'.format(topic, granted_qos))


# pylint: disable=unused-argument
def disconnected(client):
    # Disconnected function will be called if the client disconnects
    # from the Adafruit IO MQTT broker.
    print("Disconnected from Adafruit IO!")


# Initialize an Adafruit IO MQTT Client
io = IO_MQTT(mqtt_client)


# Connect the callback methods defined above to the Adafruit IO MQTT Client
io.on_connect = connected
io.on_subscribe = subscribe
io.on_disconnect = disconnected


# Connect to Adafruit IO
print("Connecting to Adafruit IO...")
io.connect()
label_status.text = " "
print("Connected!")


fill_val = 0.0
def fill_water(fill_percent):
    """Fills the background water.
    :param float fill_percent: Percentage of the display to fill.


    """
    assert fill_percent <= 1.0, "Water fill value may not be > 100%"
    # pylint: disable=global-statement
    global fill_val


    if fill_val > fill_percent:
        for _y in range(int((board.DISPLAY.height-1) - ((board.DISPLAY.height-1)*fill_val)),
                        int((board.DISPLAY.height-1) - ((board.DISPLAY.height-1)*fill_percent))):
            for _x in range(1, board.DISPLAY.width-1):
                water_bmp[_x, _y] = 0
    else:
        for _y in range(board.DISPLAY.height-1,
                        (board.DISPLAY.height-1) - ((board.DISPLAY.height-1)*fill_percent), -1):
            for _x in range(1, board.DISPLAY.width-1):
                water_bmp[_x, _y] = 1
    fill_val = fill_percent


def display_temperature(temp_val, is_celsius=False):
    """Displays the temperature from the STEMMA soil sensor
    on the PyPortal Titano.
    :param float temp: Temperature value.
    :param bool is_celsius:


    """
    if not is_celsius:
        temp_val = (temp_val * 9 / 5) + 32 - 15
        print('Temperature: %0.0fF'%temp_val)
        label_temp.text = '%0.0fF'%temp_val
        return int(temp_val)
    else:
        print('Temperature: %0.0fC'%temp_val)
        label_temp.text = '%0.0fC'%temp_val
        return int(temp_val)


# initial reference time
initial = time.monotonic()
while True:
   
    now = time.monotonic()
    





    print("reading soil sensor...")
    # Read capactive
    moisture = ss.moisture_read()
    label_level.text = str(moisture)

    # Read temperature
    temp = ss.get_temp()
    temp = display_temperature(temp)

    # Convert into percentage for filling the screen
    moisture_percentage = map_range(float(moisture), SOIL_LEVEL_MIN, SOIL_LEVEL_MAX, 0.0, 1.0)



    # fill display
    print("filling disp..")
    fill_water(moisture_percentage)
    print("disp filled..")


    print("temp: " + str(temp) + "  moisture: " + str(moisture))


    # Play water level alarms
    if moisture <= SOIL_LEVEL_MIN:
        print("Playing low water level warning...")
        #pyportal.play_file(wav_water_low)
        relay.value= True
        time.sleep(1)
        print("Opening Valve")
    elif moisture >= SOIL_LEVEL_OPTIMAL:
         relay.value= False
         time.sleep(2)
    elif moisture >= SOIL_LEVEL_MAX:
        print("Playing high water level warning...")
        pyportal.play_file(wav_water_high)
    
    if NUMBER_OF_TIMES_PLANT_HAS_BEEN_ABUSED >10:
         pyportal.play

    if now - initial > (DELAY_PUBLISH * 1):
        try:
            print("Publishing data to Adafruit IO...")
            label_status.text = "Sending to IO..."
            io.publish("moisture", moisture)
            io.publish("temperature", temp)
            print("Published")
            label_status.text = "Data Sent!"


            # reset timer
            initial = now
        except (ValueError, RuntimeError, ConnectionError, OSError) as e:
            label_status.text = "ERROR!"
            print("Failed to get data, retrying...\n", e)
            wifi.reset()
    time.sleep(DELAY_SENSOR)

```
# Bill of Materials
<!---Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs.--> 

| **Part** | **Note** | **Price** | **Link** |

| Arduino Uno | Power Supply | $5.95 | <a href="https://www.adafruit.com/product/501"> Link </a> |

| Pyportal Titano | Screen and Logic Board | $59.95 | <a href="https://www.adafruit.com/product/4444"> Link </a> |

| Adafruit STEMMA Soil Sensor | Moisture Detection | $7.50 | <a href="https://www.adafruit.com/product/4026"> Link </a> |

| Mini Oval Speaker | For Alerts | $1.95 | <a href="https://www.adafruit.com/product/3923"> Link </a> |

| STEMMA Cable | Cable to Connect PCB to Sensor | $0.75 | <a href="https://www.adafruit.com/product/3568"> Link </a> |

| Black Nylon Machine Screw and Stand-off Set | Assortment of Screws | $16.95 | <a href="https://www.adafruit.com/product/3299"> Link </a> |

| USB Type A to Type C Cable | To Connect Power Supply to PCB | $4.95 | <a href="https://www.adafruit.com/product/4474"> Link </a> |


| HFS (R) 12v Dc Electric Solenoid Valve | To control water flow | $13.99 | <a href="https://www.amazon.com/HFS-Electric-Solenoid-Valve-Water/dp/B018WRJYPY/ref=pd_ci_mcx_mh_mcx_views_0?pd_rd_w=gPWu1&content-id=amzn1.sym.0250fb24-4363-44d0-b635-ac15f859c3b5&pf_rd_p=0250fb24-4363-44d0-b635-ac15f859c3b5&pf_rd_r=0NK049FRG1Z8AQV7VBC2&pd_rd_wg=nafEh&pd_rd_r=be837bb8-2024-4515-abf9-af52dc62d3f4&pd_rd_i=B018WRJYPY"> Link </a> |
|:--:|:--:|:--:|:--:|
| Relay Module | Passing on instructions from circuit python board to solenoid. | $8.99 | <a href="https://www.amazon.com/CHENBO-Channel-Module-Shield-Arduino/dp/B07874KSLY/ref=asc_df_B07874KSLY/?tag=hyprod-20&linkCode=df0&hvadid=242010397888&hvpos=&hvnetw=g&hvrand=6854958547700363721&hvpone=&hvptwo=&hvqmt=&hvdev=c&hvdvcmdl=&hvlocint=&hvlocphy=9032171&hvtargid=pla-405732959949&psc=1"> Link </a>  |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a "href="https://www.amazon.com/MCIGICM-15SQ045-Schottky-Blocking-Diodes/dp/B07NS63XJH/ref=sr_1_3?keywords=diode&qid=1687450556&sr=8-3"> Link </a> |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
|:--:|:--:|:--:|:--:|




<!--- # Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here. -->

