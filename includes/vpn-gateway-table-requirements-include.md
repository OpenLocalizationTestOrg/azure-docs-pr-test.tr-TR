PolicyBased ve RouteBased VPN ağ geçitleri için Tablo listeleri hello gereksinimleri aşağıdaki hello. Bu tablo tooboth hello Resource Manager ve klasik dağıtım modellerine uygulanır. Merhaba Klasik modeli için PolicyBased VPN ağ geçitleri olan hello aynı statik ağ geçitleri olarak ve rota tabanlı ağ geçitleri olan hello aynı dinamik ağ geçitleri olarak.

|  | **PolicyBased temel VPN ağ geçidi** | **RouteBased temel VPN ağ geçidi** | **RouteBased standart VPN ağ geçidi** | **RouteBased yüksek performanslı VPN Gateway** |
| --- | --- | --- | --- | --- |
| **Siteden siteye bağlantı (S2S)** |PolicyBased VPN yapılandırması |RouteBased VPN yapılandırması |RouteBased VPN yapılandırması |RouteBased VPN yapılandırması |
| **Noktadan Siteye bağlantı (P2S**) |Desteklenmiyor |Destekleniyor (S2S ile birlikte var olabilir) |Destekleniyor (S2S ile birlikte var olabilir) |Destekleniyor (S2S ile birlikte var olabilir) |
| **Kimlik doğrulama yöntemi** |Önceden paylaşılan anahtar |S2S bağlantısı için önceden paylaşılan anahtar, P2S bağlantısı için sertifikalar |S2S bağlantısı için önceden paylaşılan anahtar, P2S bağlantısı için sertifikalar |S2S bağlantısı için önceden paylaşılan anahtar, P2S bağlantısı için sertifikalar |
| **S2S bağlantısı sayısı** |1 |10 |10 |30 |
| **P2S bağlantısı sayısı** |Desteklenmiyor |128 |128 |128 |
| **Etkin yönlendirme desteği (BGP)** |Desteklenmiyor |Desteklenmiyor |Destekleniyor |Destekleniyor |

