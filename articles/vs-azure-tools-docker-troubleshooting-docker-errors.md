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
# <a name="troubleshoot-visual-studio-docker-development"></a><span data-ttu-id="ebe89-103">Visual Studio Docker geliştirme sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ebe89-103">Troubleshoot Visual Studio Docker development</span></span>

<span data-ttu-id="ebe89-104">Docker Önizleme için Visual Studio Araçları ile çalışırken, hello Önizleme hello doğası nedeniyle bazı sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebe89-104">When you're working with Visual Studio Tools for Docker Preview, you may encounter some problems because of hello nature of hello preview.</span></span>
<span data-ttu-id="ebe89-105">Bazı yaygın sorunlar ve çözümleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-105">Following are some common issues and resolutions.</span></span>  

## <a name="visual-studio-2017-rc"></a><span data-ttu-id="ebe89-106">Visual Studio 2017 RC</span><span class="sxs-lookup"><span data-stu-id="ebe89-106">Visual Studio 2017 RC</span></span>

### <a name="linux-containers"></a><span data-ttu-id="ebe89-107">**Linux kapsayıcıları**</span><span class="sxs-lookup"><span data-stu-id="ebe89-107">**Linux containers**</span></span>

####  <a name="build-errors-occur-when-debugging-a-net-core-web-or-console-application"></a><span data-ttu-id="ebe89-108">Derleme hataları oluşur .NET Core web veya konsol uygulama hata ayıklama sırasında</span><span class="sxs-lookup"><span data-stu-id="ebe89-108">Build errors occur when debugging a .NET Core web or console application</span></span>  

<span data-ttu-id="ebe89-109">Bu ilgili toonot ile Docker için Windows hello proje bulunduğu hello sürücü paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-109">This could be related toonot sharing hello drive where hello project resides with Docker for Windows.</span></span>  <span data-ttu-id="ebe89-110">Merhaba aşağıdaki gibi bir hata iletisini alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ebe89-110">You may receive an error like hello following:</span></span>

```
hello "PrepareForLaunch" task failed unexpectedly.
Microsoft.DotNet.Docker.CommandLineClientException: Creating network "webapplication13628050196_default" with hello default driver
Building webapplication1
Creating webapplication13628050196_webapplication1_1
ERROR: for webapplication1  Cannot create container for service webapplication1: C: drive is not shared. Please share it in Docker for Windows Settings
```
<span data-ttu-id="ebe89-111">tooresolve bu sorunu:</span><span class="sxs-lookup"><span data-stu-id="ebe89-111">tooresolve this issue:</span></span>

1. <span data-ttu-id="ebe89-112">Sağ **Windows için Docker** hello bildirim alanına ve ardından **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-112">Right-click **Docker for Windows** in hello notification area, and then select **Settings**.</span></span>  
2. <span data-ttu-id="ebe89-113">Seçin **paylaşılan sürücüleri** ve paylaşma hello proje bulunduğu hello sürücü.</span><span class="sxs-lookup"><span data-stu-id="ebe89-113">Select **Shared Drives** and share hello drive where hello project resides.</span></span>

### <a name="windows-containers"></a><span data-ttu-id="ebe89-114">**Windows kapsayıcıları**</span><span class="sxs-lookup"><span data-stu-id="ebe89-114">**Windows containers**</span></span>

<span data-ttu-id="ebe89-115">Merhaba aşağıdaki belirli toodebugging .NET Framework web ve konsol uygulamaları Windows kapsayıcılarında sorunlardır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-115">hello following issues are specific toodebugging .NET Framework web and console applications in Windows containers.</span></span>

#### <a name="prerequisites"></a><span data-ttu-id="ebe89-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ebe89-116">Prerequisites</span></span>

