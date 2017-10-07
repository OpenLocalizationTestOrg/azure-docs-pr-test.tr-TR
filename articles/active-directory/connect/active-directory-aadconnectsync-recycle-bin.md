---
title: "Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştirme | Microsoft Docs"
description: "Bu konuda, Azure AD Connect ile AD geri dönüşüm kutusu özelliğinin hello kullan önerir."
services: active-directory
keywords: "AD geri dönüşüm kutusu, yanlışlıkla silinmesi, kaynak bağlantısı"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect eşitleme: AD Geri Dönüşüm Kutusu'nu etkinleştir
Hello AD Geri Dönüşüm Kutusu özelliği, şirket içi Active eşitlenmiş tooAzure AD olan dizinleri için etkinleştirmeniz önerilir. 

Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi ve geri yükleme, hello özelliğini kullanarak, Azure AD yükler hello karşılık gelen Azure AD kullanıcı nesnesi.  Merhaba AD Geri Dönüşüm Kutusu özelliği hakkında daha fazla bilgi için tooarticle başvurun [senaryoya genel bakış geri silinmiş Active Directory nesneleri için](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Merhaba AD etkinleştirme avantajları geri dönüşüm kutusu
Bu özellik hello aşağıdakileri yaparak Azure AD kullanıcı nesneleri geri yüklemeye yardımcı olur:

* Şirket içi yanlışlıkla sildiyseniz AD kullanıcı nesnesi, hello karşılık gelen Azure AD kullanıcı nesnesi silinecek hello sonraki eşitleme döngüsü. Varsayılan olarak, Azure AD silinmiş hello Azure AD kullanıcı nesnesi 30 gün boyunca geçici olarak silinen durumda tutar.

* Şirket içi varsa AD Geri Dönüşüm Kutusu özelliği, etkin geri yükleyebilir, silinen hello AD Kullanıcı nesnesinin kaynak bağlantısı değerini değiştirmeden şirket. Ne zaman hello kurtarılan şirket içi AD kullanıcı nesnesi eşitlenir tooAzure AD, Azure AD geri geçici olarak silinen hello karşılık gelen Azure AD kullanıcı nesnesi. Kaynak bağlantısı özniteliği hakkında daha fazla bilgi için tooarticle başvurun [Azure AD Connect: tasarım kavramları](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Şirket içi yoksa AD Geri Dönüşüm Kutusu'nu özelliği etkinleştirilmiş, gerekli toocreate bir AD kullanıcı nesnesi tooreplace hello Silinmiş nesne olabilir. Azure AD Connect eşitleme hizmetinin yapılandırılmış toouse sistem tarafından oluşturulan AD özniteliği (örneğin, objectGUID) hello kaynak bağlantısı özniteliği için ise, hello yeni oluşturulan AD kullanıcı nesnesi değil sahip hello aynı kaynak bağlantısı değeri hello AD kullanıcı nesnesi silindi olarak. Azure AD Hello yeni oluşturulan AD kullanıcı nesnesi eşitlenmiş tooAzure AD olduğunda, yeni bir oluşturur geçici olarak silinen hello Azure AD kullanıcı nesnesi geri yerine Azure AD kullanıcı nesnesi.

> [!NOTE]
> Varsayılan olarak, Azure AD tutar geçici olarak silinen durumdaki Azure AD kullanıcı nesneler tamamen silinmeden önce 30 gün boyunca silindi. Bununla birlikte, Yöneticiler bu tür nesneleri hello silinmesini hızlandırabilir. Merhaba nesneler kalıcı olarak silinir sonra artık kurtarılabilir, bile içi bağlı AD Geri Dönüşüm Kutusu özelliği etkin hale gelir.



## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)

* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
