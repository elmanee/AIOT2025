# AIOT2025 Unidad II
---

## Avtividad 1
- Sesion 1
  - KY-017
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, PWM
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    sensor_pin = 12  
    sensor = Pin(sensor_pin, Pin.IN)
    ledPin = Pin(2, Pin.OUT)
    ledPin.value(0)
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    
    client = subscribir()
    
    estado_anterior = sensor.value()
    
    while True:
        client.check_msg()  
        estado_actual = sensor.value()
      
      if estado_actual != estado_anterior:  
          if estado_actual == 1:
              print("✅ Posición vertical (Estado: 0)")
              client.publish(MQTT_TOPIC, "0")  
          else:
              print("⚠️ Posición inclinada (Estado: 1)")
              client.publish(MQTT_TOPIC, "1")  
      
      estado_anterior = estado_actual  
      sleep(1)
    ```
  - KY-027
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, PWM
    import time
    import network
    from umqtt.simple import MQTTClient
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    sensor_pin = 5  
    sensor = Pin(sensor_pin, Pin.IN)
    ledPin = Pin(16, Pin.OUT)
    ledPin.value(0)
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    
    client = subscribir()
    
    estado_anterior = sensor.value()
    
    while True:
        client.check_msg()  
        estado_actual = sensor.value()  
      
      if estado_actual != estado_anterior:  
          if estado_actual == 1:
              print("✅ Posición vertical (Estado: 1)")
              client.publish(MQTT_TOPIC, "1")  
          else:
              print("⚠️ Posición inclinada (Estado: 0)")
              client.publish(MQTT_TOPIC, "0")  
      
      estado_anterior = estado_actual  
      time.sleep(0.1)
  
  
    ```
- Sesion 2
  - KY-002
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, PWM
    import time
    import network
    from umqtt.simple import MQTTClient
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    Led = Pin(22, Pin.OUT)  
    PinSensor = Pin(18, Pin.IN)
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            Led.value(1)  
        elif msg == b'0':
            Led.value(0)  
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    
    wifi_connect()
    
    client = subscribir()
    
    estado_anterior = PinSensor.value()
    
    while True:
        client.check_msg() 
        estado_actual = PinSensor.value()  
      
      if estado_actual != estado_anterior: 
          if estado_actual == 1:  
              Led.value(1)  
              client.publish(MQTT_TOPIC, "1")  
          else:
              Led.value(0)  
              client.publish(MQTT_TOPIC, "0")  
  
          print("Cambio detectado:", estado_actual)  
          estado_anterior = estado_actual  
      
      time.sleep(0.1)  
    ```
  - KY-028
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    import network
    from time import sleep
    from umqtt.simple import MQTTClient
    from machine import Pin, ADC
    
    AO_PIN = ADC(Pin(35))  
    AO_PIN.atten(ADC.ATTN_11DB)
    
    led = Pin(2, Pin.OUT)  
    led.value(0)  
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        """Conectar a la red WiFi"""
        print("Conectando a WiFi", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
    
        for _ in range(30):  
            if sta_if.isconnected():
                print("\nWiFi conectada:", sta_if.ifconfig())
                return
            print(".", end="")
            sleep(0.3)
        
        print("\nError: No se pudo conectar a WiFi")
    
    def llegada_mensaje(topic, msg):
        """Callback para manejar mensajes MQTT"""
        print("Mensaje recibido:", msg)
        if msg == b'1':
            led.value(1)
        elif msg == b'0':
            led.value(0)
    
    def subscribir():
        """Conectar al broker MQTT y suscribirse al tópico"""
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=60)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a {MQTT_Broker}, suscrito a {MQTT_TOPIC}")
        return client
    
    wifi_connect()
    client = subscribir()
    
    ultimo_valor = None  
    
    while True:
        client.check_msg()  
        valor = AO_PIN.read() 
        temperaturaN = (valor / 4095.0) * 100  #
        temperaturaRedo = round(temperaturaN, 2) 
      
      print("Dato:", temperaturaRedo, "°C")
      
      if temperaturaRedo != ultimo_valor:
          print("Nueva temperatura detectada:", temperaturaRedo)
          client.publish(MQTT_TOPIC, str(temperaturaRedo))
          print("Dato publicado:", temperaturaRedo)
          
          led.value(1)
          sleep(0.2)
          led.value(0)
          
          ultimo_valor = temperaturaRedo
      
      sleep(1)  
    ```
