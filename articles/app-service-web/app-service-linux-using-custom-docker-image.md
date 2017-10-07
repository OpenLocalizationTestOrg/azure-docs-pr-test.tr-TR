---
title: "aaaHow toouse Linux Azure Web uygulaması için özel bir Docker görüntü | Microsoft Docs"
description: "Nasıl toouse özel Docker görüntü Linux Azure Web uygulaması için."
keywords: "Azure uygulama hizmeti, web uygulaması, linux, docker, kapsayıcı"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Linux üzerinde Azure Web uygulaması için özel bir Docker görüntü kullanma #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Uygulama hizmeti önceden tanımlanmış uygulama yığınları PHP 7.0 ve Node.js 4.5 gibi belirli sürümleri için destek ile Linux'ta sağlar. Uygulama hizmeti Linux'ta kullanan Docker kapsayıcıları toohost bunlar önceden oluşturulmuş uygulama yığınları. Bir özel Docker görüntü toodeploy Azure içinde tanımlı değil, web uygulaması tooan uygulama yığınını de kullanabilirsiniz. Özel Docker görüntülerinizi ya da bir genel veya özel Docker deposu üzerinde barındırılabilir.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Nasıl yapılır: bir web uygulaması için özel bir Docker resmi ayarlama
Merhaba özel Docker görüntü için hem de yeni ve mevcut webs uygulamalar ayarlayabilirsiniz. Oluşturduğunuzda, bir web uygulaması Linux'ta hello [Azure portal](https://portal.azure.com/#create/Microsoft.AppSvcLinux), tıklatın **yapılandırma kapsayıcısı** tooset özel Docker görüntü:

