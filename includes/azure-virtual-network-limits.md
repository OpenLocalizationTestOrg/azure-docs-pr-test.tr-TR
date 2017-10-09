<a name="virtual-networking-limits-classic"></a>Merhaba aşağıdaki sınırları yalnızca ağ abonelik başına hello Klasik dağıtım modeli üzerinden yönetilen kaynakları için geçerlidir.

| Kaynak | Varsayılan limit | Üst sınır |
| --- | --- | --- |
| Sanal ağlar |50 |100 |
| Yerel ağ siteleri |20 |desteğe başvurun |
| Sanal ağ başına DNS sunucusu sayısı |20 |100 |
| Sanal ağ başına özel IP Adresi sayısı |4096 |4096 |
| Bir sanal makine veya rol örneği NIC eşzamanlı TCP veya UDP akışlar |500K |500K |
| Ağ Güvenlik Grupları (NSG) |100 |200 |
| NSG başına NSG kuralları |200 |400 |
| Kullanıcı tanımlı yol tabloları |100 |200 |
| Yol tablosu başına kullanıcı tanımlı yol sayısı |100 |400 |
| Genel IP adresleri (dinamik) |5 |desteğe başvurun |
| Ayrılmış genel IP adresleri |20 |desteğe başvurun |
| Dağıtım başına genel VIP |5 |desteğe başvurun |
| Dağıtım başına özel VIP (ILB) |1 |1 |
| Uç Nokta Erişim Denetim Listeleri (ACL’ler) |50 |50 |

#### <a name="azure-resource-manager-virtual-networking-limits"></a>Ağ Limitleri - Azure Resource Manager
Merhaba aşağıdaki sınırları yalnızca ağ her Abonelikteki bölge başına Azure Resource Manager aracılığıyla yönetilen kaynakları için geçerlidir.

| Kaynak | Varsayılan limit | Üst Sınır |
| --- | --- | --- |
| Sanal ağlar |50 |500 |
| Sanal ağ başına alt ağ sayısı |1000 |desteğe başvurun |
| Sanal ağ başına DNS sunucusu sayısı |9 |25 |
| Sanal ağ başına özel IP Adresi sayısı |4096 |8192 |
| Ağ arabirimi başına özel IP Adresleri |50 |desteğe başvurun |
| Bir sanal makine veya rol örneği NIC eşzamanlı TCP veya UDP akışlar |500K |500K |
| Ağ Arabirimleri (NIC) |300 |10000 |
| Ağ Güvenlik Grupları (NSG) |100 |400 |
| NSG başına NSG kuralları |200 |500 |
| Kullanıcı tanımlı yol tabloları |100 |200 |
| Yol tablosu başına kullanıcı tanımlı yol sayısı |100 |400 |
| Genel IP adresleri (dinamik) |60 |desteğe başvurun |
| Genel IP adresleri (Statik) |20 |desteğe başvurun |
| Yük Dengeleyici (iç ve internet'e yönelik) |100 |desteğe başvurun |
| Yük Dengeleyici başına yük dengeleyici kuralı |150 |150 |
| IP yapılandırması başına yük dengeleyici kuralı |299 |299 |
| Yük Dengeleyici başına genel ön uç IP |10 |30 |
| Özel ön uç IP yük dengeleyici başına |10 |desteğe başvurun |
| Sanal Ağ başına eşleme |10 |50 |
| VPN Ağ Geçidi başına Noktadan Siteye Kök Sertifika Sayısı |20 |20 |
| Sanal ağ başına ikincil IP yapılandırmaları |1000 |desteğe başvurun |

[Desteğe başvurun](../articles/azure-supportability/resource-manager-core-quotas-request.md ) durumunda varsayılan tooincrease sınırları gerekir.

