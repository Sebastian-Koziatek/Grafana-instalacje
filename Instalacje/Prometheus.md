Instalacja i konfiguracja Prometheusa

1. Pobierz najnowszą wersję Prometheusa z oficjalnej strony:
   ```bash
   wget https://github.com/prometheus/prometheus/releases/download/v2.47.0/prometheus-2.47.0.linux-amd64.tar.gz
   ```
2. Rozpakuj plik:
   ```bash
   tar xvf prometheus-2.47.0.linux-amd64.tar.gz
   cd prometheus-2.47.0.linux-amd64
   ```
3. Skopiuj pliki binarne do katalogu systemowego:
   ```bash
   sudo mv prometheus /usr/local/bin/
   sudo mv promtool /usr/local/bin/
   ```
4. Utwórz katalogi na dane i konfigurację:
   ```bash
   sudo mkdir /etc/prometheus /var/lib/prometheus
   sudo mv prometheus.yml /etc/prometheus/
   ```
5. Uruchom Prometheusa:
   ```bash
   prometheus --config.file=/etc/prometheus/prometheus.yml
   ```

### Przykładowa konfiguracja `prometheus.yml`
```yaml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['localhost:9100']
```

- **scrape_interval:** Określa częstotliwość zbierania danych.
- **job_name:** Unikalna nazwa zadania zbierania danych.
- **targets:** Lista endpointów do monitorowania (w tym przypadku Node Exporter).

Dokumentacja Prometheusa: https://prometheus.io/docs/introduction/overview/
