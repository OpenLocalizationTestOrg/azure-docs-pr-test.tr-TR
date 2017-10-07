---
title: aaaAzure DNS SSS | Microsoft Docs
description: "Azure DNS hakkında sık sorulan sorular"
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Azure DNS hakkında SSS

## <a name="about-azure-dns"></a>Azure DNS hakkında

### <a name="what-is-azure-dns"></a>Azure DNS nedir?

Merhaba etki alanı adı sistemi ya da DNS, çevirmek için sorumlu (veya çözme) bir Web sitesi veya hizmet name tooits IP adresi. Azure DNS barındırma için bir DNS etki alanı, Microsoft Azure altyapısı kullanılarak ad çözümlemesi sağlamanın hizmetidir. Azure etki alanlarınızı barındırarak DNS sunucunuzun yönetebilirsiniz kullanarak kayıtları, diğer Azure hizmetleriyle aynı kimlik bilgileri, API'leri, Araçlar ve faturalama hello.

Azure DNS'de DNS etki alanı, Azure'nın genel DNS ad sunucuları ağda barındırılır. Böylece her DNS sorgusu hello en yakın kullanılabilir DNS sunucusu tarafından yanıtlanan her noktaya yayın ağ kullanın. Bu, etki alanınız için yüksek kullanılabilirlik ve hızlı performans sağlar.

Hello Azure DNS hizmeti, Azure Resource Manager temel alır. Bu nedenle, rol tabanlı erişim denetimi, denetim günlüklerini ve kaynak kilitleme gibi Resource Manager özelliklerinden yararlanır. Etki alanları ve kayıtları hello Azure portal, Azure PowerShell cmdlet'leri, yönetilebilir ve platformlar arası Azure CLI hello. Otomatik DNS Yönetimi gerektiren uygulamalar hello hizmetiyle hello üzerinden REST API ve SDK'ları tümleştirebilirsiniz.

### <a name="how-much-does-azure-dns-cost"></a>Nasıl Azure DNS maliyeti nedir?

Hello Azure DNS faturalama modelini Azure DNS ve DNS sorgularının aldıkları hello sayısı barındırılan DNS bölgeleri hello sayısını temel alır. İndirim kullanımına dayalı sağlanır.

