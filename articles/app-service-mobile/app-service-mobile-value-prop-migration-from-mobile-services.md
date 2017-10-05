---
title: "Mobile Services kullanıyorum, App Service bana nasıl yardımcı olur?"
description: "App Service’in mevcut Mobile Services projelerinize sağladığı avantajları öğrenin."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 22397b6b448b418d5b54a457c3bafaf5c68ecc7b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="getting-started"> </a>Mobile Services kullanıyorum, App Service bana nasıl yardımcı olur?
## <a name="overview"></a>Genel Bakış
Mevcut Mobil Hizmetiniz güvendedir ve desteklenmeye devam edecektir. Ancak *Azure App Service* platformunun sağladığı, mobil uygulamanız için bugün Mobile Services’de bulunmayan çok sayıda avantaj vardır:

* Web ve mobil istemciler içeren uygulamalar için daha basit, daha kolay ve daha düşük maliyetli teklifler.
* Web İşleri, özel CNames, daha iyi izleme dahil yeni ana bilgisayara özellikleri.
* Traffic Manager ile anahtar teslimi tümleştirmesi
* Karma Bağlantılara ek olarak, VNet kullanarak şirket içi kaynaklarınıza ve VPN’lere bağlantı
* NewRelic veya AppInsights kullanarak uygulamanız için izleme, uyarma ve sorun giderme.
* Temel hesaplama kaynakları ve fiyatlandırma için daha zengin yelpaze
* Yerleşik otomatik ölçeklendirme, yük dengeleme ve performans izleme
* Yerleşik hazırlık, yedekleme, geri alma ve üretim sırasında test etme özellikleri

## <a name="new-hosting-features"></a>Yeni barındırma özellikleri
*Azure App Service*’de *Mobil Uygulama* arka uç kodu; Web Uygulaması ve API Uygulaması ile aynı kapsayıcıda çalışır. Böylece, şu anda Mobile Services’de bulunmayan bazıları dahil, bu kapsayıcıdaki tüm özelliklerden faydalanabilirsiniz.

* Web İşleri aracılığıyla sürekli çalışan arka uç mantığı ekleyin
* Arka uç kodunuzun her zaman çalıştığından emin olun
* Mobil arka uç, uç noktalarınıza kolay ve kararlı adlar sağlamak için özel CNames kullanın
* Traffic Manager ile uygulamanızı coğrafi olarak ölçeklendirin
* İstediğiniz tüm kitaplıkları ve paketleri ekleyin.
* (.NET için) MVC dahil, ASP.NET’in her özelliğinden yararlanın
* (Node.js için) Ortak MVC kitaplıkları dahil, Düğüm ekosisteminin tüm saf JavaScript kitaplığından yararlanın.

## <a name="access-on-premises-data-using-vnet"></a>VNet kullanarak şirket içi verilere erişin
Günümüzde, Mobile Services ile şirket için kaynaklara erişim için Karma Bağlantıları halihazırda kullanabilirsiniz. Ancak bir VPN çözümünün tercih edildiği durumlar vardır. *Azure App Service* ile Mobil Uygulama arka uç kodunuz için Azure VNet kullanabilirsiniz.

## <a name="use-your-favorite-backend-language"></a>Sık kullanılan arka uç dilinizi kullanın
*Azure App Service* ASP.NET ve Node.js platformları için, en son çalışma zamanları dahil, daha geniş ve daha zengin bir destek sunar.

## <a name="set-up-automatic-scale"></a>Otomatik ölçeklendirme ayarlayın
Mobile Services ile arka uç kodunuzun tm örnekleri küçük VM’lerde çalışıyordu. *Azure App Service*, VM boyutlarını çok daha zengin seçeneklerle seçmenizi sağlar. Ayrıca çeşitli performans ölçümleri temelinde, gelen müşteri yükünü işlemek için hızlı şekilde ölçeği artırabilir ya da genişletebilirsiniz.

## <a name="be-in-the-know"></a>“Haberdar” olun
Sizi ve ekibinizi otomatik bilgilendiren izleme ve uyarılarla gerçek zamanlı olarak sorulara yanıt verin. Mobil uygulamanızın nasıl çalıştığına ilişkin daha zengin bir öngörü sahibi olmak için New Relic ve AppInsights’dan gelen gelişmiş uygulama analizi ve izleme özelliğini tümleştirin. *Azure App Service* ile programlı şekilde ya da Azure Portal aracılığıyla, çeşitli performans ölçümleri temelinde uyarılar ayarlayabilirsiniz.

## <a name="keep-your-assets-safe"></a>Varlıklarınızı güvende tutun
Arka ucunuzu ve veritabanınızı otomatik olarak yedekleyin. Kodunuz ve verileriniz olağanüstü durumlara karşı güvendedir ve kolayca geri yüklenebilir, böylece işletmenizi güvenle çalıştırabilirsiniz.

## <a name="ready-stage-go"></a>Hazır Ol, Hazırla, Başla!
*Azure App Service* ile artık mobil uygulamalarınız için birden fazla özel test ve hazırlık ortamı oluşturabilirsiniz. Dağıtmadan önce, bunları test gerçekleştirmek için kullanın. Kesinti süresi olmaksızın üretime geçin. Web uygulamaları, en iyi müşteri deneyimi sağlayacak şekilde önceden yüklenmiştir.

Bu [öğreticiyi](app-service-mobile-migrating-from-mobile-services.md) izleyerek mevcut Mobil Hizmetiniz için *App Service* avantajından yararlanmaya başlayabilirsiniz.
