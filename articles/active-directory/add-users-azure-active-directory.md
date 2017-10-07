---
title: "aaaAdd yeni kullanıcılar tooAzure Active Directory | Microsoft Docs"
description: "Açıklar nasıl tooadd yeni kullanıcılar Azure Active Directory'de."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Hızlı Başlangıç: yeni kullanıcılar tooAzure Active Directory ekleme
Bu makalede nasıl hello Azure Active Directory (Azure AD), kuruluşunuzdaki yeni kullanıcıların tooadd hello Azure portal kullanarak bir zamanda ya da şirket içi Windows Server AD kullanıcı eşitleme hesabı veri açıklanmaktadır. 

## <a name="add-cloud-based-users"></a>Bulut tabanlı kullanıcıları ekleme
1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **Azure Active Directory** ve ardından **kullanıcılar ve gruplar**.
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm kullanıcılar**ve ardından **yeni kullanıcı**.
   ![Merhaba Ekle komutu seçme](./media/add-users-azure-active-directory/add-user.png)
4. Ayrıntılar gibi hello kullanıcıdan girin **adı** ve **kullanıcı adı**. Merhaba hello kullanıcı adının etki alanı adı kısmını hello ilk varsayılan etki alanı adı "[etki alanı adı].onmicrosoft.com" ya da doğrulanmış, Federasyon olmayan olmalıdır [özel etki alanı adı](add-custom-domain.md) "contoso.com" gibi
5. Böylece bu işlem tamamlandıktan sonra toohello kullanıcı sağlayabilir kopyalama veya aksi Not hello tarafından oluşturulan kullanıcı parola.
6. İsteğe bağlı olarak, açın ve hello hello bilgileri doldurun **profil** dikey penceresinde, hello **grupları** dikey ya da hello **dizin rolünü** dikey penceresinde hello kullanıcı için. Kullanıcı ve yönetici rolleri hakkında daha fazla bilgi için bkz. [Azure AD'de yönetici rolü atama](active-directory-assign-admin-roles.md).
7. Merhaba üzerinde **kullanıcı** dikey penceresinde, select **oluşturma**.
8. Böylece Hello kullanıcı oturum açabilir hello oluşturulan parola toohello yeni kullanıcı güvenli bir şekilde dağıtın.

> [!TIP]
> Ayrıca şirket içi Windows Server AD kullanıcı hesabı verileri eşitleyebilirsiniz. Microsoft'un kimlik çözümleri şirket içi ve bulut tabanlı özellikleri, tek bir kullanıcı kimliği kimlik doğrulama ve yetkilendirme için konum bağımsız olarak tooall kaynakları oluşturma span. Bu karma kimlik diyoruz. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) şirket içi dizinlerinizi Azure Active Directory ile karma kimlik senaryosunda kullanılan toointegrate olabilir. Bu, kullanıcıların Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar. 

## <a name="delete-users-from-azure-ad"></a>Azure AD kullanıcıları Sil
1. İçinde toohello oturum [Azure Active Directory Yönetim Merkezi](https://aad.portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **kullanıcılar ve gruplar**.
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select hello kullanıcı toodelete hello listeden. 
4. Merhaba dikey penceresinde hello seçilen kullanıcı, seçin **genel bakış**ve hello komut çubuğunda, ardından **silmek**.
   ![Merhaba Ekle komutu seçme](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Daha fazla bilgi edinin 
* [Bir dış kullanıcı ekleme](active-directory-users-create-external-azure-portal.md)

* [Azure AD'de kullanıcı tooa rol atama](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Sonraki adımlar
Bu Hızlı Başlangıç, öğrendiğinize nasıl tooadd yeni kullanıcılar tooAzure AD Premium. 

Bağlantı toocreate yeni bir kullanıcı Azure AD'de hello Azure portal ' aşağıdaki hello kullanabilirsiniz.

> [!div class="nextstepaction"]
> [Kullanıcıların tooAzure AD ekleyin](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
