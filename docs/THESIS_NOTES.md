# Thesis Structure Notes

- **Prezentacja (`slides.tex`)**: terminologia zmieniona na pytania badawcze (projekt $\rightarrow$ wyniki).
- **Rozdział 1 – Wprowadzenie (`tex/1-wprowadzenie.tex`)**: cel pracy, pytania badawcze RQ1–RQ5, motywacja.
- **Rozdział 2 – Przegląd literatury (`tex/2-przeglad-literatury.tex`)**: przegląd LLM w IaC (Docker, Kubernetes), generowanie, naprawa konfiguracji, bezpieczeństwo, wyzwania; merytorycznie kompletne.
- **Rozdział 3 – Przegląd narzędzi (`tex/3-przeglad-narzedzi.tex`)**: po przeglądzie; opis modeli i walidacji (Hadolint, Kube-linter) oraz narzędzi uruchomieniowych (Docker/K8s przez `docker`/`kubectl` zamiast SDK) jest spójny z kodem.
- **Rozdział 4 – Projekt eksperymentów (`tex/4-projekt-eksperymentow.tex`)**: metodologia opisana per pytanie badawcze RQ1--RQ5; RQ2 rozszerzono o POC5, w RQ3 zredukowano liczbę powtórzeń do 1; opisano RQ4 (POC1--POC5, 2 modele, 5 powtórzeń) oraz sposób liczenia \texttt{diff ratio}; RQ5 obejmuje trzy warianty manipulacji kontekstem (sprzeczna specyfikacja, autorytatywne zalecenia bezpieczeństwa, pozorna zależność historyczna), a ocena opiera się na analizie artefaktów bez walidacji runtime.
- **Załączniki (`main.tex`)**: zaktualizowano nazwy i opisy załączników, aby wskazać, że 25 repozytoriów dotyczy RQ1 i RQ3.
- **Rozdział 5 – Wyniki eksperymentów (`tex/5-wyniki-eksperymentow.tex`)**: wyniki per pytanie badawcze, statystyki, walidacja automatyczna (Hadolint, Kube-linter); uzupełniono listę typowych problemów w RQ2, wyniki RQ3 (tabela i dyskusja), RQ4 (powtarzalność, wnioski) oraz RQ5 (tabela, przykłady manipulacji, dyskusja). Do dopracowania pozostają sekcje przekrojowe: porównanie modeli, synteza wyników i ograniczenia badania.
- **Planowane rozdziały [TODO]**:
  - Rozdział 6 – Dyskusja wyników: przekrojowa interpretacja odpowiedzi na RQ1–RQ5, porównanie modeli, znaczenie praktyczne wyników oraz ograniczenia badania i zagrożenia dla trafności.
  - Rozdział 7 – Podsumowanie i dalsze kierunki badań: syntetyczne podsumowanie pracy, końcowa ocena przydatności agentów LLM w DevOps oraz propozycje dalszych badań.
- **Dodatki**: abstrakty PL/EN w `main.tex` do aktualizacji po wynikach; bibliografia w `bibliografia.bib` do uzupełnienia o nowe cytowania.
