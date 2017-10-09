Bir sanal ağ geçidi oluştururken toospecify hello ağ geçidi SKU'su toouse istediğiniz gerekir. İş yükleri, kapatma, özellikleri ve SLA hello türlerine göre gereksinimlerinizi karşılayan hello SKU'ları seçin.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>Üretim *ve* Geliştirme-Test İş Yükleri Karşılaştırması

Üretim için SKU'ları aşağıdaki hello öneririz SLA ve özellik kümeleri toohello farklılıkları *karşılaştırması* geliştirme, test:

| **İş yükü**                       | **SKU'lar**               |
| ---                                | ---                    |
| **Üretim, kritik iş yükleri** | VpnGw1, VpnGw2, VpnGw3 |
| **Geliştirme-test veya kavram kanıtı**   | Temel                  |
|                                    |                        |

Merhaba eski kullanıyorsanız, hello üretim SKU önerileri standart ve HighPerformance SKU'ları SKU'lar. Eski SKU hello hakkında bilgi için bkz: [ağ geçidi SKU'ları (eski SKU)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).

###  <a name="feature"></a>Ağ geçidi SKU'su özellik kümeleri

Merhaba gateway'lerinde sunulan hello yeni ağ geçidi SKU'ları daha verimli hale hello özellik kümeleri:

| **SKU**| **Özellikler**|
| ---    | ---         |
|**Temel**   | **Rota tabanlı VPN**: P2S ile 10 tünel<br><br>**İlke tabanlı VPN** (IKEv1): 1 tünel; P2S yok|
| **VpnGw1, VpnGw2 ve VpnGw3** | **Rota tabanlı VPN**: too30 tünelleri (*), P2S, BGP yukarı etkin-etkin, özel IPSec/IKE İlkesi, ExpressRoute/VPN birlikte bulunma |
|        |             |

(*) Bir rota tabanlı VPN ağ geçidi (VpnGw1, VpnGw2, VpnGw3) toomultiple şirket içi ilke tabanlı güvenlik duvarı aygıtları "PolicyBasedTrafficSelectors" tooconnect yapılandırabilirsiniz. Çok başvuran[bağlanmak VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtları PowerShell kullanarak](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) Ayrıntılar için.

###  <a name="resize"></a>Ağ geçidi SKU'larını yeniden boyutlandırma

1. VpnGw1, VpnGw2 ve VpnGw3 SKU'ları arasında yeniden boyutlandırma gerçekleştirebilirsiniz.
2. Merhaba eski gateway SKU'ları ile çalışırken, temel, standart ve HighPerformance SKU'ları arasında yeniden boyutlandırabilirsiniz.
2. **Olamaz** standart/Basic/HighPerformance SKU'ları toohello yeniden boyutlandırma yeni VpnGw2/VpnGw1/VpnGw3 SKU'ları. Bunun yerine, gerekir [geçirmek](#migrate) toohello yeni SKU'ları.

###  <a name="migrate"></a>Eski SKU'ları toohello geçiş yeni SKU'ları

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
