---
title: "aaaManage Azure App Service'te bir web uygulaması"
description: "Azure App Service'in web uygulamasında yönetmek için bağlantılar tooresources."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Azure App Service'in web uygulamasında yönetme
Bu konu, bir web uygulamasını yönetmek için bağlantılar tooresources içerir [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Yönetim web uygulamanız sorunsuz çalışmasını devam hello görevlerin tümünü içerir. 

Bir web uygulaması hello ömrü boyunca, ilk dağıtım toonormal işlemi, Bakım ve güncelleştirmelerini taşımak gibi farklı yönetim görevleri gerçekleştirmeniz gerekecektir.

Birçok web uygulama yönetimi görevlerini hello Azure Portal gerçekleştirilebilir.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Web uygulaması tooproduction dağıtmadan önce
### <a name="choose-a-tier"></a>Bir katmanı seçin
Azure uygulama hizmeti beş katmanlarda sunulur: ücretsiz, paylaşılan, temel, standart ve Premium. Merhaba özellikler ve her katman için fiyatlandırma hakkında daha fazla bilgi için bkz: [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/app-service/). 

* [Uygulama hizmeti planları](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) hello altında birden çok web uygulamaları Grup izin aynı katmanı.
* Her zaman [geçiş katmanları](web-sites-scale.md) web uygulamanızı oluşturduktan sonra.

### <a name="configuration"></a>Yapılandırma
Kullanım hello [Azure Portal](https://portal.azure.com/) tooset çeşitli yapılandırma seçenekleri. Ayrıntılar için bkz [Azure App Service'te web uygulamalarını yapılandırma](web-sites-configure.md). Hızlı bir denetim listesi aşağıdadır:

* Seçin **çalışma zamanı sürümlerini** .NET, PHP, Java ya da gerekirse Python için.
* Etkinleştirme **WebSockets** web uygulamanız hello WebSocket Protokolü kullanıyorsa. (Bunu kullanan uygulamalar içeren [ASP.NET SignalR](http://www.asp.net/signalr) veya [Socket.IO](web-sites-nodejs-chat-app-socketio.md).)
* Sürekli web işleriniz kullanıyorsunuz? Bu durumda, etkinleştirme **her zaman açık**.
* Set hello **varsayılan belge**, index.html gibi.

Toplama toothese temel yapılandırma ayarlarında tooconfigure hello aşağıdaki isteyebilirsiniz:

* **Güvenli Yuva Katmanı (SSL)** şifreleme. SSL toouse bir özel etki alanı adı ile almanız gerekir bir SSL sertifikası ve web uygulama toouse yapılandırmak. Bkz: [Azure App Service'te bir web uygulaması için HTTPS'yi etkinleştir](app-service-web-tutorial-custom-ssl.md).
* **Özel etki alanı adı.** Web uygulamanız otomatik olarak azurewebsites.net altında bir alt etki alanı vardır. Bir özel etki alanı adı contoso.com gibi ilişkilendirebilirsiniz. Bkz: [Azure App Service'te özel etki alanı adı yapılandırma](app-service-web-tutorial-custom-domain.md).

Dile özgü yapılandırma:

* **PHP**: [Azure App Service Web Apps PHP yapılandırma](web-sites-php-configure.md).
* **Python**: [yapılandırma Python Azure uygulama hizmeti ile Web uygulamaları](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Web uygulamanızı çalışırken
Web uygulamanızı çalışırken toomake kullanılabilir olduğundan ve toomeet kullanıcı trafiğinin ölçeklendirir istiyor. Tootroubleshoot hataları da gerekebilir.

### <a name="monitoring"></a>İzleme
* Hello Azure Portal yapabilecekleriniz [performans ölçümleri eklemek](web-sites-monitor.md) CPU kullanımı ve istemci istekleri sayısı gibi.
* [Web uygulamanız ölçeği](web-sites-scale.md) yanıt tootraffic içinde. Katmanına bağlı olarak VM hello sayısını ve/veya hello VM örnekleri hello boyutunu ölçeklendirebilirsiniz. Web uygulamanız otomatik olarak sabit bir zamanlama ya yanıt tooload ölçeklendirir şekilde hello standart ve Premium katmanlar, otomatik ölçeklendirmeyi ayarlayalım ayarlayabilirsiniz.  

### <a name="backups"></a>Yedeklemeler
* Ayarlama [otomatik yedeklemeler](web-sites-backup.md) , web uygulamanızın. Yedeklemelerin hakkında daha fazla bilgi [bu videoyu](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* Başlangıç seçenekleri hakkında bilgi edinin [veritabanı kurtarma](../sql-database/sql-database-business-continuity.md) Azure SQL veritabanında.

### <a name="troubleshooting"></a>Sorun giderme
* Bir sorun yaşanırsa yapabilecekleriniz [Visual Studio'daki sorun giderme](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), tanılama günlüklerini kullanma ve hello bulutta hata ayıklama Canlı. 
* Visual Studio dışında çeşitli yolları toocollect tanılama günlükleri vardır. Bkz: [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](web-sites-enable-diagnostic-log.md).
* Node.js uygulamaları için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Verileri geri yükleme
* [Geri yükleme](web-sites-restore.md) daha önce yedeklenen bir web uygulaması.

## <a name="when-you-update-your-web-app"></a>Web uygulamanızı güncelleştirdiğinizde
Otomatik yedekleme etkinleştirmediyseniz oluşturabileceğiniz bir [el ile Yedekleme](web-sites-backup.md).

Kullanmayı [dağıtım hazırlanan](web-sites-staged-publishing.md). Bu seçenek, güncelleştirmeleri tooa yan yana çalışır dağıtım hazırlama yayımlama sağlar, Üretim dağıtımı ile. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


