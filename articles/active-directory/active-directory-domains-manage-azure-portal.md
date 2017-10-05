---
title: "Azure Active Directory'de özel etki alanı adlarını yönetme | Microsoft Docs"
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
ms.openlocfilehash: 402c1be07b8ee885ee5341128fb3f419611b924d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Azure Active Directory'de özel etki alanı adlarını yönetme
Bir etki alanı adı tanımlayıcının birçok dizin kaynaklar için önemli bir parçasıdır: kullanıcı, bir grup adresi parçası için bir kullanıcı adı veya e-posta adresi bir parçasıdır ve bir uygulama için uygulama kimliği URI'SİNİN parçası olabilir. Azure Active Directory'de (Azure AD) bir kaynak, kaynak içeren dizine ait olarak zaten doğrulanmış bir etki alanı adı ekleyebilirsiniz. Yalnızca genel yönetici Azure AD etki alanı yönetimi görevlerini gerçekleştirebilir.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Azure AD dizininiz için birincil etki alanı adı ayarlama
Dizininizi oluşturulduğunda 'contoso.onmicrosoft.com,' gibi bir ilk etki alanı adı da birincil etki alanı adıdır. Yeni bir kullanıcı oluşturduğunuzda, birincil etki alanı varsayılan etki alanı için yeni bir kullanıcı adıdır. Bir birincil etki alanı adı ayarlama Portalı'nda yeni kullanıcılar oluşturmak bir yöneticinin işlemini kolaylaştırır. Birincil etki alanı adını değiştirmek için:

1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.
   
   ![Açılış kullanıcı yönetimi](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Üzerinde ***dizin adı*** dikey penceresinde, select **etki alanı adları**.
4. Üzerinde  ***dizin adı* -etki alanı adları** dikey penceresinde istediğiniz etki alanı adı seçin, birincil etki alanı adı olun.
5. Üzerinde ***etki alanı adı*** (yeni etki alanı adınızı başlığında sahip açan diğer bir deyişle, dikey), dikey penceresinde seçin **birincil olun** komutu. Sorulduğunda Seçiminizi onaylayın.
   
   ![Bir etki alanı adı birincil olun](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Birleşik olmadığı herhangi doğrulanmış özel etki alanı olmasını dizininiz için birincil etki alanı adını değiştirebilirsiniz. Dizininiz için birincil etki alanı değiştirme var olan tüm kullanıcılar kullanıcı adlarını değiştirmez.

## <a name="add-custom-domain-names-to-your-azure-ad"></a>Azure AD ile özel etki alanı adlarını Ekle
Her Azure AD dizinine 900 özel etki alanı adları ekleyebilir. İşleme [bir ek özel etki alanı adı ekleyin](add-custom-domain.md) ilk özel etki alanı adı için aynıdır.

## <a name="add-subdomains-of-a-custom-domain"></a>Özel bir etki alanının alt etki alanlarını ekleme
'Europe.contoso.com' gibi bir üçüncü düzey etki alanı adı dizininize eklemek istiyorsanız, önce ekleyin ve contoso.com gibi ikinci düzey etki alanı doğrulamanız gerekir. Alt etki alanı otomatik olarak Azure AD tarafından doğrulanır. Yeni eklediğiniz alt etki alanı doğrulandı görmek için etki alanları listelenir tarayıcıda sayfayı yenileyin.

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a>Özel etki alanı adınız için DNS kayıt şirketi değiştirirseniz yapmanız gerekenler
Özel etki alanı adınız için DNS kayıt şirketi değiştirirseniz, Azure AD ile kendini kesinti olmadan ek yapılandırma görevleri ve özel etki alanı adınızı kullanmaya devam edebilirsiniz. Office 365, Intune veya Azure AD içinde özel etki alanı adları kullanan diğer hizmetler ile özel etki alanı adınızı kullanırsanız, bu hizmetlerin belgelerine bakın.

## <a name="delete-a-custom-domain-name"></a>Özel etki alanı silme
Kuruluşunuz artık bu etki alanı adını kullanıyorsa ya da bu etki alanı adı başka bir Azure AD ile kullanmanız gerekiyorsa, özel etki alanı adı, Azure AD'den silebilirsiniz.

Bir özel etki alanı adı silmek için önce dizininizdeki hiçbir kaynak etki alanı adını kullanan emin olmalısınız. Bir etki alanı adı, varsa dizininizden silinemiyor:

* Herhangi bir kullanıcı, bir kullanıcı adı, e-posta adresi veya etki alanı adını içeren proxy adresi vardır.
* Herhangi bir grup, bir e-posta adresi veya etki alanı adını içeren proxy adresi vardır.
* Azure ad herhangi bir uygulama, bir uygulama etki alanı adını içeren kimliği URI sahiptir.

Değiştirme veya özel etki alanı adını silmeden önce herhangi bir kaynağa Azure AD dizininizi silmeniz gerekir.

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a>Etki alanı adlarını yönetmek için PowerShell veya grafik API'sini kullanın
Azure Active Directory etki alanı adları için yönetim görevlerinin çoğunu Microsoft PowerShell veya program aracılığıyla Azure AD Graph API kullanarak tamamlanabilir.

* [Azure AD içinde etki alanı adlarını yönetmek için PowerShell kullanma](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Azure AD içinde etki alanı adlarını yönetmek için grafik API'si kullanma](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Sonraki adımlar
* [Özel etki alanı adlarını Ekle](add-custom-domain.md)

