
## Setup
Dimming?

- 6x IN-8
- 2/4x NE-2


## Strømforsyning
Nixie uret skal bruge to spændinger for at fungere: 5Vdc til microcontroller og logiske kredse, samt 180Vdc til at trække nixierørene. Hvert rør kan tåle op til 3.5mA, så med 6 rør skal strømforsyningen levere 21mA + lidt til de 4 små nixie prikker, så i alt maks. 30mA v. 180Vdc. Det er nok ikke nødvendigt med PFC ved 30mA, men det kunne måske være sjovt at lave hvis der er plads til det. Evt. kan strøforsyningen blive lavet på et separat print, som kan placeres under nixie-printet, så burde der være masser af plads. Skal den kunne skifte mellem 230Vac og 120Vac, og skal den gøre det automatisk?



### Specifikationer
- Fra IN-8 datablad:
    - Ignition voltage: &leq; 170V
    - Indication current: &leq; 2.5mA
    - Turn-off voltage: ??
- NE-2 lampe:
    - &lt;1mA
- 180Vdc, 20mA
- Current limiting, [foldback](https://www.eeeguide.com/foldback-current-limiting-circuit/)
- Temperature compensation
- Lysnetspænding i EU kan lovligt variere mellem 207Vac til 253Vac, som giver halveret DC på 146-182Vdc

### Der findes mange forskellige måder at opnå disse to spændinger:
- 12/24Vdc indgang &rarr; DC-DC til 5V + boost converter til 180Vdc
    - [Recom R12-150B](https://www.tme.eu/dk/en/details/r12-150b/dc-dc-converters/recom/)
- 230Vac indgang &rarr; diodebro som giver 325Vdc, med den rigtige modstand før 
nixierørene kan denne spænding bruges direkte; 5V AC-DC
    - Rimelig ueffektivt og ikke så sejt, men meget nemt
- 230Vac &rarr; styret thyristorbro som giver 180Vdc direkte; 5V AC-DC
    - Thyristorbroer er som regel store, ved ikke om man kan få en i DIP
- 230Vac &rarr; styret MOSFET ensretter som giver 180Vdc direkte; 5V AC-DC
    - Mere effektiv end thyristorbro
    - Skal bruge to MOSFETS hver vej for at kunne blokere = 8 MOSFETS
    - Kan evt. også laves som halvbølgeensretter, da den ikke skal levere ret meget strøm
- 230Vac &rarr; halveringstransformer 230V&rarr;115Vac &rarr; ensretter (styret/ikke styret); & 5V AC-DC
    - Ret nemt, få komponenter, ret effektivt, galvanisk adskillelse
    - Giver 160Vdc v. 230Vac, hvilket er fint, men hvis nettet går ned til 207Vdc så har vi kun 146Vdc hvilket ikke helt er nok
- 230Vac &rarr; 2/3-transformer = 195/217/239Vdc (min, nom, max)
    - enten direkte til nixierør, kunne sikkert fungere
    - eller transistor med varmetab
        - skal smide mellem 15-59V
        - ved 20mA &rarr; 0.3W-1.2W
        - TO-92: [PHE13003A](https://mou.sr/43Gdbwc) 60K/W, nogle af dem måske op til 2W??
        - TO-252 [MJD340](https://mou.sr/4o38ar5): 8.3K/W op til 15W
        - TO-220 [BUL741](https://mou.sr/3Q8gnh7): 2K/W op til 60W med heatsink
        - TO-3 [MJ15024](https://mou.sr/4uGqn01): 0.7K/W op til 250W
    - eller buck-converter?
- 230Vac &rarr; transformer 230Vac&rarr;125Vac &rarr; ensretter (styret/ikke styret); & 5V AC-DC
    - Ret nemt, få komponenter, ret effektivt, galvanisk adskillelse
    - Eller brug autotransformer, nemme at finde med 2-1 da de laver EU spænding om til US
- 230Vac &rarr; reguleret flyback converter med 2 udgange!!
    - Ret sej løsning, galvanisk adskillelse, høj virkningsgrad, ikke nemt.
    - 

Skal power supply være på et separat print?


### Heatsinks
- [U-formet](https://fischerelektronik.de/web_fischer/en/heatsinks/A07/U-Extruded%20heatsinks/$catalogue/fischerData/PR/ICK35_SA_/search.xhtml), lidt større end den jeg har, 15K/W
- [Sej en til TO-3](https://fischerelektronik.de/web_fischer/en/heatsinks/A01/Standard%20extruded%20heatsinks/$catalogue/fischerData/PR/SK36_/search.xhtml)
- [SK 65](https://fischerelektronik.de/web_fischer/en/heatsinks/A01/Standard%20extruded%20heatsinks/$catalogue/fischerData/PR/SK65_/search.xhtml) Til SOT-32 transistor, lidt lavere end SK 64
- [SK 31](https://fischerelektronik.de/web_fischer/en/heatsinks/A01/Standard%20extruded%20heatsinks/$catalogue/fischerData/PR/SK31_/search.xhtml) Til TO-3, kun 12mm høj

### Komponenter
- AC Sikring + sikringsholder
    - 100mA glassikring?
- Transformer:
    - [Hammond 229A230](https://www.digikey.com/en/products/detail/hammond-manufacturing/229A230/454947) Unhoused
        - Height: 21.6mm
    - [Bel Signal IF-6-230](https://mou.sr/49APmcG) Red housing
        - Height: 22.6mm
    - [Bel Signal 230-25-LPI](https://mou.sr/4x3g8o8) Black housing
        - Height: 22.7mm
    - [Bel Signal LP-230-25](https://mou.sr/4uTkMDK) Unhoused
        - Height: 21.6mm
- 5V supply:
    - [Mean Well IRM-01-5](https://mou.sr/4u9H5E1)
    - [PBO-3E/F](https://www.belfuse.com/products/power-supplies/ac-dc-converters)
    - [PSK-5E](https://www.belfuse.com/products/power-supplies/ac-dc-converters/psk-5e-series)
    - [TRACO Power TMPS 05-105](https://mou.sr/49ALLeS) 1x1"
    - [Mornsun LS05-23B05DR3](https://www.mornsun-power.com/html/pdf/LS05-23B05DR3.html) Very small
- Ensretter IC
    - sdf



## Komponenter
- Lamper
    - 6x IN-8
    - 2/4x NE-2
- Forsyningsprint
    - Sikring
        - 100mA
    - Transformer
    - Ensretter
    - Lyt
    - Zenerdiode(r)
        - hvis 180V så 5W
    - Effekttransistor
    - OCP transistor
    - Modstande
    - AC-DC forsyning
- Styreprint
    - ATtiny2313 x1
    - Shift register x4
    - Quad optokobler f.eks. LTV-845M x4
    - SN74141 x4

## Case
### Varmeafgivelse
- Original laserskåret lagkagekasse
    - Test 1: P=4W, UT=22C, IT=67C &rarr; +45C v. 4W = 11.25 K/W
    - Test 2: P=3W, UT=22C, IT=58C &rarr; +36C v. 3W = 12    K/W
    - Test 3: P=2W, UT=22C, IT=49C &rarr; +26C v. 2W = 13.5  K/W
    - Test 4: P=1W, UT=22C, IT=38C &rarr; +16C v. 1W = 16    K/W
    
