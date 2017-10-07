---
title: "aaaDNS azure'daki Linux sanal makineleri için ad çözümleme seçenekleri"
description: "Ad çözümleme sağlanan senaryoları Azure Iaas dahil olmak üzere, Linux sanal makineler için DNS hizmetleri, karma dış DNS ve Getir bilgisayarınızı kendi DNS sunucusu."
services: virtual-machines
documentationcenter: na
author: RicksterCDN
manager: timlt
editor: tysonn
ms.assetid: 787a1e04-cebf-4122-a1b4-1fcf0a2bbf5f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/19/2016
ms.author: rclaus
ms.openlocfilehash: 7df2320b6f6b42b479bf4070ea60fe5770a78a41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dns-name-resolution-options-for-linux-virtual-machines-in-azure"></a>Linux sanal makinelerinin Azure DNS ad çözümlemesi seçenekleri
Azure DNS ad çözümlemesi tek bir sanal ağdaki tüm sanal makineler için varsayılan olarak sağlar. Azure barındıran sanal makinelerde kendi DNS hizmetleri yapılandırarak kendi DNS ad çözümlemesi çözüm uygulayabilirsiniz. Merhaba aşağıdaki senaryolarda durumunuz için çalışan hello seçmenize yardımcı olmalıdır.

* [Azure sağlar ad çözümlemesi](#azure-provided-name-resolution)
* [Kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server)

kullandığınız ad çözümlemesi Hello türünün nasıl sanal makineler ve rol örnekleri birbirleriyle toocommunicate gereksinimlerine göre değişir.

Merhaba aşağıdaki tabloda senaryoları ve karşılık gelen ad çözümlemesi çözümleri gösterilmektedir:

| **Senaryo** | **Çözüm** | **Son eki** |
| --- | --- | --- |
| Ad çözümlemesi rol örnekleri veya hello içindeki sanal makineler arasında aynı sanal ağ |[Azure sağlar ad çözümlemesi](#azure-provided-name-resolution) |ana bilgisayar adı veya tam etki alanı adı (FQDN) |
| Rol örnekleri veya sanal makineleri farklı sanal ağlar arasındaki ad çözümlemesi |Sorguları Azure (DNS proxy) tarafından çözümlemesi için sanal ağlar arasında iletecek müşteri tarafından yönetilen DNS sunucuları. Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server). |Yalnızca FQDN |
| Şirket içi bilgisayarları ve rol örnekleri ya da sanal makineleri Azure hizmet adlarından çözümleme |Müşteri tarafından yönetilen DNS sunucuları (örneğin, şirket içi etki alanı denetleyicisi, yerel salt okunur etki alanı denetleyicisi veya bölge aktarımları kullanarak eşitlenen bir DNS ikincil). Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server). |Yalnızca FQDN |
| Şirket içi bilgisayarlardan Azure ana bilgisayar adı çözümlemesi |Sorguları tooa müşteri tarafından yönetilen DNS proxy sunucusu hello karşılık gelen sanal ağ iletin. Merhaba proxy sunucusu çözümlemesi için sorguları tooAzure iletir. Bkz: [kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server). |Yalnızca FQDN |
| İç IP'ler için ters DNS |[Kendi DNS sunucu kullanılarak ad çözümleme](#name-resolution-using-your-own-dns-server) |yok |

## <a name="name-resolution-that-azure-provides"></a>Azure sağlar ad çözümlemesi
Genel DNS ad çözünürlüğü, birlikte aynı sanal ağda bulunan rol örnekleri hello ve Azure sanal makineler için dahili ad çözümlemesi sağlar. Azure Resource Manager tabanlı sanal ağlarda hello DNS soneki hello sanal ağ arasında tutarlıdır; Merhaba FQDN gerekli değildir. DNS adları tooboth ağ arabirimi kartları (NIC) ve sanal makinelere atanabilir. Azure sağlar hello ad çözümlemesi herhangi bir yapılandırma gerektirmez rağmen tüm dağıtım senaryoları için uygun seçim hello tablo önceki hello üzerinde görülen değil.

### <a name="features-and-considerations"></a>Özellikler ve ilgili önemli noktalar
**Özellikler:**

* Hiçbir Azure sağlar gerekli toouse ad çözümlemesi yapılandırmadır.
* Azure sağlar hello ad çözümleme hizmeti yüksek oranda kullanılabilir. Toocreate ihtiyacınız yoksa ve kendi DNS sunucularınızı kümelerini yönetme.
* Azure sağlar hello ad çözümleme hizmeti, kendi DNS sunucuları tooresolve birlikte kullanılabilir hem şirket içi hem de Azure ana bilgisayar adları.
* Ad çözümlemesi hello FQDN için gerek kalmadan sanal ağlardaki sanal makineler arasında sağlanır.
* Dağıtımlarınızı en iyi şekilde açıklayan bir ana bilgisayar adları kullanabilirsiniz otomatik olarak oluşturulan adlarıyla çalışma yerine.

**Dikkate alınacak noktalar:**

