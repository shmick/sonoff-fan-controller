# Parts
* Sonoff SV Board
* DS1820B Sensor - Waterproof type with stainless steel end.
* 6 Pin waterproof / watertight locking connector

# Software
The Sonoff SV is flashed with [Tasmota](https://tasmota.github.io/docs/) to allow reading the DS1820B and controlling the relay

# Configuration
| Tasmota Command | Description |
| --- | --- |
| `hostname fancontrol` | set hostname to fancontrol |
| `FriendlyName fancontrol` | set hostname to fancontrol |
| `DeviceName fancontrol` | set hostname to fancontrol |
| `SetOption3 0` | disable mqtt cuts down on error messages |
| `module 3` | set the module type to a Sonoff SV |
| `gpio14 4` | set gpio14 to DS18B20 sensor |
| `SetOption74 1` | use internal pullup for single DS18B20 sensor |
| `mem1 100`| relay on on at 100C |
| `mem2 95` | relay off at 95C |
| `Rule1 ON DS18B20#Temperature>%mem1% DO Power on ENDON ON DS18B20#Temperature<%mem2% DO Power off ENDON` | Rule to set power on/off |
| `Rule1 5` | Set rule1 to be one-shot detection |
| `Rule1 1` | Enable rule1 to start controlling the relay |

Configure everything at once
```
backlog hostname fancontrol ; friendlyname fancontrol ; devicename fancontrol ; module 3 ; gpio14 4 ; SetOption3 0 ; SetOption74 1 ; mem1 100 ; mem2 95 ; Rule1 ON DS18B20#Temperature>%mem1% DO Power on ENDON ON DS18B20#Temperature<%mem2% DO Power off ENDON ; rule1 5 ; rule1 1
```

# Operation
The Sonoff SV is powered from the motorcycle battery. When the relay is activated, the +12v signal is passed through to the Sonoff Relay + output, driving the relay for the radiator fan.
