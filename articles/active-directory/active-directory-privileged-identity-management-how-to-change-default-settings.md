---
title: "aaaHow toomanage rol etkinleştirme ayarlarını | Microsoft Docs"
description: "Nasıl toochange hello ayrıcalıklı kimlikleri için varsayılan ayarları hello Azure Active Directory Privileged Identity Management uzantısı ile bilgi edinin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Nasıl toomanage rol etkinleştirme Azure AD Privileged Identity Management ayarlarında
Ayrıcalıklı Rol Yöneticisi Azure AD Privileged Identity Management (PIM) uygun rol ataması etkinleştirme bir kullanıcı için hello deneyimi değiştirme gibi kuruluşlarındaki özelleştirebilirsiniz.

## <a name="manage-hello-role-activation-settings"></a>Merhaba rol etkinleştirme ayarlarını yönet
1. Toohello Git [Azure portal](https://portal.azure.com) ve select hello **Azure AD Privileged Identity Management** hello panosundan uygulama.
2. Seçin **yönetmek ayrıcalıklı rolleri** > **ayarları** > **ayrıcalıklı rolleri**.
3. Merhaba rol ayarlarını seçin toomanage istiyor.

Hello Ayarları sayfasında her rol için çeşitli yapılandırabileceğiniz ayarlar vardır. Bu ayarlar yalnızca uygun yönetici, değil kalıcı yönetici sahip kullanıcıların etkiler.

**Etkinleştirme**: hello sürede sona ermeden önce bir rol etkin kalmasını saatleri. Bu, 1 ila 72 saat arasında olabilir.

**Bildirimleri**: hello sistem rol etkinleştirdikten onaylama e-postaları tooadmins gönderir olsun veya olmasın seçebilirsiniz. Bu, yetkisiz veya aykırı etkinleştirmeleri algılamak için yararlı olabilir.

**Olay/istek anahtarı**: rolleri etkinleştirdiğinizde toorequire uygun admins tooinclude bir bilet numarası olsun veya olmasın seçebilirsiniz. Rol erişim denetimleri gerçekleştirdiğinizde bu yararlı olabilir.

**Çok faktörlü kimlik doğrulaması**: seçebileceğiniz desteklemediğini toorequire kullanıcılar tooverify kimliklerini rollerine etkinleştirilebilmesi MFA ile. Bunlar yalnızca bu kez her bir rolü etkinleştirmemek her zaman oturum tooverify gerekir. İki ipuçları tookeep göz önünde MFA etkinleştirin, vardır:

* E-postaları için Microsoft hesabına sahip kullanıcıların (genellikle @outlook.com, ancak her zaman) için Azure MFA kaydedilemiyor. Microsoft hesaplarıyla tooassign rolleri toousers istiyorsanız, kalıcı yönetici yapın veya bu rol için MFA devre dışı bırakmak gerekir.
* MFA için üst düzey ayrıcalıklı rolleri Azure AD için devre dışı bırakamazsınız ve Office365. Bu, bu rolleri dikkatle korunması için bir güvenlik özelliğidir:  
  
  * Uygulama Yöneticisi
  * Uygulama Proxy sunucusu Yöneticisi
  * Faturalama Yöneticisi  
  * Uyumluluk Yöneticisi  
  * CRM Hizmet Yöneticisi
  * Müşteri kasa erişimi onaylayıcı
  * Directory yazıcısı  
  * Exchange Yöneticisi  
  * Genel yönetici
  * Intune Hizmet Yöneticisi
  * Posta kutusu Yöneticisi  
  * İş ortağı tier1 desteği  
  * İş ortağı tier2 desteği  
  * Ayrıcalıklı Rol Yöneticisi   
  * Güvenlik yöneticisi  
  * SharePoint Yöneticisi  
  * Skype Kurumsal yöneticisi  
  * Kullanıcı Hesap Yöneticisi  

MFA ile PIM kullanma hakkında daha fazla bilgi için bkz: [nasıl tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

