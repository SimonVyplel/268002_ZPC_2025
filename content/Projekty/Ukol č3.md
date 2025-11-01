---
date : '2025-10-14'
draft : false
title : 'Úkol č. 3 : 3D modelování a 3D tisk'
---

V tomto týdnu jsme se učili pracovat s asi nejuniverzálnější technologií pro prototypování, a tou je 3D tisk. Umožňuje rychle a levně vytvářet prototypy součástí a mechanismů s velmi nízkou ztrátovostí materiálu. Abychom se s touto technologií seznámili důvěrněji, dostali jsme za úkol navrhnout, vytisknout a sestrojit jednoduchý mechanismus. Podmínky byly:

* Mechanismus musí být klikový, vačkový nebo maltézský
* Maximálně múžeme využít 100g filamentu
* Ruční pohon
* Jedno uložení volné a jedno s přesahem

Rozhodl jsem se, že bych rád vytvořil scénu, ve které se při rotaci kličky něco děje. Chtěl jsem, aby byla dynamická, a tak jsem se rozhodl vytvořit dělníka, který krumpáčem těží skálu. Celý mechanismus se při otočení kličky natáhne a poté rázně udeří do kamene. Toho jsem docílil implementováním spirálové pružiny do hlavního kloubu mechanismu. Při zaklonění jsem chtěl, aby zároveň natáhl ruku – toho jsem dosáhl pomocí ozubených kol, která amplifikují rotaci ruky.

<div style="display:flex; justify-content:center; gap:10px;">
  <img src="/images/Sestava-3Dtisk.png" alt="sestava" height="400">
</div> 

Model je navržen tak, aby se tiskl bez podpěr, a jako hřídele v kloubech lze použít vlákno filamentu. Různé průměry děr (2,1 mm a 2,3 mm) zajistily, že filament nevypadne z krajních uložení, a zároveň se prostřední rotační prvek volně otáčí bez tření.
Díly jsem následně vložil do sliceru a vygeneroval G-code pro tisk.

<div style="display:flex; justify-content:center; gap:10px;">
  <img src="/images/slicer.png" alt="slicer">
</div> 

Celý mechanismus jsem poté bez problémů složil a zkontroloval jeho hmotnost.

<div style="display:flex; justify-content:center; gap:10px; flex-wrap:wrap;">
  <img src="/images/3D tisk-váha.jpg" alt="váha" style="max-width:32%; height:auto;">
  <video controls muted playsinline preload="metadata" style="max-width:32%; height:auto;" poster="/images/3D tisk-váha.jpg">
    <source src="/videos/3D%20tisk-video%201.mp4" type="video/mp4">
    Váš prohlížeč nepodporuje video tag.
  </video>
  <video controls muted playsinline preload="metadata" style="max-width:32%; height:auto;" poster="/images/3D tisk-váha.jpg">
    <source src="/videos/3D%20tisk-video%202.mp4" type="video/mp4">
    Váš prohlížeč nepodporuje video tag.
  </video>
</div> 