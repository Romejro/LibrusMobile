# 🎓 Librus Mobile (Synergia)

Nowoczesny, szybki i przejrzysty nieoficjalny klient e-dziennika **LIBRUS Synergia** dla systemu Android, stworzony w całości przy użyciu **Jetpack Compose** oraz **Material 3**.

Aplikacja zapewnia intuicyjny dostęp do ocen, planu lekcji, terminarza, wiadomości oraz frekwencji bez zbędnych reklam i opóźnień.

---

## ✨ Główne funkcje

- 🔐 **Bezpieczne logowanie:**
  - Wygodne logowanie przez wbudowany WebView z automatyczną ekstrakcją sesji i ciasteczek.
  - Elegancka nakładka ładowania ukrywająca surowy interfejs webowy Synergii.
  - Automatyczne odnawianie wygasłej sesji w tle (w oparciu o zapisane dane uwierzytelniające w bezpiecznym magazynie).
  - Tryb **Demo** do testowania interfejsu bez konieczności logowania.

- 📊 **Oceny:**
  - Podział na przedmioty, kategorie wagowe oraz semestry.
  - Automatyczne wyliczanie średnich ważonych i arytmetycznych.
  - Oceny cząstkowe, przewidywane oraz końcowe.
  - Podgląd pełnych komentarzy, dat wpisania i nauczycieli wystawiających.

- 📅 **Plan lekcji:**
  - Przejrzysty widok tygodniowy z podziałem na godziny i dni robocze.
  - Intuicyjne przełączanie tygodni (poprzedni / bieżący / kolejny).
  - Oznaczenia zastępstw, odwołanych lekcji, gabinetów i notatek do zajęć.

- ✉️ **Wiadomości:**
  - Wielostronicowa skrzynka odbiorcza (obsługa paginacji formularzy Synergii).
  - Oznaczenia wiadomości przeczytanych / nieprzeczytanych oraz załączników.
  - Wyszukiwarka i filtry (wszystkie, nieprzeczytane).
  - Szybki podgląd treści wiadomości bez opuszczania aplikacji.

- 🗓️ **Terminarz i sprawdziany:**
  - Sprawdziany, kartkówki, zadania domowe i wydarzenia szkolne.
  - Kolorystyczne rozróżnienie wag i typów wydarzeń.
  - Dni wolne od szkoły i święta.

- ⏱️ **Frekwencja i e-Usprawiedliwienia:**
  - Statystyki frekwencji: obecności, nieobecności, spóźnienia, zwolnienia.
  - Podgląd wpisów z danego dnia oraz wysłanych e-usprawiedliwień.

- ⭐ **Zachowanie i Szczęśliwy numerek:**
  - Zestawienie punktów dodatnich i ujemnych z uwagami pedagogicznymi.
  - Aktualny szczęśliwy numerek na dany dzień.

- 🔔 **Synchronizacja w tle i powiadomienia:**
  - Okresowe sprawdzanie nowych ocen, wiadomości i wpisów w terminarzu przez `WorkManager`.
  - Powiadomienia push w systemie Android.
  - Tryb offline – pełny dostęp do ostatnio zsynchronizowanych danych bez połączenia z siecią.

---

## 🛠️ Stos technologiczny

| Komponent | Zastosowanie |
|---|---|
| **Język** | [Kotlin](https://kotlinlang.org/) 2.x |
| **Interfejs UI** | [Jetpack Compose](https://developer.android.com/jetpack/compose) + [Material Design 3](https://m3.material.io/) |
| **Architektura** | MVVM (Model-View-ViewModel), StateFlow, Coroutines |
| **Sieć i Scraping** | [OkHttp](https://square.github.io/okhttp/), [Jsoup](https://jsoup.org/) |
| **Zadania w tle** | [AndroidX WorkManager](https://developer.android.com/topic/libraries/architecture/workmanager) |
| **Serializacja** | [Gson](https://github.com/google/gson) |
| **Testy** | JUnit 4, AndroidX Test |
| **Minimalna wersja Androida** | Android 8.0 (API 26) |
| **Docelowa wersja Androida** | Android 15 / 16 (API 36/37) |

---

## 🚀 Budowanie i uruchomienie

### Wymagania wstępne:
- **Android Studio** (Ladybug / Meerkat lub nowszy)
- **JDK 17**
- **Android SDK** zainstalowany z platformą API 34+

### Komendy Gradle:

1. **Uruchomienie testów jednostkowych:**
   ```bash
   ./gradlew testDebugUnitTest
   ```

2. **Zbudowanie wersji debug (do testów na emulatorze/urządzeniu):**
   ```bash
   ./gradlew assembleDebug
   ```
   Plik wynikowy: `app/build/outputs/apk/debug/app-debug.apk`

3. **Zbudowanie podpisanej wersji Release (APK):**
   ```bash
   ./gradlew assembleRelease
   ```
   Plik wynikowy: `app/build/outputs/apk/release/app-release.apk`

4. **Zbudowanie pakietu App Bundle dla Google Play (AAB):**
   ```bash
   ./gradlew bundleRelease
   ```
   Plik wynikowy: `app/build/outputs/bundle/release/app-release.aab`

---

## 📂 Struktura projektu

```text
app/src/main/java/com/example/librusmobile/
├── data/
│   ├── model/          # Modele danych (Grade, Lesson, LibrusMessage, CalendarEvent, UserSession, ...)
│   ├── network/        # Klient sieciowy LibrusClient (scraping Jsoup, parsowanie sesji i stron Synergii)
│   └── repository/     # Repozytorium zarządzające stanem, cache i synchronizacją
├── ui/
│   ├── screens/        # Ekrany Compose (Grades, Timetable, Messages, Calendar, Attendance, Login, ...)
│   ├── theme/          # Konfiguracja kolorystyki i typografii Material 3
│   ├── LibrusViewModel.kt
│   └── MainActivity.kt
└── worker/             # SyncManager & LibrusSyncWorker (powiadomienia o ocenach i wiadomościach w tle)
```

---

## 🔒 Bezpieczeństwo i prywatność

- Aplikacja **nie przesyła** żadnych danych logowania, haseł ani danych szkolnych na żadne zewnętrzne serwery firm trzecich.
- Cała komunikacja odbywa się bezpośrednio pomiędzy urządzeniem a oficjalnymi serwerami platformy LIBRUS (`synergia.librus.pl`).
- Dane logowania i ciasteczka sesyjne przechowywane są wyłącznie lokalnie w chronionym magazynie `SharedPreferences` aplikacji.

---

## 📄 Licencja

Projekt stworzony w celach edukacyjnych i prywatnych. Znaki towarowe „Librus” oraz „Synergia” są własnością Librus Sp. z o.o.
