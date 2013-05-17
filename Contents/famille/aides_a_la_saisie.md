# Les aides à la saisie {#core-ref:0b2d4cd0-4eed-41d8-ac57-37525a444194}
 
## Présentation {#core-ref:6378bc90-1560-4463-9995-8a22921c656d}

Une *aide à la saisie* permet de compléter ou de remplir des zones de saisie
lors de la modification d'un document, en proposant des suggestions à l'utilisateur.

Les suggestions sont calculées au moyen d'une fonction qui doit être définie dans
un fichier php placé dans le répertoire `/EXTERNALS/` du contexte.

Elle doit retourner un résultat sous la forme d'un tableau à 2 dimensions :

*   la première dimension correspond à la liste des suggestions ;
*   la seconde dimension correspond à la *liste des valeurs*
    à insérer dans le document lors du choix de cette suggestion.
    
    Elle est traitée de manière positionnelle :
    
    *   La première valeur est affichée en tant que suggestion pour l'utilisateur ;
    *   les valeurs suivantes sont *dépilées* et affectées dans l'ordre aux attributs cible.

Elle peut également retourner une chaîne de caractères,
qui servira de message d'erreur.


## Syntaxe {#core-ref:c3ea0d07-1032-4abf-9746-df01e9434247}

La syntaxe définissant les aides à la saisie est la suivante :

<div class="grammar">

<svg width="684" height="132" viewBox="-8 -58 684 132 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-36" >inputHelp:</text>
<rect class="symbol_rect" x="30" y="-14" width="96" height="28" rx="1" />
<text class="symbol_text" x="78" y="4" >funcName</text>
<rect class="terminal_rect" x="150" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="163" y="4" >(</text>
<rect class="symbol_rect" x="236" y="-14" width="116" height="28" rx="1" />
<text class="symbol_text" x="294" y="4" >funcInputs</text>
<path class="path" d="M236 44 L252 44" />
<path class="path" d="M200 0 L236 0 M200 0 Q212 0 212 12 M388 0 L352 0 M388 0 Q376 0 376 12" />
<path class="path" d="M224 44 L236 44 M224 44 Q212 44 212 32 L212 12 M364 44 L252 44 M364 44 Q376 44 376 32 L376 12" />
<rect class="terminal_rect" x="412" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="425" y="4" >)</text>
<rect class="terminal_rect" x="462" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="475" y="4" >:</text>
<rect class="symbol_rect" x="512" y="-14" width="126" height="28" rx="1" />
<text class="symbol_text" x="575" y="4" >funcOutputs</text>
<path class="path" d="M126 0 L150 0" />
<path class="path" d="M176 0 L200 0" />
<path class="path" d="M388 0 L412 0" />
<path class="path" d="M438 0 L462 0" />
<path class="path" d="M488 0 L512 0" />
<path class="path" d="M0 0 L30 0 M668 0 L638 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M668 -6 L668 6" />
</svg>

<svg width="458" height="144" viewBox="-8 -86 458 144 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-64" >funcInputs:</text>
<rect class="symbol_rect" x="30" y="-14" width="106" height="28" rx="1" />
<text class="symbol_text" x="83" y="4" >funcInput</text>
<rect class="terminal_rect" x="208" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="221" y="4" >,</text>
<rect class="symbol_rect" x="258" y="-14" width="106" height="28" rx="1" />
<text class="symbol_text" x="311" y="4" >funcInput</text>
<path class="path" d="M234 0 L258 0" />
<path class="path" d="M208 0 L184 0 M196 0 Q184 0 184 -12 L184 -36 Q184 -48 196 -48 L376 -48 Q388 -48 388 -36 L388 -12 Q388 0 376 0 L364 0 L388 0" />
<path class="path" d="M208 0 L160 0 Q172 0 172 12 L172 24 Q172 36 184 36 L388 36 Q400 36 400 24 L400 12 Q400 0 412 0 L364 0 M160 0 L184 0 M388 0 L412 0" />
<path class="path" d="M136 0 L160 0" />
<path class="path" d="M0 0 L30 0 M442 0 L412 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M442 -6 L442 6" />
</svg>