![Linux üzerinde yeni bir web uygulaması için özel Docker görüntü][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Nasıl yapılır: özel Docker görüntü Docker hub'dan kullanın ##
toouse Docker hub'dan özel Docker görüntü:

1. Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **Docker kapsayıcısı**.

2.  Seçin **Docker hub'a** hello olarak **görüntü kaynağı**, ya da ardından **ortak** veya **özel** ve türü hello **görüntü ve İsteğe bağlı etiket adı**, gibi `node:4.5`. Merhaba **başlangıç komutu** kümesi hello Docker yansıma dosyasında tanımlanmış üzerinde otomatik olarak temel alır, ancak kendi komutları ayarlayabilirsiniz.  

    ![Yapılandırma Docker hub'a genel depo resmi][2]

    Görüntünüzü özel depodan olduğunda tooenter hello Docker hub'a kimlik olarak da gerekir (**oturum açma kullanıcı** ve **parola**) hello özel Docker hub'a depo.

    ![Yapılandırma Docker hub'a özel depo resmi][3]

3. Merhaba kapsayıcı yapılandırdıktan sonra tıklatın **kaydetmek**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Nasıl toouse bir Docker görüntü özel görüntü kayıt defterinden ##
özel görüntü kayıt defterinden özel Docker görüntü toouse:

1. Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **Docker kapsayıcısı**.

2.  Tıklatın **özel kayıt defteri** hello olarak **görüntü kaynağı**. Merhaba girin **görüntü ve isteğe bağlı etiket adı**, **sunucu URL'si** hello kimlik bilgileri ile birlikte hello özel kayıt için (**oturum açma kullanıcı** ve **parola** ). **Kaydet** düğmesine tıklayın.

    ![Yapılandırma özel kayıt defteri Docker resmi][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Nasıl yapılır: ayarlama, Docker görüntü tarafından kullanılan başlangıç bağlantı noktası ##

Web uygulamanız için özel bir Docker görüntü kullandığınızda hello kullanabilirsiniz `WEBSITES_PORT` oluşturulan toohello kapsayıcı eklenen, Dockerfile ortam değişkeni. Söyleniş bir uygulama için bir docker dosyası örneği aşağıdaki hello göz önünde bulundurun:

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

Merhaba komutu son satırında, bu hello WEBSITES_PORT ortam değişkeni çalışma zamanında geçirilen görebilirsiniz. Büyük/küçük harf komutlarda önemli unutmayın.

Daha önce hello platform tarafından kullanılan `PORT` uygulama ayarı biz toodeprecate hello kullan ayarını bu uygulamayı planlama ve toousing taşıma `WEBSITES_PORT` özel olarak.

Başka bir kullanıcı tarafından oluşturulmuş var olan bir Docker görüntüsünü kullandığınızda, toospecify bağlantı noktası 80 dışında bir bağlantı noktası hello uygulama için gerekebilir. tooconfigure Merhaba bağlantı noktası, adlandırılmış ayarlama uygulama ekleme `WEBSITES_PORT` aşağıda gösterildiği gibi hello değere sahip:

![Özel Docker görüntü için bağlantı noktası uygulama ayarını yapılandırın][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Nasıl yapılır: hello başlangıç saati, Docker görüntüsü için ayarlayın ##

Varsayılan olarak, kapsayıcı 230 saniye önce başlamazsa hello platform, kapsayıcı yeniden başlatılır. Özel Docker görüntünüzü 230 saniyeden fazla başlarsa, hello kullanabilirsiniz `WEBSITES_CONTAINER_START_TIME_LIMIT` ayarını, uygulama için bu ayarın hello değerini saniye cinsinden, bu yeniden başlatmadan önce çalışan, kapsayıcı hello platform Koru izin verir. Merhaba varsayılan değer 230 saniyedir ve hello en büyük değer 600 saniye izin verilir.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Nasıl yapılır: hello sağlanan platformu depolama çıkarın ##

Varsayılan olarak, kalıcı depolama paylaşımı toohello hello platform bağlar `\home\` dizin. Kapsayıcı görüntünüzü kalıcı bir paylaşımı gerekli değildir, bu depolama ayarı hello tarafından takma devre dışı bırakabilirsiniz `WEBSITES_ENABLE_APP_SERVICE_STORAGE` uygulama çok ayarı`false`. Hala hello scm sitesinden erişim toothat depolama alanına sahip ve tüm Docker günlükleri (etkinse) hello platformu tarafından oluşturulan toohello günlük dosyaları yazılır.

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Nasıl yapılır: geri dönün toousing yerleşik bir görüntü ##

özel görüntü toousing yerleşik bir görüntü kullanarak tooswitch:

1. Merhaba, [Azure portal](https://portal.azure.com), web uygulamanızı Linux üzerinde sonra bulun **ayarları** tıklatın **uygulama hizmeti**.

2. Seçin, **çalışma zamanı yığın** toouse hello yerleşik görüntüsü, ardından **kaydetmek**. 

![Yerleşik Docker görüntüsü yapılandırma][5]


## <a name="troubleshooting"></a>Sorun giderme ##

Toostart özel Docker görüntünüzü ile uygulamanızı başarısız olduğunda, hello hello LogFiles dizininde Docker günlüklerini denetleyin. SCM siteniz veya FTP aracılığıyla bu dizine erişebilir.
toolog hello `stdout` ve `stderr` tooenable gerekir, kapsayıcıdan **Docker kapsayıcısı günlük** altında **tanılama günlükleri**.

![Günlüğü etkinleştirme][8]

![Kudu tooview Docker günlüklerini kullanma][7]

Merhaba SCM sitesinden erişebilirsiniz **Gelişmiş Araçlar** hello içinde **geliştirme araçları** menüsü.

## <a name="next-steps"></a>Sonraki Adımlar ##

Linux üzerinde Web uygulaması ile çalışmaya bağlantılar tooget aşağıdaki hello izleyin.   

* [Giriş tooAzure Linux üzerinde Web uygulaması](./app-service-linux-intro.md)
* [Linux üzerinde Azure Web uygulamasında Node.js için PM2 Yapılandırması'nı kullanarak](./app-service-linux-using-nodejs-pm2.md)
* [Azure App Service Web uygulaması Linux SSS](app-service-linux-faq.md)

POST sorular ve sorunları üzerinde [forumumuzda](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
