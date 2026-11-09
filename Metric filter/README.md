Van lehetőségünk a metric filter használatával alarm beállítására, akár kulcsszóra, mint ERROR. 
Hozzárendelhetjük a korábban létrehozott SNC regisztrációnkat és email-es riasztást is beállíthatunk ha a szerverünk ERROR üzenetet kap.

Először a Log management -> metric filter állítunk be: 

<img width="1189" height="660" alt="Képernyőfotó 2026-10-19 - 16 37 17" src="https://github.com/user-attachments/assets/1bc9a348-5d25-44bf-ad5a-a95ea7662e34" />

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
