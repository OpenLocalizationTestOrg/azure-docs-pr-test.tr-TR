|  | **Noktadan siteye** | **Siteden siteye** | **ExpressRoute** |
| --- | --- | --- | --- |
| **Azure Hizmetleri desteklenmez** |Cloud Services ve Virtual Machines |Cloud Services ve Virtual Machines |[Hizmetler listesi](../articles/expressroute/expressroute-faqs.md#supported-services) |
| **Tipik bant genişlikleri** |Tipik olarak < 100 Mb/sn toplu |Genellikle < 1 GB/sn toplama |50 Mb/sn, 100 Mb/sn, 200 Mb/sn, 500 Mb/sn, 1 Gb/sn, 2 Gb/sn, 5 Gb/sn, 10 Gb/sn |
| **Desteklenen protokoller** |Güvenli Yuva Tünel Protokolü (SSTP) |IPsec |VLAN, NSP'nin VPN’si teknolojileri (MPLS, VPLS,...) üzerinden doğrudan bağlantı |
| **Yönlendirme** |RouteBased (dinamik) |PolicyBased (statik yönlendirme) ve RouteBased (dinamik yönlendirme VPN) destekliyoruz |BGP |
| **Bağlantı dayanıklılığı** |Etkin-Edilgen |Etkin-pasif veya aktif-aktif |etkin-edilgen |
| **Tipik kullanım örneği** |Prototip oluşturma, Cloud Services ve Virtual Machines için geliştirme / test / laboratuvar senaryoları |Cloud Services ve Virtual Machines için geliştirme / test / laboratuvar senaryoları ve küçük ölçekli üretim iş yükleri |Tooall Azure Erişim Hizmetleri (doğrulanmış liste), kurumsal sınıf ve görev kritik iş yükleri, yedekleme, büyük veri, DR sitesi olarak Azure |
| **SLA** |[SLA](https://azure.microsoft.com/support/legal/sla/) |[SLA](https://azure.microsoft.com/support/legal/sla/) |[SLA](https://azure.microsoft.com/support/legal/sla/) |
| **Fiyatlandırma** |[Fiyatlandırma](https://azure.microsoft.com/pricing/details/vpn-gateway/) |[Fiyatlandırma](https://azure.microsoft.com/pricing/details/vpn-gateway/) |[Fiyatlandırma](https://azure.microsoft.com/pricing/details/expressroute/) |
| **Teknik belgeler** |[VPN ağ geçidi belgeleri](https://azure.microsoft.com/documentation/services/vpn-gateway/) |[VPN ağ geçidi belgeleri](https://azure.microsoft.com/documentation/services/vpn-gateway/) |[ExpressRoute belgeleri](https://azure.microsoft.com/documentation/services/expressroute/) |
| **SSS** |[VPN Gateway ile ilgili SSS](../articles/vpn-gateway/vpn-gateway-vpn-faq.md) |[VPN Gateway ile ilgili SSS](../articles/vpn-gateway/vpn-gateway-vpn-faq.md) |[ExpressRoute ile ilgili SSS](../articles/expressroute/expressroute-faqs.md) |

