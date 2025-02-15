# SOCAT for Serial Comms Testing

The STM32 Inverted Pendulum project is an example of where the
serial port on a microcontroller board is used as part of the
application.  This means that using the standard debug over 
serial/VCOM/USB conflicts with the application behaviour.

One solution is to configure a second UART/USART on the board
to function independently of the debug/VCOM port.  This can 
require additional hardware.

A convenient alternative strategy is to invoke the `socat`
program which can link the actual serial device to a 
socket so that we can tee off the bidirectional data without
the application behaviour being significantly changed (down to
possible timing differences).

```
sudo socat -x PTY,link=/dev/ttyV1,raw,echo=0,crnl,group-late=dialout,mode=660 /dev/ttyACM0,b230400,raw,echo=0,crnl
```

