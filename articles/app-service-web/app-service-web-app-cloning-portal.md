---
title: aaaWeb Azure Portal kullanarak uygulama kopyalama
description: "Bilgi nasıl tooclone, Web uygulamaları toonew Azure Portal kullanarak Web uygulamaları."
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
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure App Service uygulaması kullanarak Azure portalında kopyalama
özelliği kopyalama hello [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) hello aynı bölgede varolan web uygulamaları yeni oluşturulan tooa uygulamasını farklı bir bölgede ya da de kolayca kopyalama sağlar. Bu müşteriler toodeploy uygulamaları birkaç farklı bölgelerdeki hızla ve kolayca olanak tanır.

Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir. Merhaba yeni özellik kullandığı aynı hello Web Apps yedekleme özelliği olarak sınırlamalar bakın [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Mevcut bir uygulamayı kopyalama
hello Hello web uygulaması çalıştıran **Premium** hello web uygulaması için bir kopya toocreate sırada modu.

1. Merhaba, [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresini açın.
2. Tıklatın **Araçları**. Ardından hello **Araçları** dikey penceresinde tıklatın **kopya uygulama**.
   
    ![][1]
   
   > [!NOTE]
   > Merhaba web uygulaması zaten hello değilse **Premium** modu, uygulama kopyalama hello desteklenen modları belirten bir ileti alırsınız. Bu noktada, hello seçeneği tooselect sahip **yükseltme**.
   > 
   > 
3. Merhaba, **kopya uygulama** dikey penceresinde hello yeni web uygulaması, kaynak grubu ve uygulama hizmeti planı adını belirtin. Aynı zamanda hello kullanıcı mümkün toochoose olup olacaktır tooclone kaynak web uygulaması ayarları sayısı veya değil.
   
    ![][2]
4. ' I tıklattıktan sonra **oluşturma** hello platform hello kaynak web uygulamasının bir kopyasını oluşturma üzerinde çalışmaya başlayacak.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Var olan bir uygulama tooan uygulama hizmeti ortamı kopyalama
Merhaba, **kopya uygulama** dikey penceresinde hello müşteri, bir uygulama havuzu var olan uygulama hizmeti ortamı'nda hello seçeneği toochoose olacaktır.

## <a name="current-restrictions"></a>Geçerli kısıtlamaları
Bu özellik şu anda önizlemede değil, zaman içinde tooadd yeni özellikler çalışıyoruz, liste aşağıdaki hello Azure portalında uygulama kopyalama bilinen sınırlamalar hello geçerli desteği hello:

* Azure Traffic Manager ayarları klonlanmış değil
* Otomatik ölçek ayarları klonlanmış değil
* Yedekleme zamanlaması ayarları klonlanmış değil
* VNET ayarlarını klonlanmış değil
* App Insights otomatik olarak hello hedef web uygulamasında belirlenmedi
* Kolay kimlik doğrulama ayarları klonlanmış değil
* Kudu uzantısı değil kopyalanamıyor
* İpucu kuralları klonlanmış değil
* Veritabanı içeriğini değil kopyalanamıyor

### <a name="references"></a>Başvurular
* [Web uygulaması PowerShell kullanarak kopyalama](app-service-web-app-cloning.md)
* [Azure App Service'in web uygulamasında yedekleyin](web-sites-backup.md)
* [Nasıl tooCreate bir uygulama hizmeti ortamı](app-service-web-how-to-create-an-app-service-environment.md)
* [App Service Ortamında bir web uygulaması oluşturma](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