<svg width="856" height="380" viewBox="-8 -86 856 380 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-64" >funcInput:</text>
<rect class="terminal_rect" x="78" y="-14" width="96" height="28" rx="28" />
<text class="terminal_text" x="126" y="4" >&lt;spaces&gt;</text>
<path class="path" d="M78 0 L54 0 M66 0 Q54 0 54 -12 L54 -36 Q54 -48 66 -48 L186 -48 Q198 -48 198 -36 L198 -12 Q198 0 186 0 L174 0 L198 0" />
<path class="path" d="M78 0 L30 0 Q42 0 42 12 L42 24 Q42 36 54 36 L198 36 Q210 36 210 24 L210 12 Q210 0 222 0 L174 0 M30 0 L54 0 M198 0 L222 0" />
<rect class="symbol_rect" x="282" y="-14" width="206" height="28" rx="1" />
<text class="symbol_text" x="385" y="4" >sourceAttributeName</text>
<rect class="symbol_rect" x="282" y="30" width="206" height="28" rx="1" />
<text class="symbol_text" x="385" y="48" >familyParameterName</text>
<rect class="symbol_rect" x="282" y="74" width="56" height="28" rx="1" />
<text class="symbol_text" x="310" y="92" >text</text>
<rect class="symbol_rect" x="282" y="118" width="146" height="28" rx="1" />
<text class="symbol_text" x="355" y="136" >sourceKeyWord</text>
<rect class="symbol_rect" x="282" y="162" width="136" height="28" rx="1" />
<text class="symbol_text" x="350" y="180" >propertyName</text>
<rect class="terminal_rect" x="282" y="206" width="26" height="28" rx="28" />
<text class="terminal_text" x="295" y="224" >{</text>
<rect class="symbol_rect" x="332" y="206" width="176" height="28" rx="1" />
<text class="symbol_text" x="420" y="224" >appParameterName</text>
<rect class="terminal_rect" x="532" y="206" width="26" height="28" rx="28" />
<text class="terminal_text" x="545" y="224" >}</text>
<path class="path" d="M308 220 L332 220" />
<path class="path" d="M508 220 L532 220" />
<rect class="terminal_rect" x="282" y="250" width="26" height="28" rx="28" />
<text class="terminal_text" x="295" y="268" >{</text>
<rect class="symbol_rect" x="332" y="250" width="116" height="28" rx="1" />
<text class="symbol_text" x="390" y="268" >familyName</text>
<rect class="terminal_rect" x="472" y="250" width="26" height="28" rx="28" />
<text class="terminal_text" x="485" y="268" >}</text>
<path class="path" d="M308 264 L332 264" />
<path class="path" d="M448 264 L472 264" />
<path class="path" d="M246 0 L282 0 M246 0 Q258 0 258 12 M594 0 L488 0 M594 0 Q582 0 582 12" />
<path class="path" d="M270 44 L282 44 M270 44 Q258 44 258 32 L258 12 M570 44 L488 44 M570 44 Q582 44 582 32 L582 12" />
<path class="path" d="M270 88 L282 88 M270 88 Q258 88 258 76 L258 32 M570 88 L338 88 M570 88 Q582 88 582 76 L582 32" />
<path class="path" d="M270 132 L282 132 M270 132 Q258 132 258 120 L258 76 M570 132 L428 132 M570 132 Q582 132 582 120 L582 76" />
<path class="path" d="M270 176 L282 176 M270 176 Q258 176 258 164 L258 120 M570 176 L418 176 M570 176 Q582 176 582 164 L582 120" />
<path class="path" d="M270 220 L282 220 M270 220 Q258 220 258 208 L258 164 M570 220 L558 220 M570 220 Q582 220 582 208 L582 164" />
<path class="path" d="M270 264 L282 264 M270 264 Q258 264 258 252 L258 208 M570 264 L498 264 M570 264 Q582 264 582 252 L582 208" />
<rect class="terminal_rect" x="666" y="-14" width="96" height="28" rx="28" />
<text class="terminal_text" x="714" y="4" >&lt;spaces&gt;</text>
<path class="path" d="M666 0 L642 0 M654 0 Q642 0 642 -12 L642 -36 Q642 -48 654 -48 L774 -48 Q786 -48 786 -36 L786 -12 Q786 0 774 0 L762 0 L786 0" />
<path class="path" d="M666 0 L618 0 Q630 0 630 12 L630 24 Q630 36 642 36 L786 36 Q798 36 798 24 L798 12 Q798 0 810 0 L762 0 M618 0 L642 0 M786 0 L810 0" />
<path class="path" d="M222 0 L246 0" />
<path class="path" d="M594 0 L618 0" />
<path class="path" d="M0 0 L30 0 M840 0 L810 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M840 -6 L840 6" />
</svg>