1. <span data-ttu-id="ebe89-117">Visual Studio 2017 RC (veya üstü) ile .NET Core hello ve Docker Önizleme iş yükü yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-117">Visual Studio 2017 RC (or later) with hello .NET Core and Docker Preview workload must be installed.</span></span>
2. <span data-ttu-id="ebe89-118">Windows 10 Anniversary Update en son Windows Update ile düzeltme ekleri.</span><span class="sxs-lookup"><span data-stu-id="ebe89-118">Windows 10 Anniversary Update with that latest Windows Update patches.</span></span> <span data-ttu-id="ebe89-119">Özellikle [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) yüklü olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-119">Specifically [KB3194798](https://support.microsoft.com/en-us/help/3194798/cumulative-update-for-windows-10-version-1607-and-windows-server-2016-october-11,-2016) must be installed.</span></span> 
3. <span data-ttu-id="ebe89-120">[Windows için docker](https://docs.docker.com/docker-for-windows/) (1.13.0 yapı veya sonraki bir sürümü) yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-120">[Docker for Windows](https://docs.docker.com/docker-for-windows/) (build 1.13.0 or later) must be installed.</span></span>
4. <span data-ttu-id="ebe89-121">**Geçiş tooWindows kapsayıcıları** seçilmelidir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-121">**Switch tooWindows containers** must be selected.</span></span> <span data-ttu-id="ebe89-122">Merhaba bildirim alanında tıklatın **Windows için Docker**ve ardından **geçiş tooWindows kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-122">In hello notification area, click **Docker for Windows**, and then select **Switch tooWindows containers**.</span></span> <span data-ttu-id="ebe89-123">Merhaba makine yeniden başlatıldıktan sonra bu ayar korunur emin olun.</span><span class="sxs-lookup"><span data-stu-id="ebe89-123">After hello machine restarts, ensure that this setting is retained.</span></span>

#### <a name="console-output-does-not-appear-in-visual-studios-output-window-while-debugging-a-console-application"></a><span data-ttu-id="ebe89-124">Konsol çıktısı Visual Studio'nun çıktı penceresinde bir konsol uygulaması hata ayıklama sırasında görünmüyor</span><span class="sxs-lookup"><span data-stu-id="ebe89-124">Console output does not appear in Visual Studio's output window while debugging a console application</span></span>

<span data-ttu-id="ebe89-125">Bu, şu anda bu senaryo için tasarlanmamıştır hello Visual Studio hata ayıklayıcısı (msvsmon.exe) ile bilinen bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="ebe89-125">This is a known issue with hello Visual Studio debugger (msvsmon.exe), which is currently not designed for this scenario.</span></span> <span data-ttu-id="ebe89-126">Bu senaryo için destek gelecekteki bir sürümde dahil.</span><span class="sxs-lookup"><span data-stu-id="ebe89-126">Support for this scenario might be included in a future release.</span></span> <span data-ttu-id="ebe89-127">Visual Studio'da kullanım hello konsol uygulamasından toosee çıkışın **Docker: başlangıç projesi**, çok eşdeğerdir**Başlat hata ayıklama olmadan**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-127">toosee output from hello console application in Visual Studio, use **Docker: Start Project**, which is equivalent too**Start without Debugging**.</span></span>

#### <a name="debugging-web-applications-with-hello-release-configuration-fails-with-403-forbidden-error"></a><span data-ttu-id="ebe89-128">Web uygulamalarında hata ayıklama hello (403) Yasak hatası ile başarısız oluyor yapılandırma yayın</span><span class="sxs-lookup"><span data-stu-id="ebe89-128">Debugging web applications with hello release configuration fails with (403) Forbidden error</span></span>

<span data-ttu-id="ebe89-129">Bu soruna geçici bir çözüm toowork hello çözüm web.release.config açın ve çıkışı yorum yapmak veya satırlardan hello Sil:</span><span class="sxs-lookup"><span data-stu-id="ebe89-129">toowork around this issue, open web.release.config in hello solution and comment out or delete hello following lines:</span></span>

```
<compilation xdt:Transform="RemoveAttributes(debug)" />
```

## <a name="visual-studio-2015"></a><span data-ttu-id="ebe89-130">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ebe89-130">Visual Studio 2015</span></span>

### <a name="linux-containers"></a><span data-ttu-id="ebe89-131">**Linux kapsayıcıları**</span><span class="sxs-lookup"><span data-stu-id="ebe89-131">**Linux containers**</span></span>

#### <a name="unable-toovalidate-volume-mapping"></a><span data-ttu-id="ebe89-132">%S toovalidate birim eşleme</span><span class="sxs-lookup"><span data-stu-id="ebe89-132">Unable toovalidate volume mapping</span></span>
<span data-ttu-id="ebe89-133">Birimi eşlemenin gerekli tooshare hello kaynak kodu ve ikili dosyaları uygulamanızın hello kapsayıcısında hello uygulama klasörle ' dir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-133">Volume mapping is required tooshare hello source code and binaries of your application with hello app folder in hello container.</span></span>  <span data-ttu-id="ebe89-134">Özel birim eşlemeleri docker compose.dev.debug.yml ve docker compose.dev.release.yml içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-134">Specific volume mappings are contained within docker-compose.dev.debug.yml and docker-compose.dev.release.yml.</span></span> <span data-ttu-id="ebe89-135">Ana makinede değişen dosyaları gibi Merhaba kapsayıcılara benzer bir klasörü yapısı içinde bu değişiklikleri yansıtır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-135">As files are changed on your host machine, hello containers reflect these changes in a similar folder structure.</span></span>

<span data-ttu-id="ebe89-136">tooenable birimi eşlemenin:</span><span class="sxs-lookup"><span data-stu-id="ebe89-136">tooenable volume mapping:</span></span>

1. <span data-ttu-id="ebe89-137">Tıklatın **Moby** hello bildirim alanı seçip **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-137">Click **Moby** in hello notification area and select **Settings**.</span></span>
2. <span data-ttu-id="ebe89-138">Seçin **sürücüler paylaşılan**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-138">Select **Shared Drives**.</span></span>
3. <span data-ttu-id="ebe89-139">% USERPROFILE % bulunduğu proje ve hello sürücünüze barındıran hello sürücü seçin.</span><span class="sxs-lookup"><span data-stu-id="ebe89-139">Select hello drive that hosts your project and hello drive where %USERPROFILE% resides.</span></span>
4. <span data-ttu-id="ebe89-140">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-140">Click **Apply**.</span></span>

<span data-ttu-id="ebe89-141">tootest birimi eşlemenin çalışıyorsa, yeniden oluşturun ve bir veya daha fazla sürücü paylaşılan, veya silinmiş bir komut isteminden koddan hello çalıştırmak sonra gelen Visual Studio içinde F5 seçin.</span><span class="sxs-lookup"><span data-stu-id="ebe89-141">tootest if volume mapping is functioning, Rebuild and select F5 from within Visual Studio after one or more drives have been shared, or run hello following code from a command prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="ebe89-142">Bu örnekte, kullanıcıların klasörünüze C sürücüsünde bulunur ve paylaşılan sahip varsayılır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-142">This example assumes that your Users folder is located on drive C and that it has been shared.</span></span>
> <span data-ttu-id="ebe89-143">Farklı bir sürücü paylaştırılmışsa gerektiği şekilde düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ebe89-143">Revise as necessary if you have shared a different drive.</span></span>

```
docker run -it -v /c/Users/Public:/wormhole busybox
```

<span data-ttu-id="ebe89-144">Merhaba Linux kapsayıcısında koddan hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-144">Run hello following code in hello Linux container.</span></span>

```
/ # ls
```

<span data-ttu-id="ebe89-145">Bir dizin hello kullanıcıları/ortak klasöründen listesi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-145">You should see a directory listing from hello Users/Public folder.</span></span> <span data-ttu-id="ebe89-146">Hiçbir dosya görüntülenir ve /c/Users/Public klasörünüze boş yoksa, birimi eşlemenin düzgün yapılandırılmamış.</span><span class="sxs-lookup"><span data-stu-id="ebe89-146">If no files are displayed and your /c/Users/Public folder isn't empty, volume mapping is not configured properly.</span></span>

```
bin       etc       proc      sys       usr       wormhole
dev       home      root      tmp       var
```

<span data-ttu-id="ebe89-147">Değiştirme toohello deliği dizin toosee Merhaba içeriğine hello `/c/Users/Public` dizini:</span><span class="sxs-lookup"><span data-stu-id="ebe89-147">Change toohello wormhole directory toosee hello contents of hello `/c/Users/Public` directory:</span></span>

```
/ # cd wormhole/
/wormhole # ls
AccountPictures  Downloads        Music            Videos
Desktop          Host             NuGet.Config     desktop.ini
Documents        Libraries        Pictures
/wormhole #
```

> [!NOTE]
> <span data-ttu-id="ebe89-148">Linux VM'ler ile çalışırken, hello kapsayıcı dosya sistemi büyük küçük harfe duyarlı değil.</span><span class="sxs-lookup"><span data-stu-id="ebe89-148">When you're working with Linux VMs, hello container file system is case-sensitive.</span></span>

## <a name="build-prepareforbuild-task-failed-unexpectedly"></a><span data-ttu-id="ebe89-149">Derleme: "PrepareForBuild" görevi beklenmedik şekilde başarısız oldu</span><span class="sxs-lookup"><span data-stu-id="ebe89-149">Build: "PrepareForBuild" task failed unexpectedly</span></span>

<span data-ttu-id="ebe89-150">Microsoft.DotNet.Docker.CommandLine.ClientException: Çalışırken tooconnect bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="ebe89-150">Microsoft.DotNet.Docker.CommandLine.ClientException: An error occurred trying tooconnect.</span></span>

<span data-ttu-id="ebe89-151">Merhaba varsayılan Docker barındıran çalışıp çalışmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ebe89-151">Verify that hello default Docker host is running.</span></span> <span data-ttu-id="ebe89-152">Bir komut istemi açın ve yürütün:</span><span class="sxs-lookup"><span data-stu-id="ebe89-152">Open a command prompt and execute:</span></span>

```
docker info
```

<span data-ttu-id="ebe89-153">Bu hata verirse toostart hello denemesi **Windows için Docker** masaüstü uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ebe89-153">If this returns an error, then attempt toostart hello **Docker for Windows** desktop app.</span></span> <span data-ttu-id="ebe89-154">Merhaba masaüstü uygulaması, ardından çalışıyorsa **Moby** hello bildirim alanında görünür olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ebe89-154">If hello desktop app is running, then **Moby** should be visible in hello notification area.</span></span> <span data-ttu-id="ebe89-155">Sağ **Moby** açarak **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ebe89-155">Right-click **Moby** and open **Settings**.</span></span> <span data-ttu-id="ebe89-156">Tıklatın **sıfırlama**ve Docker yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-156">Click **Reset**, and then restart Docker.</span></span>

## <a name="an-error-dialog-occurs-when-attempting-tooadd-docker-support-or-debug-f5-an-aspnet-core-application-in-a-container"></a><span data-ttu-id="ebe89-157">Hata iletişim kutusu tooadd Docker destek çalışırken oluşur veya (F5) bir kapsayıcı ASP.NET Core uygulamada hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="ebe89-157">An error dialog occurs when attempting tooadd Docker Support or debug (F5) an ASP.NET Core application in a container</span></span>

<span data-ttu-id="ebe89-158">Kaldırma ve uzantılarını yüklemeden sonra Visual Studio Yönetilen Genişletilebilirlik Çerçevesi (MEF) önbellekte hello bozulabilir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-158">After uninstalling and installing extensions, hello Managed Extensibility Framework (MEF) cache in Visual Studio can become corrupted.</span></span> <span data-ttu-id="ebe89-159">Bu durumda, Docker desteği ekleme olduğunda ve/veya toorun çalışırken çeşitli hata iletilerine neden veya (F5) ASP.NET Core uygulamanızda hata ayıklama yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ebe89-159">When this occurs, it can cause various error messages when you're adding Docker Support and/or attempting toorun or debug (F5) your ASP.NET Core application.</span></span> <span data-ttu-id="ebe89-160">Geçici bir çözüm olarak, aşağıdaki adımları toodelete ve yeniden hello MEF önbelleği hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-160">As a temporary workaround, use hello following steps toodelete and regenerate hello MEF cache.</span></span>

1. <span data-ttu-id="ebe89-161">Visual Studio tüm örneklerini kapatın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-161">Close all instances of Visual Studio.</span></span>
1. <span data-ttu-id="ebe89-162">% USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\ açın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-162">Open %USERPROFILE%\AppData\Local\Microsoft\VisualStudio\14.0\.</span></span>
1. <span data-ttu-id="ebe89-163">Klasörleri aşağıdaki hello Sil:</span><span class="sxs-lookup"><span data-stu-id="ebe89-163">Delete hello following folders:</span></span>
     ```
       ComponentModelCache
       Extensions
       MEFCacheBackup
    ```
1. <span data-ttu-id="ebe89-164">Visual Studio'yu açın.</span><span class="sxs-lookup"><span data-stu-id="ebe89-164">Open Visual Studio.</span></span>
1. <span data-ttu-id="ebe89-165">Merhaba senaryo yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ebe89-165">Attempt hello scenario again.</span></span>
