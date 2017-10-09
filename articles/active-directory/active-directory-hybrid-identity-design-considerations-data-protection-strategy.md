---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - veri koruma stratejisini tanımlayın | Microsoft Docs"
description: "Tanımladığınız karma kimlik çözümü toomeet hello iş gereksinimlerinizi için hello veri koruma stratejisini tanımlayın."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Karma kimlik çözümü için veri koruma stratejisini tanımlayın
Bu görevde tanımlanan karma kimlik çözümü toomeet hello iş gereksinimleriniz için hello veri koruma stratejisini tanımlayın:

* [Veri koruma gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [İçerik Yönetimi gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Erişim denetimi gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Olay yanıtlama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Veri koruma seçeneklerini tanımlayın
İçinde açıklanan [dizin eşitleme gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), Microsoft Azure AD, Active Directory etki alanı Hizmetleri ile (AD DS) eşitlemek, şirket içi bulunan. Tooaccess şirket kaynaklarına çalışırken bu tümleştirme kuruluşlar tooleverage Azure AD tooverify kullanıcının kimlik bilgilerini sağlar. Bu her iki senaryo için yapılabilir: veri rest şirket içi ve hello bulutta.  Erişim toodata Azure AD'de bir güvenlik belirteci hizmeti (STS) aracılığıyla kullanıcı kimlik doğrulaması gerektirir.

Kimlik doğrulaması, hello kullanıcı asıl adı (UPN) hello kimlik doğrulaması belirtecinden okunur ve hello bölüm ve kapsayıcı karşılık gelen çoğaltılan sonra toohello kullanıcının etki alanı belirlenir. Merhaba istenen erişim toohello hedef Kiracı bu kullanıcı için bu oturumda yetkilendirilip yetkilendirilmediğini hello kullanıcının varlığı, etkin durumunu ve rol bilgilerini hello yetkilendirme sistem toodetermine tarafından kullanılır. Yetkili belirli eylemleri (özellikle, kullanıcı, parola sıfırlama Oluştur) bir kiracı tarafından kullanılan bir denetim izi oluşturma yönetici toomanage uyumluluk çaba veya araştırmalar.

Azure Storage, şirket içi veri merkezine Internet bağlantısı üzerinden taşıma verileri her zaman toodata birim, bant genişliği kullanılabilirliğini veya diğer noktalar uygun olmayabilir. Merhaba [Azure depolama içeri/dışarı aktarma hizmeti](../storage/common/storage-import-export-service.md) yerleştirme ve alma büyük miktarda veriyi blob depolama için bir donanım tabanlı seçeneği sağlar. Toosend tanır [BitLocker şifrelenmiş](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) tooreturn tooan burada bulut operatörleri karşıya yükleme hello içeriği tooyour depolama hesabı veya, Azure veri tooyour indirebilirsiniz Azure veri merkezi sürücüleri doğrudan sabit disk sürücüleri tooyou. Yalnızca şifrelenmiş diskleri (Merhaba hizmetin kendisini hello iş Kurulum sırasında tarafından oluşturulan bir BitLocker anahtarını kullanarak) Bu işlem için kabul edilir. Merhaba BitLocker anahtarını tooAzure böylece bant anahtar paylaşımı dışında sağlayan ayrı ayrı sağlanır.

Aktarımdaki verileri farklı senaryolarında gerçekleşebilir, aynı zamanda Microsoft Azure kullanan ilgili tooknow olduğu [sanal ağ](https://azure.microsoft.com/documentation/services/virtual-network/) önlemleri gibi ana bilgisayar ve Konuk düzeyi kullanan tooisolate kiracılar trafiği birbirinden, Güvenlik duvarları, IP paket filtreleme, bağlantı noktası engelleme ve HTTPS uç noktalarının. Ancak, Azure'nın iç iletişimler, altyapı altyapı ve altyapı müşteri (şirket) dahil olmak üzere çoğu de şifrelenir. Başka bir önemli bir senaryo hello iletişimleri Azure veri merkezleri içinde ise; Microsoft hiçbir VM taklit veya başka bir IP adresi hello misafiri ağları tooassure yönetir. TLS/SSL, Azure Storage veya SQL veritabanları erişirken veya tooCloud Hizmetleri bağlanırken kullanılır. Bu durumda, bir TLS/SSL sertifikası alma ve tootheir Kiracı altyapısı dağıtma Merhaba müşteri yönetici sorumludur. Sanal makineler arasında taşıyarak veri trafiği hello aynı dağıtım veya Microsoft Azure sanal ağı aracılığıyla tek bir dağıtımda kiracılar arasındaki HTTPS, SSL/TLS veya diğerleri gibi şifreli iletişim protokolleri üzerinden korunabilir.

Nasıl hello sorulara verdiğiniz yanıtlara bağlı olarak [veri koruma gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), verilerinizi tooprotect istediğiniz nasıl ve hello karma kimlik çözümü, üzerinde yardımcı olacak nasıl mümkün toodetermine olmalıdır. Merhaba tablo her veri koruma senaryosu için kullanılabilir olan Azure tarafından desteklenen hello seçeneklerini gösterir.

| Veri koruma seçenekleri | Bekleyen hello bulutta | REST şirket içi | Aktarım sırasında |
| --- | --- | --- | --- |
| BitLocker Sürücü Şifrelemesi |X |X | |
| SQL Server tooencrypt veritabanları |X |X | |
| VM VM şifreleme | | |X |
| SSL/TLS | | |X |
| VPN | | |X |

> [!NOTE]
> Okuma [uyumluluk özelliği tarafından](https://azure.microsoft.com/support/trust-center/services/) adresindeki [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow her Azure hizmeti ile uyumludur hello sertifikalar hakkında daha fazla.
> Merhaba seçenekleri veri koruması sağlamak için çok katmanlı bir yaklaşım kullandığından, bu seçenekler arasında karşılaştırma olmayan bu görev için uygulanabilir. Merhaba veriler her durum için kullanılabilir tüm seçenekleri yararlanarak emin olun.
>
>

## <a name="define-content-management-options"></a>İçerik yönetimi seçeneklerini tanımlayın
Azure AD toomanage bir karma kimlik altyapısı kullanmanın bir avantajı hello işlem hello son kullanıcının açısından tamamen saydam olmasıdır. Merhaba kullanıcı tooaccess paylaşılan bir kaynak deneyecek, hello kaynak kimlik doğrulaması gerektirir, hello kullanıcı sipariş tooobtain içinde bir kimlik doğrulama isteği tooAzure AD belirteci hello ve hello kaynağa erişim toosend sahip olur. Tüm bu işlem, kullanıcı etkileşimi olmadan arka planda gerçekleşir. Aynı zamanda olası toogrant izin tooa olan [grup](active-directory-manage-groups.md#getting-started-with-access-management) sipariş tooallow kullanıcıların bunları tooperform ortak belirli eylemleri.

Genellikle veri gizliliğiyle ilgili endişeleri olan kuruluşlar veri sınıflandırması için kendi çözümü gerektirir. Geçerli şirket içi altyapısını zaten veri sınıflandırması kullanarak, kullanıcı kimliği için hello ana deposu olarak olası tooleverage Azure AD olur. Veri Sınıflandırması adlı için kullanılan şirket içi olduğundan emin genel bir aracı [veri sınıflandırma Araç Seti](https://msdn.microsoft.com/library/Hh204743.aspx) Windows Server 2012 R2 için. Bu araç tooidentify Yardım, sınıflandırmak ve özel bulut dosya sunucularında verileri korumak. Aynı zamanda olası tooleverage hello olan [otomatik dosya sınıflandırma](https://technet.microsoft.com/library/hh831672.aspx) Windows Server 2012 tooaccomplish içinde bu.

Kuruluşunuzun veri sınıflandırma yerinde yok ancak yeni sunucuları şirket içi eklemeden tooprotect hassas dosyalar gerekir, Microsoft kullanabileceklerini [Azure Rights Management hizmeti](https://technet.microsoft.com/library/JJ585026.aspx).  Azure RMS, dosyalarınızın ve e-posta şifreleme, kimlik ve yetkilendirme ilkeleri toohelp güvenli kullanır ve birden çok cihazda çalışır — telefonları, Tablet ve bilgisayar. Azure RMS bir bulut hizmeti olduğundan, gerek yoktur tooexplicitly, korumalı içeriği kendileriyle paylaşabilmek için öncelikle bu güvenleri diğer kuruluşlarla yapılandırın. Bir Office 365 veya Azure AD dizini zaten varsa, kuruluşlar arası işbirliği otomatik olarak desteklenir. Ayrıca, yalnızca, Azure RMS toosupport ortak bir kimlik, şirket içi Active Directory hesaplarınızı Azure Active Directory Eşitleme Hizmetleri (AAD eşitleme) veya Azure AD Connect kullanarak gerektiğini hello dizin özniteliklerini eşitleyebilirsiniz.

İçerik Yönetimi sürecinin hayati bir parçası hangi kaynağın erişen toounderstand, bu nedenle zengin günlüğe kaydetme özelliğine hello kimlik yönetimi çözümü için önemlidir. Azure AD günlük dahil olmak üzere 30 gün sağlar:

* Rol üyelik değişiklikleri (örn: kullanıcı eklenen tooGlobal Yönetici rolü)
* Kimlik bilgisi güncelleştirmeleri (örn: parola değişikliklerini)
* Etki alanı yönetimi (örn: bir etki alanı kaldırma özel bir etki alanı doğrulama)
* Ekleme veya uygulamaları kaldırma
* Kullanıcı Yönetimi (örn: ekleme, kaldırma, bir kullanıcı güncelleştirme)
* Ekleme veya lisanslarını kaldırma

> [!NOTE]
> Okuma [Microsoft Azure güvenlik ve Denetim Günlüğü Yönetimi](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow azure'da günlüğe kaydetme özellikleri hakkında daha fazla bilgi.
> Nasıl hello sorulara verdiğiniz yanıtlara bağlı olarak [içerik yönetimi gereklilikleri](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), karma kimlik çözümü içinde yönetilen içerik toobe hello biçiminizi mümkün toodetermine olmalıdır. Tablo 6'kullanıma sunulan tüm seçenekleri Azure AD ile tümleştirilebilen olsa da, iş gereksinimleriniz için daha uygun olan önemli toodefine var.
>
>

| İçerik yönetimi seçenekleri | Avantajları | Olumsuz yönleri |
| --- | --- | --- |
| Şirket içinde Merkezi (Active Directory Rights Management sunucusu) |Merhaba sunucu altyapısı hello verileri sınıflandırmak için sorumlu üzerinde tam denetim <br> Yerleşik yetenek Windows Server'daki ek lisans ya da abonelik gerek yoktur <br> Karma bir senaryoda Azure AD ile tümleşik <br> Exchange Online ve SharePoint Online ve Office 365 gibi Microsoft Online Services Bilgi Hakları Yönetimi (IRM) özelliklerini destekler <br> Exchange Server, SharePoint Server ve Windows Server ve dosya sınıflandırma altyapısı (FCI) çalıştıran dosya sunucuları gibi şirket içi Microsoft sunucu ürünlerini destekler. |Bu yana daha yüksek Bakım (Canlı yukarı güncelleştirmeler, yapılandırma ve olası yükseltmeleri), BT hello sunucu sahibi <br> Şirket içi sunucu altyapısı gerektirir<br> Doesn'tleverage Azure özelliklerini yerel olarak |
| (Azure RMS) Hello bulutta Merkezi |Daha kolay karşılaştırıldığında toomanage toohello içi çözüm <br> Karma bir senaryoda AD DS ile tümleştirilir. <br>  Azure AD ile tamamen tümleşik <br> Bir sunucu gerektirmeyen şirket içi sipariş toodeploy hello hizmeti <br> Destekleyen şirket içi Microsoft Exchange Server, SharePoint, sunucu ve Windows Server ve dosya sınıflandırma altyapısı (FCI) çalıştıran dosya sunucuları gibi sunucu ürünleri <br> BT, BYOK yeteneği kiracısının anahtarıyla tam denetime sahip olabilir. |Kuruluşunuz RMS'yi destekleyen bir bulut aboneliğine sahip olmalıdır <br> Kuruluşunuz Azure AD directory toosupport kullanıcı kimlik doğrulaması için RMS sahip olmalıdır |
| Karma (Azure RMS ile tümleşik, şirket içi Active Directory Rights Management sunucusu) |Bu senaryo hello avantajları hem, şirket içinde merkezi ve hello bulutta birikir. |Kuruluşunuz RMS'yi destekleyen bir bulut aboneliğine sahip olmalıdır <br> Kuruluşunuz Azure AD directory toosupport kullanıcı kimlik doğrulaması için RMS olmanız gerekir. <br> Azure bulut hizmeti arasında bir bağlantı gerektirir ve şirket içi altyapı |

## <a name="define-access-control-options"></a>Erişim denetim seçeneklerini tanımlayın
Merhaba kimlik doğrulaması yararlanarak, yetkilendirme ve erişim yetenekleri mümkün tooenable olacaktır Azure AD'de kullanılabilen, şirket toouse merkezi kimlik deposu kullanıcılar ve iş ortakları toouse çoklu oturum açma (SSO) hello gösterildiği gibi verirken denetim Aşağıdaki şekilde:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Merkezi Yönetim'i ve tam olarak diğer dizinleri ile tümleştirme

Şirket içi web uygulamaları ve Azure Active Directory SaaS uygulamalarının tek oturum açma toothousands sağlar. Merhaba okuyun [Azure Active Directory Federasyon Uyumluluğu Listesi: kullanılan tooimplement olabilecek üçüncü taraf kimlik sağlayıcıları çoklu oturum açma](https://msdn.microsoft.com/library/azure/jj679342.aspx) makale hello tarafından test edilmiş SSO üçüncü taraf hakkında daha fazla ayrıntı için Microsoft. Bu özellik kuruluş tooimplement B2B senaryolarını çeşitli hello kimlik ve erişim yönetimi denetimin tutarken sağlar. Ancak, işlem tasarlama hello sırasında B2B hello iş ortağı tarafından kullanılır ve bu yöntem Azure tarafından desteklenip desteklenmediğini doğrulamak önemli toounderstand hello kimlik doğrulama yöntemidir. Şu anda Azure AD tarafından desteklenen yöntemleri şunlardır:

* Güvenlik onaylama işlemi biçimlendirme dili (SAML)
* OAuth
* Kerberos
* Belirteçler
* Sertifikalar

> [!NOTE]
> Okuma [Azure Active Directory kimlik doğrulama protokolleri](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow her protokolü ve Azure özelliklerini hakkında daha ayrıntılı.
>
>

Hello Azure AD desteği, mobil iş uygulamalar kullanabilir kullanarak hello aynı kolay Mobile Services kimlik doğrulama deneyimi tooallow çalışanlar toosign kullanıcıların şirket Active Directory kimlik bilgileriyle mobil uygulamalarına. Bu özellik ile Azure AD Mobile Services'de kimlik sağlayıcısı ile hello desteklenir (hangi Microsoft Accounts, Facebook kimliği, Google kimliği ve Twitter kimliği dahil) zaten destekliyoruz diğer kimlik sağlayıcılardan. Merhaba içi hello şirketin AD DS bulunan kullanıcının kimlik bilgilerini kullanan hello uygulamalar, iş ortakları ve hello buluttan gelen kullanıcıların hello erişimden saydam olmalıdır. Kullanıcının koşullu erişim denetimi too(cloud-based) web uygulamaları, web API, Microsoft bulut Hizmetleri, 3 taraf SaaS uygulamalarında ve yerel (mobil) istemci uygulamaları yönetme ve güvenlik, hello yararları sahip denetimi, hepsi bir raporlama yerleştirin. Ancak, bir üretim dışı ortamda veya kullanıcılar ile sınırlı bir süre ile toovalidate bu önerilir.

> [!TIP]
> AD DS olduğu gibi Azure AD Grup İlkesi yok önemli toomention olur. Cihazlar için sipariş tooenforce ilkesindeki bir mobil cihaz yönetimi çözümü gibi gerekir [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Azure AD kullanarak Hello kullanıcı doğrulandıktan sonra kullanıcı hello erişim tooevaluate hello düzeyi olması önemlidir. Merhaba kullanıcı hello erişim düzeyini kaynak üzerinde sahip olur değişebilir, Azure AD denetleme erişim toosome kaynaklar tarafından bir ek güvenlik katmanı ekleyebilirsiniz, ancak hello kaynak kendisi de kendi erişim denetim listesi sahip göz önünde bulundurmanız ayrıca gerekir Ayrıca, bir dosya sunucusunda bulunan dosyalar için hello erişim denetimi gibi. Aşağıdaki Hello şekilde hello düzeyleri, karma bir senaryoda olabilir erişim denetimi özetlenmektedir:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Şekil X gösterdi hello diyagramdaki her etkileşim Azure AD tarafından kapsanan bir erişim denetimi senaryosunun temsil eder. Aşağıda, her senaryonun açıklaması vardır:

1. Olan koşullu erişim tooapplications şirket içinde barındırılan: uygulamalar toouse AD FS Windows Server 2012 R2 ile yapılandırılmış için kayıtlı cihazlara erişim ilkeleri ile kullanabilirsiniz. Şirket içi uygulamalara koşullu erişimi ayarlama hakkında daha fazla bilgi edinmek için bkz. [Azure Active Directory Cihaz Kaydı hizmetini kullanarak Şirket İçi Uygulamalara Koşullu Erişim](active-directory-conditional-access.md).

2. Erişim denetimi toohello Azure portalında: Azure de sağlar Denetim erişim toohello portal rol tabanlı erişim denetimi (RBAC) kullanarak). Bu yöntem hello şirket toorestrict hello tek bir hello Azure portalında yapabileceğiniz işlemleri miktarını sağlar. RBAC toocontrol erişim toohello portal kullanarak, BT yöneticilerinin erişim yönetimi yaklaşımlar aşağıdaki hello kullanarak erişim atayabilirsiniz:

* Grup tabanlı rol ataması: erişim yerel Active Directory'nizden eşitlenebilen tooAzure AD grupları atayabilirsiniz. Bu, kuruluşunuzun araçları ve grupları yönetmek için işlemlerdeki yaptı tooleverage hello mevcut yatırımların sağlar. Azure AD Premium hello temsilci Grup Yönetimi özelliği de kullanabilirsiniz.
* Azure rollerinde yerleşik Dengeleme: üç rol kullanabilirsiniz — sahibi, katkıda bulunan ve okuyucu tooensure kullanıcılar ve gruplar ihtiyaç duydukları toodo işlerini izni toodo yalnızca hello görevler sahiptir.
* Ayrıntılı erişim tooresources: roller toousers ve belirli bir abonelik, kaynak grubu veya bir Web sitesi veya veritabanı gibi ayrı bir Azure kaynak grupları atayabilirsiniz. Bu şekilde, kullanıcıların ihtiyaç duydukları tooall hello kaynaklarına erişmek ve toomanage gerekmez hiçbir erişim tooresources sahip olduğunuzdan emin olabilirsiniz.

> [!NOTE]
> Uygulamaları oluşturmak ve bunları toocustomize hello erişim denetimi istiyorsanız, olası toouse yetkilendirme için Azure AD uygulama rolleri de olur. Bu gözden [WebApp RoleClaims DotNet örnek](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) nasıl toobuild uygulama toouse bu yeteneği.
>
>

3. Microsoft Intune ile Office 365 uygulamaları için koşullu erişim: BT yöneticileri, koşullu erişim cihaz ilkeleri toosecure şirket kaynaklarına, hazırlayabilirsiniz, hello aynı uyumlu cihazların tooaccess hello izin bilgi çalışanları zaman sırada Hizmetler. Daha fazla bilgi edinmek için bkz. [Office 365 hizmetleri için Koşullu Erişim Cihaz İlkeleri](active-directory-conditional-access-device-policies.md).

4. Saas uygulamaları için koşullu erişim: [bu özellik](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) değil güvenilir bir ağ üzerinde tooconfigure uygulama başına çok faktörlü kimlik doğrulama erişim kuralları ve kullanıcılar hello özelliği tooblock erişimi sağlar. Atanan toohello uygulama ya da yalnızca içinde kullanıcılar için güvenlik grupları belirtilen hello çok faktörlü kimlik doğrulama kuralları tooall kullanıcılar uygulayabilirsiniz. Kullanıcıların hariç tutulamaz hello çok faktörlü kimlik doğrulaması gereksinimden bunlar Merhaba uygulaması bir IP adresinden söz konusu iç erişiyorsanız kuruluşun ağına hello.

Merhaba seçenekleri erişim denetimi için çok katmanlı bir yaklaşım kullandığından, bu seçenekler arasında karşılaştırma olmayan bu görev için uygulanabilir. Toocontrol tooyour kaynaklarına erişim gerektiren her senaryo için kullanılabilir tüm seçenekleri yararlanarak emin olun.

## <a name="define-incident-response-options"></a>Olay yanıtlama seçeneklerini tanımlayın
Azure AD BT tooidentity yetenek toogain görünürlük hello bütünlüğü ve güvenlik kuruluşunuzun dizininin kullanım raporları ve Azure AD erişim güvenlik riskleri kullanıcının etkinliği, BT izleme tarafından hello ortamında yararlanın olası yardımcı olabilir. Bu bilgi ile bir BT yöneticisi, böylece bunlar yeterli bu riskleri toomitigate planlayabilirsiniz olası güvenlik riskleri kalan daha iyi belirleyebilirsiniz.  [Azure AD Premium aboneliği](active-directory-get-started-premium.md) BT tooobtain bu bilgileri etkinleştirebilirsiniz güvenlik raporları kümesi vardır. [Azure AD raporları](active-directory-view-access-usage-reports.md) aşağıda gösterildiği gibi kategorilere ayrılır:

* **Kural dışı durum raporları**: oturum açma olayları toobe anormal bulduk olduğunu içerir. Amacımız toomake olduğundan, bu tür etkinliğini kullanan ve toobe mümkün toomake bir olay şüpheli olup olmadığı hakkında bir belirleme etkinleştirin.
* **Uygulama rapor tümleşik**: Bulut uygulamalarını, kuruluşunuzda nasıl kullanıldığını içine Öngörüler sağlar. Azure Active Directory bulut uygulamalarını binlerce ile tümleştirme sağlar.
* **Hata raporlarını**: hesapları tooexternal uygulamalar sağlama sırasında meydana gelebilecek hatalarını gösterir.
* **Kullanıcıya özgü raporları**: Aygıt/oturum belirli bir kullanıcı için etkinlik verileri görüntüleyebilirsiniz.
* **Etkinlik günlükleri**: hello son 24 saat, son 7 gün içindeki tüm Denetlenen olayları kaydını içeren veya son 30 gün yanı sıra grup etkinlik değişikliklerini ve parola sıfırlama ve kayıt etkinliği.

> [!TIP]
> Olay yanıtı ekip bir servis talebi üzerinde çalışması hello yardımcı olabilecek başka bir hello rapordur [sızan kimlik bilgilerine sahip kullanıcı](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) rapor.  Bu rapor, bu sızan kimlik bilgileri listesi ve Kiracı arasında eşleşmeleri ortaya çıkarır.
>
>

Diğer önemli raporlarda bir olay yanıtlama İnceleme sırasında kullanılan Azure AD'de oluşturulmuş ve şunlardır:

* **Parola sıfırlama etkinliği**: hello Yöneticisi ne kadar etkin parola sıfırlama hello kuruluşunuzda kullanılan içine Öngörüler sağlar.
* **Parola sıfırlama kayıt etkinlik**: içine kullanıcılar parola sıfırlama için kendi yöntemlerini kaydettirdiğiniz Öngörüler sağlar ve hangi yöntemlerin seçili.
* **Grup etkinlik**: değişiklikler toohello grubu geçmişini sağlar (örn: eklenen veya kaldırılan kullanıcılar) hello erişim paneli başlatılan.

Ayrıca toohello çekirdek raporlama özelliği Azure AD Premium bir olay yanıtı araştırma işlemi sırasında BT de yararlanılabilir kullanılabilir yararlanan denetim rapor tooobtain bilgileri gibi:

* Rol üyelik değişiklikleri (örn: kullanıcı eklenen tooGlobal Yönetici rolü)
* Kimlik bilgisi güncelleştirmeleri (örn: parola değişikliklerini)
* Etki alanı yönetimi (örn: bir etki alanı kaldırma özel bir etki alanı doğrulama)
* Ekleme veya uygulamaları kaldırma
* Kullanıcı Yönetimi (örn: ekleme, kaldırma, bir kullanıcı güncelleştirme)
* Ekleme veya lisanslarını kaldırma

Olay yanıtlama Hello seçeneklerini çok katmanlı bir yaklaşım kullandığından, bu seçenekler arasında karşılaştırma olmayan bu görev için uygulanabilir. Toouse Azure AD raporlama özelliği, şirketinizin olay yanıtlama işleminin parçası olarak gerektiren her senaryo için kullanılabilir tüm seçenekleri yararlanarak emin olun.

## <a name="next-steps"></a>Sonraki adımlar
[Karma kimlik yönetimi görevleri belirleme](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Ayrıca Bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)
