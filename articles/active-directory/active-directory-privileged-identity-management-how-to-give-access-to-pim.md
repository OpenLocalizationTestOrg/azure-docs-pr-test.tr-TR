---
title: "aaaHow toogive erişim tooPrivileged Kimlik Yönetimi - Azure | Microsoft Docs"
description: "PIM yönetilebilir tooadd rolleri toousers ile Azure Active Directory Privileged Identity Management uzantısı nasıl hello öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a>Erişim toomanage Azure AD Privileged Identity Management vermiş
Azure AD Privileged Identity Management (PIM) bir kuruluş için otomatik olarak etkinleştirir hello genel yönetici rol atamalarını almak ve tooPIM erişebilirsiniz. Hiç kimsenin yazma erişimi varsayılan olarak, ancak başka genel yöneticiler de dahil olmak üzere alır. Diğer genel yöneticileri, güvenlik yöneticileri ve güvenlik okuyucular salt okunur erişim tooAzure AD PIM sahiptir. toogive erişim tooPIM hello ilk kullanıcı atayabilirsiniz başkalarının toohello **ayrıcalıklı Rol Yöneticisi** rol. Bu atama gelen PIM içinde yapılmalıdır ve PowerShell veya diğer portallar değiştirilemez.

> [!NOTE]
> Azure AD PIM yönetme Azure MFA gerektirir. Microsoft hesapları için Azure MFA kaydedilemiyor olduğundan, bir Microsoft hesabıyla oturum açan bir kullanıcı Azure AD PIM erişemiyor.
> 
> 

Her zaman en az iki kullanıcılar ayrıcalıklı Rol Yöneticisi rolünde bir kullanıcı kilitli durumda veya kullanıcıların hesap silindi emin olun.

## <a name="give-another-user-access-toomanage-pim"></a>Başka bir kullanıcı erişimi toomanage PIM verin
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve select hello **Azure AD Privileged Identity Management** hello Pano uygulaması.
2. Seçin **yönetmek ayrıcalıklı rolleri** > **ayrıcalıklı Rol Yöneticisi** > **Ekle**.
   
    ![Ayrıcalıklı rol yöneticileri - ekran görüntüsü ekleme][1]
3. Merhaba yönetilen Kullanıcı Ekle dikey, 1. adım zaten tamamlanmış olur. 2. adımı seçin **kullanıcı seçin** ve arama hello kullanıcıdan tooadd istiyor.
   
    ![Kullanıcılar - ekran görüntüsü seçin][2]
4. Merhaba Arama sonuçlarından Hello kullanıcı seçin ve tıklatın **Bitti**.
5. Tıklatın **Tamam** toosave seçiminizi. Seçtiğiniz hello kullanıcı hello ayrıcalıklı rol Yöneticiler listesinde görünür.
   
   * Yeni bir rol toosomeone atadığınız zaman, bunlar otomatik olarak uygun tooactivate hello rolü olarak ayarlanır. Toomake istiyorsanız, bunları hello rolü'nde, kalıcı hello kullanıcı hello listesinde tıklatın. Seçin **izin olun** hello kullanıcı bilgileri menüsünde.
6. Merhaba kullanıcı bağlantısı çok Gönder[Azure AD Privileged Identity Management ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md).

## <a name="remove-another-users-access-rights-for-managing-pim"></a>PIM yönetmek için başka bir kullanıcının erişim haklarını kaldır
Birisi hello ayrıcalıklı rol yöneticisi rolünden kaldırmadan önce her zaman tooit atanan iki kullanıcılar çıkarılsın emin olun.

1. Merhaba rolü'nde Hello PIM panosunda tıklatın **ayrıcalıklı Rol Yöneticisi**.  şu anda bu roldeki kullanıcılar Hello listesi görüntülenir.
2. Merhaba kullanıcı hello kullanıcı listesinde tıklayın.
3. Tıklayın **kaldırmak**.  Bir onay iletisi ile sunulur.
4. Tıklatın **Evet** hello rolünden tooremove hello kullanıcı.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
