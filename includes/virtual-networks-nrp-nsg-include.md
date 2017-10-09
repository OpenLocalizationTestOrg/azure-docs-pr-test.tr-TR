## <a name="network-security-group"></a>Ağ güvenlik grubu
Bir NSG kaynağı hello iş yükleri için güvenlik sınırı oluşturmanıza olanak tanıyan, uygulama tarafından izin ver ve Reddet kurallarının. Bu tür bir kurallar olabilir uygulanan tooa VM, bir NIC veya bir alt ağ.

| Özellik | Açıklama | Örnek değerler |
| --- | --- | --- |
| **alt ağlar** |Alt ağ kimlikleri hello NSG listesi uygulanır. |/Subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/Subnets/FrontEnd |
| **securityRules** |NSG hello güvenlik kuralları listesi |Bkz: [güvenlik kuralı](#Security-rule) aşağıda |
| **defaultSecurityRules** |Varsayılan güvenlik kuralları her NSG'de mevcut listesi |Bkz: [varsayılan güvenlik kuralları](#Default-security-rules) aşağıda |

* **Güvenlik kuralı** -bir NSG tanımlanan birden çok güvenlik kuralları sahip olabilir. Her bir kural izin verebilir veya trafiği farklı türlerde reddet.

### <a name="security-rule"></a>Güvenlik kuralı
Güvenlik kuralı aşağıdaki hello özelliklerini içeren bir NSG bir alt kaynaktır.

| Özellik | Açıklama | Örnek değerler |
| --- | --- | --- |
| **Açıklama** |Merhaba kuralı için açıklama |Alt ağda X tüm VM'ler için gelen trafiğe izin ver |
| **Protokolü** |Protokol toomatch hello kuralı için |TCP, UDP veya * |
| **sourcePortRange** |Kaynak bağlantı noktası aralığı toomatch hello kuralı için |80, 100-200, * |
| **destinationPortRange** |Hedef bağlantı noktası aralığı toomatch hello kuralı için |80, 100-200, * |
| **sourceAddressPrefix** |Kaynak adres ön eki toomatch hello kuralı için |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **destinationAddressPrefix** |Hedef adres ön eki toomatch hello kuralı için |10.10.10.1, 10.10.10.0/24, VirtualNetwork |
| **yönü** |Merhaba kuralı için trafiği toomatch yönü |gelen veya giden |
| **öncelik** |Merhaba kuralı için öncelik. Kurallar öncelik sırasına göre denetlenir, bir kural uygulandığı zaman başka hiçbir kural eşleştirme için test edilmez. |10, 100, 65000 |
| **erişim** |Merhaba kuralın eşleşmesi durumunda erişim tooapply türü |izin ver veya reddet |

JSON biçiminde NSG örneği:

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a>Varsayılan güvenlik kuralları

Varsayılan güvenlik kuralları olan hello aynı özellikleri güvenlik kurallarında kullanılabilir. Bunlar tooprovide temel bağlantıyı uygulanan Nsg'ler toothem sahip kaynaklar arasında mevcut. Hangi bildiğinizden emin olun [güvenlik kuralları varsayılan](../articles/virtual-network/virtual-networks-nsg.md#default-rules) yok.

### <a name="additional-resources"></a>Ek kaynaklar
* Hakkında daha fazla bilgi almak [Nsg'ler](../articles/virtual-network/virtual-networks-nsg.md).
* Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163615.aspx) Nsg'ler için.
* Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt163580.aspx) güvenlik kuralları için.
