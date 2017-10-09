---
title: "aaaData güvenlik ve şifreleme en iyi yöntemler | Microsoft Docs"
description: "Bu makalede veri güvenliği için en iyi yöntemler kümesi sağlar ve şifreleme kullanılarak Azure özellikleri."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 17ba67ad-e5cd-4a8f-b435-5218df753ca4
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: yurid
ms.openlocfilehash: 5057c85ed3107921462a40045e716675ea41e4bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-security-and-encryption-best-practices"></a>Azure veri güvenliği ve şifreleme en iyi uygulamalar
Hello anahtarları toodata koruma hello bulutta birini hello olası durumlar verilerinizi ortaya çıkabilecek ve bu durum için hangi denetimlerin kullanılabilir hesap. Azure veri güvenlik ve şifreleme en iyi uygulamaları Hello amaçla hello önerileri verilerinin durumları aşağıdaki hello geçici bir çözüm olacaktır:

* : Çalışmıyorken Bu depolama nesneleri, kapsayıcıları ve statik olarak fiziksel medyada mevcut türleri manyetik veya optik disk olması tüm bilgileri içerir.
* Aktarım sırasında: Ne zaman veri aktarılmakta olan bileşenleri, konumlara veya programları arasında gibi hello ağ üzerinden bir hizmet veri yolundan (şirket içi toocloud ve ExpressRoute gibi karma bağlantılar dahil olmak üzere tersi,) üzerinden veya bir giriş/çıkış sırasında işlem, bu düşündüğünüz olarak hareket halinde.

Bu makalede Azure data güvenlik ve şifreleme en iyi uygulamaları koleksiyonu aşağıdakiler ele alınacaktır. Bu en iyi uygulamaları ile Azure veri güvenliği deneyimi bizim türetilen ve şifreleme ve hello karşılaştığında müşterilerin kendiniz gibi.

En iyi her uygulama için açıklayacağız:

* Hangi hello en iyi uygulamadır
* Neden bu en iyi uygulama tooenable istiyor
* Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
* Olası alternatifler toohello en iyi uygulama
* Tooenable hello en iyi yöntem nasıl öğrenin

Bu makalenin yazıldığı hello aynı anda var Bu Azure veri güvenliği ve şifreleme en iyi yöntemler makalesi anlaşma fikir ve Azure platformu özellikleri ve özellik kümeleri dayanır. Bu makalede olacaktır ve görüşlerini ve teknolojileri değiştirmek zaman içinde bu değişiklikleri düzenli olarak tooreflect üzerinde güncelleştirildi.

Bu makalede ele alınan azure veri güvenlik ve şifreleme en iyi uygulamalar şunlardır:

* Çok faktörlü kimlik doğrulamasını zorunlu
* Kullanım rol tabanlı erişim denetimi (RBAC)
* Azure virtual machines şifreleme
* Donanım güvenlik modelleri kullanma
* Güvenli iş istasyonları ile yönetme
* SQL veri şifrelemeyi etkinleştir
* Aktarımdaki verileri korumak
* Dosya düzeyinde veri şifrelemeyi zorunlu kılma

## <a name="enforce-multi-factor-authentication"></a>Çok faktörlü kimlik doğrulamasını zorunlu
veri erişimi ilk adımda Hello ve Microsoft Azure denetiminde tooauthenticate hello kullanıcıdır. [Azure multi-Factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md) yalnızca bir kullanıcı adı ve parola'den başka bir yöntem kullanarak kullanıcının kimliğini doğrulayan bir yöntemdir. Bu kimlik doğrulama yöntemi kullanıcı talebine basit bir oturum açma işlemi için buluştururken koruma erişim toodata ve uygulamaları yardımcı olur.

Kullanıcılarınız için Azure MFA etkinleştirerek, güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı ekliyorsunuz. Bu durumda, bir işlem bir dosya sunucusunda veya, SharePoint Online'da bulunan bir belge erişiyor. Azure MFA, güvenliği aşılmış bir kimlik bilgisi erişim tooorganization'ın veri olduğunu BT tooreduce hello olasılığı da yardımcı olur.

