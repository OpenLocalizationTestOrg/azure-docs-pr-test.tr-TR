---
title: "aaaHow tooperform erişim gözden geçirme | Microsoft Docs"
description: "Nasıl bir gözden geçirme ile tooperform hello Azure Privileged Identity Management uygulaması hakkında bilgi edinin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a>Nasıl tooperform access gözden Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management, ayrıcalıklı erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services kuruluşların nasıl yönettiğini basitleştirir.  

Tooan Yönetici rolü atanmışsa, kuruluşunuzun ayrıcalıklı Rol Yöneticisi isteyebilir tooregularly onaylayın bu rol hala işiniz için gerekir. Bir bağlantı içeren bir e-posta alabilirsiniz veya düz toohello gidebilirsiniz [Azure portal](https://portal.azure.com). Bu makale tooperform atanan rollerinizi Self gözden Hello adımları izleyin.

Erişim incelemeler ilgilenen bir ayrıcalıklı rol yöneticisi değilseniz, daha fazla bilgi almak [toostart erişimini nasıl gözden](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-hello-privileged-identity-management-application"></a>Merhaba Privileged Identity Management uygulaması ekleyin
Merhaba Azure AD Privileged Identity Management (PIM) uygulaması hello kullanabilirsiniz [Azure portal](https://portal.azure.com/) tooperform gözden geçirilecek.  Portalınızda hello Azure AD Privileged Identity Management uygulaması yoksa, bu adımları tooget başlatılan izleyin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Kullanıcı adınıza hello sağ üst köşesinde hello Azure portal ve burada şunları yapacaksınız, select hello dizin işletim seçin.
3. Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.
4. Denetleme **PIN toodashboard** ve ardından **oluşturma**. Merhaba Privileged Identity Management uygulaması açılır.

## <a name="approve-or-deny-access"></a>Onaylamak veya erişim engelle
Onaylama ya da erişimini yalnızca hello İnceleme bu rolü veya kullanmaya devam olup olmadığını belirten. Seçin **Onayla** toostay hello rolündeki istiyorsanız veya **reddetme** erişim artık hello yoktur. Merhaba İnceleme hello sonuçları geçerli olana kadar durumunuzu hemen değiştirmez.
Bu adımları toofind izleyin ve hello erişim gözden geçirme tamamlayın:

1. Hello PIM uygulama, seçin **gözden geçirme ayrıcalıklı erişim**. Tüm bekleyen erişim incelemeler varsa, Azure AD erişim dikey incelemeleri hello görünür.
2. Merhaba gözden toocomplete istediğiniz seçin.
3. Merhaba gözden geçirme oluşturduğunuz sürece, yalnızca hello gözden geçirme kullanıcı hello gibi görünür. Merhaba onay işareti sonraki tooyour adını seçin.
4. Ya da seçin **onaylama** veya **Reddet**. Tooinclude kararınızı hello içinde nedeni gerekebilir **bir gerekçe sağlamasını** metin kutusu.  
5. Kapat hello **gözden geçirme Azure AD rolleri** dikey.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
