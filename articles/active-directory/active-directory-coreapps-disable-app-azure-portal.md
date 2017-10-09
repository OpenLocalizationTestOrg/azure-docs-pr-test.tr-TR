---
title: "aaaDisable kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için | Microsoft Docs"
description: "Nasıl toodisable Kurumsal uygulama böylece hiçbir kullanıcı tooit Azure Active Directory'de oturum açma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırak
Kolay toodisable Kurumsal uygulama, böylelikle kullanıcı tooit Azure Active Directory'de (Azure AD) oturum açma. Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.

## <a name="how-do-i-disable-user-sign-ins"></a>Kullanıcı oturum açma işlemleri nasıl devre dışı bırakabilirim?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.
3. Merhaba üzerinde **Azure Active Directory** -  ***directoryname*** dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**. Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.
5. Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.
6. Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **özellikleri**.

    ![Merhaba tüm uygulamaları komutu seçme](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Merhaba üzerinde ***appname*** - **özellikleri** dikey penceresinde, select **Hayır** için **toosign bileşenini kullanıcılar için etkin?**.
8. Select hello **kaydetmek** komutu.

## <a name="next-steps"></a>Sonraki adımlar
* [My tüm grupları görmek](active-directory-groups-view-azure-portal.md)
* [Bir kullanıcı veya grup tooan kuruluş uygulama atama](active-directory-coreapps-assign-user-azure-portal.md)
* [Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Merhaba adını veya bir kuruluş uygulama logosunu değiştirme](active-directory-coreapps-change-app-logo-user-azure-portal.md)
