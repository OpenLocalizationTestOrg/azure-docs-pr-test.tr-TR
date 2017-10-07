---
title: "Active Directory kimlik koruması - aaaAzure nasıl toounblock kullanıcılar | Microsoft Docs"
description: "Bilgi nasıl bir Azure Active Directory kimlik koruması İlkesi tarafından engellendi kullanıcıların Engellemeyi Kaldır."
services: active-directory
keywords: "Azure active directory kimlik koruması, kullanıcının engelini kaldırma"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: a953d425-a3ef-41f8-a55d-0202c3f250a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: cdda2808822888f76aa75cf46478738c94df51a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection---how-toounblock-users"></a>Azure Active Directory kimlik koruması - nasıl toounblock kullanıcılar
Azure Active Directory kimlik koruması ile hello koşullar yapılandırdıysanız tooblock kullanıcılar karşılanır ilkelerini yapılandırabilirsiniz. Engeli kaldırılmış genellikle, bir engellenen kullanıcı kişiler Yardım Masası toobecome. Bu konular toounblock engellenen bir kullanıcı gerçekleştirebilirsiniz hello adımları açıklanmaktadır.

## <a name="determine-hello-reason-for-blocking"></a>Engelleme nedeni hello belirleme
Bir ilk adım toounblock bir kullanıcı, sonraki adımlarda üzerinde çünkü hello kullanıcı engelledi İlkesi toodetermine hello türünü gerekir.
Azure Active Directory kimlik koruması ile bir kullanıcı ya da bir oturum açma riski İlkesi veya bir kullanıcı risk İlkesi tarafından engellenebilir.

Merhaba toohello kullanıcı bir oturum açma girişimi sırasında sunulan hello iletişim hello başlığına kullanıcıdan engelledi ilke türünü alabilirsiniz:

| İlke | Kullanıcı iletişim kutusu |
| --- | --- |
| Oturum açma riski |![Engellenen oturum açma](./media/active-directory-identityprotection-unblock-howto/02.png) |
| Kullanıcı riski |![Engellenen hesabı](./media/active-directory-identityprotection-unblock-howto/104.png) |

Tarafından engellenen bir kullanıcı:

* Bir oturum açma riski olarak da bilinen şüpheli oturum açma ilkedir
* Kullanıcı risk ilkesi olarak da bilinen bir risk hesabıdır

## <a name="unblocking-suspicious-sign-ins"></a>Engellemeyi kaldırma şüpheli oturum açma işlemleri
toounblock bir şüpheli oturum açma seçenekleri aşağıdaki hello vardır:

1. **Oturum açma tanıdık bir konumdan veya aygıt** -engellenen şüpheli oturum açma işlemleri için ortak bir nedeni olan oturum açma denemeleri tanınmayan konumlardan veya cihazlar. Kullanıcılarınıza hızlı bir şekilde bu toosign bileşenini tanıdık konumu ya da cihaz deneyerek neden engelleme hello olup olmadığını belirleyebilirsiniz.
2. **İlkenin dışında tutmak** - düşünüyorsanız hello yapılandırmasına oturum açma ilkenizin belirli kullanıcılar için sorunları neden, hello kullanıcılar dışlayabilirsiniz. Bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) daha fazla ayrıntı için.
3. **İlkeyi devre dışı** - düşünüyorsanız, ilke yapılandırması, tüm kullanıcılar için sorunlara neden olup, hello ilkesi devre dışı bırakabilirsiniz. Bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) daha fazla ayrıntı için.

## <a name="unblocking-accounts-at-risk"></a>Risk engellemesini kaldırma hesapları
toounblock hesabı risk bir seçenekleri aşağıdaki hello vardır:

1. **Parola sıfırlama** -hello kullanıcının parolasını sıfırlayabilir. Bkz: [el ile güvenli parola sıfırlama](active-directory-identityprotection.md#manual-secure-password-reset) daha fazla ayrıntı için.
2. **Tüm risk olayı kapatmak** -hello kullanıcı risk ilkesine bir kullanıcı erişimi engelleme için yapılandırılmış hello kullanıcı risk düzeyi ulaştıysanız engeller. Bir kullanıcı azaltabilir el ile kapatarak risk düzeyi risk olaylarını bildirilen kullanıcının. Daha fazla ayrıntı için bkz: [risk olaylarını el ile kapatma](active-directory-identityprotection.md#closing-risk-events-manually).
3. **İlkenin dışında tutmak** - düşünüyorsanız hello yapılandırmasına oturum açma ilkenizin belirli kullanıcılar için sorunları neden, hello kullanıcılar dışlayabilirsiniz. Bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) daha fazla ayrıntı için.
4. **İlkeyi devre dışı** - düşünüyorsanız, ilke yapılandırması, tüm kullanıcılar için sorunlara neden olup, hello ilkesi devre dışı bırakabilirsiniz. Bkz: [Azure Active Directory kimlik koruması](active-directory-identityprotection.md) daha fazla ayrıntı için.

## <a name="next-steps"></a>Sonraki adımlar
 Azure AD kimlik koruması hakkında daha fazla tooknow istiyor musunuz? Kullanıma [Azure Active Directory kimlik koruması](active-directory-identityprotection.md).
