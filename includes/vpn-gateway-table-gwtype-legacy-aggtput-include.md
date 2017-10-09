Merhaba aşağıdaki tabloda hello ağ geçidi türleri ve tahmini toplam verimlilik hello SKU ağ geçidiyle gösterilmektedir. Bu tablo toohello Resource Manager ve klasik dağıtım modellerine uygulanır. 

Ağ geçidi SKU'ları arasında fiyatlandırma farklılık gösterir. Daha fazla bilgi için bkz. [VPN Gateway Fiyatlandırması](https://azure.microsoft.com/pricing/details/vpn-gateway).

Bu tabloda SKU temsil edilmeyen bu hello UltraPerformance ağ geçidi unutmayın. Merhaba hello UltraPerformance SKU hakkında daha fazla bilgi için bkz [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) belgeleri.

|  | **VPN Gateway performansı (1)** | **VPN Gateway maks. IPsec tüneli (2)** | **ExpressRoute Gateway performansı** | **VPN Gateway ve ExpressRoute bir arada** |
| --- | --- | --- | --- | --- |
| **Temel SKU (3)(5)(6)** |100 Mbps |10 |500 Mbps (6) |Hayır |
| **Standart SKU (4)(5)** |100 Mbps |10 |1000 Mb/sn |Evet |
| **Yüksek Performanslı SKU (4)** |200 Mbps |30 |2000 Mb/sn |Evet |


(1) hello VPN verimlilik olduğu hello ölçümleri hello Vnet'ler arasında dayalı bir kaba tahmini aynı Azure bölgesi. Şirket içi bağlantılar için garantili işleme hello Internet değil. Merhaba olası en yüksek verimlilik ölçüm olur.

(2) tooRouteBased VPN tünelleri hello sayısı bakın. PolicyBased VPN yalnızca tek bir Siteden Siteye VPN tünelini destekleyebilir.

(3) BGP Merhaba temel SKU desteklenmez.

(4) PolicyBased VPN'ler bu SKU için desteklenmez. Bunlar yalnızca hello temel SKU için desteklenir.

(5) Etkin-etkin S2S VPN Gateway bağlantıları bu SKU için desteklenmiyor. Etkin-etkin yalnızca hello HighPerformance SKU üzerinde desteklenir.

(6) temel SKU ExpressRoute ile kullanmak için kullanım dışıdır.
