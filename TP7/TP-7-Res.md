# TP7 INFRA : 3-tier architecture et redondance

## 1. Présentation archi

### A. Topologie réseau

![shéma de la topologie](/TP7/topologie-tp7.png)

### B. Tableau d'adressage et C. Tableau des VLANs

## 2. Technos utilisées

**🌞 show-run sur tous les équipements**

- [routeur_1](/TP7/routeur1.md)
- [routeur_2](/TP7/routeur2.md)
- [switch_1](/TP7/swt1.md)
- [switch_2](/TP7/swt2.md)
- [switch_3](/TP7/swt3.md)
- [switch_4](/TP7/swt4.md)
- [switch_5](/TP7/swt5.md)
- [switch_6](/TP7/swt6.md)
- [switch_7](/TP7/swt7.md)

**🌞 depuis pc4.tp7.b1**

```shell
PC1> ping 10.7.30.11 #note mon PC1 = PC4 de la topologie donnée

84 bytes from 10.7.30.11 icmp_seq=1 ttl=63 time=15.601 ms
84 bytes from 10.7.30.11 icmp_seq=2 ttl=63 time=14.640 ms
84 bytes from 10.7.30.11 icmp_seq=3 ttl=63 time=23.058 ms
84 bytes from 10.7.30.11 icmp_seq=4 ttl=63 time=23.718 ms
84 bytes from 10.7.30.11 icmp_seq=5 ttl=63 time=19.830 ms

PC1> ping ynov.com
ynov.com resolved to 104.26.10.233

84 bytes from 104.26.10.233 icmp_seq=1 ttl=59 time=30.735 ms
84 bytes from 104.26.10.233 icmp_seq=2 ttl=59 time=30.994 ms
84 bytes from 104.26.10.233 icmp_seq=3 ttl=59 time=31.433 ms
84 bytes from 104.26.10.233 icmp_seq=4 ttl=59 time=30.752 ms
84 bytes from 104.26.10.233 icmp_seq=5 ttl=59 time=30.986 ms
```

## 3. Bonus

### A. ACL

**🌞 Le réseau 10.7.30.0/24...**