* Azure oluşturduğu hello DNS soneki değiştirilemez.
* Kendi kayıtları el ile kaydettirilemedi.
* WINS ve NetBIOS desteklenmez.
* Ana bilgisayar adları DNS uyumlu olması gerekir.
    Adları, yalnızca 0-9, a-z, kullanmalıdır ve '-', ve başlayamaz veya bitemez bir '-'. RFC 3696 bölüm 2 bakın.
* DNS sorgu trafiğinin her sanal makine için kısıtlanır. Azaltma uygulamaların çoğu etkisi döndürmemelidir.  İstek azaltma gözlenir, istemci tarafı önbelleğe alma etkin olduğundan emin olun.  Daha fazla bilgi için bkz: [hello sağlayan Azure name resolution çoğu alma](#getting-the-most-from-name-resolution-that-azure-provides).

### <a name="getting-hello-most-from-name-resolution-that-azure-provides"></a>Merhaba sağlayan Azure name resolution çoğu alma
**İstemci tarafı önbelleğe alma:**

Bazı DNS sorgularını hello ağ üzerinden gönderilmez. İstemci tarafı önbelleğe alma gecikme süresini azaltmak ve yerel önbelleğinden yinelenen DNS sorgularını çözülerek esnekliği toonetwork tutarsızlıklar geliştirilmesine yardımcı olur. Bir yaşam süresi (kayıt yenilik etkilemeden hello önbellek toostore hello kaydı mümkün olduğunca uzun bir süre tanıyan TTL), DNS kayıtlarını içerir. Sonuç olarak, istemci tarafı önbelleğe alma çoğu durumlar için uygundur.

Bazı Linux dağıtımları varsayılan önbelleğe alma dahil etmeyin. Önbellek tooeach Linux sanal makine olmadığından yerel bir önbellek zaten denetledikten sonra eklemenizi öneririz.

Birkaç farklı DNS dnsmasq gibi paketleri önbelleğe alma kullanılabilir. Merhaba en yaygın dağıtımları hello adımları tooinstall dnsmasq şunlardır:

**Ubuntu (kullandığı resolvconf)**
  * Merhaba dnsmasq paketini ("sudo get apt yükleme dnsmasq") yükleyin.

**SUSE (kullandığı netconf)**:
1. Merhaba dnsmasq paketini ("sudo zypper yükleme dnsmasq") yükleyin.
2. Merhaba dnsmasq hizmetini ("systemctl etkinleştir dnsmasq.service") etkinleştirin.
3. Merhaba dnsmasq hizmetini ("systemctl başlangıç dnsmasq.service") başlatın.
4. Düzenle "/ etc/sysconfig/ağ/config" NETCONFIG_DNS_FORWARDER değiştirip = "" çok "dnsmasq".
5. Yerel DNS Çözümleyicisi hello gibi resolv.conf ("netconfig güncelleştirme") tooset hello önbelleğini güncelleştirin.

**CentOS yanlış Wave yazılımlar (önceki adıyla OpenLogic; NetworkManager kullanır)**
1. Merhaba dnsmasq paketini ("sudo yum yükleme dnsmasq") yükleyin.
2. Merhaba dnsmasq hizmetini ("systemctl etkinleştir dnsmasq.service") etkinleştirin.
3. Merhaba dnsmasq hizmetini ("systemctl başlangıç dnsmasq.service") başlatın.
4. "Başına etki alanı adı sunucuları 127.0.0.1;" eklemek too"/etc/dhclient-eth0.conf".
5. Yerel DNS Çözümleyicisi hello gibi Hello ağ hizmeti ("service ağ restart") tooset hello önbelleği yeniden başlatın

> [!NOTE]
> : hello 'dnsmasq' paketidir Linux için kullanılabilir olan birçok DNS önbelleğe hello yalnızca biri. Kullanmadan önce kendi uygunluğu gereksinimleriniz için denetleyin ve başka bir önbellek yüklü.
>
>

**İstemci tarafı yeniden deneme**

DNS öncelikle bir UDP protokolüdür. Merhaba UDP protokolünü ileti teslimi garanti etmez çünkü hello DNS protokolü kendisini yeniden deneme mantığı işler. Her DNS istemcisi (işletim sistemi) hello oluşturanın tercih bağlı olarak farklı yeniden deneme mantığı sergilemesine:

* Windows işletim sistemlerinin bir sonra ikinci ve daha sonra tekrar başka sonra iki, dört ve başka bir dört saniye yeniden deneyin.
* Merhaba varsayılan Linux kurulumu yeniden denemelerden sonra beş saniyede.  Beş kez bir saniyelik aralıklarla bu tooretry değiştirmeniz gerekir.  

toocheck geçerli ayarları bir Linux sanal makinede, 'kat /etc/resolv.conf' hello ve hello 'Seçenekler' satırında, örneğin bakın:

    options timeout:1 attempts:5

Merhaba resolv.conf dosyası otomatik olarak oluşturulan ve düzenlenmemelidir. 'hello seçenekler satır farklılık göre dağıtım' eklemek belirli adımlar hello:

**Ubuntu** (resolvconf kullanır)
1. Başlangıç seçenekleri satır too'/etc/resolveconf/resolv.conf.d/head Ekle '.
2. 'Resolvconf -u' tooupdate çalıştırın.

**SUSE** (netconf kullanır)
1. 'Timeout:1 denemeleri: 5' toohello NETCONFIG_DNS_RESOLVER_OPTIONS Ekle = "" içinde '/ etc/sysconfig/ağ/config' parametresi.
2. 'Netconfig Güncelleştirme' tooupdate çalıştırın.

**CentOS yanlış Wave yazılımı (önceki adıyla OpenLogic) tarafından** (NetworkManager kullanır)
1. Too'/etc/NetworkManager/dispatcher.d/11-dhclient 'Yankı "timeout:1 denemeleri: 5 Seçenekleri" ' Ekle '.
2. 'Hizmet ağ restart' tooupdate çalıştırın.

## <a name="name-resolution-using-your-own-dns-server"></a>Kendi DNS sunucu kullanılarak ad çözümleme
Ad çözümleme gereksinimlerinizi Azure sağladığı hello özellikleri gidebilir. Örneğin, DNS çözümlemesi sanal ağlar arasında gerektirebilir. toocover bu senaryo, kendi DNS sunucuları kullanabilirsiniz.  

Aynı sanal ağda bulunan sanal ağ can toorecursive çözümleyiciler Azure tooresolve ana bilgisayar adları, ileriye doğru DNS sorguları içinde DNS sunucuları hello. Örneğin, Azure'da çalışan bir DNS sunucusu, kendi DNS tooDNS sorgularında dosyaları bölge ve diğer tüm sorguları tooAzure iletmek yanıt verebilir. Bu işlev sanal makineleri toosee hem girişlerinizi (Merhaba ileticisi) Azure sağlayan bir ana bilgisayar adları ve bölge dosyaları sağlar. Erişim toohello özyinelemeli çözümleyiciler Azure hello sanal IP 168.63.129.16 sağlanır.

DNS iletme aynı zamanda sanal ağlar arasında DNS çözümlemesi sağlar ve Azure sağlayan, şirket içi makineler tooresolve ana bilgisayar adlarını sağlar. tooresolve hello DNS sunucusu sanal makinesi bir sanal makinenin ana bilgisayar adı, bulunmalıdır hello aynı sanal ağ ve yapılandırılmış tooforward hostname sorguları tooAzure olabilir. Merhaba DNS soneki her sanal ağ farklı olduğundan, koşullu iletme kullanabilirsiniz toosend DNS sorguları toohello kuralları çözümlemesi için sanal ağ düzeltin. Merhaba aşağıdaki görüntü iki sanal ağ ve DNS çözümlemesi bu yöntemi kullanarak sanal ağlar arasında bulunurken bir şirket içi ağ göstermektedir:

![Sanal ağlar arasında DNS çözümlemesi](./media/azure-dns/inter-vnet-dns.png)

Azure sağlar ad çözümlemesi kullandığınızda, hello iç DNS soneki DHCP kullanarak tooeach sanal makine sağlanır. Kendi ad çözümlemesi çözümünü kullandığınızda, diğer DNS mimarileri ile Merhaba soneki uğratan çünkü bu soneki sağlanan toovirtual makineler değil. sanal makinelerinizi FQDN veya tooconfigure hello ekini tarafından toorefer toomachines, PowerShell veya hello API toodetermine hello soneki kullanabilirsiniz:

* Azure Resource Manager tarafından yönetilen sanal ağlar için hello soneki hello kullanılabilir [ağ arabirim kartı](https://msdn.microsoft.com/library/azure/mt163668.aspx) kaynak. Merhaba de çalıştırabilirsiniz `azure network public-ip show <resource group> <pip name>` toodisplay hello içerir, genel IP ayrıntılarını hello hello NIC FQDN'sini komutu

TooAzure gereksinimlerinize uygun olmayan sorguları iletme, kendi DNS çözüm tooprovide gerekir.  DNS çözüm gerekir:

* Uygun ana bilgisayar adı çözümlemesi, örneğin aracılığıyla sağlamak [DDNS](../../virtual-network/virtual-networks-name-resolution-ddns.md). DDNS kullanırsanız, toodisable DNS kaydı atmayı gerekebilir. DHCP kiralarını Azure çok uzun ve atma DNS kayıtlarını erken kaldırabilirsiniz.
* Dış etki alanı adlarının uygun özyinelemeli çözümleme tooallow çözümlemesi sağlar.
* Erişilebilir (TCP ve UDP bağlantı noktası 53), hizmet verdiği hello istemcilerden olması ve mümkün tooaccess hello Internet olmalıdır.
* Dış aracıları tarafından teşkil hello Internet toomitigate tehditlerinden erişime karşı korunması.

> [!NOTE]
> En iyi performans için sanal makineleri Azure DNS sunucularının kullandığınızda, IPv6 devre dışı bırakın ve ata bir [örnek düzeyinde ortak IP](../../virtual-network/virtual-networks-instance-level-public-ip.md) tooeach DNS sunucusu sanal makine.  
>
>
