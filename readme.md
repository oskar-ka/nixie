


## Strømforsyning
Nixie uret skal bruge to spændinger for at fungere: 5Vdc til microcontroller og logiske kredse, samt 180Vdc til at trække nixierørene.

Der findes mange forskellige måder at opnå disse to spændinger:
- 12/24Vdc indgang &rarr; DC-DC til 5V + boost converter til 180Vdc
- 230Vac indgang &rarr; diodebro som giver 325Vdc, med den rigtige modstand før 
nixierørene kan denne spænding bruges direkte; 5V AC-DC
    - Rimelig ueffektivt og ikke så sejt, men meget nemt
- 230Vac &rarr; styret thyristorbro som giver 180Vdc direkte; 5V AC-DC
    - Thyristorbroer er som regel store, ved ikke om man kan få en i DIP
- 230Vac &rarr; styret MOSFET ensretter som giver 180Vdc direkte; 5V AC-DC
    - Mere effektiv end thyristorbro
- 230Vac &rarr; transformer 230V&rarr;125V &rarr; ensretter (styret/ikke styret); & 5V AC-DC
    - Ret nemt, få komponenter, ret effektivt, galvanisk adskillelse
- 230Vac &rarr; reguleret DC-forsyning med transformer med 2 udgange!!
    - Ret sej løsning, galvanisk adskille, høj virkningsgrad, overhovedes ikke nemt.

## Komponenter
- ATtiny2313 x1
- Shift register x4
- Quad optokobler f.eks. LTV-845M x4
- SN74141 x4