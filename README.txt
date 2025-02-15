STM32F4 Discovery & ILI9341 TFT with XPT2046 Touch Controller

This project demonstrates the integration of an ILI9341 TFT LCD display with
an STM32F4 Discovery board, including touch functionality using the 
XPT2046 resistive touch controller. The firmware is developed in
C using STM32 HAL libraries, and SPI communication is used to interface with the peripherals.

----------------------------------------------------------------------------------------------

🛠 Hardware Used

STM32F407 Discovery Board

ILI9341 TFT LCD Display (240x320, 2.4-inch)

XPT2046 Touch Controller

SPI Communication for Display & Touch

SPI1 for ILI9341 Display Control

SPI2 for XPT2046 Touch Controller

----------------------------------------------------------------------------------------------

🔧 Key Features

Display initialization and graphical rendering

Touch input processing via XPT2046

Coordinate mapping to match the display resolution

Optimized SPI communication for efficient data transfer

----------------------------------------------------------------------------------------------

🛠 Circuit Connections

	LCD  	      STM32F4	

SPI1 for ILI9341 Display Control

	LCD_CS_PIN -- GPIOA_PIN_4
	LCD_RST_PIN -- GPIOA_PIN_6
	LCD_DC_PIN -- GPIOC_PIN_4
	LCD_SCK -- SPI1_SCK (PA5)
	LCD_MOSI -- SPI1_MOSI (PA7)
	LCD_LED -- STM32_VCC
	LCD_VCC	-- STM32_VCC
	LCD_GND -- STM32_GND
	
SPI2 for XPT2046 Touch Controller

	XPT2046_SCK (T_CLK) -- SPI2_SCK (PB13)
	XPT2046_MISO (T_D0) -- SPI2_MISO (PB14)
	XPT2046_MOSI (T_DIN) -- SPI2_MOSI (PB15)
	XPT2046_CS (T_CS) -- GPIOB_PIN_12
	XPT2046_IRQ (T_IRQ) -- NaN
	

----------------------------------------------------------------------------------------------

🖥️ Libraries

for ILI9341 Display Control

	Inc	fonts.h
		ILI9341_GFX.h
		ILI9341_STM32_Driver.h
	
	Src	fonts.c
		ILI9341_GFX.c
		ILI9341_STM32_Driver.c

for XPT2046 Touch Controller
	
	Inc	xpt2946.h

	Src	xpt2046.c

----------------------------------------------------------------------------------------------

🖥️ Installation & Setup

Clone the repository:

git clone <repository_link>

Open the project in STM32CubeIDE or your preferred IDE.

Connect the STM32F4 Discovery board via USB.

Compile and flash the firmware using an ST-Link debugger.

Power up and test the display & touch functionality.

----------------------------------------------------------------------------------------------

🚀 Issues Encountered & Fixes

1. Incorrect Touch Mapping

Issue: Touch coordinates did not match the display orientation.

Fix: Adjusted RAW_MIN_X, RAW_MAX_X, RAW_MIN_Y, RAW_MAX_Y values in xpt2046.h to correctly map the coordinates for a 240x320 resolution.

2. Inverted X/Y Axis

Issue: Touch response was flipped along one or both axes.

Fix: Configured XPT2046_MIRROR_X and XPT2046_MIRROR_Y in xpt2046.h.

3. SPI Communication Instability

Issue: Occasional miscommunication between STM32 and peripherals.

Fix: Increased SPI clock stability and adjusted NSS handling in xpt2046.c.

	SPI2 Baud Rate = 1.125 MBits/s
	SPI2 Prescaler = 32
	
	SPI1 Baud Rate = 18.0 MBits/s
	SPI1 Prescaler = 2
	
	(Clock Configuration HCLK = 72 MHz )

----------------------------------------------------------------------------------------------


📚 Useful References

ILI9341 Display Datasheet: https://cdn-shop.adafruit.com/datasheets/ILI9341.pdf

XPT2046 Touch Controller Datasheet: https://www.ti.com/lit/ds/symlink/xpt2046.pdf

STM32F4 Discovery Board Documentation: https://www.st.com/en/evaluation-tools/32f407g-disc1.html