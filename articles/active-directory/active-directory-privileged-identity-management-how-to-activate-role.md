---
title: "aaaHow tooactivate veya bir rolü devre dışı bırakma | Microsoft Docs"
description: "Nasıl tooactivate rolleri için kimlikleri Merhaba Azure Privileged Identity Management uygulaması ile ayrıcalıklı öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Nasıl tooactivate veya Azure AD Privileged Identity Management rollerinde devre dışı bırakma
Azure Active Directory (AD) Privileged Identity Management, ayrıcalıklı erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services kuruluşların nasıl yönettiğini basitleştirir.  

Bir yönetici rolü için uygun yapılmışsa, ayrıcalıklı tooperform Eylemler gerektiğinde bu rol etkinleştirebilirsiniz anlamına gelir. Office 365 özellikleri bazen yönetiyorsanız, bu rolü diğer hizmetler çok etkiler Örneğin, kuruluşunuzun ayrıcalıklı rol Yöneticiler kalıcı genel yönetici kararı değil. Bunun yerine, bunlar, Exchange Online yönetici gibi Azure AD rolleri için uygun yapın. Bu rol, kendi ayrıcalıklarına sahip olmanız gerekir ve ardından önceden belirlenmiş bir süre için yönetici denetim gerekir tooactivate isteyebilir.

Bu makalede tooactivate isteyen yöneticiler için Azure AD Privileged Identity Management (PIM) içinde kendi rolüdür. Merhaba izinlerinizin olması gerekir ve tamamladığınızda hello rolünü devre dışı olduğunda, hello adımları tooactivate bir rolü açıklanmaktadır. Ayrıca, ayrıcalıklı rol Yöneticiler onay tooactivate bir rol (Önizleme) gerektirebilir. Daha fazla bilgi edinmek [PIM onay iş akışları](./privileged-identity-management/azure-ad-pim-approval-workflow.md) burada.

## <a name="add-hello-privileged-identity-management-application"></a>Merhaba Privileged Identity Management uygulaması ekleyin
Merhaba Azure AD Privileged Identity Management uygulaması hello kullan [Azure portal](https://portal.azure.com/) toorequest toooperate başka bir portal veya PowerShell kullanacaksanız bile, rol etkinleştirme. Azure Portal'da hello Azure AD Privileged Identity Management uygulaması yoksa, bu adımları tooget başlatılan izleyin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Kullanıcı adınıza hello sağ üst köşesinde hello Azure portal ve burada şunları yapacaksınız, select hello dizin işletim seçin.
3. Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.
4. Denetleme **PIN toodashboard** ve ardından **oluşturma**. Merhaba Privileged Identity Management uygulaması açılır.

## <a name="activate-a-role"></a>Bir rolü etkinleştirmesi
Bir rol üzerinde tootake gerektiğinde Merhaba seçerek etkinleştirme isteyebilir **My rolleri** hello Azure AD Privileged Identity Management uygulaması Gezinti seçeneğinde sol gezinti sütun.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve select hello Azure AD Privileged Identity Management kutucuk.
2. Seçin **My rolleri**. Merhaba hello sayfanın başında gruplandırma hello atanmış uygun rollerinizi listesi görüntülenir.
3. Bir rol tooactivate seçin.
4. Seçin **etkinleştirme**. Merhaba **rol etkinleştirme isteği** dikey penceresi görünür.
5. Merhaba rolünü etkinleştirmeden önce bazı roller çok faktörlü kimlik doğrulama (MFA) gerektirir. Her oturum için bir kez tooauthenticate yeterlidir.
   
    ![MFA ile rol etkinleştirme - ekran görüntüsü önce doğrulayın][2]
6. Merhaba etkinleştirme isteği Hello nedeni hello metin alanına girin.  Bazı roller toosupply sorun bileti numarası gerektirir.
7. **Tamam**’ı seçin.  Merhaba rol onay gerektirmiyorsa, şimdi etkinleştirilir ve hello rol (doğrudan aşağıda uygun rol atamalarını listesi hello) etkin rollerin hello listesinde görünür. Merhaba, [rolünü onay gerektiren](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, bildirim kısaca görünür hello sağ üst köşesinde hello isteğidir onay bekleyen bildiren tarayıcınız.

    ![Bildirim - ekran görüntüsü istek][3]

## <a name="deactivate-a-role"></a>Bir rolü devre dışı bırakma
Bir rolü etkinleştirildikten sonra süresi sınırına (uygun süresi) ulaşıldığında otomatik olarak devre dışı bırakır.

Yönetim görevlerinizi erken tamamlarsanız, bir rolde el ile hello Azure AD Privileged Identity Management uygulaması devre dışı bırakabilirsiniz.  Seçin **My rolleri**, tamamladıktan hello rolünü seçin hello kullanarak **etkin rol atamalarını** gruplandırma ve select **devre dışı bırak**.  

## <a name="cancel-a-pending-request"></a>Bekleyen isteği iptal et
Merhaba olay onayı gerektiren bir rolü etkinleştirmesi gerektirmez, herhangi bir zamanda bekleyen isteği iptal edebilirsiniz. Yalnızca select hello **My rolleri** hello Azure AD Privileged Identity Management uygulaması Gezinti seçeneğinde sol gezinti sütun.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) ve select hello Azure AD Privileged Identity Management kutucuk.
2. Seçin **My rolleri**. Merhaba hello sayfanın başında gruplandırma hello atanmış uygun rollerinizi listesi görüntülenir.
3. Bir rol seçin.
4. Select hello **etkinleştirme durumda onay bekleyen** hello rol etkinleştirme ayrıntıları dikey penceresinde başlık.
5. Seçin **iptal** hello hello üstündeki **onay bekleyen** dikey.

   ![Bekleyen isteği ekran iptal et][4]

## <a name="next-steps"></a>Sonraki adımlar
Azure AD Privileged Identity Management hakkında daha fazla bilgi edinmek isterseniz hello aşağıdaki bağlantılardan daha fazla bilgi sahip.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
