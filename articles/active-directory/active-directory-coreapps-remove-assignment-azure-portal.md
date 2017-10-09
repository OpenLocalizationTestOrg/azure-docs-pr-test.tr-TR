---
title: "bir kullanıcı veya grup ataması Kurumsal uygulama Azure Active Directory'de aaaRemove | Microsoft Docs"
description: "Nasıl tooremove hello erişim bir kullanıcı veya grup ataması Kurumsal uygulama Azure Active Directory'de"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup ataması kaldırma
Kolay tooremove bir kullanıcı veya Azure Active Directory'de (Azure AD), Kurumsal uygulamalarınızın erişim tooone atanmasını gelen bir grup değil. Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Bir kullanıcı veya grup ataması nasıl kaldırabilirim?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.
3. Merhaba üzerinde **Azure Active Directory - *directoryname***  dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**. Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.
5. Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.
6. Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **kullanıcıları ve grupları**.

    ![Kullanıcıları veya grupları seçme](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Merhaba üzerinde ***appname*** **-kullanıcı ve grup atama** dikey penceresinde, daha fazla kullanıcı veya grup seçin ve ardından hello seçin **kaldırmak** komutu. Kararınızı hello isteminde onaylayın.

    ![Merhaba Kaldır komutu seçme](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Tüm my gruplarının bakın](active-directory-groups-view-azure-portal.md)
* [Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)
* [Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak](active-directory-coreapps-disable-app-azure-portal.md)
* [Merhaba adını veya bir kuruluş uygulama logosunu değiştirme](active-directory-coreapps-change-app-logo-user-azure-portal.md)
