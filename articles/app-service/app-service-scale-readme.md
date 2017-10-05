---
title: "Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme"
description: "Uygulamayı App Service'te ölçeklendirme, ayrıntıları hakkında bilgi edinin."
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme
Azure App Service içinde barındırılan uygulamalar için [yoğun ölçeği elde etmek](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Ancak, bir uygulamayı ölçeklendirme "bir boyutu tüm uygun" Çözüm sahip olmayan bir karmaşık sorunudur. Doğru Ölçekle uygulamanız var. uygulamaları başarınız katkıda bulunan 3 önemli alanlar şunlardır:

1. Uygulama mimarisi ve onun zayıf anlama.
   * Uygulama durum bilgisi mi? Durum bilgisiz?
   * Uygulamanızın tüm bileşenleri nelerdir?
     * Uygulamada performans sorunlarını nerede?
   * Yük uygulamanıza uygulandığında ne ilk çalışmamasına neden olur?
2. Beklenen yükü ve performans gereksinimlerini anlama.
   * Uygulama bin kullanıcılar hizmet gerekiyor mu? veya bir milyon?
   * Trafik tek bir coğrafi konumdan veya genel olarak gelir?
   * Mevsimlik Çeşitlemeler var mı? trafik yükselmeleri?
   * Uygulamanın ne kadar hızlı yanıt? 1 saniye? 1 milisaniyelik?
3. Anlama ve doğru şekilde uygulamanızı barındırma platformu yararlanın.
   * My ölçek hedeflerinize ulaşmak için hangi özelliklerin yararlanıyor?

Bu bölümde, tüm Etkenler ve ölçeklenebilirlik hedeflerinize ulaşmak için gerekli uygulama hizmeti özelliklerinden yararlanır bir strateji insanlara yardım anlamanıza yardımcı olur.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

