# A.I.S.T.A.T.E – Artificial Intelligence Speech-To-Analysis-Translation Engine

Autor: **Tomasz Pawlicki**  
Plik główny: `app21.py`  
Dodatkowe narzędzie demonstracyjne diarizacji tekstu/audio: `dia1.py`

---

## Opis

A.I.S.T.A.T.E to graficzna aplikacja (PyQt5), która:

- wykonuje **transkrypcję mowy** do tekstu za pomocą **OpenAI Whisper** (lokalne modele),
- robi **diarizację mówców po głosie** z użyciem **pyannote.audio**,
- koloruje i porządkuje transkrypt według mówców,
- umożliwia **tłumaczenie** tekstu (HuggingFace Transformers),
- potrafi wykonywać prostą **analizę treści** i rozmowę z użyciem lokalnego LLM (Ollama).

Plik `dia1.py` zawiera uproszczone GUI w Tkinterze, pokazujące te same idee diarizacji tekstu i diarizacji po głosie (Whisper + pyannote).

---

## Funkcje

### 1. Transkrypcja (ASR – Whisper)

- Obsługiwane modele: `tiny`, `base`, `small`, `medium`, `large-v2`, `large-v3`.
- Modele są pobierane i przechowywane lokalnie w katalogu:
  - `~/konwerter_audio_ai/models/whisper`

### 2. Diarizacja mówców (pyannote.audio)

- Pipeline: `pyannote/speaker-diarization-3.1` (z fallbackiem do `3.0`).
- Audio wejściowe jest automatycznie przekodowywane do **WAV 16 kHz mono** przez `ffmpeg`,
  co eliminuje błędy w stylu:

  > file resulted in XXXX samples instead of the expected YYYY samples

- Działa zarówno z pyannote.audio 3.x, jak i 4.x (obsługa `output.speaker_diarization`).

### 3. Tłumaczenie (HuggingFace Transformers)

- Wykorzystuje modele z rodziny **Helsinki-NLP/opus-mt** (np. `pl→en`, `en→pl`, itd.).
- Modele MT przechowywane są w:
  - `~/konwerter_audio_ai/models/mt`

### 4. Analiza + LLM (Ollama)

- Aplikacja potrafi pytać lokalny serwer **Ollama** (np. `qwen2:1.5b-instruct`, `llama3.2:3b`),
- Z poziomu zakładki „Ustawienia” można:
  - sprawdzić połączenie z Ollama,
  - uruchomić lokalnie `ollama serve`,
  - pobierać i usuwać modele.

---

## Wymagania

- Python **3.10+** (testowane głównie pod **Linux/Kali/Ubuntu**).
- Zainstalowane paczki z `requirements.txt`:

  ```bash
  pip install -r requirements.txt
