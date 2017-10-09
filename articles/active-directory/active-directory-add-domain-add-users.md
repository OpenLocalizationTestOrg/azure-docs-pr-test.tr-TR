---
title: "aaaAssign kullanıcılar tooa özel etki alanı Azure Active Directory'de | Microsoft Docs"
description: "Nasıl toopopulate özel bir etki alanı Azure Active Directory'deki kullanıcı hesaplarına sahip."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Kullanıcıların tooa özel etki alanı atayın
Active Directory, özel etki alanı tooAzure ekledikten sonra bunları kimlik doğrulaması başlayabilmesi hello kullanıcı hesaplarını bu etki alanı eklemeniz gerekir.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Hello Azure AD Yönetim Merkezi'nde etki alanınızın nasıl toomanage adları için bkz: [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Bir şirket içi Directory'den eşitlenen kullanıcılar
Zaten bir bağlantı ayarlamak, şirket içi arasında Active Directory ve Azure Active Directory ayarladıysanız, eşitleme hello hesapları doldurabilirsiniz. Azure Active Directory, şirket içi Active Directory ile nasıl toosynchronize bakın hakkında daha fazla bilgi için [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Eklenen ve hello bulutta yönetilen kullanıcılar
Varolan bir kullanıcı hesabı için toochange hello etki alanı:

1. Açık hello genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalı
2. Dizininizi açın.
3. Select hello **kullanıcılar** sekmesi.
4. Merhaba kullanıcı hello listeden seçin.
5. Hello etki alanı hello kullanıcı için değiştirin ve ardından **kaydetmek**.

Bu ayrıca yapılabilir kullanarak [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) veya hello [grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Yeni bir kullanıcı oluşturulurken özel bir etki alanı seçin
1. Açık hello genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalı
2. Dizininizi açın.
3. Select hello **kullanıcılar** sekmesi.
4. Merhaba komut çubuğunda seçin **Ekle**.
5. Merhaba kullanıcı adı eklediğinizde, hello özel etki alanı hello etki alanı listesinden seçin.
6. **Kaydet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar
* [Kullanıcılarınız için oturum açma, özel etki alanı adları toosimplify hello deneyimi kullanma](active-directory-add-domain.md)
* [Özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md)
* [Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme](active-directory-add-domain-concepts.md)

