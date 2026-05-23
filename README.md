🇵🇱 Wersja Polska: Podsumowanie Techniczne
1. Cel i przeznaczenie
Kod stanowi implementację interfejsu graficznego (GUI) opartego na bibliotece VCL (C++Builder), służącego do modyfikacji, ekstrakcji oraz zarządzania plikami archiwalnymi .MIX z niewymienionej z nazwy gry komputerowej (architektura wskazuje na gry oparte na silnikach strategicznych lub zręcznościowych z przełomu lat 90. i 00., wykorzystujące algorytm RefPack). Głównym celem aplikacji jest automatyzacja procesu wypakowywania zasobów poziomów (mapy, obiekty, tekstury) do celów modyfikacji (tzw. "moddingu").
2. Główne funkcjonalności

    Skanowanie struktury katalogów (ScanSphereFolder): Automatyczne przeszukiwanie folderów aplikacji (SPHERE1 do SPHERE3), identyfikacja podfolderów poziomów i wizualizacja struktury plików w komponencie drzewa (TTreeView).
    Walidacja i selekcja plików (Button1Click): Filtrowanie otwieranego pliku za pomocą systemowego okna dialogowego i twardo zakodowana weryfikacja na podstawie białej listy oficjalnych plików poziomów (np. L1_DC.MIX, L3_DH.MIX).
    Automatyczny Backup: Przed przystąpieniem do operacji na pliku .MIX, aplikacja tworzy jego kopię bezpieczeństwa w dedykowanym katalogu KOPY_MIX.
    Rozpoznawanie zawartości archiwum (Heurystyka i Rozmiar):
        Funkcja LooksLikeMap analizuje nagłówek pliku pod kątem występowania specyficznych wartości liczbowych w celu identyfikacji pliku mapy.
        Wydzielanie typów plików (MAP - mapa, ODF - definicje obiektów, TEX - tekstury) na podstawie relatywnych różnic w rozmiarach plików wewnątrz archiwum (dla archiwów zawierających 2 lub 3 pliki).
    Ekstrakcja niskopoziomowa (extract_file): Wydobywanie surowych strumieni danych z określonych przesunięć (offsetów) wewnątrz pliku .MIX i zapisywanie ich do osobnych plików na dysku.

3. Stos technologiczny i zależności

    Środowisko i Język: C++ (C++Builder / Embarcadero RAD Studio).
    Biblioteki GUI: VCL (Visual Component Library) – użycie komponentów TForm1, TTreeView, TMemo, TOpenDialog.
    Zależności systemowe: Win32 API (CopyFileW), funkcje standardowe C (fopen, fread, fseek, _mkdir).
    Struktury danych: Bezpośrednie mapowanie struktur binarnych z wyrównaniem do 1 bajtu (#pragma pack(push,1)) dla nagłówków plików i wpisów indeksu archiwum MIX.

4. Architektura i przepływ danych

    Wejście (Input): Plik .MIX wybrany przez użytkownika, struktura katalogów SPHERE na dysku.
    Przetwarzanie: Odczyt nagłówka MixHeader pobierającego liczbę spakowanych plików. Następnie następuje parsowanie tabeli alokacji plików (MixIndexEntry), obliczenie adresów bezwzględnych (base_offset) oraz sortowanie plików według rozmiaru w celu automatycznej kategoryzacji ich typów.
    Wyjście (Output): Pliki składowe poziomu wyekstrahowane do dynamicznie tworzonego folderu strukturalnego WORK\<Nazwa_Poziomu>\, logowanie operacji w komponencie tekstowym TMemo oraz aktualizacja stanów przycisków interfejsu (aktywacja/dezaktywacja opcji dekompresji i budowania struktur).

🇬🇧 English Version: Technical Summary
1. Purpose & Objective
This code implements a Graphical User Interface (GUI) tool using the VCL framework (C++Builder), designed to parse, extract, and manage .MIX archive files from a computer game. The project structure indicates a modding utility for games utilizing the RefPack compression method (common in legacy real-time strategy or action titles from the late 90s/early 00s). Its main objective is to automate the process of unpacking level assets (maps, object definitions, and textures) for alteration purposes.
2. Core Features

    Directory Structure Scanning (ScanSphereFolder): Automatically traverses application subdirectories (SPHERE1 to SPHERE3), detects layout folders, and visually maps the file hierarchy using a TTreeView component.
    File Validation and Whitelisting (Button1Click): Intercepts user input via a native file dialog, strictly enforcing a whitelist of supported asset filenames (e.g., L1_DC.MIX, L3_DH.MIX) before processing.
    Automated Backup Routine: Implements an automated safety measure by cloning the targeted .MIX file into a dedicated KOPY_MIX directory prior to any destructive operation.
    Archive Asset Identification (Heuristics & Sizing):
        The LooksLikeMap helper inspects the initial bytes of a data stream, analyzing numeric distributions to identify map files.
        Determines embedded file roles (MAP - terrain data, ODF - object definitions, TEX - textures) dynamically by analyzing and comparing the relative sizes of assets contained within 2-file or 3-file archives.
    Low-Level Extraction (extract_file): Seeks specific byte offsets inside the .MIX binary stream and writes raw unsegmented chunks out to standalone files.

3. Tech Stack & Dependencies

    Environment & Language: C++ (C++Builder / Embarcadero RAD Studio).
    GUI Framework: VCL (Visual Component Library) – utilizing TForm1, TTreeView, TMemo, and TOpenDialog components.
    System Dependencies: Win32 API (CopyFileW) paired with C standard library I/O utilities (fopen, fread, fseek, _mkdir).
    Data Layouts: Packed binary structures (#pragma pack(push,1)) to guarantee identical memory alignment when reading custom archive formats (MixHeader, MixIndexEntry).

4. Architecture & Data Flow

    Input: User-selected .MIX archive file, local disk directory structures (SPHERE folders).
    Processing: Reads the archive's MixHeader to determine the total file count. It then iterates over the allocation tables (MixIndexEntry), computes absolute pointers (base_offset), and runs a size-sorting algorithm to logically categorize asset types.
    Output: Individual level files extracted into a freshly created WORK\<Level_Name>\ directory layout, operation telemetry outputs pushed to a TMemo log screen, and status updates applied to interface controls (enabling extraction and preparing decompression routines).
