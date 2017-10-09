---
title: "self servis uygulamaya erişim yönetimi için Azure Active Directory yukarı aaaSetting | Microsoft Docs"
description: "Self Servis Grup Yönetimi kullanıcıları toocreate sağlar ve güvenlik grupları veya Office 365 grupları Azure Active Directory ve teklifleri kullanıcılar hello olasılığı toorequest güvenlik grubu veya Office 365 grup üyeliği yönetme"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Self servis grup yönetimi için Azure Active Directory'yi ayarlama
Self Servis Grup Yönetimi, kullanıcıların toocreate sağlar ve güvenlik grupları veya Office 365 grupları Azure Active Directory'de (Azure AD) yönetin. Kullanıcılar ayrıca güvenlik grubu veya Office 365 grup üyeliği isteyebilir ve ardından hello hello grubun sahibi onaylayabilir veya üyelik reddet. Bu şekilde, grup üyeliği günlük denetimi o üyeliğe ilişkin hello iş bağlamı anlamak temsilci toopeople olabilir. Self servis grup yönetimi özellikleri yalnızca güvenlik grupları ve Office 365 grupları için kullanılabilir, ancak posta etkin güvenlik grupları veya dağıtım listeleri için kullanılamaz.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı.

Self servis grup yönetimi, şu anda iki temel senaryo içerir: temsilcili grup yönetimi ve self servis grup yönetimi.

* **Temsilcili Grup Yönetimi** hello şirket kullanarak tooa SaaS uygulamasına erişimi yöneten bir yönetici bir örnektir. Bu yönetici yeni bir grup hello iş sahibi toocreate ister için bu erişim haklarını yönetmek sıkıcı durumundadır. Hello Yöneticisi hello uygulama toohello yeni grup için erişim atar ve zaten toohello uygulamaya erişmeyi herkes toohello grubu ekler. Hello işletme sahibi daha sonra daha fazla kullanıcı ekleyebilir ve otomatik olarak sağlanan toohello uygulama bu kullanıcılardır. Merhaba işletme sahibi toowait hello yönetici toomanage erişimi kullanıcılar için gerekli değildir. Hello Yöneticisi verirse hello aynı izni tooa Yöneticisi'nde farklı bir iş grubunun, bu kişi ayrıca kendi kendi kullanıcılarının erişimini yönetebilir. Merhaba işletme sahibi ne hello Yöneticisi görüntüleyebilir veya diğer kişilerin kullanıcıları yönetme. Hello Yöneticisi hala erişim toohello uygulama ve gerekirse erişim haklarını engelleyebilir olan tüm kullanıcıları görebilirsiniz.
* **Self servis grup yönetimi** SharePoint Online sitelerine sahip olan ve bu siteleri ayrı şekilde ayarlayan iki kullanıcı, bu senaryoya örnek olarak verilebilir. Toogive her diğer kişilerin erişimini tootheir siteleri ekipleri isterler. tooaccomplish Bu, Azure AD'de bir grup oluşturabilirsiniz ve SharePoint Online ile bunların her biri bu Grup tooprovide erişim tootheir siteleri seçer. Birisi erişim istediğinde erişim paneli hello istekte ve onay sonrası erişim tooboth SharePoint Online sitesine otomatik olarak elde. Daha sonra bunlardan birini hello sitesine erişen tüm kişilerin de erişim tooa belirli SaaS uygulamasına aldığından emin karar verir. Hello Yöneticisi hello SaaS uygulamasına hello uygulama toohello SharePoint Online sitesi için erişim hakları ekleyebilirsiniz. Daha sonra onaylanmış istekleri erişim toohello iki SharePoint Online siteleri ve ayrıca toothis SaaS uygulaması sağlar.

## <a name="making-a-group-available-for-end-user-self-service"></a>Bir grubu, son kullanıcı self servisi için kullanıma sunma
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), Azure AD dizininizi açın.
2. Merhaba üzerinde **yapılandırma** sekmesinde, ayarlamak **Grup Yönetimi için temsilci** tooEnabled.
3. Ayarlama **kullanıcılar güvenlik grupları oluşturabilir** veya **kullanıcılar Office grupları oluşturabilir** tooEnabled.

Zaman **kullanıcılar güvenlik grupları oluşturabilir** olan etkinleştirildiğinde, dizininizdeki tüm kullanıcılara toocreate yeni güvenlik grubuna izin verilir ve üyeleri toothese grupları ekleyin. Bu yeni gruplar da diğer tüm kullanıcılar için erişim paneli hello görünmesini. Hello ilke ayarını hello grubunda izin veriyorsa, diğer kullanıcıların istekleri toojoin bu grupları oluşturabilirsiniz. **Kullanıcılar güvenlik grupları oluşturabilir** seçeneği devre dışı ise kullanıcılar grup oluşturamaz ve sahibi oldukları mevcut grupları değiştiremez. Ancak, bunlar hala hello bu grupların üyeliklerini yönetebilir ve bunları gruplara diğer kullanıcıların toojoin gelen istekleri onaylayabilir.

Aynı zamanda **güvenlik grupları için Self Servis kullanabilen kullanıcılar** tooachieve kullanıcılarınız için Self Servis Grup Yönetimi üzerinde daha ayrıntılı bir erişim denetimi. Zaman **kullanıcılar, gruplar oluşturabilir** olan etkinleştirildiğinde, dizininizdeki tüm kullanıcılara toocreate yeni gruplar kullanılabilir ve üyeleri toothese grupları ekleyin. Ayrıca ayarlayarak **güvenlik grupları için Self Servis kullanabilen kullanıcılar** tooSome, kısıtlama Grup Yönetimi tooonly sınırlı bir kullanıcı grubu. Bu anahtar tooSome ayarladığınızda, yeni gruplar oluşturabilir ve üye toothem eklemek için önce kullanıcıların toohello Grup SSGMSecurityGroupsUsers eklemeniz gerekir. Ayarlayarak **güvenlik grupları için Self Servis kullanabilen kullanıcılar** tooAll, tüm kullanıcılar, dizin toocreate yeni gruplarında etkinleştirin.

Merhaba de kullanabilirsiniz **güvenlik grupları için Self Servis kullanan Grup** toospecify üyeleri, Self Servis kullanabileceğiniz bir grup için bir özel ad kutusuna.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
