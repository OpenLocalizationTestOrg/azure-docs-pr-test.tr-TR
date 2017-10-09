---
title: "aaaHow tooadd veya bir kullanıcı rolünü kaldırmak | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management uygulaması tooadd rolleri tooprivileged kimliklerle nasıl hello öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 6a47ced8-cf34-4ce8-bea2-e4fc548cfe22
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim;oldportal;it-pro;
ms.openlocfilehash: f84639757dd76061ea12ed6ea7ec9e62ad942109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-privileged-identity-management-how-tooadd-or-remove-a-user-role"></a>Azure AD Privileged Identity Management: Nasıl tooadd veya bir kullanıcı rolünü kaldır
Azure Active Directory (AD ile), bir genel yönetici (veya şirket Yöneticisi) kullanıcıları olan güncelleştirebilirsiniz **kalıcı olarak** tooroles Azure AD'de atanmış. Bu PowerShell cmdlet'leri gibi gerçekleştirilir `Add-MsolRoleMember` ve `Remove-MsolRoleMember`. Ya da açıklandığı gibi hello Klasik Azure portalını kullanabilirsiniz [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md).

Hello Azure AD Privileged Identity Management uygulaması ayrıcalıklı rol yöneticilerinin toomake kalıcı rol atamaları de sağlar. Ayrıca, ayrıcalıklı rol Yöneticiler kullanıcılar yapabilir **uygun** yönetici rolleri. Uygun bir yönetici hello rol ihtiyaç duydukları ve bunlar bitirdiğinizde izinlerini sona etkinleştirebilirsiniz.

## <a name="manage-roles-with-pim-in-hello-azure-portal"></a>Hello Azure portal ile PIM rolleri yönetme
Kuruluşunuzdaki kullanıcılar Azure AD'de Office 365 ve diğer Microsoft Hizmetleri ve uygulamaları toodifferent yönetici rollerini atayabilirsiniz.  Merhaba kullanılabilir rolleri hakkında daha fazla ayrıntı bulunabilir [Azure AD PIM rolleri](active-directory-privileged-identity-management-roles.md).

tooadd veya Kaldır ayrıcalıklı Kimlik Yönetimi'ni kullanarak bir roldeki kullanıcı hello PIM Pano çıkarır. Ya da hello tıklatın ardından **yönetici rolleri** düğmesini veya hello rolleri tablosundan (örneğin, genel yönetici) belirli bir rol seçin.

> [!NOTE]
> PIM hello Azure portal henüz etkinleştirmediyseniz, çok Git[Azure AD PIM ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md) Ayrıntılar için.

Başka bir kullanıcı erişimi tooPIM kendisini hello kullanıcı toohave daha ayrıntılı açıklanır PIM gerektiren hello rolleri toogive istiyorsanız [nasıl toogive erişim tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="add-a-user-tooa-role"></a>Kullanıcı tooa rolü ekleme
1. Merhaba, [Azure portal](https://portal.azure.com/)seçin hello **Azure AD Privileged Identity Management** döşeme hello Panoda.
2. Seçin **yönetmek ayrıcalıklı rolleri**.
3. Merhaba, **Rol Özeti** tablo, select hello rol toomanage istiyor.
4. Merhaba rol dikey penceresinde, seçin **Ekle**.
5. Tıklatın **kullanıcı seçin** ve hello hello kullanıcı Ara **kullanıcı seçin** dikey.  
6. Merhaba kullanıcı hello arama sonuçları listesinden seçip'ı tıklatın **Bitti**.
7. Tıklatın **Tamam** toosave seçiminizi. Seçtiğiniz hello kullanıcı hello listesinde hello rol için uygun olarak görünür.

> [!NOTE]
> Bir rolü yeni kullanıcılar yalnızca varsayılan hello rolü için uygundur. Toomake hello rol kalıcı istiyorsanız hello kullanıcı hello listesinde tıklatın. Merhaba kullanıcının bilgileri yeni bir dikey pencerede görüntülenir. Seçin **yapma izni** hello kullanıcı bilgileri menüsünde.  
> Bir kullanıcı Azure çok faktörlü kimlik doğrulama (MFA) kaydedilemiyor veya bir Microsoft hesabı kullanıyorsanız (genellikle @outlook.com), toomake ihtiyacınız bunları kendi tüm rollerde kalıcı. Uygun admins tooregister etkinleştirme sırasında MFA için istenir.

Merhaba kullanıcı rolü için uygun olup, bunu toohello yönergelerinde göre etkinleştirme olduğunu bildirmek [nasıl tooactivate veya bir rolü devre dışı bırakma](active-directory-privileged-identity-management-how-to-activate-role.md).

## <a name="remove-a-user-from-a-role"></a>Bir kullanıcıyı rolden kaldırır
Uygun rol atamaları Kullanıcıları Kaldır, ancak her zaman kalıcı genel yönetici olan en az bir kullanıcı olduğundan emin olun.

Bu adımları tooremove belirli bir kullanıcıyı rolden izleyin:

1. Merhaba rolü listesinde toohello rol hello Azure AD PIM panosunda bir rolü seçerek veya üzerinde hello tıklatarak gidin **yönetici rolleri** düğmesi.
2. Merhaba kullanıcı hello kullanıcı listesinde tıklayın.
3. Tıklatın **kaldırmak**. Bir ileti tooconfirm isteyecektir.
4. Tıklatın **Evet** tooremove hello hello kullanıcı rolünden.

Hangi kullanıcıların yine rol atamalarını gerekir emin değilseniz sonra şunları yapabilirsiniz [hello rol için erişim incelemesi başlatma](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

