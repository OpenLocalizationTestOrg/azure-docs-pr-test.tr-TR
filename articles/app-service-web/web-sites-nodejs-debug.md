---
title: "aaaHow toodebug Azure App Service'te bir Node.js web uygulaması"
description: "Nasıl toodebug bir Node.js web uygulamasını Azure App Service'te öğrenin."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a>Nasıl toodebug bir Node.js web uygulamasını Azure App Service'te
Azure içinde barındırılan Node.js uygulamalarında hata ayıklama ile yerleşik tanılama tooassist sağlar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları. Bu makalede, öğreneceksiniz nasıl tooenable günlük stdout ve stderr, görünen hata bilgilerini hello tarayıcıda ve nasıl toodownload ve görünüm günlük dosyaları.

Azure üzerinde barındırılan Node.js uygulamaları için tanılama tarafından sağlanan [IISNode]. Tanılama bilgilerini toplamak için hello en yaygın ayarları bu makalede ele olsa da, onu tam bir başvuru IISNode ile çalışmak için sağlamaz. Merhaba IISNode ile çalışma hakkında daha fazla bilgi için bkz: [IISNode Benioku] github'da.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Günlü kaydını etkinleştir
Varsayılan olarak, bir App Service web uygulaması yalnızca Git kullanarak bir web uygulaması dağıttığınızda gibi dağıtımları hakkında tanılama bilgilerini yakalar. Başvurulan modül yüklenirken bir hata gibi dağıtım sırasında sorun yaşıyorsanız bu bilgiler yararlıdır **package.json**, veya bir özel dağıtım komut dosyası kullanıyorsanız.

tooenable hello stdout ve stderr akışları günlüğü, oluşturmanız gerekir bir **IISNode.yml** dosya hello Node.js uygulamanızı kökünde ve hello aşağıdakileri ekleyin:

    loggingEnabled: true

Bu, Node.js uygulamanızdan stdout ve stderr hello günlük kaydını etkinleştirir.

Merhaba **IISNode.yml** bir hata oluştuğunda kolay hataları veya Geliştirici hataları toohello tarayıcı döndürülen olup olmadığını dosya kullanılan toocontrol de olabilir. tooenable Geliştirici hataları ekleme satırı toohello aşağıdaki hello **IISNode.yml** dosyası:

    devErrorsEnabled: true

Bu seçenek etkinleştirildiğinde, IISNode hello son 64 K "bir iç sunucu hatası oluştu"gibi kolay hatası yerine toostderr gönderilen bilgi döndürür.

> [!NOTE]
> DevErrorsEnabled geliştirme sırasında sorunları tanılamada yararlı olsa da, bir üretim ortamında etkinleştirme tooend kullanıcılara gönderilen geliştirme hatalarına neden olabilir.
> 
> 

Merhaba, **IISNode.yml** dosya, uygulama içinde zaten yoktu, güncelleştirilmiş hello uygulama yayımlandıktan sonra web uygulamanızı yeniden başlatmanız gerekir. Var olan ayarları değiştiriyorsanız **IISNode.yml** daha önce yayımlanan dosyası, yeniden başlatma gereklidir.

> [!NOTE]
> Web uygulamanızı hello Azure komut satırı araçlarını veya Azure PowerShell cmdlet'leri, varsayılan kullanarak oluşturduysanız **IISNode.yml** dosyası otomatik olarak oluşturulur.
> 
> 

