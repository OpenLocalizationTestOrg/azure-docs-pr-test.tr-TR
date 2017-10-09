## <a name="route-tables"></a>Yönlendirme tabloları
Rota tablosu kaynakları Azure altyapısı içinde trafiğinin nasıl akacağını kullanılan yolları toodefine içerir. Belirli alt ağ tooa sanal gereç, bir güvenlik duvarı veya izinsiz giriş algılama sistemi gibi (Kimlikler) gelen tüm trafiği kullanıcı tanımlı yolları (UDR) toosend kullanabilirsiniz. Bir rota tablosu toosubnets ilişkilendirebilirsiniz. 

Yönlendirme tabloları aşağıdaki özelliklere hello içerir.

| Özellik | Açıklama | Örnek değerler |
| --- | --- | --- |
| **yollar** |Kullanıcı koleksiyonu yolları hello rota tablosunda tanımlı. |bkz: [kullanıcı tanımlı yollar](#User-defined-routes) |
| **alt ağlar** |Alt ağlar hello yol tablosu koleksiyonunu çok uygulanır|bkz: [alt ağlar](#Subnets) |

### <a name="user-defined-routes"></a>Kullanıcı tanımlı yollar
Hedef adresine göre burada trafiği, gönderilmesi gereken Udr'ler toospecify oluşturabilirsiniz. Bir yolu, bir ağ paketinin hello hedef adresine göre hello varsayılan ağ geçidi tanımı olarak düşünebilirsiniz.

Aşağıdaki özelliklere hello Udr'ler içerir. 

| Özellik | Açıklama | Örnek değerler |
| --- | --- | --- |
| **addressPrefix** |Merhaba hedef tam IP adresini veya adres öneki |192.168.1.0/24, 192.168.1.101 |
| **nextHopType** |Cihaz hello trafik türü çok gönderilir|Değerinin VirtualAppliance, VPN ağ geçidi, Internet |
| **Nexthopıpaddress** |Merhaba sonraki atlama IP adresi |192.168.1.4 |

JSON biçiminde örnek yol tablosu:

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a>Ek kaynaklar
* Hakkında daha fazla bilgi almak [Udr'ler](../articles/virtual-network/virtual-networks-udr-overview.md).
* Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502549.aspx) yönlendirme tabloları için.
* Okuma hello [REST API başvuru belgeleri](https://msdn.microsoft.com/library/azure/mt502539.aspx) için kullanıcı tanımlı yollar (Udr'ler).

