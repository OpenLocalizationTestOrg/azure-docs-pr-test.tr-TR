---
title: "Azure AD Connect eşitleme: yanlışlıkla silmeleri engelleme | Microsoft Docs"
description: "Bu konu, hello açıklar Azure AD Connect özelliği (yanlışlıkla silmeleri engelleme) yanlışlıkla silmeleri engelleme."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Azure AD Connect Eşitleme: Yanlışlıkla Silmeleri Engelleme
Bu konu, hello açıklar Azure AD Connect özelliği (yanlışlıkla silmeleri engelleme) yanlışlıkla silmeleri engelleme.

Azure AD Connect yükleme engellediğinizde yanlışlıkla silmeleri, varsayılan olarak etkindir ve yapılandırılmış toonot izin verme ile 500'den fazla siler. Bu özellik, yanlışlıkla yapılandırmadan ve çok sayıda kullanıcı ve diğer nesneleri etkileyecek tooyour şirket içi dizin değiştirir tasarlanmış tooprotect olur.

## <a name="what-is-prevent-accidental-deletes"></a>Ne yanlışlıkla silmeleri engelleme olduğu
Dahil birçok siler gördüğünüzde yaygın senaryolar:

* Çok değiştirir[filtreleme](active-directory-aadconnectsync-configure-filtering.md) tüm burada [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) veya [etki alanı](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) seçildiyse.
* Bir OU'daki tüm nesneler silinir.
* Bir OU içindeki tüm nesneleri eşitleme için kapsam dışına toobe kabul edilen biçimde adlandırılır.

PowerShell ile Merhaba varsayılan değer 500 nesnelerin değiştirilebilir kullanarak `Enable-ADSyncExportDeletionThreshold`. Bu değer toofit hello boyutu, kuruluşunuzun yapılandırmanız gerekir. Merhaba eşitleme Zamanlayıcı 30 dakikada bir çalışır olduğundan, hello değer hello 30 dakika içinde görülen siler sayısıdır.

Varsa hello dışa aktarma durur ve böyle bir e-posta alırsınız sonra çok sayıda hazırlanan siler toobe tooAzure AD, dışarı:

![E-posta yanlışlıkla silmeleri engelleme](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Merhaba (teknik kişi). (Zaman) silme hello sayısı (kuruluş adı) için hello yapılandırılmış silme eşiği aşıldı hello kimlik eşitleme hizmeti algıladı. (Sayı) toplam nesneleri çalıştırmak bu kimlik eşitleme silinmek gönderildi. Bu karşıladığında veya (sayı) nesneleri yapılandırılmış hello silme eşik değerini aştı. Bu silme işlemlerini olmalıdır tooprovide onay ihtiyacımız ilerlemeden önce işlenir. Lütfen bu e-posta iletisinde listelenen hello hata hakkında daha fazla bilgi için yanlışlıkla silmeleri engelleme hello bakın.*
>
> 

Ayrıca hello durumunu görebilirsiniz `stopped-deletion-threshold-exceeded` hello baktığınızda **Eşitleme Hizmeti Yöneticisi'ni** hello verme profili için kullanıcı Arabirimi.
![Eşitleme Hizmeti Yöneticisi kullanıcı Arabirimi yanlışlıkla silmeleri engelleme](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Beklenmeyen olduysa, araştırın ve düzeltici eylemleri gerçekleştirin. nesneler hakkında toobe silinmiş olan toosee hello aşağıdaki:

1. Başlat **eşitleme hizmeti** hello Başlat menüsü gelen.
2. Çok Git**Bağlayıcılar**.
3. Select hello bağlayıcı türü olan **Azure Active Directory**.
4. Altında **Eylemler** toohello sağa, select **arama bağlayıcı alanı**.
5. Merhaba altında açılır içinde **kapsam**seçin **bağlantısı kesilmiş beri** ve hello son bir saat seçin. Tıklatın **arama**. Bu sayfa silinmiş toobe hakkında tüm nesnelerin bir görünümünü sağlar. Her öğe tıklayarak hello nesne hakkında ek bilgi alabilirsiniz. Tıklatarak **sütun ayarı** tooadd ek öznitelikler toobe hello kılavuzunda görünür.

![Bağlayıcı alanı arama](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Ardından tüm hello siler isterseniz, aşağıdaki hello:

1. Merhaba PowerShell cmdlet'ini çalıştırın tooretrieve hello geçerli silme eşiği, `Get-ADSyncExportDeletionThreshold`. Bir Azure AD genel yönetici hesabı ve parolası belirtin. Merhaba varsayılan değer 500'dür.
2. tootemporarily bu korumayı devre dışı bırakın ve Git, hello PowerShell cmdlet'ini çalıştırın bu siler izin verin: `Disable-ADSyncExportDeletionThreshold`. Bir Azure AD genel yönetici hesabı ve parolası belirtin.
   ![Kimlik Bilgileri](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Hello Azure Active Directory Bağlayıcısı seçiliyken hello bir eylem seçin **çalıştırmak** seçip **verme**.
4. toore etkinleştir hello koruma, Hello PowerShell cmdlet'ini çalıştırın: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. 500 hello geçerli silme eşiği alınırken fark hello değerle değiştirin. Bir Azure AD genel yönetici hesabı ve parolası belirtin.

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
