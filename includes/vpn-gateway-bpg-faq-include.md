### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>BGP tüm Azure VPN Gateway SKU'larında destekleniyor mu?
Hayır, BGP Azure **Standart**’ta ve **HighPerformance** VPN Gateway’lerinde desteklenir. **Temel** SKU DESTEKLENMEZ.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Azure İlke Temelli VPN ağ geçitleriyle BGP kullanabilir miyim?
Hayır, BGP yalnızca Rota Temelli VPN Gateway’lerinde desteklenir.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Özel ASN’ler (Otonom Sistem Numaralarını) kullanabilir miyim?
Evet, kendi ortak ASN’lerinizi veya özel ASN’lerinizi hem şirket içi ağlarda, hem de Azure sanal ağlarda kullanabilirsiniz.

### <a name="are-there-asns-reserved-by-azure"></a>Azure tarafından ayrılan bir ASN var mı?
Evet, hello aşağıdaki Asn'ler Azure tarafından iç ve dış eşlemeleri için ayrılmıştır:

* Ortak ASN’ler: 8075, 8076, 12076
* Özel ASN’ler: 65515, 65517, 65518, 65519, 65520

Bu Asn'ler şirketinizdeki için VPN aygıtları tooAzure VPN ağ geçitleri bağlanırken belirtemezsiniz.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Kullanamayacağım başka ASN var mı?
Evet, Asn'ler aşağıdaki hello olan [IANA tarafından ayrılmış](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) ve Azure VPN ağ geçidinizi üzerinde yapılandırılamaz:

23456, 64496-64511, 65535-65551 and 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>Merhaba kullanabilirim her ikisi için de aynı ASN şirket içi VPN ağlarında hem Azure Vnet?
Hayır, BGP’yle bunlara birlikte bağlanıyorsanız, şirket içi ağlar ve Azure VNet'ler arasında farklı ASN’ler atamanız gerekir. Şirket içi ve dışı karışık bağlantınız için BGP'nin etkin olup olmamasından bağımsız olarak Azure VPN Ağ Geçitlerine varsayılan 65515 ASN'si atanmıştır. Merhaba VPN gateway oluştururken farklı ASN atayarak bu varsayılanı geçersiz kılabilir veya hello ağ geçidi oluşturulduktan sonra hello ASN değiştirin. Azure yerel ağ geçitlerine karşılık gelen, şirket içi Asn'ler toohello tooassign gerekir.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>Hangi adres önekleri Azure VPN ağ geçitleri tanıtma toome?
Azure VPN ağ geçidi yollarını tooyour şirket içi BGP cihazları aşağıdaki hello tanıtacaktır:

* VNet adres önekleriniz
* Her yerel ağ geçidi bağlı toohello Azure VPN ağ geçidi için adres önekleri
* Diğer BGP eşliği oturumlarını bağlı toohello Azure VPN ağ geçidi'nden, öğrenilen rotalar **dışında varsayılan bir yol veya yollar herhangi bir VNet önekiyle çakışan**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Varsayılan yol (0.0.0.0/0) tooAzure VPN ağ geçitleri tanıtma?
Evet.

Bu, şirket içi sitenizi bulunun tüm VNet çıkış trafiği zorlar ve hello VNet VM'ler hello Internet doğrudan, böyle bir RDP veya SSH hello Internet toohello VM'ler ortak iletişimini kabul etmesini engeller lütfen unutmayın.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>My sanal ağ öneklerini tam hello öneklerini yayınlamak?

Hayır, aynı sanal ağ adres öneklerini herhangi biri önekleri reklam hello engellenen veya Azure platformu hello göre filtrelenir. Ancak, Sanal Ağınızda bulunanların üst kümesi olan bir ön ek tanıtabilirsiniz. 

