---
title: "aaaTroubleshoot tooAzure AD eşitlemiyor nesneyi | Microsoft Docs"
description: "Bir nesne tooAzure AD eşitlemiyor neden sorunlarını giderin."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>TooAzure AD eşitlemiyor nesneyi sorun giderme

Bir nesne beklenen tooAzure AD eşitlemiyor, nedeniyle birkaç nedeni olabilir. Bir hata e-posta Azure AD'den alınan veya Azure AD Connect Health hello hataya bakın, sonra okuma [verme hatalarında sorun giderme](active-directory-aadconnect-troubleshoot-sync-errors.md) yerine. Ancak hello nesnesi Azure AD içinde olduğu bir sorun gideriyorsanız, ardından bu konu sizin için. Bunu nasıl toofind hataları hello şirket içi bileşeninde Azure AD Connect eşitleme açıklar.

toofind hello hataları toolook sırasının hello birkaç farklı yerlerde kalacaklarını:

1. Merhaba [işlem günlükleri](#operations) içeri aktarma ve eşitleme sırasında hello eşitleme altyapısı tarafından tanımlanan hataları bulmak için.
2. Merhaba [bağlayıcı alanı](#connector-space-object-properties) eksik nesneler ve Eşitleme hataları bulmak için.
3. Merhaba [meta veri deposu](#metaverse-object-properties) veri ilgili sorunları bulmak için.

Başlat [Eşitleme Hizmeti Yöneticisi'ni](active-directory-aadconnectsync-service-manager-ui.md) adımları başlamadan önce.

## <a name="operations"></a>İşlemler
Merhaba işlemleri hello Synchronization Service Manager sorun gidermeyi nereden başlamanız sekmesindedir. Hello işlemleri sekmesinde hello en son işlemleri hello sonuçlarını gösterir.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

Merhaba üst yarı tüm metinler chronic sırayla gösterir. Varsayılan olarak, hello işlemleri günlük hello hakkında bilgi son yedi gün korur, ancak bu ayar ile Merhaba değiştirilebilir [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md). Başarı durumunu göstermez herhangi çalıştırmak için toolook istiyor. Merhaba üstbilgilerini tıklatarak sıralama hello değiştirebilirsiniz.

Merhaba **durum** hello en önemli bilgileri bir sütundur ve hello bir çalıştırma için en önemli bir sorun gösterir. Merhaba en yaygın durumları tooinvestigate öncelik sırasına göre hızlı bir özeti aşağıda verilmiştir (burada * birkaç olası hata dizeleri gösterir).

| Durum | Açıklama |
| --- | --- |
| durdurulmuş-* |çalıştırma hello tamamlanamadı. Örneğin, hello uzak sistem kapalı ve bağlantı kurulamıyor. |
| durduruldu-hata-sınırı |5. 000'den fazla hataları vardır. çalıştırma hello otomatik olarak toohello çok sayıda hata durduruldu. |
| Tamamlanan -\*-hataları |Merhaba tamamlanmış çalıştırın, ancak araştırılması gereken bir hata (daha az 5.000). |
| Tamamlanan -\*-uyarıları |Merhaba çalıştırma tamamlandı, ancak bazı verileri beklenen hello durumda değil. Hatalar varsa, bu ileti genellikle yalnızca bir belirti içindir. Hataları ele kadar uyarıları araştırmanız gereken değil. |
| başarılı |Sorunu yok. |

Bir satır seçtiğinizde, hello alt tooshow hello ayrıntılarını çalıştıran güncelleştirir. toohello hello sonuna kadar sol, liste bildiren olabilir **adım #**. Burada her etki alanı adımı tarafından temsil edilen ormanınızdaki birden çok etki alanı varsa, bu listede yalnızca görünür. Merhaba etki alanı adı hello başlığı altında bulunabilir **bölüm**. Altında **eşitleme istatistikleri**, hello işlenen değişikliklerin sayısı hakkında daha fazla bilgi bulabilirsiniz. Merhaba bağlantılar tooget değiştirilen hello nesnelerin bir listesini tıklatabilirsiniz. Hatalarla nesneniz varsa, bu hataları altında görünmesini **eşitleme hatalarını**.

### <a name="troubleshoot-errors-in-operations-tab"></a>İşlemler sekmesinde hatalarında sorun giderme
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Hatalar varsa, her iki hello nesnesinde hata ve hello hata kendisini daha fazla bilgi sağlayan bağlantıları verilmiştir.

Merhaba hata dizesi tıklayarak başlangıç (**eşitleme kuralı-hata-işlevi-tetiklenen** hello resimdeki). İlk hello nesnesine bir bakış sunulmuştur. toosee hello gerçek bir hata hello düğmesini **yığın izleme**. Bu izleme hello hatası için hata ayıklama düzeyi bilgileri sağlar.

Hello sağ **çağrı yığını bilgileri** kutusunda, seçin **Tümünü Seç**, ve **kopya**. Sonra hello yığını kopyalayın ve Not Defteri gibi sık kullanılan, Düzenleyicisi'nde hello hatasında bakın.

* Merhaba hata ise **SyncRulesEngine**, hello çağrı yığını bilgileri, tüm özniteliklerin listesini ilk hello nesnesinde yok. daha sonra. Merhaba başlık görene kadar aşağı kaydırın **InnerException = >**.  
  ![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  hata gösterir hello sonra hello satırı. Yukarıdaki Hello resim içinde bir özel eşitleme kuralı oluşturulan Fabrikam hello hata var.

Ardından Hello hata kendisini yeterli bilgi sağlamaz, zaman toolook hello veri kendisini olur. Merhaba nesne tanımlayıcısı ile Merhaba bağlantısına tıklayın ve hello sorun giderme devam [bağlayıcı alanı içeri aktarılan nesnenin](#cs-import).

## <a name="connector-space-object-properties"></a>Bağlayıcı alanı nesne özellikleri
Hello bulunan herhangi bir hata yoksa [operations](#operations) sekmesinde toofollow hello bağlayıcı alanı nesne Active Directory, toohello meta veri deposu ve tooAzure AD hello sonraki adım ise. Bu yolda hello sorun olduğu bulmanız gerekir.

### <a name="search-for-an-object-in-hello-cs"></a>Merhaba CS nesnesi için arama

İçinde **Eşitleme Hizmeti Yöneticisi'ni**, tıklatın **Bağlayıcılar**, select hello Active Directory Bağlayıcısı ve **arama bağlayıcı alanı**.

İçinde **kapsam**seçin **RDN** (istediğinizde hello CN öznitelikte toosearch) veya **DN ya da bağlantı** (istediğinizde hello distinguishedName öznitelikte toosearch). Bir değer girin ve tıklayın **arama**.  
![Bağlayıcı alanı arama](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Merhaba nesne bulamazsanız, aradığınız sonra onu ile filtrelendi [etki alanı tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) veya [OU tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Okuma hello [filtrelemeyi yapılandırma](active-directory-aadconnectsync-configure-filtering.md) filtreleme hello konu tooverify beklendiği şekilde yapılandırılır.

Başka bir yararlı arama tooselect hello Azure AD Bağlayıcısı bulunduğu **kapsam** seçin **bekleyen alma**ve select hello **Ekle** onay kutusu. Bu arama bir şirket içi nesne ile ilişkili olamaz Azure AD'de tüm eşitlenmiş nesnelerin sağlar.  
![Bağlayıcı alanı arama artık](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Bu nesneleri başka bir eşitleme altyapısı veya farklı bir filtreleme yapılandırması ile eşitleme altyapısı tarafından oluşturuldu. Bu görünüm listesidir **artık** artık yönetilen nesneleri. Bu listeyi gözden geçirin ve hello kullanarak bu nesneleri kaldırmayı düşünün [Azure AD PowerShell](http://aka.ms/aadposh) cmdlet'leri.

### <a name="cs-import"></a>CS alma
Cs nesnesini açtığınızda, hello üstünde birkaç sekme vardır. Merhaba **alma** sekmesi bir içeri aktarma işleminden sonra hazırlanan hello veriler gösterir.  
![CS nesnesi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Merhaba **eski değer** ne şu anda Bağlan ve hello depolanan gösterir **yeni değer** ne hello kaynak sistemden alınan ve henüz uygulanmadı. Merhaba nesnesinde bir hata varsa, değişiklikler işlenmez.

**Hata**  
![CS nesnesi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Merhaba **eşitleme hatası** sekmesini görülebilir yalnızca hello nesne ile ilgili bir sorun varsa. Daha fazla bilgi için bkz: [eşitleme hatalarını giderme](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>CS çizgileri
Merhaba çizgileri sekmesini nasıl hello bağlayıcı alanı nesne ilgili toohello meta veri deposu nesne gösterilir. Merhaba bağlayıcı son değişiklik aktarıldığında bağlı sistem hello ve meta veri deposu, uygulanan kurallar toopopulate veri hello görebilirsiniz.  
![CS çizgileri](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
Merhaba, **eylem** sütunu, bir görebilirsiniz **gelen** eşitleme kuralı hello eylemiyle **sağlama**. Bu bağlayıcı alanı nesne mevcut olduğu sürece hello meta veri deposu nesne kalır gösterir. Eşitleme kuralları Hello listesini bunun yerine bir eşitleme kuralının yönünde gösterir, **giden** ve **sağlama**, hello meta veri deposu nesnesi silindiğinde, bu nesne silindi gösterir.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
Hello de görebilirsiniz **PasswordSync** gelen bağlayıcı alanı hello sütun bir eşitleme kuralı başlangıç değeri varsa bu yana değişiklikler toohello parola katkıda **doğru**. Bu parolayı tooAzure AD hello giden kuralı üzerinden gönderilir.

Merhaba çizgileri sekmesinden tıklayarak toohello meta veri deposu alabilirsiniz [meta veri deposu nesne özellikleri](#mv-attributes).

Tüm sekmeler Hello altındaki iki düğme vardır: **Önizleme** ve **günlük**.

### <a name="preview"></a>Önizleme
Merhaba Önizleme sayfası kullanılan toosynchronize tek tek nesnesidir. Bazı özel eşitleme kuralları sorun giderme ve tek bir nesne üzerinde yapılan bir değişiklik toosee hello etkisi istiyorsanız kullanışlıdır. Aşağıdaki seçeneklerden birini seçebilirsiniz **tam eşitleme** ve **Delta eşitleme**. Arasında seçim yapabilirsiniz **oluşturmak Önizleme**, hangi yalnızca tutar hello değişiklik bellekte ve **Commit Önizleme**hello meta veri deposu güncelleştirildiği ve tüm aşamaları tootarget bağlayıcı alanları değiştirir.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Merhaba nesne ve belirli öznitelik akışı için hangi kuralın uygulanacağı inceleyebilirsiniz.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Günlük
Merhaba günlük kullanılan toosee hello parola eşitleme durumunu ve geçmişini sayfasıdır. Daha fazla bilgi için bkz: [parola eşitleme sorunlarını giderme](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Meta veri deposu nesne özellikleri
Active Directory hello kaynağından arama genellikle daha iyi toostart olan [bağlayıcı alanı](#connector-space). Ancak, hello meta veri deposu arama başlatabilirsiniz.

### <a name="search-for-an-object-in-hello-mv"></a>Merhaba MV nesnesi için arama
İçinde **Eşitleme Hizmeti Yöneticisi'ni**, tıklatın **meta veri deposu arama**. Bulur hello kullanıcı bildiğiniz bir sorgu oluşturun. AccountName (sAMAccountName) ve userPrincipalName gibi ortak öznitelikleri için arama yapabilirsiniz. Daha fazla bilgi için bkz: [meta veri deposu arama](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

Merhaba, **arama sonuçları** penceresinde hello nesnesine tıklayın.

Merhaba nesne bulamadı, ardından bunu henüz hello meta veri deposu ulaştı değil. Merhaba Active Directory toosearch hello nesnesinin devam [bağlayıcı alanı](#connector-space-object-properties). Gelen gelecek toohello meta veri deposu hello nesnesinden engelleyen bir hata olabilir veya bir filtre uygulanmış olabilir.

### <a name="mv-attributes"></a>MV öznitelikleri
Merhaba öznitelikler sekmesinde hangi bağlayıcı katkıda bulunan ve başlangıç değerleri görebilirsiniz.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Bir nesne eşitlemiyor, ardından hello meta veri deposu öznitelikleri aşağıdaki hello bakın:
- Merhaba özniteliği **cloudFiltered** sunmak ve çok ayarlamak**true**? Bunun ardından, toohello adımlarda göre filtre uygulanmış [özniteliği tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- Merhaba özniteliği **sourceAnchor** var? Değilse, bir hesap-kaynak orman topolojisini var mı? Bir nesne bağlı bir posta kutusu tanımladıysanız (Merhaba özniteliği **msExchRecipientTypeDetails** başlangıç değeri 2), hello sourceAnchor etkinleştirilmiş bir Active Directory hesabı ile Merhaba orman tarafından katkıda bulunan sonra. Hello yöneticisi hesap içeri aktarılan ve doğru eşzamanlı emin olun. hello Hello yönetici hesabı listelenen [Bağlayıcılar](#mv-connectors) hello nesnesi.

### <a name="mv-connectors"></a>MV bağlayıcılar
Merhaba bağlayıcılar sekmesi hello nesne gösterimini sahip tüm bağlayıcı alanları gösterir.  
![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
Bir bağlayıcı olmalıdır:

- Her bir Active Directory orman hello kullanıcı olarak temsil edilir. Bu gösterim foreignSecurityPrincipals ve kişi nesneleri içerebilir.
- Azure AD'de bağlayıcı.

Merhaba bağlayıcı tooAzure AD eksikse, ardından okuma [MV öznitelikleri](#MV-attributes) olan tooverify hello ölçütlerini tooAzure AD sağlandı.

Bu sekme ayrıca toonavigate toohello sağlar [bağlayıcı alanı nesne](#connector-space-object-properties). Bir satır seçin ve tıklatın **özellikleri**.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
