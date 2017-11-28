---
title: "Active Directory kimlik doğrulama protokolleri aaaAzure | Microsoft Docs"
description: "Azure Active Directory (AD tarafından) desteklenen hello kimlik doğrulama protokolleri genel bakış"
documentationcenter: dev-center-name
author: priyamohanram
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 7a838ae2-c24c-4304-b6c0-e77fb888e6c0
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 1584efa83d30746075e970b8523c3abdccd34859
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory kimlik doğrulama protokolleri
Azure Active Directory (Azure AD) birkaç hello en yaygın olarak kullanılan kimlik doğrulama ve yetkilendirme kurallarının destekler. Merhaba bu bölümdeki konular, desteklenen hello protokolleri ve uygulamalarının Azure AD'de açıklanmaktadır. Merhaba konuları desteklenen talep türleri, Federasyon meta verilerini bir giriş toohello kullanımını gözden dahil, OAuth 2.0 ayrıntılı. ve SAML 2.0 protokolü başvurusu belgeleri ve sorun giderme bölümü.

## Makaleler ve başvuru kimlik doğrulama protokolleri
* [Önemli bilgiler hakkında imzalama anahtarı Rollover Azure AD'de](active-directory-signing-key-rollover.md) – Azure AD anahtar geçişi tempoyla, değişiklikler yapabilirsiniz tooupdate hello anahtarı otomatik olarak ve nasıl tooupdate hello en yaygın uygulama senaryoları için tartışma imzalama hakkında bilgi edinin.
* [Desteklenen belirteç ve talep türleri](active-directory-token-and-claims.md) -Azure AD verir hello belirteçleri hello Taleplerde hakkında bilgi edinin.
* [Federasyon meta verileri](active-directory-federation-metadata.md) -öğrenin nasıl toofind ve Azure AD oluşturur hello meta veri belgelerini çevirebilir.
* [Azure AD'de OAuth 2.0](active-directory-protocols-oauth-code.md) -hello uygulamasında OAuth 2.0 Azure AD hakkında bilgi edinin.
* [Openıd Connect 1.0](active-directory-protocols-openid-connect-code.md) -öğrenin nasıl kimlik doğrulaması için OAuth 2.0, Yetkilendirme Protokolü toouse.
* [Hizmet tooService çağrıları istemci kimlik bilgileri ile](active-directory-protocols-oauth-service-to-service.md) -nasıl hizmeti tooservice çağrıları için akışı toouse OAuth 2.0 istemci kimlik bilgileri verin öğrenin.
* [Hizmet On-Behalf-Of akış tooService aramaları](active-directory-protocols-oauth-on-behalf-of.md) -toouse hizmet tooservice için OAuth 2.0 On-Behalf-Of akışı nasıl çağırır öğrenin.
* [SAML Protokolü başvurusu](active-directory-saml-protocol-reference.md) -hello çoklu oturum açma ve tek Sign-out SAML profilleri Azure ad hakkında bilgi edinin.

## Ayrıca Bkz.
[Azure Active Directory Geliştirici Kılavuzu](active-directory-developers-guide.md)

[Azure AD kimlik doğrulaması kullanma](../../app-service-web/web-sites-authentication-authorization.md)

[Active Directory kod örnekleri](active-directory-code-samples.md)
