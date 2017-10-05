---
title: "Azure Active Directory'ye yeni kullanıcı ekleme | Microsoft Belgeleri"
description: "Azure Active Directory'de yeni kullanıcıların eklenmesini veya kullanıcı bilgilerinin değiştirilmesini açıklar."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: bfe0c556d94d50207a23d2e3984371fb602e9406
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-new-users-to-azure-active-directory"></a>Azure Active Directory'ye yeni kullanıcı ekleme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-users-create-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-create-users.md)
>
>

Bu makalede, Azure Active Directory'de (Azure AD), kuruluşunuzdaki yeni kullanıcı ekleme açıklanmaktadır. 

1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcılar ve gruplar](./media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **Ekle**.

   ![Ekle komutu seçme](./media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. Kullanıcı için Ayrıntılar gibi girin **adı** ve **kullanıcı adı**. Kullanıcı adı etki alanı adı kısmını ya da ilk varsayılan etki alanı adı "foo.onmicrosoft.com" etki alanı adı ya da "contoso.com" gibi bir doğrulanmış, Federasyon olmayan etki alanı adı olması gerekir
5. Kopyalama veya aksi takdirde bu işlem tamamlandıktan sonra kullanıcıya sağlayabilir böylece oluşturulmuş kullanıcı parolası not edin.
6. İsteğe bağlı olarak, açın ve bilgileri doldurun **profil** dikey penceresinde **grupları** dikey penceresinde veya **dizin rolünü** dikey penceresinde kullanıcı için. Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).
7. Üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.
8. Böylece kullanıcı oturum açarak yeni kullanıcı için oluşturulmuş bir parola güvenli bir şekilde dağıtın.

### <a name="next-steps"></a>Sonraki adımlar
* [Bir dış kullanıcı ekleme](active-directory-users-create-external-azure-portal.md)
* [Yeni Azure portalında bir kullanıcının parolasını sıfırlama](active-directory-users-reset-password-azure-portal.md)
* [Kullanıcının iş bilgilerini değiştirme](active-directory-users-work-info-azure-portal.md)
* [Kullanıcı profillerini yönetme](active-directory-users-profile-azure-portal.md)
* [Azure AD'de kullanıcı silme](active-directory-users-delete-user-azure-portal.md)
* [Bir kullanıcı, Azure AD'de rol atama](active-directory-users-assign-role-azure-portal.md)
