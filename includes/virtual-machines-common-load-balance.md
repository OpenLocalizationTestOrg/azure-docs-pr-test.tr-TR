

Azure altyapı hizmetleri için Yük Dengeleme iki düzeyi vardır:

* **DNS düzeyi**: trafiği toodifferent bulut Hizmetleri için Yük Dengeleme yer alan farklı veri merkezleri, toodifferent Azure Web siteleri yer alan farklı veri merkezlerinde veya tooexternal uç noktaları. Bu Azure Traffic Manager ile gerçekleştirilir ve hello hepsini bir kez Yük Dengeleme yöntemi.
* **Ağ düzeyinde**: Yük Dengeleme gelen Internet trafiği toodifferent sanal makinelerin bir bulut hizmeti ya da Yük Dengeleme sanal makineler bir bulut hizmeti ya da sanal ağ arasında trafiği. Bu hello Azure yük dengeleyici ile gerçekleştirilir.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>Trafik Yöneticisi Yük Dengeleme bulut Hizmetleri ve Web siteleri için
Trafik Yöneticisi toocontrol hello bulut Hizmetleri, Web siteleri, dış sitelere ve diğer Traffic Manager profillerini içerebilir kullanıcı trafiği tooendpoints dağıtımını sağlar. Trafik Yöneticisi, bir akıllı ilke altyapısı tooDomain Adı Sistemi (DNS) sorguları, Internet kaynakların hello etki alanı adları için uygulayarak çalışır. Bulut Hizmetleri veya Web siteleri farklı veri merkezlerinde Merhaba dünya genelindeki çalıştırıyor olabilir.

REST veya Windows PowerShell tooconfigure dış uç noktalar veya Traffic Manager profillerini uç noktalar olarak kullanmanız gerekir.

Trafik Yöneticisi üç kullanan yük dengeleme yöntemleri toodistribute trafiğini:

* **Yük devretme**: toouse birincil bir uç nokta için tüm trafiği istiyor, ancak birincil hello kullanılamaz hale gelmesi durumu yedeklemeleri sağlar, bu yöntemi kullanın.
* **Performans**: uç noktası farklı coğrafi konumlarda bulunan ve istemcilerin toouse hello "en yakın" uç nokta hello en düşük gecikme süresi açısından isteyen istediğinizde bu yöntemi kullanın.
* **Hepsini bir kez:** toodistribute yük kümesi boyunca bulut Hizmetleri hello aynı istediğinizde bu yöntemi kullanın datacenter veya Bulut Hizmetleri ya da farklı veri merkezlerinde bulunan Web siteleri arasında.

Daha fazla bilgi için bkz: [hakkında trafik Yöneticisi Yük Dengeleme yöntemleri](../articles/traffic-manager/traffic-manager-routing-methods.md).

Diyagram aşağıdaki hello hello farklı bulut hizmetleri arasında trafiği dağıtmak için hepsini bir kez Yük Dengeleme yöntemi örneği gösterilmektedir.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

Merhaba temel işlem hello aşağıda verilmiştir:

1. Bir Internet istemcisi bir etki alanı adı karşılık gelen tooa web hizmeti sorgular.
2. DNS hello adı sorgu isteği tooTraffic Yöneticisi iletir.
3. Trafik Yöneticisi hello sonraki bulut hizmeti hello hepsini bir kez listesi seçer ve DNS adı geri gönderir hello. Hello Internet istemcinin DNS sunucusu hello adı tooan IP adresi çözümler ve toohello Internet istemcisi gönderir.
4. Trafik Yöneticisi tarafından seçilen hello bulut hizmeti ile Merhaba Internet istemcisi bağlanır.

Daha fazla bilgi için bkz: [trafik Yöneticisi](../articles/traffic-manager/traffic-manager-overview.md).

