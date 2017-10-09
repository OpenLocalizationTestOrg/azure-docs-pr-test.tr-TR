## <a name="load-balancer-differences"></a>Load Balancer farklılıkları

Microsoft Azure kullanarak farklı seçenekler toodistribute ağ trafiğini vardır. Bu seçenekler birbirlerinden farklı şekilde çalışır, farklı özelliklere sahiptir ve farklı senaryoları destekler. Birbirlerinden ayrı olarak veya birleştirilerek kullanılabilirler.

* **Azure yük dengeleyici** hello aktarım katmanında (Merhaba OSI Ağ başvurusu yığınında katman 4) çalışır. Hello çalışan bir uygulama örnekleri arasında trafiği ağ düzeyinde dağıtım sağladığı aynı Azure veri merkezi.
* **Uygulama ağ geçidi** hello uygulama katmanında (Merhaba OSI Ağ başvurusu yığınında katman 7) çalışır. Merhaba istemci bağlantısı kesiliyor bir ters proxy hizmeti davranır ve iletme tooback uç uç noktaları ister.
* **Trafik Yöneticisi** DNS düzeyi hello çalışır.  DNS yanıtları toodirect son kullanıcı trafiği dağıtılmış tooglobally uç noktaları kullanır. İstemciler daha sonra toothose uç noktaları doğrudan bağlanır.

Aşağıdaki tablonun hello her hizmeti tarafından sunulan hello özellikleri özetlenmektedir:

| Hizmet | Azure Load Balancer | Application Gateway | Traffic Manager |
| --- | --- | --- | --- |
| Teknoloji |Aktarım düzeyi (Katman 4) |Uygulama düzeyi (Katman 7) |DNS düzeyi |
| Desteklenen uygulama protokolleri |Herhangi biri |HTTP, HTTPS ve WebSockets |Herhangi biri (Uç nokta izleme için HTTP uç noktası gereklidir) |
| Uç Noktalar |Azure VM’leri ve Cloud Services rol örnekleri |Herhangi bir iç Azure IP adresi, genel internet IP adresi, Azure VM veya Azure Bulut Hizmeti |Azure VM’leri, Cloud Services, Azure Web Apps ve dış uç noktalar |
| Vnet desteği |Hem İnternet’e yönelik hem de iç (Vnet) uygulamalar için kullanılabilir |Hem İnternet’e yönelik hem de iç (Vnet) uygulamalar için kullanılabilir |Yalnızca İnternet'e yönelik uygulamaları destekler |
| Uç Nokta İzleme |Araştırmalar aracılığıyla desteklenir |Araştırmalar aracılığıyla desteklenir |HTTP/HTTPS GET aracılığıyla desteklenir |

Azure yük dengeleyici ve uygulama ağ geçidi rota ağ trafiği tooendpoints ancak farklı kullanım senaryoları toowhich trafiği toohandle sahip. Merhaba aşağıdaki tabloda anlama hello hello iki yük dengeleyici birbirinden yardımcı olur:

| Tür | Azure Load Balancer | Application Gateway |
| --- | --- | --- |
| Protokoller |UDP/TCP |HTTP, HTTPS ve WebSockets |
| IP ayırma |Destekleniyor |Desteklenmiyor |
| Yük dengeleme modu |5’li demet (kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası, protokol türü) |Hepsini Bir Kez Deneme<br>URL'ye dayalı yönlendirme |
| Yük dengeleme modu (kaynak IP/yapışkan oturumlar) |2’li demet (kaynak IP ve hedef IP), 3’lü demet (kaynak IP, hedef IP ve bağlantı noktası). Yukarı veya aşağı hello sanal makinelerin sayısına göre ölçeği |Tanımlama bilgisi tabanlı benzeşim<br>URL'ye dayalı yönlendirme |
| Sistem durumu araştırmaları |Varsayılan: araştırma aralığı - 15 saniye Yönlendirme dışına çıkarma: Arka arkaya 2 hata. Kullanıcı tanımlı araştırmaları destekler |Boşta araştırma aralığı 30 saniye. Arka arkaya 5 canlı trafik hatasından veya boşta modunda tek bir araştırma hatasından sonra çıkarılır. Kullanıcı tanımlı araştırmaları destekler |
| SSL aktarma |Desteklenmiyor |Destekleniyor |
| URL tabanlı yönlendirme | Desteklenmiyor | Destekleniyor|
| SSL İlkesi | Desteklenmiyor | Destekleniyor|
