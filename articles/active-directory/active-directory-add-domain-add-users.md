---
title: "Azure Active Directory'de özel etki alanı kullanıcıları atamak | Microsoft Docs"
description: "Azure Active Directory'de özel olarak etki alanı kullanıcı hesapları ile doldurmak nasıl."
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
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a>Özel bir etki alanına kullanıcı atama
Özel etki alanınızı Azure Active Directory'ye ekledikten sonra bunları kimlik doğrulaması başlayabilmeniz için bu etki alanı kullanıcı hesaplarını eklemeniz gerekir.

> [!IMPORTANT]
> Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor. Azure AD Yönetim Merkezi'nden, etki alanı adlarını yönetmek için bkz: nasıl [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Bir şirket içi Directory'den eşitlenen kullanıcılar
Zaten bir bağlantı ayarlamak, şirket içi arasında Active Directory ve Azure Active Directory ayarladıysanız, eşitleme hesapları doldurabilirsiniz. Şirket içi Active Directory ile Azure Active Directory eşitleme hakkında daha fazla bilgi için bkz: [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-the-cloud"></a>Eklenen ve bulutta yönetilen kullanıcılar
Varolan bir kullanıcı hesabı için etki alanını değiştirmek için:

1. Genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalını açın
2. Dizininizi açın.
3. **Users (Kullanıcılar)** sekmesini seçin.
4. Kullanıcı listeden seçin.
5. Kullanıcı için etki alanını değiştirmek ve ardından **kaydetmek**.

Bu ayrıca yapılabilir kullanarak [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) veya [grafik API'si](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Yeni bir kullanıcı oluşturulurken özel bir etki alanı seçin
1. Genel yönetici veya Kullanıcı Yöneticisi olan bir hesabı kullanarak Klasik Azure portalını açın
2. Dizininizi açın.
3. **Users (Kullanıcılar)** sekmesini seçin.
4. Komut çubuğunda seçin **Ekle**.
5. Kullanıcı adı eklediğinizde, özel etki alanı etki alanı listesinden seçin.
6. **Kaydet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar
* [Kullanıcılarınız için oturum açma deneyimini basitleştirmek için özel etki alanı adlarını kullanma](active-directory-add-domain.md)
* [Özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md)
* [Azure AD'deki etki alanı yönetimi kavramları hakkında bilgi edinme](active-directory-add-domain-concepts.md)

