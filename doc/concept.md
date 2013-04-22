
Jeder Kampf besteht aus n ∈ ℕ Armeen.
Er läuft in mehreren Runden ab.
Jede Armee besteht aus m ∈ ℕ Einheiten.

## Einheiten
Eine Einheit ist durch folgende Eigenschaften definiert:

* Einheitentyp
* Rüstung
* List der Waffensysteme
* Ausweichwahrscheinlichkeit _(0 < wd < 1)_
* wirkende Effekte
* Befehle

## Waffensystem
Jedes Waffensystem ist durch folgende Eigenschaften definiert:

* Waffengattung
* Schaden _(s > 0)_
* Trefferwahrscheinlichkeit _(0 < wt < 1)_
* Schussfrequenz _(f > 0)_
* Durchschlagsfaktor _(p >= 0)_
* initialen Durschlagstrefferwahrscheinlichkeit _(0 <= ipwt <= 1)_
* Durschlagstrefferwahrscheinlichkeitsfaktor _(0 <= dpwt <= 1)_
* Zielpriorität

Die Zielpriorität legt fest in welcher Reihenfolge die Ziele ausgewählt werden.
Also welcher Einheitentyp zuerst angegriffen werden soll. Ist für keine der
verbleibenden Einheiten eine Priorität definiert wird zufällig gewählt.

## Rüstung

Die Rüstung einer Einheit ist durch folgene Eigenschaften definiert:

 * Rüstungspunkte _(r > 0)_
 * Rüstungsregeneration _(rr >= 0)_
 * Regenerationsfrequenz _(rrf >= 0)_
 * Reflektionsfaktor _(rf >= 0)_

Sinkt die Rüstung einer Einheit auf oder unter 0 gilt diese Einheit als zerstört
und führt keine weiteren Aktionen aus, kann aber auch nicht mehr Ziel weiterer
Angriffe werden.

Die Regenerationsfrequenz wird analog zur Schussfrequenz behandelt.
Rüstungsregeneration wird vor der Schadenberechnung berechnet, startet jedoch eine
Aktionsrunden später.
Die Rüstung kann nicht über den vordefinierten Wert hinaus steigen.

## Effekt

## Befehle


## Schadenberechnung
Des weiteren wird der Schaden durch einen Rüstungsfaktor _(0 < rf < 1)_ bestimmt
der von dem Rüstungstyp und der Waffengattung abhängt.

Wahrscheinlichkeit für einen Treffer _t := wt*(1-wd)_

Schaden des Treffers: _s := s*rf_

Neue Rüstungspunkte: _r[n+1] := r[n]-s_


## Durchschlagsschaden
Der Durchschlagsfaktor bestimmt wie viel Schaden der Treffer bei jedem weiteren
Zeil verursacht. Nach jedem Treffer wird hierbei die Trefferwahrscheinlichkeit
wie folgt neu berechnet:

_wt = ipwt_
_ipwt = ipwt * dpwt_

Die Wahrscheinlichkeit für jeden weiteren Treffer leitet sich also aus der initialen
Durschlagstrefferwahrscheinlichkeit sowie dem Durschlagstrefferwahrscheinlichkeitsfaktor
ab. Dabei ist zu beachten das nach dem initialen Treffer immer der initialwert für
ipwt genutzt wird, für jeden weiteren Duchschlagstreffer wird diese dann neu berechnet.
Daraufhin wird dann erneut der oben beschriebene Ablauf durchgeführt um den weiteren
Schaden diese Angriffs auszuwerten.
Verfehlt ein Angriff werden keine weiteren Durschlagstreffer berechnet.

Die wirkenden Effekte können alle Faktoren der Schadenberechnung beeinflussen.
Beispiele:

* erhöhte wt für alle Systeme
* erhöhte wt für bestimmte Systeme
* erhöhter s gegen bestimmte Rüstungstypen

## Aktionsrunden
Jeder Kampf wird in mehreren Runden ausgetragen.
Jede Runde ist aufgeteilt in _c ∈ ℕ_ Aktionsrunden.
_c := kgv(∀f U ∀rrf)_
Dieser Wert wird am Anfang jeder Runde neu ermittelt.
Wärend einer Runde können keine neuen Einheiten in den Kampf eintreten.

In der ersten Aktionsrunde in einem Kampf schießt jeder.
Nach seinem Schuss wird die Angriffsverzögerung berechnet.
_ad := c / f_
In jeder Aktionsrunde wird dieser Wert um 1 gesenkt.
Wird ad <= 0, so darf diese Einheit wieder Angreifen.
