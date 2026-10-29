Hingeschludert ... ja. verzeihung. Die Umsetzung ist wichtiger als DEUTSCHkUrS. Entschuldigung *rylps*

ESPHome installieren (falls noch nicht geschehen):
pip3 install esphome

ESP32 per USB anschließen und flashen:
esphome run sensor_garten.yaml

Verify Formatting and Build Local Binaries:
	esphome compile sensor_garten.yaml
Flash onto the DollaTek Board over USB:
	esphome upload sensor_garten.yaml



Hier ist die vollständige, konsolidierte YAML-Konfiguration für deinen ESP32-Garten-Sensor. Sie enthält alle besprochenen Funktionen: den kapazitiven Touch-Sensor, die Akku-Spannungs- und Prozentmessung, das Taster-Kalibriersystem im Deep-Sleep, die Status-LED-Muster, die Text-Sensoren für das Dashboard sowie die Frostschutz-Logik über den DS18B20-Temperatursensor.

λ esphome compile sensor_garten.yaml
INFO ESPHome 2026.9.1
INFO Reading configuration sensor_garten.yaml...
Failed config

api: [source sensor_garten.yaml:104]

  The 'password' option has been removed in ESPHome 2026.1.0.
  Password authentication was deprecated in May 2022.
  Please migrate to encryption for secure API communication:

  api:
    encryption:
      key: !secret api_encryption_key

  Generate a key with: openssl rand -base64 32
  Or visit https://esphome.io/components/api/#configuration-variables.
  password: EinSicheresPasswort
  

You can easily generate a completely valid, unique 32-byte base64 key directly in your terminal using this Python command: 
 python -c "import base64, os; print(base64.b64encode(os.urandom(32)).decode())"


MAC
24:6F:28:D0:56:FC


_  IoT mosquitto_sub -v  -t "garten/feuchtigkeit/#"
garten/feuchtigkeit/debug [I][deep_sleep:058]: Sleeping for 900000000us
garten/feuchtigkeit/status offline
garten/feuchtigkeit/sensor/batterie_spannung/state 2.07
garten/feuchtigkeit/sensor/kalibrierwert_trocken__0__/state 80.000000
garten/feuchtigkeit/sensor/kalibrierwert_nass__100__/state 20.000000
^C
_  IoT tmmosquitto_sub -v -t "garten/feuchtigkeit/#" | awk '{ print strftime("%Y-%m-%d %H:%M:%S"), $0; fflush(); }' | tee -a garten-sensors.txt
2026-10-21 10:42:46 garten/feuchtigkeit/debug [I][deep_sleep:058]: Sleeping for 900000000us
2026-10-21 10:42:46 garten/feuchtigkeit/status offline
2026-10-21 10:42:46 garten/feuchtigkeit/sensor/batterie_spannung/state 2.07
2026-10-21 10:42:46 garten/feuchtigkeit/sensor/kalibrierwert_trocken__0__/state 80.000000
2026-10-21 10:42:46 garten/feuchtigkeit/sensor/kalibrierwert_nass__100__/state 20.000000

