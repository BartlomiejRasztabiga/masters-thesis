# Thesis Structure Notes

- **Rozdział 1 – Wprowadzenie (`tex/1-wprowadzenie.tex`)**: cel pracy, hipotezy H1–H5, motywacja; TODO dopisać opis/prototyp PaaS w końcówce i zaktualizować listę zagadnień.
- **Rozdział 2 – Przegląd literatury (`tex/2-przeglad-literatury.tex`)**: przegląd LLM w IaC (Docker, Kubernetes), generowanie, naprawa konfiguracji, bezpieczeństwo, wyzwania; merytorycznie kompletne.
- **Rozdział 3 – Przegląd narzędzi (`tex/3-przeglad-narzedzi.tex`)**: po przeglądzie; opis modeli i walidacji (Hadolint, Kube-linter) oraz narzędzi uruchomieniowych (Docker/K8s przez `docker`/`kubectl` zamiast SDK) jest spójny z kodem.
- **Rozdział 4 – Projekt eksperymentów (`tex/4-projekt-eksperymentow.tex`)**: metodologia i weryfikacja opisana szczegółowo dla H1; sekcja H2 (metodyka, metryki, kryteria) uzupełniona i rozszerzona o POC5, H3–H5 do uzupełnienia w kolejnej iteracji.
- **Rozdział 5 – Wyniki eksperymentów (`tex/5-wyniki-eksperymentow.tex`)**: wyniki per hipoteza, statystyki, walidacja (automatyczna, LLM-as-a-Judge, ekspercka); dodać wykresy/tabele i podsumowanie rozdziału.
- **Planowane rozdziały [TODO]**:
  - Rozdział 6 – Praktyczne zastosowanie (system PaaS): architektura, funkcje, demonstracja wdrożenia, ograniczenia.
  - Rozdział 7 – Wnioski i dalsze kierunki: podsumowanie weryfikacji H1–H5, ocena użyteczności agentów LLM w DevOps, przyszłe prace.
- **Dodatki**: abstrakty PL/EN w `main.tex` do aktualizacji po wynikach/PaaS; bibliografia w `bibliografia.bib` do uzupełnienia o nowe cytowania.
