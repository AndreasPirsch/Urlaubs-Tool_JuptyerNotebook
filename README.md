# Urlaubs-Tool_JuptyerNotebook
Beschreibung:

Dieses Notebook analysiert Urlaubsdaten eines

Unternehmens und gibt Einblick in Verteilung, Häufigkeit

und mögliche Engpässe.

Ziel ist es, die Urlaubsverteilung im Laufe eines Kalenderjahres zu analysieren. Das
Unternehmen möchte Engpässe erkennen, Stoßzeiten identifzieren und mögliche
Handlungsempfehlungen ableiten.

**1. Einleitung**

**2. Bibliotheken importieren**

import pandas as pd

import matplotlib.pyplot as plt

import seaborn as sns

from datetime import datetime

Visualisierung schöner darstellen

sns.set(style="whitegrid")

%matplotlib inline

**3. Daten einlesen**

Die Daten liegen im CSV-Format vor. Jede Zeile repräsentiert einen genehmigten Urlaubsantrag.

# Beispiel-Daten laden

df = pd.read_csv("/content/urlaubsantraege.csv", parse_dates=["start_datum", "end_datum"])

# Erster Blick auf die Daten

df.head()

**4. Datenüberblick und Vorbereitung**

Wir schauen uns die Struktur an und bereiten neue Spalten zur Analyse vor.

Basisinformationen

df.info()

Dauer berechnen

df["urlaubstage"] = (df["end_datum"] - df["start_datum"]).dt.days + 1

Monat extrahieren

df["monat"] = df["start_datum"].dt.month

**5. Explorative Analyse**

Wie ist der Urlaub über das Jahr verteilt? Welche Monate sind besonders beliebt?

 Urlaubstage pro Monat

urlaub_monat = df.groupby("monat")["urlaubstage"].sum().reset_index()

# Visualisierung

plt.figure(figsize=(10, 6))

sns.barplot(data=urlaub_monat, x="monat", y="urlaubstage", palette="Blues_d")

plt.title("Urlaubstage pro Monat")

plt.xlabel("Monat")

plt.ylabel("Anzahl Urlaubstage")

plt.xticks(range(0,12), ["Jan", "Feb", "Mär", "Apr", "Mai", "Jun", "Jul", "Aug", "Sep", "Okt"

plt.show()

**6. Weitere Analysen (optional)**

• Urlaub nach Abteilung

• Urlaub nach Mitarbeiter

• Durchschnittliche Urlaubsdauer

**7. Fazit**

Die Auswertung zeigt eine Konzentration von Urlauben in den Sommermonaten. Daraus lässt
sich ableiten, dass besonders im Juli und August eine erhöhte Ausfallrate vorliegt. Eine bessere
Urlaubsplanung könnte helfen, Engpässe zu vermeiden.
