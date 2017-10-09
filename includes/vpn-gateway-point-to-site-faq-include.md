### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Noktadan Siteye ile hangi istemci işletim sistemlerini kullanabilirim?

istemci işletim sistemleri aşağıdaki hello desteklenir:

* Windows 7 (32 bit ve 64 bit)
* Windows Server 2008 R2 (yalnızca 64 bit)
* Windows 8 (32 bit ve 64 bit)
* Windows 8.1 (32 bit ve 64 bit)
* Windows Server 2012 (yalnızca 64 bit)
* Windows Server 2012 R2 (yalnızca 64 bit)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>SSTP destekleyen Noktadan Siteye için herhangi bir yazılım VPN istemcisi kullanabilir miyim?

Hayır. Destek, yukarıda listelenen sınırlı yalnızca toohello Windows işletim sistemi sürümleri içindir.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Noktadan Siteye yapılandırmamda kaç VPN istemci uç noktam olabilir?

Too128 VPN istemcileri toobe mümkün tooconnect tooa sanal ağına hello yukarı aynı destekliyoruz zaman.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Noktadan Siteye bağlanabilirlik için kendi iç PKI kök CA’mı kullanabilir miyim?

Evet. Önceden, yalnızca otomatik olarak imzalanan kök sertifikalar kullanılabiliyordu. 20 kök sertifika yükleyebilirsiniz.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Noktadan Siteye özelliğini kullanarak ara sunucuları ve güvenlik duvarlarını geçirebilir miyim?

Evet. Güvenlik duvarları üzerinden tootunnel SSTP (Güvenli Yuva Tünel Protokolü) kullanıyoruz. Bu tünel bir HTTPs bağlantısı olarak görünür.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Noktası Site için yapılandırılmış bir istemci bilgisayarı yeniden başlatırsanız, hello VPN otomatik olarak yeniden bağlanacak mı?

Varsayılan olarak, hello istemci bilgisayar hello VPN bağlantısı otomatik olarak yeniden başlatmaz.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Noktası Site destek otomatik olarak yeniden ve DDNS üzerinde VPN istemcileri hello?

Otomatik olarak yeniden ve DDNS şu anda Noktadan Siteye VPN'lerde desteklenmiyor.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Siteden siteye sahip olabilir ve noktadan siteye yapılandırmaları bir arada Merhaba aynı sanal ağ?

Evet. Bu her iki çözüm de, ağ geçidiniz için Yol Tabanlı VPN türünüz varsa çalışacaktır. Merhaba Klasik dağıtım modeli için dinamik ağ geçidi gerekir. Biz değil destek noktası siteye statik yönlendirme VPN ağ geçitleri veya hello kullanan ağ geçitleri için yapmak `-VpnType PolicyBased` cmdlet'i.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Merhaba bir noktadan siteye istemci tooconnect toomultiple sanal ağları yapılandırabilirsiniz aynı anda?

Evet, olabilir. Ancak hello sanal ağlar çakışan IP öneklerini sahip olamaz ve hello noktadan siteye adres alanlarının hello sanal ağlar arasında çakışmaması gerekir.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Siteden Siteye ve Noktadan Siteye bağlantılardan ne kadar verimlilik bekleyebilirim?

Zor toomaintain hello tam verimini hello VPN tünelleri olur. IPsec ve SSTP şifrelemesi ağır VPN protokolleridir. Üretilen iş hello gecikme süresi ve şirket içi ve hello Internet arasındaki bant genişliği de sınırlıdır.