## <a name="azure-load-balancing-for-virtual-machines"></a>Azure Yük Dengelemesi için sanal makineler
Sanal makineler aynı bulut hizmetine hello veya sanal ağ birbirleri ile özel IP adreslerini kullanarak doğrudan iletişim kurabilir. Bilgisayarlar ve hizmetler hello dışında bulut hizmeti veya sanal ağ yalnızca sanal makineler bir bulut hizmeti ya da sanal ağ ile yapılandırılmış bir uç noktası ile iletişim kurabilir. Bir eşleme bir ortak IP adresi ve bağlantı noktası toothat özel IP adresi ve bağlantı noktası bir sanal makine veya bir Azure bulut hizmeti içinde web rolü bir uç noktadır.

Hello Azure yük dengeleyici gelen trafiği belirli bir türde birden çok sanal makineleri veya hizmetleri yük dengeli bir küme olarak bilinen bir yapılandırma rastgele dağıtır. Örneğin, birden çok web sunucuları veya web rolleri web isteği trafiği hello yükünü yayılabilir.

Merhaba Aşağıdaki diyagramda hello ortak ve özel TCP bağlantı noktası 80 için üç sanal makineler arasında paylaşılan standart (şifrelenmemiş) web trafiği için yük dengeli bir uç nokta gösterilmektedir. Bu üç sanal makine bir yük dengeli kümesi yok.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

Daha fazla bilgi için bkz: [Azure yük dengeleyici](../articles/load-balancer/load-balancer-overview.md). Merhaba, yük dengeli kümesi toocreate adımları için bkz: [yük dengeli bir küme Yapılandır](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md).

Azure bulut hizmeti ya da sanal ağ içinde bakiye de yükleyebilirsiniz. Bu, iç Yük Dengeleme olarak bilinir ve yolları aşağıdaki hello kullanılabilir:

* çok katmanlı bir uygulama (örneğin, web ve veritabanı katmanları arasında) farklı katmanlarda sunucuları arasında tooload bakiye.
* (ek yük dengeleyici donanım veya yazılım gerektirmeden Azure üzerinde barındırılan tooload Bakiye satır iş kolu LOB) uygulamaları.
* tooinclude sunucular, bilgisayarlar, trafik yükü dengelenmiş hello kümesi şirket içi.

Benzer tooAzure Yük Dengeleme iç Yük Dengeleme bir iç yük dengeli kümesi yapılandırarak sayesinde kolaylaşır.

Aşağıdaki diyagramda hello iç yük dengeli uç nokta bir hattı üç sanal makineler arasında bir şirket içi sanal ağda paylaşılan iş (LOB) uygulaması için bir örneği gösterilmektedir.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>Yük Dengeleyici konuları
Bir yük dengeleyicinin varsayılan olarak yapılandırılmış tootimeout 4 dakika boşta oturumunda bir. Yük Dengeleyici arkasında uygulamanız bağlantı boşta 4 dakikadan fazla bırakır ve tutma yapılandırma yok, hello bağlantı bırakılır. Merhaba yük dengeleyici davranışını tooallow değiştirebileceğiniz bir [Azure yük dengeleyici için uzun bir zaman aşımı ayarını](../articles/load-balancer/load-balancer-tcp-idle-timeout.md).

Diğer göz önünde bulundurarak, Azure yük dengeleyici tarafından desteklenen dağıtım modunun hello türüdür. Kaynak IP benzeşimi (kaynak IP, hedef IP) veya kaynak IP Protokolü (kaynak IP, hedef IP ve Protokolü) yapılandırabilirsiniz. Kullanıma [Azure yük dengeleyici dağıtım modu (kaynak IP benzeşim)](../articles/load-balancer/load-balancer-distribution-mode.md) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba, yük dengeli kümesi toocreate adımları için bkz: [bir iç yük dengeli kümesi yapılandırma](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md).

Yük Dengeleyici hakkında daha fazla bilgi için bkz: [iç Yük Dengeleme](../articles/load-balancer/load-balancer-internal-overview.md).

