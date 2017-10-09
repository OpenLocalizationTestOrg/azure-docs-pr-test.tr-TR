---
title: "aaaAzure AD v2 JS SPA destekli Kurulumu - giriş | Microsoft Docs"
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Çağrı hello Microsoft Graph API öğesinden bir JavaScript tek sayfa uygulama (SPA)

Bu kılavuz bir JavaScript tek sayfa uygulama (SPA) kişisel, iş ne kaydolabilirsiniz gösterir ve Okul hesapları, erişim belirteci almak ve hello Microsoft Graph API çağrısı veya Azure Active Directory v2 endpoint gelen erişim belirteçleri gerektiren diğer API'leri hello.

### <a name="how-this-guide-works"></a>Bu kılavuz nasıl çalışır?

![Bu kılavuz tarafından oluşturulan hello örnek uygulaması nasıl çalışır](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Daha Fazla Bilgi

Bu kılavuz tarafından oluşturulan Merhaba örnek uygulaması JavaScript SPA tooquery hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar. Bu senaryoda, sonra bir kullanıcı oturum açtığında, bir erişim belirteci hello authorization üstbilgisi aracılığıyla istenen ve eklenen tooHTTP isteği sayısıdır. Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından işlenir.

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Kitaplıkları

Bu kılavuz kitaplığı aşağıdaki hello kullanır:

|Kitaplık|Açıklama|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|JavaScript Önizleme için Microsoft kimlik doğrulama kitaplığı|

> [!NOTE]
> *msal.js* hedefleri hello *Azure Active Directory v2 endpoint* -kişisel ve iş, okul hesapları toosign sağlar ve belirteçleri almak. Merhaba *Azure Active Directory v2 endpoint* sahip [bazı sınırlamalar](..\active-directory-v2-limitations.md). Yalnızca iş ve Okul hesapları ilgileniyorsanız kullanmak *adal.js* ve hello *V1 endpoint*. Merhaba v1 ve v2 uç noktaları arasındaki farklar toounderstand okuma hello [v1 v2 karşılaştırma](..\active-directory-v2-compare.md).

<!--end-collapse-->
