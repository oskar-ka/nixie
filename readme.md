


## Strømforsyning
Nixie uret skal bruge to spændinger for at fungere: 5Vdc til microcontroller og logiske kredse, samt 180Vdc til at trække nixierørene. Hvert rør kan tåle op til 3.5mA, så med 6 rør skal strømforsyningen levere 21mA + lidt til de 4 små nixie prikker, så i alt maks. 30mA v. 180Vdc. Det er nok ikke nødvendigt med PFC ved 30mA, men det kunne måske være sjovt at lave hvis der er plads til det. Evt. kan strøforsyningen blive lavet på et separat print, som kan placeres under nixie-printet, så burde der være masser af plads. Skal den kunne skifte mellem 230Vac og 120Vac, og skal den gøre det automatisk?

Der findes mange forskellige måder at opnå disse to spændinger:
- 12/24Vdc indgang &rarr; DC-DC til 5V + boost converter til 180Vdc
- 230Vac indgang &rarr; diodebro som giver 325Vdc, med den rigtige modstand før 
nixierørene kan denne spænding bruges direkte; 5V AC-DC
    - Rimelig ueffektivt og ikke så sejt, men meget nemt
- 230Vac &rarr; styret thyristorbro som giver 180Vdc direkte; 5V AC-DC
    - Thyristorbroer er som regel store, ved ikke om man kan få en i DIP
- 230Vac &rarr; styret MOSFET ensretter som giver 180Vdc direkte; 5V AC-DC
    - Mere effektiv end thyristorbro
    - Skal bruge to MOSFETS hver vej for at kunne blokere = 8 MOSFETS
    - Kan evt. også laves som halvbølgeensretter, da den ikke skal levere ret meget strøm
- 230Vac &rarr; transformer 230Vac&rarr;125Vac &rarr; ensretter (styret/ikke styret); & 5V AC-DC
    - Ret nemt, få komponenter, ret effektivt, galvanisk adskillelse
- 230Vac &rarr; reguleret flyback converter med 2 udgange!!
    - Ret sej løsning, galvanisk adskillelse, høj virkningsgrad, ikke nemt.
    - 

Skal power supply være på et separat print?

## Komponenter
- ATtiny2313 x1
- Shift register x4
- Quad optokobler f.eks. LTV-845M x4
- SN74141 x4