<svg width="478" height="144" viewBox="-8 -86 478 144 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-64" >funcOutputs:</text>
<rect class="symbol_rect" x="30" y="-14" width="116" height="28" rx="1" />
<text class="symbol_text" x="88" y="4" >funcOutput</text>
<rect class="terminal_rect" x="218" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="231" y="4" >,</text>
<rect class="symbol_rect" x="268" y="-14" width="116" height="28" rx="1" />
<text class="symbol_text" x="326" y="4" >funcOutput</text>
<path class="path" d="M244 0 L268 0" />
<path class="path" d="M218 0 L194 0 M206 0 Q194 0 194 -12 L194 -36 Q194 -48 206 -48 L396 -48 Q408 -48 408 -36 L408 -12 Q408 0 396 0 L384 0 L408 0" />
<path class="path" d="M218 0 L170 0 Q182 0 182 12 L182 24 Q182 36 194 36 L408 36 Q420 36 420 24 L420 12 Q420 0 432 0 L384 0 M170 0 L194 0 M408 0 L432 0" />
<path class="path" d="M146 0 L170 0" />
<path class="path" d="M0 0 L30 0 M462 0 L432 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M462 -6 L462 6" />
</svg>

<svg width="354" height="132" viewBox="-8 -58 354 132 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-36" >funcOutput:</text>
<rect class="symbol_rect" x="66" y="-14" width="206" height="28" rx="1" />
<text class="symbol_text" x="169" y="4" >targetAttributeName</text>
<rect class="symbol_rect" x="66" y="30" width="146" height="28" rx="1" />
<text class="symbol_text" x="139" y="48" >targetKeyWord</text>
<path class="path" d="M30 0 L66 0 M30 0 Q42 0 42 12 M308 0 L272 0 M308 0 Q296 0 296 12" />
<path class="path" d="M54 44 L66 44 M54 44 Q42 44 42 32 L42 12 M284 44 L212 44 M284 44 Q296 44 296 32 L296 12" />
<path class="path" d="M0 0 L30 0 M338 0 L308 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M338 -6 L338 6" />
</svg>

<svg width="324" height="176" viewBox="-8 -58 324 176 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-36" >text:</text>
<rect class="terminal_rect" x="66" y="-14" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="4" >&apos;</text>
<rect class="terminal_rect" x="116" y="-14" width="76" height="28" rx="28" />
<text class="terminal_text" x="154" y="4" >&lt;text&gt;</text>
<path class="path" d="M92 0 L116 0" />
<rect class="terminal_rect" x="66" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="48" >&apos;</text>
<rect class="terminal_rect" x="116" y="30" width="76" height="28" rx="28" />
<text class="terminal_text" x="154" y="48" >[^&apos;,]+</text>
<rect class="terminal_rect" x="216" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="229" y="48" >&apos;</text>
<path class="path" d="M92 44 L116 44" />
<path class="path" d="M192 44 L216 44" />
<rect class="terminal_rect" x="66" y="74" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="92" >&quot;</text>
<rect class="terminal_rect" x="116" y="74" width="76" height="28" rx="28" />
<text class="terminal_text" x="154" y="92" >[^&quot;,]+</text>
<rect class="terminal_rect" x="216" y="74" width="26" height="28" rx="28" />
<text class="terminal_text" x="229" y="92" >&quot;</text>
<path class="path" d="M92 88 L116 88" />
<path class="path" d="M192 88 L216 88" />
<path class="path" d="M30 0 L66 0 M30 0 Q42 0 42 12 M278 0 L192 0 M278 0 Q266 0 266 12" />
<path class="path" d="M54 44 L66 44 M54 44 Q42 44 42 32 L42 12 M254 44 L242 44 M254 44 Q266 44 266 32 L266 12" />
<path class="path" d="M54 88 L66 88 M54 88 Q42 88 42 76 L42 32 M254 88 L242 88 M254 88 Q266 88 266 76 L266 32" />
<path class="path" d="M0 0 L30 0 M308 0 L278 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M308 -6 L308 6" />
</svg>