Daha fazla bilgi için bkz: Merhaba [Azure fiyatlandırma sayfası DNS](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Azure DNS için başlangıç SLA nedir?

Geçerli DNS isteklerine yanıt en az bir Azure DNS ad sunucusundan en az % 99,99 hello zaman alacağını garanti ediyoruz.

Daha fazla bilgi için bkz: Merhaba [Azure DNS SLA sayfa](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>'DNS bölgesini' nedir? Bunu hello aynı DNS etki alanı olarak mı? 

Bir etki örneğin "contoso.com" Merhaba etki alanı adı sistemi içinde benzersiz bir ad alanıdır.

Bir DNS bölgesi belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını ' dir. Örneğin, contoso.com' hello etki alanı' 'mail.contoso.com"(bir posta sunucusu) ve 'www.contoso.com' (bir web sitesi) gibi birçok DNS kayıtlarını içerebilir. Bu barındırılan hello DNS bölgesine "contoso.com".

Bir etki alanı adı *yalnızca bir adı*, buna karşın bir DNS bölgesi bir etki alanı adı için hello DNS kayıtlarını içeren bir veri kaynağı. Azure DNS toohost bir DNS bölgesi sağlar ve azure'de bir etki alanı için DNS kayıtlarını hello yönetin. Ayrıca DNS ad sunucuları hello Internet kaynaklı tooanswer DNS sorgularını sağlar.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>Bir DNS etki alanı adı toouse Azure DNS toopurchase gerekiyor mu? 

Olmayabilir.

Bir etki alanı toohost Azure DNS'de bir DNS bölgesi toopurchase gerekmez. Merhaba etki alanı adına sahip olmadan dilediğiniz zaman bir DNS bölgesi oluşturabilirsiniz. Bu bölge için DNS sorgularını yalnızca bunlar atanan toohello bölge toohello Azure DNS ad sunucuları yönlendirilir, çözer.

Hiyerarşiye hello Genel DNS – DNS gelen herhangi bir yere hello world toofind DNS bölgenizi sorgular ve DNS kayıtlarınızı yanıtlanması bu etkinleştirir DNS bölgenizi toolink istiyorsanız toopurchase hello etki alanı adı gerekir.

## <a name="azure-dns-features"></a>Azure DNS özellikleri

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Azure DNS, DNS tabanlı trafik yönlendirme veya uç nokta yük devretme destekliyor mu?

DNS tabanlı trafik yönlendirme ve uç nokta yük devretme Azure trafik Yöneticisi tarafından sağlanır. Azure DNS ile birlikte kullanılan ayrı bir Azure hizmet budur. Daha fazla bilgi için bkz: Merhaba [trafik Yöneticisi'ne genel bakış](../traffic-manager/traffic-manager-overview.md).

Azure DNS yalnızca destekler, her bir DNS sorgusu belirli bir DNS kaydı için her zaman alır hello 'static' DNS etki alanı, barındırma aynı DNS yanıtı.

### <a name="does-azure-dns-support-domain-name-registration"></a>Azure DNS etki alanı adı kayıt destekliyor mu?

Hayır. Azure DNS, etki alanı adlarını satın alma şu anda desteklemiyor. Toopurchase etki alanları istiyorsanız, bir üçüncü taraf etki alanı adı kayıt toouse gerekir. Merhaba Kaydedici genellikle küçük bir yıllık ücret ister. Merhaba etki alanları için DNS kayıtlarını Yönetimi sonra Azure DNS'de barındırılabilir. Bkz: [bir etki alanı tooAzure DNS temsilci](dns-domain-delegation.md) Ayrıntılar için.

Bu bizim biriktirme listesi üzerinde izlemekte olduğunuz bir özelliktir. Geri bildirim sitemizi kullanabileceğine[bu özellik için destek kaydetmek](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>Azure DNS 'özel' etki alanları destekliyor mu?

Hayır. Azure DNS yalnızca şu anda İnternete etki alanlarını destekler.

Bu bizim biriktirme listesi üzerinde izlemekte olduğunuz bir özelliktir. Geri bildirim sitemizi kullanabileceğine[bu özellik için destek kaydetmek](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Azure iç DNS seçenekleri hakkında daha fazla bilgi için bkz: [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>Azure DNS DNSSEC destekliyor mu?

Hayır. Azure DNS DNSSEC şu anda desteklemiyor.

Bu bizim biriktirme listesi üzerinde izlemekte olduğunuz bir özelliktir. Geri bildirim sitemizi kullanabileceğine[bu özellik için destek kaydetmek](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Azure DNS bölge aktarımları (AXFR/IXFR) destekliyor mu?

Hayır. Azure DNS bölge aktarımlarının şu anda desteklemiyor. DNS bölgelerini olabilir [Azure hello Azure CLI kullanarak DNS içeri](dns-import-export.md). DNS kayıtlarını sonra hello yönetilebilir [Azure DNS Yönetim Portalı](dns-operations-recordsets-portal.md), bizim [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet'leri](dns-operations-recordsets.md), veya [ CLI aracı](dns-operations-recordsets-cli.md).

Bu bizim biriktirme listesi üzerinde izlemekte olduğunuz bir özelliktir. Geri bildirim sitemizi kullanabileceğine[bu özellik için destek kaydetmek](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>Azure DNS URL yeniden yönlendirmeleri destekliyor mu?

Hayır. URL yeniden yönlendirme hizmetleri gerçekte bir DNS hizmeti olmayan - hello HTTP, yerine düzeyinde hello DNS düzeyi çalışırlar. Bazı DNS sağlayıcıları toobundle kendi genel teklifinin bir parçası olarak bir URL yeniden yönlendirme hizmeti. Bu Azure DNS tarafından şu anda desteklenmiyor.

Bu özellik bizim biriktirme listesi üzerinde izlenir. Geri bildirim sitemizi kullanabileceğine[bu özellik için destek kaydetmek](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Azure DNS kullanma

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Yapabilirim barındırmayı Azure DNS ve başka bir DNS sağlayıcısı kullanarak bir etki alanı?

Evet. Azure DNS diğer DNS Hizmetleri ile birlikte barındırma etki alanlarını destekler.

toodo toomodify hello NS kayıtları (hangi sağlayıcıları alma DNS denetleyen sorgular hello etki alanı için) hello etki alanı için gereken bu nedenle, her iki sağlayıcılarının toopoint toohello ad sunucuları. Bu NS kayıtlarını 3 yerlerde değiştiren toobe gerekir: Azure DNS'de, diğer sağlayıcı hello ve hello üst bölgesinde (genellikle hello etki alanı adı kayıt yapılandırılmış). DNS temsilcisi hakkında daha fazla bilgi için bkz: [DNS etki alanı temsilcisi](dns-domain-delegation.md).

Ayrıca, hello etki alanı için DNS kayıtlarını hello hem DNS sağlayıcılar arasında eşitleme tooensure gerekir. Azure DNS, DNS bölge aktarımları şu anda desteklemiyor. Ya da hello kullanarak toosynchronize DNS kayıtları gereksinim [Azure DNS Yönetim Portalı](dns-operations-recordsets-portal.md), bizim [REST API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell cmdlet'leri](dns-operations-recordsets.md) , veya [CLI aracı](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>Etki alanı tooall 4 Azure DNS ad Sunucularım toodelegate var mı?

Evet. Azure DNS 4 ad sunucuları hata Yalıtımı ve artan esneklik için tooeach DNS bölgesini atar. tooqualify için Azure DNS SLA Merhaba, etki alanı tooall 4 ad sunucuları toodelegate gerekir.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Azure DNS için hello kullanım sınırları nelerdir?

Azure DNS kullanarak varsayılan sınırları aşağıdaki hello uygulayın:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Bir Azure DNS bölgesi kaynak grupları arasında veya abonelikler arasında taşıyabilir miyim?

Evet. DNS bölgelerini kaynak grupları arasında veya abonelikler arasında taşınabilir.

Üzerinde etkisi yoktur DNS sorgularını bir DNS bölgesi taşırken. toohello bölge atanan hello ad sunucuları aynı ve DNS sorgularını boyunca normal olarak işlenen hello kalır.

Daha fazla bilgi ve yönergeler için bkz: toomove DNS bölgeleri [kaynakları tooa yeni kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Ne kadar süreyle için DNS değişiklikleri tootake efekti sürer?

Genellikle yeni DNS bölgeleri ve DNS kayıtlarını hello Azure DNS ad sunucuları üzerinde hızlı bir şekilde, birkaç saniye içinde yansıtılır.

Değişiklikleri tooexisting DNS kayıtlarını biraz uzun sürebilir ancak hello Azure DNS ad sunucuları üzerinde 60 saniye içinde hala yansıtılması. Bu durumda, DNS Azure DNS dışında (DNS istemcileri ve DNS özyinelemeli çözümleyiciler) önbelleğe alma de bir DNS değişiklik toobe için etkili geçen hello süre etkileyebilir. Bu önbellek süresi, her kayıt kümesinin hello yaşam süresi (TTL) özelliği kullanılarak denetlenebilir.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>My DNS bölgeleri yanlışlıkla silinmeye karşı nasıl koruyabilirim?

Azure DNS, Azure Resource Manager kullanılarak yönetilir ve avantajları hello gelen erişim denetimi özellikleri, Azure Resource Manager sağlar. Rol tabanlı erişim denetimi kullanılan toocontrol hangi kullanıcıların okuma veya yazma erişimi tooDNS bölgeleri ve kayıt kümelerini sahip olabilir. Kaynak kilitleri uygulanan tooprevent yanlışlıkla değiştirilmesini veya DNS bölgeleri ve kayıt kümelerini silinmesini olabilir.

Daha fazla bilgi için bkz: [koruma DNS bölgeleri ve kayıtları](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Azure DNS'de SPF kayıtlarının nasıl ayarlayabilirim?

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Bir uluslararası etki alanı adı (IDN) ayarlama Azure DNS'ye nasıl ayarlarım?

Uluslararası etki alanı adlarını (IDN'ler) iş her DNS adını kullanarak kodlayarak '[punycode](https://en.wikipedia.org/wiki/Punycode)'. DNS sorguları bu punycode kodlu adları kullanılarak yapılır.

Kayıt kümesi adı toopunycode veya ilk dönüştürme hello bölge adına göre Azure DNS'de uluslararası etki alanı adlarını (IDN'ler) yapılandırabilirsiniz. Azure DNS denetleyicisinden punycode yerleşik dönüştürme şu anda desteklemiyor.

## <a name="next-steps"></a>Sonraki adımlar

[Azure DNS hakkında daha fazla bilgi edinin](dns-overview.md)
<br>
[DNS bölgeleri ve kayıtlar hakkında daha fazla bilgi edinin](dns-zones-records.md)
<br>
[Azure DNS ile çalışmaya başlama](dns-getstarted-portal.md)

