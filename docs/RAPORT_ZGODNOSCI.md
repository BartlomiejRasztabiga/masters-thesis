# Raport zgodności pracy z kodem i wynikami

**Zakres i źródła**
- Praca: `main.tex`, `tex/4-projekt-eksperymentow.tex`, `tex/5-wyniki-eksperymentow.tex`, `THESIS_NOTES.md`.
- Kod i konfiguracje: `/Users/rasztabigab/Studia/run/experiments/h1.yaml`, `/Users/rasztabigab/Studia/run/experiments/h2.yaml`, `/Users/rasztabigab/Studia/run/experiments/h3.yaml`, `/Users/rasztabigab/Studia/run/experiments/h4.yaml`, `/Users/rasztabigab/Studia/run/src/generator/tools/repository_tools.py`, `/Users/rasztabigab/Studia/run/src/generator/core/workspace.py`, `/Users/rasztabigab/Studia/run/scripts/summarize_experiment.py`.
- Wyniki: `/Users/rasztabigab/Studia/run/results/experiments/h1/20251212_175508`, `/Users/rasztabigab/Studia/run/results/experiments/h2/20251230_155353`, `/Users/rasztabigab/Studia/run/results/experiments/h3/20260103_211448`, `/Users/rasztabigab/Studia/run/results/experiments/h4/20260104_123319`.

**Podsumowanie zgodności**
- H1, H3 i H4 w pracy są liczbowo zgodne z artefaktami wyników, a konfiguracje H1/H3/H4 w kodzie odpowiadają opisom w rozdziale 4.
- H2 ma istotne rozbieżności: konfiguracja w kodzie nie odpowiada wynikom, a liczba powtórzeń w pracy nie zgadza się z wynikami.
- H5 nie ma wyników ani konfiguracji w kodzie; sekcja wyników w pracy jest pusta, a abstrakt deklaruje weryfikację wszystkich hipotez.

**H1 – Autonomiczna generacja funkcjonalnych konfiguracji**
- Zgodność konfiguracji: `experiments/h1.yaml` (25 repozytoriów, 3 modele, 2 powtórzenia) jest spójne z opisem w `tex/4-projekt-eksperymentow.tex` i z metadanymi w `results/experiments/h1/20251212_175508/status.json`.
- Zgodność wyników: tabele i liczby w `tex/5-wyniki-eksperymentow.tex` odpowiadają `results/experiments/h1/20251212_175508/results.tex` i `results.txt` (np. 94/150 = 62,7%, Build 118/150, Apply 115/150, Runtime 94/150).
- Zgodność kryterium repozytoriów: 16/25 repozytoriów z sukcesem ≥ 50% potwierdza się w `summary.csv`.
- Brak istotnych rozbieżności.

**H2 – Ograniczenia złożonościowe**
- Zgodność wyników z artefaktami: wartości w `tex/5-wyniki-eksperymentow.tex` odpowiadają `results/experiments/h2/20251230_155353/results.tex` i `results.txt` (np. 15/45 = 33,3%, trend 100%→0%).
- Rozbieżność liczby powtórzeń: w `tex/4-projekt-eksperymentow.tex` zapisano 2 powtórzenia, a `results/experiments/h2/20251230_155353/status.json` wskazuje 3 powtórzenia (łącznie 45 przebiegów).
- Konfiguracja w kodzie po resecie: `experiments/h2.yaml` zawiera POC1–POC5 i 3 modele, ale `repetitions: 1`, co nadal nie odpowiada wynikom (3 powtórzenia) ani opisowi w pracy (2 powtórzenia).
- Rozbieżność w artefakcie LaTeX: `results/experiments/h2/20251230_155353/results.tex` ma podpisy i etykiety od H1 (np. “Skuteczność etapów w H1”), co jest niezgodne semantycznie z H2.

