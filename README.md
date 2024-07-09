# r-duino-led-3V3-logic
Ahoj, dneska se naučíme jak přepnout vnitřní logické napětí Ř-duina-LED z 5V na 3.3V za pomocí ArduinoISP.
ArduinoISP je program pro platformu Arduino, který umožňuje použití jednoho Ř-Duina jako programátoru pro nahrání programu do jiného Ř-Duino-LED nebo jiného mikrokontroléru.
Z jednoho Ř-Duino vytváříme fleshovací jednotku ArduinoISP

# Součástky
### Povinné:
- Ř-duino-LED
- Ř-duino (programátor)
- Vodiče

### Vloitelné:
- Rezistor 1kΩ
- Nepájivé pole
- LED

# Ř-Duino-LED ISP
Existuje několik důvodů, proč byste mohli chtít používat ArduinoISP:

1. Programování mikrokontrolérů: Pokud potřebujete nahrát program do mikrokontroléru, který není kompatibilní s Arduino, můžete použít ArduinoISP jako programátor.

2. Programování Arduino bez sériového rozhraní: Někdy může být sériové rozhraní (pomocí USB) zaneprázdněno nebo nepřístupné. Použití ArduinoISP umožňuje programování Arduina pomocí jiného rozhraní.

3. Programování nebo obnovení bootloaderu: Pokud jste omylem vymazali bootloader z vašeho Arduina nebo pokud potřebujete nahrát nový bootloader, ArduinoISP může být použito k obnovení bootloaderu.

# Proč Používat 3,3V
1. Spotřeba energie: Pokud máte aplikaci, která musí být energeticky úsporná nebo provozovaná na baterii, snížení napětí a frekvence může snížit spotřebu energie. Prostředí s nižším napětím a frekvencí může mít menší spotřebu energie než standardní 5V 16MHz konfigurace.
2. Kompatibilita s periferiemi: Některé periferie, jako jsou senzory nebo komunikační moduly, mohou být navrženy pro práci s nižším napětím než 5V. Použití 3,3V Arduina umožňuje snadnější integraci s těmito periferiemi.
3. Omezení teploty: V některých aplikacích, jako jsou ty, které musí pracovat v extrémních teplotách, může být 3,3V konfigurace vhodnější kvůli lepšímu chlazení.

# Co Je to MiniCore
Jádro Arduino pro počítače ATmega328, ATmega168, ATmega88, ATmega48 a ATmega8, které běží na zavaděči Urboot bootloader.

# MiniCore
Otevřete Arduino IDE.

Otevřete položku z nabídky Soubor > Předvolby.

Do pole adresy URL Správce dalších fór zadejte následující adresu URL:

https://mcudude.github.io/MiniCore/package_MCUdude_MiniCore_index.json

# Nahravani ArduinoISP
ArduinoISP je výkonný nástroj, který vám umožní přeměnit vaši desku Arduino na obvodový programátor. Pojďme se ponořit do detailů:

Bootloader a mikrokontroléry:

Každou desku Arduino lze snadno naprogramovat pomocí softwaru Arduino (IDE). Když připojíte Arduino k počítači přes USB a kliknete na ikonu „Nahrát“, vaše skica se přenese do Flash paměti mikrokontroleru.

Tento proces se opírá o speciální část kódu zvanou Bootloader. Bootloader se spustí pokaždé, když se mikrokontrolér resetuje a hledá náčrt k nahrání přes sériový/USB port. Pokud není detekováno žádné spojení, pokračuje ve spuštění vaší skici.

Bootloader se nachází ve specifické oblasti paměti mikrokontroléru, kterou nelze přeprogramovat jako běžnou skicu. Hraje klíčovou roli při bezproblémovém programování Arduina.

In-Circuit Serial Programmer (ISP):

K naprogramování Bootloaderu a zajištění kompatibility se softwarem Arduino potřebujete In-Circuit Serial Programmer (ISP). Toto zařízení se připojuje ke konkrétním pinům na mikrokontroléru, což vám umožňuje naprogramovat celou flash paměť včetně Bootloaderu.

