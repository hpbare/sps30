# SPS30
Portable C driver for the Sensirion SPS30 particulate matter sensor.

## Features
- Supports both UART/SHDLC and I2C interfaces.
- Hardware abstraction via HAL callbacks for read/write/delay/flush.
- Measurement control: start, stop, sleep, wake, reset.
- Reads PM concentrations and particle number data.
- Reads status, version, serial number, and device info.
- No OS-specific dependencies; usable in embedded and host projects.

## Supported protocols
- UART: SHDLC protocol.
- I2C: Sensirion I2C protocol.

## Typical usage
```c
SPS30_Dev dev = {
    .protocol = SPS30_PROTOCOL_UART,
    .fmt      = SPS30_FORMAT_FLOAT,
    .state    = SPS30_STATE_IDLE,
    .hal.uart = {
        my_uart_read,
        my_uart_write,
        my_delay_ms,
        my_uart_flush_rx
    }
};

SPS30_Init(&dev);
SPS30_StartMeasurement(&dev);

SPS30_Data data;
SPS30_ReadMeasurement(&dev, &data);

SPS30_StopMeasurement(&dev);
```

## Example
A working UART example is provided in `example/sps30_eg_uart.c`.

## Notes
- The sensor requires a warm-up period before valid readings are available.
- UART communication uses SHDLC framing and includes checksum validation.
- The driver expects the caller to provide the platform-specific I/O layer.

## License
See the [LICENSE](./LICENSE) file.
