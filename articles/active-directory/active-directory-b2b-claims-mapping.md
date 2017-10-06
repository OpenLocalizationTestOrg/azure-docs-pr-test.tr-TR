---
title: "aaaB2B işbirliği kullanıcı talepleri, Azure Active Directory'de eşleme | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği için başvuru eşleme talepleri"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a>Eşleme Azure Active Directory B2B işbirliği kullanıcı talepleri

B2B işbirliği kullanıcılar için hello SAML belirtecinde verilen hello talepler özelleştiriliyor azure Active Directory (Azure AD) destekler. Bir kullanıcı toohello uygulama doğruladığında, Azure AD benzersiz olarak tanımlayan hello kullanıcı hakkında bilgileri (veya talep) içeren bir SAML belirteci toohello uygulaması verir. Varsayılan olarak, bu hello kullanıcının kullanıcı adı, e-posta adresi, ad ve Soyadı içerir. Görüntüleyin ya da hello SAML belirteci toohello uygulama hello öznitelikler sekmesi altında gönderilen hello talep düzenleyin.

Merhaba SAML belirtecinde verilen tooedit hello talepler neden gerekebilecek iki olası nedeni vardır.

1. farklı bir talep URI'ler ayarlayın veya talep değerleri toorequire Hello uygulaması yazıldı

2. Uygulamanız Azure Active Directory'de depolanan hello kullanıcı asıl adı dışında bir şey hello NameIdentifier talep toobe gerektirir.

  ![SAML belirteci görünüm talepleri](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

Bu makalede talep özelleştirme nasıl tooadd ve düzenleme talepleri hakkında daha fazla bilgi için kullanıma [hello Azure Active Directory'de önceden tümleştirilen uygulamalar için SAML belirtecinde verilen talepler özelleştiriliyor](develop/active-directory-saml-claims-customization.md). B2B işbirliği için NameID ve UPN arası Kiracı eşleme kullanıcıları, güvenlik nedenleriyle engellenir.


## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [B2B işbirliği kullanıcı özellikleri](active-directory-b2b-user-properties.md)
* [B2B işbirliği kullanıcı tooa rolü ekleme](active-directory-b2b-add-guest-to-role.md)
* [B2bB işbirliği davetleri temsilci seçme](active-directory-b2b-delegate-invitations.md)
* [Dinamik gruplar ve B2B işbirliği](active-directory-b2b-dynamic-groups.md)
* [B2B işbirliği kodu ve PowerShell örnekleri](active-directory-b2b-code-samples.md)
* [SaaS uygulamaları B2B işbirliği için yapılandırma](active-directory-b2b-configure-saas-apps.md)
* [Office 365 dış paylaşım](active-directory-b2b-o365-external-user.md)
* [B2B işbirliği kullanıcı belirteçleri](active-directory-b2b-user-token.md)
* [B2B işbirliği geçerli sınırlamalar](active-directory-b2b-current-limitations.md)
