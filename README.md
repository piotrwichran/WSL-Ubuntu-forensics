**Languages / Wersje językowe:** [Polski](#polski) | [English](#english)
---

## Polski

# Instalacja, konfiguracja i przygotowanie WSL (Ubuntu) do pracy z narzędziami forensics

Krok-po-kroku lista czynności dla Windows 10 (build 19041+) lub Windows 11. Wszystkie polecenia w **PowerShell** lub **Terminal Windows** uruchamiane jako **Administrator**.

### 1. Instalacja WSL 2 i Ubuntu

1. Otwórz PowerShell jako Administrator.
2. Włącz WSL i platformę maszyn wirtualnych: wsl --install
    - Automatycznie włączy potrzebne funkcje, zainstaluje WSL 2 i domyślną dystrybucję **Ubuntu** (najnowszą LTS).
    - Jeśli polecenie nie działa (starszy Windows), ręcznie: dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestartdism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
		- Restart komputera.
		- Po restarcie system pobierze i zainstaluje Ubuntu z Microsoft Store automatycznie.
5. Po pierwszym uruchomieniu Ubuntu (wpisz wsl lub ubuntu w terminalu):
    - Utwórz nazwę użytkownika Linux (np. forensics lub student).
    - Ustaw hasło UNIX (nie będzie widoczne podczas wpisywania).

### 2. Podstawowa konfiguracja WSL

1. Sprawdź wersję i status: wsl --list --verbose Powinieneś zobaczyć Ubuntu z VERSION 2.
2. Ustaw WSL 2 jako domyślny (jeśli nie jest): wsl --set-default-version 2
3. Ustaw Ubuntu jako domyślną dystrybucję: wsl --set-default Ubuntu
4. Aktualizuj system Ubuntu: W terminalu WSL (już jako użytkownik Linux): sudo apt update && sudo apt upgrade -y
5. Zainstaluj podstawowe narzędzia: sudo apt install -y git curl wget nano net-tools

### 3. Przydatna konfiguracja dodatkowa

1. Dostęp do plików Windows z Linuxa: Pliki z dysku C: są w /mnt/c/ (np. /mnt/c/Users/TwojeImie/Documents).
2. Dostęp do plików Linuxa z Windows: W Eksploratorze wpisz \\wsl$\Ubuntu\home\twoja_nazwa_uzytkownika
3. Integracja z VS Code (opcjonalnie, ale bardzo przydatna):
    - Zainstaluj rozszerzenie „Remote – WSL” w VS Code.
    - Otwórz folder w WSL jednym kliknięciem.
4. Automatyczne montowanie dysków (np. pendrive): Edytuj /etc/wsl.conf (sudo nano):
```
[automount]
enabled = true
options = "metadata,umask=22,fmask=11"
```
Potem wsl --shutdown w PowerShell i uruchom ponownie.

### 4. Instalacja popularnych programów forensics w Ubuntu

W terminalu WSL (Ubuntu) wykonaj:

1. Aktualizacja repozytoriów: sudo apt update
2. Podstawowe narzędzia do imagingu i analizy dysków: sudo apt install -y sleuthkit autopsy guymager foremost scalpel testdisk dc3dd dcfldd
3. Analiza pamięci i inne: sudo apt install -y volatility wireshark tshark exiftool binwalk bulk-extractor
4. Volatility 3 (nowsza wersja): sudo apt install -y python3-pippip3 install volatility3
5. Plaso (timeline): sudo apt install -y plaso-tools
6. Dodatkowe przydatne: sudo apt install -y extundelete rekall

### 5. Szybki test instalacji

- fls – powinno działać (Sleuth Kit).
- vol – Volatility 3.
- autopsy – uruchomi GUI Autopsy (jeśli masz X-server lub WSLg w Windows 11).

---

## English

# Installation, configuration and preparation of WSL (Ubuntu) for forensics tools
Step-by-step instructions for Windows 10 (build 19041+) or Windows 11. All commands in PowerShell or Windows Terminal run as Administrator.

### 1. Installing WSL 2 and Ubuntu

1. Open PowerShell as Administrator.
2. Enable WSL and virtual machine platform:  wsl --install 
	- Automatically enables required features, installs WSL 2 and default Ubuntu distribution (latest LTS).
	- If the command doesn’t work (older Windows), manually:  dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart 
		- Restart your computer.
		- After restart, the system will download and install Ubuntu from Microsoft Store automatically.
5. After first Ubuntu launch (type  wsl  or  ubuntu  in terminal):
	- Create Linux username (e.g.  forensics  or  student ).
	- Set UNIX password (it won’t be visible while typing).
	
### 2. Basic WSL configuration

1. Check version and status:  wsl --list --verbose  You should see Ubuntu with VERSION 2.
2. Set WSL 2 as default (if not already):  wsl --set-default-version 2 
3. Set Ubuntu as default distribution:  wsl --set-default Ubuntu 
4. Update Ubuntu system: In WSL terminal (as Linux user):  sudo apt update && sudo apt upgrade -y 
5. Install basic tools:  sudo apt install -y git curl wget nano net-tools 
	
### 3. Useful additional configuration

1. Access Windows files from Linux: Files from C: drive are in  /mnt/c/  (e.g.  /mnt/c/Users/YourName/Documents ).
2. Access Linux files from Windows: In Explorer, type  \\wsl$\Ubuntu\home\your_username 
3. VS Code integration (optional but very useful):
	- Install “Remote – WSL” extension in VS Code.
	- Open folder in WSL with one click.
4. Automatic disk mounting (e.g. USB): Edit  /etc/wsl.conf  (sudo nano):
    ```
    [automount]
    enabled = true
    options = "metadata,umask=22,fmask=11"
    ```
    Then  wsl --shutdown  in PowerShell and restart.
	
### 4. Installing popular forensics programs in Ubuntu

In WSL (Ubuntu) terminal, run:

1. Update repositories:  sudo apt update 
2. Basic imaging and disk analysis tools:  sudo apt install -y sleuthkit autopsy guymager foremost scalpel testdisk dc3dd dcfldd 
3. Memory analysis and others:  sudo apt install -y volatility wireshark tshark exiftool binwalk bulk-extractor 
4. Volatility 3 (newer version):  sudo apt install -y python3-pip   pip3 install volatility3 
5. Plaso (timeline):  sudo apt install -y plaso-tools 
6. Additional useful:  sudo apt install -y extundelete rekall 
	
### 5. Quick installation test

- fls  – should work (Sleuth Kit).
- vol  – Volatility 3.
- autopsy  – launches Autopsy GUI (if you have X-server or WSLg on Windows 11).
