---
title: "aaaGet Azure AD Privileged Identity Management ile çalışmaya | Microsoft Docs"
description: "Azure portalında Merhaba Azure Active Directory Privileged Identity Management uygulaması kimliklerle toomanage nasıl ayrıcalıklı öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management'ı kullanmaya başlama
Azure Active Directory (AD) Privileged Identity Management sayesinde kuruluşunuz içindeki erişimi yönetebilir, denetleyebilir ve izleyebilirsiniz. Bu kapsam erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services içerir.

Bu makalede nasıl tooadd hello Azure AD PIM uygulamasını tooyour Azure portalı panosunun söyler.

## <a name="add-hello-privileged-identity-management-application"></a>Merhaba Privileged Identity Management uygulaması ekleyin
Azure AD Privileged Identity Management kullanmadan önce tooadd hello uygulama tooyour Azure portalı panosunun gerekir.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) dizininizin genel Yöneticisi olarak.
2. Kuruluşunuz birden fazla dizine sahipse, kullanıcı adınızı hello sağ üst köşesinde hello Azure portalı içinde seçin. Merhaba dizini toouse PIM istediğiniz yeri seçin.
3. Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.
4. Denetleme **PIN toodashboard** ve ardından **oluşturma**. Merhaba Privileged Identity Management uygulaması açılır.

Dizininizde Azure AD Privileged Identity Management ilk kişinin toouse olduğunuz hello durumunda, hello otomatik olarak atanır **Güvenlik Yöneticisi** ve **ayrıcalıklı Rol Yöneticisi** rolleri Merhaba dizininde. Yalnızca ayrıcalıklı rol yöneticileri kullanıcıların rol atamalarını yönetebilir. Ayrıca, toorun hello seçebilirsiniz [Güvenlik Sihirbazı.](active-directory-privileged-identity-management-security-wizard.md) hello ilk bulma ve atama deneyimi boyunca eşlik eder.

## <a name="navigate-tooyour-tasks"></a>Tooyour görevleri gidin
Azure AD Privileged Identity Management ayarladıktan sonra hello uygulamayı her açtığınızda hello Gezinti dikey penceresine bakın. Bu dikey tooaccomplish kimlik yönetimi görevleri kullanın.

![PIM için üst düzey görevler - ekran görüntüsü](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **My rolleri** tooa tooyou atanan rollerin listesini alır. Bu bölümde, uygun olduğunuz tüm rolleri etkinleştirebilirsiniz.
* **İstekleri Onayla (Önizleme)**, dizininizdeki kullanıcılardan gelen beklemedeki etkinleştirme isteklerinin listesini görüntüler. [Daha fazla bilgi edinin.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **Bekleyen istekler (Önizleme)** tüm geçerli istekleri yapılan toohave tooactivate görüntüler.
* **Gözden erişim** , tooany erişim bekleyen incelemeleri toocomplete, gereken erişim kendiniz ya da başka birinin gözden olup olmadığını alır.
* **Azure AD Directory rolleri** hello 'Yönet' bölümü altında ayrıcalıklı rol admins toomanage rol atamaları, rol etkinleştirme ayarlarını değiştir, başlangıç erişim gözden geçirme ve daha fazlası için hello Pano bulunur. Bu panoyu Hello seçeneklerinde bir ayrıcalıklı Rol Yöneticisi değil herkes için devre dışı bırakılır.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba [Azure AD Privileged Identity Management genel bakış](active-directory-privileged-identity-management-configure.md) yönetim erişimi, kuruluşunuzda nasıl yönetebileceğiniz konusunda daha ayrıntılı bilgi içerir.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
