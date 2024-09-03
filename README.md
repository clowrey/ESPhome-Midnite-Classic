

Example response to MODBUS request https://midniteftp.com/forum/index.php?topic=4880.30

Modbus debugging terminal tool https://github.com/ClassicDIY/ModbusTool

NodeRed example https://flows.nodered.org/flow/b1e47c5b460931c4407d662fbb4ed85f

"
let battV = msg.payload[0] / 10
let battI = msg.payload[2] / 10
let arrayV = msg.payload[1] / 10
let arrayI = msg.payload[6] / 10
let statenum = msg.payload[5] >> 8
let hsTemp = msg.payload[19] / 10
let rtsTemp = msg.payload[17] / 10
let outPower = msg.payload[4]
let kWh = msg.payload[3] / 10

//change state values to match Tristar
if (statenum == 0) { statenum = 3 } // Off/Night
else if (statenum == 10) { statenum = 4 } // Fault
else if (statenum == 4) { statenum = 5 } // Bulk
else if (statenum == 3) { statenum = 6 } // Absorb
else if (statenum == 5 || statenum == 6) { statenum = 7 } // Float
else if (statenum == 7 || statenum == 18) { statenum = 8 } // Equalise

let siteID = msg.topic

msg.topic = "solar/"+siteID

msg.payload = {
    "battV": battV,
    "battI": battI,
    "arrayV": arrayV,
    "arrayI": arrayI,
    "state": statenum,
    "hsTemp": hsTemp,
    "rtsTemp": rtsTemp,
    "outPower": outPower,
    "kWh": kWh
}

return msg;


The midnite clssic is by default on dddress 10 decimal not hex.
Hardware layer is via RS232 RX/TX lines not A/B type RS-485
Baud rate is 19200
