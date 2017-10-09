---
title: "Visual Studio kullanarak aaaTroubleshooting Docker istemci hataları Windows | Microsoft Docs"
description: "Visual Studio toocreate kullanırken karşılaştığınız sorunları gidermek ve Windows'da web uygulamaları tooDocker Visual Studio kullanarak dağıtın."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 346f70b9-7b52-4688-a8e8-8f53869618d3
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 7421ae8e044d58fc412d748fb870da4c9b2fdb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-visual-studio-docker-development"></a>Visual Studio Docker geliştirme sorun giderme

Docker Önizleme için Visual Studio Araçları ile çalışırken, hello Önizleme hello doğası nedeniyle bazı sorunlarla karşılaşabilirsiniz.
Bazı yaygın sorunlar ve çözümleri aşağıda verilmiştir.  

## <a name="visual-studio-2017-rc"></a>Visual Studio 2017 RC

### <a name="linux-containers"></a>**Linux kapsayıcıları**

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a>Derleme hataları oluşur .NET Core web veya konsol uygulama hata ayıklama sırasında  

Bu ilgili toonot ile Docker için Windows hello proje bulunduğu hello sürücü paylaşımı olabilir.  Merhaba aşağıdaki gibi bir hata iletisini alabilirsiniz:

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
tooresolve bu sorunu:

1. Sağ **Windows için Docker** hello bildirim alanına ve ardından **ayarları**.  
2. Seçin **paylaşılan sürücüleri** ve paylaşma hello proje bulunduğu hello sürücü.

### <a name="windows-containers"></a>**Windows kapsayıcıları**

Merhaba aşağıdaki belirli toodebugging .NET Framework web ve konsol uygulamaları Windows kapsayıcılarında sorunlardır.

#### <a name="prerequisites"></a>Ön koşullar

1. Visual Studio 2017 RC (veya üstü) ile .NET Core hello ve Docker Önizleme iş yükü yüklü olmalıdır.
2. Windows 10 Anniversary Update en son Windows Update ile düzeltme ekleri. Özellikle [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) yüklü olması gerekir. 
3. [Windows için docker](https://docs.docker.com/docker-for-windows/) (1.13.0 yapı veya sonraki bir sürümü) yüklü olmalıdır.
4. **Geçiş tooWindows kapsayıcıları** seçilmelidir. Merhaba bildirim alanında tıklatın **Windows için Docker**ve ardından **geçiş tooWindows kapsayıcıları**. Merhaba makine yeniden başlatıldıktan sonra bu ayar korunur emin olun.

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a>Konsol çıktısı Visual Studio'nun çıktı penceresinde bir konsol uygulaması hata ayıklama sırasında görünmüyor

Bu, şu anda bu senaryo için tasarlanmamıştır hello Visual Studio hata ayıklayıcısı (msvsmon.exe) ile bilinen bir sorundur. Bu senaryo için destek gelecekteki bir sürümde dahil. Visual Studio'da kullanım hello konsol uygulamasından toosee çıkışın **Docker: başlangıç projesi**, çok eşdeğerdir**Başlat hata ayıklama olmadan**.

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a>Web uygulamalarında hata ayıklama hello (403) Yasak hatası ile başarısız oluyor yapılandırma yayın

Bu soruna geçici bir çözüm toowork hello çözüm web.release.config açın ve çıkışı yorum yapmak veya satırlardan hello Sil:

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a>Visual Studio 2015

### <a name="linux-containers"></a>**Linux kapsayıcıları**

#### <a name="unable-toovalidate-volume-mapping"></a>%S toovalidate birim eşleme
Birimi eşlemenin gerekli tooshare hello kaynak kodu ve ikili dosyaları uygulamanızın hello kapsayıcısında hello uygulama klasörle ' dir.  Özel birim eşlemeleri docker compose.dev.debug.yml ve docker compose.dev.release.yml içinde yer alır. Ana makinede değişen dosyaları gibi Merhaba kapsayıcılara benzer bir klasörü yapısı içinde bu değişiklikleri yansıtır.

tooenable birimi eşlemenin:

1. Tıklatın **Moby** hello bildirim alanı seçip **ayarları**.
2. Seçin **sürücüler paylaşılan**.
3. % USERPROFILE % bulunduğu proje ve hello sürücünüze barındıran hello sürücü seçin.
4. **Uygula**'ya tıklayın.

tootest birimi eşlemenin çalışıyorsa, yeniden oluşturun ve bir veya daha fazla sürücü paylaşılan, veya silinmiş bir komut isteminden koddan hello çalıştırmak sonra gelen Visual Studio içinde F5 seçin.

> [!NOTE]
> Bu örnekte, kullanıcıların klasörünüze C sürücüsünde bulunur ve paylaşılan sahip varsayılır.
> Farklı bir sürücü paylaştırılmışsa gerektiği şekilde düzeltin.

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

Merhaba Linux kapsayıcısında koddan hello çalıştırın.

```
/ # ls
```

Bir dizin hello kullanıcıları/ortak klasöründen listesi görmeniz gerekir. Hiçbir dosya görüntülenir ve /c/Users/Public klasörünüze boş yoksa, birimi eşlemenin düzgün yapılandırılmamış.

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

Değiştirme toohello deliği dizin toosee Merhaba içeriğine hello `/c/Users/Public` dizini:

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> Linux VM'ler ile çalışırken, hello kapsayıcı dosya sistemi büyük küçük harfe duyarlı değil.

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a>Derleme: "PrepareForBuild" görevi beklenmedik şekilde başarısız oldu

Microsoft.DotNet.Docker.CommandLine.ClientException: Çalışırken tooconnect bir hata oluştu.

Merhaba varsayılan Docker barındıran çalışıp çalışmadığını denetleyin. Bir komut istemi açın ve yürütün:

```
docker info
```

Bu hata verirse toostart hello denemesi **Windows için Docker** masaüstü uygulaması. Merhaba masaüstü uygulaması, ardından çalışıyorsa **Moby** hello bildirim alanında görünür olmalıdır. Sağ **Moby** açarak **ayarları**. Tıklatın **sıfırlama**ve Docker yeniden başlatın.

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a>Hata iletişim kutusu tooadd Docker destek çalışırken oluşur veya (F5) bir kapsayıcı ASP.NET Core uygulamada hata ayıklama

Kaldırma ve uzantılarını yüklemeden sonra Visual Studio Yönetilen Genişletilebilirlik Çerçevesi (MEF) önbellekte hello bozulabilir. Bu durumda, Docker desteği ekleme olduğunda ve/veya toorun çalışırken çeşitli hata iletilerine neden veya (F5) ASP.NET Core uygulamanızda hata ayıklama yükleyebilir. Geçici bir çözüm olarak, aşağıdaki adımları toodelete ve yeniden hello MEF önbelleği hello kullanın.

1. Visual Studio tüm örneklerini kapatın.
1. % USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\ açın.
1. Klasörleri aşağıdaki hello Sil:
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. Visual Studio'yu açın.
1. Merhaba senaryo yeniden deneyin.
