Grafana może korzystać z InfluxDB jako źródła danych do tworzenia wizualizacji w czasie rzeczywistym lub analizy historycznej. Integracja pozwala na monitorowanie metryk zebranych np. przez **Telegraf**, który przesyła dane do InfluxDB.

## Instalacja i konfiguracja InfluxDB

### Instalacja InfluxDB (na przykładzie Ubuntu 24.04)

1. Zainstaluj InfluxDB za pomocą `apt`:
   ```bash
   sudo apt update
   sudo apt install influxdb
   ```

2. Uruchom i skonfiguruj usługę:
   ```bash
   sudo systemctl start influxdb
   sudo systemctl enable influxdb
   ```

Adres URL
```
http://localhost:8086
```