Proces programování ISP také zahrnuje nastavení pojistek, které definují, jak mikrokontrolér pracuje za specifických podmínek.

Použití Arduina jako ISP:

Mezi různými programovacími zařízeními je metoda „Arduino jako ISP“ nákladově efektivní a praktická. Je to vynikající řešení pro vypálení bootloaderu na jinou desku Arduino s mikrokontroléry ATmega, 32U4 nebo ATtiny.

# Instalace MiniCore
Otevřete položku nabídky Nástroje - Deska - Manager desek - vyhledáme si MiniCore a dáme instalovat

# Ř-Duino (Jako ISP Programátor):ZAPOJENÍ
  - Ř-Duino (jako ISP programátor):
  - Pin 10 (SS) -> Pin RESET na Ř-duino-LED
  - Pin 11 (MOSI) -> Pin 11 na Ř-duino-LED
  - Pin 12 (MISO) -> Pin 12 na Ř-duino-LED
  - Pin 13 (SCK) -> Pin 13 na Ř-duino-LED
  - 5V -> 5V na Ř-duino-LED
  - GND -> GND na Ř-duino-LED

V tomto nastavení je Ř-Duino nakonfigurován jako ISP (In-System Programmer) a používá se k programování Ř-duino-LED . Pin 10 (SS) na Ř-Duino je připojen na RESET pin na Ř-duino-LED , což umožňuje Ř-Duinu resetovat Ř-duino-LED během programování. Piny 11, 12 a 13 jsou připojeny k MOSI, MISO a SCK na obou Ř-duinech, což umožňuje komunikaci mezi nimi pomocí SPI protokolu. Propojení 5V a GND slouží k napájení obou Ř-duin.

# Nastavení Desky + Vypalení Zavaděče
Otevřete položku nabídky Nástroje - Deska - MiniCore - ATmega328
Otevřete položku nabídky Nástroje - Clock - "Internal 8 MHZ"
poté nastaveni Programátoru
Otevřete položku nabídky Nástroje - Programátor: - Arduino as IP
Otevřete položku nabídky Nástroje - vypálit zavaděč

# Přepnutí Jumperu 5V Na 3,3V 8Mhz
Na desce Ř-Duino-LED se hned za USB-C PORTem nacházají tři piny, které se používají pro přepnutí logického napětí. V základu desky Ř-duino-LED přichází s jumperem spojujícím prostřední pin, který určuje logické napětí, a pin 5V. Pokud chceme změnit logické napětí na 3.3V musíme přepojit jumper tak, aby spojoval prostřední pin a pin 3V3. 

# Připojení LED
Vytvoříme si jednoduchý program, abychom otestovali, zda vše proběhlo bezchybně. Bude se jednat o jednoduchý blikač, kdy k desce připojíme externí LEDku a pomocí kódu ji rozblikáme.
Připojení LED: 
Připojte rezistor (1k Ohm) k libovolnému digitálnímu pinu na Ř-duinu-LED (na příklad pin 13) 
Připojte rezistor k anodě LED (delší nožka). 
Připojte katodu LED (kratší nožka) k připojte k pinu GND na Ř-duinu-LED. 

# Programování
Naprogramujte Ř-duino tak, aby pulsovalo na napájecím pinu, na kterém je připojena LEDka, z HIGH na LOW a zpět, aby vytvořilo blikající efekt.
Zde je jednoduchý kód:
```cpp
// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(LED_BUILTIN, OUTPUT);
}


// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}
```

Nyní Ř-duino-LED připojte přes USB k počítači, vyberte nabízený PORT a klikněte na iknou "Nahrát".

# Závěr
V tomto tutoriálu jsete se naučili jak přepnout vnitřní logiku Ř-duina-LED z 5V na 3.3V. Pokud byste chtěli ji přepnout zase zpět, stačí jen stejným způsobem přepnout vnitřní frekvenci zpět na 16 MHz a přepojit jumper.

Ještě bych rád zmínil, že pokud se rozhodnete využívat vnitřní logiku 3.3V, bohužel příjdete o možnost využití zabudovaných LEDek a u některých našich projektů, pak budete muset zapojit LEDky externí.
