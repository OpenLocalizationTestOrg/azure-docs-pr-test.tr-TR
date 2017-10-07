---
title: "aaaHow tooAssign kullanıcılar tooapplications | Microsoft Docs"
description: "Kullanıcılar Kiracı tooan uygulamada nasıl atanır anlama"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Nasıl tooassign kullanıcılar tooapplications

Bu makale toounderstand yardımcı kullanıcılar Kiracı tooan uygulamada nasıl atanır.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Nasıl kullanıcılar Azure AD'de tooan uygulama atanır?

Bir kullanıcı tooaccess bir uygulama için önce bir şekilde tooit atanmaları gerekir. Atama bir yönetici, bir iş temsilci veya hello kullanıcı tarafından bazı durumlarda, kendilerini gerçekleştirilebilir. Aşağıda kullanıcılar tooapplications atanan hello yolları açıklanmaktadır:

1.  Bir yönetici [kullanıcı atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) doğrudan toohello uygulama

2.  Bir yönetici [bir grup atar](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) bu hello kullanıcının toohello uygulama üyesi olduğu da dahil olmak üzere:

  * Şirket içi eşitlendiği bir grup

  * Merhaba bulutta oluşturulan bir statik güvenlik grubu

  * A [dinamik güvenlik grubu](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) hello bulutta oluşturulan

  * Merhaba bulutta oluşturulan bir Office 365 Grup

  * Merhaba [tüm kullanıcılar](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grubu

3.  Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama bir kullanıcı tooadd hello tooallow [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özelliği **iş onayı olmadan**

4.  Yöneticinin paylaşılan [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kullanarak bir uygulama bir kullanıcı tooadd hello tooallow [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **uygulama Ekle** özellik, ancak yalnızca w **iş onaylayanlar seçili kümesinden i önceki onayı**

5.  Yöneticinin paylaşılan [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow kullanıcı toojoin uygulamanın çok atanmış bir gruba**iş onayı olmadan**

6.  Yöneticinin yerel veya uzak [Self Servis Grup Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow kullanıcı toojoin bir uygulama için ancak yalnızca atanmış bir gruba **iş onaylayanlar seçili kümesinden önceki Onayla**

7.  Bir yönetici gibi bir lisans tooa kullanıcı birinci taraf uygulama için doğrudan atar [Microsoft Office 365](http://products.office.com/)

8.  Kullanıcı hello lisans tooa grubunun bir üyesidir tooa birinci taraf uygulama gibi bir yönetici atar [Microsoft Office 365](http://products.office.com/)

9.  Bir [yönetici izin tooan uygulama](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe tüm kullanıcılar tarafından kullanılan ve toohello uygulamada bir kullanıcı oturum açtığında

10. Bir kullanıcı [tooan uygulama izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) kendilerini toohello uygulamada oturum açarak

## <a name="next-steps"></a>Sonraki adımlar
[Azure Active Directory ile uygulamaları yönetme](active-directory-enable-sso-scenario.md)
