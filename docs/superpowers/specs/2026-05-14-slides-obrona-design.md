---
name: slides-obrona-design
description: Projekt prezentacji na obronę pracy magisterskiej — slides_obrona.tex, 15 minut, 15 slajdów, pgfplots, wyniki zagregowane
metadata:
  type: project
---

# Projekt: slides_obrona.tex

Przepisanie prezentacji seminarium dyplomowego na prezentację obrony. Nowy plik `slides_obrona.tex` (źródło `slides.tex` zostaje bez zmian).

## Wymagania

- Czas: ~15 minut
- Slajdy: 15
- Podejście: klasyczna narracja akademicka A→Z
- Wykresy: pgfplots (te same co w pracy)
- Bez podziału na modele w wykresach — tylko wyniki zagregowane
- 1 slajd literatura + luki (zamiast 2)
- 1 slajd na RQ (zamiast 2 — projekt + wyniki)
- RQ5 z pełnymi wynikami (był "projekt" w starych slajdach)

## Struktura slajdów

| # | Tytuł | Czas | Uwagi |
|---|-------|------|-------|
| 1 | Tytuł | — | titlepage, promotor |
| 2 | Agenda | 0.5' | |
| 3 | Motywacja + cel | 1.5' | problem IaC + LLM, cel główny, główne pytanie badawcze |
| 4 | Literatura + luki (1 slajd) | 1' | 2 kolumny: 4 prace kluczowe | 3 luki badawcze |
| 5 | Pytania badawcze RQ1–RQ5 | 0.5' | lista 5 RQ |
| 6 | System + modele + metodyka | 1.5' | diagram tikz pipeline + 3 modele + MicroK8s, 1 shot |
| 7 | RQ1 — Skuteczność | 1.5' | pgfplots bar: build/apply/runtime + warunkowe |
| 8 | RQ2 — Złożoność | 1.5' | pgfplots bar: POC1-5 (100%→0%), Spearman=-1.0 |
| 9 | RQ3 — Jakość + prompt engineering | 1.5' | pgfplots grouped bar: bazowy vs ulepszony |
| 10 | RQ4 — Powtarzalność | 1' | pgfplots bar: śr. diff_ratio per POC (agregat) |
| 11 | RQ5 — Manipulacja kontekstem | 1.5' | pgfplots hbar: per wariant ataku + nagłówek 56.7% |
| 12 | Wnioski + odpowiedź + implikacje | 2' | odpowiedź warunkowa pogrubiona + 3 implikacje |
| 13 | Zagrożenia trafności | 0.5' | 3-4 punkty |
| 14 | Wkład do wiedzy + dalsze kierunki | 1' | 2 kolumny: 3 wkłady | 3 kierunki |
| 15 | Dziękuję | — | |

**Łącznie: ~15 minut**

## Dane do wykresów

### RQ1 (N=150)
- Build: 78.7% (118/150)
- K8s apply: 76.7% (115/150)
- Runtime: 62.7% (94/150)
- apply|build: 97.5% (115/118)
- runtime|apply: 81.7% (94/115)

### RQ2 (N=45)
- POC1: 100.0% (9/9)
- POC2: 33.3% (3/9)
- POC3: 22.2% (2/9)
- POC4: 11.1% (1/9)
- POC5: 0.0% (0/9)
- Spearman = -1.0, Pearson ≈ -0.89

### RQ3 (N=75)
- Przebiegi z ostrzeżeniami: 82.7% (bazowy) → 25.3% (ulepszony)
- Konfiguracje bez ostrzeżeń: 17.3% (bazowy) → 74.7% (ulepszony)
- Łącznie ostrzeżeń: 147 → 30 (-79.6%)

### RQ4 — zagregowane diff_ratio (śr. Gemini + DeepSeek)
- POC1: 0.2583
- POC2: 0.4623
- POC3: 0.4942
- POC4: 0.8784
- POC5: 0.7227
- Średnia ogółem: 0.56, mediana: 0.55

### RQ5 (N=90)
- Ogółem: 56.7% (51/90)
- W1 sprzeczna specyfikacja: 66.7% (20/30)
- W2 autorytatywne zalecenia bezpieczeństwa: 33.3% (10/30)
- W3 pozorna zależność historyczna: 70.0% (21/30)

## Treść kluczowych slajdów

### Slajd 3 — Motywacja + cel
- IaC (Dockerfile, K8s) jest złożone i podatne na błędy przy ręcznym tworzeniu
- LLM obiecują automatyzację, ale brak oceny end-to-end w literaturze
- Cel: ocena możliwości i ograniczeń agentów LLM w autonomicznej generacji konfiguracji IaC
- Główne pytanie: _Czy agent LLM może bez ingerencji człowieka wygenerować funkcjonalne, bezpieczne i zgodne z dobrymi praktykami konfiguracje wdrożeniowe?_

### Slajd 4 — Literatura + luki
- Lewa kolumna (prace): Repo2Run, Don't Train Just Prompt, GenKubeSec, CloudEval-YAML
- Prawa kolumna (luki): brak oceny autonomicznej (agent czyta kod), brak walidacji runtime, brak analizy powtarzalności i ataków kontekstowych

### Slajd 6 — System + modele + metodyka
- Diagram tikz: repozytorium → agent LLM → Dockerfile+manifesty → walidacja (build/apply/runtime) → metryki
- 3 modele: GPT-5 Mini, Gemini 2.5 Flash, DeepSeek V3.2
- Środowisko: MicroK8s, lokalny rejestr, jeden shot bez pętli sprzężenia zwrotnego

### Slajd 12 — Wnioski
- Odpowiedź warunkowa (pogrubiona): _tak dla prostych jednokomponentowych; nie dla złożonych wielousługowych i środowisk z niezaufaną dokumentacją_
- Implikacje: ograniczony kontekst wejściowy, rozbudowana instrukcja systemowa, walidacja statyczna + ludzki przegląd bezpieczeństwa

### Slajd 14 — Wkład + dalsze kierunki
- Wkład (3 z 5): pierwsza empiryczna weryfikacja repo poisoning w IaC, walidacja end-to-end z runtime, kwantyfikacja prompt engineeringu (-79.6%)
- Dalej: pętla sprzężenia zwrotnego z runtime, stabilizacja przez agregację, zastosowanie w PaaS

## Decyzje techniczne
- Plik: `slides_obrona.tex` (nowy, źródło `slides.tex` niezmienione)
- Preambuła: ta sama co slides.tex (beamer aspectratio=169, babel polish, biblatex)
- Wykresy: pgfplots (ybar / xbar), bez podziału na modele
- Diagram systemu: tikz (rozbudowanie istniejącego z slides.tex)
- Motyw beamera: bez zmian (domyślny)
