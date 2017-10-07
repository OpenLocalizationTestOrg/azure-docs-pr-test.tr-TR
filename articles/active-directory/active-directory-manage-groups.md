---
title: "aaaUse grupları Azure Active Directory'de toomanage erişim tooresources | Microsoft Docs"
description: "Nasıl toouse gruplara Azure Active Directory toomanage kullanıcı tooon içi ve bulut uygulamalarına ve kaynaklarına erişebilirsiniz."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Azure Active Directory grupları ile erişim tooresources yönetme
Azure Active Directory (Azure AD) şu özellikleri toomanage erişim tooon içi ve bulut uygulamalarını ve Office 365 gibi Microsoft Çevrimiçi hizmetler gibi kaynakları güçlü bir kümesi sağlayan kapsamlı bir kimlik ve erişim yönetimi çözüm ve Microsoft olmayan SaaS uygulamaları dünyasına. Bu makalede genel bir bakış sağlar, ancak isterseniz Azure AD kullanarak toostart şu anda gruplar, hello yönergeleri izleyin [Azure AD'deki güvenlik gruplarını yönetme](active-directory-accessmanagement-manage-groups.md). Toosee istiyorsanız, PowerShell toomanage nasıl kullanabileceğiniz daha fazla okuyabilir Azure Active Directory'deki grupları [Grup Yönetimi için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> Azure Active Directory toouse, bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, şunları yapabilirsiniz [ücretsiz bir Azure hesabı için kaydolun](https://azure.microsoft.com/pricing/free-trial/).
>
>

Azure AD içinde hello önemli özelliklerin hello özelliği toomanage erişim tooresources biridir. Bu kaynaklar hello dizin ya da SaaS uygulamaları, Azure Hizmetleri ve SharePoint siteleri veya şirket içi gibi dış toohello directory kaynaklarını rolleri aracılığıyla izinleri toomanage nesnelerin hello durumda olduğu gibi hello dizin parçası olabilir kaynaklar. Kullanıcı erişim haklarını tooa kaynak atanabilir dört yolu vardır:

1. Doğrudan atama

    Kullanıcılar bu kaynak hello sahibi tarafından doğrudan tooa kaynak atanabilir.
2. Grup üyeliği

    Bir grup tooa kaynak hello kaynak sahibi tarafından ve bunu yaparak bu Grup erişim toohello kaynak hello üyeleri verme atanabilir. Merhaba grubunun üyeliği sonra hello Grup hello sahibi tarafından yönetilebilir. Etkili bir şekilde hello kaynak sahibi temsilciler izin tooassign kullanıcılar tootheir kaynak toohello hello grubun sahibi hello.
3. Kural tabanlı

    Merhaba kaynak sahibi hangi kullanıcıların erişim tooa kaynak atanmalıdır bir kural tooexpress kullanabilirsiniz. Bunu yaparak, hello kaynak sahibi etkili bir şekilde hello sağ toomanage erişim tootheir kaynak toohello yetkili kaynağı hello atar ve hello kural Hello sonucunu, kural ve değerleri, belirli kullanıcılar için kullanılan hello öznitelikler bağlıdır Merhaba kuralda kullanılan öznitelikleri. Merhaba kaynak sahibi hala hello kural kendisi yönetir ve hangi öznitelikleri ve değerleri erişim tootheir kaynak sağlamak belirler.
4. Dış yetkilisi

    Merhaba erişim tooa kaynak bir dış kaynaktan elde edilir; Örneğin, bir şirket içi dizin gibi yetkili bir kaynak veya WorkDay gibi bir SaaS uygulaması eşitlenen bir grup. Merhaba Grup tooprovide erişim toohello kaynak Hello kaynak sahibi atar ve hello dış kaynak hello grubunun üyeleri, hello yönetir.

   ![Erişim Yönetimi diyagramı genel bakış](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Erişim Yönetimi açıklayan bir videoyu izleyin
Bu konuda daha açıklayan kısa bir video izleyebilirsiniz:

**Azure AD: Giriş toodynamic üyelik grupları için**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Nasıl erişim yönetimini Azure Active Directory çalışma?
Merhaba hello Azure AD erişim yönetimi çözümü merkezinin hello güvenlik grubudur. Bir güvenlik grubu toomanage erişim tooresources hello hedeflenen kullanıcı grubuna bir esnek ve kolay anlaşılır şekilde tooprovide erişim tooa kaynak izin veren bir iyi bilinen standardı kullanmaktır. Merhaba kaynak sahibi (veya hello dizinin hello Yöneticisi) bir grup tooprovide oldukları bir belirli erişim sağ toohello kaynakları atayabilirsiniz. Merhaba grubunun üyeleri, hello hello erişim sağlanması ve hello kaynak sahibi hello sağ toomanage hello üyeleri bir bölüm Yöneticisi'ni veya bir Yardım Masası Yöneticisi gibi başka bir grup toosomeone listesi atayabilirsiniz.

![Azure Active Directory erişim yönetimi diyagramı](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

bir grubun Hello sahibi, ayrıca bu grubun Self Servis isteklerine için kullanılabilir yapabilirsiniz. Bunu yaparken, bir son kullanıcı aramak ve hello Grup bulabilir ve etkili bir şekilde hello grubu üzerinden yönetilir izni tooaccess hello kaynaklarını arayan bir istek toojoin olun. Böylece katılma istekleri otomatik olarak onaylanır veya hello grubunun hello sahibinin onayı iste hello grubunun hello sahibi hello grubu ayarlayabilirsiniz. Bir kullanıcı grubu istek toojoin yaptığında hello katılma isteğini toohello hello grubun sahiplerini iletilir. Merhaba sahiplerinden biri hello isteği onaylarsa, hello istekte bulunan kullanıcı bildirimi ve hello kullanıcı birleştirilmiş toohello grubudur. Merhaba sahiplerinden biri hello isteği reddeder, hello istekte bulunan kullanıcı bilgilendirilir ancak toohello Grup katılmamış.

## <a name="getting-started-with-access-management"></a>Access management ile çalışmaya başlama
Hazır tooget başladı? Azure AD grupları ile yapabileceğiniz hello temel görevlerden bazıları çıkışı denemelisiniz. Bu özellikleri tooprovide özelleştirilmiş kullanım toodifferent grupları kişilerin kuruluşunuzdaki farklı kaynaklar için erişim. Temel ilk adımlar listesi aşağıda listelenmektedir.

* [Bir grup yönelik dinamik üyelikler tooconfigure basit bir kural oluşturma](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Bir grup toomanage erişim tooSaaS uygulamaları kullanma](active-directory-accessmanagement-group-saasapps.md)
* [Bir grup için son kullanıcı Self Servis kullanıma](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect'i kullanarak bir şirket içi Grup tooAzure eşitleniyor](active-directory-aadconnect.md)
* [Bir grubun sahiplerini yönetme](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Sonraki adımlar
Erişim Yönetimi hello temelleri anladım, burada kullanılabilir ek bazı gelişmiş özelliklerin Azure Active Directory'ye erişim tooyour uygulamaları ve kaynakları yönetmek için.

* [Kuralları Gelişmiş toocreate öznitelikleri kullanma](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Azure AD içinde güvenlik gruplarını yönetme](active-directory-accessmanagement-manage-groups.md)
* [Azure AD içinde ayrılmış grupları ayarlama](active-directory-accessmanagement-dedicated-groups.md)
* [Gruplar için grafik API'si başvurusu](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
