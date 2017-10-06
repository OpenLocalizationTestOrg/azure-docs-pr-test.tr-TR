---
title: "Uygulama proxy'si uygulama aaaAn çok uzun tooload alır | Microsoft Docs"
description: "Hello Azure AD uygulama proxy'si sayfa yükleme performans sorunlarını giderme"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Uygulama proxy'si uygulamanın çok uzun tooload alır

Bu makale neden bir Azure AD uygulama proxy'si uygulama sürebilir uzun süre tooload ve ne toounderstand yardımcı bu sorunu tooresolve yapabilirsiniz.

## <a name="overview"></a>Genel Bakış
Uygulamalarınızı çalışıyoruz ancak uzun bir gecikme bkz, ağ topolojinizi tooimprove hello hızını göz önünde bulundurabilirsiniz bazı küçük tweaks olabilir. Hello farklı topolojilerinin değerlendirme için bkz: [ağ konuları belge](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Bu konuları yardımcı olmuyorsa, biz ne yazık ki şu anda yoksa performans ayarlaması için diğer öneriler. Merhaba uygulama proxy'si hizmeti daha yakından tooyou olabilir toomore veri merkezleri genişletir gibi geliştirilmiş toosee gecikme doğrudan başlayabilir. toosee hello tam listesini Azure veri merkezleri, hello görebilirsiniz [gecikme test sayfası](http://www.azurespeed.com/Azure/Latency). 

Merhaba hello uygulama proxy'si hizmeti ile veri merkezleri ile Merhaba bulunabilir [Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Uygulama proxy'si veri merkezi konumlarını geri bildirimi 
Uygulama proxy'si olarak henüz içerme ancak tooa harika gecikme geliştirme, sunulmasını Azure veri merkezlerinde olabilir. Merhaba veri merkezi konumda < aadapfeedback@microsoft.com > biz genişletin gibi biz geri bildirim tooplan kullanabilirsiniz.

Biz hello gecikme süresi şu anda uzun gecikme bkz kiracılar için geliştirilmesine yardımcı olun bazı ek özellikler üzerinde çalıştığınız ve emin tooshare belgeleri kullanılabilir sonra olmalıdır.

## <a name="next-steps"></a>Sonraki adımlar
[Mevcut şirket içi proxy sunucuları ile çalışma](application-proxy-working-with-proxy-servers.md)
