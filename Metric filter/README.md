Van lehetőségünk a metric filter használatával alarm beállítására, akár kulcsszóra, mint ERROR. 
Hozzárendelhetjük a korábban létrehozott SNC regisztrációnkat és email-es riasztást is beállíthatunk ha a szerverünk ERROR üzenetet kap.

Először a Log management -> metric filter állítunk be: 


<img width="1204" height="404" alt="Képernyőfotó 2026-11-09 - 14 29 08" src="https://github.com/user-attachments/assets/6124d839-3e1f-4388-ad3a-59f52a00951e" />

<img width="1187" height="667" alt="Képernyőfotó 2026-11-09 - 14 29 52" src="https://github.com/user-attachments/assets/1f2d33ff-4606-49de-97ec-22ebfb729604" />

Meghatározzuk, milyen filter pattern szeretnénk. Jelen esetben nekünk az ERROR-ra van szükségünk. 

<img width="1199" height="636" alt="Képernyőfotó 2026-11-09 - 14 30 37" src="https://github.com/user-attachments/assets/82e13e79-00a0-4351-afec-4ff9ef3563e6" />

Elnevezzük és konfiguráljuk az filterünket és létrehozzuk a Create Filter gombbal.

<img width="1180" height="661" alt="Képernyőfotó 2026-11-09 - 14 31 45" src="https://github.com/user-attachments/assets/cab5bbcb-8f15-41b4-b331-c9d5b3c82fbb" />
<img width="862" height="340" alt="Képernyőfotó 2026-11-09 - 14 31 58" src="https://github.com/user-attachments/assets/4ea56325-fc2e-4f3e-9c3b-3d7f3f6ee0fd" />


Ezután, hogy megjelenjen nekünk a metrika, először csatlakozni kell az EC2-hez és egy hiba üzenetet generálni. Ehhez használhatjuk az alábbi segédletet: 

```bash
logger "CloudMentor: ERROR teszt uzenet"
```

Ezután a létrehozott metric filterre a Cloudwatchban beállítunk egy Alarm-ot. Az elküldött hibaüzenettel azonnal megjelenik a metrikák között az előzőleg generált error-count-vms elnevezésű:

<img width="655" height="672" alt="Képernyőfotó 2026-11-09 - 14 37 00" src="https://github.com/user-attachments/assets/3b2e963a-5475-4c82-8430-c13aa1a25e1a" />

Ezt fogjuk kiválasztani és konfigurálni a riasztásunkat. 

<img width="1328" height="729" alt="Képernyőfotó 2026-11-09 - 14 37 13" src="https://github.com/user-attachments/assets/d2c61cc3-6b7b-4aa6-a0a9-7133cad9fd12" />

A beállításokkor azt adjuk meg, hogy minimum 5 hibaüzenetnek kell érkeznie 5 percen belül, hogy riasztást küldjön nekünk a Cloudwatch. 

<img width="1139" height="665" alt="Képernyőfotó 2026-11-09 - 14 38 29" src="https://github.com/user-attachments/assets/4660f44c-453d-4f4e-a76c-5cf4add888ce" />

A kiegészítő beállításnál kiválasztott not breaching lehetőséggel azt fogadjuk el, hogy ha nincs meg az 5 hibaüzenet akkor minden rendben van. 

<img width="369" height="471" alt="Képernyőfotó 2026-11-09 - 14 38 35" src="https://github.com/user-attachments/assets/c1a4c0c2-a466-4625-aef8-181fb6a5b15d" />



<img width="1450" height="712" alt="Képernyőfotó 2026-10-19 - 16 42 53" src="https://github.com/user-attachments/assets/20bd180a-c76e-43a5-9e47-777102932861" />

Beállítjuk, mind az ALARM, mind az OK esetén az email értesítést. Ez azt fogja jelenteni, hogy ha 5 perc alatt 5db ERROR üzenet érkezik riasztást küld és emailben is jelez. Ha letelik az 5 perc és nincs 5db ERROR üzenet OK állapotba kerül vissza és jelezni fogja a rendszer nekünk, hogy minden rendben.


Teszteljük a riasztást és ERROR üzenetet küldünk a szervernek. Ha mindent jól csináltunk akkor riasztást fog jelezni a Cloudwatch-ban és email-ben is kapunk üzenetet.

<img width="661" height="688" alt="Képernyőfotó 2026-11-09 - 14 40 11" src="https://github.com/user-attachments/assets/7a81a100-852d-4a60-b5a5-8a49f3228914" />

Ahogy látjuk a sok ERROR üzenet hatására átlépte a beállított határértéket:

<img width="1194" height="661" alt="Képernyőfotó 2026-11-09 - 14 42 09" src="https://github.com/user-attachments/assets/8ec0379a-a8a2-40dd-9ea2-d723ea009fdc" />

Email riasztás megérkezett a regisztrált SNC email címre

<img width="749" height="713" alt="Képernyőfotó 2026-11-09 - 14 44 01" src="https://github.com/user-attachments/assets/d18c4fc4-e2b9-4818-ab2e-d3da4f6b50af" />

Miután nem érkezett több ERROR üzenet a szerverre visszaállt az alap OK beállításra, és email üzenetet is küldött:

<img width="1185" height="635" alt="Képernyőfotó 2026-11-09 - 15 04 05" src="https://github.com/user-attachments/assets/1297e140-4438-4dd0-afef-0189c3c484eb" />

<img width="757" height="745" alt="Képernyőfotó 2026-11-09 - 15 04 17" src="https://github.com/user-attachments/assets/da916d5a-9540-4eb7-93d0-f365eff5838b" />
