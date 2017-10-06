---
title: "aaaHow toochange hello belirteç ömrü özel geliştirilmiş bir uygulama için varsayılan olarak | Microsoft Docs"
description: "Nasıl üzerinde Azure AD geliştirdiğiniz uygulamanız için tooupdate belirteç ömrü ilkeleri"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>Nasıl toochange hello belirteç ömrü özel geliştirilmiş bir uygulama için varsayılanları

Azure AD Premium uygulama geliştiricileri ve Kiracı yöneticileri tooconfigure hello ömrü gizli olmayan istemciler için yayınlanan belirteçleri sağlar. Belirteç ömrü ilkeleri Kiracı genelinde veya erişilen hello kaynakların üzerinde ayarlanır.

 * bir belirteç ömrü ilkesi tooset, gereksinim duyduğunuz toodownload hello [Azure AD PowerShell Modülü](https://www.powershellgallery.com/packages/AzureADPreview).

 * Merhaba çalıştırmak **Connect-Azuread'i-Onayla** komutu.

 * Merhaba Maksimum yaş tek Faktörlü yenileme belirteci ayarlar bir örnek İlkesi aşağıdadır. Hello ilkesi oluşturun:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Checkout hello [yapılandırma belirteç ömrü](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) toolearn nasıl belge toocreate diğer özel.

## <a name="next-steps"></a>Sonraki adımlar
[Belirteç ömrü yapılandırma](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD belirteç başvurusu](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

