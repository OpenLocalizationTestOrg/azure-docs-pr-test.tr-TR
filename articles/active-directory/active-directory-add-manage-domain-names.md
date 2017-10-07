---
title: "Azure Active Directory'de aaaManaging özel etki alanı adları | Microsoft Docs"
description: "Yönetim Kavramları ve Azure Active Directory'de özel etki alanı yönetmek için nasıl yapılır?"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Azure Active Directory'de özel etki alanı adlarını yönetme
Bir etki alanı adı, birçok dizin kaynaklar için önemli bir tanımlayıcı bir parçası olarak şunlar olabilir:

* Bir kullanıcı için bir kullanıcı adı veya e-posta adresi
* bir grup için başlangıç adresi
* bir uygulama için Hello uygulama kimliği URI'si

Azure Active Directory'de (Azure AD) bir kaynak hello kaynak içeren toobe hello dizine ait zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz. Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Hello Azure AD Yönetim Merkezi'nde etki alanınızın nasıl toomanage adları için bkz: [Azure Active Directory'de özel etki alanı adlarını yönetme](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Azure AD dizininiz için Hello birincil etki alanı adı ayarlama
Dizininize oluşturulduğunda 'contoso.onmicrosoft.com,' gibi hello ilk etki alanı adı da hello birincil etki alanı dizininizin adıdır. Merhaba birincil etki alanı olduğunda hello varsayılan etki alanı adını yeni bir kullanıcı için yeni bir kullanıcı hello oluşturmak [Klasik Azure portalı](https://manage.windowsazure.com/), veya diğer portallarını hello Office 365 Yönetici portalı gibi. Bu, bir yönetici toocreate yeni kullanıcılar için hello portal hello işlemini kolaylaştırır.

dizininiz için toochange hello birincil etki alanı adı:

1. İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com/) Azure AD dizininizin genel yöneticisi olan bir kullanıcı hesabı ile.
2. Seçin **Active Directory** hello sol gezinti çubuğunda.
3. Dizininizi açın.
4. Select hello **etki alanları** sekmesi.
5. Select hello **değişiklik birincil** hello komut çubuğunda düğmesi.
6. Dizininiz için toobe hello yeni birincil etki alanı istediğiniz hello etki alanını seçin.

Birleşik olmadığı herhangi doğrulanmış özel etki alanı, dizin toobe hello birincil etki alanı adını değiştirebilirsiniz. Merhaba birincil etki alanı değişen dizininiz için var olan tüm kullanıcılar hello kullanıcı adları değişmez.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Özel etki alanı adları tooyour Azure AD ekleyin
Too900 özel etki alanı adları tooeach Azure AD dizini ekleyebilirsiniz. işlem çok hello[bir ek özel etki alanı adı ekleyin](active-directory-add-domain.md) olan hello aynı hello ilk özel etki alanı adı.

## <a name="add-subdomains-of-a-custom-domain"></a>Özel bir etki alanının alt etki alanlarını ekleme
Tooadd 'europe.contoso.com' tooyour dizini gibi bir üçüncü düzey etki alanı adı istiyorsanız, önce ekleyin ve contoso.com gibi hello ikinci düzey etki doğrulamanız gerekir. Merhaba alt etki alanı otomatik olarak Azure AD tarafından doğrulanır. Yeni eklediğiniz alt etki alanı hello toosee doğrulandı, yenileme hello sayfasını hello tarayıcıda dizininizde hello etki alanları listelenir.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Özel etki alanı adınızı hello DNS kayıt şirketi değiştirirseniz, hangi toodo
Özel etki alanı adınızı hello DNS kayıt şirketi değiştirirseniz, özel etki alanı adınızı Azure AD ile kendini kesinti olmadan ek yapılandırma görevleri ve toouse devam edebilirsiniz. Office 365, Intune veya Azure AD içinde özel etki alanı adları kullanan diğer hizmetler ile özel etki alanı adınızı kullanırsanız, bu hizmetleri toohello belgelerine başvurun.

## <a name="delete-a-custom-domain-name"></a>Özel etki alanı silme
Kuruluşunuz artık bu etki alanı adını kullanıyorsa ya da başka bir Azure AD etki alanı adını toouse gereksinim duyarsanız, özel etki alanı adı, Azure AD'den silebilirsiniz.

toodelete bir özel etki alanı adı, dizininizdeki hiçbir kaynak hello etki alanı adını kullanan ilk emin olmalısınız. Bir etki alanı adı, varsa dizininizden silinemiyor:

* Herhangi bir kullanıcı, bir kullanıcı adı, e-posta adresi veya hello etki alanı adını içeren proxy adresi vardır.
* Herhangi bir grup, bir e-posta adresi veya hello etki alanı adını içeren proxy adresi vardır.
* Azure ad herhangi bir uygulama kimliği URI'hello etki alanı adını içeren bir uygulama vardır.

Değiştirme veya hello özel etki alanı adı silmeden önce herhangi bir kaynağa Azure AD dizininizi silmeniz gerekir.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>PowerShell veya grafik API'si toomanage etki alanı adlarını kullanın
Azure Active Directory etki alanı adları için yönetim görevlerinin çoğunu Microsoft PowerShell veya program aracılığıyla Azure AD Graph API kullanarak tamamlanabilir.

* [Azure AD PowerShell toomanage etki alanı adlarını kullanma](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Azure AD grafik API'si toomanage etki alanı adlarını kullanma](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Sonraki adımlar
* [Azure AD içinde etki alanı adları hakkında bilgi edinin](active-directory-add-domain-concepts.md)
* [Özel etki alanı adlarını yönetme](active-directory-add-manage-domain-names.md)

