# slides_obrona.tex — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Napisać `slides_obrona.tex` — 15-slajdową prezentację na obronę pracy magisterskiej (~15 min), z wykresami pgfplots i zagregowanymi wynikami RQ1–RQ5.

**Architecture:** Nowy plik `slides_obrona.tex` (źródło `slides.tex` zostaje bez zmian). Preambuła identyczna jak `slides.tex` plus `\usepackage{pgfplots}`. Każde RQ = 1 slajd z wykresem pgfplots + bullet pointy. Slajdy budujemy inkrementalnie, kompilując po każdym zadaniu.

**Tech Stack:** LaTeX, Beamer (aspectratio=169), pgfplots (wykresy), TikZ (diagram systemu), biblatex/biber

---

## Pliki

- Tworzone: `docs/slides_obrona.tex`
- Nie modyfikowane: `docs/slides.tex`, `docs/bibliografia.bib`

---

### Task 1: Preambuła + szkielet + slajd tytułowy

**Files:**
- Create: `docs/slides_obrona.tex`

- [ ] **Krok 1: Utwórz plik z preambuła i pustym dokumentem**

```latex
\documentclass[aspectratio=169]{beamer}

\usepackage[T1]{fontenc}
\usepackage[utf8]{inputenc}
\usepackage{lmodern}
\usepackage[polish]{babel}
\usepackage{tikz}
\usetikzlibrary{positioning}
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}
\usepackage{fancyvrb}
\usepackage[backend=biber,style=authoryear]{biblatex}
\addbibresource{bibliografia.bib}

\title{Zastosowanie dużych modeli językowych do generowania konfiguracji Docker i Kubernetes}
\author{Bartłomiej Rasztabiga}
\newcommand{\supervisor}{Promotor: dr inż. Mateusz Modrzejewski}
\institute{Instytut Automatyki i Informatyki Stosowanej}
\date{Czerwiec 2026}

\begin{document}

\begin{frame}
    \titlepage
    \vspace{-1.5em}
    \centering
    \supervisor
\end{frame}

\end{document}
```

- [ ] **Krok 2: Skompiluj i sprawdź czy buduje się bez błędów**

```bash
cd /Users/rasztabigab/Studia/masters-thesis/docs
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: `slides_obrona.pdf` gotowy, 1 strona, tytuł i promotor widoczny.

- [ ] **Krok 3: Commit**

```bash
git add slides_obrona.tex
git commit -m "feat(slides): szkielet slides_obrona.tex z tytułem"
```

---

### Task 2: Agenda

**Files:**
- Modify: `docs/slides_obrona.tex` — dodaj przed `\end{document}`

- [ ] **Krok 1: Dodaj slajd Agenda**

```latex
\begin{frame}{Agenda}
    \begin{itemize}
        \item Motywacja i cel pracy
        \item Przegląd literatury i luki badawcze
        \item Pytania badawcze
        \item Metodyka i system badawczy
        \item Wyniki (RQ1–RQ5)
        \item Wnioski i implikacje praktyczne
        \item Wkład do wiedzy i dalsze kierunki
    \end{itemize}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 2 strony, agenda widoczna.

---

### Task 3: Motywacja + cel (slajd 3)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd Motywacja i cel**