- Sesion 3
  - KY-008
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    from umqtt.simple import MQTTClient
    import network
    
    led = Pin(2, Pin.OUT)  
    sensor = Pin(12, Pin.IN, Pin.PULL_UP)  
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        """Conectar a la red WiFi"""
        print("Conectando a WiFi", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
    
        for _ in range(30):  
            if sta_if.isconnected():
                print("\nWiFi conectada:", sta_if.ifconfig())
                return
            print(".", end="")
            sleep(0.3)
        
        print("\nError: No se pudo conectar a WiFi")
    
    def llegada_mensaje(topic, msg):
        """Callback para manejar mensajes MQTT"""
        print("Mensaje recibido:", msg)
        if msg == b'1':
            led.value(1)
        elif msg == b'0':
            led.value(0)
    
    def subscribir():
        """Conectar al broker MQTT y suscribirse al tópico"""
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=60)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a {MQTT_Broker}, suscrito a {MQTT_TOPIC}")
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()  

    valor = sensor.value()  
    
    if valor == 0:
        client.publish(MQTT_TOPIC, str("Laser bloqueado: LED ENCENDIDO"))
        led.value(1) 
    else:
        client.publish(MQTT_TOPIC, str("Laser detectado: LED APAGADO"))
        led.value(0)
    
    led.value(0)
    sleep(1)  
    ```
  - KY-
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    
    ```
- Sesion 4
  - KY-003
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    from umqtt.simple import MQTTClient
    import network
    
    sensor = Pin(4, Pin.IN, Pin.PULL_UP)
    led = Pin(2, Pin.OUT)  
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        """Conectar a la red WiFi"""
        print("Conectando a WiFi", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
    
        for _ in range(30):  
            if sta_if.isconnected():
                print("\nWiFi conectada:", sta_if.ifconfig())
                return
            print(".", end="")
            sleep(0.3)
        
        print("\nError: No se pudo conectar a WiFi")
    
    def llegada_mensaje(topic, msg):
        """Callback para manejar mensajes MQTT"""
        print("Mensaje recibido:", msg)
        if msg == b'1':
            led.value(1)
        elif msg == b'0':
            led.value(0)
    
    def subscribir():
        """Conectar al broker MQTT y suscribirse al tópico"""
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=60)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a {MQTT_Broker}, suscrito a {MQTT_TOPIC}")
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        try:
            client.check_msg()  
        except OSError as e:
            print("Error MQTT:", e)
            client = subscribir()  

    valor = sensor.value()
    
    if valor == 0:
        client.publish(MQTT_TOPIC, "1") 
        led.value(1)
    else:
        client.publish(MQTT_TOPIC, "0")  
        led.value(0)
        
    sleep(1)
    ```
  - KY-012
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    import network
    from time import sleep
    from umqtt.simple import MQTTClient
    from machine import Pin
    
    buzzer = Pin(18, Pin.OUT)  
    led = Pin(2, Pin.OUT)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        """Conectar a la red WiFi"""
        print("Conectando a WiFi", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
    
        for _ in range(30):  
            if sta_if.isconnected():
                print("\nWiFi conectada:", sta_if.ifconfig())
                return
            print(".", end="")
            sleep(0.3)
        
        print("\nError: No se pudo conectar a WiFi")
    
    def llegada_mensaje(topic, msg):
        """Callback para manejar mensajes MQTT"""
        print("Mensaje recibido:", msg)
        if msg == b'1':
            led.value(1)
        elif msg == b'0':
            led.value(0)
    
    def subscribir():
        """Conectar al broker MQTT y suscribirse al tópico"""
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=60)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a {MQTT_Broker}, suscrito a {MQTT_TOPIC}")
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        buzzer.value(1)
        led.value(1)
        client.publish(MQTT_TOPIC, "1")  
        print("Estado: ON - Buzzer activado")
        sleep(0.5)
    
    buzzer.value(0)
    led.value(0)
    client.publish(MQTT_TOPIC, "0")  
    print("Estado: OFF - Buzzer desactivado")
    sleep(1)
    
    client.check_msg()  

    ```
