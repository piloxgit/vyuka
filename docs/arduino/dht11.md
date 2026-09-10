# DHT11 a Arduino v PlatformIO

Krátký návod, jak připojit senzor DHT11 k Arduinu, přidat knihovnu Mark Ruys do projektu PlatformIO a vypsat teplotu a vlhkost do sériového monitoru.

Knihovna `markruys/DHT` podporuje DHT11 i DHT22, umí automaticky rozpoznat typ senzoru a používá jednoduché rozhraní `setup()`, `getHumidity()` a `getTemperature()`.


![Pinout senzoru DHT11 s popisem pinů](https://agents-download.skywork.ai/image/rt/fc077aafc691e945f954b169445a2a39.jpg)

## Přidání knihovny do `platformio.ini`

Nejdůležitější částí konfigurace je volba **`lib_deps`**. PlatformIO podle ní knihovnu automaticky vyhledá v registru a nainstaluje do projektu při sestavení, ladění nebo testování.

V kořenu projektu otevři soubor `platformio.ini` a doplň závislost:

```ini
[env:nanoatmega328]
platform = atmelavr
board = nanoatmega328
framework = arduino

lib_deps = markruys/DHT
```

Zápis `markruys/DHT` používá formát **vlastník/knihovna** a odpovídá knihovně z PlatformIO Registry..

### Proč použít `lib_deps`

-   knihovna se stáhne automaticky na každém počítači, kde projekt sestavíš,
-   závislost je uložená přímo v projektu,
-   není nutné kopírovat knihovnu ručně do globální složky Arduino IDE,
-   další knihovny můžeš přidat na další řádky pod `lib_deps`.

## Program v `src/main.cpp`

Vytvoř nebo uprav soubor `src/main.cpp`:

```cpp
#include <Arduino.h>
#include "DHT.h"

const byte DHT_PIN = 2;
DHT dht;

void setup()
{
  Serial.begin(9600);

  dht.setup(DHT_PIN); 
}

void loop()
{
  delay(dht.getMinimumSamplingPeriod());

  Serial.print(dht.getHumidity());
  Serial.print("\t");
  Serial.print(dht.getTemperature());
}
```