---
title: "Azure App Service’teki bir Node.js web uygulamasına hata ayıklama"
description: "Azure App Service'te Node.js web uygulamasına hata ayıklama öğrenin."
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
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a>Azure App Service’teki bir Node.js web uygulamasına hata ayıklama
Azure içinde barındırılan Node.js uygulamalarını hata ayıklamaya yardımcı olması için yerleşik tanılama sağlar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web uygulamaları. Bu makalede, stdout ve stderr günlük kaydını etkinleştirmek için tarayıcıda hata bilgilerini görüntülemek nasıl ve indirmek ve günlük dosyalarını görüntülemek nasıl öğreneceksiniz.

Azure üzerinde barındırılan Node.js uygulamaları için tanılama tarafından sağlanan [IISNode]. Tanılama bilgilerini toplamak için en yaygın ayarları bu makalede ele olsa da, onu tam bir başvuru IISNode ile çalışmak için sağlamaz. IISNode ile çalışma hakkında daha fazla bilgi için bkz: [IISNode Benioku] github'da.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Günlü kaydını etkinleştir
Varsayılan olarak, bir App Service web uygulaması yalnızca Git kullanarak bir web uygulaması dağıttığınızda gibi dağıtımları hakkında tanılama bilgilerini yakalar. Başvurulan modül yüklenirken bir hata gibi dağıtım sırasında sorun yaşıyorsanız bu bilgiler yararlıdır **package.json**, veya bir özel dağıtım komut dosyası kullanıyorsanız.

Stdout ve stderr akışları günlüğe yazılmasını etkinleştirmek için oluşturmalısınız bir **IISNode.yml** dosya, Node.js uygulamanızın kök dizininde ve aşağıdakileri ekleyin:

    loggingEnabled: true

Bu, Node.js uygulamanızdan stdout ve stderr günlük kaydını etkinleştirir.

**IISNode.yml** dosya de kullanılabilir denetlemek için bir hata oluştuğunda kolay hataları veya Geliştirici hataları tarayıcıya döndürülür olup olmadığını. Geliştirici hataları etkinleştirmek için aşağıdaki satırı ekleyin **IISNode.yml** dosyası:

    devErrorsEnabled: true

Bu seçenek etkinleştirildiğinde, IISNode son 64 K stderr kolay hatası yerine "İç sunucu hatası oluştu"gibi gönderilen bilgi döndürür.

> [!NOTE]
> DevErrorsEnabled geliştirme sırasında sorunları tanılamada yararlı olsa da, bir üretim ortamında etkinleştirme son kullanıcılara gönderilen geliştirme hataları neden olabilir.
> 
> 

Varsa **IISNode.yml** dosya, uygulama içinde zaten yoktu, güncelleştirilmiş uygulama yayımlandıktan sonra web uygulamanızı yeniden başlatmanız gerekir. Var olan ayarları değiştiriyorsanız **IISNode.yml** daha önce yayımlanan dosyası, yeniden başlatma gereklidir.

> [!NOTE]
> Web uygulamanızı Azure komut satırı araçlarını veya Azure PowerShell cmdlet'leri, varsayılan kullanarak oluşturduysanız **IISNode.yml** dosyası otomatik olarak oluşturulur.
> 
> 

