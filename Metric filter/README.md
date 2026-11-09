Van lehetőségünk a metric filter használatával alarm beállítására, akár kulcsszóra, mint ERROR. 
Hozzárendelhetjük a korábban létrehozott SNC regisztrációnkat és email-es riasztást is beállíthatunk ha a szerverünk ERROR üzenetet kap.

Először a Log management -> metric filter állítunk be: 


<img width="1204" height="404" alt="Képernyőfotó 2026-11-09 - 14 29 08" src="https://github.com/user-attachments/assets/6124d839-3e1f-4388-ad3a-59f52a00951e" />

<img width="1187" height="667" alt="Képernyőfotó 2026-11-09 - 14 29 52" src="https://github.com/user-attachments/assets/1f2d33ff-4606-49de-97ec-22ebfb729604" />

Meghatározzuk, milyen filter pattern szeretnénk. Jelen esetben nekünk az ERROR-ra van szükségünk. 

<img width="1199" height="636" alt="Képernyőfotó 2026-11-09 - 14 30 37" src="https://github.com/user-attachments/assets/82e13e79-00a0-4351-afec-4ff9ef3563e6" />

Elnevezzük és konfiguráljuk az filterünket: 

<img width="1180" height="661" alt="Képernyőfotó 2026-11-09 - 14 31 45" src="https://github.com/user-attachments/assets/cab5bbcb-8f15-41b4-b331-c9d5b3c82fbb" />


A Cloudwatchban beállítunk egy Alarm-ot, az előbb létrehozott filterre: 

<img width="1442" height="668" alt="Képernyőfotó 2026-10-19 - 16 42 13" src="https://github.com/user-attachments/assets/01a668b6-86fe-4e40-b35e-b639ce15a3da" />


<img width="1450" height="712" alt="Képernyőfotó 2026-10-19 - 16 42 53" src="https://github.com/user-attachments/assets/20bd180a-c76e-43a5-9e47-777102932861" />

Beállítjuk, mind az ALARM, mind az OK esetén az email értesítést.

<img width="1208" height="445" alt="Képernyőfotó 2026-10-19 - 16 43 35" src="https://github.com/user-attachments/assets/5d635fa6-bd11-4031-a925-cee04e5ec9d1" />

Teszteljük a riasztást és ERROR üzenetet küldünk a szervernek. Ha mindent jól csináltunk akkor riasztást fog jelezni a Cloudwatch-ban és email-ben is kapunk üzenetet.

<img width="864" height="336" alt="Képernyőfotó 2026-10-19 - 16 44 35" src="https://github.com/user-attachments/assets/18d6b951-a492-4e3e-b3ac-c12b4789a4ba" />

Email riasztás megérkezett a regisztrált SNC email címre

<img width="716" height="690" alt="Képernyőfotó 2026-10-19 - 16 47 08" src="https://github.com/user-attachments/assets/335b4d47-826f-4a76-bcc6-8296f16e9c08" />

Tesztünket a minden rendben üzenettel zárjuk, amire riasztást nem kapunk mivel nem tartalmazza az ERROR szót.

<img width="799" height="396" alt="Képernyőfotó 2026-10-19 - 16 50 25" src="https://github.com/user-attachments/assets/d905902f-497e-4272-8125-8a7d8898340f" />
