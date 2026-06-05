# STM32-AD7173-Data-Acquisition
STM32F4 reads 16-channel ADC AD7173 via SPI, sends data over USB Virtual COM port, and controls PWM motor driver. LabVIEW GUI for data visualization.

# STM32 + AD7173 16-Channel Data Acquisition

This project reads 16 channels from **AD7173** 32-bit ADC using **STM32F4** over SPI and sends data to PC via USB Virtual COM Port.  
A **LabVIEW** GUI visualizes and logs the data.

## Features
- 16 differential/SE channels
- 10 kHz PWM motor driver (TIM1)
- USB CDC (Virtual COM Port)
- Control commands over USB:
  - `0x09` – Start acquisition
  - `0x02` – Stop motors and exit
- Status bits in received byte control left/right motors

## Folder Structure
- `Keil_STM32/` – Full Keil uVision project (tested on STM32F407)
- `LabVIEW/` – LabVIEW 2020 GUI (.vi files)
- `Docs/` – AD7173 datasheet, schematic, register map

## Hardware
- MCU: STM32F407VET6
- ADC: AD7173 (Analog Devices)
- SPI: 10.5 MHz, Mode 3 (CPOL=1, CPHA=1)
- USB: Full Speed (Virtual COM Port)

## How to Use
1. Open Keil project, compile, flash to STM32.
2. Connect USB to PC – should appear as COM port.
3. Run LabVIEW GUI, select COM port, press "Start".
4. Send `0x09` from any serial tool or LabVIEW to begin reading.

## Known Issues
- Current firmware reads only 1 channel due to loop bug. Fix: change `for(i=0;i<1;i++)` to `for(ch=0;ch<16;ch++)` in `getMainData()`.

## License
MIT – feel free to use and modify.