Web uygulaması yeniden için web uygulaması seçin [Azure Portal](https://portal.azure.com)ve ardından **yeniden** düğmesi:

![düğme yeniden başlatın][restart-button]

Azure komut satırı araçları geliştirme ortamınızda yüklü değilse, web uygulaması yeniden başlatmak için aşağıdaki komutu kullanabilirsiniz:

    azure site restart [sitename]

> [!NOTE]
> En sık IISNode.yml yapılandırma seçenekleri tanılama bilgileri yakalamak için kullanılan loggingEnabled ve devErrorsEnabled olmakla birlikte, IISNode.yml çeşitli barındırma ortamınız için seçenekleri yapılandırmak için kullanılabilir. Yapılandırma seçeneklerinin tam bir listesi için bkz: [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) dosya.
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a>Günlükleri erişme
Tanılama günlüklerini üç yolla erişilebilir; Dosya Aktarım Protokolü (Zip arşivini indirme FTP), kullanarak veya bir dinamik güncelleştirilen akış günlük (kuyruk olarak da bilinir). Günlük dosyalarının Zip arşivini indirilirken veya bir canlı akışı görüntüleme Azure komut satırı araçları gerektirir. Bunlar, aşağıdaki komutu kullanarak yüklenebilir:

    npm install azure-cli -g

Yüklendikten sonra Araçlar 'azure' komutunu kullanarak erişilebilir. Komut satırı araçlarını, ilk Azure aboneliğinizi kullanmak üzere yapılandırılmalıdır. Bu görevi gerçekleştirmek hakkında daha fazla bilgi için bkz: **nasıl yükleneceği ve yayımlama ayarlarını içeri aktar** bölümünü [Azure komut satırı araçlarını kullanın nasıl](../xplat-cli-connect.md) makale.

### <a name="ftp"></a>FTP
FTP aracılığıyla tanılama bilgilerine erişmek için ziyaret [Azure Portal](https://portal.azure.com)web uygulamanızı seçin ve ardından **PANO**. İçinde **hızlı bağlantılar** bölümünde **FTP tanılama GÜNLÜKLERİ** ve **FTPS tanılama GÜNLÜKLERİ** bağlantılar FTP protokolünü kullanarak günlükleri erişim sağlar.

> [!NOTE]
> Daha önce kullanıcı adı ve parola FTP veya dağıtım için yapılandırmadıysanız, nden yapabilirsiniz **Hızlı Başlangıç** seçerek Yönetim sayfasında **dağıtım kimlik bilgilerini ayarlayın**.
> 
> 

FTP panosunda döndürülen URL içindir **LogFiles** aşağıdaki alt dizinler içerecek dizini:

* [Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, aynı ada sahip bir dizin oluşturulur ve dağıtımları için ilgili bilgiler içerir.
* nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri

### <a name="zip-archive"></a>Zip arşivini
Tanılama günlüklerinin Zip arşivini indirmek için Azure komut satırı araçları aşağıdaki komutu kullanın:

    azure site log download [sitename]

Bu yükleyecek bir **diagnostics.zip** geçerli dizin. Bu Arşiv aşağıdaki dizin yapısını içerir:

* dağıtımları - uygulamanızın dağıtımları hakkında bilgi günlüğü
* LogFiles
  
  * [Dağıtım yöntemi](web-sites-deploy.md) -Git gibi dağıtım yöntemi kullanırsanız, aynı ada sahip bir dizin oluşturulur ve dağıtımları için ilgili bilgiler içerir.
  * nodejs - (loggingEnabled true olduğunda.), uygulamanızın tüm örneklerden yakalanan Stdout ve stderr bilgileri

### <a name="live-stream-tail"></a>Canlı akış (kuyruk)
Canlı akış tanılama günlük bilgileri görüntülemek için Azure komut satırı araçları aşağıdaki komutu kullanın:

    azure site log tail [sitename]

Bu sunucu üzerinde meydana gelirken, güncelleştirilmiş günlük olaylarının bir akış döndürür. (LoggingEnabled true olduğunda.) Bu akış stdout ve stderr bilgi yanı sıra dağıtım bilgilerini döndürür

<a id="nextsteps"></a>

## <a name="next-steps"></a>Sonraki Adımlar
Bu makalede etkinleştirmek ve Azure tanılama bilgilerine öğrendiniz. Bu bilgiler ile uygulamanızı oluşan anlama sorunları kullanışlı olsa da, kullanmakta olduğunuz veya App Service Web Apps tarafından kullanılan Node.js sürümünü dağıtım ortamınızda kullanılan olandan farklı bir modülü bir soruna işaret edebilir.

Modüllerle çalışma Azure ile ilgili bilgi için [Azure uygulamalarıyla Node.js modüllerini kullanma](../nodejs-use-node-modules-azure-apps.md).

Uygulamanız için Node.js sürümünü belirtme hakkında daha fazla bilgi için bkz: [bir Azure uygulamasında Node.js sürümünü belirtme].

Daha fazla bilgi için Ayrıca bkz. [Node.js Geliştirici Merkezi](/develop/nodejs/).

## <a name="whats-changed"></a>Yapılan değişiklikler
* Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Benioku]: https://github.com/tjanczuk/iisnode#readme
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[bir Azure uygulamasında Node.js sürümünü belirtme]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

