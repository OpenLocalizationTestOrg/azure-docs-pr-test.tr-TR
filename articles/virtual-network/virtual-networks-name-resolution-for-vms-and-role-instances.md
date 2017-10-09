---
title: "VM'ler ve rol örnekleri için aaaResolution"
description: "Azure Iaas, farklı bulut Hizmetleri, Active Directory ve kendi DNS sunucusu kullanılarak arasındaki karma çözümleri için çözüm senaryoları adı "
services: virtual-network
documentationcenter: na
author: GarethBradshawMSFT
manager: carmonm
editor: tysonn
ms.assetid: 5d73edde-979a-470a-b28c-e103fcf07e3e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/06/2016
ms.author: telmos
ms.openlocfilehash: 0ec7903cf200c1d04d75601a5b0cefe4268f3dcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="name-resolution-for-vms-and-role-instances"></a>VM’ler ve Rol Örnekleri için Ad Çözümleme
Azure toohost Iaas ve PaaS karma çözümleri kullanma bağlı olarak, tooallow hello VM'ler ve rol örnekleri toocommunicate birbirleri ile oluşturduğunuz gerekebilir. Bu iletişim, IP adreslerini kullanarak yapılabilir rağmen kolay anımsanacak ve değiştirmeyin daha kolay toouse adların eklenir. 

Rol örnekleri ve Azure üzerinde barındırılan sanal makineleri tooresolve etki alanı adları toointernal IP adreslerine gerektiğinde, bunlar iki yöntemden birini kullanabilirsiniz:

