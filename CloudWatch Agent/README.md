CloudWatch agentet telepítünk az EC2 példányunkra, hogy a log fájlokat tudjuk naplózni és teszteljük a működését.

Első lépésként az EC2 példánynak hozzá kell rendelni az IAM role-hoz a `CloudWatchAgentServerPolicy`

<img width="1146" height="222" alt="Képernyőfotó 2026-10-23 - 11 00 55" src="https://github.com/user-attachments/assets/117cee7f-f1f3-4124-81f4-a75b6f82baf8" />

Security fülnél már csak beállítottam a szerverre:

<img width="1449" height="345" alt="Képernyőfotó 2026-10-19 - 14 44 17" src="https://github.com/user-attachments/assets/5efd37cc-1b7e-4999-8d2f-20fa56b9c7eb" />

Ezután csatlakozunk a szerverünkhöz és telepítjük az agent-t. Amazon Linux 2023-on a `/var/log/messages` fájl nem mindig jön létre automatikusan. Először telepíteni kell az `rsyslog` szolgáltatást, ami létrehozza és írja ezt a logfájlt. 

```bash
sudo dnf install -y rsyslog amazon-cloudwatch-agent
sudo systemctl enable --now rsyslog
sudo systemctl status rsyslog
```
<img width="1463" height="716" alt="Képernyőfotó 2026-10-19 - 14 47 00" src="https://github.com/user-attachments/assets/79d8e06e-0820-4b56-88e0-d1369f627956" />

Ezután konfiguráljuk az agent-t a `/var/log/messages` fájlra, log group `/ec2/messages` -re. Ezt egy konfigurációs fájlt kell létrehoznunk json formátumban.

A következő parancsokat tudjuk beírni a konfigurációs fájl betápláláshoz:
```bash
sudo mkdir -p /opt/aws/amazon-cloudwatch-agent/etc
sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```
A megnyílt szerkesztőbe tudjuk a json fájlunkat bemásolni:
```bash

{
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/var/log/messages",
            "log_group_name": "/ec2/messages",
            "log_stream_name": "i-0aa94f1d833439c02",
            "timezone": "Local"
          }
        ]
      }
    }
  }
}
```
<img width="1252" height="319" alt="Képernyőfotó 2026-10-19 - 15 51 26" src="https://github.com/user-attachments/assets/ceb6c6d5-6245-48e9-b788-7172e6cf9ba2" />

Itt a file path lesz a beállított log fájlok. A log group name az Ec2/message elnevezést kapja. A stream neve az EC2 ID-ja. 

Ezután már készen áll az agent az indításra:
```bash
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl \
  -a fetch-config \
  -m ec2 \
  -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json \
  -s
```

Létrejött log group a CLoudWatchban:
<img width="1194" height="245" alt="Képernyőfotó 2026-10-19 - 15 51 14" src="https://github.com/user-attachments/assets/57cd97ed-c93e-4e2d-a456-1067902043c6" />

Hogy teszteljük az agent-t küldünk egy mentoring ERROR teszt üzenetet és megnézzük megjelenik-e a log gorupban.

<img width="411" height="62" alt="Képernyőfotó 2026-10-19 - 15 55 03" src="https://github.com/user-attachments/assets/aba82ab2-9e9f-48c7-a5b3-46590cb5f0ee" />

Látszik a küldött üzenet, hogy naplózásra került:
<img width="1163" height="94" alt="Képernyőfotó 2026-10-19 - 15 55 24" src="https://github.com/user-attachments/assets/651a6e61-1ec5-4010-9403-6be5451bccbd" />

A logunkat ellenőrizni is tudjuk a Log insight-ban. Itt lehetőség van szűrőket beállítani a keresésre pl. ERROR üznetünket akarjuk megtalálni, hogy ne kelljen keresgetni a több 1000log között. 

<img width="1451" height="507" alt="Képernyőfotó 2026-10-19 - 16 09 36" src="https://github.com/user-attachments/assets/69bdc32b-f452-4ed2-b3fb-a72a43be5638" />