toorestart hello web uygulaması, select hello web uygulamasında hello [Azure Portal](https://portal.azure.com)ve ardından **yeniden** düğmesi:

![düğme yeniden başlatın][restart-button]

Hello Azure komut satırı araçları geliştirme ortamınızda yüklü değilse, komutu toorestart hello web uygulama aşağıdaki hello kullanabilirsiniz:

    azure site restart [sitename]

> [!NOTE]
> LoggingEnabled ve devErrorsEnabled tanılama bilgileri yakalamak için en yaygın olarak kullanılan hello IISNode.yml yapılandırma seçenekleri olsa da, IISNode.yml kullanılan tooconfigure çeşitli seçenekleri barındırma ortamınıza olabilir. Merhaba hello yapılandırma seçeneklerinin tam bir listesi için bkz: [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) dosya.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Günlükleri erişme
Tanılama günlüklerini üç yolla erişilebilir; Hello Dosya Aktarım Protokolü (Zip arşivini indirme FTP), kullanarak veya bir dinamik güncelleştirilen akış hello günlüğünün (kuyruk olarak da bilinir). Merhaba Zip arşivini hello günlük dosyalarının indirilirken veya hello canlı akış görüntüleme hello Azure komut satırı araçları gerektirir. Bu komutu aşağıdaki hello kullanılarak yüklenebilir:

    npm install azure-cli -g

Bir kez yüklendikten sonra hello araçları hello 'azure' komutunu kullanarak erişilebilir. komut satırı araçları hello ilk yapılandırılmış toouse, Azure aboneliğinizin olması gerekir. Merhaba nasıl tooaccomplish bu görev hakkında daha fazla bilgi için bkz **nasıl toodownload ve içeri aktarma yayımlama ayarları** hello bölümünü [nasıl tooUse hello Azure komut satırı araçları](../xplat-cli-connect.md) makalesi.

### <a name="ftp"></a>FTP
FTP üzerinden tooaccess hello tanılama bilgilerini ziyaret hello [Azure Portal](https://portal.azure.com), web uygulamanızı seçin ve ardından hello seçin **PANO**. Merhaba, **hızlı bağlantılar** hello bölümünde **FTP tanılama GÜNLÜKLERİ** ve **FTPS tanılama GÜNLÜKLERİ** hello FTP protokolünü kullanarak erişim toohello günlükleri bağlantılar sağlar.

> [!NOTE]
> Daha önce kullanıcı adı ve parola FTP veya dağıtım için yapılandırmadıysanız, hello bunu yapabilirsiniz **Hızlı Başlangıç** seçerek Yönetim sayfasında **dağıtım kimlik bilgilerini ayarlayın**.
> 
> 

Merhaba FTP hello panosunda döndürülen Merhaba URL'dir **LogFiles** alt dizinleri izleyen hello içerecek dizini:

* [Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, bir dizin aynı adı oluşturulur ve bilgileri içerir hello toodeployments ilgili.
* nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri

### <a name="zip-archive"></a>Zip arşivini
Zip arşivini hello Azure komut satırı araçları'ndan komutu aşağıdaki kullanım hello hello tanılama günlüklerinin toodownload:

    azure site log download [sitename]

Bu yükleyecek bir **diagnostics.zip** hello geçerli dizinde. Bu Arşiv hello aşağıdaki dizin yapısını içerir:

* dağıtımları - uygulamanızın dağıtımları hakkında bilgi günlüğü
* LogFiles
  
  * [Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, bir dizin aynı adı oluşturulur ve bilgileri içerir hello toodeployments ilgili.
  * nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri

### <a name="live-stream-tail"></a>Canlı akış (kuyruk)
tooview tanılama günlük bilgilerinin kullanımı hello hello Azure komut satırı araçları'ndan komutu aşağıdaki canlı akış:

    azure site log tail [sitename]

Bu hello sunucuda oluşurken, güncelleştirilmiş günlük olaylarının bir akış döndürür. (LoggingEnabled true olduğunda.) Bu akış stdout ve stderr bilgi yanı sıra dağıtım bilgilerini döndürür

<a id="nextsteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
Bu, nasıl öğrenilen makale Azure tooenable ve erişim tanılama bilgileri. Bu bilgiler yararlı olsa da, kullanmakta olduğunuz bir modül veya App Service Web Apps tarafından kullanılan Node.js hello sürümünün tooa sorun gösterebilir uygulamanızla birlikte oluşan anlama sorunları hello Dağıtımınızda kullanılan farklı ortam.

Modüllerle çalışma Azure ile ilgili bilgi için [Azure uygulamalarıyla Node.js modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md).

Uygulamanız için Node.js sürümünü belirtme hakkında daha fazla bilgi için bkz: [bir Azure uygulamasında Node.js sürümünü belirtme].

Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Benioku]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[bir Azure uygulamasında Node.js sürümünü belirtme]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

