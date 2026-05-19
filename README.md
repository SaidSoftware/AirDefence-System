# 🛡️ Air Defense Simulation

<img width="1907" height="1010" alt="image" src="https://github.com/user-attachments/assets/2288a74f-9f5f-4e10-858f-6da769dda480" />

<div align="center">

![Version](https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge)
![.NET](https://img.shields.io/badge/.NET-8.0-purple?style=for-the-badge&logo=dotnet)
![Platform](https://img.shields.io/badge/Platform-Windows-lightblue?style=for-the-badge&logo=windows)
![License](https://img.shields.io/badge/Lizenz-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Aktiv-brightgreen?style=for-the-badge)

**Eine Echtzeit-Simulation eines Luftverteidigungssystems mit vollständiger Stadtmodellierung, intelligenter Bedrohungserkennung und detaillierter Ereignisverfolgung.**

</div>

---

## 📋 Inhaltsverzeichnis

- [Über das Projekt](#-über-das-projekt)
- [Features](#-features)
- [Systemarchitektur](#-systemarchitektur)
- [Klassendiagramm](#-klassendiagramm)
- [Komponentendiagramm](#-komponentendiagramm)
- [Installation](#-installation)
- [Verwendung](#-verwendung)
- [Eingabeparameter](#-eingabeparameter)
- [Validierung](#-validierung)
- [Tests](#-tests)
- [Projektstruktur](#-projektstruktur)
- [Technologien](#-technologien)
- [Mitwirkende](#-mitwirkende)

---

## 🎯 Über das Projekt

Die **Air Defense Simulation** ist eine objektorientierte Echtzeit-Simulationsanwendung, die komplexe Luftabwehrszenarien modelliert. Das System simuliert den Angriff feindlicher Luftobjekte auf eine Stadt und die automatisierte Reaktion eines Verteidigungssystems.

Das Projekt entstand als Lernprojekt im Bereich Softwarearchitektur und Simulation. Es demonstriert MVVM-Designmuster, objektorientierte Vererbungshierarchien und Echtzeit-Ereignisverarbeitung.

### Hauptziele:
- Modellierung realistischer Luftabwehrszenarien
- Visualisierung von Stadtschäden und Bevölkerungsverhalten
- Analyse und Auswertung von Verteidigungsstrategien
- Demonstration moderner Softwarearchitektur-Patterns

---

## ✨ Features

| Feature | Beschreibung |
|---|---|
| 🏙️ **Stadtmodellierung** | Dynamische Generierung von Gebäuden, Bevölkerung und Bunkern |
| ✈️ **3 Bedrohungstypen** | Kampfflugzeuge, Raketen und Drohnen mit individuellem Verhalten |
| 🛡️ **Automatische Abwehr** | Intelligentes Verteidigungssystem mit Zielverfolgung |
| 👥 **Evakuierungssimulation** | Bevölkerung reagiert mit Panik und Bunkersuche |
| 📊 **Timeline-Tracking** | Vollständige Ereignisverfolgung und Snapshot-Analyse |
| ⚡ **Echtzeit-Rendering** | Flüssige Visualisierung aller Simulationselemente |
| ✅ **Eingabevalidierung** | Robuste Prüfung aller Parameter mit klaren Fehlermeldungen |
| 🔄 **Steuerbarkeit** | Start, Pause und Reset der Simulation jederzeit möglich |

---

## 🏗️ Systemarchitektur

Das System basiert auf einer **4-schichtigen Architektur**:

```
┌─────────────────────────────────────┐
│         Presentation Layer          │
│        UI  │  ViewModel             │
├─────────────────────────────────────┤
│          Rendering Engine           │
│     Graphics  │  Visualization      │
├─────────────────────────────────────┤
│         Business Logic Layer        │
│  SimulationEngine │ CityManagement  │
│  AirObjects │ DefenseSystem         │
│          Timeline                   │
├─────────────────────────────────────┤
│            Data Layer               │
│  DataModels │ Configuration         │
│          Persistence                │
└─────────────────────────────────────┘
```

### Designprinzipien
- **MVVM-Pattern** für saubere Trennung von UI und Logik
- **Abstrakte Basisklassen** für alle Luftobjekte (`AirObject`)
- **Kompositions-Beziehungen** für Lebenszyklus-Management
- **Ereignisgesteuerte Architektur** für Timeline-Tracking

---

## 📐 Klassendiagramm

Das folgende Klassendiagramm zeigt alle Klassen und ihre Beziehungen:

```
City ──────────────────────────────────────────────────────────┐
 │ ◆ 1:*   ◆ 1:*   ◆ 1:*                                      │
 ▼          ▼        ▼                                         │
Building  Person   Bunker                               DefenseSystem
                                                              │ ◆ 1:*
            «abstract»                                        │
            AirObject ◄──────────────────────────────── DefenseMissile
               ▲  ▲  ▲  ▲                                (trackedTarget)
               │  │  │  │
     ┌─────────┘  │  │  └──────────┐
     │            │  │              │
EnemyFighter EnemyMissile EnemyDrone
```

**Beziehungstypen:**
- `◆` **Komposition** (1 zu 0..*) – Lebenszyklus abhängig
- `▲` **Vererbung** – Ableitung von `AirObject`
- `┄▶` **Abhängigkeit** (`«uses»`) – `MainViewModel` nutzt alle Hauptklassen
- `──▶` **Assoziation** – `DefenseMissile.TrackedTarget` zeigt auf `AirObject`

---

## 🧩 Komponentendiagramm

Das System ist in folgende Hauptkomponenten unterteilt:

**Presentation Layer:**
- `UI` – MainWindow, SimulationView, ControlPanel, StatisticsPanel
- `ViewModel` – MainViewModel, InputValidator, DataBinding

**Rendering Engine:**
- `Graphics` – RenderEngine, Canvas, DrawingContext, AnimationController
- `Visualization` – CityRenderer, AirObjectRenderer, EffectsRenderer

**Business Logic Layer:**
- `SimulationEngine` – SimulationController, CollisionDetector, PhysicsEngine
- `CityManagement` – City, Building, Person, Bunker, DamageCalculator
- `AirObjects` – AirObject (abstract), EnemyFighter, EnemyMissile, EnemyDrone, DefenseMissile
- `DefenseSystem` – TargetingSystem, ThreatAnalyzer, LaunchController
- `Timeline` – TimelineTracker, TimelineEvent, TimelineSnapshot

**Data Layer:**
- `DataModels` – Vector2D, Rect, SimulationState, EventType
- `Configuration` – SimulationParameters, ConfigManager, ValidationRules
- `Persistence` – DataSerializer, FileManager, ExportService

---

## 🚀 Installation

### Voraussetzungen

- [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- Windows 10 / Windows 11
- Visual Studio 2022 oder JetBrains Rider

### Schritt 1: Repository klonen

```bash
git clone https://github.com/dein-username/air-defense-simulation.git
cd air-defense-simulation
```

### Schritt 2: Abhängigkeiten installieren

```bash
dotnet restore
```

### Schritt 3: Projekt bauen

```bash
dotnet build --configuration Release
```

### Schritt 4: Anwendung starten

```bash
dotnet run --project AirDefenseSimulation
```

---

## 🎮 Verwendung

### Simulation starten

1. Anwendung öffnen
2. Eingabeparameter konfigurieren (siehe unten)
3. **„Simulation starten"** klicken
4. Simulationsverlauf beobachten
5. Statistiken in der Timeline auswerten

### Steuerung

| Aktion | Beschreibung |
|---|---|
| `StartSimulation()` | Startet die Simulation mit den aktuellen Parametern |
| `PauseSimulation()` | Hält die Simulation an, Zustand bleibt erhalten |
| `ResetSimulation()` | Setzt alles auf den Anfangszustand zurück |

---

## ⚙️ Eingabeparameter

| Parameter | Typ | Min | Max | Beschreibung |
|---|---|---|---|---|
| `FighterCount` | int | 0 | 100 | Anzahl feindlicher Kampfflugzeuge |
| `MissileCount` | int | 0 | 200 | Anzahl feindlicher Raketen |
| `DroneCount` | int | 0 | 150 | Anzahl feindlicher Drohnen |
| `Population` | int | 100 | 50.000 | Ausgangsbevölkerung der Stadt |
| `SimulationSpeed` | double | 0.1 | 10.0 | Geschwindigkeitsfaktor |
| `RocketCapacity` | int | 1 | 500 | Anzahl verfügbarer Abwehrraketen |

### Empfohlene Konfigurationen

**Einsteiger-Szenario:**
```
FighterCount=3 | MissileCount=5 | DroneCount=2
Population=5000 | SimulationSpeed=1.0 | RocketCapacity=20
```

**Mittleres Szenario:**
```
FighterCount=10 | MissileCount=20 | DroneCount=8
Population=10000 | SimulationSpeed=1.5 | RocketCapacity=50
```

**Intensiv-Szenario:**
```
FighterCount=25 | MissileCount=50 | DroneCount=20
Population=20000 | SimulationSpeed=2.0 | RocketCapacity=80
```

---

## ✅ Validierung

Das System prüft alle Eingaben mit klaren Fehlermeldungen:

```
Bitte korrigieren Sie folgende Eingabefehler:

• Das Feld 'Kampfflugzeuge' darf nicht leer sein.
• 'abc' ist keine gültige Zahl für 'Feindliche Raketen'.
• 'Population' muss mindestens 100 sein. Aktuell: 50
• 'Raketenkapazität' darf maximal 500 sein. Aktuell: 600
```

**Validierungsregeln:**
- Pflichtfelder dürfen **nicht leer** sein
- Werte müssen **gültige Zahlen** sein
- Werte müssen **innerhalb des erlaubten Bereichs** liegen
- Konfigurationswarnungen bei problematischen Szenarien (z.B. sehr wenige Abwehrraketen)

---

## 🧪 Tests

### Tests ausführen

```bash
dotnet test
```

### Testergebnisse (v1.0)

| Testkategorie | Anzahl | Bestanden | Quote |
|---|---|---|---|
| Komponententests | 14 | 14 | ✅ 100% |
| Vererbungstests | 5 | 5 | ✅ 100% |
| Kompositionstests | 4 | 4 | ✅ 100% |
| Systemtests | 3 | 3 | ✅ 100% |
| Performance-Tests | 2 | 2 | ✅ 100% |
| **Gesamt** | **28** | **28** | ✅ **100%** |

> Vollständiges Testprotokoll siehe [`TESTPROTOKOLL.md`](./docs/TESTPROTOKOLL.md)

---

## 📁 Projektstruktur

```
air-defense-simulation/
│
├── 📁 src/
│   ├── 📁 Models/
│   │   ├── City.cs
│   │   ├── Building.cs
│   │   ├── Person.cs
│   │   ├── Bunker.cs
│   │   ├── AirObject.cs          ← abstrakt
│   │   ├── EnemyFighter.cs
│   │   ├── EnemyMissile.cs
│   │   ├── EnemyDrone.cs
│   │   ├── DefenseMissile.cs
│   │   └── DefenseSystem.cs
│   │
│   ├── 📁 Timeline/
│   │   ├── TimelineTracker.cs
│   │   ├── TimelineEvent.cs
│   │   └── TimelineSnapshot.cs
│   │
│   ├── 📁 ViewModels/
│   │   ├── MainViewModel.cs
│   │   └── InputValidator.cs
│   │
│   ├── 📁 Views/
│   │   ├── MainWindow.xaml
│   │   └── SimulationView.xaml
│   │
│   └── 📁 Data/
│       ├── Vector2D.cs
│       ├── Rect.cs
│       └── SimulationParameters.cs
│
├── 📁 tests/
│   └── AirDefenseSimulation.Tests/
│
├── 📁 docs/
│   ├── UML_Klassendiagramm.png
│   ├── UML_Komponentendiagramm.png
│   └── TESTPROTOKOLL.md
│
├── README.md
├── LICENSE
└── AirDefenseSimulation.sln
```

---

## 🛠️ Technologien

| Technologie | Version | Verwendung |
|---|---|---|
| **.NET** | 8.0 | Laufzeitumgebung |
| **C#** | 12.0 | Programmiersprache |
| **MVVM** | – | Architektur-Pattern |
| **xUnit** | 2.6 | Unit-Testing |

---

## 📊 Metriken & Auswertung

Die Simulation liefert folgende Auswertungsmetriken:

```
Abfangquote      = TotalInterceptions / (FighterCount + MissileCount + DroneCount)
Verlustrate      = CasualtiesCount / InitialPopulation
Effizienz        = TotalInterceptions / MissilesLaunched
Stadtintegrität  = CityHealth (0–100%)
```

---

## 👥 Mitwirkende

| Name | Rolle |
|---|---|
| Entwickler | Architektur, Implementierung, Tests |

---

## 📄 Lizenz

Dieses Projekt steht unter der **MIT-Lizenz**.
Weitere Details in der Datei [`LICENSE`](./LICENSE).

---

<div align="center">

**Air Defense Simulation** – Entwickelt als Softwarearchitektur-Projekt

⭐ Wenn dir dieses Projekt gefällt, hinterlasse einen Stern!

</div>
