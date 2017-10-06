---
title: "Azure Active Directory B2B işbirliği aaaDelegate davetleri | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği kullanıcı özellikleri yapılandırılabilir"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: c0122d6f60d494c6e251c41d947dc254ea887620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="delegate-invitations-for-azure-active-directory-b2b-collaboration"></a>Azure Active Directory B2B işbirliği için temsilci davetleri

Azure Active Directory (Azure AD) işletmeden işletmeye (B2B) işbirliğiyle, toobe bir genel yönetici toosend davetleri gerekmez. Bunun yerine, ilkeleri kullanın ve davetleri toousers toosend davetleri izin olan roller atayabilirsiniz. Bir önemli yeni yolu toodelegate Konuk kullanıcı davetleri hello Konuk davet eden rolü üzerinden olur.

## <a name="guest-inviter-role"></a>Konuk davet eden rolü
Sizi davet eden rol toosend davetleri hello kullanıcı tooGuest atayabilirsiniz. Merhaba genel yönetici rolü toosend davetleri toobe üyesi yok. Varsayılan olarak, normal kullanıcı genel yönetici davetleri normal kullanıcılar için devre dışı bırakılmamışsa hello davet API de çalıştırabilirsiniz. Bir kullanıcı hello API hello Azure portal veya PowerShell kullanarak da çağırabilirsiniz.

İşte gösteren bir örnek nasıl toouse PowerShell tooadd kullanıcı toohello Konuk davet eden rolü:

```
Add-MsolRoleMember -RoleObjectId 95e79109-95c0-4d8e-aee3-d01accf2d47b -RoleMemberEmailAddress <RoleMemberEmailAddress>
```

## <a name="control-who-can-invite"></a>Davet edebilirsiniz denetimi

![Denetim nasıl tooinvite](media/active-directory-b2b-delegate-invitations/control-who-to-invite.png)

Azure AD B2B işbirliği ile bir kiracı Yöneticisi aşağıdaki davet ilkeler hello ayarlayabilirsiniz:

- Davetiye devre dışı bırakma
- Yalnızca Yöneticiler ve kullanıcılar hello Konuk davet eden rolündeki davet edebilirsiniz
- Yöneticiler, hello Konuk davet eden rolü ve üyeleri davet edebilirsiniz
- Konuklar, dahil tüm kullanıcıları davet edebilir

Varsayılan olarak, kiracılar çok ayarlanır #4. (Tüm kullanıcılar, Konuklar, dahil B2B kullanıcıları davet edebilirsiniz.)

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
