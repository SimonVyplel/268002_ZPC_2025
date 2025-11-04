---
date : '2025-10-27'
draft : false
title : 'Úkol č. 5 : Elektronický obvod s mikrokontrolérem'
---

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/themes/prism-tomorrow.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/prism/1.29.0/prism.min.js"></script>

<style>
/* Minimalistický tmavý styl */
pre[class*="language-"] {
  background: #1e1e1e !important;
  border: none;
  border-radius: 10px;
  padding: 1rem;
  font-family: 'JetBrains Mono', monospace;
  font-size: 14px;
  line-height: 1.5;
  overflow-x: auto;
  box-shadow: 0 2px 6px rgba(0,0,0,0.15);
}
code[class*="language-"] {
  background: none !important;
  color: #dcdcdc !important;
}
pre {
  margin: 1.5em 0;
}
</style>


V tomto týdnu jsme se zabývali prací s mikrokontrolérem, zapojováním jednoduchých obvodů a dostali jsme zadaný miniprojekt, v rámci kterého máme navrhnout vlastní obvod. Já jsem se rozhodl vytvořit unikátní ovládání světel pomocí joysticku. Jako úkol jsem si stanovil vytvořit obvod, který na základě vstupů ovládá tři LED diody. Po stisknutí a držení tlačítka joysticku začne ovládání LED diod. Při pohybu zleva doprava se mění počet diod, které svítí, a při pohybu nahoru a dolů se mění perioda, s jakou blikají. Obvod jsem zapojil následovně:

<div style="display:flex; justify-content:center; gap:10px;">
  <img src="/images/obvod.png" alt="obvod" >
</div> 

Co se týče programu tak jsem začal tím, že jsem si nadefinoval proměnné a k nim přiřadil piny, případně výchozí hodnoty.

<pre><code class="language-cpp">
const int buttonPin = 2;
const int xPin = A0;
const int yPin = A1;
const int ledPins[] = {13, 12, 11};

int numLEDs = 3;           // kolik LED aktuálně svítí
int blinkDelay = 500;      // rychlost blikání
bool ledState = false;
unsigned long previousMillis = 0;
</code></pre>

Dále v programu probíhá část setup. V ní jsem nastavil režim pinů pomocí pinMode pro vstupy z tlačítka a výstupy na LEDky. Zároveň jsem jim přiřadil základní hodnoty. Na konci této části jsem inicializoval sériový výstup do konzole.

<pre><code class="language-cpp">
void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  for (int i = 0; i < 3; i++) {
    pinMode(ledPins[i], OUTPUT);
    digitalWrite(ledPins[i], LOW);
  }
  Serial.begin(9600);
}
</code></pre>

V rámci hlavní smyčky loop začínáme načtením hodnot ze vstupů. Poté, pod podmínkou, že je tlačítko stisknuté, na základě přečtených vstupů aktualizujeme proměnné pro počet svítících LED diod a délku prodlevy mezi blikáním.

Následně nastavujeme blikání diod se zadanou prodlevou. Je potřeba se vyhnout příkazu delay(), protože ten zastaví celý program. Toho jsem dosáhl porovnáváním aktuálního času, který uplynul od začátku programu, s hodnotou posledního přepnutí diod. V případě, že je jejich rozdíl větší než zadaná prodleva, aktualizujeme hodnotu posledního přepnutí a logickou hodnotu pro stav diod překlopíme.

V předposlední části programu určujeme, které diody mají svítit. Ve smyčce projdeme všechny diody a pokud splňují podmínky pro svícení (stav diody = 1 a číslo LEDky je menší než počet svítících diod), nastavíme je jako svítící.

Nakonec vypíšeme načtené hodnoty ze vstupů a virtuální hodnoty určující, jak rychle a kolik diod má svítit, do konzole pro ladění (při fyzickém zapojování jsem měl problém se vstupy).

<pre><code class="language-cpp">
void loop() {
  bool buttonPressed = (digitalRead(buttonPin) == LOW);
  int xValue = analogRead(xPin);
  int yValue = analogRead(yPin);

  if (buttonPressed) {
    // Osa X - kolik LED
    if (xValue < 341) {
      numLEDs = 1;
    } else if (xValue < 682) {
      numLEDs = 2;
    } else {
      numLEDs = 3;
    }

    // Osa Y - rychlost blikání
    blinkDelay = map(yValue, 0, 1023, 1000, 0); // 0–1s
    if (blinkDelay < 50) blinkDelay = 50;       // minimální možné zpoždění
  }

  // --- Blikání LED ---
  unsigned long currentMillis = millis();
  if (currentMillis - previousMillis >= blinkDelay) {
    previousMillis = currentMillis;
    ledState = !ledState;
  }

  // --- Nastavení LED ---
  for (int i = 0; i < 3; i++) {
    if (i < numLEDs && ledState) {
      digitalWrite(ledPins[i], HIGH);
    } else {
      digitalWrite(ledPins[i], LOW);
    }
  }

  // Debug výpis
  Serial.print("Button: "); Serial.print(buttonPressed ? "Pressed" : "Released");
  Serial.print(" | X: "); Serial.print(xValue);
  Serial.print(" | Y: "); Serial.print(yValue);
  Serial.print(" | LEDs: "); Serial.print(numLEDs);
  Serial.print(" | BlinkDelay: "); Serial.println(blinkDelay);
  delay(10);
}
</code></pre>

<div style="display:flex; justify-content:center; gap:10px; flex-wrap:wrap;">
  <video controls muted playsinline preload="metadata" style="max-width:80%; height:auto;" poster="/images/3D-tisk-váha.jpg">
    <source src="/videos/obvod.mp4" type="video/mp4">
    Váš prohlížeč nepodporuje video tag.
  </video>
</div> 