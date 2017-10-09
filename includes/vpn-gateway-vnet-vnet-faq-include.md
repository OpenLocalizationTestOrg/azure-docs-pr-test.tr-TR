Merhaba VNet-VNet SSS tooVPN ağ geçidi bağlantılara uygulanır. Sanal Ağ Eşleme konusunu arıyorsanız bkz. [Sanal Ağ Eşleme](../articles/virtual-network/virtual-network-peering-overview.md)

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Azure sanal ağlar arasındaki trafik için ücretli midir?

VNet-VNet trafiği hello içinde aynı bölge olduğunda her iki yön için boş bir VPN ağ geçidi bağlantısı kullanarak. Bölge sanal ağdan sanal ağa çıkış trafiği hello giden arası VNet veri aktarım hızı hello kaynak bölgelerine bağlı ücretlendirilir. Toohello başvuran [VPN ağ geçidi fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/vpn-gateway/) Ayrıntılar için. VNet eşlemesi, VPN ağ geçidi yerine, sanal ağlar bağlanıyorsanız hello bkz [sanal ağ fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>VNet-VNet trafiği hello Internet yolculuk ediyor mu?

Hayır. VNet-VNet trafiği hello Microsoft Azure omurga, hello Internet geçen.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Sanal Ağdan Sanal Ağa trafiği güvenli mi?

Evet, IPsec/IKE şifrelemesiyle korunur.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>Bir VPN cihazı tooconnect sanal ağlar birlikte gerekiyor mu?

Hayır. İşletmeler arası bağlantı gerekmediği sürece birden fazla Azure sanal ağını birleştirmek için VPN cihazına gerek yoktur.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>My sanal ağlar hello toobe gerek aynı bölgede?

Hayır. Merhaba sanal ağlar hello olabilir aynı veya farklı Azure bölgeleri (konumlara).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Merhaba sanal ağlar içinde değilse aynı hello hello abonelikleri aboneliğiniz hello aynı AD Kiracı ile ilişkilendirilen toobe?

Hayır.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Sanal Ağdan Sanal Ağa bağlantıyı çoklu site bağlantılarıyla birlikte kullanabilir miyim?

Evet. Sanal ağ bağlantısı, çoklu site VPN’leri ile eşzamanlı olarak kullanılabilir.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Bir sanal ağ kaç şirket içi siteye ve sanal ağa bağlanabilir?

[Ağ geçidi gereksinimleri](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) tablosuna bakın.

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>I VNet-VNet tooconnect VM'ler kullanabilir veya Bulut hizmetlerini bir sanal ağ dışında?

Hayır. Sanal Ağdan Sanal Ağa, sanal ağları bağlamayı destekler. Bir sanal ağ içinde olmayan sanal makineleri veya bulut hizmetlerini bağlamayı desteklemez.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Bir bulut hizmeti ya da bir yük dengeleme uç noktası sanal ağlara yayılabilir mi?

Hayır. Bir bulut hizmeti ya da yük dengeleme uç noktası, birbirlerine bağlı olsa da sanal ağlara yayılamaz.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Sanal Ağdan Sanal Ağa veya Çoklu Site bağlantıları için PolicyBased VPN türü kullanabilir miyim?

Hayır. Sanal Ağdan Sanal Ağa ve Çoklu Site bağlantıları, Azure VPN ağ geçitlerinin, önceki adı Dinamik Yönlendirme olan RouteBased VPN türleri ile bağlantılarını VPN geçidi ile bağlamalarını gerektirir.

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>PolicyBased VPN türüne bir RouteBased VPN türü tooanother VNet t bir VNet bağlanabiliyor musunuz?

Hayır, her iki sanal ağın da rota tabanlı (önceki adıyla Dinamik Yönlendirme) VPN kullanıyor olması GEREKİR.

### <a name="do-vpn-tunnels-share-bandwidth"></a>VPN tünelleri bant genişliğini paylaşır mı?

Evet. Merhaba sanal ağ tüm VPN tünelleri hello hello Azure VPN ağ geçidi üzerinde kullanılabilir bant genişliğini paylaşır ve aynı VPN ağ geçidi çalışma süresi SLA azure'da hello.

### <a name="are-redundant-tunnels-supported"></a>Yedekli tüneller destekleniyor mu?

Bir sanal ağ çifti arasındaki yedekli tüneller, sanal ağ geçitlerinden biri etkin-etkin olarak yapılandırıldığında desteklenir.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Sanal Ağdan Sanal Ağa yapılandırmalar için çakışan adres alanları kullanabilir miyim?

Hayır. Çakışan IP adresi aralıklarını kullanamazsınız.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Bağlı sanal ağlar ve şirket içi yerel siteleri arasında çakışan adres alanları olabilir mi?

Hayır. Çakışan IP adresi aralıklarını kullanamazsınız.



