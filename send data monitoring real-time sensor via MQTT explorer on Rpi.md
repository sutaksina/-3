import paho.mqtt.publish as publish
import sys
import Adafruit_DHT
import time
hostname = "127.0.1.1" //IP hostname ค้นหาโดยการรันhostname -i ลงในterminal
port = 1883
auth = {
   'username':'puieiei', //ชื่อuserของเรา
   'password':'puirpi' //passwordของเรา
}
sensor = 11
pin = 4

while True:
  humidity, temperature = Adafruit_DHT.read_retry(sensor, pin)
  if humidity is not None and temperature is not None:
    publish.single("pui/test",'Temp={0:0.1f}*C  Humidity={1:0.1f}%'.format(temperature, humidity), hostname=hostname, port=port, auth=auth)//"pui/testคือtopicที่ใช้ส่งข้อมูลตั้งได้ตามใจ
    print 'sending...'
    time.sleep(2)
  else:
    print 'Failed to get reading. Try again!'
