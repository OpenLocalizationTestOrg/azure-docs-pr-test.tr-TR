---
title: "Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme"
description: "Merhaba, uygulamayı App Service'te ölçeklendirme ayrıntıları hakkında bilgi edinin."
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
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure uygulama hizmeti: Uygulama hizmeti uygulamaları ölçeklendirme
Azure App Service içinde barındırılan uygulamalar için [yoğun ölçeği elde etmek](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Ancak, bir uygulamayı ölçeklendirme "bir boyutu tüm uygun" Çözüm sahip olmayan bir karmaşık sorunudur. toocorrectly uygulamanız ölçeği tooyour uygulamaları başarı katkıda bulunan 3 önemli konu vardır:

1. Uygulama mimarisi ve onun zayıf anlama.
   * Uygulama durum bilgisi mi? Durum bilgisiz?
   * Merhaba, uygulama bileşenlerinin tümünü nelerdir?
     * Merhaba uygulaması hello darboğazları nerede?
   * Yük uygulanan tooyour uygulama olduğunda hangi ilk çalışmamasına neden olur?
2. Yük ve performans gereksinimlerini anlama hello bekleniyordu.
   * Merhaba uygulaması tooserve bin kullanıcılar gerekiyor mu? veya bir milyon?
   * Trafik tek bir coğrafi konumdan veya genel olarak gelir?
   * Mevsimlik Çeşitlemeler var mı? trafik yükselmeleri?
   * Merhaba uygulama ne kadar hızlı yanıt? 1 saniye? 1 milisaniyelik?
3. Anlama ve doğru şekilde uygulamanızı barındırma Dengeleme hello platformu.
   * Hangi özelliklerin gerektiğini ı tooachieve my ölçek hedefleri yararlanır?

Bu bölümde, tüm hello Etkenler ve ölçeklenebilirlik hedeflerinizi hello gerekli uygulama hizmeti özellikleri tooachieve yararlanan bir strateji insanlara yardım anlamanıza yardımcı olur.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

