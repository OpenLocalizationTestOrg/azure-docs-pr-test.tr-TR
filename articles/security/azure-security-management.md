---
title: "aaaEnhance uzaktan yönetim güvenliği | Microsoft Docs"
description: "Bu makalede bulut hizmetleri, Sanal Makineler ve özel uygulamalar dahil, Microsoft Azure ortamlarını yönetirken uzaktan yönetim güvenliğini geliştirme adımları açıklanmaktadır."
services: security
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: TomSh
ms.assetid: 2431feba-3364-4a63-8e66-858926061dd3
ms.service: security
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 9262cfb98bfe51d15fbad8f18997c4573668d9ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security-management-in-azure"></a>Azure’da Güvenlik Yönetimi
Azure aboneleri yönetim iş istasyonları, geliştirici PC’leri ve hatta göreve özel izinleri bulunan ayrıcalıklı son kullanıcı cihazları dahil birden fazla cihazda kendi bulut ortamlarını yönetebilir. Bazı durumlarda, yönetim işlevleri hello gibi web tabanlı konsollar aracılığıyla gerçekleştirilir [Azure portal](https://azure.microsoft.com/features/azure-portal/). Diğer durumlarda, olabilir doğrudan bağlantılar tooAzure şirket içi sistemlerden sanal özel ağlar (VPN), Terminal Hizmetleri, istemci uygulaması protokolleri veya hello Azure Hizmet Yönetimi API'si (SMAPI) (programlı olarak). Ayrıca, istemci uç noktaları ya da etki alanına katılmış veya yalıtılmış ve yönetilmeyen olabilir, tabletler veya akıllı telefonlar gibi.

Birden çok erişim ve yönetim özellikleri zengin bir seçenek kümesi sunmasına karşın, bu değişkenlik önemli riski tooa bulut dağıtımı ekleyebilirsiniz. Zor toomanage olabilir izleme ve denetim yönetim eylemlerini. Ayrıca bu değişkenlik bulut hizmetlerini yönetmek için kullanılan tooclient uç düzenlenmemiş erişim aracılığıyla güvenlik tehditlerine neden olabilir. Altyapı geliştirme ve yönetme amacıyla genel ya da kişisel iş istasyonlarını kullanmak, web’e gözatma (örneğin, su kaynağı saldırıları) ya da e-posta (örneğin, sosyal mühendislik ve kimlik avı) gibi öngörülemeyen tehdit vektörlerini açar.

![][1]

Merhaba saldırıları için olası zor tooconstruct güvenlik ilkeleri ve mekanizmaları tooappropriately değişken uç noktalardan erişim tooAzure arabirimlerine (SMAPI gibi) yönetme olduğundan bu ortam türünü artırır.

### <a name="remote-management-threats"></a>Uzaktan yönetim tehditleri
Saldırganlar genellikle hesap kimlik bilgilerini (örneğin, parolanıza deneme yanılma yapma, kimlik avı ve aracılığıyla kimlik bilgisi toplama) tehlikeye ya da kullanıcıları zararlı kod (örneğin, zararlı Web sitelerinden ile kullanmak üzere kandırarak toogain ayrıcalıklı erişim girişiminde sürücü tarafından yükler veya zararlı e-posta eklerinden). Uzaktan yönetilen bulut ortamında, hesap ihlallerini tooan açabilir risk artan son tooanywhere, her zaman erişim.

Sıkı denetimlerle dahi birincil yönetici hesaplarında, alt düzey kullanıcı hesapları birinin güvenlik stratejisindeki içinde kullanılan tooexploit zayıf olabilir. Uygun güvenlik eğitimi olmaması da yanlışlıkla açıklanması veya ortaya çıkması hesap bilgilerinin aracılığıyla toobreaches yol açabilir.

Bir kullanıcı iş istasyonu yönetim görevleri için kullanıldığında, birçok farklı noktada tehlikeye girebilir. Bir kullanıcı olup hello Web'e gözatma, 3. taraf ve açık kaynaklı Araçları'nı kullanarak veya Truva atı içeren zararlı bir belge dosyasını açma.

Genel olarak, veri ihlalleriyle sonucu olabilir çoğu hedefli saldırı toobrowser açıkları, eklenti (örneğin, Flash, PDF, Java) ve kimlik avı (e-posta) Masaüstü makinelerde izlenen. Bu makineler yönetici düzeyi olabilir veya hizmet düzeyi izinlere tooaccess sunucuları Canlı veya ağ aygıtları geliştirme veya diğer varlıklar için kullanıldığında işlemleri için.

### <a name="operational-security-fundamentals"></a>İşlem güvenliği temelleri
Daha güvenli yönetim ve işlemler için hello olası giriş noktası sayısını azaltarak istemcinin saldırı yüzeyini en aza indirebilirsiniz. Bu, güvenlik ilkeleri aracılığıyla yapılabilir: “görevler ayrımı” ve “ortamların ayrımı”.

Bir düzeyde hata tooa ihlali başka bir programda müşteri adayları, birbirine toodecrease hello olasılığını hassas işlevleri yalıtma. Örnekler:

* Yönetim görevleri tooa güvenliğinin aşılmasına (örneğin, kötü amaçlı yazılımın altyapı sunucusuna bulaşması yöneticinin e-posta) yol açabilecek etkinliklerle birleştirilmemelidir.
* Yüksek duyarlılık işlemleri için kullanılan bir iş istasyonu aynı sistem gözatma hello Internet gibi yüksek riskli amacıyla kullanılan hello olmamalıdır.

Gereksiz yazılımları kaldırarak Hello sistemin saldırı yüzeyini azaltın. Örnek:

* Merhaba cihazın ana amacı toomanage bulut Hizmetleri ise standart yönetim, destek ya da geliştirme iş istasyonu bir e-posta istemcisi ya da diğer üretim uygulamalarının yüklenmesini gerektirmemelidir.

Yönetici erişim tooinfrastructure bileşenleri olmalıdır sahip istemci sistemleri toohello sıkı olası ilkelere tooreduce güvenlik riskleri tabi. Örnekler:

* Güvenlik ilkeleri hello cihaz ve kısıtlayıcı güvenlik duvarı yapılandırması kullanımını açık Internet erişimini reddeden Grup İlkesi ayarları dahil edebilirsiniz.
* Doğrudan erişim gerekiyorsa, Internet Protokolü Güvenliği (IPsec) VPN’leri kullanın.
* Ayır yönetim ve geliştirme Active Directory etki alanları yapılandırın.
* Yönetim iş istasyonu ağ trafiğini yalıtın ve filtreleyin.
* Kötü amaçlı yazılımdan korunma yazılımı kullanın.
* Çok faktörlü kimlik doğrulaması tooreduce hello çalınan kimlik bilgileri riskini uygulayın.

Erişim kaynaklarını sağlamlaştırmak ve yönetilmeyen uç noktaları ortadan kaldırmak da yönetim görevlerini kolaylaştırır.

### <a name="providing-security-for-azure-remote-management"></a>Azure remote management için güvenlik sağlama
Azure, Azure bulut Hizmetleri ve sanal makineleri yöneten mekanizmaları tooaid Yöneticiler güvenlik sağlar. Bu mekanizmalar şunları:

* Kimlik doğrulama ve [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).
* İzleme, günlük kaydı ve denetim.
* Sertifikalar ve şifreli iletişim.
* Web yönetim portalı.
* Ağ paketi filtreleme.

İstemci tarafı güvenlik yapılandırması ve veri merkezi dağıtımının Yönetimi ağ geçidi ile olası toorestrict ve İzleyici yönetici erişimi toocloud uygulamaları ve verileri sağlanır.

> [!NOTE]
> Bu makaledeki bazı öneriler artan veri, ağ ya da işlem kaynağı kullanımına neden olabilir ve lisans ya da abonelik maliyetlerinizi artırabilir.
>
>

## <a name="hardened-workstation-for-management"></a>Yönetim için sağlamlaştırılmış iş istasyonu
bir iş istasyonunu sağlamlaştırmanın hello hedeftir tooeliminate tüm ancak hello en kritik işlevler için gerekli hello olası saldırı yüzeyini mümkün olduğunca küçülterek toooperate. Sistem sağlamlaştırma, yüklü hizmetler ve uygulamalar, ağ erişim tooonly gerekenleri, kısıtlama, uygulama yürütmeyi sınırlama hello sayısını en aza indirir ve her zaman toodate hello sistemi tutma içerir. Ayrıca, yönetim için sağlamlaştırılmış bir iş istasyonu kullanmak yönetim araçlarını ve etkinlikleri diğer son kullanıcı görevlerinden ayırır.

Bir şirket içi Kurumsal ortamda hello ayrılmış yönetim ağları, kart erişimli sunucu odaları ve korumalı alanlarının hello ağ üzerinde çalıştırılan iş istasyonları aracılığıyla fiziksel altyapınızın saldırı yüzeyini sınırlayabilirsiniz. Bulut veya karma BT modelinde, güvenli Yönetim Hizmetleri hakkında dikkatli olmak hello tooIT kaynaklarına fiziksel erişim eksiği nedeniyle daha karmaşık olabilir. Koruma çözümleri uygulamak dikkatli yazılım yapılandırma, güvenlik odaklı işlemler ve kapsamlı ilkeler gerektirir.

En az ayrıcalıklı minimuma indirilmiş yazılım ayak izini kilitli bir iş istasyonu için bulut Yönetimi'ni kullanarak — ve uygulama geliştirme için — hello uzaktan yönetim ve geliştirme ortamlarını standart hale getirerek güvenlik olayları hello riskini azaltabilir. Sağlamlaştırılmış bir istasyonu yapılandırması kötü amaçlı yazılım ve açıklar tarafından kullanılan birçok ortak yolu kapatarak kritik bulut kaynaklarını kullanılan toomanage olan hesaplarının hello güvenliğinin aşılmasına önlenmesine yardımcı olabilir. Özellikle, kullanabilir [Windows AppLocker](http://technet.microsoft.com/library/dd759117.aspx) ve Hyper-V teknolojisi toocontrol yalıtmak istemci sistemi davranışlarını ve e-posta veya Internet'e gözatma dahil olmak üzere tehditleri azaltmak.

Sağlamlaştırılmış bir iş istasyonunda hello yönetici (yönetici düzeyi yürütmeyi engelleyen) bir standart kullanıcı hesabı çalıştırır ve ilişkili uygulamalar bir izin listesi tarafından denetlenir. Merhaba sağlamlaştırılmış iş istasyonunun temel öğeleri aşağıdaki gibidir:

* Etkin tarama ve düzeltme eki uygulama. Kötü amaçlı yazılımdan koruma yazılımı dağıtın, normal güvenlik açığı taramaları gerçekleştirin ve hello en son güvenlik güncelleştirmesini vakitli şekilde kullanarak tüm iş istasyonlarını güncelleştirin.
* Sınırlı işlev. Gerekli olmayan uygulamaları kaldırın ve gereksiz hizmetleri (başlangıç) devre dışı bırakın.
* Ağ sağlamlaştırma. Windows Güvenlik duvarı kuralları tooallow yalnızca geçerli IP adresleri, bağlantı noktaları ve URL'leri ilgili tooAzure Yönetimi kullanın. Bu gelen uzak bağlantılara toohello iş istasyonu da engellenen emin olun.
* Yürütme kısıtlama. Yönetim toorun için gerekli olan önceden tanımlanmış yürütülebilir dosyalar yalnızca bir dizi izin ver (tooas "varsayılan ret" denir). Varsayılan olarak, kullanıcıların izni reddedilmelidir program tüm hello açıkça tanımlanmış sürece toorun izin listesinde.
* En düşük öncelik. Yönetim iş istasyonu kullanıcıları hello yerel makinenin kendisinde yönetim ayrıcalıklarına sahip olmamalıdır. Bu şekilde hello sistem yapılandırmasını veya hello sistem dosyalarını, kasıtlı veya kasıtsız olarak değiştiremezler.

Tüm bu kullanarak yaptırmak [Grup İlkesi nesneleri](https://www.microsoft.com/download/details.aspx?id=2612) (GPO'lar) Active Directory etki alanı Hizmetleri (AD DS) ve (yerel) yönetim etki alanı tooall yönetim hesaplarınızı uygulama.

### <a name="managing-services-applications-and-data"></a>Hizmetleri, uygulamaları ve verileri yönetme
Azure cloud services yapılandırması hello Azure portal ya da SMAPI üzerinden hello Windows PowerShell komut satırı arabirimi veya bu RESTful arabirimlerinden yararlanan özel olarak geliştirilmiş bir uygulama aracılığıyla gerçekleştirilir. Bu mekanizmaları kullanan hizmetler Azure Active Directory (Azure AD), Azure Storage, Azure Websites ve Azure Virtual Network’ü içerir.

Sanal makine – dağıtılmış uygulamalar kendi istemci araçlarını ve hello Microsoft Yönetim Konsolu (MMC), kurumsal bir Yönetim Konsolu (örneğin, Microsoft System Center veya Windows Intune) veya başka bir yönetim gibi gerektiği gibi arabirimleri sağlar uygulama — Microsoft SQL Server Management Studio, örneğin. Bu araçlar, genellikle bir kurumsal ortamda veya istemci ağında bulunur. Bunlar, doğrudan, durum bilgisi olan bağlantılar gerektiren, Uzak Masaüstü Protokolü (RDP) gibi belirli ağ protokollerine bağlı olabilir. Bazıları açık yayımlanmaması ya hello Internet üzerinden erişilebilir olmaması web etkin arabirimlere sahip olabilir.

Kullanarak Azure erişim tooinfrastructure ve platform Hizmetleri Yönetimi kısıtlayabilirsiniz [çok faktörlü kimlik doğrulaması](../multi-factor-authentication/multi-factor-authentication.md), [X.509 yönetim sertifikaları](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/)ve güvenlik duvarı kuralları. Hello Azure portal ve SMAPI Aktarım Katmanı Güvenliği (TLS) gerektirir. Ancak, hizmetler ve Azure'a dağıttığınız uygulamalar uygulamanıza dayalı uygun koruma önlemleri tootake gerektirir. Bu mekanizmalar standart sağlamlaştırılmış iş istasyonu konfigürasyonuyla sık sık daha kolay etkinleştirilebilir.

### <a name="management-gateway"></a>Yönetimi ağ geçidi
tüm yönetim toocentralize erişmek ve izleme ve günlüğe kaydetme kolaylaştırmak için ayrılmış bir dağıtabilirsiniz [Uzak Masaüstü Ağ Geçidi](https://technet.microsoft.com/library/dd560672) (RD Ağ Geçidi) sunucusu şirket içi ağ, bağlı tooyour Azure ortamı.

Uzak Masaüstü Ağ geçidi, güvenlik gereksinimlerini uygulayan ilke tabanlı bir RDP proxy hizmetidir. Windows Server Network Access Protection ile RD Ağ Geçidi uygulamak yalnızca Active Directory Etki Alanı Hizmetleri (AD DS) Grup İlkesi Nesneleri (GPO'lar) tarafından oluşturulan belirli güvenlik durumu ölçütlerini karşılayan istemcilerin bağlanabilmesinin sağlanmasına yardımcı olur. Buna ek olarak:

* Sağlama bir [Azure yönetim sertifikası](http://msdn.microsoft.com/library/azure/gg551722.aspx) izin hello yalnızca ana bilgisayar olmasını hello RD Ağ Geçidi üzerinde Azure portal tooaccess hello.
* Merhaba RD Ağ Geçidi toohello katılma aynı [Yönetim etki alanı](http://technet.microsoft.com/library/bb727085.aspx) yönetici iş istasyonları hello gibi. Tek yönlü güven tooAzure AD sahip bir etki alanı içinde bir siteden siteye IPSec VPN ya da ExpressRoute kullanırken ya da şirket içi arasında Kimlik federasyonunu bu gereklidir AD DS örneği ve Azure AD.
* Yapılandırma bir [istemci bağlantısı yetkilendirme ilkesi](http://technet.microsoft.com/library/cc753324.aspx) toolet hello RD Ağ Geçidi hello istemci makine adıdır, (geçerli etki alanına katılmış) ve izin verilen tooaccess hello Azure portal doğrulayın.
* İçin IPSec kullanın [Azure VPN](https://azure.microsoft.com/documentation/services/vpn-gateway/) toofurther yönetim trafiğini İleri gizli dinleme ve belirteç hırsızlığından korumak veya aracılığıyla yalıtılmış bir Internet bağlantısını dikkate [Azure ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).
* RD Ağ Geçidi üzerinden oturum açan yöneticiler için multi-factor authentication ([Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md) aracılığıyla) ya da akıllı kart kimlik doğrulamasını etkinleştirin.
* Kaynak yapılandırma [IP adresi sınırlamaları](http://azure.microsoft.com/blog/2013/08/27/confirming-dynamic-ip-address-restrictions-in-windows-azure-web-sites/) veya [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md) Azure toominimize hello sayısı izin verilen yönetim uç noktalar olarak.

## <a name="security-guidelines"></a>Güvenlik yönergeleri
Genel olarak, tüm şirket için kullanılan benzer toohello yöntemler hello bulut ile kullanmak için toosecure yönetici iş istasyonları yardımcı — Örneğin, yapı ve kısıtlayıcı izinler simge durumuna küçültülmüş. Bulut Yönetimi bazı benzersiz yönleri şunlardır: daha akin tooremote ya da bant dışı kuruluş yönetimi. Bunlar hello kullanın ve kimlik bilgileri, uzaktan erişim, Gelişmiş Güvenlik ve tehdit algılama ve yanıt denetimini içerir.

### <a name="authentication"></a>Kimlik Doğrulaması
Denetim erişim isteklerine ve Yönetimsel Araçlar erişmek için Azure oturum açma kısıtlamaları tooconstrain kaynak IP adresleri kullanın. toohelp Azure tanımlamak SMAPI (üzerinden Windows PowerShell cmdlet'leri gibi müşteri tarafından geliştirilen Araçlar) ve hello Azure portal toorequire istemci-tarafı yönetim sertifikaları toobe yapılandırabilirsiniz yönetim istemcilerini (iş istasyonları ve/veya uygulamalar), yüklü, ayrıca tooSSL sertifikalar. Yönetici erişiminin multi-factor authentication gerektirmesine de öneriyoruz.

Azure’a dağıttığınız bazı uygulamalar veya hizmetler hem son kullanıcı hem de yönetici erişimi için kendi kimlik doğrulama mekanizmalarına sahip olabilirken, diğerleri Azure AD’den faydalanabilir. Olup, kimlik bilgileri Active Directory Federasyon Hizmetleri (AD FS) aracılığıyla dizin eşitlemeyi kullanmak veya kullanıcı hesapları yalnızca hello koruma federasyonunu bağlı olarak kullanarak, bulut [Microsoft Identity Manager](https://technet.microsoft.com/library/mt218776.aspx) (parçası Azure AD Premium) hello kaynaklar arasında kimlik yaşam döngülerini yönetmenize yardımcı olur.

### <a name="connectivity"></a>Bağlantı
Çeşitli mekanizmalar kullanılabilir toohelp güvenli istemci bağlantıları tooyour Azure sanal ağlardır. Bu mekanizmaların ikisi, [siteden siteye VPN](https://channel9.msdn.com/series/Azure-Site-to-Site-VPN) (S2S) ve [noktadan siteye VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) (P2S) etkinleştirmek hello kullanımını endüstri standardı IPSec (S2S) veya hello [Güvenli Yuva Tünel Protokolü](https://technet.microsoft.com/magazine/2007.06.cableguy.aspx)(SSTP) (P2S) şifreleme ve tünel oluşturma. Azure hello Azure portalı gibi toopublic yönelik Azure Hizmetleri yönetimine bağlandığında, Azure Köprü Metni Aktarım Protokolü güvenli (HTTPS) gerektirir.

TooAzure RD Ağ geçidi üzerinden bağlanmayan bir tek başına sağlamlaştırılmış iş istasyonu hello SSTP tabanlı noktadan siteye VPN toocreate hello ilk bağlantı toohello Azure sanal ağ kullanın ve RDP bağlantı tooindividual sanal oluşturun Merhaba VPN tüneli ile makinelerden.

### <a name="management-auditing-vs-policy-enforcement"></a>Yönetim denetimi ilke uygulama karşılaştırması
Genellikle, toosecure yönetim işlemlerine yardımcı olmak için iki yaklaşım vardır: denetim ve ilke uygulama. İkisini de uygulamak kapsamlı denetimler sağlasa da bu, her durumda mümkün olmayabilir. Ayrıca, her iki yaklaşımın farklı düzeylerde risk, maliyet ve çaba özellikle hem kişiler hem de sistem yapılarındaki güven düzeyini toohello ilgili olarak güvenlik, yönetmeyle ilgili sahiptir.

İzleme, günlüğe kaydetme ve Denetim izleme ve yönetim etkinlikleri anlamak için bir temel sunar ancak ayrıntı toohello oluşturulan veri miktarı nedeniyle tüm eylemlerin tamamlamak uygun tooaudit her zaman olmayabilir. Merhaba hello yönetim ilkelerinin verimliliğini denetlemek en iyi, ancak uygulamadır.

Sıkı erişim denetimleri içeren ilke uygulama yönetici eylemlerini yönetebilecek programlı bir mekanizma oluşturur ve olası tüm koruma önlemlerinin kullanılmasını sağlar. Günlük kaydı kimin ne, nerede ve ne zaman yaptığını, toplama tooa kaydındaki uygulama kanıtı sağlar. Ayrıca oturum tooaudit ve karşılaştırmasını yöneticilerin ilkeleri nasıl izlediğine hakkında bilgi sağlar ve etkinliklere dair kanıt sunar

## <a name="client-configuration"></a>İstemci yapılandırması
Sağlamlaştırılmış iş istasyonu için üç temel yapılandırma öneririz. Merhaba büyük differentiators aralarında maliyeti, kullanılabilirlik ve erişilebilirlik, tüm seçenekleri arasında benzer bir güvenlik profili korurken var. Aşağıdaki tablonun hello hello avantajları ve risklerinin tooeach kısa bir analizini sağlar. ("Kurumsal PC" rolleri bağımsız olarak tüm etki alanı kullanıcıları için dağıtılabilecek tooa standart masaüstü PC yapılandırması anlamına geldiğini unutmayın.)

| Yapılandırma | Avantajlar | Simgeler |
| --- | --- | --- |
| Tek başına sağlamlaştırılmış iş istasyonu |Sıkı denetlenen iş istasyonu |ayrılmış masaüstü bilgisayarlar için daha yüksek maliyet |
| - | Azaltılmış uygulama açıkları riski |Artan yönetim çabası |
| - | Net görev ayrımları | - |
| Sanal makine olarak kurumsal PC |Sınırlı donanım maliyetleri | - |
| - | Rol ve uygulamaların ayrımı | - |
| BitLocker Sürücü Şifrelemesi ile Windows toogo |Çoğu PC ile uyumluluk |Varlık izleme |
| - | Düşük maliyet ve taşınabilirlik | - |
| - | Yalıtılmış yönetim ortamı |- |

Merhaba sağlamlaştırılmış iş istasyonu hello ana bilgisayardır ve değil hello hello arasında bir şey olmadan Konuk ana bilgisayar işletim sistemi ve hello donanım önemlidir. Merhaba "temiz kaynak İlkesi" aşağıdaki (olarak da bilinen "güvenli kaynak") hello barındıran hello en sıkı anlamına gelir. Aksi takdirde, hello sağlamlaştırılmış iş istasyonu (konuk) üzerinde barındırıldığı hello sistemde konu tooattacks olur.

Yalnızca hello araçları yüklü her sağlamlaştırılmış iş istasyonu için ayrılmış sistem görüntüleri üzerinden yönetim işlevlerini daha fazla ayırabilirsiniz ve izinler yönetmek için Azure seçebilir ve uygulamalarla hello özel yerel AD DS GPO bulut Gerekli görevler.

Hiçbir şirket içi altyapısı (tüm sunucular hello bulutta olduğundan GPO'lar için yerel AD DS örneği Örneğin, hiçbir erişim tooa), BT ortamları için gibi bir hizmet [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx) dağıtmaya ve korumaya basitleştirebilir İş istasyonu yapılandırması.

### <a name="stand-alone-hardened-workstation-for-management"></a>Yönetim için tek başına sağlamlaştırılmış iş istasyonu
Tek başına sağlamlaştırılmış iş istasyonu ile, yöneticiler yönetim görevleri için kullandıkları bir PC ya da dizüstü bilgisayara ve yönetim dışı görevler için kullandıkları ayrı PC ya da dizüstü bilgisayara sahiptir. Bir iş istasyonu ayrılmış toomanaging Azure hizmetlerinizi yüklü diğer uygulamaları gerekmez. Ayrıca, [Güvenilir Platform Modülü 	](https://technet.microsoft.com/library/cc766159) (TPM) ya da benzer bir donanın düzeyi şifreleme teknolojisi cihaz kimlik doğrulamasına ve belirli saldırıların önlenmesine yardımcı olur. TPM ayrıca hello sistem sürücüsünün tam birim korumasını kullanarak destekleyebilir [BitLocker Sürücü Şifrelemesi](https://technet.microsoft.com/library/cc732774.aspx).

(Aşağıda gösterilen) hello tek başına sağlamlaştırılmış iş istasyonu senaryosunda hello yerel Windows Güvenlik Duvarı (veya Microsoft dışı istemci güvenlik duvarı) yapılandırılmış tooblock örneğidir gelen RDP gibi bağlantıları. Hello Yöneticisi toohello üzerinde oturum sağlamlaştırılmış iş istasyonu ve VPN Azure sanal ağı ile bağlanmak, ancak tooa Kurumsal PC ve kullanım RDP tooconnect toohello üzerinde oturum açamaz kurduktan sonra tooAzure bağlayan RDP oturumu bir başlangıç sağlamlaştırılmış iş istasyonu kendisi.

![][2]

### <a name="corporate-pc-as-virtual-machine"></a>Sanal makine olarak kurumsal PC
Ayrı bir tek başına sağlamlaştırılmış iş istasyonunun engelleyici ya da kullanışsız, hello burada maliyeti olması durumunda, sağlamlaştırılmış iş istasyonu bir sanal makine tooperform Yönetim dışı görevleri barındırabilir.

![][3]

tooavoid sistem yönetimi ve diğer günlük iş görevleri için bir iş istasyonu kullanarak oluşabilecek çeşitli güvenlik riskleri, dağıttığınız Windows Hyper-V sanal makine toohello sağlamlaştırılmış iş istasyonu. Bu sanal makine Kurumsal PC hello olarak kullanılabilir. Merhaba Kurumsal PC ortamı Merhaba, saldırı yüzeyini azaltan ve önemli yönetim görevleri ile birlikte hello kullanıcının günlük etkinliklerini (örneğin, e-posta) kaldıran konağı ndan yalıtılmış durumda kalabilir.

Merhaba Kurumsal PC sanal makinesi korumalı alanda çalışır ve kullanıcı uygulamaları sağlar. Merhaba ana bilgisayar "temiz kaynak" olarak kalır ve hello kök işletim sisteminde (örneğin, RDP erişimini engelleme hello sanal makineden) katı ağ ilkeleri uygular.

### <a name="windows-toogo"></a>Windows tooGo
Başka bir alternatif toorequiring tek başına sağlamlaştırılmış iş istasyonu toouse olan bir [Windows tooGo](https://technet.microsoft.com/library/hh831833.aspx) sürücü, istemci tarafı USB önyükleme özelliğini destekleyen bir özellik. Windows tooGo şifrelenmiş bir USB flash sürücüde çalışan kullanıcılar tooboot uyumlu bir PC tooan yalıtılmış sistem görüntüsü sağlar. Bu ek denetimleri için uzaktan yönetim uç noktaları hello görüntü, sıkı güvenlik ilkeleri, en az bir işletim sistemi yapı kurumsal BT grubu tarafından tam olarak yönetilebilir ve TPM desteğiyle çünkü sağlar.

Hello şekilde hello taşınabilir görüntü önceden yapılandırılmış tooconnect yalnızca tooAzure, çok faktörlü kimlik doğrulaması gerektirir ve tüm yönetim dışı trafiği engeller. bir etki alanına katılmış sistemdir. Kullanıcı önyüklemeleri aynı PC toohello standart kurumsal görüntüye ve Azure Yönetim Araçları için RD Ağ Geçidi erişme çalıştığında Merhaba, hello oturum engellenir. Windows tooGo hello kök düzeyinde işletim sistemi haline gelir ve gerekli (ana bilgisayar işletim sistemi, hiper yönetici, sanal makine) ek katman olan daha savunmasız toooutside saldırıları olabilir.

![][4]

USB flash sürücü ortalama bir masaüstü bilgisayar daha kolay kaybolur önemli toonote olur. BitLocker'ı tooencrypt hello birimin tamamını, güçlü bir parola kullanımını daha az olası bir saldırganın zararlı amaçlar için hello sürücü görüntüsü kullanabileceğiniz hale getirir. Ayrıca, hello USB flash sürücü kaybolursa, iptal etme ve [yeni bir yönetim sertifikası verme](https://technet.microsoft.com/library/hh831574.aspx) yanı sıra Hızlı parola sıfırlama tehlikeye maruz kalmayı azaltabilir. Yönetim denetim günlüklerinin daha olası veri kayıplarını azaltır değil hello istemcide Azure içinde bulunur.

## <a name="best-practices"></a>En iyi uygulamalar
Merhaba uygulamalar ve veri yönetirken aşağıdaki ek yönergeleri dikkate alın.

### <a name="dos-and-donts"></a>Yapılması gerekenler ve yapılmaması gerekenler
Bir iş istasyonu, kilitlendiğinden diğer ortak güvenlik gereksinimleri karşılayıp toobe gerekmez varsaymayın. Merhaba riski yönetici hesaplarının genellikle sahip olduğu yükseltilmiş erişim düzeyleri nedeniyle daha yüksektir. Risk örnekleri ve bunların alternatif güvenli uygulamaları hello aşağıdaki tabloda gösterilmektedir.

| Yapmayın | Yapın |
| --- | --- |
| Yönetici erişimine ilişkin kimlik bilgilerini veya diğer parolaları (ör. SSL veya yönetim sertifikaları) e-posta ile göndermeyin |Hesap adlarını ve parolaları sesli olarak ileterek gizliliği koruyun (ancak bunları sesli posta olarak depolamayın), istemci/sunucu sertifikalarının uzaktan yüklemesini gerçekleştirin (şifreli oturum yoluyla), korumalı ağ paylaşımından indirin ya da taşınabilir medya kullanarak el ile dağıtın. |
| - | Yaşam döngüsü yönetimi sertifikanızı proaktif olarak yönetin. |
| Hesap parolalarını şifrelenmemiş ya da karma olmayan uygulama depolama biriminde depolamayın (örneğin, elektronik tablolarda, SharePoint sitelerinde ya da dosya paylaşımlarında). |Güvenlik Yönetim ilkeleri ve sistem sağlamlaştırma ilkeleri oluşturun ve bunları tooyour geliştirme ortamı uygulayabilirsiniz. |
| - | Kullanım [Enhanced Mitigation Experience Toolkit 5.5](https://technet.microsoft.com/security/jj653751) sertifikası sabitleme kuralları tooensure tooAzure SSL/TLS sitelerine uygun erişme. |
| Hesapları ve parolaları yöneticiler arasında paylaşmayın veya parolaları birden fazla kullanıcı hesabında ya da hizmette yeniden kullanmayın, özellikle sosyal medya ve diğer yönetim dışı etkinlikler için olanları. |Azure aboneliğinize adanmış bir Microsoft hesabı toomanage oluşturma — Kişisel e-postalar için kullanılmayan bir hesap. |
| Yapılandırma dosyalarını e-posta ile göndermeyin. |Yapılandırma dosyaları ve profilleri, e-posta gibi kolayca tehlikeye girebilecek bir mekanizmadan değil, güvenilir bir kaynaktan yüklenmelidir (örneğin, şifrelenmiş bir USB flash sürücü). |
| Zayıf veya basit oturum açma parolaları kullanmayın. |Güçlü parola ilkeleri, sona erme döngüleri (ilk kullanımda değiştirme), konsol zaman aşımları ve otomatik hesap kilitlemeleri uygulayın. Parola kasa erişimi için multi-factor authentication ile istemci parola yönetimi sistemi kullanın. |
| Yönetim bağlantı noktaları toohello Internet'e sunmayın. |Azure bağlantı noktaları ve IP adreslerini toorestrict yönetim erişimi kilitleme. Daha fazla bilgi için bkz: Merhaba [Azure ağ güvenliği](http://download.microsoft.com/download/4/3/9/43902EC9-410E-4875-8800-0788BE146A3D/Windows%20Azure%20Network%20Security%20Whitepaper%20-%20FINAL.docx) teknik incelemesi. |
| - | Tüm yönetim bağlantıları için güvenlik duvarları, VPN’ler ve NAP kullanın. |

## <a name="azure-operations"></a>Azure işlemleri
Microsoft’un Azure işlemleri çerçevesinde, Azure’un üretim sistemlerine erişimi olan işlem mühendisleri ve destek personeli iç kurumsal ağ erişimi ve uygulamaları için (e-posta, intranet gibi) kendilerine sağlanan [sanal makineler ile sağlamlaştırılmış iş istasyonu bilgisayarları](#stand-alone-hardened-workstation-for-management) kullanır. Tüm yönetim iş istasyonu bilgisayarlarında TPM'ler bulunur, hello ana bilgisayar önyükleme sürücüsü BitLocker ile şifrelenmiştir ve bunlar birleştirilmiş tooa özel kuruluş biriminde (OU) Microsoft'un birincil Kurumsal etki alanı.

Sistem sağlamlaştırma merkezileştirilmiş yazılım güncelleştirme ile Grup İlkesi aracılığıyla uygulanır. Denetim ve çözümleme için olay günlükleri (örneğin, güvenlik ve AppLocker) yönetim istasyonlarından toplanır ve tooa merkezi konuma kaydedilir.

Ayrıca, ayrılmış atlama-iki faktörlü kimlik doğrulaması gerektiren Microsoft'un ağda kullanılan tooconnect tooAzure'nın üretim ağı kutularıdır.

## <a name="azure-security-checklist"></a>Azure güvenlik denetim listesi
Sağlamlaştırılmış bir iş istasyonunda yöneticilerin gerçekleştirebileceği görevleri Hello sayısını en aza indirir, geliştirme ve yönetim ortamı hello saldırı yüzeyini en aza indirmenize yardımcı olur. Teknolojileri toohelp aşağıdaki kullanım hello sağlamlaştırılmış iş istasyonunuzu koruyun:

* IE sağlamlaştırma. Merhaba Internet Explorer tarayıcı (veya bu herhangi bir web tarayıcısı) bir anahtar girişi tooits dış sunucularla olan yoğun etkileşimleri nedeniyle zararlı bir kod noktasıdır. İstemci ilkelerinizi inceleyin ve korumalı modda çalışma, eklentileri devre dışı bırakma, dosya yüklemelerini devre dışı bırakma ve [Microsoft SmartScreen](https://technet.microsoft.com/library/jj618329.aspx) filtrelemesi seçeneklerini kullanın. Güvenlik uyarılarının göründüğünden emin olun. İnternet bölgelerinden faydalanın ve makul sağlamlaştırma yapılandırdığınız güveniliri siteler için bir listesini oluşturun. Tüm diğer siteleri ve ActiveX ve Java gibi tarayıcı içi kodları engelleyin.
* Standart kullanıcı. Standart kullanıcı çok sayıda fayda getirir gibi hello hangisinin büyük kötü amaçlı yazılımı aracılığıyla yönetici kimlik bilgilerinin çalınmasının daha zor olduğunu çalışıyor. Ayrıca, standart kullanıcı hesabı hello kök işletim sisteminde yükseltilmiş ayrıcalıkları yok ve birçok yapılandırma seçeneği ve API'leri varsayılan olarak kilitlidir.
* AppLocker. Kullanabileceğiniz [AppLocker](http://technet.microsoft.com/library/ee619725.aspx) toorestrict hello programlar ve kullanıcıların çalıştırabileceği komut dosyaları. AppLocker’ı denetim veya zorlama modunda çalıştırabilirsiniz. Varsayılan olarak, AppLocker yönetici belirteci toorun olan kullanıcıların hello istemcideki tüm kodları sağlar bir izin verme kuralı vardır. Bu kural tooprevent yöneticilerin kendilerini çıkışı kilitleme var ve yalnızca tooelevated belirteçleri uygular. Ayrıca Windows Server [çekirdek güvenlik](http://technet.microsoft.com/library/dd348705.aspx) parçası olarak Kod Bütünlüğü’ne bakın.
* Kod imzalama. Yöneticiler tarafından kullanılan tüm araçlar ve betiklerde kod imzalama uygulama kilitleme ilkeleri dağıtmak için yönetilebilir bir mekanizma sağlar. Karmaları hızlı değişiklikler toohello koduyla ölçeklenmez ve dosya yolları yüksek düzeyde güvenlik sağlamaz. AppLocker kuralları bir PowerShell ile birleştirmelisiniz [yürütme İlkesi](http://technet.microsoft.com/library/ee176961.aspx) yalnızca özel imzalı kod sağlar ve toobe komutlar [yürütülen](http://technet.microsoft.com/library/hh849812.aspx).
* Grup İlkesi. Genel yönetim ilkesi oluşturma Yönetim (ve tüm başkalarından gelen erişimi engellemek) için kullanılan uygulanan tooany etki alanı iş istasyonu ve toouser hesapları bu istasyonlarında kimlik doğrulaması.
* Gelişmiş güvenlik sağlama. Taban çizgisi sağlamlaştırılmış iş istasyonunu görüntünüzü koruyun toohelp kurcalanmaya karşı koruma. Şifreleme ve yalıtım toostore görüntüler, sanal makineler ve betikleri gibi güvenlik önlemleri kullanın ve erişim (belki de kullanımı bir denetlenebilir iade-içinde/kullanıma işlemi) kısıtlayın.
* Düzeltme eki uygulama. Tutarlı yapıyı koruyun (ya da geliştirme işlemleri ve diğer yönetim görevleri için ayrı görüntülere sahip), değişiklikler ve kötü amaçlı yazılım düzenli olarak, toodate hello yapıyı tutun ve gerektiğinde makineleri yalnızca etkinleştirme için tarama.
* Şifreleme. Yönetim iş istasyonları güvenle sağlamak TPM toomore olduğundan emin olun [şifreleme dosya sistemi](https://technet.microsoft.com/library/cc700811.aspx) (EFS) ve BitLocker'ı. Windows tooGo kullanıyorsanız, yalnızca şifrelenmiş USB anahtarlarını BitLocker ile birlikte kullanın.
* İdare. Dosya paylaşımı gibi tüm hello yöneticinin Windows arabirimleri AD DS GPO'ları toocontrol kullanın. Yönetim iş istasyonlarını denetim, izleme ve günlüğe kaydetme işlemlerine dahil edin. Tüm yönetici ve geliştirici erişimini ve kullanımını izleyin.

## <a name="summary"></a>Özet
Azure bulut hizmetlerinizi, Sanal Makinelerinizi ve uygulamalarınızı yönetmek için sağlamlaştırılmış iş istasyonları kullanmak kritik önemdeki BT altyapısını uzaktan yönetmenin getirebileceği çok sayıda riskten ve tehditten kaçınmanıza yardımcı olabilir. Hem Azure hem de Windows toohelp uygulayabileceğiniz mekanizmalar korumak ve iletişimleri, kimlik doğrulaması ve istemci davranışını denetleyen sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba aşağıdaki kullanılabilir tooprovide kaynaklardır Azure hakkında daha fazla genel bilgi ve Microsoft Hizmetleri, bu belgede başvurulan toplama toospecific öğeleri ilgili:

* [Ayrıcalıklı erişimi güvenli hale getirme](https://technet.microsoft.com/library/mt631194.aspx) – tasarlama ve Azure Yönetim için güvenli yönetim iş istasyonu oluşturmak için hello teknik ayrıntıları alın
* [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Security/AzureSecurity) - Azure dokusunu hello koruyan Azure platformu özellikleri hakkında bilgi edinin ve iş yükleri, çalıştırılacak Azure hello
* [Microsoft Security Response Center](http://www.microsoft.com/security/msrc/default.aspx) --Azure ile ilgili sorunları dahil Microsoft güvenlik açıklarının bildirilmesi veya e-posta yoluyla çok[secure@microsoft.com](mailto:secure@microsoft.com)
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) – en son Azure güvenlik hello üzerinde toodate tutun

<!--Image references-->
[1]: ./media/azure-security-management/typical-management-network-topology.png
[2]: ./media/azure-security-management/stand-alone-hardened-workstation-topology.png
[3]: ./media/azure-security-management/hardened-workstation-enabled-with-hyper-v.png
[4]: ./media/azure-security-management/hardened-workstation-using-windows-to-go-on-a-usb-flash-drive.png