<svg width="534" height="352" viewBox="-8 -58 534 352 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-36" >sourceKeyWord:</text>
<rect class="terminal_rect" x="66" y="-14" width="36" height="28" rx="28" />
<text class="terminal_text" x="84" y="4" >CT</text>
<rect class="terminal_rect" x="66" y="30" width="36" height="28" rx="28" />
<text class="terminal_text" x="84" y="48" >CT</text>
<rect class="terminal_rect" x="126" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="139" y="48" >[</text>
<rect class="symbol_rect" x="176" y="30" width="226" height="28" rx="1" />
<text class="symbol_text" x="289" y="48" >relationAttributeName</text>
<rect class="terminal_rect" x="426" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="439" y="48" >]</text>
<path class="path" d="M102 44 L126 44" />
<path class="path" d="M152 44 L176 44" />
<path class="path" d="M402 44 L426 44" />
<rect class="terminal_rect" x="66" y="74" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="92" >D</text>
<rect class="terminal_rect" x="66" y="118" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="136" >I</text>
<rect class="terminal_rect" x="66" y="162" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="180" >K</text>
<rect class="terminal_rect" x="66" y="206" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="224" >T</text>
<rect class="terminal_rect" x="66" y="250" width="26" height="28" rx="28" />
<text class="terminal_text" x="79" y="268" >A</text>
<path class="path" d="M30 0 L66 0 M30 0 Q42 0 42 12 M488 0 L102 0 M488 0 Q476 0 476 12" />
<path class="path" d="M54 44 L66 44 M54 44 Q42 44 42 32 L42 12 M464 44 L452 44 M464 44 Q476 44 476 32 L476 12" />
<path class="path" d="M54 88 L66 88 M54 88 Q42 88 42 76 L42 32 M464 88 L92 88 M464 88 Q476 88 476 76 L476 32" />
<path class="path" d="M54 132 L66 132 M54 132 Q42 132 42 120 L42 76 M464 132 L92 132 M464 132 Q476 132 476 120 L476 76" />
<path class="path" d="M54 176 L66 176 M54 176 Q42 176 42 164 L42 120 M464 176 L92 176 M464 176 Q476 176 476 164 L476 120" />
<path class="path" d="M54 220 L66 220 M54 220 Q42 220 42 208 L42 164 M464 220 L92 220 M464 220 Q476 220 476 208 L476 164" />
<path class="path" d="M54 264 L66 264 M54 264 Q42 264 42 252 L42 208 M464 264 L92 264 M464 264 Q476 264 476 252 L476 208" />
<path class="path" d="M0 0 L30 0 M518 0 L488 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M518 -6 L518 6" />
</svg>

<svg width="534" height="132" viewBox="-8 -58 534 132 " xmlns="http://www.w3.org/2000/svg" version="1.1">
<defs><style type="text/css">.terminal_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.terminal_text{fill:black;font-family:Verdana,Sans-serif;text-anchor:middle;font-size:14px;}.symbol_rect{fill:rgb(206,255,206);stroke:black;stroke-width:2;}.symbol_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-style:italic;text-anchor:middle;font-size:14px;}.path{fill:none;stroke:black;stroke-width:2;}.rule_text{fill:black;font-family:Verdana,Sans-serif;font-weight:bold;font-size:14px;}.rule_path_edge{fill:none;stroke:black;stroke-width:3;}</style></defs>
<text class="rule_text" x="0" y="-36" >targetKeyWord:</text>
<rect class="terminal_rect" x="66" y="-14" width="36" height="28" rx="28" />
<text class="terminal_text" x="84" y="4" >CT</text>
<rect class="terminal_rect" x="66" y="30" width="36" height="28" rx="28" />
<text class="terminal_text" x="84" y="48" >CT</text>
<rect class="terminal_rect" x="126" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="139" y="48" >[</text>
<rect class="symbol_rect" x="176" y="30" width="226" height="28" rx="1" />
<text class="symbol_text" x="289" y="48" >relationAttributeName</text>
<rect class="terminal_rect" x="426" y="30" width="26" height="28" rx="28" />
<text class="terminal_text" x="439" y="48" >]</text>
<path class="path" d="M102 44 L126 44" />
<path class="path" d="M152 44 L176 44" />
<path class="path" d="M402 44 L426 44" />
<path class="path" d="M30 0 L66 0 M30 0 Q42 0 42 12 M488 0 L102 0 M488 0 Q476 0 476 12" />
<path class="path" d="M54 44 L66 44 M54 44 Q42 44 42 32 L42 12 M464 44 L452 44 M464 44 Q476 44 476 32 L476 12" />
<path class="path" d="M0 0 L30 0 M518 0 L488 0" />
<path class="rule_path_edge" d="M0 -6 L0 6 M518 -6 L518 6" />
</svg>