- Sesion 5
  - KY-018
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, ADC
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    ledPin = Pin(2, Pin.OUT)
    ledPin.value(0)
    
    sensor_luz = ADC(Pin(34))
    sensor_luz.atten(ADC.ATTN_11DB)  
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    
    client = subscribir()
    
    estado_anterior = sensor_luz.read()
    while True:
        client.check_msg()
    
    valor = sensor_luz.read()
    
    if valor != estado_anterior:
        print(f"Intensidad lumínica: {valor}")
        client.publish(MQTT_TOPIC, str(valor))
    
    estado_anterior = valor
    sleep(0.5)
    ```
  - KY-019
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    RELAY_PIN = 14
    relay = Pin(RELAY_PIN, Pin.OUT)
    estado_actual = 0  
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando a WiFi", end="")
        sta = network.WLAN(network.STA_IF)
        sta.active(True)
        sta.connect("MARCOS 3310", "123456789")
    
    while not sta.isconnected():
        print(".", end="")
        sleep(0.3)
    print("\nWiFi conectada! IP:", sta.ifconfig()[0])

    def mqtt_callback(topic, msg):
        global estado_actual
        mensaje = msg.decode().lower()
    
    if mensaje == "on":
        relay.value(1)
        estado_actual = 1
        client.publish(MQTT_TOPIC, "RELAY_ON")
        print("Relé ACTIVADO")
    elif mensaje == "off":
        relay.value(0)
        estado_actual = 0
        client.publish(MQTT_TOPIC, "RELAY_OFF")
        print("Relé DESACTIVADO")

    def mqtt_connect():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=60)
        client.set_callback(mqtt_callback)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a MQTT: {MQTT_Broker}")
        return client
    
    
    wifi_connect()
    client = mqtt_connect()
    client.publish(MQTT_TOPIC, "Sistema_Iniciado")  
        
    while True:
        client.check_msg()
        sleep(0.1)
    ```
- Sesion 6
  - KY-021
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    SENSOR_PIN = 14  
    sensor = Pin(SENSOR_PIN, Pin.IN, Pin.PULL_UP)  
    led = Pin(2, Pin.OUT)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            sleep(0.3)  
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            led.value(1)  
        elif msg == b'0':
            led.value(0)  
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()  
    
    estado = sensor.value()
    
    if estado == 0:
        client.publish(MQTT_TOPIC, "1")
        led.value(1)
        print("Estado: 1 - Imán detectado 🧲")
    else:
        client.publish(MQTT_TOPIC, "0")
        led.value(0)
        print("Estado: 0 - Buscando...")
    
    sleep(0.2)
    ```
  - KY-024
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, ADC
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    HALL_ANALOG = 34   
    led = Pin(2, Pin.OUT)
    
    analog_pin = ADC(Pin(HALL_ANALOG))
    analog_pin.atten(ADC.ATTN_11DB)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()
        valor_actual = analog_pin.read() 
    
    client.publish(MQTT_TOPIC, str(valor_actual))
    print("Publicado:", valor_actual)
    
    sleep(1)
    ```
- Sesion 7
  - KY-025
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    sensor = Pin(14, Pin.IN, Pin.PULL_UP)  
    led = Pin(2, Pin.OUT)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()

    estado = sensor.value()  
    
    if estado == 0:
        led.value(1)
        client.publish(MQTT_TOPIC,"Detectado")
       
    else:
        led.value(0)
        client.publish(MQTT_TOPIC,"No detectado")
    
    sleep(0.5)
    ```
  - KY-026
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    FLAME_PIN = 14  
    led = Pin(2, Pin.OUT)
    sensor = Pin(FLAME_PIN, Pin.IN)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()

    estado = sensor.value()  
    
    if estado == 0:
        client.publish(MQTT_TOPIC, "Llama detectada")
        led.value(1)
        
    else:
        client.publish(MQTT_TOPIC,"Sin llama")
        led.value(0)

    sleep(0.5)
    ```
- Sesion 8
  - KY-034
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    HALL_PIN = 14
    led = Pin(2, Pin.OUT)
    sensor = Pin(HALL_PIN, Pin.IN, Pin.PULL_UP)
    
    MQTT_BROKER = "192.168.137.233"
    MQTT_PORT = 1883
    MQTT_TOPIC = "utng/cm"
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando a WiFi", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        
        if not sta_if.isconnected():
            sta_if.connect("MARCOS 3310", "123456789")
            while not sta_if.isconnected():
                print(".", end="")
                sleep(0.3)
        
        print("\nWiFi conectada!")
        print("IP:", sta_if.ifconfig()[0])
    
    def llegada_mensaje(topic, msg):
        print(f"Mensaje: {msg.decode()} desde {topic.decode()}")
        if msg == b'1':
            led.value(1)
        elif msg == b'0':
            led.value(0)
    
    def mqtt_connect():
        client = MQTTClient(CLIENT_ID, MQTT_BROKER, port=MQTT_PORT)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a MQTT: {MQTT_BROKER}")
        return client
    
    try:
        wifi_connect()
        client = mqtt_connect()
        
        while True:
            client.check_msg()
            estado = sensor.value()
            
            mensaje = "ALERTA_MAGNETICA" if estado == 0 else "NORMAL"
            client.publish(MQTT_TOPIC, mensaje)
            print("Estado:", mensaje)
            
            led.value(0 if estado else 1)
            sleep(0.5)
    
    except Exception as e:
        print("Error crítico:", e)
        machine.reset()
    ```
  - KY-035
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    HALL_PIN = 14
    led = Pin(2, Pin.OUT)
    sensor = Pin(HALL_PIN, Pin.IN, Pin.PULL_UP)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()
    
        estado = sensor.value()
            
        mensaje = "ALERTA_MAGNETICA" if estado == 0 else "NORMAL"
        client.publish(MQTT_TOPIC, mensaje)
        print("Estado:", mensaje)
            
        led.value(0 if estado else 1)
        sleep(0.5)
    ```
