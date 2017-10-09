---
title: "Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama aaaAssign | Microsoft Docs"
description: "Nasıl tooselect Kurumsal uygulama tooassign Azure Active Directory'de bir kullanıcı veya grup tooit"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama
Kolay tooassign bir kullanıcı veya grup tooyour kurumsal uygulamalar Azure Active Directory'de (Azure AD) değil. Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Kullanıcı erişim tooan kuruluş uygulama nasıl atayabilirim?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, Azure Active Directory hello metin kutusuna girin ve ardından **Enter**.
3. Merhaba üzerinde **Azure Active Directory - *directoryname***  dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**. Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.
5. Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.
6. Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **kullanıcıları ve grupları**.

    ![Merhaba tüm uygulamaları komutu seçme](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. Merhaba üzerinde ***appname*** **-kullanıcı ve grup atama** dikey penceresinde, select hello **Ekle** komutu.
8. Merhaba üzerinde **eklemek atama** dikey penceresinde, select **kullanıcılar ve gruplar**.

    ![Bir kullanıcı veya grup toohello uygulama atama](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select bir veya daha fazla bölümünden kullanıcıları veya grupları hello listelemek ve hello seçin **seçin** hello dikey penceresinde hello sonundaki düğmesi.
10. Merhaba üzerinde **eklemek atama** dikey penceresinde, select **rol**. Ardından hello üzerinde **rolü Seç** dikey penceresinde, bir rol tooapply toohello Seçili kullanıcıları veya grupları ve ardından select hello **Tamam** hello dikey penceresinde hello sonundaki düğmesi.
11. Merhaba üzerinde **eklemek atama** dikey penceresinde, select hello **atamak** hello dikey penceresinde hello sonundaki düğmesi. Kullanıcıların Hello atanan veya grupları hello seçilen rol için bu kuruluş uygulama tarafından tanımlanan hello izinlerine sahip olacaktır.

## <a name="next-steps"></a>Sonraki adımlar
* [Tüm my gruplarının bakın](active-directory-groups-view-azure-portal.md)
* [Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak](active-directory-coreapps-disable-app-azure-portal.md)
* [Merhaba adını veya bir kuruluş uygulama logosunu değiştirme](active-directory-coreapps-change-app-logo-user-azure-portal.md)
