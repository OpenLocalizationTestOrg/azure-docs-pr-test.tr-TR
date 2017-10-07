---
title: "hello Azure portalında gezinme aaaReference"
description: "Merhaba farklı kullanıcı deneyimleri için App Service Web hello Yönetim Portalı ve hello Azure Portal arasında bilgi edinin"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Hello Azure portalında gezinme için başvuru
Azure Web siteleri artık adlı [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Bu ad değişikliği ve tooprovide yönergeleri hello Azure Portal için tüm bizim belgelerine tooreflect güncelleştiriyoruz. Bu işlem yapılana kadar hello Azure portal Web Apps ile çalışmak için bu belgede bir kılavuz olarak kullanabilirsiniz.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>Merhaba geleceği hello Klasik Azure portalı
Marka değişiklikleri hello Klasik Azure portalı üzerinde hello fark edeceksiniz, ancak bu portalı hello Azure Portal tarafından değiştirilen hello işlemi kullanılıyor. Merhaba Klasik portal aşamalı olarak Sonlandırılmakta gibi yeni yazılım geliştirme için hello odak toohello Azure Portal kaydırma. Web uygulamaları için tüm yaklaşan yeni özellikler hello Azure Portal gelecektir. Hello Azure Portal tootake hello en son ve en büyük Web Apps toooffer sahip avantajlarından kullanmaya başlayın.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Düzen farklarını hello Klasik Azure portalı ve Azure portalı
Merhaba Klasik Portalı'nda, tüm Azure hello Hizmetleri hello sol tarafında listelenir. Merhaba Klasik portalında Gezinti ağaç yapısı, burada hello hizmetinden başlatmak ve her bir öğeye gidin izler. Bu yapı bağımsız bileşenler yönetirken iyi çalışır. Ancak, Azure üzerinde oluşturulan uygulamaların birbirine bağlı hizmetler koleksiyonu olan ve bu ağaç yapısı Hizmetleri koleksiyonları ile çalışmak için ideal değil. 

Hello Azure portalında kolay toobuild uygulamalar için uçtan birden çok Hizmetleri'nden bileşenlerle kolaylaştırır. Merhaba portal olarak düzenlenir *Yolculuklar*. A *gezisine* bir dizi *dikey*, hangi farklı bileşenler için hello kapsayıcılardır. Örneğin, otomatik bir web uygulaması için ölçeklendirmeyi ayarlama bir *gezisine* aldığı, birkaç Kanatlar hello aşağıdaki örnekte gösterildiği gibi: Merhaba **web sitesi** dikey (dikey penceresi başlığı henüz güncelleştirilmiş toouse olduğunu değil Hello yeni terimlerle) hello **ayarları** dikey penceresinde ve hello **ölçeğini** dikey. Bu yüzden de hello örnekte otomatik ölçeklendirme toodepend CPU kullanımını yukarı ayarlı bir **CPU yüzdesi** dikey. Merhaba bileşenleri hello içinde *dikey* denir *bölümleri*, kutucukları gibi arayın. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Gezinti örnek: bir web uygulaması oluşturma
Yeni web uygulamaları oluşturma 1-2-3 hala kadar kolaydır. bir web uygulaması ve çalışan değil çok hello adımları sayısında değişen görüntü gösterir hello Klasik portal ve hello portal yan yana toodemonstrate aşağıdaki hello tooget gerekli. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Merhaba Portalı'nda hello en yaygın tür web uygulamaları, WordPress gibi popüler galeri uygulamalar dahil olmak üzere arasından seçim yapabilirsiniz. Kullanılabilir uygulamaların tam listesi için hello ziyaret [Azure Marketi].

URL, belirttiğiniz bir web uygulaması oluşturduğunuzda uygulama hizmeti planı ve konum hello Klasik Portalı'nda yaptığınız gibi hello portalında. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Ayrıca, hello portal, diğer genel ayarları tanımlamanıza olanak sağlar. Örneğin, [kaynak grupları](../azure-resource-manager/resource-group-overview.md) basit toosee yapın ve ilgili Azure kaynaklarını yönetme. 

## <a name="navigation-example-settings-and-features"></a>Gezinti örnek: ayarları ve özellikleri
Tüm hello ayarları ve özellikleri artık mantıksal olarak gezinmek tek bir dikey pencerede gruplandırılır.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Örneğin, özel etki alanlarını tıklayarak oluşturabileceğiniz **özel etki alanları ve SSL** hello içinde **ayarları** dikey.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

bir izleme uyarısı yukarı tooset tıklatın **istekleri ve hataları** ve ardından **eklemek uyarı**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

tooenable tanılama **tanılama günlükleri** hello içinde **ayarları** dikey.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

tooconfigure uygulama ayarlar'ı **uygulama ayarları** hello içinde **ayarları** dikey. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Merhaba marka adı dışında birkaç hello portalında yeniden adlandırılmış veya silinmiş farklı şekilde gruplandırılmış toomake bunu daha kolay toofind bunları. Örneğin, uygulama ayarları için hello karşılık gelen sayfasının ekran görüntüsü aşağıda verilmiştir (**yapılandırma**) hello Klasik Portalı'nda.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Daha Fazla Kaynak
[Azure Portal]: https://portal.azure.com
[Azure Marketi]: /marketplace/

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

