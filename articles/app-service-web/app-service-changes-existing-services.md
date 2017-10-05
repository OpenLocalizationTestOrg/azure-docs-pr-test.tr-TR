---
title: Azure App Service ve mevcut Azure hizmetlerine etkileri
description: "Var olan Azure hizmetlerinde yeni Azure App Service ve özelliklerini nasıl etkisi açıklanmaktadır."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure Uygulama Hizmeti ve var olan Azure hizmetleri
Bu makalede, çeşitli Azure hizmetlerine bir araya getirme değiştirilecek bir parçası olarak mevcut Azure hizmetlerine değişiklikler özetlenmektedir [Azure App Service](https://azure.microsoft.com/services/app-service/), yeni bir tümleşik sunum.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Genel Bakış
[Azure uygulama hizmeti](https://azure.microsoft.com/services/app-service/) geliştiricilerin web ve herhangi bir platform ve herhangi bir aygıt için mobil uygulamaları oluşturmalarına olanak veren bir yeni ve benzersiz bir bulut hizmetidir. Uygulama, yinelenen kodlama işlevleri kolaylaştırmak, kurumsal ve SaaS sistemlerle tümleştirmek ve güvenlik, güvenilirlik ve ölçeklendirilebilirlik, ihtiyaçlarını iş süreçlerini otomatikleştirmek için tasarlanmış tümleşik bir çözüm hizmetidir.

Uygulama hizmeti getirir birlikte aşağıdaki mevcut Azure Hizmetleri - [Web siteleri](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), ve [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) eklenirken hizmeti, tek bir birleştirilmiş güçlü yeni özellikleri.  Uygulama hizmeti aşağıdaki uygulama türlerini barındırmanıza olanak sağlar:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

Aşağıdaki tabloda, uygulama hizmeti nasıl mevcut Azure hizmetlerine eşlemesine ve içinde kullanılabilir uygulama türleri açıklanmaktadır.

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%">Var olan Azure hizmeti</th>
<th align="left", style="width:10%">Azure App Service</th>
<th align="left", style="width:80%">Neler değişti</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Azure Web Siteleri</td>
<td align="left">Web Apps</td>
<td align="left"><li>Azure Web siteleri için App Service Web Apps için Web siteleri adını değiştirmek için kesinlikle sınırlıdır.
<p><li>Web sitelerinin tüm mevcut örnekleri App Service'te Web uygulamalarını sunulmuştur.</p>
<p><li>Varolan sitelerinizi aracılığıyla erişebilirsiniz <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, altındaki tüm var olan siteler bulacaksınız burada <em>Web Apps</em>.</p>
<p><li><em>Web barındırma planına</em> artık <em>App Service planı</em>. Bir <em>App Service planı</em> uygulama her türlü Web, mobil, mantığı veya API uygulamaları gibi uygulama hizmeti barındırabilir.</p>
<p><li>Azure App Service Web Apps genel kullanılabilirlik olması.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Web Apps hakkında daha fazla bilgi</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Hizmetleri</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services bağımsız bir hizmet olarak kullanılabilir ve tam olarak desteklenen kalması için devam edin.</p>
<p><li>Mobile Apps, Mobile Services ve daha fazlasını işlevselliğini tümünün tümleştirir App Service içinde bir uygulama türüdür.</p>
<p><li>Kolay <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">mobil uygulamaları için Mobile Services geçirme</a>.</p>
<p><li>Uygulama hizmeti bir parçası olarak, Mobile Apps Mobile Services ötesinde şirket içi ve SaaS sistemleri ile tümleştirme gibi yeni özellikler hazırlama yuvaları, Web işleri, daha iyi ölçeklendirme seçenekleri ve daha fazla bilgi alın.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Mobile Apps hakkında daha fazla bilgi</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>API uygulamaları kolayca oluşturmanıza ve bulut API'leri kullanmasına olanak sağlayan bir App Service içinde yeni bir uygulama türüdür.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/api/">API Apps hakkında daha fazla bilgi</a>.</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left">Logic Apps</td>
<td align="left">
<p><li>Logic Apps, App Service'te kolayca iş süreçlerini otomatikleştirmek olanak sağlayan yeni bir uygulama türüdür.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/logic/">Logic Apps hakkında daha fazla bilgi</a>.</p></td>
</tr>
<tr class="odd">
<td align="left">Azure BizTalk Hizmetleri</td>
<td align="left">BizTalk API uygulamaları</td>
<td align="left">
<li><p>BizTalk Services bağımsız bir hizmet olarak kullanılabilir ve tam olarak desteklenen kalması için devam edin.</p>
<li><p>BizTalk Services tüm özelliklerini uygulama hizmetinde API uygulamaları etkinleştirme kullanıcıların Kurumsal uygulama tümleştirmesi ve uygulama türlerinin herhangi biriyle B2B tümleştirme senaryolarına App Service'te gerçekleştirmesini olarak tümleşiktir.</p>
<li><p>Logic Apps ile iş süreçlerini iş akışları oluşturmak için bir görsel tasarım deneyimi kullanarak otomatikleştirebilirsiniz.</p></td>
</tr>
</tbody>
</table>

Daha fazla bilgi için lütfen ziyaret [uygulama hizmeti belgeleri](https://azure.microsoft.com/documentation/services/app-service/).

