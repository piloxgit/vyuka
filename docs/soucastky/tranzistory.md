# Tranzistory – stručný a názorný přehled

Tranzistor je polovodičová součástka, která umí **zesilovat signál** nebo fungovat jako **elektronický spínač**. Má tři vývody a malým řídicím signálem ovládá větší proud.

## Jak se tranzistory dělí

```text
TRanzistory
├── Bipolární (BJT)       – NPN, PNP
└── Unipolární (FET)
    ├── n-kanál
    └── p-kanál
```

- **Bipolární tranzistor (BJT)** využívá oba typy nosičů náboje – elektrony i díry. Řídí se **proudem do báze**.
- **Unipolární tranzistor (FET)** využívá převážně jeden typ nosičů náboje. Řídí se **napětím na řídicí elektrodě**.
- Označení **N** a **P** popisuje typ polovodičové oblasti:
  - **N** – převládají elektrony,
  - **P** – převládají „díry“ (kladné nosiče).

## Skutečné součástky

Tranzistory mohou vypadat jako malé plastové součástky pro desku plošných spojů nebo jako větší výkonová pouzdra s kovovou ploškou pro chlazení.

![Různá pouzdra tranzistorů – například SOT-23, TO-92, TO-220 a výkonová pouzdra](https://agents-download.skywork.ai/image/rt/7379619fd2fcf8b7a58201595b891d47.jpg)

*Obrázek 1: Příklady skutečných tranzistorových pouzder. Zdroj obrázku: [Wikimedia Commons](https://en.wikipedia.org/wiki/Transistor).*

> Pozor: pořadí vývodů (např. E-B-C nebo G-D-S) se liší podle konkrétního typu. Vždy ověřte katalogový list.

## Bipolární tranzistory: NPN a PNP

BJT má vývody:

- **B – báze**: řídicí vývod,
- **C – kolektor**: vývod hlavního proudu,
- **E – emitor**: vývod hlavního proudu.

![Schematické značky PNP a NPN tranzistoru](https://agents-download.skywork.ai/image/rt/b6b8d507c0470d39d49fc31bb161f303.jpg)

*Obrázek 2: Základní značky BJT. U NPN šipka na emitoru míří ven, u PNP míří dovnitř. Zdroj: [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Transistor_symbols.png).*

### NPN

- Běžné zapojení jako **spínač na záporné straně** zátěže.
- Malý proud do báze otevře cestu proudu z kolektoru do emitoru.
- Pro sepnutí bývá báze asi o několik desetin voltu až přibližně 0,7 V výše než emitor (u křemíkového BJT).

### PNP

- Je „zrcadlem“ NPN: často spíná **kladnou stranu** napájení.
- Pro sepnutí musí být báze níže než emitor.
- Hodí se například jako horní (high-side) spínač.

### Výhody a nevýhody BJT

| Výhody | Nevýhody |
|---|---|
| Levné a snadno dostupné | Báze odebírá řídicí proud |
| Dobré zesílení proudu a signálu | Vyšší ztráty při větším proudu než u vhodného MOSFETu |
| Jednoduché analogové zesilovací obvody | Při zahřívání se může pracovní bod měnit |

## Unipolární tranzistory: FET

U FETu jsou typické vývody:

- **G – gate (hradlo)**: řídicí elektroda,
- **D – drain (drain/kolektor)**,
- **S – source (source/zdroj)**.

![Schematické značky n-kanálového a p-kanálového MOSFETu](https://agents-download.skywork.ai/image/rt/04805d2d942b02f873d3cec38cd84dbf.jpg)

*Obrázek 3: Zjednodušené značky n-kanálového a p-kanálového MOSFETu. Zdroj: [mbedded.ninja](https://blog.mbedded.ninja/electronics/components/transistors/mosfets/).*

### n-kanál

- Sepíná se kladným napětím na hradle vůči source.
- Častá volba pro spínání zátěže proti zemi.
- Obvykle má velmi malý řídicí proud do hradla.

### p-kanál

- Sepíná se zápornějším napětím na hradle vůči source.
- Často se používá pro spínání kladné větve napájení.
- Je praktický tam, kde nechceme další řídicí obvod s napětím vyšším než napájení.

### Výhody a nevýhody FET

| Výhody | Nevýhody |
|---|---|
| Téměř nulový stejnosměrný proud do hradla | Je citlivý na statickou elektřinu |
| Malé ztráty při sepnutí (u vhodně zvoleného typu) | Parametry silně závisí na napětí hradla |
| Vhodný pro rychlé digitální spínání | Některé typy mají vyšší cenu nebo složitější buzení |

> V praxi se pod „FET“ často myslí MOSFET. Existují i jiné varianty, například JFET; zde je neřešíme do detailu.

## Základní princip na NPN: spínání LED

NPN tranzistor pracuje jako elektronický spínač:

1. **Řídicí signál = 0 V** → báze nemá proud → tranzistor je vypnutý → LED nesvítí.
2. **Řídicí signál = 5 V** → přes rezistor teče malý proud do báze → tranzistor se sepne.
3. Proud teče z napájení přes rezistor a LED, dále kolektorem a emitorem do země → LED svítí.

![NPN tranzistor jako spínač LED](https://agents-download.skywork.ai/image/rt/c87f2ecd682ba610bc9255be8ed4d85e.jpg)

*Obrázek 4: Příklad NPN spínače LED s řídicím rezistorem. Zdroj: [Fiz-ix](https://fiz-ix.com/2012/11/how-to-use-an-npn-transistor-as-a-switch/).*

### Zjednodušené schéma zapojení

```text
             +5 V
              │
            RLED
          220–330 Ω
              │
             LED
              │
              C
ŘÍDICÍ ──RBASE──B   Q1 = NPN
  5 V    1 kΩ      E
                   │
                  GND
```

- **RLED** omezuje proud LED; bez něj se LED může poškodit.
- **RBASE** omezuje proud do báze.
- Emitter (E) je v tomto zapojení připojen na zem.
- Hodnoty rezistorů jsou příklad pro malé napětí a malou LED; konkrétní hodnoty závisí na napájení, LED a tranzistoru.

## Rychlé srovnání

| Typ | Řídí se | Typické spínání | Hlavní plus | Hlavní mínus |
|---|---|---|---|---|
| NPN (BJT) | Proud báze | Zátěž proti zemi | Jednoduché a levné | Potřebuje proud báze |
| PNP (BJT) | Proud báze | Zátěž v kladné větvi | Jednoduchý horní spínač | Také zatěžuje řídicí výstup |
| n-kanál MOSFET | Napětí G vůči S | Zátěž proti zemi | Malé ztráty, téměř žádný řídicí proud | Musí být správně buzen hradlem |
| p-kanál MOSFET | Napětí G vůči S | Zátěž v kladné větvi | Pohodlný horní spínač | Obvykle větší odpor v sepnutém stavu než u srovnatelného n-kanálu |

### Zapamatování

- **BJT:** malý proud řídí větší proud.
- **FET:** napětí na hradle řídí proud kanálem.
- **NPN / n-kanál:** často spínají směrem k zemi.
- **PNP / p-kanál:** často spínají kladnou větev.
- Šipka na BJT: **NPN – šipka ven, PNP – šipka dovnitř**.

## Zdroje obrázků

- [Transistor symbols – Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Transistor_symbols.png)
- [MOSFET schematic symbols – mbedded.ninja](https://blog.mbedded.ninja/electronics/components/transistors/mosfets/)
- [NPN transistor switch – Fiz-ix](https://fiz-ix.com/2012/11/how-to-use-an-npn-transistor-as-a-switch/)
- [Transistor packages – Wikipedia](https://en.wikipedia.org/wiki/Transistor)

