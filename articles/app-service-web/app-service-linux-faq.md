---
title: "aaaAzure App Service Web uygulamasında Linux SSS | Microsoft Docs"
description: "Azure App Service Web uygulaması Linux SSS."
keywords: "Azure uygulama hizmeti, web uygulaması, SSS, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: c7798d9144d936eecdc0e191fc870b0ee0b220c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-on-linux-faq"></a>Azure App Service Web uygulaması Linux SSS

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Özellik ekleme ve geliştirmeler tooour platform yapmadan Linux üzerinde Web uygulaması Hello sürümüyle çalışıyoruz. Bazı sık sorulan aşağıda verilmiştir müşterilerimizin bize hello son isteyen sorular (SSS) ay.
Varsa, yorum hello makale üzerinde sorularınız ve biz bunu mümkün olan en kısa sürede yanıt.

## <a name="built-in-images"></a>Yerleşik görüntüleri

**S:** platform hello toofork hello yerleşik Docker kapsayıcıları sağlar istiyorum. Bu dosyaları nereden bulabilirim?

**Y:** tüm Docker dosyaları bulabilirsiniz [GitHub](https://github.com/azure-app-service). Tüm Docker kapsayıcıları bulabilirsiniz [Docker hub'a](https://hub.docker.com/u/appsvc/).

**S:** hello çalışma zamanı yığını yapılandırdığınızda hello beklenen değerler hello başlatma dosyası bölümü için nelerdir?

**Y:** için Node.Js, belirttiğiniz hello PM2 yapılandırma dosyası veya komut dosyası. .NET Core için derlenmiş DLL adınızı belirtin. Ruby için hello Söyleniş betik belirtebilirsiniz, uygulamanızı tooinitialize istiyor.

## <a name="management"></a>Yönetim

**S:** hello yeniden düğmesine hello Azure portal bastığınızda ne olur?

**Y:** bu olduğu hello Docker yeniden karşılığıdır.

**S:** güvenli Kabuk (SSH) tooconnect toohello uygulama kapsayıcı sanal makine (VM) kullanabilir miyim?

**Y:** Evet, hello SCM sitesi aracılığıyla daha fazla bilgi için onay hello aşağıdaki makalesi yapabileceğiniz [Linux üzerinde Web uygulaması için SSH desteği](./app-service-linux-ssh-support.md)

**S:** toocreate Linux uygulama hizmeti düzlemi SDK veya bir ARM şablonu aracılığıyla istediğiniz, nasıl ı elde edebileceğiniz bu?

**Y:** tooset hello gereksinim `reserved` hello uygulama alanının hizmet çok`true`.

## <a name="continuous-integrationdeployment"></a>Sürekli Tümleştirme/dağıtım

**S:** Docker hub'a hello görüntüde güncelleştirilmiş sonra web Uygulamam hala eski Docker kapsayıcısı görüntüyü kullanır. Sürekli Tümleştirme/özel kapsayıcılar dağıtımını destekliyor musunuz?

**Y:** aşağıdaki makaleye bakın onay hello tarafından Azure kapsayıcı kayıt defteri veya DockerHub görüntü için sürekli tümleştirme/dağıtım tooset [Linux Azure Web uygulaması ile sürekli dağıtımın](./app-service-linux-ci-cd.md). Özel kayıt defterleri için durdurma ve ardından web uygulamanızı başlatma hello kapsayıcı yenileyebilirsiniz. Değiştirme veya tooforce, kapsayıcı yenileme ayarlama sahte bir uygulama ekleyin.

**S:** hazırlama ortamlarını desteklemek musunuz?

**Y:** Evet.

**S:** kullanabilirim **web dağıtımı** toodeploy web Uygulamam?

**Y:** tooset denilen bir uygulamaya Evet, ihtiyacınız `WEBSITE_WEBDEPLOY_USE_SCM` çok`false`.

## <a name="language-support"></a>Dil desteği

**S:** derlenmemiş .NET Core uygulamaları desteği musunuz?

**Y:** Evet.

**S:** PHP uygulamaları için bir bağımlılık Yöneticisi olarak Oluşturucu desteklemez?

**Y:** Evet. Git dağıtımı sırasında bir PHP uygulaması (teşekkürler toohello dosyasının varlığı, yönetimin bir composer.json) dağıtma ve sizin için bir oluşturucu yükleme tetikleyecek Kudu tanımalıdır.

## <a name="custom-containers"></a>Özel kapsayıcılar

**S:** kendi özel kapsayıcı kullanıyorum. Uygulamam hello bulunduğu `\home\` dizin, ancak bulamıyor dosyalarımı ı hello kullanarak hello içerik göz attığınızda [SCM site](https://github.com/projectkudu/kudu) veya bir FTP istemcisi. Dosyalarımı nerede?

**Y:** biz bir SMB paylaşım toohello bağlama `\home\` dizin. Bu, var olan herhangi bir içerik geçersiz kılar.

**S:** kendi özel kapsayıcı kullanıyorum. Merhaba platform toomount bir SMB paylaşım toohello istemiyorum `\home\`.

**Y:** bunu ayarı hello tarafından yapabilirsiniz `WEBSITES_ENABLE_APP_SERVICE_STORAGE` uygulama çok ayarı`false`.

**S:** uzun süre toostart My özel kapsayıcı alır ve hello platform yeniden hello kapsayıcı kendisinden önce tamamlanır başlatılıyor.

**Y:** hello platform, kapsayıcı yeniden başlatmadan önce bekleyeceği hello süre yapılandırabilirsiniz. Bu ayarı hello tarafından yapılabilir `WEBSITES_CONTAINER_START_TIME_LIMIT` uygulama ayarı toohello saniye cinsinden değeri gerekli. Merhaba varsayılan 230 saniyedir ve hello en fazla 600 saniyedir.

**S:** özel kayıt defteri sunucu URL'si için hello biçimi nedir?

**Y:** tooprovide hello tam kayıt defteri URL'si de dahil olmak üzere ihtiyacınız `http://` veya `https://`.

**S:** özel kayıt defteri seçeneğinde hello görüntü adı için hello biçimi nedir?

**Y:** hello özel kayıt defteri (ör. url dahil olmak üzere tooadd hello tam görüntü adı gerekiyor myacr.azurecr.io/dotnet:Latest)

**S:** tooexpose birden fazla bağlantı noktası my özel kapsayıcı görüntüde istiyorum. Bu mümkün mü?

**Y:** , şu anda desteklenmiyor.

**S:** kendi depolama kullanıma sunabilirsiniz?

**Y:** , şu anda desteklenmiyor.

**S:** hello SCM sitesinden my özel kapsayıcının dosya sistemi veya çalışan işlemler öğesine göz atamıyor. Bunun nedeni nedir?

**Y:** hello SCM site ayrı bir kapsayıcıda çalışır. Merhaba dosya sistemi denetlenemiyor veya çalışan işlemler hello uygulama kapsayıcısının.

**S:** tooa bağlantı noktası 80 numaralı bağlantı noktası dışındaki My özel kapsayıcı dinler. Uygulama tooroute hello istekleri toothat Noktam nasıl yapılandırabilir miyim?

**Y:** otomatik bağlantı noktası algılama sahibiz, denilen bir uygulama da belirtebilirsiniz **WEBSITES_PORT**ve beklenen hello bağlantı noktası numarası hello değeri verin. Daha önce hello platform tarafından kullanılan `PORT` uygulama ayarı biz toodeprecate hello kullan ayarını bu uygulamayı planlama ve toousing taşıma `WEBSITES_PORT` özel olarak.

**S:** tooimplement HTTPS my özel kapsayıcısında zorunda.

**Y:** Hayır, paylaşılan hello ön uçlar HTTPS sonlandırmanın hello platform işler.

## <a name="pricing-and-sla"></a>Fiyatlandırma ve SLA

**S:** ne olduğunu hello fiyatlandırma hello genel Önizleme kullanırken?

**Y:** hello normal Azure uygulama hizmeti fiyatlandırması ile uygulamanızın çalıştırdığı saat yarım hello sayısını ücretlendirilirsiniz. Bu, normal Azure uygulama hizmeti fiyatlandırması üzerinde bir yüzde 50 indirim almak anlamına gelir.

## <a name="other"></a>Diğer

**S:** hello desteklenen karakter uygulama ayarları adları nelerdir?

**Y:** yalnızca, A-Z, a-z, 0-9 kullanın ve alt çizgi uygulama ayarları için hello.

**S:** burada ı isteyebileceği yeni özellikler?

**Y:** ilişkin düşünceniz hello adresindeki gönderebilirsiniz [Web Apps geri bildirim Forumunda](https://aka.ms/webapps-uservoice). "[Linux]" toohello başlığı, fikir ekleyin.

## <a name="next-steps"></a>Sonraki adımlar
* [Linux üzerinde Azure Web uygulaması nedir?](app-service-linux-intro.md)
* [Linux üzerinde Azure Web uygulaması için SSH desteği](./app-service-linux-ssh-support.md)
* [Hazırlık Azure App Service ortamları ayarlama](./web-sites-staged-publishing.md)
* [Linux üzerinde Azure Web uygulaması ile sürekli dağıtımı](./app-service-linux-ci-cd.md)
