---
title: "tooan uygulamada oturum açarken aaaUnexpected onay istemi | Microsoft Docs"
description: "Nasıl bir kullanıcı bir uygulama için bir onay istemi gördüğünde tootroubleshoot, değil beklediğiniz neydi Azure AD ile tümleşik"
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
ms.openlocfilehash: 32b7a5e6256faee0dcfe2e1644da3d3428812d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-consent-prompt-when-signing-in-tooan-application"></a>Tooan uygulamada oturum açarken beklenmeyen onay istemi

Azure Active Directory ile tümleştirme pek çok uygulama sipariş toorun toovarious kaynaklarında izinleri gerektirir. Bu kaynaklar ayrıca Azure Active Directory ile tümleşik olduğunda bunları istenen hello Azure AD kullanarak izinleri tooaccess framework olursunuz. 

Bu, bir onay istemi hello tek seferlik bir işlem olduğu çoğunlukla bir uygulama kullanılır, ilk kez gösteriliyor sonuçlanır. 

## <a name="scenarios-in-which-users-see-consent-prompts"></a>Hangi kullanıcıların gördüğü senaryoları istemleri onayı

Ek istekler çeşitli senaryolarda beklenebilir:

* Merhaba uygulama için gereken izinleri Hello kümesi değişti.

* Başlangıçta toohello uygulama rıza hello kullanıcı yönetici değil ve şimdi farklı (yönetici olmayan) bir kullanıcı Merhaba uygulaması hello için ilk kez kullanıyor.

* ilk olarak toohello uygulama rıza hello kullanıcı için bir yönetici olsa da, bunlar hello tüm kuruluş ın adına izin değil.

* Merhaba uygulaması kullanarak [artımlı ve dinamik izin](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-compare#incremental-and-dynamic-consent) onay başlangıçta verildi sonra toorequest ek izinler. Ek bir uygulamanın isteğe bağlı özellikler ötesinde temel işlevleri için gereken izinleri gerektirir, bu genellikle kullanılır.

* Onay, başlangıçta verilmeden sonra iptal edildi.

* her kullanılışında Hello Geliştirici hello uygulama toorequire bir onay istemi yapılandırmamış (Not: Bu en iyi yöntem değildir).

## <a name="next-steps"></a>Sonraki adımlar

-   [Uygulamalar, izinler ve onay Azure Active Directory'de (v1.0 uç noktası)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)

-   [Kapsam, izinleri ve hello Azure Active Directory (v2.0 uç noktası) onay](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


