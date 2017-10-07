---
title: "aaaDynamic grupları ve Azure Active Directory B2B işbirliği | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği dinamik Azure AD grupları ile kullanılabilir"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.reviewer: sasubram
ms.openlocfilehash: b011298de5fd2c851c6d9caaf5c2b257807ef0a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dynamic-groups-and-azure-active-directory-b2b-collaboration"></a>Dinamik gruplar ve Azure Active Directory B2B işbirliği

## <a name="what-are-dynamic-groups"></a>Dinamik grupların nelerdir?
Azure Active Directory (Azure AD) için dinamik yapılandırma, güvenlik grubunun üyeliği kullanılabilir [Azure portal hello](https://portal.azure.com). Yöneticiler, Azure Active Directory'de oluşturulan toopopulate grupları (örneğin, userType, bölüme veya ülke) kullanıcı özniteliklerini temel alarak kurallar ayarlayabilir. Üyeleri, kendi özniteliklerini temel alarak bir güvenlik grubu tooor kaldırılmasını otomatik olarak eklenebilir. Tooassign toomembers lisansları ve bu grupları tooapplications veya Bulut kaynakları (SharePoint siteleri, belgeleri) erişim sağlayabilirsiniz. Dinamik grupları hakkında daha fazla bilgiyi [ayrılmış Azure Active Directory'deki grupları](active-directory-accessmanagement-dedicated-groups.md).

Merhaba uygun [lisans Azure AD Premium P1 veya P2](https://azure.microsoft.com/pricing/details/active-directory/) gerekli toocreate ve kullanım dinamik grupları. Merhaba makalede daha fazla bilgi edinin [öznitelik tabanlı kurallar dinamik grup üyeliği için Azure Active Directory'de oluşturmak](active-directory-groups-dynamic-membership-azure-portal.md).

## <a name="what-are-hello-built-in-dynamic-groups"></a>Merhaba yerleşik dinamik grupların nelerdir?
Merhaba **tüm kullanıcılar** dinamik Grup tek bir hello kiracıdaki tüm kullanıcıları içeren bir grubu tıklatın Kiracı yöneticileri toocreate sağlar. Varsayılan olarak, hello **tüm kullanıcılar** Grup üyeleri ve konuklar gibi hello dizinde tüm kullanıcıları içerir.
Merhaba yeni Azure Active Directory Yönetim Portalı içinden tooenable hello seçebilirsiniz **tüm kullanıcılar** Grup ayarlarını görüntülemek hello grubu.

![yerleşik gruplar](media/active-directory-b2b-dynamic-groups/built-in-groups.png)

## <a name="hardening-hello-all-users-dynamic-group"></a>Sağlamlaştırma hello tüm kullanıcılar dinamik Grup
Varsayılan olarak, hello **tüm kullanıcılar** grubu B2B işbirliği (konuk) kullanıcılarınızın de içerir. Daha fazla güvenli, **tüm kullanıcılar** bir kural tooremove Konuk kullanıcılar kullanarak grup. Merhaba aşağıda gösterilmiştir hello **tüm kullanıcılar** grubunu tooexclude konuklar değiştirdi.

![tüm kullanıcılar grubu etkinleştir](media/active-directory-b2b-dynamic-groups/enable-all-users-group.png)

Böylece ilkeleri (örneğin, Azure AD koşullu erişim ilkeleri) toothem uygulayabilirsiniz yararlı toocreate yalnızca konuk kullanıcılar içeren yeni bir dinamik Grup bulabilirsiniz.
Ne tür bir grup aşağıdaki gibi görünmelidir:

![Konuk kullanıcılar Dışla](media/active-directory-b2b-dynamic-groups/exclude-guest-users.png)

## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2B işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği kullanıcı taleplerini eşleme](active-directory-b2b-claims-mapping.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
