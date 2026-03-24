### Pomoc WSL
```shell
wsl --help
```

### Sprawdzenie statusu WSL
```shell
wsl --status
```

### Sprawdzenie wersji WSL
```shell
wsl --version
```

### Aktualizacja WSL
```shell
wsl --update
```

### Wyświetlenie listy zainstalowanych dystrybucji
*(Domyślna wersja dystrybucji jest jawnie podana w nawiasie.)*
```shell
wsl -l
wsl --list
```

### Wyświetlenie listy dystrybucji Linuksa dostępnych w sklepie online
```shell
wsl -l -o
wsl --list --online
```

### Wyświetlenie zainstalowanych dystrybucji wraz z ich statusem działania oraz informacją, czy konfiguracja WSL to 1 czy 2
*(Domyślna dystrybucja jest oznaczona prefiksem `*` przed nazwą.)*
```shell
wsl -l --verbose
wsl -l -v
```

### Ustawienie domyślnej wersji WSL
```shell
wsl --set-default-version <Wersja>
```

### Uruchomienie konkretnej dystrybucji
```shell
wsl -d nazwa_dystrybucji
wsl --distribution nazwa_dystrybucji
```

### Zatrzymanie / wyłączenie konkretnej dystrybucji
```shell
wsl -t nazwa_dystrybucji_do_wylaczenia
wsl --terminate nazwa_dystrybucji_do_wylaczenia
```

### Wyłączenie wszystkich dystrybucji
```shell
wsl --shutdown
```

### Ustawienie konkretnej dystrybucji jako domyślnej
```shell
wsl -s moja_domyslna_dystrybucja
wsl --set-default moja_domyslna_dystrybucja
```

### Eksport uruchomionej dystrybucji do obrazu
*(Domyślnie eksport odbywa się do formatu tar.)*
```shell
wsl --export nazwa_dystrybucji_do_eksportu sciezka_windows\nazwa_pliku.tar
```

### Eksport uruchomionej dystrybucji do obrazu w formacie VHD
*(Obsługiwane tylko w WSL 2.)*
```shell
wsl --export nazwa_dystrybucji_do_eksportu --vhd sciezka_windows\nazwa_pliku.vhd
```

### Import obrazu jako dystrybucji
```shell
wsl --import nowa_nazwa_dystrybucji lokalizacja_instalacji_w_windows plik.tar --version wersja-wsl-1-lub-2
wsl --import Ubuntu-20 D:\VMs\WSL\Ubuntu-20\ Ubuntu-20.04.tar --version 2
wsl --import Ubuntu-20 --vhd D:\VMs\WSL\Ubuntu-20\ Ubuntu-20.04.vhd --version 2
```

### Wyrejestrowanie dystrybucji
*(Usuwa również jej pliki z dysku.)*
```shell
wsl --unregister nazwa_dystrybucji_do_usuniecia
```

### Uruchomienie dystrybucji WSL jako wskazany użytkownik
```shell
wsl -u nazwa_uzytkownika -d nazwa_dystrybucji
wsl -u root -d Ubuntu-20.04
```

### Zmiana domyślnego użytkownika dla dystrybucji
```shell
NazwaDystrybucji config --default-user NazwaUzytkownika
ubuntu config --default-user moja_domyslna_nazwa_uzytkownika
ubuntu2004.exe config --default-user johndoe
```

### Identyfikacja adresu IP dystrybucji Linuksa zainstalowanej przez WSL 2
*(Adres maszyny wirtualnej WSL 2.)*
```shell
wsl hostname -I
```

### Identyfikacja adresu IP komputera z Windows widzianego z poziomu WSL 2
```shell
ip route show | grep -i default | awk '{ print $3 }'
```

### Ręczne zmniejszenie zajętości dysku WSL
*Rozmiar dysku WSL zwiększa się automatycznie, ale nie zmniejsza się automatycznie. Aby go zmniejszyć, najpierw trzeba zamknąć dystrybucję, jak poniżej.*

*Otwórz Windows Terminal w trybie administratora:*
```shell
cd D:\VM\WSL\Ubuntu
wsl -l -v
wsl --shutdown nazwa-twojej-dystrybucji
Optimize-VHD -Path .\ext4.vhdx -Mode full
```

*Jeśli pominiesz nazwę dystrybucji, zostaną wyłączone wszystkie dystrybucje. Jeżeli działa Docker Desktop, on również zostanie wyłączony.*

### Lista przestarzałych poleceń WSL
*Te polecenia były oryginalną składnią do konfiguracji dystrybucji Linuksa zainstalowanych w WSL, ale zostały zastąpione przez składnię `wsl` lub `wsl.exe`.*
```shell
wslconfig.exe [Argument] [Opcje]
bash [Opcje]
lxrun /[Argument]
```
