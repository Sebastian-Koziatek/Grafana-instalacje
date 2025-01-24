
##### Dodanie klucza GPG i repozytorium InfluxData

```bash

wget -qO- https://repos.influxdata.com/influxdb.key | sudo gpg --dearmor -o /usr/share/keyrings/influxdata-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/influxdata-archive-keyring.gpg] https://repos.influxdata.com/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdata.list

```
##### Krok 2: Aktualizacja listy pakietów

Zaktualizuj listę pakietów systemowych:
```bash
sudo apt update
```

Zainstaluj Telegraf za pomocą menedżera pakietów `apt`:

```bash
sudo apt install -y telegraf
```
## Krok 4: Konfiguracja Telegraf

  Plik konfiguracyjny Telegraf znajduje się w:
```bash
/etc/telegraf/telegraf.conf
```

Możesz wygenerować domyślny plik konfiguracyjny za pomocą polecenia:

```bash
telegraf config > /etc/telegraf/telegraf.conf
```  

Uruchom i włącz usługę Telegraf, aby startowała automatycznie przy uruchomieniu systemu:

  

```bash
sudo systemctl start telegraf
sudo systemctl enable telegraf
```

Sprawdź status usługi, aby upewnić się, że działa poprawnie:

```bash
sudo systemctl status telegraf
```

##### Przykładowy plik konfiguracyjny
```config
# Globalna konfiguracja Telegrafa

**[global_tags]**

  # Możesz dodać tutaj globalne tagi (np. host = "nazwa_hosta")

  

**[agent]**

  interval = "10s"                # Interwał zbierania danych
  round_interval = true
  metric_batch_size = 1000
  metric_buffer_limit = 10000
  collection_jitter = "0s"
  flush_interval = "10s"
  flush_jitter = "0s"
  precision = ""
  hostname = ""
  omit_hostname = false

  

# Wyjście danych: InfluxDB v2

[[outputs.influxdb_v2]]

  urls = ["http://localhost:8086"] # Adres InfluxDB
  token = "<tokenID>"
  organization = "grafana"
  bucket = "grafana"

  

# Zbieranie danych: CPU

[[inputs.cpu]]
  percpu = true
  totalcpu = true
  collect_cpu_time = false
  report_active = true


# Zbieranie danych: pamięć RAM
[[inputs.mem]]

# Zbieranie danych: dyski
[[inputs.disk]]

  ignore_fs = ["tmpfs", "devtmpfs"]


# Zbieranie danych: system
[[inputs.system]]


# Zbieranie danych: procesy
[[inputs.processes]]


# Zbieranie danych: sieć
[[inputs.net]]

  interfaces = ["ens18"] # Zmień na nazwę swojej karty sieciowej, jeśli inna niż "eth0"
```



Tutaj jest dokumentacja dotycząca telegrafa - https://docs.influxdata.com/telegraf/v1/
