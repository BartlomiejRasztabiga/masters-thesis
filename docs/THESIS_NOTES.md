# Thesis Structure Notes

- **Prezentacja (`slides.tex`)**: uporządkowano slajdy per hipoteza (projekt $\rightarrow$ wyniki), przeniesiono opisy zbiorów danych do slajdów projektowych i dodano punkt o hipotezach w agendzie.
- **Rozdział 1 – Wprowadzenie (`tex/1-wprowadzenie.tex`)**: cel pracy, hipotezy H1–H5, motywacja; TODO zaktualizować listę zagadnień.
- **Rozdział 2 – Przegląd literatury (`tex/2-przeglad-literatury.tex`)**: przegląd LLM w IaC (Docker, Kubernetes), generowanie, naprawa konfiguracji, bezpieczeństwo, wyzwania; merytorycznie kompletne.
- **Rozdział 3 – Przegląd narzędzi (`tex/3-przeglad-narzedzi.tex`)**: po przeglądzie; opis modeli i walidacji (Hadolint, Kube-linter) oraz narzędzi uruchomieniowych (Docker/K8s przez `docker`/`kubectl` zamiast SDK) jest spójny z kodem.
- **Rozdział 4 – Projekt eksperymentów (`tex/4-projekt-eksperymentow.tex`)**: metodologia i weryfikacja opisana szczegółowo dla H1; sekcja H2 (metodyka, metryki, kryteria) uzupełniona i rozszerzona o POC5, w H3 zredukowano liczbę powtórzeń do 1; opisano projekt H4 (POC1--POC5, 2 modele, 5 powtórzeń) oraz doprecyzowano sposób liczenia \texttt{diff ratio} i próg 0{,}4 na podstawie wyników pilotażowych, H5 przebudowano na trzy warianty manipulacji kontekstem (conflicting spec, authoritative security, legacy dependency) oraz doprecyzowano, że ocena opiera się na analizie artefaktów bez walidacji runtime.
- **Załączniki (`main.tex`)**: zaktualizowano nazwy i opisy załączników, aby wskazać, że 25 repozytoriów dotyczy H1 i H3.
- **Rozdział 5 – Wyniki eksperymentów (`tex/5-wyniki-eksperymentow.tex`)**: wyniki per hipoteza, statystyki, walidacja automatyczna (Hadolint, Kube-linter); uzupełniono listę typowych problemów w H2, wyniki H3 (tabela i wniosek), H4 (powtarzalność, wnioski) oraz H5 (tabela, przykłady manipulacji, werdykt). Do dopracowania pozostają sekcje przekrojowe: porównanie modeli, synteza wyników i ograniczenia badania.
- **Planowany rozdział [TODO]**:
  - Rozdział 6 – Wnioski i dalsze kierunki: podsumowanie weryfikacji H1–H5, ocena użyteczności agentów LLM w DevOps, przyszłe prace.
- **Dodatki**: abstrakty PL/EN w `main.tex` do aktualizacji po wynikach; bibliografia w `bibliografia.bib` do uzupełnienia o nowe cytowania.
