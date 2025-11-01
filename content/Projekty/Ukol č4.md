---
date : '2025-10-22'
draft : false
title : 'Úkol č. 4 : 3D skenování'
---

V tomto týdnu jsme byli zaškoleni na 3D skener a dostali jsme zadání miniprojektu. Cílem projektu je naskenovat objekt pomocí 3D skeneru SimScan a exportovat digitální data ve formátu STL. Naskenovaná data pak zpracovat a zjistit následující parametry:

* Povrch dílu
* Maximální rozměr dílu a jeden libovolně zvolený rozměr

Díl, který jsem si pro skenování vylosoval, byla plastová láhev s objemem 5 l. Tu jsem musel před skenováním připravit, protože je průhledná. Aby skener zachytil povrch PET lahve, musel jsem ji nastříkat matným sprejem.

<div style="display:flex; justify-content:center; gap:10px;">
  <img src="/images/3D-scan/Lahev.jpg" alt="lahev-matna" height="400">
  <img src="/images/3D-scan/Lahev-matna.jpg" alt="lahev-matna" height="400">
  <img src="/images/3D-scan/Lahev-body.jpg" alt="lahev-matna" height="400">
</div> 

Pro orientaci v prostoru skener používá reflexní body, kterými se musí model polepit. Stejnými body je také polepena otočná deska, na které je model položen. Kromě toho jsem okolo modelu rozložil referenční bloky, které mají na každé ploše nalepený lokalizační bod.

<div style="display:flex; justify-content:center; gap:10px;">
  
</div>

Skenovací parametry:
* Rozlišení skenu: 0,5 mm
* Expoziční čas: 5 ms

Toto je výsledný model po 3D skenování bez jakýchkoliv úprav:
<script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
<div style="display:flex; justify-content:center; gap:10px; margin:1rem 0;">
  <model-viewer src="/models/lahev.glb"
                alt="Náhled 3D modelu láhve"
                camera-controls
                auto-rotate
                environment-image="neutral"
                style="width:100%; max-width:640px; height:480px;">
  </model-viewer>
</div>

V programu GOM jsem v modelu zaplátoval díry, lehce zjemnil povrch a snížil počet polygonů, protože polygonová síť je po 3D skenování zbytečně hustá.
Zde je upravený model:

<script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
<div style="display:flex; justify-content:center; gap:10px; margin:1rem 0;">
  <model-viewer src="/models/lahev_upravene.glb"
                alt="Náhled 3D modelu láhve"
                camera-controls
                auto-rotate
                environment-image="neutral"
                style="width:100%; max-width:640px; height:480px;">
  </model-viewer>
</div>

Na závěr jsem změřil povrch modelu, jeho výšku a průměr hrdla:
* Povrch: 177932,39 mm²
* Průměr vršku: 41,09mm
* Výška: 326,56 mm

Pro zajímavost, objem modelu vychází 5 101 547,19 mm³, tedy přibližně 5,1 litru, což odpovídá našemu očekávání.

<div style="display:flex; justify-content:center; gap:10px;">
  <img src="/images/3D-scan/Lahev-rozmery.jpg" alt="lahev-matna" height="600">
</div>