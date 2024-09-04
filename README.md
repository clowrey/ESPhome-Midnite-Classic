
<img src="https://github.com/user-attachments/assets/ba8363a7-4b55-46d3-a947-f0b1c2634309" width=40% height=40%>


Recommended hardware https://shop.m5stack.com/products/atomic-rs232-base-w-o-atom-lite


also get the S3 Nano Lite for a total less than $20 https://shop.m5stack.com/products/atoms3-lite-esp32s3-dev-kit


<img src="https://github.com/user-attachments/assets/61d543c1-f6c2-4192-aaae-f4c8ebd4f595" width=50% height=50%>


<img src="https://github.com/user-attachments/assets/ed473efa-b41e-4859-ba22-4957d99729a6" width=50% height=50%>

Example response to MODBUS request https://midniteftp.com/forum/index.php?topic=4880.30

Modbus debugging terminal tool https://github.com/ClassicDIY/ModbusTool

NodeRed example https://flows.nodered.org/flow/b1e47c5b460931c4407d662fbb4ed85f

<img src="https://github.com/user-attachments/assets/ab5bd3e6-311f-4b11-b49e-4b123c795ced" width=70% height=70%>

<img src="https://github.com/user-attachments/assets/9bf73787-1a18-4118-97fd-0974a79dd33c" width=70% height=70%>

I use the middle port which also includes 9V output to power it. Connect RX=TX, TX=RX. 

<img src="https://github.com/user-attachments/assets/31c895c0-dd7c-45ff-8b5f-bc68f252754a" width=50% height=50%>

Debugging example:
```yaml
uart:
  id: mod_bus
  tx_pin: GPIO5
  rx_pin: GPIO6
  baud_rate: 19200
  stop_bits: 1
  rx_buffer_size: 384
  debug: # Minimal debug configuration example, logs hex strings by default
    after:
      bytes: 1500 #max bytes
      timeout: 1s #max timeout - default 150ms
      delimiter: "\r"
      #delimiter: [0xCF, 0x6F] #list of bytes to send the serial data on BF E7 EF EB
      #delimiter: [0x6F, 0xEF] #list of bytes to send the serial data on         #F8 72 6F EF CF

    #dummy_receiver: true #necessary to log data if no other device is using this serial port
    sequence:
      - lambda: |-
          UARTDebug::log_string(direction, bytes);
```

The midnite clssic is by default on dddress 10 decimal not hex.
Hardware layer is via RS232 RX/TX lines not A/B type RS-485
Baud rate is 19200
