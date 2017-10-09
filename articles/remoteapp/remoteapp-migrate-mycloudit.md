---
title: "Azure RemoteApp için aaaChange hello fatura | Microsoft Docs"
description: "Bilgi toostop Azure RemoteApp için fatura nasıl."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 8f94da9a-7848-4ddc-b7b7-d9c280ccf4d7
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: mbaldwin
ms.openlocfilehash: fe3841a88978ec56829932621489e75d5dd7e673
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-azure-remoteapp-toomycloudit"></a>Azure RemoteApp tooMyCloudIT geçirme 

**Şu anda Microsoft Azure RemoteApp kullanıyor musunuz?** : MyCloudIT yerleşik bir otomatik aracı toomigrate Azure RemoteApp (ARA) collection(s) toohello MyCloudIT Yönetimi platformunuz Microsoft Azure üzerinde toorun devam ederken.

**Hello Azure Resource Manager portal yararlanmak**: Merhaba MyCloudIT platform içine tamamlanan geçiş anında erişim tooAzure'nın yeni Azure Resource Manager portal sağlar. Yenilikler Microsoft Azure tarafından sunulan erişim tooVirtual makine boyutlarını tooensure de dahil olmak üzere, dağıtımınızı toosupport hello işletmenizin gereksinimlerine yerleşik olarak bulunur ve bu portalı tüm hello yeni özellikler içerir.

**Paralel tooensure hello doğru çözümü gereksinimlerinize test**: Merhaba MyCloudIT geçiş aracı tooinitiate hello geçiş işlemi ve paralel süre geçerli ARA kullanıcılarınızın devam toouse ARA test oluşturulur.  Kullanıcılarınızın geçişinizi kadar ARA içinde kalır ve testi tamamlandı.  Merhaba geçiş aracı toohandle hello tipik ARA koleksiyonu yerleşik olarak bulunur.  Düşünüyorsanız lütfen bizimle iletişime geçin benzersiz, standart olmayan bir senaryo varsa [ sales@conexlink.com ](mailto:sales@conexlink.com) uyarlanmış planı tooassist geçişinizi ile sağlayabilir.

**Hizmet olarak masaüstü özellikleri**: Lütfen unutmayın MyCloudIT yalnızca için alışkın hello RemoteApp özellikler sunar, ancak ayrıca tam masaüstü-bir hizmet olarak sunuyoruz hello yeteneklerini aynı maliyet en az bir kullanıcı olmaksızın aylık gereksinimleri.

## <a name="what-we-will-do-for-you"></a>Biz sizin için ne yapacağını

MyCloudIT hello geçiş hello Klasik Azure portalından, abonelik toohello aboneliğinizin bizim otomatik geçiş aracı ile Azure Resource Manager Portal, Azure RemoteApp şablonunuzun otomatikleştirir.  

> [!NOTE]
> özgün Azure RemoteApp dağıtımınızı aynı Azure bölgesinde hello Hello Azure RemoteApp şablon kalmalıdır.  Merhaba geçiş sırasında toochange Azure bölgeleri ya da Azure abonelik ihtiyacınız varsa, bize ek yönergeler için temasa [ sales@conexlink.com ](mailto:sales@conexlink.com).

Merhaba MyCloudIT geçiş aracı hello otomatik geçiş işlemine ilişkin ayrıntılı bilgi için aşağıda okuyun:

1. Merhaba geçiş aracı, tüm var olan ARA dağıtımlar için geçerli Abonelikleriniz tarar.  
2. Bir ARA koleksiyonu toomigrate aynı anda seçin.  Birden çok koleksiyon varsa, sunduğumuz aracı birden çok kez çalıştırın.
3. Eski veri almak veya el ile UPD toohello yeni dağıtım eşlemek için hello seçeneği toocopy hello kullanıcı profili diskleri (UPD) tooyour yeni dağıtım sahip. UPD toocopy seçerseniz, biz hello UPD kaydetmek ve hello UPD ad tooeach kullanıcıların ad eşleyen bir metin dosyası içerir.  Merhaba UPD kopyalanan tooa hello RDSMGMT Sunucusu paylaşımında olacaktır `F:\Shares\LegacyUPD` ve hello paylaşım yoluyla kullanıma `\\RDSmgmt\LegacyUPD`. 
4. Geçişinizi geçerli ARA dağıtımınız için kapalı kalma süresi gerektirir.  Ancak, yapılan herhangi bir değişiklik toohello UPD (ARA) sonra hello kopyalama, bu değişiklikleri hello Azure Resource Manager portalında saklanan hello UPD içinde yansıtılmaz. 
5. İçinde etki alanı denetleyicileri gibi ek VM'ye sahip ve sanal ağ varolan Klasik Azure sanal ağınız arasında eşleme biz Klasik Azure sanal ağınızda dosya sunucuları kuracak ve hello yeni bir sanal ağ biz için oluşturursanız, yeni Azure kaynak hello Yönetici portalı.
6. Otomatik çözümümüzdür yalnızca sanal ağ varolan Klasik Azure sanal ağınız arasında eşleme kurmak ve var olan ARA dağıtımınızı karma bir dağıtım ise yeni bir sanal ağ hello; yani, bir Windows Server Active Directory etki alanı denetleyicisi Klasik sanal ağı varolan hello ile doğrulama. Biz koleksiyonunuz için VNet eşlemesi kurma değil, ancak sanal ağ eşleme gerektirir, lütfen bize olarak başvurun [ sales@conexlink.com ](mailto:sales@conexlink.com) ve biz mutluluk tooconfigure hiçbir ek ücret VNet eşlemesi olacaktır.
7. Azure DNS yapılandırmanızı güncelleştirilir otomatik çözümümüzdür sağlayacak hello yeni sanal ağ ayarlarını tooensure ile etki alanı denetleyicisi hello varolan tooyour yeni dağıtımınızı bağlanabilir Klasik VNet.
8. Otomatik çözümümüzdür bu yeni bir sanal ağ oluşturmak ve hello var olan Windows Server Active Directory Server sahip dağıtımlar için VNet eşlemesi oluşturmak gibi hiçbir IP adresi çakışmalarını olduğundan emin.
9. Kimlik doğrulaması için yalnızca Azure AD kullanıyorsanız MyCloudIT yeni bir Windows Server Active Directory etki alanı oluşturma ve Azure AD Connect toosynchronize kullanıcılar hello mevcut Azure AD örneğiyle yeni Windows Server Active Directory etki alanı oluşturulan hello arasında kullanma MyCloudIT tarafından.
10. Windows Server Active Directory etki alanı tooauthenticate ARA kullanıcıların kullanıyorsanız, otomatik çözümümüzdür VNet eşlemesi aracılığıyla Windows Server Active Directory etki alanı denetleyicisi var, yeni MyCloudIT dağıtım tooyour bağlanır.
11. Azure Active Directory etki alanı Hizmetleri kimlik doğrulaması kullanıyorsanız, size geçiş ancak biz bir özel geçiş planı sizin için oluşturabilmesi için lütfen bizimle iletişime geçin.  Lütfen bir e-posta çok gönderin[sales@conexlink.com](mailto:sales@conexlink.com). 
12. Merhaba koleksiyonu toobe geçirilen sonra Onaylandı, arkanıza yaslanın ve otomatik çözümümüzdür ARA toplama ve kullanıcı profili diskleri (isteğe bağlı) toohello yeni güdümlü MyCloudIT uzak uygulamalar çözümün geçirir sırada hafifletin.
13. Merhaba dağıtım tamamlandıktan sonra biz yeniden yayımlayacak hello içinde ARA yayımlanan aynı uygulamaları ve mümkün toopublish ek uygulamalar, gereken dağıtım sonrasında.

