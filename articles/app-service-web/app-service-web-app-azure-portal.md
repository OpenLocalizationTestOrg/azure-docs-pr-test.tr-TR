---
title: "Azure portalında gezinme için başvuru"
description: "Farklı kullanıcı deneyimleri için App Service Web Yönetim Portalı ve Azure portalı arasında bilgi edinin"
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
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a>Azure portalında gezinme için başvuru
Azure Web siteleri artık adlı [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). Tüm bu ad değişikliği yansıtacak şekilde ve Azure Portal yönergeler sağlamak için Belgelerimizi güncelleştiriyoruz. Bu işlem yapılana kadar Azure portalında Web Apps ile çalışmak için bu belgede bir kılavuz olarak kullanabilirsiniz.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a>Klasik Azure portalı geleceği
Klasik Azure portalı marka değişiklikleri fark edeceksiniz, ancak bu Azure Portal tarafından değiştirilen sürecinde portalıdır. Klasik Portalı'nı aşamalı olarak Sonlandırılmakta gibi yeni yazılım geliştirme için odak Azure Portalı'na kaydırma. Tüm yaklaşan yeni özellikler Web uygulamaları için Azure Portalı'nda gelecektir. Web uygulamaları sunmaya sahip en son ve en büyük avantajlarından yararlanmak için Azure Portalı'nı kullanarak başlatın.

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a>Düzen farklarını Klasik Azure portalı ve Azure portalı
Klasik portalda tüm Azure hizmetlerini sol tarafında listelenir. Klasik portalda Gezinti ağaç yapısı, burada hizmetinden başlatmak ve her bir öğeye gidin izler. Bu yapı bağımsız bileşenler yönetirken iyi çalışır. Ancak, Azure üzerinde oluşturulan uygulamaların birbirine bağlı hizmetler koleksiyonu olan ve bu ağaç yapısı Hizmetleri koleksiyonları ile çalışmak için ideal değil. 

Azure portal uygulamaları için uçtan birden çok hizmet bileşenlerini içeren derleme kolay hale getirir. Portal olarak düzenlenmiş *Yolculuklar*. A *gezisine* bir dizi *dikey*, farklı bileşenler için kapsayıcı olduğu. Örneğin, otomatik bir web uygulaması için ölçeklendirmeyi ayarlama bir *gezisine* aldığı, birkaç Kanatlar aşağıdaki örnekte gösterildiği gibi: **web sitesi** (dikey penceresi başlığı henüz yeni terimlerle kullanılacak güncelleştirildiğini değil) dikey penceresinde **ayarları** dikey penceresinde ve **ölçeğini** dikey. Örnekte, otomatik ölçeklendirme CPU kullanımı, bu yüzden de bağımlı ayarlanan bir **CPU yüzdesi** dikey. İçinde bileşenleri *dikey* denir *bölümleri*, kutucukları gibi arayın. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Gezinti örnek: bir web uygulaması oluşturma
Yeni web uygulamaları oluşturma 1-2-3 hala kadar kolaydır. Aşağıdaki resimde Klasik Portalı'nı ve portal-değil çok çalıştıran ve bir web uygulaması hale getirmek için gereken adımları sayısında değiştiğini göstermek için yana gösterir. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Portalda web uygulamaları, WordPress gibi popüler galeri uygulamalar dahil olmak üzere en yaygın türleri arasından seçim yapabilirsiniz. Kullanılabilir uygulamaların tam listesi için ziyaret [Azure Marketi].

URL, belirttiğiniz bir web uygulaması oluşturduğunuzda uygulama hizmeti planı ve klasik portalda yapmak gibi portal konumda. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Buna ek olarak, portal, diğer genel ayarları tanımlamanıza olanak sağlar. Örneğin, [kaynak grupları](../azure-resource-manager/resource-group-overview.md) ilgili Azure kaynaklarını görmeyi ve yönetmeyi kolaylaştırır. 

## <a name="navigation-example-settings-and-features"></a>Gezinti örnek: ayarları ve özellikleri
Tüm ayarları ve özellikleri artık mantıksal olarak gezinmek tek bir dikey pencerede gruplandırılır.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Örneğin, özel etki alanlarını tıklayarak oluşturabileceğiniz **özel etki alanları ve SSL** içinde **ayarları** dikey.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

Bir izleme uyarısı ayarlamak için tıklatın **istekleri ve hataları** ve ardından **eklemek uyarı**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Tanılama etkinleştirmek için **tanılama günlükleri** içinde **ayarları** dikey.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Uygulama ayarlarını yapılandırmak için tıklatın **uygulama ayarları** içinde **ayarları** dikey. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Marka adı dışında birkaç portalında yeniden adlandırılmış veya silinmiş bunları bulmayı kolaylaştırmak için farklı bir şekilde gruplandırılmış. Örneğin, uygulama ayarları için karşılık gelen sayfasının ekran görüntüsü aşağıda verilmiştir (**yapılandırma**) Klasik Portalı'nda.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Daha Fazla Kaynak
[Azure Portal]: https://portal.azure.com
[Azure Marketi]: /marketplace/

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