</div>

Ce qui donne en [BNF][WP_BNF] :

    inputHelp       ::= funcName '(' ( funcInputs |  ) ')' ':' funcOutputs
    
    funcInputs      ::= funcInput ( ',' funcInput )*
    
    funcInput       ::= '<spaces>'* ( sourceAttributeName | familyParameterName | text | sourceKeyWord | propertyName | '{' appParameterName '}' | '{' familyName '}' ) '<spaces>'*
    
    funcOutputs     ::= funcOutput ( ',' funcOutput )*
    
    funcOutput      ::= ( targetAttributeName | targetKeyWord )
    
    text            ::= ( "'" '<text>' ) | ( "'" "[^',]+" "'" ) | ( '"' '[^",]+' '"' )
    
    sourceKeyWord   ::= ( 'CT' | 'CT' '[' relationAttributeName ']' | 'D' | 'I' | 'K' | 'T' | 'A' )
    
    targetKeyWord   ::= ( 'CT' | 'CT' '[' relationAttributeName ']' )

avec les éléments suivants :

sourceAttributeName
:   Un nom d'attribut existant dans la famille.
    
    La fonction de calcul recevra la valeur de l'attribut au moment de l'appel.
    
    Lorsque *attributeName* est dans un array, alors la valeur passée est :
    
    *   la valeur sur la même ligne si l'attribut sur lequel est définie
        l'aide à la saisie est dans le même tableau,
    *   la valeur de la colonne (sous la forme d'un tableau php) si l'attribut
        sur lequel est définie l'aide à la saisie est en dehors du tableau
    *   la valeur sur la même ligne  si l'attribut est dans un autre tableau, ce
        qui peut conduire à des comportements surprenants.

familyParametername
:   Un nom de paramètre existant dans la famille.
    
    La fonction de calcul recevra la valeur du paramètre au moment de l'appel.

sourceKeyWord
:   Un mot clé qui est remplacé par une valeur dynamique.
    
    CT[relationAttributeName]
    :   La valeur de l'input correspondant à la relation *relationAttributeName*.
        
        Lorsque l'id est rempli, cela correspond au titre du document cible,
        sinon cela correspond au texte saisi dans cet input.
    
    CT
    :   Raccourci pour CT[currentAttributeName]
        (où *currentAttributeName* est le nom de l'attribut sur lequel est définie
        l'aide à la saisie).
        
        Ne peut être utilisé que sur les attributs de type relation.
    
    D
    :   Accès à la base de données.
    
    I
    :   Id du document courant.
    
    K
    :   L'index de la ligne en cours si l'attribut est dans un tableau.
        
        Si l'attribut n'est pas dans un tableau, la valeur passée est `-1`
    
    T
    :   L'objet php correspondant au document en cours.
        
        L'objet récupéré est le document tel qu'il est en base de donnée.
    
    A
    :   L'action courante (un objet de la classe `Action`).
        
        Cela permet, par exemple, de récupérer des informations sur
        l'utilisateur courant.

propertyName
:   Une propriété du document.
    
    Elle sera remplacée par sa valeur.

appParameterName
:   Un paramètre applicatif.
    
    Ce paramètre doit obligatoirement être global.

familyName
:   Un nom logique de famille.
    
    Il sera remplacé par son *id*.

targetAttributeName
:   Un nom d'attribut existant dans la famille.
    
    Lors du choix d'une des suggestions, les valeurs correspondant à ces
    suggestions sont insérées dans l'ordre dans les attributs désignés par
    *targetAttributeName*

targetKeyWord
:   Un mot clé désignant la cible de l'aide à la saisie.
    
    CT[relationAttributeName]
    :   L'input correspondant à la relation *relationAttributeName*.
    
    CT
    :   Raccourci pour CT[currentAttributeName]
        (où *currentAttributeName est le nom de l'attribut sur lequel est définie
        l'aide à la saisie).
    
    ?
    :   permet de "sauter" une des valeurs de retour sans l'utiliser.
        
        Est particulièrement utile dans le cas d'aides à la saisie génériques
        qui retournent plus de valeurs que d'attributs à compléter.

## Exemples {#core-ref:009f3b42-23a0-4599-91fc-f3589db52c55}

### Retour unique {#core-ref:6b090586-613e-4a0f-91ba-fa2c5ccc33af}

| attrid    | label | type | visibility | phpfile    | phpfunc                        |
| -         |       |      |            |            |                                |
| city_name | Ville | text | W          | cities.php | getCities(city_name):city_name |

    [php]
    <?php
    /**
     * EXTERNALS/cities.php
     */
    
    function getCities($userInput=''){
        $suggestions = array();
        // Liste des villes utilisables
        $availableCities = array(
            "Paris",
            "Toulouse",
            "Souillac"
        );
        //teste si les villes correspondent à la saisie de l'utilisateur
        foreach($availableCities as $city){
            if( ''===$userInput || preg_match(strToLower($userInput), strToLower($city)) ){
                $suggestions[] = array(
                    $city,      //le nom de la suggestion
                    $city       //la valeur qui ira dans attr_city
                );
            }
        }
        return $suggestions;
    }
    
    ?>

### Retour multiple {#core-ref:56dc74f4-488f-48f9-86a5-3a6af94404c3}

| attrid     | label       | type | visibility | phpfile      | phpfunc                                     |
| -          |             |      |            |              |                                             |
| city_name  | Ville       | text | W          | `cities.php` | `getCities(city_name):city_name`            |
| city_cedex | Code postal | int  | W          | `cities.php` | `getCedex(city_cedex):city_cedex,city_name` |



    [php]
    <?php
    /**
     * EXTERNALS/cities.php
     */
    
    function getCedex($userInput=''){
        $suggestions = array();
        // Liste des villes utilisables
        $availableCities = array(
            "75000" => "Paris",
            "31000" => "Toulouse",
            "46200" => "Souillac"
        );
        //teste si les villes correspondent à la saisie de l'utilisateur
        foreach($availableCities as $cedex => $city){
            if( ''===$userInput || preg_match($userInput, $cedex) ){
                $suggestions[] = array(
                    sprintf("[%d] %s", $cedex, $city),      //le nom de la suggestion
                    $cedex,                                 //la valeur qui ira dans attr_cedex
                    $city                                   //la valeur qui ira dans attr_city
                );
            }
        }
        return $suggestions;
    }
    
    ?>

## Astuces {#core-ref:b9c6c197-ae52-4c5c-ab0d-5ca968a3cd32}

### attributs relation {#core-ref:71c36648-8145-4dc5-985b-d6967cdf1b94}

*   Lorsqu'une aide à la saisie remplit un attribut de type *docid*,
    il faut penser à remplir l'id et le titre affiché (*attrid* et *CT[attrid]*).
*   Lorsqu'un attribut est masqué (visibilité R ou H), alors le champ désigné
    par *CT[attrid]* n'existe pas, il est donc impossible de les désigner comme
    retour des aides à la saisie.

### attributs htmltext {#core-ref:04bb23b2-21a6-43b9-b4a7-6616091878bf}

*   Lorsqu'un attribut de type *htmltext* est utilisé en entrée
    d'une aide à la saisie, la valeur reçue est encodée. il est donc nécessaire
    de la décoder (au moyen de [html_entity_decode][PHP_html_entity_decode])

<!-- links -->
[WP_BNF]: http://fr.wikipedia.org/wiki/Backus_Naur_Form "Définition de la Forme de Backus-Naur sur Wikipedia"
[PHP_html_entity_decode]: http://php.net/manual/fr/function.html-entity-decode.php "Documentation de html_entity_decode sur php.net"