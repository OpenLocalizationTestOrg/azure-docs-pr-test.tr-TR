---
title: "aaaAssign bir kullanıcı Azure Active Directory'de tooadministrator rolü | Microsoft Docs"
description: "Açıklar nasıl toochange kullanıcı yönetim bilgilerinin Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.openlocfilehash: 8bb6711c2570843962fe075b6026542a4bca525f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-tooadministrator-roles-in-azure-active-directory"></a>Bir kullanıcı Azure Active Directory'de tooadministrator Rolleri Ata
Bu makalede açıklanır nasıl tooassign Azure Active Directory (Azure AD) ortamında bir yönetici rolü tooa kullanıcı. Kuruluşunuzdaki yeni kullanıcı ekleme hakkında daha fazla bilgi için bkz: [yeni kullanıcılar tooAzure Active Directory eklemek](active-directory-users-create-azure-portal.md). Eklenen kullanıcılar varsayılan olarak yönetici izinlerine sahip olmayan, ancak herhangi bir zamanda roller toothem atayabilirsiniz.

## <a name="assign-a-role-tooa-user"></a>Rol tooa kullanıcı atama
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**.

   ![Açılış hello tüm kullanıcılar dikey penceresi](./media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. Merhaba üzerinde **kullanıcılar ve gruplar - tüm kullanıcılar** dikey penceresinde, kullanıcı hello listeden seçin.
5. Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **dizin rolünü**ve ardından hello hello kullanıcı tooa rolü atayın **dizin rolünü** listesi. Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).

      ![Bir kullanıcı tooa rolü atama](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. **Kaydet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar
* [Kullanıcı ekleme](active-directory-users-create-azure-portal.md)
* [Merhaba yeni Azure portalında bir kullanıcının parolasını sıfırlama](active-directory-users-reset-password-azure-portal.md)
* [Kullanıcının iş bilgilerini değiştirme](active-directory-users-work-info-azure-portal.md)
* [Kullanıcı profillerini yönetme](active-directory-users-profile-azure-portal.md)
* [Azure AD'de kullanıcı silme](active-directory-users-delete-user-azure-portal.md)
