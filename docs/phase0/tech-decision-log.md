# Tech-Decision Log (WanderApp)  
*Stand: 2025-04 | Verantwortlich: Lead Developer*  

## 📌 Entscheidung: Flutter für Android + Web (iOS erst V1.2)  
| Aspekt | Begründung |
|--------|------------|
| **Einheitliche UI** | Barrierefreiheit erfordert konsistente Größen/Contrast – Flutter-Widgets bieten mehr Kontrolle als native Views |
| **Offline-DB** | `sqflite` (SQLite) ist stabil, dokumentiert & gut in Flutter integriert → wichtig für GPX-Parsing |
| **Karten** | `flutter_map` + `openstreetmap` → komplett kostenlos, keine API-Key-Grenzen wie bei Google |
| **Risiko** | iOS-Unterstützung verzögert sich um ~2 Monate | **Workaround**: Web-PWA als Notlösung bis iOS-Release |

## 📌 Entscheidung: Kein Backend im MVP  
| Aspekt | Begründung |
|--------|------------|
| **Datenverbleib lokal** | Vertrauen durch Transparenz („meine Daten – mein Handy“) → entspricht Zielgruppe 72+ |
| **Komplexität reduzieren** | Auth, Sync, Backup verlangsamen MVP-Loop |
| **Zukunftssicherung** | Wenn gewünscht: later add Google Drive backup API (ohne Rewrite nötig) |

> ✅ *Hinweis:* Diese Entscheidungen werden alle 2 Wochen im Team reviewt – ggf. Anpassung notwendig.

