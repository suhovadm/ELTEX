*** Всякая полезная инфа по ELTEX-ам. ***  

// Как посмотреть какие IP-шники на каких VLAN-ах висят?  
show ip interface  

// Как посмотреть есть ли на Eltex 99 vlan.  
show vlan id 99, либо  
show vlan tag 99 на Eltex mes2324  

// Как создать 99-й влан на Eltex?  
conf t  
vlan 99  
name MGMT, или  
vlan 99 name MGMT на Eltex mes2324  
vlan active // на mes2324 это, скорее всего, вводить не нужно.  
exit  

// Как удалить 99-й VLAN на Eltex?  
conf t  
no vlan 99  
exit  

// Как посмотреть в каком режиме находится порт и какие VLAN-ы висят на порту?  
show running-config interface TengigabitEthernet 1/0/4, или 0/4  

// На Eltex VLAN на порт вешается вот так:  
configure  
interface tengigabitethernet 0/2  
switchport mode general  
switchport general allowed vlan add 99  

// Чтобы узнать мак-адрес шлюза - набираем:  
show ip arp  
Мак-адрес шлюза будет заканчиваться на .1, или на .254.  

// Чтобы узнать, откуда летит аплинк - пишем:  
show mac-address-table address [вставляем мак-адрес шлюза], нажимаем Enter  

// Чтобы посмотреть lldp-соседей в среде Eltex-ов:  
show lldp neighbors  

// Чтобы посмотреть прошивку и спеки Eltex-a:  
show system information  
show system  
show version  

// Как посмотреть, подключено ли что-то в порт?  
show interfaces description  

show interfaces [номер конкретного порта, например te 0/2]  

// Как посмотреть спеки портов - статус работы, скорость, дуплекс, тип медиа/трансивера?  
show interfaces status  
