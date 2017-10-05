---
title: "SaaS uygulamalarına erişimi yönetmek için bir grup kullanma | Microsoft Docs"
description: "Azure Active Directory Premium veya Basic grupları Azure Active Directory ile tümleşik SaaS uygulamalarına erişimi atamak için nasıl kullanılacağını."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>SaaS uygulamalarına erişimi yönetmek için grup kullanma
Bir Azure AD Premium veya Azure AD temel lisansı ile Azure Active Directory (Azure AD) kullanarak Azure AD ile tümleşik bir SaaS uygulaması erişim atamak için grupları kullanabilirsiniz. Örneğin, beş farklı SaaS uygulamaları kullanmak pazarlama departmanı için erişim atamak istiyorsanız, pazarlama departmanındaki kullanıcılar içeren bir grup oluşturabilir ve tarafından gerekli olan bu beş SaaS uygulamaları için o grubun atayın Pazarlama departmanı. Bu şekilde, tek bir yerde pazarlama departmanı üyeliğini yöneterek zaman tasarrufu sağlar. Kullanıcılar daha sonra uygulamaya pazarlama grubunun bir üyesi olarak eklenir ve pazarlama gruptan kaldırdığınızda atamalarını uygulamasından kaldırmış atanır.

> [!IMPORTANT]
> Microsoft, Azure AD’yi bu makalede bahsedilen Klasik Azure Portalı yerine Azure portalındaki [Azure AD yönetim merkezini](https://aad.portal.azure.com) kullanarak yönetmenizi öneriyor. 

Bu özellik, Azure AD uygulama galerisinde içinde ekleyebilirsiniz uygulamaları yüzlerce kullanılabilir.

**Bir SaaS uygulaması için bir grup için erişim atamak için**

1. İçinde [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory** sol taraftaki gezinti çubuğunda.
2. Seçin **Directory** sekmesini ve sonra bir SaaS uygulaması için bir grup için erişim atamak istediğiniz dizini açın.
3. Seçin **uygulamaları** sekmesi. Uygulama Galeriden eklenen bir uygulama seçin ve ardından **kullanıcılar ve gruplar** sekmesi.
4. Üzerinde **kullanıcılar ve gruplar** sekmesinde **başlayarak** alanına erişim atamak istediğiniz grubun adını girin ve ardından üst köşedeki onay işaretini seçin. Yalnızca ilk bölümü bir grubun adını yazmanız gerekir.
5. Grup seçin ve ardından **atamak erişim** düğmesi. Seçin **Evet** onay iletisi görürsünüz. Şu anda uygulamalara grup tabanlı atama yapmak için iç içe geçmiş grup üyelikleri desteklenmiyor.
6. Hangi kullanıcıların uygulamayı, doğrudan veya bir gruba üyelik tarafından atanan de görebilirsiniz. Bunu yapmak için değiştirme **'Gruplarından' açılır Göster** için **'Tüm kullanıcılar'**. Liste, dizinde ve isteyip istemediğinizi her bir kullanıcı uygulamaya atanan kullanıcıları gösterir. Liste ayrıca atanan kullanıcılar uygulamaya doğrudan ('doğrudan' gösterilen atama türü) ya da grup üyeliği ('Devralınan' gösterilen atama türü), atanmış olup olmadığını gösterir

> [!NOTE]
> Yalnızca Azure AD Premium veya Azure AD temel etkinleştirdikten sonra kullanıcılar ve Gruplar sekmesinde görebilirsiniz.
>
>

### <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile kaynaklara erişimi yönetme](active-directory-manage-groups.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Grup ayarlarını yapılandırmak için Azure Active Directory cmdlet'leri](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
