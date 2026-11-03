# Bitki Bakım ve İzleme Robotu

İç mekanda çalışan iki tekerlekli robot. Saksıya gider, toprak nemini ölçer ve koşullar uygunsa kısa süre su verir. Telemetri ve hareket komutları ThingsBoard Cloud üzerinden gider.

Losant raporda karşılaştırmadır. İkinci bir platforma veri gönderilmez.

## İlk iş

1. ThingsBoard Avrupa hesabında `BitkiBakimRobotu` cihazını açın. Access token tek kişide kalsın.
2. ESP32, USB-UART portundan veri kablosuyla bağlanır. Anahtar kapalıyken kart yalnız USB’den beslenir.
3. İlk mesaj `v1/devices/me/telemetry` konusuna gider. Latest telemetry dolmadan panele geçilmez.

Örnek telemetri:

```json
{"soil_moisture": 42, "distance_cm": 18, "battery_voltage": 11.8, "robot_state": "idle", "pump_state": false}
```

İlk komutlar `move` ve `stop`. Engel, süre ve bağlantı kopması kontrolleri ESP32 içindedir. Bulut kesilince motor ve pompa yerelde kapanır.

## Pinler

| İş | Pin |
| --- | --- |
| Motor yön ve hız | GPIO14, GPIO21, GPIO41, GPIO42 |
| Mesafe sensörü I2C | GPIO38, GPIO39 |
| Nem | GPIO1 |
| Servo sinyali | GPIO40 |
| Pompa kapısı | GPIO47 |
| İleride IMU kesmesi | GPIO2, boş bırakın |

Kamera pinlerine başka iş verilmez. Derleyicide PSRAM açık olmalıdır.

## Güç

Paket 3S, 11,1 V. Motor sürücüsü bu hattan beslenir. ESP32 yalnız sabit 5 V regülatörden, servo ve pompa 6,0 V’a ayarlı ayrı regülatörden beslenir. Eksi uçlar ortaktır. Sürücü kartının 5 V çıkışı ESP32’ye bağlanmaz.

## Depoya konmayacaklar

Access token, Wi-Fi parolası ve `.env` dosyaları bu depoya girmez.
