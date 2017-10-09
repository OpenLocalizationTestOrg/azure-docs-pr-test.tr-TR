---
title: "aaaDeploy MongoDB kullanan bir Node.js uygulaması | Microsoft Docs"
description: "İzlenecek yol nasıl toopackage birden çok Konuk yürütülebilir dosyalar toodeploy tooan Azure Service Fabric kümesi"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="35897-103">Konuk tarafından yürütülebilir birden çok uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="35897-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="35897-104">Bu makalede gösterilmektedir nasıl toopackage ve birden çok Konuk yürütülebilir dosyalar tooAzure Service Fabric dağıtın.</span><span class="sxs-lookup"><span data-stu-id="35897-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="35897-105">Oluşturma ve tek bir Service Fabric paketi dağıtma nasıl çok okumak için[Konuk yürütülebilir tooService doku dağıtmak](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="35897-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="35897-106">Bu kılavuzda nasıl toodeploy MongoDB hello veri deposu olarak kullanan bir Node.js ön ucuna sahip bir uygulama, başka bir uygulama bağımlılıkları olan hello adımları tooany uygulama uygulayabileceğiniz gösterirken.</span><span class="sxs-lookup"><span data-stu-id="35897-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="35897-107">Birden çok Konuk yürütülebilir dosyaları içeren Visual Studio tooproduce hello uygulama paketi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35897-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="35897-108">Bkz: [kullanarak Visual Studio toopackage varolan bir uygulama](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="35897-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="35897-109">Merhaba ilk Konuk yürütülebilir ekledikten sonra sağ hello uygulama projesi seçin hello tıklayın ve **Ekle -> Yeni Service Fabric hizmet** tooadd hello ikinci Konuk yürütülebilir proje toohello çözüm.</span><span class="sxs-lookup"><span data-stu-id="35897-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="35897-110">Not: hello hello Visual Studio çözümü oluşturma, Visual Studio projesi toolink hello kaynağında, emin olmanızı sağlayacak seçerseniz, uygulama paketinizi hello kaynağındaki değişikliklerle toodate çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="35897-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="35897-111">Örnekler</span><span class="sxs-lookup"><span data-stu-id="35897-111">Samples</span></span>
* [<span data-ttu-id="35897-112">Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek</span><span class="sxs-lookup"><span data-stu-id="35897-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="35897-113">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="35897-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="35897-114">El ile paket hello birden çok Konuk yürütülebilir uygulama</span><span class="sxs-lookup"><span data-stu-id="35897-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="35897-115">Bunun yerine el ile Merhaba Konuk yürütülebilir paketleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35897-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="35897-116">Hello için el ile paketleme, bu makalede şu adresten edinilebilir hello Service Fabric paketleme aracı kullanır [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="35897-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="35897-117">Paketleme hello Node.js uygulaması</span><span class="sxs-lookup"><span data-stu-id="35897-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="35897-118">Bu makale, Node.js hello Service Fabric kümesindeki hello düğümlerinde yüklü olmadığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="35897-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="35897-119">Sonuç olarak tooadd Node.exe toohello kök dizini paketleme önce düğüm uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="35897-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="35897-120">Merhaba dizin yapısını (Express web çerçevesi ve Jade şablon motoru kullanarak) Merhaba Node.js uygulaması, aşağıdaki benzer toohello bir görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="35897-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="35897-121">Bir sonraki adım hello Node.js uygulaması için uygulama paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="35897-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="35897-122">Aşağıdaki Hello kodu Merhaba Node.js uygulaması içeren bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35897-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="35897-123">Kullanılmakta olan hello parametreleri açıklamasını aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="35897-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="35897-124">**/ source** paketlenmesi Merhaba uygulaması noktaları toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="35897-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="35897-125">**/ target** hangi hello paket oluşturulmalıdır hello dizin tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35897-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="35897-126">Bu dizin toobe hello kaynak dizinden farklı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="35897-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="35897-127">**Appname** hello uygulama hello var olan uygulamanın adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35897-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="35897-128">Bu hello bildiriminde toohello hizmet adı ve değil toohello Service Fabric uygulaması adı dönüşür önemli toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="35897-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="35897-129">**/ exe** hello Service Fabric toolaunch, bu durumda beklenir yürütülebilir tanımlar `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="35897-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="35897-130">**/ma** kullanılan toolaunch hello yürütülebilir yüklenmekte olan hello bağımsız değişken tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35897-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="35897-131">Node.js yüklenmemiş gibi Service Fabric toolaunch hello Node.js web sunucusu yürüterek gereken `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="35897-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="35897-132">`/ma:'bin/www'`Merhaba paketleme aracı toouse söyler `bin/ma` node.exe hello bağımsız değişken olarak.</span><span class="sxs-lookup"><span data-stu-id="35897-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="35897-133">**/ Uygulama türü** hello Service Fabric uygulaması türü adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="35897-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="35897-134">Merhaba/target parametresinde belirtilen toohello dizin göz atarsanız, aşağıda gösterildiği gibi hello aracı tam olarak işlevsel bir Service Fabric paketi oluşturdu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="35897-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="35897-135">Merhaba oluşturulan ServiceManifest.xml artık hello aşağıdaki kod parçacığında gösterildiği gibi nasıl hello Node.js web sunucusu başlatılması gerekir, açıklayan bir bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="35897-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="35897-136">Tooupdate hello uç nokta bilgileri aşağıda gösterildiği gibi hello ServiceManifest.xml dosyasında gerekir böylece bu örnekte, 3000, tooport hello Node.js web sunucusu dinler.</span><span class="sxs-lookup"><span data-stu-id="35897-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="35897-137">Paketleme hello MongoDB uygulama</span><span class="sxs-lookup"><span data-stu-id="35897-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="35897-138">Merhaba Node.js uygulaması paketlenmiş, devam edin ve MongoDB paket.</span><span class="sxs-lookup"><span data-stu-id="35897-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="35897-139">Önceden belirtildiği gibi şimdi geçtikleri hello adımları belirli tooNode.js ve MongoDB olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="35897-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="35897-140">Aslında, bunlar bir Service Fabric uygulaması olarak arada paketlenmiş toobe yöneliktir tooall uygulamalar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="35897-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="35897-141">toopackage MongoDB, toomake Mongod.exe ve Mongo.exe paketi emin istiyor.</span><span class="sxs-lookup"><span data-stu-id="35897-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="35897-142">Her iki ikili dosyaları hello bulunur `bin` , MongoDB yükleme dizininin dizin.</span><span class="sxs-lookup"><span data-stu-id="35897-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="35897-143">Merhaba dizin yapısına benzer toohello biri aşağıda arar.</span><span class="sxs-lookup"><span data-stu-id="35897-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="35897-144">Service Fabric gereken bir komut benzer toohello biri ile toostart MongoDB aşağıdaki toouse hello gereken şekilde `/ma` MongoDB paketleme, parametre.</span><span class="sxs-lookup"><span data-stu-id="35897-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="35897-145">Merhaba düğümünün hello yerel dizin hello MongoDB veri dizini yerleştirirseniz hello veriler bir düğüm hatası hello durumda korunmaz.</span><span class="sxs-lookup"><span data-stu-id="35897-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="35897-146">Dayanıklı depolama kullanabilir veya bir MongoDB çoğaltma sırası tooprevent veri kaybına kümesi uygulamak.</span><span class="sxs-lookup"><span data-stu-id="35897-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="35897-147">PowerShell veya hello komut kabuğunda biz şu parametreler hello ile Merhaba paketleme aracını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="35897-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="35897-148">Sipariş tooadd MongoDB tooyour Service Fabric uygulama paketinde, toomake o hello/target parametresi toohello işaret ettiğinden emin gereksinim duyduğunuz zaten hello uygulama bildirimini Merhaba Node.js uygulaması ile birlikte içeren aynı dizini.</span><span class="sxs-lookup"><span data-stu-id="35897-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="35897-149">Toomake kullanmakta olduğunuz emin etmeniz aynı ApplicationType adı hello.</span><span class="sxs-lookup"><span data-stu-id="35897-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="35897-150">Şimdi toohello dizinine göz atın ve incelemek hangi hello aracı oluşturdu.</span><span class="sxs-lookup"><span data-stu-id="35897-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="35897-151">Gördüğünüz gibi hello aracı hello MongoDB ikili dosyaları içeren yeni bir klasör, MongoDB, toohello dizin eklendi.</span><span class="sxs-lookup"><span data-stu-id="35897-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="35897-152">Merhaba açarsanız `ApplicationManifest.xml` dosya, o hello şimdi pakette Merhaba Node.js uygulaması ve MongoDB görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35897-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="35897-153">Aşağıdaki Hello kodu hello hello uygulama bildiriminin içerik gösterir.</span><span class="sxs-lookup"><span data-stu-id="35897-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="35897-154">Yayımlama hello uygulama</span><span class="sxs-lookup"><span data-stu-id="35897-154">Publishing hello application</span></span>
<span data-ttu-id="35897-155">Merhaba son toopublish hello uygulama toohello yerel Service Fabric kümesi hello PowerShell betikleri kullanılarak adımdır:</span><span class="sxs-lookup"><span data-stu-id="35897-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="35897-156">Merhaba uygulaması başarıyla yayımlanan toohello yerel kümeye eklendiğinde, Merhaba Node.js uygulaması hello hizmet bildiriminde Merhaba Node.js uygulaması--örneğin http://localhost: 3000 girmiş olduğunuz hello bağlantı noktasında erişebilir.</span><span class="sxs-lookup"><span data-stu-id="35897-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="35897-157">Bu öğreticide, nasıl tooeasily paketini iki varolan uygulamaları bir Service Fabric uygulaması olarak gördünüz.</span><span class="sxs-lookup"><span data-stu-id="35897-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="35897-158">Ayrıca öğrendiniz nasıl toodeploy, tooService şekilde hello bazıları yüksek kullanılabilirlik ve sistem durumu sistem tümleştirme gibi Service Fabric özellikleri korumasından yararlanabilmek için doku.</span><span class="sxs-lookup"><span data-stu-id="35897-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="35897-159">Yeoman Linux'ta kullanarak daha fazla Konuk yürütülebilir dosyalar tooan varolan uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="35897-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="35897-160">tooadd başka bir hizmet tooan uygulaması zaten kullanılarak oluşturulan `yo`, hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="35897-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="35897-161">Merhaba var olan uygulamanın toohello kök dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="35897-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="35897-162">Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="35897-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="35897-163">Çalıştırma `yo azuresfguest:AddService` ve hello gerekli ayrıntıları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="35897-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35897-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35897-164">Next steps</span></span>
* <span data-ttu-id="35897-165">İle kapsayıcıları dağıtma hakkında bilgi edinin [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="35897-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="35897-166">Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek</span><span class="sxs-lookup"><span data-stu-id="35897-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="35897-167">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="35897-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