## <a name="post-migration-benefits"></a>POST geçiş avantajları

1. Uzak uygulamalar dağıtımınızın toomanage hello tam yaşam verir hello Yönetim Konsolu sunuyoruz.
2. Bizim portalından, sanal makineleri mümkün toomanage olacaktır.  Başlatma / durdurma ve gerekirse tek tek sanal makineleri yeniden boyutlandırın.
3. Merhaba Yönetim Konsolu sağlar ve kullanıcıları yönetme yeteneği toocreate hello / grupları bizim Yönetim Portalı'ndan.
4. Merhaba Yönetim Konsolu hello özelliği toosynchronize Office 365 toocreate kullanıcılarla aynı oturum açma deneyimi sağlar.
5. Merhaba Yönetim Konsolu sağlar hello özelliği toocreate ek RemoteApp ve Masaüstü koleksiyonları yinelenen kullanıcı maliyetleri veya en düşük kullanıcı gereksinimleri olmadan. 
6. Merhaba Yönetim Konsolu toopublish yeni uzak uygulamalar uygulamaları hello yeteneği sağlar.
7. çözümünüzü yalnızca belirli saatlerde gerekiyorsa hello özelliği tooschedule hello başlatma ve kapatma, uzak uygulamalar dağıtımınızın hello Yönetim Konsolu sağlar.
8. Merhaba özelliği tooautomate hello yükleme ve yapılandırma, müşteri verileri için bir belge bekletme geçmişini sağlayan hello Azure yedekleme Aracısı'nın Hello Yönetim Konsolu sağlar.
9. Merhaba Yönetim Konsolu, dağıtımınızın erişim tooperformance ölçümleri sağlar.  Ek performans yönetim araçlarını yükleme olmadan tüm olası performans sorunları özelliği tooidentify hello kazandırır.
10. Birden çok oturumu ana bilgisayar varsa, bu nedenle yalnızca hello oturum çalıştıran toobe gereken ana çalışan ölçeklendirme yapabilir tooenable otomatik olacaktır.
11. MyCloudIT toohello RDWeb ağ geçidi üzerinden erişilemiyor. sunucu MyCloudIT etki alanı adı sağlar.  Ayrıca hello özelliği toore eşleme hello tooa özel URL'si markalama son kullanıcıdan sunuyoruz.

## <a name="prerequisites-for-migration"></a>Geçiş için Önkoşullar

1. Erişim toohello geçerli Azure RemoteApp çözümünüzü barındıran Azure aboneliğinizin olması gerekir.
2. Bizim portal, abonelik toomigrate içinde şablon ve toocreate izinleri / yeni MyCloudIT dağıtımınızı değiştirin.
3. Azure RemoteApp içinde tooa sınırlama, her bir koleksiyon yalnızca üç kez geçirilebilir olduğunu unutmayın.  Üç defadan fazla toomigrate koleksiyonu gerekiyorsa, bir bilet tooAzure tooincrease verme sayınız yükseltmek veya bizimle iletişime geçin ve hello ARA isteği tooincrease hello verme sayıma yardımcı olacaktır.

## <a name="mycloudit-billing"></a>MyCloudIT faturalama

Lütfen bakın [MyCloudIT fiyatlandırma RemoteApp çözümleri için](https://mcitdocuments.blob.core.windows.net/terms/MyCloudIT_Pricing_Overview.pdf) (PDF) hakkında bilgi için toopredict ve genel Azure maliyetleriniz yönetin.

Hala sorularınız varsa lütfen bizimle iletişime geçin [ sales@conexlink.com ](mailto:sales@conexlink.com) veya hello tam tanıtım videosunu izleyin [Azure RemoteApp geçiş aracı - MyCloudIT](https://www.youtube.com/watch?v=YQ_1F-JeeLM&t=482s). 

