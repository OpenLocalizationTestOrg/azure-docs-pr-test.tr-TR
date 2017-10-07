---
title: "onay tooan uygulama gerçekleştirilirken beklenmeyen hata aaa | Microsoft Docs"
description: "Onaylıyorsunuz tooan uygulama ve bunları hakkında neler yapabileceğinizi hello işlemi sırasında oluşabilecek hatalar açıklanır"
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
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Onay tooan uygulama gerçekleştirirken beklenmeyen bir hata

Bu makalede onaylıyorsunuz tooan uygulama hello işlemi sırasında oluşabilecek hatalar açıklanır. Sorun giderme beklenmeyen varsa, onay ister olmayan herhangi bir hata iletisi içeren bkz [Azure AD için kimlik doğrulama senaryoları](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Azure Active Directory ile tümleştirme pek çok uygulama izinleri tooaccess sipariş toofunction diğer kaynaklar gerektirir. Bu kaynaklar ayrıca Azure Active Directory ile tümleşik olduğunda, bunları sık istenen hello ortak kullanarak izinleri tooaccess framework olursunuz. 

Bu, genellikle bir uygulama kullanılır ancak Merhaba uygulaması üzerinde bir sonraki kullanımı da oluşabilir ilk kez hello oluşan görüntülenmesini, bir onay istemi sonuçlanır.

Belirli koşullar uygulama gerektiren kullanıcı tooconsent toohello izinlerini doğru olması gerekir. Bu koşullar karşılanmazsa, çeşitli hatalar oluşabilir. Bunlar:

## <a name="requesting-not-authorized-permissions-error"></a>Yetki verilmemiş izinleri hata isteme
* **AADSTS90093:** &lt;clientAppDisplayName&gt; çalıştığınız bir veya daha fazla izinler yetkili toogrant istiyor. Kimin toothis uygulama sizin adınıza onayı bir yöneticiye başvurun.

Şirket Yöneticisi olmayan bir kullanıcı toouse yalnızca bir yönetici verebilirsiniz izinleri isteyen bir uygulama çalıştığında bu hata oluşur. Bu hata, verme erişim toohello uygulama kuruluşu adına bir yönetici tarafından çözülebilir.

## <a name="policy-prevents-granting-permissions-error"></a>İlke engeller izin verme hatası
* **AADSTS90093:** yönetici &lt;tenantDisplayName&gt; atamanızı engeller bir ilke ayarladığı &lt;uygulama adını&gt; Merhaba, istediği izinleri. Bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;, kimin izinleri toothis uygulama sizin adınıza vermek.

Kullanıcıların tooconsent tooapplications hello yeteneği şirket Yöneticisi kapatır toouse onay gerektiren bir uygulama yönetici olmayan kullanıcı deneyip daha sonra bu hata oluşur. Bu hata, verme erişim toohello uygulama kuruluşu adına bir yönetici tarafından çözülebilir.

## <a name="intermittent-problem-error"></a>Aralıklı sorun hata
* **AADSTS90090:** çalıştığınız toogrant çok hello izinleri kaydı aralıklı bir sorunla karşılaştık gibi görünüyor&lt;clientAppDisplayName&gt;. Daha sonra yeniden deneyin.

Bu hata, bir aralıklı Hizmet tarafı sorunu oluştuğunu gösterir. Tooconsent toohello uygulamayı yeniden deneyerek çözülebilir.

## <a name="resource-not-available-error"></a>Kaynak kullanılamaz hatası
* **AADSTS65005:** hello uygulama &lt;clientAppDisplayName&gt; izinleri tooaccess bir kaynağın istenen &lt;resourceAppDisplayName&gt; kullanılabilir değil. 

Merhaba uygulama geliştiricisine başvurun.

##  <a name="resource-not-available-in-tenant-error"></a>Kaynak Kiracı hata mevcut değil
* **AADSTS65005:** &lt;clientAppDisplayName&gt; erişim tooa kaynak isteyen &lt;resourceAppDisplayName&gt; , kuruluşunuzda mevcut değil &lt; tenantDisplayName&gt;. 

Bu kaynak kullanılabilir olduğundan emin olun veya bir sistem yöneticisine başvurun &lt;tenantDisplayName&gt;.

## <a name="permissions-mismatch-error"></a>İzinleri uyuşmazlığı hatası
* **AADSTS65005:** hello uygulama istenen onay tooaccess kaynak &lt;resourceAppDisplayName&gt;. Merhaba app uygulama kaydı sırasında önceden yapılandırılmış nasıl eşleşmediğinden bu isteği başarısız oldu. Kişi hello uygulama vendor.* *

Merhaba uygulaması tooconsent toois izinleri tooaccess (Kiracı) hello kuruluşunuzun dizininde bulunan bir kaynak uygulaması isteyen kullanıcı çalışırken tüm bu hataları oluşur. Bu, çeşitli nedenlerle oluşabilir:

-   Merhaba istemci uygulaması geliştirici kendi uygulama toorequest erişim tooan geçersiz kaynak neden yanlış yapılandırdı. Bu durumda, hello uygulama geliştiricisinin bu sorunu hello istemci uygulaması tooresolve hello yapılandırmasını güncelleştirmeniz gerekir.

-   Merhaba hedef kaynak uygulaması temsil eden bir hizmet sorumlusu hello kuruluşunuzda mevcut değil veya hello geçmiş vardı ancak kaldırılmıştır. Bu sorun, bir hizmet sorumlusu Merhaba istemci uygulaması izinleri tooit isteyebilir Merhaba kaynak uygulaması hello kuruluşta sağlanmalıdır için tooresolve. Uygulamanın, hello türüne bağlı olarak çeşitli yollarla bir numarasında durum olabilir dahil olmak üzere:

    -   Merhaba kaynak uygulaması (Microsoft yayımlanan uygulamaları) için bir abonelik alınıyor

    -   Onaylıyorsunuz toohello kaynak uygulama

    -   Hello Azure Portal aracılığıyla Hello uygulama izin verme

    -   Azure AD uygulama galerisinde hello Hello uygulama ekleme

## <a name="next-steps"></a>Sonraki adımlar 

[Uygulamalar, izinler ve onay Azure Active Directory'de (v1 uç noktası)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Kapsam, izinleri ve hello Azure Active Directory (v2.0 uç noktası) onay](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)


