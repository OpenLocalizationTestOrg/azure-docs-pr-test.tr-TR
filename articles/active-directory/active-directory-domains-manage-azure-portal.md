---
title: "Azure Active Directory'de aaaManaging özel etki alanı adları | Microsoft Docs"
description: "Yönetim Kavramları ve Azure Active Directory'de bir etki alanı adı yönetmek için nasıl yapılır?"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Azure Active Directory'de özel etki alanı adlarını yönetme
Bir etki alanı adı hello tanımlayıcının birçok dizin kaynaklar için önemli bir parçasıdır: hello adresi bir grup için bir parçası olan bir kullanıcı için bir kullanıcı adı veya e-posta adresi bir parçasıdır ve bir uygulama için hello uygulama kimliği URI'SİNİN parçası olabilir. Azure Active Directory'de (Azure AD) bir kaynak hello kaynak içeren hello dizine ait olarak zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz. Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Azure AD dizininiz için Hello birincil etki alanı adı ayarlama
Dizininizi oluşturulduğunda 'contoso.onmicrosoft.com,' gibi hello ilk etki alanı adı da hello birincil etki alanı adıdır. Yeni bir kullanıcı oluşturduğunuzda hello birincil etki alanı hello varsayılan etki alanı için yeni bir kullanıcı adıdır. Bir birincil etki alanı adı ayarlama bir yönetici toocreate yeni kullanıcılar için hello portal hello işlemini kolaylaştırır. toochange hello birincil etki alanı adı:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Merhaba üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.
4. Merhaba üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde, toomake hello birincil etki alanı adı istediğinizi seçin hello etki alanı adı.
5. Merhaba üzerinde ***etki alanı adı*** (yeni etki alanı adınızı hello başlığında sahip açan diğer bir deyişle, hello dikey), dikey penceresinde hello seçin **birincil olun** komutu. Sorulduğunda Seçiminizi onaylayın.
   
   ![Bir etki alanı adı birincil olun](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Birleşik olmadığı herhangi doğrulanmış özel etki alanı, dizin toobe hello birincil etki alanı adını değiştirebilirsiniz. Merhaba birincil etki alanı değişen dizininiz için var olan tüm kullanıcılar hello kullanıcı adları değişmez.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Özel etki alanı adları tooyour Azure AD ekleyin
Too900 özel etki alanı adları tooeach Azure AD dizini ekleyebilirsiniz. işlem çok hello[bir ek özel etki alanı adı ekleyin](add-custom-domain.md) olan hello aynı hello ilk özel etki alanı adı.

## <a name="add-subdomains-of-a-custom-domain"></a>Özel bir etki alanının alt etki alanlarını ekleme
Tooadd 'europe.contoso.com' tooyour dizini gibi bir üçüncü düzey etki alanı adı istiyorsanız, önce ekleyin ve contoso.com gibi hello ikinci düzey etki doğrulamanız gerekir. Merhaba alt etki alanı otomatik olarak Azure AD tarafından doğrulanır. Yeni eklediğiniz alt etki alanı hello toosee doğrulandı, yenileme hello sayfasını hello tarayıcıda hello etki alanları listelenir.

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
* [Özel etki alanı adlarını Ekle](add-custom-domain.md)

