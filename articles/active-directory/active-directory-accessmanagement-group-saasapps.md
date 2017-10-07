---
title: "bir grup toomanage erişim tooSaaS uygulamaları aaaUsing | Microsoft Docs"
description: "Nasıl toouse grupları Azure Active Directory Premium veya Basic tooassign Azure Active Directory ile tümleşik tooSaaS uygulamaları erişin."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Bir grup toomanage erişim tooSaaS uygulamaları kullanma
Bir Azure AD Premium veya Azure AD temel lisansı ile Azure Active Directory (Azure AD) kullanarak Azure AD ile tümleşik grupları tooassign access tooa SaaS uygulaması kullanabilirsiniz. Örneğin, tooassign erişim hello pazarlama departmanı toouse beş farklı SaaS uygulamaları için isterseniz, hello pazarlama departmanındaki hello kullanıcıları içeren bir grup oluşturabilir ve bu Grup toothese beş SaaS uygulamaları atayın Merhaba pazarlama departmanı tarafından gerekli. Bu şekilde pazarlama departmanı tek bir yerde hello hello üyeliğini yöneterek zaman tasarrufu sağlar. Kullanıcılar, ardından hello pazarlama grubunun bir üyesi olarak eklenir ve pazarlama grubunun hello kaldırıldığında atamalarını hello uygulamasından kaldırmış toohello uygulama atanır.

> [!IMPORTANT]
> Microsoft önerir hello kullanarak Azure AD'yi yönetme [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) hello yerine Azure portal hello bu makalede başvurulan Klasik Azure portalı. 

Bu özellik, Azure AD uygulama galerisinde hello içinde ekleyebilirsiniz uygulamaları yüzlerce kullanılabilir.

**bir grup tooa SaaS uygulaması için tooassign erişim**

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory** hello hello sol taraftaki gezinti çubuğunda.
2. Select hello **Directory** sekmesini ve ardından açık hello dizin tooassign erişim grubu tooa SaaS uygulaması için istediğiniz.
3. Select hello **uygulamaları** sekmesi. Uygulama Galerisi hello eklenen bir uygulama seçin ve hello ardından **kullanıcılar ve gruplar** sekmesi.
4. Merhaba üzerinde **kullanıcılar ve gruplar** sekmede hello **başlayarak** hello ad alanına, tooassign erişim istediğiniz hello Grup toowhich ve ardından sağ üst hello onay işareti seçin hello. Yalnızca tootype hello ilk bölümü bir grubun adı gerekir.
5. Merhaba grubunu seçin ve ardından hello seçip **atamak erişim** düğmesi. Seçin **Evet** hello onay iletisi görürsünüz. İç içe geçmiş grup üyelikleri grup tabanlı atama tooapplications için şu anda desteklenmiyor.
6. Hangi kullanıcıların toohello uygulama, doğrudan veya bir gruba üyelik tarafından atanan de görebilirsiniz. toodo Bu, değişiklik hello **'Gruplarından' açılır Göster** çok**'Tüm kullanıcılar'**. Merhaba liste hello dizin ve isteyip istemediğinizi her kullanıcı toohello uygulama atanmış kullanıcıları gösterir. Merhaba liste hello atanan kullanıcıların doğrudan toohello uygulama ('doğrudan' gösterilen atama türü) atanmış olup olmadığını veya grup üyeliği ('Devralınan' gösterilen atama türü), ayrıca gösterir

> [!NOTE]
> Yalnızca Azure AD Premium veya Azure AD temel etkinleştirdikten sonra hello kullanıcılar ve Gruplar sekmesinde görebilirsiniz.
>
>

### <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
