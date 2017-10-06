---
title: "azure'da kaynak erişimini aaaUnderstanding | Microsoft Docs"
description: "Bu konuda, abonelik yöneticileri toocontrol kaynak erişimini hello kullanma hakkında kavramlar açıklanmaktadır tam Azure portalı"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Azure'da kaynak erişimini anlama
> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. Hello Azure portal sağlar [rol tabanlı erişim denetimi](role-based-access-control-configure.md) Azure kaynaklarını daha kesin olarak yönetilecek şekilde.
> 
> 

Ekim 2013'te hello Klasik Azure portalı ve hizmet yönetim API'leri Azure Active Directory ile sipariş toolay hello öğrenmeniz erişim tooAzure kaynakları yönetmek için hello kullanıcı deneyimini geliştirmek için tümleşik. Azure Active Directory zaten kullanıcı yönetimi, şirket içi dizin eşitleme, çok faktörlü kimlik doğrulaması ve uygulama erişim denetimi gibi harika özellikler sağlar. Doğal olarak, bunlar ayrıca Azure kaynaklarını yönetmek için kullanılabilir across-the-board yapılması gerekir.

Azure erişim denetimi faturalandırma açısından başlatır. Merhaba hello ziyaret ederek erişilen bir Azure hesabı sahibinin [Azure hesaplar Merkezi](https://account.windowsazure.com/subscriptions), hello Hesap Yöneticisi (AA) değil. Abonelik faturalama için bir kapsayıcı olsa da, bunlar aynı zamanda bir güvenlik sınırı hareket: her abonelik bir Hizmet Yöneticisi (kimin eklemek, kaldırmak ve bu abonelik Azure kaynaklarında hello kullanarak değiştirme SA) sahip [Klasik Azure portalı](https://manage.windowsazure.com/). Yeni bir abonelik Hello varsayılan SA, hello AA olmakla birlikte hello AA hello SA'hello Azure hesaplar merkezi değiştirebilirsiniz.

<br><br>![Azure hesapları][1]

Abonelikler, bir dizin ile bir ilişkilendirme de vardır. Merhaba dizin, bir kullanıcı kümesini tanımlar. Bunlar hello iş ya da hello dizin oluşturulmuş Okul kullanıcılardan olabilir veya dış kullanıcılar (diğer bir deyişle, Microsoft Accounts) olabilir. Abonelikler, bir alt kümesini Hizmet Yöneticisi (SA) veya ortak yönetici (CA) olarak atanmış olan dizin kullanıcılar tarafından erişilebilir; Merhaba yalnızca eski nedeniyle, Microsoft Accounts (eskiden Windows Live kimliği) SA veya CA hello dizinde bulunduğundan olmadan atanabilir, istisnadır.

<br><br>![Azure erişim denetimi][2]

Merhaba Klasik Azure portalı içinde işlevini etkinleştirir bir abonelik hello kullanarak ilişkili bir Microsoft Account toochange hello dizin kullanarak imzalanmış SAs **dizini Düzenle** hello komutunu**Abonelikleri** sayfasındaki **ayarları**. Bu işlem bu aboneliğin erişim denetimini hello etkileri olduğuna dikkat edin.

> [!NOTE]
> Merhaba **dizini Düzenle** komut hello Azure Klasik portalı kullanarak bir iş imzalanmış kullanılabilir toousers değil veya Okul hesabınız bu hesaplar yalnızca toohello directory toowhich ait oldukları imzalayabilirsiniz olduğundan.
> 
> 

<br><br>![Basit kullanıcı oturum açma akışı][3]

Merhaba basit durumda, bir kuruluş (örneğin, Contoso) faturalama zorlamak ve aynı abonelikleri ayarlamak hello erişim denetimi. Diğer bir deyişle, tek bir Azure hesabı tarafından sahip olunan ilişkili toosubscriptions hello dizindir. Başarılı oturum açma toohello Klasik Azure portalı üzerinde kullanıcıları (turuncu hello önceki çizimde gösterilen) kaynakların iki koleksiyon bakın:

* (Veya yabancı sorumlu eklenen kaynaklanan) kullanıcı hesapları bulunduğu dizinleri. Dizinlerinizi günlüğe nerede bağımsız olarak her zaman gösterilecek şekilde oturum açma için kullanılan bu hello dizine ilgili toothis hesaplama değil unutmayın.
* Oturum açma için kullanılan hello dizini ile ilişkili olan ve hangi kullanıcı hello abonelikleri parçası olan kaynaklar (SA veya CA oldukları) erişebilir.

<br><br>![Birden çok aboneliğe ve dizine sahip kullanıcı][4]

Birden çok dizin Aboneliklerde kullanıcılarla hello abonelik filtresini kullanarak hello özelliği tooswitch hello geçerli bağlamı, hello Klasik Azure portalı sahip. Merhaba kapsar altında bu ayrı oturum açma tooa farklı dizinde olur, ancak bu sorunsuz çoklu oturum açma (SSO) kullanılarak gerçekleştirilir.

Kaynakları abonelikler arasında taşıma gibi işlemleri abonelikleri sonucunda bu tek bir dizin görünüm daha zor olabilir. tooperform hello kaynak aktarımı olabilir gerekli toofirst kullanmak hello **dizini Düzenle** hello abonelikler sayfasında komutunu **ayarları** tooassociate hello abonelikleri toohello aynı dizinde .

## <a name="next-steps"></a>Sonraki Adımlar
* toolearn nasıl toochange Yöneticiler bir Azure aboneliğine yönelik bakın hakkında daha fazla bilgi [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing/billing-add-change-azure-subscription-administrator.md)
* Azure Active Directory tooyour Azure aboneliği ilişkilendirilme şekli ile ilgili daha fazla bilgi için bkz: [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory-how-subscriptions-associated-directory.md)
* Hakkında daha fazla bilgi için bkz: tooassign rolleri Azure AD'de [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