**H3 – Jakość i zgodność z dobrymi praktykami**
- Zgodność konfiguracji: `experiments/h3.yaml` (25 repozytoriów, 3 modele, 2 prompty, 1 powtórzenie, `enable_runtime_validation: false`) jest zgodne z opisem w `tex/4-projekt-eksperymentow.tex`.
- Zgodność wyników jakości: wartości w `tex/5-wyniki-eksperymentow.tex` odpowiadają sekcji “H3 quality stats” w `results/experiments/h3/20260103_211448/results.txt` (62/75 vs 19/75, 147→30 ostrzeżeń, średnie 1,96→0,40).
- Spójność prompta: treść w dodatku `main.tex` jest zgodna z `prompts/best_practices.prompt`, ale w pracy występuje nazwa `best_practises` (pisownia), a w kodzie `best_practices`.
- Potencjalna niejasność: w pracy zapisano “wyłączono aplikowanie manifestów na klaster”, co odpowiada `enable_runtime_validation: false`. Skrypt `summarize_experiment.py` raportuje jednak etap “apply” na podstawie `k8s_syntax` (dry-run). Warto doprecyzować w pracy, że “apply” w H3 to walidacja syntaktyczna, nie rzeczywiste wdrożenie.

**H4 – Niezawodność i powtarzalność**
- Zgodność konfiguracji: `experiments/h4.yaml` (POC1–POC5, 2 modele, `temperature=0`, `seed=42`, 5 powtórzeń) jest spójne z opisem w `tex/4-projekt-eksperymentow.tex` i z `status.json`.
- Zgodność tabeli per repozytorium/model: wartości w `tex/5-wyniki-eksperymentow.tex` odpowiadają `repeatability.json` (avg diff ratio i tool steps mean/std).
- Zgodność wniosków cząstkowych: 7/10 kombinacji z diff ratio > 0,4 oraz 1/10 z odchyleniem > 20% potwierdza `repeatability.json`.
- Zgodność statystyki mediany: w pracy po korekcie mediana diff ratio wynosi 0,5401 i jest zgodna z `repeatability.json`. Średnia 0,5632 jest zgodna.

**H5 – Podatność na manipulację kontekstem**
- W pracy opisano metodykę i trzy warianty ataku (A1–A3), ale `results/experiments` nie zawiera H5, a w `experiments/` brak konfiguracji H5.
- W dodatku `main.tex` dla H5 wskazano jedno repozytorium (`poc-jailbreak1`), co nie odpowiada opisowi A1–A3 (trzy warianty). To wewnętrzna niespójność pracy.
- Sekcja H5 w `tex/5-wyniki-eksperymentow.tex` pozostaje w całości jako TODO.

**Inne aspekty zgodności**
- Liczba narzędzi agenta: w pracy podano 11 narzędzi; w kodzie `RepositoryTools.create_tools()` tworzy 11 narzędzi (zgodne).
- Usuwanie plików mylących: opis w pracy odpowiada implementacji w `RepositoryWorkspace._cleanup_confusing_files()`.
- Abstrakt w `main.tex` deklaruje weryfikację wszystkich pięciu hipotez, co jest niezgodne z brakiem wyników H5 oraz “częściowo potwierdzoną” H4.

**Uwagi i rzeczy do zrobienia**
- Ustalić spójność H2: albo zmienić `experiments/h2.yaml` na `repetitions: 3`, albo przeliczyć wyniki pod `repetitions: 1` lub `2` i zaktualizować liczby w pracy.
- Zaktualizować opis H2 w `tex/4-projekt-eksperymentow.tex` tak, aby liczba powtórzeń była spójna z wynikami i konfiguracją.
- Wyjaśnić w H3, że etap “apply” w raportach to walidacja syntaktyczna (dry-run), a nie realne wdrożenie.
- Ujednolicić nazwę prompta: `best_practises` → `best_practices` w `main.tex` i/lub opisie H3.
- Uzupełnić H5: dodać konfigurację eksperymentu, uruchomić i załączyć wyniki, albo jawnie oznaczyć hipotezę jako niezweryfikowaną.
- Usunąć/uzupełnić TODO w `tex/5-wyniki-eksperymentow.tex` (H5, porównanie modeli, synteza wyników) oraz w `THESIS_NOTES.md`.
- Zaktualizować abstrakt w `main.tex`, aby nie deklarował weryfikacji wszystkich pięciu hipotez, jeśli H5 pozostaje bez wyników.
- Jeśli `results.tex` ma być używany w pracy, poprawić podpisy i etykiety w `results/experiments/h2/.../results.tex` i `results/experiments/h3/.../results.tex`.