- Sesion 9
  - KY-039
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin, ADC
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    sensor = ADC(Pin(34))  
    sensor.atten(ADC.ATTN_11DB)
    led = Pin(2, Pin.OUT)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    def wifi_connect():
        print("Conectando", end="")
        sta_if = network.WLAN(network.STA_IF)
        sta_if.active(True)
        sta_if.connect("MARCOS 3310", "123456789")
        while not sta_if.isconnected():
            print(".", end="")
            time.sleep(0.3)
        print("\nWiFi conectada")
    
    def llegada_mensaje(topic, msg):
        print("Mensaje recibido:", msg)
        if msg == b'1':
            ledPin.value(1)  
        elif msg == b'0':
            ledPin.value(0)
    
    def subscribir():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT, keepalive=0)
        client.set_callback(llegada_mensaje)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print("Conectado a %s, suscrito a %s" % (MQTT_Broker, MQTT_TOPIC))
        return client
    
    wifi_connect()
    client = subscribir()
    
    while True:
        client.check_msg()
        valor = sensor.read()
            
        print(valor)
        client.publish(MQTT_TOPIC, str(valor))
    
        sleep(1)
    ```
  - KY-040
  - Videos y un flujo JSON. [Videos](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
  - Diagrama de conexión. [Link](https://app.cirkitdesigner.com/project/49a9701f-8221-4eb5-8f83-a209cd198ce3)
  - Codigo
    ```
    from machine import Pin
    from time import sleep
    import network
    from umqtt.simple import MQTTClient
    
    CLK_PIN = 14  
    DT_PIN = 12    
    SW_PIN = 13    
    
    clk = Pin(CLK_PIN, Pin.IN, Pin.PULL_UP)
    dt = Pin(DT_PIN, Pin.IN, Pin.PULL_UP)
    sw = Pin(SW_PIN, Pin.IN, Pin.PULL_UP)
    
    MQTT_Broker = "192.168.137.233"
    MQTT_TOPIC = "utng/cm"
    MQTT_PORT = 1883
    MQTT_CLIENT_ID = "cliente_unico_1"
    
    ultimo_estado = clk.value()
    ultimo_boton = 1
    
    def wifi_connect():
        print("Conectando a WiFi", end="")
        sta = network.WLAN(network.STA_IF)
        sta.active(True)
        sta.connect("MARCOS 3310", "123456789")
        
        while not sta.isconnected():
            print(".", end="")
            sleep(0.3)
        print("\nWiFi conectada! IP:", sta.ifconfig()[0])
    
    def mqtt_callback(topic, msg):
        print(f"Mensaje recibido: {msg.decode()}")
    
    def mqtt_connect():
        client = MQTTClient(MQTT_CLIENT_ID, MQTT_Broker, port=MQTT_PORT)
        client.set_callback(mqtt_callback)
        client.connect()
        client.subscribe(MQTT_TOPIC)
        print(f"Conectado a MQTT: {MQTT_Broker}")
        return client
    
    wifi_connect()
    client = mqtt_connect()
    
    while True:
        estado_actual = clk.value()
        if estado_actual != ultimo_estado:
            if dt.value() != estado_actual:
                client.publish(MQTT_TOPIC, "HORARIO")
                print("Giro horario detectado")
            else:
                client.publish(MQTT_TOPIC, "ANTIHORARIO")
                print("Giro antihorario detectado")
            ultimo_estado = estado_actual
        
        estado_boton = sw.value()
        if estado_boton != ultimo_boton:
            if estado_boton == 0:
                client.publish(MQTT_TOPIC, "BOTON")
                print("Botón presionado")
                sleep(0.5)  
            ultimo_boton = estado_boton
        
        client.check_msg()
        sleep(0.01)
    ```
---
## Actividad 2
- Figura
---
## Actividad 3
### Curos *JavaScript Fundamentals 2*
  - Link de curso . [Curso](https://drive.google.com/drive/folders/1th2CfdkuDAnleux_esrkI1_HvYIbwpvy?usp=sharing)
---
