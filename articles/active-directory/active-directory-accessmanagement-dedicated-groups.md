---
title: "Azure Active Directory'de aaaDedicated gruplarını | Microsoft Docs"
description: "Azure Active Directory ve nasıl oluşturulduğunu nasıl ayrılmış gruplar işlerinde genel bakış."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Azure Active Directory'de ayrılmış gruplar
Azure Active Directory'de (Azure AD), hello ayrılmış gruplar özelliği otomatik olarak oluşturur ve önceden tanımlanmış Azure AD grupları üyeliğini doldurur. Ayrılmış gruplarının üyeleri eklenemez veya kaldırılan kullanarak hello Azure Klasik portalı, Windows PowerShell cmdlet'lerini veya program aracılığıyla.

> [!NOTE]
> Bir Azure AD Premium lisansı atanmış ayrılmış gruplar gerektirir
>
> * Merhaba grupta kuralı yöneten hello Yöneticisi
> * toobe hello grubunun bir üyesi tarafından hello seçilen tüm kullanıcılar kural
>
>

**ayrılmış tooenable grupları**

1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com)seçin **Active Directory**ve ardından, kuruluşunuzun dizininde açın.
2. Select hello **grupları** sekmesini ve ardından açık hello grubu tooedit.
3. Select hello **yapılandırma** sekmesini tıklatın ve ardından **ayrılmış gruplar etkinleştirmek** çok**Evet**.

Ayrılmış gruplar etkinleştirmek geçiş hello çok ayarlandıktan sonra**Evet**, daha fazla etkinleştirebilirsiniz hello dizin tooautomatically ayarı hello tarafından hello tüm kullanıcılar ayrılmış Grup Oluştur **etkinleştir "Tüm kullanıcılar" grubu** çok geçiş**Evet**. Sonra da bu adanmış grubunun hello adı hello yazarak düzenleyebilirsiniz **"Tüm kullanıcılar" için görünen ad grup** alan.

Merhaba tüm kullanıcılar Grup kullanılabilir tooassign hello dizininizdeki aynı izinleri tooall hello kullanıcılara. Örneğin, hello tüm kullanıcılar ayrılmış Grup toothis uygulama için erişim atayarak tüm kullanıcılar, dizin erişim tooa SaaS uygulamasına verebilirsiniz.

ayrılmış hello tüm kullanıcılar Grup konuklar ve dış kullanıcılar dahil olmak üzere hello dizinde tüm kullanıcıları içerir. Bir grup ihtiyacınız varsa, dış kullanıcılar hariç, ardından bir öznitelik tabanlı dinamik kuralı ile Merhaba aşağıdaki gibi bir grup oluşturarak bunu gerçekleştirebilirsiniz:

                (user.userPrincipalName -notContains "#EXT#@")

Tüm konuklar dışlar bir grup için bir kural hello aşağıdaki gibi kullanın:

                (user.userType -ne "Guest")

konusunda toolearn toocreate *Gelişmiş* kuralları (birden çok karşılaştırma içeren kurallar) dinamik grup üyeliği için bkz: [öznitelikleri toocreate kullanarak gelişmiş kurallar](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Azure Active Directory grupları ile erişim tooresources yönetme](active-directory-manage-groups.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
* [Azure Active Directory nedir?](active-directory-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
