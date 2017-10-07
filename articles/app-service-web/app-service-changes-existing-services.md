---
title: aaaAzure App Service ve mevcut Azure hizmetlerine etkileri
description: "Açıklayan yeni Azure App Service'nasıl hello ve mevcut Azure hizmetlerinde özelliklerini etkileyebilir."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a>Azure Uygulama Hizmeti ve var olan Azure hizmetleri
Bu makalede Azure Hizmetleri hello değişiklik toobring birlikte bir parçası olarak çeşitli Azure hizmetlerine hello değişiklikleri tooexisting özetlenmektedir [Azure App Service](https://azure.microsoft.com/services/app-service/), yeni bir tümleşik sunum.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a>Genel Bakış
[Azure uygulama hizmeti](https://azure.microsoft.com/services/app-service/) , geliştiricilerin toocreate web ve mobil uygulamaları herhangi bir platform ve herhangi bir aygıt için sağlayan bir yeni ve benzersiz bir bulut hizmetidir. Kodlama işlevleri tasarlanmış tümleşik bir çözüm toostreamline yinelenen uygulama hizmetidir, kurumsal ve SaaS sistemlerle tümleştirmek ve güvenlik, güvenilirlik ve ölçeklendirilebilirlik, ihtiyaçlarını iş süreçlerini otomatikleştirmek.

Uygulama hizmeti getirir birlikte var olan Azure aşağıdaki hello Hizmetleri - [Web siteleri](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), ve [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) hizmeti, tek bir birleştirilmiş sırada güçlü yeni özellikler ekleme.  Uygulama hizmeti toohost hello şu uygulama türlerini sağlar:

* Web Apps
* Mobile Apps
* API Apps
* Logic Apps

Merhaba aşağıdaki tabloda açıklanmaktadır nasıl mevcut Azure Hizmetleri eşleme tooApp hizmeti ve hello uygulama türleri içinde kullanılabilir.

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
<td align="left"><li>Azure Web siteleri için uygulama kesinlikle sınırlı toochanging hello adı Web siteleri tooWeb uygulamaları hizmetidir.
<p><li>Web sitelerinin tüm mevcut örnekleri App Service'te Web uygulamalarını sunulmuştur.</p>
<p><li>Varolan sitelerinizi hello aracılığıyla erişebilirsiniz <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, altındaki tüm var olan siteler bulacaksınız burada <em>Web Apps</em>.</p>
<p><li><em>Web barındırma planına</em> artık <em>App Service planı</em>. Bir <em>App Service planı</em> uygulama her türlü Web, mobil, mantığı veya API uygulamaları gibi uygulama hizmeti barındırabilir.</p>
<p><li>Azure App Service Web Apps genel kullanılabilirlik olması.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/web/">Web Apps hakkında daha fazla bilgi</a>.</p></td>
</tr>
<tr class="even">
<td align="left">Azure Mobile Hizmetleri</td>
<td align="left">Mobile Apps</td>
<td align="left"><p><li>Mobile Services toobe bağımsız bir hizmet olarak kullanılabilir devam etmek ve tam olarak desteklenen kalır.</p>
<p><li>Mobile Apps tüm hello işlevselliğini Mobile Services ve daha fazlasını tümleştirir App Service içinde bir uygulama türüdür.</p>
<p><li>Çok kolaydır<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">Mobile Services tooMobile uygulamaları geçiş</a>.</p>
<p><li>Uygulama hizmeti bir parçası olarak, Mobile Apps Mobile Services ötesinde şirket içi ve SaaS sistemleri ile tümleştirme gibi yeni özellikler hazırlama yuvaları, Web işleri, daha iyi ölçeklendirme seçenekleri ve daha fazla bilgi alın.</p>
<p><li><a href="http://azure.microsoft.com/services/app-service/mobile/">Mobile Apps hakkında daha fazla bilgi</a>.</p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left">API Apps</td>
<td align="left">
<p><li>API uygulamaları kolayca oluşturmanıza ve hello bulutta API'lerini geliştirmenize olanak sağlayan bir App Service içinde yeni bir uygulama türüdür.</p>
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
<li><p>BizTalk Services toobe bağımsız bir hizmet olarak kullanılabilir devam etmek ve tam olarak desteklenen kalır.</p>
<li><p>BizTalk Services tüm hello özelliklerini uygulama hizmetinde API uygulamaları etkinleştirme kullanıcıları tooperform Kurumsal uygulama tümleştirmesi ve B2B tümleştirme senaryolarına herhangi biriyle hello App Service'deki uygulama türleri olarak tümleşiktir.</p>
<li><p>Logic Apps ile artık bir görsel tasarım deneyimi toocreate iş akışlarını kullanarak iş süreçlerini otomatik hale getirebilirsiniz.</p></td>
</tr>
</tbody>
</table>

toolearn daha, lütfen şu adresi ziyaret [uygulama hizmeti belgeleri](https://azure.microsoft.com/documentation/services/app-service/).

