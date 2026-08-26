# Jednoduchý návod: blikání LED diodou

V tomto návodu vytvoříme program, který bude pravidelně rozsvěcet a zhasínat LED diodu připojenou k Arduinu.

## Co potřebujeme

- Arduino, například Arduino Uno
- LED diodu
- rezistor $220\ \Omega$
- nepájivé kontaktní pole a propojovací vodiče
- USB kabel

## Zapojení

1. Delší vývod LED diody (anodu) připojte přes rezistor k pinu **13**.
2. Kratší vývod LED diody (katodu) připojte k pinu **GND**.

Arduino Uno má na pinu 13 vestavěnou LED, takže pro první vyzkoušení není nutné připojovat externí LED.

## Program

Otevřete Arduino IDE, vytvořte nový program a vložte tento kód:

```cpp
const int ledPin = 13;

void setup() {
	pinMode(ledPin, OUTPUT);
}

void loop() {
	digitalWrite(ledPin, HIGH);
	delay(1000);

	digitalWrite(ledPin, LOW);
	delay(1000);
}
```

## Nahrání programu

1. Připojte Arduino k počítači pomocí USB kabelu.
2. V Arduino IDE vyberte správnou desku a port v nabídce **Nástroje**.
3. Klikněte na tlačítko **Nahrát**.
4. Po nahrání začne LED každou sekundu svítit a každou sekundu zhasne.

Hodnotu `1000` v příkazech `delay()` můžete změnit. Číslo udává dobu čekání v milisekundách, takže například `500` způsobí rychlejší blikání.