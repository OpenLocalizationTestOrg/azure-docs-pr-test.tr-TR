---
title: "aaaAzure AD SAML Protokolü başvurusu | Microsoft Docs"
description: "Bu makalede, Azure Active Directory'de hello çoklu oturum açma ve tek Sign-Out SAML profilleri genel bir bakış sağlar."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory hello SAML Protokolü kullanma
Azure Active Directory (Azure AD) kullanan hello SAML 2.0 protokolü tooenable uygulamaları tooprovide bir çoklu oturum açma deneyimi tootheir kullanıcılar. Merhaba [çoklu oturum açma](active-directory-single-sign-on-protocol-reference.md) ve [tek oturum kapatma](active-directory-single-sign-out-protocol-reference.md) SAML profilleri Azure ad açıklayan SAML onaylar, protokolleri ve bağlamaları hello kimlik sağlayıcı hizmetine nasıl kullanılır.

SAML Protokolü hello kimlik sağlayıcısı (Azure AD) ve hello hizmet sağlayıcısı (Merhaba uygulaması) tooexchange bilgilerini kendileri hakkında gerektirir.

Bir uygulamayı Azure AD ile kaydedildikten sonra hello uygulama geliştiricisi Azure AD ile Federasyon ile ilgili bilgileri kaydeder. Bu hello içerir **yeniden yönlendirme URI'si** hello uygulamasının.

Azure Active Directory Kiracı özel ve ortak (Kiracı bağımsız) tek oturum açma ve çoklu oturum kapatma uç noktalarını kullanıma sunar. Bu URL'leri adreslenebilir konumlarını temsil eden--toohello uç nokta tooread hello meta verileri olabilmesi bunlar yalnızca bir tanımlayıcıları--değildir.

* Merhaba Kiracı özgü endpoint adresindedir `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Merhaba <TenantDomainName> yer tutucu Azure AD kiracısı Tenantıd GUID'si veya kaydedilmiş bir etki alanı adını temsil eder. Merhaba contoso.com Kiracı hello Federasyon meta verileri altındadır örneğin: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* Merhaba Kiracı bağımsız endpoint adresindedir `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. Bu uç nokta adresi **ortak** , bir kiracı etki alanı adı veya kimliği yerine görüntülenir

Azure AD yayımlar hello Federasyon meta veri belgelerini hakkında daha fazla bilgi için bkz: [Federasyon meta verileri](active-directory-federation-metadata.md).