```latex
\begin{frame}{Motywacja i cel pracy}
    \begin{columns}[T]
        \column{0.55\textwidth}
        \textbf{Problem:}
        \begin{itemize}
            \item IaC (Dockerfile, manifesty K8s) jest złożone i podatne na błędy przy ręcznym tworzeniu
            \item LLM obiecują automatyzację, lecz brak twardej oceny end-to-end w literaturze
            \item Generowanie kodu aplikacyjnego przez LLM jest dobrze zbadane --- generowanie infrastruktury znacznie słabiej
        \end{itemize}
        \column{0.45\textwidth}
        \textbf{Cel pracy:}\\
        Ocena możliwości i ograniczeń agentów LLM w autonomicznej generacji konfiguracji IaC (Dockerfile + Kubernetes).
        \vspace{1em}

        \textbf{Główne pytanie:}\\
        \textit{Czy agent LLM może --- bez ingerencji człowieka --- wygenerować funkcjonalne, bezpieczne i zgodne z dobrymi praktykami konfiguracje wdrożeniowe?}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj i sprawdź layout dwukolumnowy**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 3 strony, dwie kolumny czytelne.

---

### Task 4: Literatura + luki badawcze (slajd 4)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd Literatura + luki**

```latex
\begin{frame}{Przegląd literatury i luki badawcze}
    \begin{columns}[T]
        \column{0.48\textwidth}
        \textbf{Kluczowe prace:}
        \begin{itemize}
            \item \textbf{Repo2Run} \cite{hu_llm-based_2025} --- generacja środowisk Docker z repozytoriów
            \item \textbf{Don't Train, Just Prompt} \cite{kratzke_dont_2024} --- prompt engineering dla IaC
            \item \textbf{GenKubeSec} \cite{malul_genkubesec_2024} --- LLM a bezpieczeństwo K8s
            \item \textbf{CloudEval-YAML} \cite{xu_cloudeval-yaml_2023} --- benchmark dla konfiguracji chmurowych
        \end{itemize}
        \column{0.48\textwidth}
        \textbf{Luki badawcze:}
        \begin{itemize}
            \item Brak oceny autonomicznej --- agenty czytające kod, nie tylko opis słowny
            \item Dominuje walidacja statyczna/składniowa, brak weryfikacji \textbf{runtime}
            \item Brak ilościowej analizy powtarzalności i podatności na manipulację kontekstem
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj i sprawdź cytowania**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 4 strony, cytowania rozwiązane.

---

### Task 5: Pytania badawcze RQ1–RQ5 (slajd 5)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ**

```latex
\begin{frame}{Pytania badawcze}
    \begin{itemize}
        \item \textbf{RQ1:} Na ile agent generuje działające konfiguracje IaC end-to-end?
        \item \textbf{RQ2:} Jak złożoność systemu wpływa na skuteczność agenta?
        \item \textbf{RQ3:} Jaka jest jakość konfiguracji i czy \textit{prompt engineering} ją poprawia?
        \item \textbf{RQ4:} Na ile powtarzalny jest proces przy deterministycznych parametrach?
        \item \textbf{RQ5:} Jak podatny jest agent na manipulację kontekstem repozytorium?
    \end{itemize}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 5 stron.

---

### Task 6: System badawczy + modele (slajd 6)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd z diagramem i modelami**

```latex
\begin{frame}{Metodyka i system badawczy}
    \begin{columns}[T]
        \column{0.45\textwidth}
        \textbf{Modele:}
        \begin{itemize}
            \item OpenAI GPT-5 Mini
            \item Google Gemini 2.5 Flash
            \item DeepSeek V3.2
        \end{itemize}
        \vspace{0.5em}
        \textbf{Środowisko:} MicroK8s, lokalny rejestr obrazów\\[0.3em]
        \textbf{Podejście:} Jeden strzał (one-shot), brak pętli sprzężenia zwrotnego\\[0.3em]
        \textbf{Walidacja:} lint $\to$ build $\to$ apply $\to$ runtime (HTTP)

        \column{0.52\textwidth}
        \centering
        \begin{tikzpicture}[
            node distance=0.55cm and 0.3cm,
            box/.style={draw, rounded corners, align=center, font=\footnotesize,
                        minimum width=3.2cm, minimum height=0.65cm}
        ]
            \node[box] (repo) {Repozytorium (kod)};
            \node[box, below=of repo] (agent) {Agent LLM + narzędzia};
            \node[box, below=of agent] (cfg) {Dockerfile + manifesty K8s};
            \node[box, below=of cfg] (val) {Walidacja\\build / apply / runtime};
            \node[box, below=of val] (out) {Metryki + raport};
            \draw[->] (repo) -- (agent);
            \draw[->] (agent) -- (cfg);
            \draw[->] (cfg) -- (val);
            \draw[->] (val) -- (out);
            \node[font=\scriptsize, right=0.1cm of val] {MicroK8s};
        \end{tikzpicture}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj i sprawdź diagram**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 6 stron, diagram tikz wyrównany w prawej kolumnie.

- [ ] **Krok 3: Commit postępu**

```bash
git add slides_obrona.tex
git commit -m "feat(slides): slajdy 1-6 (wstęp, lit, RQ, system)"
```

---

### Task 7: RQ1 — Skuteczność (slajd 7)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ1 z wykresem pgfplots**

```latex
\begin{frame}{RQ1 --- Skuteczność end-to-end}
    \begin{columns}[T]
        \column{0.55\textwidth}
        \begin{tikzpicture}
        \begin{axis}[
            ybar,
            ymin=0, ymax=110,
            bar width=14pt,
            width=\columnwidth, height=5.2cm,
            xtick=data,
            symbolic x coords={Build,{K8s apply},Runtime,{apply/build},{runtime/apply}},
            x tick label style={font=\tiny, rotate=20, anchor=east},
            nodes near coords,
            nodes near coords style={font=\tiny, anchor=south},
            ymajorgrids=true, grid style=dashed,
            enlarge x limits=0.15,
            legend style={font=\tiny, at={(0.5,-0.25)}, anchor=north},
            legend columns=2,
            ylabel style={font=\footnotesize},
            ylabel={\%},
        ]
        \addplot[fill=blue!55, draw=blue!80!black] coordinates {
            (Build,78.7) ({K8s apply},76.7) (Runtime,62.7)
        };
        \addplot[fill=green!55!black, draw=green!70!black] coordinates {
            ({apply/build},97.5) ({runtime/apply},81.7)
        };
        \legend{Bezwarunkowe, Warunkowe}
        \end{axis}
        \end{tikzpicture}

        \column{0.42\textwidth}
        \textbf{N = 150} (25 repo $\times$ 3 modele $\times$ 2 powtórzenia)
        \vspace{0.5em}
        \begin{itemize}
            \item Największy spadek: etap \textbf{runtime} (62,7\%)
            \item Problemy semantyczne, nie składniowe --- błędy widoczne dopiero przy uruchomieniu
            \item Zmienne środowiskowe, zależności, konflikty wersji
            \item Jeśli build $\to$ apply prawie zawsze (97,5\%)
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj i sprawdź wykres**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 7 stron, 5 słupków w 2 kolorach z wartościami nad słupkami.

---

### Task 8: RQ2 — Złożoność (slajd 8)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ2**

```latex
\begin{frame}{RQ2 --- Wpływ złożoności na skuteczność}
    \begin{columns}[T]
        \column{0.55\textwidth}
        \begin{tikzpicture}
        \begin{axis}[
            ybar,
            ymin=0, ymax=110,
            bar width=20pt,
            width=\columnwidth, height=5.2cm,
            xtick=data,
            symbolic x coords={POC1,POC2,POC3,POC4,POC5},
            x tick label style={font=\footnotesize},
            nodes near coords,
            nodes near coords style={font=\tiny, anchor=south},
            ymajorgrids=true, grid style=dashed,
            enlarge x limits=0.15,
            ylabel style={font=\footnotesize},
            ylabel={\%},
        ]
        \addplot[
            fill={rgb,255:red,40;green,160;blue,80},
            draw={rgb,255:red,20;green,120;blue,50},
            point meta=explicit symbolic,
            nodes near coords style={font=\tiny}
        ] coordinates {
            (POC1,100) (POC2,33.3) (POC3,22.2) (POC4,11.1) (POC5,0)
        };
        \end{axis}
        \end{tikzpicture}

        \column{0.42\textwidth}
        \small
        \begin{tabular}{ll}
            \textbf{POC1} & FastAPI monolit \\
            \textbf{POC2} & +PostgreSQL \\
            \textbf{POC3} & +React \\
            \textbf{POC4} & +3 serwisy, RabbitMQ \\
            \textbf{POC5} & +Node.js, Redis \\
        \end{tabular}
        \vspace{0.5em}
        \begin{itemize}
            \item Spearman $= -1{,}0$
            \item Pearson $\approx -0{,}89$
            \item Różnica 100 p.p. (POC1 vs POC5)
            \item Złożoność = główne ograniczenie
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 8 stron, gradient kolorów słupków (opcjonalnie), 5 słupków malejących.

---

### Task 9: RQ3 — Jakość + prompt engineering (slajd 9)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ3 z wykresem grouped bar**

```latex
\begin{frame}{RQ3 --- Jakość konfiguracji i prompt engineering}
    \begin{columns}[T]
        \column{0.58\textwidth}
        \begin{tikzpicture}
        \begin{axis}[
            ybar,
            ymin=0, ymax=100,
            bar width=16pt,
            width=\columnwidth, height=5.2cm,
            xtick=data,
            symbolic x coords={{Przebiegi z ostrz.},{Bez ostrzeżeń}},
            x tick label style={font=\small},
            nodes near coords,
            nodes near coords style={font=\tiny, anchor=south},
            ymajorgrids=true, grid style=dashed,
            enlarge x limits=0.4,
            legend style={font=\small, at={(0.5,-0.22)}, anchor=north},
            legend columns=2,
            ylabel style={font=\footnotesize},
            ylabel={\%},
        ]
        \addplot[fill=red!60!white, draw=red!80!black] coordinates {
            ({Przebiegi z ostrz.},82.7) ({Bez ostrzeżeń},17.3)
        };
        \addplot[fill=green!55!black, draw=green!70!black] coordinates {
            ({Przebiegi z ostrz.},25.3) ({Bez ostrzeżeń},74.7)
        };
        \legend{Prompt bazowy, Prompt ulepszony}
        \end{axis}
        \end{tikzpicture}

        \column{0.39\textwidth}
        \textbf{N = 75} (25 repo $\times$ 3 modele)\\
        Narzędzia: Hadolint + Kube-linter
        \vspace{0.5em}
        \begin{itemize}
            \item Ostrzeżenia: $147 \to 30$\\(\textbf{$-79{,}6\%$})
            \item Przebiegi z ostrzeżeniami:\\$82{,}7\% \to 25{,}3\%$
            \item Bez ostrzeżeń:\\$17{,}3\% \to 74{,}7\%$
            \item Modele \textit{stosują} wytyczne z promptu
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 9 stron, grouped bar z 2 grupami (czerwony vs zielony).

---

### Task 10: RQ4 — Powtarzalność (slajd 10)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ4**

```latex
\begin{frame}{RQ4 --- Powtarzalność przy temperature=0}
    \begin{columns}[T]
        \column{0.55\textwidth}
        \begin{tikzpicture}
        \begin{axis}[
            ybar,
            ymin=0, ymax=1.05,
            bar width=20pt,
            width=\columnwidth, height=5.2cm,
            xtick=data,
            symbolic x coords={POC1,POC2,POC3,POC4,POC5},
            x tick label style={font=\footnotesize},
            nodes near coords,
            nodes near coords align={vertical},
            nodes near coords style={font=\tiny, anchor=south,
                /pgf/number format/.cd, fixed, precision=2},
            ymajorgrids=true, grid style=dashed,
            enlarge x limits=0.15,
            ylabel style={font=\footnotesize},
            ylabel={diff ratio (śr.)},
            yticklabel style={font=\footnotesize},
        ]
        \addplot[fill=blue!50, draw=blue!80!black] coordinates {
            (POC1,0.258) (POC2,0.462) (POC3,0.494) (POC4,0.878) (POC5,0.723)
        };
        \draw[dashed, red!70!black, thick] (axis cs:POC1-,0.4) -- (axis cs:POC5+,0.4)
            node[right, font=\tiny, red!70!black] {próg 0,4};
        \end{axis}
        \end{tikzpicture}

        \column{0.42\textwidth}
        \textbf{Metoda:} 5 powtórzeń, \texttt{temperature=0}, stały \texttt{seed}
        \vspace{0.5em}
        \[
            \texttt{diff\_ratio} = \frac{\text{zm. linie}}{\frac{1}{2}(|A|+|B|)}
        \]
        \begin{itemize}
            \item Średnia: \textbf{0,56} (mediana 0,55)
            \item $> 50\%$ linii różni się między powtórzeniami
            \item 7/10 kombinacji przekracza próg 0,4
            \item Niedeterminizm pochodzi z architektury agentowej, nie z próbkowania
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

Uwaga: linia przerywana `\draw[dashed,...]` z `axis cs:POC1-,` może wymagać korekty składni. Jeśli kompilator zgłosi błąd, zastąp linię przerywana uproszczoną wersją lub usuń ją.

Alternatywa jeśli linia przerywana nie kompiluje:
```latex
\draw[dashed, red!70!black, thick]
    (axis cs:POC1,0.4) -- (axis cs:POC5,0.4);
```

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 10 stron, 5 słupków rosnących (z wyjątkiem POC5 < POC4).

---

### Task 11: RQ5 — Manipulacja kontekstem (slajd 11)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd RQ5**

```latex
\begin{frame}{RQ5 --- Podatność na manipulację kontekstem}
    \begin{columns}[T]
        \column{0.52\textwidth}
        \begin{tikzpicture}
        \begin{axis}[
            xbar,
            xmin=0, xmax=85,
            bar width=18pt,
            width=\columnwidth, height=4.5cm,
            ytick=data,
            symbolic y coords={{W2: zał. bezp.},{W1: sprzeczna spec.},{W3: poz. zależność}},
            y tick label style={font=\small},
            nodes near coords,
            nodes near coords style={font=\small, anchor=west},
            xmajorgrids=true, grid style=dashed,
            enlarge y limits=0.35,
            xlabel style={font=\footnotesize},
            xlabel={\% przebiegów z odchyleniem},
        ]
        \addplot[fill=orange!65!white, draw=orange!80!black] coordinates {
            (33.3,{W2: zał. bezp.})
            (66.7,{W1: sprzeczna spec.})
            (70.0,{W3: poz. zależność})
        };
        \end{axis}
        \end{tikzpicture}

        \column{0.45\textwidth}
        \large\textbf{56,7\%} przebiegów\\z krytycznym odchyleniem
        \normalsize\textit{(51/90)}
        \vspace{0.5em}
        \begin{itemize}
            \item Agent ufa dokumentacji bardziej niż kodowi
            \item W1: błędny port 9000 zamiast 8080 --- agent przepisuje spójnie do całej konfiguracji
            \item W3: dodaje Redis bez żadnej zależności w kodzie
            \item Nieskomplikowane techniki = realne zagrożenie
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 11 stron, poziomy wykres słupkowy z 3 wariantami.

- [ ] **Krok 3: Commit postępu**

```bash
git add slides_obrona.tex
git commit -m "feat(slides): slajdy RQ1-RQ5 z wykresami pgfplots"
```

---

### Task 12: Wnioski + odpowiedź + implikacje (slajd 12)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd Wnioski**

```latex
\begin{frame}{Wnioski i implikacje praktyczne}
    \textbf{Odpowiedź na główne pytanie badawcze:}\\[0.3em]
    \begin{block}{}
        \textbf{Tak} --- dla prostych aplikacji jednokomponentowych z czytelną strukturą kodu.\\
        \textbf{Nie} --- dla złożonych systemów wielousługowych oraz środowisk z podwyższonymi wymaganiami bezpieczeństwa lub niezaufaną dokumentacją.
    \end{block}
    \vspace{0.4em}
    \textbf{Implikacje praktyczne:}
    \begin{itemize}
        \item \textbf{Ograniczony kontekst wejściowy} --- tylko pliki kodu, bez dokumentacji i historii (ogranicza RQ5)
        \item \textbf{Rozbudowana instrukcja systemowa} --- konkretna checklista dobrych praktyk redukuje ostrzeżenia o $>79\%$ (RQ3)
        \item \textbf{Obowiązkowa walidacja statyczna} --- Hadolint + Kube-linter jako element CI/CD
        \item \textbf{Ludzki przegląd} --- artefakty z security context i uprawnieniami wymagają weryfikacji
    \end{itemize}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 12 stron, blok z odpowiedzią wyróżniony.

---

### Task 13: Zagrożenia trafności (slajd 13)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd**

```latex
\begin{frame}{Zagrożenia trafności}
    \begin{itemize}
        \item Zbiór RQ1: 25 prostych aplikacji może nie uogólniać się na złożone systemy produkcyjne
        \item Walidacja runtime pojedynczym \texttt{curl} nie weryfikuje w pełni dostępności usługi
        \item 5 repozytoriów PoC (RQ2) --- zbyt mała próba do precyzyjnej charakterystyki punktu krytycznego złożoności
        \item Brak pętli sprzężenia zwrotnego z runtime --- architektura one-shot może zaniżać wyniki względem systemów iteracyjnych
    \end{itemize}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 13 stron.

---

### Task 14: Wkład do wiedzy + dalsze kierunki (slajd 14)

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd**

```latex
\begin{frame}{Wkład do wiedzy i dalsze kierunki}
    \begin{columns}[T]
        \column{0.52\textwidth}
        \textbf{Wkład do wiedzy:}
        \begin{itemize}
            \item Pierwsza empiryczna weryfikacja \textit{repo poisoning} (indirect prompt injection) w kontekście IaC
            \item Walidacja end-to-end z testami runtime --- ujawnia błędy niewidoczne dla narzędzi statycznych
            \item Ilościowy pomiar wpływu prompt engineeringu na jakość IaC ($-79{,}6\%$ ostrzeżeń)
        \end{itemize}
        \column{0.45\textwidth}
        \textbf{Dalsze kierunki:}
        \begin{itemize}
            \item Pętla sprzężenia zwrotnego z runtime --- agent reaguje na błędy wdrożenia
            \item Stabilizacja wyników przez wielokrotne generacje i agregację
            \item Zastosowanie w systemie PaaS --- automatyczne wdrożenie po podaniu linku do repozytorium
        \end{itemize}
    \end{columns}
\end{frame}
```

- [ ] **Krok 2: Skompiluj**

```bash
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: 14 stron.

---

### Task 15: Slajd końcowy + bibliografia + kompilacja finalna

**Files:**
- Modify: `docs/slides_obrona.tex`

- [ ] **Krok 1: Dodaj slajd Dziękuję i bibliografię**

```latex
\begin{frame}{}
    \centering
    \large Dziękuję za uwagę.
\end{frame}

\begin{frame}[allowframebreaks]{Bibliografia}
    \printbibliography
\end{frame}
```

- [ ] **Krok 2: Finalna kompilacja (dwukrotna, dla bibliografii)**

```bash
cd /Users/rasztabigab/Studia/masters-thesis/docs
latexmk -pdf -interaction=nonstopmode slides_obrona.tex
```

Oczekiwane: `slides_obrona.pdf` z 15 slajdami (bez strony bibliografii w liczeniu), brak ostrzeżeń o niezdefiniowanych referencjach.

- [ ] **Krok 3: Sprawdź PDF**

Zweryfikuj ręcznie:
- [ ] Slajd 7 (RQ1): 5 słupków w 2 kolorach, wartości nad słupkami
- [ ] Slajd 8 (RQ2): 5 słupków malejących POC1→POC5 (100%→0%)
- [ ] Slajd 9 (RQ3): grouped bar, 2 pary słupków
- [ ] Slajd 10 (RQ4): 5 słupków + linia przerywana 0,4
- [ ] Slajd 11 (RQ5): poziomy wykres, 3 warianty
- [ ] Slajd 12: blok z odpowiedzią warunkową wyróżniony
- [ ] Cytowania na slajdzie 4 rozwiązane

- [ ] **Krok 4: Commit końcowy**

```bash
git add slides_obrona.tex
git commit -m "feat(slides): slides_obrona.tex — kompletna prezentacja obrony (15 slajdów)"
```
