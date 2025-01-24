##### Dodanie repozytoriów i instalacja
```bash
#Dodanie repozytorium
sudo apt-get install -y apt-transport-https software-properties-common wget
sudo mkdir -p /etc/apt/keyrings/
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

#Aktualizacja repozytoriów
sudo apt-get update

# Instalacja grafany
sudo apt-get install grafana
```

##### Start usługi grafany i dodanie do autostartu

```bash
sudo systemctl start grafana-server 
sudo systemctl enable grafana-server
```

##### Połaczenie z grafaną

Otwórz przeglądarkę i przejdź pod adres:

```
http://<IP-Serwera>:3000
```

Domyślny port Grafany to **3000**.  
2. Zaloguj się, używając domyślnych danych uwierzytelniających:

- **Login**: `admin`
- **Hasło**: `admin`  
    Po pierwszym logowaniu zostaniesz poproszony o zmianę hasła.

##### Plik konfiguracyjny grafany
```bash
sudo nano /etc/grafana/grafana.ini
```