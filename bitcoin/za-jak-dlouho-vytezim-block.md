---
layout: math
title: Za jak dlouho vytezim block
---

[bitcoin](.)

# {{ page.title }}

Chci tezit sam na sebe, za jak dlouho najdu blok?

Je na to jednoduchy vypocet. Vypocet je pouze statisticky odhad.

Nejdrive si popiseme vstupy vypoctu:

* difficulty - je nasobek zaklani difficulty (2^32)
* hashrate - je to hashrate v hash za sekundu

Vysledek je cas ve vterinach.

<div class="math">t = \frac{difficulty * 2^{32}}{hashrate}</div>

Protoze hashrate je dnes zalezitost GH/s, vypocet trosku upravime:

<div class="math">t = \frac{difficulty * 2^{32}}{hashrate\_ghps * 10^{9}}</div>


Aktualni difficulty (16. 4. 2015) je __49446390688.24__.

Muzeme si ukazat nejake priklady

#### 300 MH/s

    t = (difficulty * 2^32) / (hashrate_ghps * 10^9)
      = (49446390688.24 * 2^32) / (0.3 * 10^9)
      = 49446390688 sekund = 8193311 dni = 22447 let

#### 50 TH/s

    t = (difficulty * 2^32) / (hashrate_ghps * 10^9)
      = (49446390688.24 * 2^32) / (50*10^3 * 10^9)
      = 4247412 sekund = 49 dni

#### 12 PH/s (Slush Pool)

    t = (difficulty * 2^32) / (hashrate_ghps * 10^9)
      = (49446390688.24 * 2^32) / (50*10^6 * 10^9)
      = 17697 sekund = 4.9 hodin

#### 302 PH/s (Bitcoin Network)

    t = (difficulty * 2^32) / (hashrate_ghps * 10^9)
      = (49446390688.24 * 2^32) / (302*10^6 * 10^9)
      = 702 sekund = 10 min


Vypocet prepisu do pythonu:

    def time_to_block(hashrate_ghps, difficulty):
        return (difficulty * (2**32)) / (hashrate_ghps * (10**9))


<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.2.0/katex.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/KaTeX/0.2.0/katex.min.js"></script>

<script>
var elements = document.getElementsByClassName('math');
for (i = 0; i < elements.length; i++){
    katex.render(elements[i].innerHTML, elements[i]);
}
</script>

