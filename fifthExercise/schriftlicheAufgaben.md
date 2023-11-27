## Mugabe 1
Aufgabe 1)
Kommt drauf an, ob mit Test oder Trainingsdatensatz gemacht wird. Testdatensatz hat 500 Elemente, es wird aber bei Teilaufgabe 2 auf 501 Elemente geprüft.
Für 1) wäre Lösung: Trainingsdatensatz: 75/25. Testdatensatz: 50/50
Für 2) wäre Lösung: Trainingsdatensatz: 100/0, Testdatensatz: keine Entscheidung (50/50)?

k = 1 auf dem Trainingsdatensatz:
       Da k auf 1 gesetzt ist, wird für jeden Punkt im Trainingsdatensatz der Punkt mit der nächstgelegenen Nachbarschaft betrachtet.
Da es 750 Punkte mit Label 0 und 250 Punkte mit Label 1 gibt, wird der k-Nearest-Neighbor-Classifier immer das dominierende Label wählen, das in diesem Fall Label 0 ist.
Daher wird die Genauigkeit auf dem Trainingsdatensatz 75% betragen, da 75% der Punkte das Label 0 haben.

k = 501 auf dem Trainingsdatensatz und Testdatensatz:
Bei k = 501 werden für jeden Punkt die 501 nächsten Nachbarn betrachtet. Da es insgesamt 750 Punkte mit Label 0 und 250 Punkte mit Label 1 gibt, wird der k-Nearest-Neighbor-Classifier wiederum immer das dominierende Label wählen, Label 0.
Die Genauigkeit auf dem Trainingsdatensatz wird daher 100% betragen.
Die Genauigkeit auf dem Testdatensatz wird auch 50% betragen, da das k größer gewählt ist, als die Anzahl der Elemente, wird es runtergeschraubt auf k = 500. Da Label 0 und Label 1 beide 250 haben, gibt es eine Wahrscheinlichkeit von 50%. Es könnte auch sein, dass dort gar nicht entschieden wird, weil k größer als die Anzahl der Datenpunkte ist.
	
Auswirkungen, wenn zwei Punkte im Trainingsdatensatz die gleichen Koordinaten haben:
Wenn zwei Punkte im Trainingsdatensatz die gleichen Koordinaten haben, könnte dies die Ergebnisse beeinflussen. Bei k = 1 würde dies bedeuten, dass es zwei Punkte gibt, die identisch sind, und der nächste Nachbar wäre der gleiche Punkt. Dies könnte zu einer höheren Genauigkeit führen, da es möglicherweise weniger Unsicherheit in der Klassifikation gibt.
Bei k > 1 könnte dies zu einer Veränderung der Rangfolge der nächsten Nachbarn führen, da die Reihenfolge der Punkte im Datensatz entscheidend ist. Daher könnten identische Punkte die Entscheidungsfindung beeinflussen, wenn sie die gleichen Koordinaten haben.
In der Praxis ist es oft wünschenswert, dass keine zwei Punkte im Datensatz die gleichen Koordinaten haben, um solche Unsicherheiten zu vermeiden und eine stabilere Klassifikation zu gewährleisten.



## Aufgabe 2
Suche nach den k nächsten Nachbarn:
Die grundlegende Operation ist die Suche nach den k nächsten Nachbarn für einen gegebenen Punkt. Dies erfordert die Berechnung der Distanz zwischen diesem Punkt und allen anderen Punkten im Datensatz, was  O(n⋅d) Zeit benötigen kann, wobei n die Anzahl der Datenpunkte und d die Anzahl der Features ist.
		
Sortieren der Distanzen:
Nachdem die Distanzen berechnet wurden, müssen sie sortiert werden, um die k nächsten Nachbarn zu identifizieren. Dieser Schritt erfordert O(n logn) Zeit.

Entscheidung treffen:
Schließlich muss eine Entscheidung basierend auf den Labels der k nächsten Nachbarn getroffen werden.
Die Gesamtlaufzeit des kNN-Algorithmus für die Klassifizierung eines Punktes beträgt daher O(n⋅d + n logn).

Wo sind die Schwierigkeiten + Lösung?
Es werden immer die Werte für alle Datensätze ausgerechnet und bei einer großen Menge an Daten verbraucht dies sehr viel Rechenkapazität und ist Zeitaufwendig, da die Distanzenfür jeden Datenpunkt immer neu berechnet werden. 
Ein Lösungsansatz wäre, anstatt alle Punkte einzeln zu Betrachten, sie als Paare von Datenpunkten zu betrachten. Es wird ein Graph erstellt, in dem nur die Beziehungen zwischen nahe beieinander liegenden Punkten berücksichtigt werden. Dieser Graph wird dann für die Nachbarschaftssuche verwendet. 


## Aufgabe 3
(21, 4) -> (20, 0) ist 4,12
(21, 4) -> (10, 5) ist 11,04
(21, 4) -> (-10, 1) ist 31,14
(21, 4) -> (-20, 6) ist 41,05

# 1-Nearest-Neighbor-Classification mit Min-Max-Skalierung

In diesem Beispiel werden die Min-Max-Skalierung und die 1-Nearest-Neighbor-Classification auf Trainingsdaten angewendet.

## Trainingsdatenpunkte und Labels

- \( x_1 = (-10,1) \), \( y_1 = 0 \)
- \( x_2 = (10,5) \), \( y_2 = 1 \)
- \( x_3 = (-20,6) \), \( y_3 = 1 \)
- \( x_4 = (20,0) \), \( y_4 = 0 \)

## Testdatenpunkt und Label

- Testpunkt \( p = (21,4) \), Label \( y_p = 1 \)

## Min-Max-Skalierung

Die Min-Max-Skalierung wird auf die Trainings- und Testdaten angewendet, um die Werte in den Bereich [0, 1] zu normalisieren.

- \( x_{1, \text{skaliert}} = (0.25, 0.1667) \)
- \( x_{2, \text{skaliert}} = (0.75, 0.8333) \)
- \( x_{3, \text{skaliert}} = (0, 1) \)
- \( x_{4, \text{skaliert}} = (1, 0) \)
- \( p_{\text{skaliert}} = (1.025, 0.6667) \)

## Euklidische Distanzen nach der Skalierung

1. \( \text{Distanz}(p_{\text{skaliert}}, x_{1, \text{skaliert}}) \approx 0.5417 \)
2. \( \text{Distanz}(p_{\text{skaliert}}, x_{2, \text{skaliert}}) \approx 0.8594 \)
3. \( \text{Distanz}(p_{\text{skaliert}}, x_{3, \text{skaliert}}) \approx 1.2925 \)
4. \( \text{Distanz}(p_{\text{skaliert}}, x_{4, \text{skaliert}}) \approx 1.025 \)

## 1-Nearest-Neighbor-Classification

Der Testpunkt \( p \) wird dem Trainingspunkt \( x_2 \) zugeordnet, da \( x_2 \) die geringste euklidische Distanz aufweist. Das vorhergesagte Label für \( p \) ist daher \( \hat{y}_p = 1 \).