* [Azure tarafından sağlanan ad çözümlemesi](#azure-provided-name-resolution)
* [Kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) (hangi iletmek sorguları toohello Azure tarafından sağlanan DNS sunucuları) 

kullandığınız ad çözümlemesi Hello türünün nasıl VM'ler ve rol örnekleri birbirleriyle toocommunicate gereksinimlerine göre değişir.

**Merhaba aşağıdaki tabloda senaryoları ve karşılık gelen ad çözümlemesi çözümleri gösterilmektedir:**

| **Senaryo** | **Çözüm** | **Son eki** |
| --- | --- | --- |
| Rol örnekleri veya VMs arasındaki ad çözümlemesi bulunan hello aynı bulut hizmeti ya da sanal ağ |[Azure tarafından sağlanan ad çözümlemesi](#azure-provided-name-resolution) |ana bilgisayar adı veya FQDN |
| Rol örnekleri veya farklı sanal ağlarda yer alan VM'ler arasında ad çözümleme |Müşteri tarafından yönetilen DNS sunucuları (DNS proxy) Azure tarafından çözümlemesi için sanal ağlar arasındaki sorguları iletme.  Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) |Yalnızca FQDN |
| Şirket içi bilgisayar hizmeti adları ve rol örnekleri veya azure'da VM çözümleme |Müşteri tarafından yönetilen DNS sunucuları (örneğin şirket içi etki alanı denetleyicisi, yerel salt okunur etki alanı denetleyicisi veya bölge aktarımları kullanarak eşitlenen bir DNS ikincil).  Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) |Yalnızca FQDN |
| Şirket içi bilgisayarlardan Azure ana bilgisayar adı çözümlemesi |İletme sorguları tooa müşteri tarafından yönetilen DNS proxy sunucusu hello karşılık gelen vnet hello proxy sunucusu çözümlemesi için sorguları tooAzure iletir. Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) |Yalnızca FQDN |
| İç IP'ler için ters DNS |[Kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) |yok |
| Sanal makineler veya sanal ağ içinde olmayan farklı bulut Hizmetleri bulunan rol örnekleri arasında ad çözümleme |Geçerli değil. VM'ler ve rol örnekleri farklı bulut hizmetleri arasında bağlantı sanal ağ dışında desteklenmiyor. |yok |

## <a name="azure-provided-name-resolution"></a>Azure tarafından sağlanan ad çözümlemesi
Genel DNS ad çözünürlüğü, birlikte bulunan rol örnekleri aynı sanal ağ veya Bulut hizmeti hello ve Azure VM'ler için dahili ad çözümlemesi sağlar.  VM'ler/örnekleri bir bulut hizmetinde aynı DNS (Merhaba ana bilgisayar adı tek başına yeterli olacak şekilde) soneki ancak hello FQDN gerekli tooresolve adları farklı bulut hizmetleri arasında olacak şekilde Klasik sanal ağlar farklı bulut Hizmetleri farklı DNS sonekleri hello paylaşır.  Sanal ağlar hello Resource Manager dağıtım modelinde hello DNS soneki (Merhaba FQDN gerekli olmadığı için) hello sanal ağ arasında tutarlıdır ve DNS adlarını tooboth NIC ve sanal makineleri atanabilir. Azure tarafından sağlanan ad çözümlemesi herhangi bir yapılandırma gerektirmez rağmen tüm dağıtım senaryoları için uygun seçim hello yukarıdaki hello tabloda görüldüğü gibi değil.

> [!NOTE]
> Web ve çalışan rolleri Hello durumda hello iç IP adreslerini hello Azure Hizmet Yönetimi REST API kullanarak hello rol adı ile örnek numarasını temel alan rol örneklerinin de erişebilirsiniz. Daha fazla bilgi için bkz: [Hizmet Yönetimi REST API Başvurusu](https://msdn.microsoft.com/library/azure/ee460799.aspx).
> 
> 

### <a name="features-and-considerations"></a>Özellikler ve ilgili önemli noktalar
**Özellikler:**

* Kullanım kolaylığı: hiçbir yapılandırma sipariş toouse Azure tarafından sağlanan ad çözümlemesi gereklidir.
* Hello Azure tarafından sağlanan ad çözümleme hizmeti yüksek oranda kullanılabilir, kaydetme, hello toocreate gerekir ve kendi DNS sunucularınızı kümelerini yönetme.
* Kendi DNS sunucuları tooresolve ile birlikte kullanılan şirket içi ve Azure ana bilgisayar adları.
* Aynı bulut hizmeti için bir FQDN gerek kalmadan rol örnekleri/VMs hello içinde arasındaki ad çözümlemesi sağlanır.
* Ad çözümlemesi hello FQDN için gerek kalmadan hello Resource Manager dağıtım modeli kullanan sanal ağları VM'ler arasında sağlanır. Merhaba Klasik dağıtım modelinde sanal ağlar farklı bulut Hizmetleri adları çözümlerken hello FQDN gerektirir. 
* Dağıtımlarınızı, en iyi şekilde açıklayan bir ana bilgisayar adları kullanabilirsiniz otomatik olarak oluşturulan adlarıyla çalışma yerine.

**Dikkate alınacak noktalar:**

* Merhaba oluşturulan Azure DNS soneki değiştirilemez.
* Kendi kayıtları el ile kaydettirilemedi.
* WINS ve NetBIOS desteklenmez. (Windows Gezgini'nde, VM'lerin göremiyorum.)
* Ana bilgisayar adları DNS uyumlu olması gerekir (yalnızca 0-9, a-z kullanmanız gerekir ve '-' ve başlayamaz veya bitemez bir '-'. RFC 3696 bölümüne 2 bakın.)
* DNS sorgu trafiğinin her VM için kısıtlanır. Bu, çoğu uygulamayı etkileyen döndürmemelidir.  İstek azaltma gözlenir, istemci tarafı önbelleğe alma etkin olduğundan emin olun.  Daha fazla ayrıntı için bkz: [hello sağlanan Azure name resolution çoğu alma](#Getting-the-most-from-Azure-provided-name-resolution).
* Merhaba ilk 180 bulut Hizmetleri'nde yalnızca VM'ler, her bir sanal ağı Klasik dağıtım modelinde kaydedilir. Bu, Resource Manager dağıtım modellerinde toovirtual ağlarda uygulanmaz.

### <a name="getting-hello-most-from-azure-provided-name-resolution"></a>Merhaba sağlanan Azure name resolution çoğu alma
**İstemci tarafı önbelleğe alma:**

Her DNS sorgusu hello ağ üzerinden gönderilen toobe gerekir.  İstemci tarafı önbelleğe alma gecikme süresini azaltmak ve yerel önbelleğinden yinelenen DNS sorgularını çözülerek esnekliği toonetwork blips geliştirilmesine yardımcı olur.  DNS kayıtlarını bir yaşam süresi (istemci tarafı önbelleğe alma çoğu durumlar için uygun olacak şekilde kayıt yenilik etkilemeden hello önbellek toostore hello kaydı mümkün olduğunca uzun bir süre tanıyan TTL) içerir.

Merhaba varsayılan Windows DNS istemcisi yerleşik bir DNS önbelleği sahiptir.  Varsayılan olarak önbelleğe alma distro'lar eklemeniz gerekmez, bazı Linux biri (olmadığından yerel bir önbellek zaten denetledikten sonra) tooeach Linux VM eklenmesi önerilir.

Bir dizi farklı DNS önbelleğe alma paketleri, örneğin dnsmasq vardır, hello en yaygın distro'lar üzerinde hello adımları tooinstall dnsmasq şunlardır:

* **Ubuntu (kullandığı resolvconf)**:
  * yalnızca hello dnsmasq paketini ("sudo get apt yükleme dnsmasq") yükleyin.
* **SUSE (kullandığı netconf)**:
  * Merhaba dnsmasq paketini ("sudo zypper yükleme dnsmasq") yükle 
  * Merhaba dnsmasq hizmeti ("systemctl etkinleştir dnsmasq.service") etkinleştir 
  * Merhaba dnsmasq hizmetini ("systemctl başlangıç dnsmasq.service") başlatın 
  * Düzenle "/ etc/sysconfig/ağ/config" NETCONFIG_DNS_FORWARDER değiştirip = "" çok "dnsmasq"
  * yerel DNS Çözümleyicisi hello gibi resolv.conf ("netconfig güncelleştirme") tooset hello önbelleğini güncelleştirin
* **OpenLogic (NetworkManager kullanır)**:
  * Merhaba dnsmasq paketini ("sudo yum yükleme dnsmasq") yükle
  * Merhaba dnsmasq hizmeti ("systemctl etkinleştir dnsmasq.service") etkinleştir
  * Merhaba dnsmasq hizmetini ("systemctl başlangıç dnsmasq.service") başlatın
  * "başına etki alanı adı sunucuları 127.0.0.1;" eklemek too"/etc/dhclient-eth0.conf"
  * Yerel DNS Çözümleyicisi hello gibi Hello ağ hizmeti ("service ağ restart") tooset hello önbelleği yeniden başlatın

> [!NOTE]
> Merhaba 'dnsmasq' paket yalnızca hello birçok DNS önbellekler için Linux biridir.  Kullanmadan önce lütfen kendi gereksinimlerinize uygunluğuna denetleyin ve başka bir önbellek yüklenir.
> 
> 

**İstemci tarafı yeniden deneme sayısı:**

DNS öncelikle bir UDP protokolüdür.  Merhaba UDP protokolünü ileti teslimi garanti etmez gibi yeniden deneme mantığı hello DNS protokolünde kendisini ele alınır.  Her DNS istemcisi (işletim sistemi) hello oluşturucuları tercih bağlı olarak farklı yeniden deneme mantığı sergilemesine:

* Windows işletim sistemlerinin 1 saniye ve daha sonra tekrar başka bir 2, 4 ve başka sonra 4 saniye yeniden deneyin. 
* Merhaba varsayılan Linux kurulumu yeniden denemelerden sonra 5 saniye.  Bu toochange bu tooretry 5 kez 1 ikinci aralıklarla önerilir.  

toocheck geçerli ayarlarına bir Linux VM 'kat /etc/resolv.conf' hello ve hello 'Seçenekler' satırında, örneğin bakın:

    options timeout:1 attempts:5

Merhaba resolv.conf dosyası genellikle otomatik olarak oluşturulan ve düzenlenmemelidir.  hello 'Seçenekler' satır eklemek için belirli adımlar hello distro göre farklılık gösterir:

* **Ubuntu** (resolvconf kullanır):
  * Başlangıç seçenekleri satır too'/etc/resolveconf/resolv.conf.d/head Ekle ' 
  * 'resolvconf -u' tooupdate çalıştırın
* **SUSE** (netconf kullanır):
  * 'timeout:1 denemeleri: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS Ekle = "" içinde '/ etc/sysconfig/ağ/config' parametresi 
  * 'netconfig Güncelleştirme' tooupdate çalıştırın
* **OpenLogic** (NetworkManager kullanır):
  * too'/etc/NetworkManager/dispatcher.d/11-dhclient 'Yankı "timeout:1 denemeleri: 5 Seçenekleri" ' Ekle ' 
  * 'hizmet ağ restart' tooupdate çalıştırın

## <a name="name-resolution-using-your-own-dns-server"></a>Kendi DNS sunucu kullanılarak ad çözümleme
Ad çözümleme gereksinimlerinizi Azure tarafından sağlanan örneğin ne zaman hello özelliklerini Active Directory etki alanları kullanarak Git veya sanal ağlar (vnet'ler) arasında DNS çözümlemesi gerektiğinde bir dizi durum vardır.  toocover bu senaryolar, Azure, kendi DNS sunucularınızı, toouse hello yeteneği sağlar.  

Bir sanal ağ içinde DNS sunucularına DNS sorguları tooAzure'nın özyinelemeli çözümleyiciler tooresolve ana bilgisayar adları bu sanal ağ içinde iletebilirsiniz.  Örneğin, Azure'da çalışan bir etki alanı denetleyicisi (DC), etki alanları için tooDNS sorguları yanıtlamak ve diğer tüm sorguları tooAzure iletebilir.  Bu sanal makineleri toosee sağlar (aracılığıyla hello DC) şirket içi kaynaklara ve Azure tarafından sağlanan ana bilgisayar adları (aracılığıyla hello ileticisi).  Erişim tooAzure'nın özyinelemeli çözümleyiciler hello sanal IP 168.63.129.16 sağlanır.

DNS iletme de ağlar arası vnet DNS çözümlemesi sağlar ve şirket içi makineler tooresolve Azure tarafından sağlanan ana bilgisayar adlarını sağlar.  İçinde bir sanal makinenin ana bilgisayar adı tooresolve sipariş, hello DNS sunucusu VM hello bulunması gerekir aynı sanal ağ ve yapılandırılmış tooforward hostname sorguları tooAzure olabilir.  Merhaba DNS soneki her bir vnet'teki farklı olarak, koşullu iletme kullanabilirsiniz toosend DNS sorguları toohello kuralları çözümlemesi için sanal ağ düzeltin.  Görüntü aşağıdaki hello iki sanal ağlar ve bu yöntemi kullanarak ağlar arası vnet DNS çözümlemesi yaparken bir şirket içi ağ gösterir.  Bir örnek DNS ileticisi hello kullanılabilir [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/301-dns-forwarder/) ve [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/301-dns-forwarder).

![Ağlar arası vnet DNS](./media/virtual-networks-name-resolution-for-vms-and-role-instances/inter-vnet-dns.png)

Azure tarafından sağlanan ad çözümlemesi, bir iç DNS soneki kullanırken (*. internal.cloudapp.net) DHCP kullanarak sağlanan tooeach VM.  Bu kayıtları hello internal.cloudapp.net bölgesinde bulunan hello ana bilgisayar adı olarak ana bilgisayar adı çözümlemesi sağlar.  Diğer DNS mimarileri (örneğin, etki alanına katılmış senaryoları) ile uğratan çünkü kendi ad çözümlemesi çözüm kullanırken IDN'ler soneki değil hello tooVMs sağlanan.  Bunun yerine bir çalışmayan yer tutucu (reddog.microsoft.com) sağlar.  

Gerekirse, PowerShell veya hello API kullanarak hello iç DNS soneki belirlenebilir:

* Resource Manager dağıtım modellerinde sanal ağlar için hello soneki hello kullanılabilir [ağ arabirim kartı](https://msdn.microsoft.com/library/azure/mt163668.aspx) kaynak veya hello aracılığıyla [Get-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619434.aspx) cmdlet'i.    
* Klasik dağıtım modellerinde hello soneki hello kullanılabilir [alma dağıtım API](https://msdn.microsoft.com/library/azure/ee460804.aspx) çağrısı veya hello aracılığıyla [Get-AzureVM-hata ayıklama](https://msdn.microsoft.com/library/azure/dn495236.aspx) cmdlet'i.

TooAzure gereksinimlerinize uygun olmayan sorguları iletme, kendi DNS çözüm tooprovide gerekir.  DNS çözüm gerekir:

* Uygun ana bilgisayar adı, örn aracılığıyla çözümlemesi [DDNS](virtual-networks-name-resolution-ddns.md).  Azure'nın DHCP kiralarını çok uzun ve atma DNS kaldırabilir toodisable DNS kaydı atmayı gerekebilir DDNS kullanarak erken kaydediyorsa unutmayın. 
* Dış etki alanı adlarının uygun özyinelemeli çözümleme tooallow çözümlemesi sağlar.
* Olması erişilebilir (TCP ve UDP bağlantı noktası 53) hizmet ve mümkün tooaccess olması hello istemcilerinden hello Internet.
* Güvenli hello erişimden karşı Internet, dış aracıları tarafından teşkil toomitigate tehditleri.

> [!NOTE]
> Azure VM'ler DNS sunucuları olarak kullanırken en iyi performans için IPv6 devre dışı bırakılması gerekir ve bir [örnek düzeyinde ortak IP](virtual-networks-instance-level-public-ip.md) tooeach DNS sunucusu VM atanmalıdır.  DNS sunucunuz olarak toouse Windows Server'ı seçerseniz [bu makalede](http://blogs.technet.com/b/networking/archive/2015/08/19/name-resolution-performance-of-a-recursive-windows-dns-server-2012-r2.aspx) ek Performans Analizi ve iyileştirmeler sağlar.
> 
> 

### <a name="specifying-dns-servers"></a>DNS sunucularını belirtme
Kendi DNS sunucularını kullanırken, Azure sanal ağ başına birden çok DNS sunucusu hello özelliği toospecify sağlar veya ağ başına (Resource Manager) arabirim / bulut hizmeti (Klasik).  Bir bulut hizmeti/ağ arabirimi için belirtilen DNS sunucularına öncelik hello sanal ağ için belirtilen üzerinden alın.

> [!NOTE]
> Ağ bağlantısı özellikleri, DNS sunucusu IP'leri, değil düzenlenmesi gerekir gibi doğrudan Windows VM bunlar hizmeti sırasında silinmesi gibi hello sanal ağ bağdaştırıcısı yerini, onarma. 
> 
> 

Merhaba Resource Manager dağıtım modelini kullanarak, DNS sunucuları hello Portal, API/şablonları belirtilebilir ([vnet](https://msdn.microsoft.com/library/azure/mt163661.aspx), [NIC](https://msdn.microsoft.com/library/azure/mt163668.aspx)) veya PowerShell ([vnet](https://msdn.microsoft.com/library/mt603657.aspx), [NIC](https://msdn.microsoft.com/library/mt619370.aspx)).

Merhaba sanal ağ içinde belirtilen için hello Klasik dağıtım modeli kullanılırken, DNS sunucuları Portal hello veya [hello *ağ yapılandırması* dosya](https://msdn.microsoft.com/library/azure/jj157100).  Bulut Hizmetleri için hello DNS sunucuları aracılığıyla belirtilen [hello *hizmet yapılandırmasını* dosya](https://msdn.microsoft.com/library/azure/ee758710) veya PowerShell ([New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)).

> [!NOTE]
> Merhaba zaten dağıtılmış bir sanal ağ/sanal makine için DNS ayarlarını değiştirirseniz, toorestart hello değişiklikleri tootake efekti için etkilenen her VM gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Resource Manager dağıtım modeli:

* [Bir sanal ağ oluştur veya güncelleştir](https://msdn.microsoft.com/library/azure/mt163661.aspx)
* [Bir ağ arabirimi kartı güncelle](https://msdn.microsoft.com/library/azure/mt163668.aspx)
* [Yeni-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx)
* [AzureRmNetworkInterface yeni](https://msdn.microsoft.com/library/mt619370.aspx)

Klasik dağıtım modeli:

* [Azure hizmet yapılandırma şeması](https://msdn.microsoft.com/library/azure/ee758710)
* [Sanal ağ yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100)
* [Bir ağ yapılandırma dosyası kullanarak bir sanal ağ yapılandırma](virtual-networks-using-network-configuration-file.md) 