Örneğin: kullanıcılarınız için Azure MFA zorlamak ve hello kullanıcının kimlik bilgileri aşılıp aşılmadığını toouse bir telefon araması veya kısa mesaj doğrulama yapılandırın, hello saldırgan olmaz kendisine erişim toouser'ın telefon olmaz beri mümkün tooaccess herhangi bir kaynak olabilir. Bu ek kimlik koruması katmanı eklemeyin kuruluşlar toodata güvenliğinin aşılmasına neden olabilir kimlik bilgisi hırsızlığı saldırısına için daha açıktır.

Bir alternatif tookeep hello kimlik doğrulama denetimi isteyen kuruluşların için şirket içi olan toouse [Azure çok faktörlü kimlik doğrulama sunucusu](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), MFA şirket içi olarak da bilinir. Bu yöntemi kullanarak hello MFA sunucusu şirket içi korurken mümkün tooenforce çok faktörlü kimlik doğrulaması yine olacaktır.

Azure MFA hakkında daha fazla bilgi için lütfen hello makaleyi okuyun [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Kullanım rol tabanlı erişim denetimi (RBAC)
Merhaba üzerinde bağlı erişimi kısıtlayabilirsiniz [tooknow gerek](https://en.wikipedia.org/wiki/Need_to_know) ve [en az ayrıcalık](https://en.wikipedia.org/wiki/Principle_of_least_privilege) güvenlik ilkeleri. Bu, veri erişimi için tooenforce güvenlik ilkeleri istediğiniz kuruluşlar için zorunludur. Azure rol tabanlı erişim denetimi (RBAC) kullanılan tooassign izinleri toousers, gruplar ve uygulamalar belirli bir kapsamda olabilir. bir rol ataması Hello kapsamını bir abonelik, bir kaynak grubu veya tek bir kaynak olabilir.

Yararlanabileceğiniz [yerleşik RBAC rolleri](../active-directory/role-based-access-built-in-roles.md) Azure'da tooassign toousers ayrıcalıkları. Kullanmayı *depolama hesabı katkıda bulunan* toomanage depolama hesapları gereken bulut operatörleri için ve *Klasik depolama hesabı katkıda bulunan* rol toomanage Klasik depolama hesapları. Toomanage Vm'leri ve depolama hesabı gerekiyor bulut operatörleri için bunları çok eklemeyi düşünün*sanal makine Katılımcısı* rol.

Veri erişim denetimi RBAC gibi özellikler yararlanarak zorlamaz kuruluşlar kendi kullanıcıları için gerekenden daha fazla ayrıcalık vermiş. Merhaba ilk yerinde olmamalıdır erişim toodata olan bazı kullanıcılar sağlayarak bu toodata güvenliğinin aşılmasına neden olabilir.

Merhaba makale okuyarak Azure RBAC hakkında daha fazla bilgiyi [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

## <a name="encrypt-azure-virtual-machines"></a>Azure Virtual Machines şifreleme
Çoğu kuruluş için [bekleyen verileri şifreleme](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) veri gizliliği, uyumluluk ve veri egemenliği doğru zorunlu bir adımdır. Azure Disk şifrelemesi, BT yöneticileri tooencrypt Windows ve Linux Iaas sanal makine (VM) diskleri sağlar. Azure Disk şifrelemesi hello endüstri standart BitLocker özelliği, Windows ve Linux tooprovide birim şifreleme hello işletim sistemi için hello DM-Crypt özelliği ve hello veri diskleri yararlanır.

Azure Disk şifrelemesi yararlanabilirsiniz toohelp korumak ve kuruluşunuzun güvenlik ve uyumluluk gereksinimlerini veri toomeet koruyun. Kuruluşlar, şifreleme kullanarak da düşünmelisiniz toohelp riskleri ilgili toounauthorized veri erişimi etkisini azaltır. Sürücüleri önceki toowriting hassas verileri toothem şifrelemeniz önerilir.

Emin tooencrypt VM veri birimleri ve önyükleme birimi sipariş tooprotect verilerini Azure depolama hesabınızdaki REST yapın. Koruma hello şifreleme anahtarları ve gizli anahtarları yararlanarak [Azure anahtar kasası](../key-vault/key-vault-whatis.md).

Şirket içi Windows sunucuları için şifreleme en iyi uygulamaları izleyerek hello göz önünde bulundurun:

* Kullanım [BitLocker](https://technet.microsoft.com/library/dn306081.aspx) için veri şifreleme
* Kurtarma bilgileri AD DS'de depolar.
* BitLocker anahtarları aşılmış herhangi bir sorun varsa, tüm örneklerini hello sürücü veya sizin hello BitLocker meta verilerini hello sürücünün tamamını yeniden şifrelemek ve şifresini çözmek hello sürücü tooremove ya da biçimlendirmek öneririz.

Veri şifrelemeyi zorunlu olmayan kuruluşlar büyük olasılıkla açığa toobe toodata veri hırsızlığı kötü amaçlı veya standart dışı kullanıcılar gibi bütünlüğü sorunlar var ve yetkisiz erişim toodata Temizle biçiminde sağlamasını hesapları tehlikeye. Bu riskleri yanı sıra, sektör düzenlemelerini ile toocomply kullanan şirket gerekir kanıtlamak dikkatli ve hello doğru güvenlik denetimleri tooenhance veri güvenliği kullanma.

Merhaba makale okuyarak Azure Disk şifrelemesi hakkında daha fazla bilgiyi [için Azure Disk şifrelemesi Windows ve Linux Iaas VM'ler](azure-security-disk-encryption.md).

## <a name="use-hardware-security-modules"></a>Donanım güvenlik modülleri kullanma
Endüstri şifreleme çözümleri gizli anahtarlarına tooencrypt verileri kullanın. Bu nedenle, bu anahtarları güvenli şekilde depolanan önemlidir. Kullanılan tooencrypt veri çevrelerini toostore gizli anahtarları olacağından anahtar yönetimi veri koruması'nın ayrılmaz bir parçası olur.

Azure disk şifrelemesi kullanan [Azure anahtar kasası](https://azure.microsoft.com/services/key-vault/) toohelp, denetlemek ve disk şifreleme anahtarları ve gizli anahtarları Azure bekleyen hello sanal makine disklerdeki tüm veriler şifrelenir sağlarken anahtar kasası aboneliğinizde yönetme depolama alanı. Azure anahtar kasası tooaudit anahtarları ve ilke kullanım kullanmanız gerekir.

Verilerinizi kullanılan tooencrypt olan yer tooprotect hello gizli anahtarları uygun güvenlik denetimleri sahip birçok devralınmış riskleri ilgili toonot vardır. Saldırganlar erişiminiz varsa toohello gizli anahtarları, bunlar mümkün toodecrypt hello veriler ve tooconfidential bilgilerine erişme potansiyeline sahip.

Merhaba makale okuyarak Azure sertifika yönetimi için genel öneriler hakkında daha fazla bilgiyi [Azure sertifika yönetimi: ilgilenmenin](https://blogs.msdn.microsoft.com/azuresecurity/2015/07/13/certificate-management-in-azure-dos-and-donts/).

Azure anahtar kasası hakkında daha fazla bilgi için okuma [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).

## <a name="manage-with-secure-workstations"></a>Güvenli iş istasyonları ile yönetme
Hello çoğunluğu hello saldırıları hedef hello son kullanıcı bu yana, saldırı hello birincil noktalarından birini hello uç noktası olur. Bir saldırgan hello endpoint etkilediğinde, kendisinin hello kullanıcının kimlik bilgilerini toogain erişim tooorganization ait veri yararlanabilirsiniz. Çoğu uç nokta saldırıları son kullanıcıların kendi yerel iş istasyonlarını Yöneticiler hello bulunmasına mümkün tootake avantajlarından ' dir.

Güvenli yönetim iş istasyonu kullanarak bu riskleri azaltabilirsiniz. Kullanmanızı öneririz bir [ayrıcalıklı erişim iş istasyonları (PENÇE)](https://technet.microsoft.com/library/mt634654.aspx) tooreduce hello saldırı yüzeyini iş istasyonları. Bu güvenli yönetim iş istasyonları, bunlardan bazıları azaltmaya yardımcı olabilir saldırıları Yardım verilerinizi daha güvenli olduğundan emin olun. Emin toouse PENÇE tooharden ve kilit istasyonunuzu olun. Bu önemli adım tooprovide yüksek güvenlik çıkışların hassas hesapları, görevleri ve veri koruması için olur.

Uç nokta koruma eksikliği verilerinizi riske, bu hello veri konumu (Bulut veya şirket içi) bağımsız olarak kullanılan tooconsume veri tüm cihazlar arasında güvenlik ilkeleri emin tooenforce olun.

Ayrıcalıklı hakkında daha fazla erişim iş istasyonu hello makale okuyarak öğrenebilirsiniz [ayrıcalıklı erişimi güvenli hale getirme](https://technet.microsoft.com/library/mt631194.aspx).

## <a name="enable-sql-data-encryption"></a>SQL veri şifrelemeyi etkinleştir
[Azure SQL veritabanında saydam veri şifreleme](https://msdn.microsoft.com/library/dn948096.aspx) (TDE), gerçek zamanlı şifreleme ve şifre çözme hello veritabanının, ilişkili yedeklemelerinizi gerçekleştirerek kötü amaçlı etkinliği hello tehdide karşı korunmasına yardımcı olur ve işlem günlüğü dosyalarını REST gerektiren değişiklikler toohello uygulama.  TDE, bir simetrik anahtar adlı hello veritabanı şifreleme anahtarı kullanarak veritabanının tamamını hello depolanmasını şifreler.

Merhaba tüm depolama bile şifreli olduğunda tooalso şifrelemek, veritabanınızı çok önemlidir. Bu veri koruması derinliği yaklaşımda hello savunma uygulamasıdır. Kullanıyorsanız [Azure SQL veritabanı](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx) ve tooprotect hassas verileri istiyor kredi kartı veya sosyal güvenlik numarası gibi birçok hello gereksinimleri karşılayan 140-2 doğrulanmış 256 bit AES şifreleme FIPS veritabanlarıyla şifreleyebilirsiniz. endüstri standartları (örn., HIPAA, PCI).

İlgili dosyaları çok önemli toounderstand olan[arabellek havuzu genişletme](https://msdn.microsoft.com/library/dn133176.aspx) (BPE) TDE kullanarak bir veritabanı şifreli olduğunda şifrelenmez. BitLocker'ı veya hello gibi dosya sistemi düzeyinde şifreleme araçları kullanmalısınız [şifreleme dosya sistemi](https://technet.microsoft.com/library/cc700811.aspx) (EFS) dosyaları için BPE ilgili.

Yetkili bir kullanıcı bu yana gibi bir güvenlik yöneticisi veya bir veritabanı yöneticisi Hello veritabanı ile TDE, şifreli olsa bile hello verilere erişebilir hello önerileri aşağıda da izlemelidir:

* Merhaba veritabanı düzeyinde SQL kimlik doğrulaması
* RBAC rollerini kullanarak azure AD kimlik doğrulaması
* Kullanıcılar ve uygulamalar ayrı hesaplar tooauthenticate kullanmanız gerekir. Bu şekilde toousers ve uygulamaları hello izinler sınırlayabilir ve kötü amaçlı etkinliğin hello riskleri azaltın
* Uygulama veritabanı düzeyi güvenlik (örneğin, db_datareader veya db_datawriter) sabit veritabanı rollerinin veya kullanarak izinler tooselected veritabanı nesnelerini uygulama toogrant için özel rolleri oluşturabilirsiniz

Veritabanı düzeyinde şifreleme kullanılarak olmayan kuruluşlar daha açıktır. SQL veritabanlarında bulunan verilere tehlikeye atabilir saldırıları için olabilir.

Merhaba makale okuyarak SQL TDE'nin şifreleme hakkında daha fazla bilgiyi [saydam veri şifrelemesi ile Azure SQL veritabanı](https://msdn.microsoft.com/library/0bf7e8ff-1416-4923-9c4c-49341e208c62.aspx).

## <a name="protect-data-in-transit"></a>Aktarımdaki verileri korumak
Aktarımdaki verileri koruma temel veri koruma stratejinizin parçası olmalıdır. Verileri geri ve İleri birçok konumlardan taşıma beri hello genel SSL/TLS protokolleri tooexchange verileri her zaman farklı konumlar arasında kullanmanız önerilir. Bazı durumlarda, şirket içi ve bulut arasındaki tooisolate hello tüm iletişim kanalını isteyebilirsiniz sanal özel ağ (VPN) kullanarak altyapı.

Şirket içi altyapınızı ve Azure arasında taşıma verileri için HTTPS veya VPN gibi uygun güvenlik önlemleri göz önünde bulundurmalısınız.

Birden çok iş istasyonları şirket içi tooAzure toosecure erişimden gereken kuruluşlar için kullanmak [Azure siteden siteye VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md).

Bir iş istasyonundan toosecure erişmeniz kuruluşlar için şirket içi tooAzure, kullanım bulunan [noktası siteye VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md).

Büyük veri kümeleri taşınabilir ayrılmış bir yüksek hızlı WAN bağlantısı üzerinden gibi [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Toouse ExpressRoute seçerseniz, ayrıca uygulama düzeyi hello kullanarak hello verileri şifreleyebilir [SSL/TLS](https://support.microsoft.com/kb/257591) veya diğer protokoller için ek koruma.

Hello Azure portalı Azure Storage ile etkileşim, tüm işlemleri HTTPS oluşur. [Storage REST API'sini](https://msdn.microsoft.com/library/azure/dd179355.aspx) HTTPS üzerinden de ile kullanılan toointeract olabilir [Azure Storage](https://azure.microsoft.com/services/storage/) ve [Azure SQL veritabanı](https://azure.microsoft.com/services/sql-database/).

Aktarım tooprotect verileri başarısız kuruluşlar için daha açıktır [man-in--middle saldırıları](https://technet.microsoft.com/library/gg195821.aspx), [gizli dinleme](https://technet.microsoft.com/library/gg195641.aspx) ve oturumu ele geçirme. Bu saldırıların erişim tooconfidential veri sağlamasını hello ilk adımı olabilir.

Merhaba makale okuyarak Azure VPN seçeneği hakkında daha fazla bilgiyi [planlama ve tasarım VPN ağ geçidi için](../vpn-gateway/vpn-gateway-plan-design.md).

## <a name="enforce-file-level-data-encryption"></a>Dosya düzeyinde veri şifrelemeyi zorunlu kılma
Bir başka hello verileriniz için güvenlik düzeyini artırabilirsiniz koruma katmanı hello dosyasının kendisini, hello dosya konumu bağımsız olarak şifreleme.

[Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) kullandığı şifreleme, kimlik ve yetkilendirme ilkeleri toohelp güvenli dosyalarınızın ve e-posta. Azure RMS birden çok cihazda çalışır — telefonları, Tablet ve PC'leri hem kuruluşunuz içinde hem de kuruluşunuz dışındaki koruma tarafından. Azure RMS bile, kuruluşunuzun sınırları dışına çıktığında hello veriler devam koruma düzeyini eklediğinden bu olası bir yetenektir.

Azure RMS tooprotect dosyalarınızı kullandığınızda, endüstri standardı şifreleme ile tam destek kullanmakta olduğunuz [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Veri koruma için Azure RMS yararlanan, hello denetimi altında olmayan kopyalanan toostorage olsa bile hello koruma hello dosyayla kalır hello güvence sahip bir bulut depolama hizmeti gibi BT'nin. Merhaba aynı e-posta ile paylaşılan dosyaları için gerçekleşir, hello dosya eki tooan e-posta eki olarak korunur, yönergelerle ek nasıl tooopen hello korumalı.

Azure RMS benimseme için planlama yaparken hello şunları öneririz:

* Merhaba yüklemek [RMS sharing uygulaması](https://technet.microsoft.com/library/dn339006.aspx). Bu uygulama tarafından bir Office Eklentisi-kullanıcıların kolayca dosyaları doğrudan koruyabilmeniz için Office uygulamalarıyla ile tümleşir.
* Uygulamaları ve Hizmetleri toosupport Azure RMS yapılandırma
* Oluşturma [özel şablonlar](https://technet.microsoft.com/library/dn642472.aspx) iş gereksinimlerinizi yansıtır. Örneğin: tüm üst gizliliği uygulanması gereken üst gizli veriler için bir şablon ilgili e-postaları.

Üzerinde zayıf kuruluşlar [veri sınıflandırması](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) ve dosya koruması daha açıktır. toodata sızıntısı olabilir. Uygun dosya koruma, kuruluşların iş öngörüleri, uygunsuz kullanım izleme mümkün tooobtain olmalı ve kötü amaçlı erişime toofiles önlemek olmaz.

Merhaba makale okuyarak Azure RMS hakkında daha fazla bilgiyi [Azure Rights Management ile çalışmaya başlama](https://technet.microsoft.com/library/jj585016.aspx).
