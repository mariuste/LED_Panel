# LED light panel with adjustable color temperature
# Project Parameters
Name: "LED light panel with adjustable color temperature"
Description: "USB-C powered LED Light with adjustable brigthness and color temperature"
Short Name: "LED Panel"
Github Name: "LED_Panel"
PCB Name: "LED_Panel"

# Description
/TODO/

# ToDos
- create requirements
- define critical components (MCU, poti, Mosfets, emc)
- define mechanical constraints (dimensios glass, mounting priciple, screw positios)
- create 3D Mockup
- create schematic
- create layout


# Specification for LED_board

## Usage
- plug in -> LED will go to last setting (maybe slight fade) if sw is on
- on/off switch integrated in poti 1
- turn poti 1 for adjusting brightness
- turn poti 2 for adjusting light color

## HMI
- Large Pot for brightness and on/off
- Small Poti for light color

## LEDs
- LEDs can be divided every 13mm; 608 LED per meter (304 per color); 22W per meter
- three rows of 130mm strips

## Core Function
- create soft light and adjust light color

## Software
- brightness and light color controlled via two PWM MOSFETs


### Fault handling
- not enough voltage/power from USB-C: light pattern to indicate error

## Software
- loop: read USB-PD for available power, read poti, set brightness and color

## Power concept
- LEDs: 22W/m -> 3 * 130mm * 22W = 8.58W // 715mA@12V -> with 80%DCDC: 686mA@15V / 515mA@20V
- USB-PD board set to 15V, >= 1.0A (15W)
- DC/DC to regulate 15V to 12V, 1A
- when switch is off-> reset USB PD

## Mechanics
- acryl from https://expresszuschnitt.de (170mm * 90mm * 4mm, rounded corner of 8mm radius)
- M4 mounting to enclosure
- M4 mounting for mounting plate (75 * 75)




# Part selection
- MCU: STM32L011F3U6TR
- Poti /w switch: P091S-FC20BR10K
- Poti /wo Switch: P091N-FC25BR10K
- LED: COB44-079  by LED24
- USB: UJC-HP2-3-SMT-TR

- Regulator: TPS62932DRLR
- Inductor: 7447709150

- MOSFET: SI1308EDL-T1-GE3
- LDO: NCP716MT30TBG

- USBPD: STUSB4500

obsolet (could replace DC/DC and MOSFET):
- LED-driver: TPS92200D2RXLR ? AL8861Y-13 ? IS31LT3350-V1SDLS2-TR

# Preliminary pinmapping
## USB-PD IC
- SDA PB7
- SCL PB6
- reset PD PA9 (OUT)
- alarm in PA10 (IN)

## Debuging (GPIOS)
- GPIO1 PC14
- GPIO2 PC15

## Debugging (SWD)
- SWDIO PA13
- SWCLK PA14

## Poti Readback (Vref: 1.224V)
- Poti1 PA0 (AIN0)
- Poti2 PA4 (AIN4)

## PWM outputs
- LED1 PA5 (TIM2_CH1)
- LED2 PA1 (TIM2_CH2)

