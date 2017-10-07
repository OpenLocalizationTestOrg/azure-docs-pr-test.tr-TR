---
title: "yerel bir Docker kapsayıcısı aaaDebugging uygulamalarında | Microsoft Docs"
description: "Nasıl toomodify yerel Docker kapsayıcısı içinde çalışan bir uygulama hello kapsayıcı düzenleme ve yenileme aracılığıyla yenileyin ve hata ayıklama kesme noktaları ayarlayın öğrenin"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>Yerel Docker kapsayıcısındaki uygulamalar için hata ayıklama
## <a name="overview"></a>Genel Bakış
Docker için Visual Studio Araçları Hello bir tutarlı bir yol toodevelop sağlar ve uygulamanızda yerel olarak Linux Docker kapsayıcısı doğrulayın.
Bir kod değişikliği yaptığınızda toorestart hello kapsayıcısı yok.
Bu makalede nasıl toouse hello "Düzenle ve Yenile" özelliği toostart yerel bir Docker kapsayıcısı ASP.NET çekirdek Web uygulamasında gerekli değişiklikleri yapın ve ardından bu değişiklikleri hello tarayıcı toosee yenileyin gösterilmektedir.
Bu makalede ayrıca nasıl gösterilmektedir hata ayıklama için tooset kesme noktaları.

> [!NOTE]
> Windows kapsayıcı desteği gelecekteki bir sürümde geliyor
>
>

## <a name="prerequisites"></a>Ön koşullar
Araçlar aşağıdaki hello yüklü olması gerekir.

* [Visual Studio en son sürümü](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET Core 1.0 SDK'sı](https://go.microsoft.com/fwlink/?LinkID=809122)

yerel olarak toorun Docker kapsayıcıları için yerel docker istemci gerekir.
Hello kullanabilirsiniz [Docker araç](https://www.docker.com/products/docker-toolbox), Hyper-V toobe devre dışı gerektiren veya kullanabilirsiniz [Docker için Windows](https://www.docker.com/get-docker), Hyper-V kullanır ve Windows 10 gerektirir.

Docker araç kullanıyorsanız, çok gerekir[hello Docker istemcisini yapılandırma](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1. Web uygulaması oluşturma
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2. Docker desteği ekleme
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3. Kod ve yenileme Düzenle
tooquickly yinelemek değişiklikleri, uygulamanızı bir kapsayıcıdaki başlatın ve IIS Express ile olduğu gibi bunları görüntüleme toomake değişiklikler devam.

1. Merhaba çözüm yapılandırma çok ayarlamak`Debug` ve tuşuna basın  **&lt;CTRL + F5 >** toobuild, docker görüntü ve yerel olarak çalıştırın.

    Merhaba kapsayıcı görüntü oluşturulduğundan ve Docker kapsayıcısı içinde çalışan sonra Visual Studio varsayılan tarayıcınızda hello Web uygulaması başlatın.
    Merhaba Microsoft Edge tarayıcı kullanıyorsanız veya aksi halde hatalar varsa, bkz: [sorun giderme](vs-azure-tools-docker-troubleshooting-docker-errors.md) bölümü.
2. Toohello toomake değişikliklerimizi burada yapacağız olduğundan sayfa hakkında gidin.
3. TooVisual Studio dönün ve açık `Views\Home\About.cshtml`.
4. HTML içerik toohello hello dosyasının sonuna aşağıdaki hello ekleyin ve hello değişiklikleri kaydedin.

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. Hello çıktı penceresinde hello .NET derleme tamamlandığında ve bu satırları görmek görüntüleme, geri tooyour tarayıcı geçin ve sayfa hakkında hello yenileyin.

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. Yaptığınız değişiklikleri uygulandı!

## <a name="4-debug-with-breakpoints"></a>4. Kesme noktaları ile hata ayıklama
Genellikle, değişiklikleri daha ayrıntılı denetleme, Visual Studio'nun özellikleri hata ayıklama hello yararlanarak gerekir.

1. Dönüş tooVisual Studio ve Aç`Controllers\HomeController.cs`
2. Merhaba About() yöntemi Merhaba içeriğine hello şununla değiştirin:

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. Kesme noktası toohello Merhaba sol kümesi `string message`... satır.
4. İsabet  **&lt;F5 >** toostart hata ayıklama.
5. Sayfa toohit hakkında toohello isabetini gidin.
6. TooVisual Studio tooview hello kesme geçin ve ileti hello değerini inceleyin.

   ![][2]

## <a name="summary"></a>Özet
İle [Docker için Visual Studio 2015 Araçları](https://aka.ms/DockerToolsForVS), yerel olarak Docker kapsayıcısı içinde geliştirmenin hello üretim daha iyi çalışma hello verimliliği elde edebilirsiniz.

## <a name="troubleshooting"></a>Sorun giderme
[Visual Studio Docker geliştirme sorunlarını giderme](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>Visual Studio, Windows ve Azure ile Docker hakkında daha fazla bilgi
* [Visual Studio için docker Araçları](http://aka.ms/dockertoolsforvs) -.NET Core kodunuzda bir kapsayıcı geliştirme
* [Visual Studio Team Services için docker Araçları](http://aka.ms/dockertoolsforvsts) - yapı ve docker kapsayıcıları dağıtın
* [Visual Studio Code için docker Araçları](http://aka.ms/dockertoolsforvscode) -daha fazla e2e senaryo gelen docker dosyalarını düzenlemek için dil Hizmetleri
* [Windows kapsayıcı bilgileri](http://aka.ms/containers)-Windows Server ve Nano Server bilgileri
* [Azure kapsayıcı hizmeti](https://azure.microsoft.com/services/container-service/) - [Azure kapsayıcı hizmeti içerik](http://aka.ms/AzureContainerService)
* Docker ile çalışmaya ilişkin daha fazla örnek için bkz: [Docker ile çalışma](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) hello gelen [tanıtımında](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/). Merhaba tanıtımında demo öğesinden daha fazla quickstarts için bkz: [Azure geliştirici araçları hızlı başlangıç ipuçları](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).

## <a name="various-docker-tools"></a>Çeşitli Docker araçları
[Bazı harika docker Araçlar (Steve Lasker'ın blogu)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>İyi makaleler
[Giriş tooMicroservices NGINX gelen](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>Sunular
* [Steve Lasker: VS Las Vegas 2016 - Docker e2e Canlı](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [Yapı 2016 - Burada, adresindeki Demo @ giriş tooASP.NET çekirdek](https://channel9.msdn.com/Events/Build/2016/B810)
* [Kapsayıcılardaki Channel 9 .NET uygulamaları geliştirme](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
