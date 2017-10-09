Merhaba eski (eski) VPN ağ geçidi SKU'ları şunlardır:

* Temel
* Standart
* HighPerformance

VPN ağ geçidi hello UltraPerformance ağ geçidi SKU'su kullanmaz. Merhaba hello UltraPerformance SKU hakkında daha fazla bilgi için bkz [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) belgeleri.

İle çalışırken, eski SKU'ları Merhaba, hello aşağıdakileri göz önünde bulundurun:

* Toouse PolicyBased VPN türüne istiyorsanız hello temel SKU kullanmanız gerekir. PolicyBased VPN'ler (daha önce Statik Yönlendirme olarak biliniyordu), diğer SKU’larda desteklenmez.
* BGP hello temel SKU üzerinde desteklenmiyor.
* ExpressRoute VPN ağ geçidi bir arada yapılandırmaları hello temel SKU üzerinde desteklenmiyor.
* Etkin-etkin S2S VPN Gateway bağlantıları yalnızca hello HighPerformance SKU üzerinde yapılandırılabilir.
