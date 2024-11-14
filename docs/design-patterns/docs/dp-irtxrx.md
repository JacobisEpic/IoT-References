# IR Communications Background

We'll cover the following

1. IR signal, LOS
2. Modulation – OOK
3. Carrier – noise immunity (chipset)
4. How to drive the beacon – H-bridge
5. FOV at source, emitter
6. UART – same comms model, using different pins


## On-Off Keying, and with Manchester Encoding

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/c/cb/Biphase_Mark_Code.svg" width="80%">
</p>
<p align="center">
<i> OOK Modulation </i>
</p>

## Modulated On-Off Keying TV Remote

<p align="center">
<img src="/docs/images/ir-uart.png" width="90%">
</p>
<p align="center">
<i> On-off keying and-gated with carrier</i>
</p>

## H-Bridge -- Two Inputs

<p align="center">
<img src="/docs/images/driver-enable.png" width="40%">
</p>
<p align="center">
<i> H-Bridge Logic </i>
</p>


## IR LED
Looks like a regular white LED. You can replace the LED with a visible one (e.g., RED) and see it flickering at 1200 baud. 

## IR Receiver Module

<p align="center">
<img src="/docs/images/schematic-TSOP.png" width="70%">
</p>
<p align="center">
<i> On-off keying and-gated with carrier</i>
</p>

## And UART

<p align="center">
<img src="https://upload.wikimedia.org/wikipedia/commons/2/24/UART_timing_diagram.svg" width="100%">
</p>
<p align="center">
<i> UART Data Pattern</i>
</p>

```c

uart_config_t uart_config =
{
        .baud_rate = 115200,
        .data_bits = UART_DATA_8_BITS,
        .parity    = UART_PARITY_DISABLE,
        .stop_bits = UART_STOP_BITS_1,
        .flow_ctrl = UART_HW_FLOWCTRL_DISABLE
}

```

<p align="center">
<img src="/docs/images/scope-uart.png" width="100%">
</p>
<p align="center">
<i>UART TX Signal</i>
</p>

## Reading and Reference Material
- [IR Receiver Diode - TSOP38238](https://www.sparkfun.com/products/10266)
- [IR LED - 950nm](https://www.sparkfun.com/products/9349)
- [Wiki Modulation](https://en.wikipedia.org/wiki/Modulation)
- [Wiki OOK](https://en.wikipedia.org/wiki/On-off_keying)
- [Wiki Optical Communications](https://en.wikipedia.org/wiki/Optical_communication)
