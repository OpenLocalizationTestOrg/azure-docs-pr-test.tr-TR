---
title: "Azure AD Connect eşitleme: hello AD DS hesap parolası değiştiriliyor | Microsoft Docs"
description: "Bu konuda belge tooupdate hello AD DS hesabı hello parola sonra Azure AD Connect nasıl değiştirilir açıklar."
services: active-directory
keywords: "AD DS hesabı, Active Directory hesap parolası"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a>Merhaba AD DS hesap parolasını değiştirme
Merhaba AD DS hesap şirket içi Active Directory ile Azure AD Connect toocommunicate tarafından kullanılan toohello kullanıcı hesabına başvuruyor. Merhaba AD DS hesabı hello parolasını değiştirirseniz, Azure AD Connect eşitleme hizmeti hello yeni parolayla güncelleştirmeniz gerekir. Aksi takdirde eşitleme artık doğru şekilde hello ile eşitleyebilirsiniz hello içi Active Directory ve aşağıdaki hatalar hello karşılaşırsınız:

* Hello Eşitleme Hizmeti Yöneticisi, içeri aktarma veya dışarı aktarma işlemi AD başarısız ile şirket içi **Hayır başlangıç kimlik** hata.

* Windows Olay Görüntüleyicisi'ni altında hello uygulama olay günlüğüne bir hata ile içeren **olay kimliği 6000** ve ileti **'hello yönetim Aracısı "contoso.com" başarısız toorun hello kimlik bilgileri geçersiz olduğundan'** .


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a>Nasıl tooupdate hello eşitleme hizmeti ile AD DS hesabı için yeni parola
Merhaba yeni parolayla tooupdate hello eşitleme hizmeti:

1. Merhaba Eşitleme Hizmeti Yöneticisi'ni (Başlangıç → eşitleme hizmeti) başlatın.
</br>![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)  

2. Toohello Git **Bağlayıcılar** sekmesi.

3. Select hello **AD Bağlayıcısı** toohello AD DS hesap parolası değiştirildi karşılık gelir.

4. Altında **Eylemler**seçin **özellikleri**.

5. Merhaba açılan iletişim kutusunda seçin **tooActive Directory ormanına Bağlan**:

6. Yeni bir parola Hello hello AD DS hesabının hello girin **parola** metin kutusu.

7. Tıklatın **Tamam** toosave hello yeni parola ve Kapat hello açılan iletişim.

8. Hello Azure AD Connect eşitleme hizmeti altında Windows Hizmet Denetimi Yöneticisi'ni yeniden başlatın. Tooensure budur, başvuru toohello eski parola hello bellek önbellekten kaldırılır.

## <a name="next-steps"></a>Sonraki adımlar
**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)

* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
