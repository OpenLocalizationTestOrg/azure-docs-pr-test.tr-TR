---
title: "Azure Portal kullanarak Web uygulaması kopyalama"
description: "Web uygulamalarınızı Azure Portal kullanarak yeni Web uygulamaları için kopyalama öğrenin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure App Service uygulaması kullanarak Azure portalında kopyalama
Kopyalama özelliği [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kolayca kopyalama varolan sağlar web uygulamaları için farklı bir bölgede ya da aynı bölgede yeni oluşturulan bir uygulama. Bu uygulama sayısı farklı bölgeler arasında hızlı ve kolay bir şekilde dağıtmasını sağlar.

Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir. Yeni özellik aynı sınırlamalar Web Apps yedekleme özelliği kullanan, bkz: [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Mevcut bir uygulamayı kopyalama
Web uygulamasının çalışır durumda **Premium** web uygulaması için bir kopya oluşturmak için sırayla modu.

1. İçinde [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresini açın.
2. Tıklatın **Araçları**. Ardından **Araçları** dikey penceresinde tıklatın **kopya uygulama**.
   
    ![][1]
   
   > [!NOTE]
   > Web uygulaması zaten değilse **Premium** modu, uygulama kopyalama desteklenen modları belirten bir ileti alırsınız. Bu noktada, seçmek için seçeneğiniz **yükseltme**.
   > 
   > 
3. İçinde **kopya uygulama** dikey penceresinde yeni web uygulaması, kaynak grubu ve uygulama hizmeti planı adını belirtin. Ayrıca kullanıcı kaynak web uygulaması ayarları sayısı kopyalamak isteyip istemediğinizi seçin kuramaz veya değil.
   
    ![][2]
4. ' I tıklattıktan sonra **oluşturma** platform kaynak web uygulamasının bir kopyasını oluşturma üzerinde çalışmaya başlar.

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>Bir uygulama hizmeti ortamı var olan bir uygulamaya kopyalama
İçinde **kopya uygulama** dikey müşteri var olan uygulama hizmeti ortamı'nda bir uygulama havuzu seçmek için seçeneği vardır.

## <a name="current-restrictions"></a>Geçerli kısıtlamaları
Bu özellik şu anda önizlemede değil, zaman içinde yeni özellikler eklemek için çalışıyoruz, aşağıdaki listede olan uygulama Azure Portalı'nda kopyalama bilinen kısıtlamalar geçerli desteği:

* Azure Traffic Manager ayarları klonlanmış değil
* Otomatik ölçek ayarları klonlanmış değil
* Yedekleme zamanlaması ayarları klonlanmış değil
* VNET ayarlarını klonlanmış değil
* App Insights otomatik olarak hedef web uygulamasında belirlenmedi
* Kolay kimlik doğrulama ayarları klonlanmış değil
* Kudu uzantısı değil kopyalanamıyor
* İpucu kuralları klonlanmış değil
* Veritabanı içeriğini değil kopyalanamıyor

### <a name="references"></a>Başvurular
* [Web uygulaması PowerShell kullanarak kopyalama](app-service-web-app-cloning.md)
* [Azure App Service'in web uygulamasında yedekleyin](web-sites-backup.md)
* [App Service Ortamı Oluşturma](app-service-web-how-to-create-an-app-service-environment.md)
* [App Service Ortamında bir web uygulaması oluşturma](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [App Service Ortamı’na giriş](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
