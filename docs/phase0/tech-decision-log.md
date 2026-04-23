# Tech-Decision Log (WanderApp)  
**Stand**: 2025-04 | **Letzte Revision**: 10.06.2025  

## 📌 Entscheidung: Flutter als einzige Codebasis (Android, iOS, Web)  
| Aspekt | Begründung |
|--------|------------|
| **Einheitliche UI/UX** | Barrierefreiheit erfordert *exakt* gleiche Interaktionen auf allen Geräten – Flutter-Widgets bieten hier maximale Konsistenz (z. B. Touch-Target ≥48dp überall, gleicher Contrast). Native Implementierungen sind fehleranfällig (iOS: VoiceOver ≠ Android TalkBack). |
| **Offline-Fokus** | `sqflite`, `path_provider`, `flutter_secure_storage` – alle成熟ed Packages mit stabiler iOS-Unterstützung (siehe [pub.dev/stats](https://pub.dev/packages/sqflite)). Kein Known-Issue für iOS 14+. |
| **Karten** | `flutter_map` + OpenStreetMap → *vollständig offline-fähig*, keine API-Limits, keine Kosten. iOS-Unterstützung seit v3.0 stabil ([siehe Changelog](https://github.com/fluttermap/flutter_map/blob/main/CHANGELOG.md)). |
| **iOS-Entwicklungsgeschwindigkeit** | ❌ *Keine Verzögerung* – im Gegenteil: Wir bauen iOS parallel mit Android (CI/CD mit GitHub Actions). |
| **Risiko** | Nur bei *Platform Channels* oder *Native UI-Modulen* kann es zu Aufwänden kommen (z. B. HealthKit für Schrittzähler). → Aber: Für MVP reicht GPS-Daten aus `location`-Package (iOS & Android kompatibel). |
| **Workaround?** | 🔴 **Nicht nötig!** Wir verzichten bewusst auf Web-PWA als „Notlösung“, da: <br> 1. PWA ist für *Wandern* ungeeignet (kein Offline-Cache-Speicher im Browser, keine Hintergrund-GPS-Verfolgung) <br> 2. PWA verletzt das Vertrauensversprechen „App auf dem Handy“ <br> → Stattdessen: **iOS-Release innerhalb von 4 Wochen nach Android** (durch paralleles Testen & Review). |

## 📌 Entscheidung: Kein Backend im MVP  
| Aspekt | Begründung |
|--------|------------|
| **Datenverbleib lokal** | Vertrauen durch Transparenz → entspricht Zielgruppe 72+ (siehe Persona „Herr Müller“) |
| **Keine Auth-Hürden** | App kann sofort genutzt werden – kein E-Mail, keine Passwortwahl. |
| **Zukunftssicherung** | Backup über Google Drive oder iCloud Drive später als *optional* integrierbar (ohne Architektur-Änderung). |

> ✅ **Entscheidung bestätigt am 08.06.2025 im Team**: Flutter ist der einzige Weg zu einer konsistenten, barrierefreien App in <3 Monaten MVP.
