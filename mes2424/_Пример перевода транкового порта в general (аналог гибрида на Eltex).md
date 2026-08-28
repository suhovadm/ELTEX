// Пример перевода транкового порта в general (это аналог гибрида на Eltex).  

___ [Был такой конфиг на порту] ___  
interface tengigabitethernet 0/2  
  switchport mode trunk  
  switchport trunk native vlan 1850  
  no lldp transmit // запрещает отправку LLDP-пакетов с интерфейса.  
  no lldp receive // запрещает приём LLDP-пакетов на интерфейсе. Таким образом, интерфейс не отправляет и не принимает LLDP-информацию.  

___ [Стал такой конфиг на порту] ___  
interface tengigabitethernet 0/2  
  switchport general allowed vlan add 1850 untagged  
  switchport general pvid 1850  
  no lldp transmit  
  no lldp receive  

// Какими командами этого добиться на Eltex mes2424 rev B. версия прошивки 10.2.7.2 ?  
conf t  
interface tengigabitethernet 0/2  
switchport mode general  
switchport general allowed vlan add 1850 untagged <--- здесь нужно писать и add и untagged!  
switchport general pvid 1850 // pvid 1850 вводится после untagged-a,  
// либо же, после untagged-a, также, можно шарахнуть switchport general allowed vlan 1850 <--- здесь НЕ нужно ни add, ни tagged!  
// и эффект будет тот же самый.  
no lldp transmit  
no lldp receive  

copy running-config startup-config  

_______________________________________________________________________________________________________________________________________  

// Чем отличается trunk от hybrida?  
// Главное отличие: hybrid гибче - на одном порту можно иметь одни VLAN tagged, другие untagged.  
// Trunk: VLAN 10, 20, 30 - tagged и только tagged.  
// Hybrid: VLAN 10 - untagged, а VLAN 20 и 30 - tagged.  

_______________________________________________________________________________________________________________________________________  
