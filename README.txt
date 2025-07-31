STM32F4 Discovery & ILI9341 TFT ve XPT2046 Dokunmatik Kontrolör

Bu proje, STM32F4 Discovery kartı ile ILI9341 TFT LCD ekranının entegrasyonunu ve XPT2046 dirençli dokunmatik kontrolör kullanarak dokunmatik fonksiyonalitesini göstermektedir. Firmware, STM32 HAL kütüphaneleri kullanılarak C dilinde geliştirilmiş olup, çevresel birimlerle arayüz için SPI haberleşmesi kullanılmaktadır.


🛠 Kullanılan Donanım

	STM32F407 Discovery Kartı
	ILI9341 TFT LCD Ekran** (240x320, 2.4-inç)
	XPT2046 Dokunmatik Kontrolör
	Ekran ve Dokunmatik için SPI Haberleşmesi
	ILI9341 Ekran Kontrolü için SPI1
	XPT2046 Dokunmatik Kontrolör için SPI2


🔧 Temel Özellikler

	Ekran başlatma ve grafik render işlemleri
	XPT2046 aracılığıyla dokunmatik giriş işleme
	Ekran çözünürlüğüne uygun koordinat eşleme
	Verimli veri transferi için optimize edilmiş SPI haberleşmesi


🛠 Devre Bağlantıları

		**LCD**  	  **STM32F4**
	
	ILI9341 Ekran Kontrolü için SPI1
	
		LCD_CS_PIN -- GPIOA_PIN_4
		LCD_RST_PIN -- GPIOA_PIN_6
		LCD_DC_PIN -- GPIOC_PIN_4
		LCD_SCK -- SPI1_SCK (PA5)
		LCD_MOSI -- SPI1_MOSI (PA7)
		LCD_LED -- STM32_VCC
		LCD_VCC	-- STM32_VCC
		LCD_GND -- STM32_GND
		
	XPT2046 Dokunmatik Kontrolör için SPI2
	
		XPT2046_SCK (T_CLK) -- SPI2_SCK (PB13)
		XPT2046_MISO (T_D0) -- SPI2_MISO (PB14)
		XPT2046_MOSI (T_DIN) -- SPI2_MOSI (PB15)
		XPT2046_CS (T_CS) -- GPIOB_PIN_12
		XPT2046_IRQ (T_IRQ) -- Kullanılmıyor
	


🖥️ Kütüphaneler

	ILI9341 Ekran Kontrolü için
	
		Inc	fonts.h
			ILI9341_GFX.h
			ILI9341_STM32_Driver.h
		
		Src	fonts.c
			ILI9341_GFX.c
			ILI9341_STM32_Driver.c
	
	XPT2046 Dokunmatik Kontrolör için
		
		Inc	xpt2946.h
	
		Src	xpt2046.c


🖥️ Kurulum ve Ayarlama

	Depoyu klonlayın
	Projeyi STM32CubeIDE veya tercih ettiğiniz IDE'de açın.
	STM32F4 Discovery kartını USB ile bağlayın.
	ST-Link debugger kullanarak firmware'i derleyin ve flash'layın.
	Sistemi çalıştırın ve ekran ile dokunmatik fonksiyonalitesini test edin.


🚀 Karşılaşılan Sorunlar ve Çözümler

	1. Yanlış Dokunmatik Eşleme
		Sorun: Dokunmatik koordinatları ekran yönlendirmesiyle eşleşmiyordu.
		Çözüm: 240x320 çözünürlük için koordinatları doğru eşlemek amacıyla xpt2046.h dosyasındaki RAW_MIN_X, RAW_MAX_X, RAW_MIN_Y, RAW_MAX_Y değerleri ayarlandı.
	
	2. Ters Çevrilmiş X/Y Ekseni
		Sorun: Dokunmatik yanıt bir veya her iki eksen boyunca ters çevrilmişti.
		Çözüm: xpt2046.h dosyasında XPT2046_MIRROR_X ve XPT2046_MIRROR_Y yapılandırıldı.
	
	3. SPI Haberleşme Kararsızlığı
		Sorun: STM32 ve çevresel birimler arasında ara sıra haberleşme hataları oluşuyordu.
		Çözüm: SPI clock kararlılığı artırıldı ve xpt2046.c dosyasında NSS işleme ayarlandı.
	
			SPI2 Baud Rate = 1.125 MBits/s
			SPI2 Prescaler = 32
			
			SPI1 Baud Rate = 18.0 MBits/s
			SPI1 Prescaler = 2
			
			(Clock Yapılandırması HCLK = 72 MHz)