Örneğin, sanal ağınızı hello adres alanı 10.0.0.0/16 kullandıysanız, 10.0.0.0/8 tanıtım. Ancak 10.0.0.0/16 veya 10.0.0.0/24 tanıtamazsınız.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>VNet - VNet bağlantılarımla BGP kullanabilir miyim?
Evet, BGP’yi hem şirket içi bağlantılar için, hem de VNet - VNet bağlantıları için kullanabilirsiniz.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Azure VPN Gateway’lerim için BGP’yi BGP olmayan bağlantılarla karıştırabilir miyim?
Evet, her iki BGP karıştırabilirsiniz ve aynı Azure VPN ağ geçidi için BGP olmayan bağlantıları hello.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Azure VPN Gateway BGP transit rotasını destekliyor mu?
Evet, BGP transit rotasını, Azure VPN gateway'lerinin hello özel durumla destekleniyor **değil** tooother BGP eşleri varsayılan yolları tanıtma. tooenable transit birden çok Azure VPN ağ geçidi yönlendirme, BGP tüm ara VNet-VNet bağlantıları etkinleştirmeniz gerekir.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Azure VPN Gateway ve şirket içi ağım arasında birden fazla tünelim olabilir mi?
Evet, bir Azure VPN Gateway ve şirket içi ağınız arasında birden fazla S2S tüneli kurabilirsiniz. Lütfen bu tüneller tünelleri, Azure VPN ağ geçitleri için toplam sayısı hello karşı sayılan ve üzerinde her iki tünel BGP etkinleştirmelisiniz unutmayın.

Örneğin, Azure VPN ağ geçidinizi ve şirket içi ağlarınız arasında iki yedekli tüneller varsa, bunlar hello toplam kotasından (Standard için 10) ve HighPerformance için de 30'de, Azure VPN ağ geçidi 2 Tünel tüketir.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>BGP bulunan iki Azure VNet arasında birden çok tünelim olabilir mi?
Evet, ancak hello sanal ağ geçitlerini en az birinin etkin-etkin yapılandırmada olması gerekir.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>BGP’yi ExpressRoute/S2S VPN birlikte varolma yapılandırmasında S2S VPN için kullanabilir miyim?
Evet. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Azure VPN Gateway BGP Eşdeğer IP’si için hangi adresi kullanıyor?
Hello Azure VPN ağ geçidi hello hello sanal ağ için ayrılan GatewaySubnet aralığından gelen tek bir IP adresi ayırır. Varsayılan olarak, bu hello ikinci son hello aralığı adresidir. Örneğin, GatewaySubnet 10.12.255.0/27 ise, 10.12.255.0 arasında değişen too10.12.255.31, hello hello Azure VPN ağ geçidi BGP eşdeğer IP adresi 10.12.255.30 olacaktır. Hello Azure VPN gateway bilgilerini listelediğinizde bu bilgileri bulabilirsiniz.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>VPN cihazımdaki BGP eşdeğer IP adreslerinin hello hello gereksinimleri nelerdir?
Şirket içi BGP eş adresinizi **gerekir** olması hello aynı hello ortak IP adresi, VPN cihazınızın olarak. Farklı bir IP adresi hello VPN cihazında BGP eşdeğer IP'si için kullanın. Merhaba aygıt toohello geri döngü arabirimine atanmış bir adres olabilir. Bu adres hello karşılık gelen yerel ağ geçidi temsil eden hello konumu belirtin.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>BGP kullandığımda ne ı my hello yerel ağ geçidi için adres önekleri olarak belirtmeniz gerekir?
Azure yerel ağ geçidi hello şirket içi ağ için hello başlangıç adresi öneklerini belirtir. BGP ile Merhaba konak önekini ayırmalısınız (/ 32 önek) bu şirket içi ağın adres alanı hello olarak BGP eşdeğer IP adresinizin. BGP eşdeğer IP'niz 10.52.255.254 olursa, hello bu şirket içi ağda temsil yerel ağ geçidi, hello localNetworkAddressSpace olarak "10.52.255.254/32" belirtmeniz gerekir. Azure VPN hello tooensure budur ağ geçidi hello hello S2S VPN tüneli aracılığıyla BGP oturumunu oluşturur.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>Ne toomy şirket içi VPN cihazı hello BGP eşdeğer oturumu için eklemelisiniz?
Toohello IPSec S2S VPN tüneli işaret eden VPN cihazınızdaki Azure BGP eşdeğer IP adresi hello konak rotasını eklemeniz gerekir. Örneğin, Hello Azure VPN eşdeğer IP'si "10.12.255.30" ise, VPN cihazınızdaki hello eşleşen IPSec tüneli arabiriminin sonraki atlama arabirimiyle "10.12.255.30" için bir konak rotası eklemelisiniz.

