---
title: "MongoDB kullanan bir Node.js uygulaması dağıtma | Microsoft Docs"
description: "Bir Azure Service Fabric kümesi dağıtmak için birden çok Konuk yürütülebilir dosyalar paketini konusunda gözden geçirme"
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
ms.openlocfilehash: b71723034e5f663986c49481072bfd6779d3d57b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="0eca1-103">Konuk tarafından yürütülebilir birden çok uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="0eca1-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="0eca1-104">Bu makalede, paket ve birden çok Konuk yürütülebilir dosyalar için Azure Service Fabric dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-104">This article shows how to package and deploy multiple guest executables to Azure Service Fabric.</span></span> <span data-ttu-id="0eca1-105">Derleme ve tek bir Service Fabric paketi dağıtmak için okuma nasıl için [yürütülebilir Konuk dağıtmak için Service Fabric](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0eca1-105">For building and deploying a single Service Fabric package read how to [deploy a guest executable to Service Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="0eca1-106">Bu kılavuz, MongoDB veri deposu olarak kullanan bir Node.js ön ucuna sahip bir uygulamanın nasıl dağıtılacağı gösterilmektedir, ancak başka bir uygulama üzerinde bağımlılıklara sahip herhangi bir uygulama adımları uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-106">While this walkthrough shows how to deploy an application with a Node.js front end that uses MongoDB as the data store, you can apply the steps to any application that has dependencies on another application.</span></span>   

<span data-ttu-id="0eca1-107">Birden çok Konuk yürütülebilir dosyaları içeren uygulama paketini oluşturmak için Visual Studio'yu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-107">You can use Visual Studio to produce the application package that contains multiple guest executables.</span></span> <span data-ttu-id="0eca1-108">Bkz: [var olan bir uygulama paketi için Visual Studio'yu kullanarak](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0eca1-108">See [Using Visual Studio to package an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="0eca1-109">İlk Konuk yürütülebilir ekledikten sonra uygulama projesine sağ tıklayın ve seçin **Ekle -> Yeni Service Fabric hizmet** ikinci Konuk yürütülebilir proje çözüme eklemek için.</span><span class="sxs-lookup"><span data-stu-id="0eca1-109">After you have added the first guest executable, right click on the application project and select the **Add->New Service Fabric service** to add the second guest executable project to the solution.</span></span> <span data-ttu-id="0eca1-110">Not: Visual Studio projesini kaynak bağlamayı seçerseniz, Visual Studio çözümü oluşturma uygulama paketinizi kaynağındaki değişikliklerle güncel olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0eca1-110">Note: If you choose to link the source in the Visual Studio project, building the Visual Studio solution, will make sure that your application package is up to date with changes in the source.</span></span> 

## <a name="samples"></a><span data-ttu-id="0eca1-111">Örnekler</span><span class="sxs-lookup"><span data-stu-id="0eca1-111">Samples</span></span>
* [<span data-ttu-id="0eca1-112">Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek</span><span class="sxs-lookup"><span data-stu-id="0eca1-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0eca1-113">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="0eca1-113">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-the-multiple-guest-executable-application"></a><span data-ttu-id="0eca1-114">El ile birden çok Konuk yürütülebilir uygulama paketi</span><span class="sxs-lookup"><span data-stu-id="0eca1-114">Manually package the multiple guest executable application</span></span>
<span data-ttu-id="0eca1-115">Bunun yerine el ile yürütülebilir Konuk paketleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-115">Alternatively you can manually package the guest executable.</span></span> <span data-ttu-id="0eca1-116">El ile paketleme için bu makalede şu adresten edinilebilir Service Fabric paketleme aracı kullanan [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="0eca1-116">For the manual packaging, this article uses the Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-the-nodejs-application"></a><span data-ttu-id="0eca1-117">Node.js Uygulama paketleme</span><span class="sxs-lookup"><span data-stu-id="0eca1-117">Packaging the Node.js application</span></span>
<span data-ttu-id="0eca1-118">Bu makale, Node.js Service Fabric kümesindeki düğümlere yüklü olmadığını varsayar.</span><span class="sxs-lookup"><span data-stu-id="0eca1-118">This article assumes that Node.js is not installed on the nodes in the Service Fabric cluster.</span></span> <span data-ttu-id="0eca1-119">Sonuç olarak paketlemeden önce düğüm uygulamanızın kök dizinine Node.exe eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-119">As a consequence, you need to add Node.exe to the root directory of your node application before packaging.</span></span> <span data-ttu-id="0eca1-120">(Express web çerçevesi ve Jade şablon motoru kullanarak) Node.js uygulaması dizin yapısını birine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="0eca1-120">The directory structure of the Node.js application (using Express web framework and Jade template engine) should look similar to the one below:</span></span>

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

<span data-ttu-id="0eca1-121">Sonraki adım olarak, Node.js uygulaması için uygulama paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0eca1-121">As a next step, you create an application package for the Node.js application.</span></span> <span data-ttu-id="0eca1-122">Aşağıdaki kodu Node.js uygulaması içeren bir Service Fabric uygulama paketi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0eca1-122">The code below creates a Service Fabric application package that contains the Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="0eca1-123">Kullanılmakta olan parametreleri açıklamasını aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="0eca1-123">Below is a description of the parameters that are being used:</span></span>

* <span data-ttu-id="0eca1-124">**/ source** paketlenmesi uygulama dizinine işaret eder.</span><span class="sxs-lookup"><span data-stu-id="0eca1-124">**/source** points to the directory of the application that should be packaged.</span></span>
* <span data-ttu-id="0eca1-125">**/ target** içinde paket oluşturulmalıdır dizin tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0eca1-125">**/target** defines the directory in which the package should be created.</span></span> <span data-ttu-id="0eca1-126">Bu dizin kaynak dizinden farklı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-126">This directory has to be different from the source directory.</span></span>
* <span data-ttu-id="0eca1-127">**Appname** var olan uygulamaya uygulama adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0eca1-127">**/appname** defines the application name of the existing application.</span></span> <span data-ttu-id="0eca1-128">Bu hizmet adı bildiriminde ve değil Service Fabric uygulama adı dönüşür anlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-128">It's important to understand that this translates to the service name in the manifest, and not to the Service Fabric application name.</span></span>
* <span data-ttu-id="0eca1-129">**/ exe** Service Fabric başlatın, bu durumda olması yürütülebilir tanımlar `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="0eca1-129">**/exe** defines the executable that Service Fabric is supposed to launch, in this case `node.exe`.</span></span>
* <span data-ttu-id="0eca1-130">**/ma** yürütülebilir başlatmak için kullanılan bağımsız değişken tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0eca1-130">**/ma** defines the argument that is being used to launch the executable.</span></span> <span data-ttu-id="0eca1-131">Node.js yüklenmemiş gibi Service Fabric yürüterek Node.js web sunucusu başlatmak gereken `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="0eca1-131">As Node.js is not installed, Service Fabric needs to launch the Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="0eca1-132">`/ma:'bin/www'`kullanılacak paketleme aracı söyler `bin/ma` node.exe bağımsız değişkeni olarak.</span><span class="sxs-lookup"><span data-stu-id="0eca1-132">`/ma:'bin/www'` tells the packaging tool to use `bin/ma` as the argument for node.exe.</span></span>
* <span data-ttu-id="0eca1-133">**/ Uygulama türü** Service Fabric uygulaması türü adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0eca1-133">**/AppType** defines the Service Fabric application type name.</span></span>

<span data-ttu-id="0eca1-134">/ Target parametresinde belirtilen dizine göz atarsanız, araç tümüyle işlevsel bir Service Fabric paketi aşağıda gösterildiği gibi oluşturdu görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0eca1-134">If you browse to the directory that was specified in the /target parameter, you can see that the tool has created a fully functioning Service Fabric package as shown below:</span></span>

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
<span data-ttu-id="0eca1-135">Oluşturulan ServiceManifest.xml şimdi nasıl Node.js web sunucusu başlatılması gerekir, aşağıdaki kod parçacığında gösterildiği gibi açıklayan bir bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="0eca1-135">The generated ServiceManifest.xml now has a section that describes how the Node.js web server should be launched, as shown in the code snippet below:</span></span>

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
<span data-ttu-id="0eca1-136">Aşağıda gösterildiği gibi ServiceManifest.xml dosyasında uç nokta bilgileri güncelleştirmek gereken şekilde bu örnekte, bağlantı noktası 3000, Node.js web sunucusu dinler.</span><span class="sxs-lookup"><span data-stu-id="0eca1-136">In this sample, the Node.js web server listens to port 3000, so you need to update the endpoint information in the ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-the-mongodb-application"></a><span data-ttu-id="0eca1-137">MongoDB Uygulama paketleme</span><span class="sxs-lookup"><span data-stu-id="0eca1-137">Packaging the MongoDB application</span></span>
<span data-ttu-id="0eca1-138">Node.js uygulaması paketlenmiş, devam edin ve MongoDB paket.</span><span class="sxs-lookup"><span data-stu-id="0eca1-138">Now that you have packaged the Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="0eca1-139">Önceden belirtildiği gibi şimdi geçtikleri adımlar Node.js ve MongoDB özel değildir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-139">As mentioned before, the steps that you go through now are not specific to Node.js and MongoDB.</span></span> <span data-ttu-id="0eca1-140">Aslında, bir Service Fabric uygulaması olarak birlikte paketlenmesi yönelik tüm uygulamalar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-140">In fact, they apply to all applications that are meant to be packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="0eca1-141">MongoDB paketlemek için Mongod.exe ve Mongo.exe paketi emin olmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-141">To package MongoDB, you want to make sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="0eca1-142">Her iki ikili dosyaları bulunan `bin` , MongoDB yükleme dizininin dizin.</span><span class="sxs-lookup"><span data-stu-id="0eca1-142">Both binaries are located in the `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="0eca1-143">Dizin yapısı birine benzer.</span><span class="sxs-lookup"><span data-stu-id="0eca1-143">The directory structure looks similar to the one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="0eca1-144">Service Fabric gereken MongoDB, benzer bir komutla aşağıdaki başlatmak kullanmanız gereken şekilde `/ma` MongoDB paketleme, parametre.</span><span class="sxs-lookup"><span data-stu-id="0eca1-144">Service Fabric needs to start MongoDB with a command similar to the one below, so you need to use the `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path to data]
```
> [!NOTE]
> <span data-ttu-id="0eca1-145">Düğümün yerel dizin MongoDB veri dizini yerleştirirseniz veriler bir düğümü hatasına karşı korunmaz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-145">The data is not being preserved in the case of a node failure if you put the MongoDB data directory on the local directory of the node.</span></span> <span data-ttu-id="0eca1-146">Dayanıklı depolama kullanabilir veya veri kaybını önlemek için ayarlanmış bir MongoDB çoğaltma uygulamak.</span><span class="sxs-lookup"><span data-stu-id="0eca1-146">You should either use durable storage or implement a MongoDB replica set in order to prevent data loss.</span></span>  
>
>

<span data-ttu-id="0eca1-147">PowerShell ya da komut kabuğunu biz paketleme aracını aşağıdaki parametrelerle çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0eca1-147">In PowerShell or the command shell, we run the packaging tool with the following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path to data]' /AppType:NodeAppType
```

<span data-ttu-id="0eca1-148">Service Fabric uygulama paketinizi MongoDB eklemek için uygulama zaten var. aynı dizine/target parametresi noktaları yanı sıra Node.js uygulama bildirimi emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-148">In order to add MongoDB to your Service Fabric application package, you need to make sure that the /target parameter points to the same directory that already contains the application manifest along with the Node.js application.</span></span> <span data-ttu-id="0eca1-149">Ayrıca aynı ApplicationType adı kullandığınızdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-149">You also need to make sure that you are using the same ApplicationType name.</span></span>

<span data-ttu-id="0eca1-150">Şirketinizdeki dizine gözatın ve aracı oluşturulmuş inceleyin.</span><span class="sxs-lookup"><span data-stu-id="0eca1-150">Let's browse to the directory and examine what the tool has created.</span></span>

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
<span data-ttu-id="0eca1-151">Gördüğünüz gibi aracı yeni bir klasör, MongoDB, MongoDB ikili dosyaları içeren dizine eklendi.</span><span class="sxs-lookup"><span data-stu-id="0eca1-151">As you can see, the tool added a new folder, MongoDB, to the directory that contains the MongoDB binaries.</span></span> <span data-ttu-id="0eca1-152">Açarsanız `ApplicationManifest.xml` dosya, paket artık Node.js uygulaması ve MongoDB içerdiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-152">If you open the `ApplicationManifest.xml` file, you can see that the package now contains both the Node.js application and MongoDB.</span></span> <span data-ttu-id="0eca1-153">Aşağıdaki kod, uygulama bildirimi içeriğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="0eca1-153">The code below shows the content of the application manifest.</span></span>

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

### <a name="publishing-the-application"></a><span data-ttu-id="0eca1-154">Uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="0eca1-154">Publishing the application</span></span>
<span data-ttu-id="0eca1-155">PowerShell komut dosyalarını kullanarak yerel Service Fabric kümesi için uygulama yayımlamak için son adımdır bakın:</span><span class="sxs-lookup"><span data-stu-id="0eca1-155">The last step is to publish the application to the local Service Fabric cluster by using the PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="0eca1-156">Uygulamayı yerel kümeye başarıyla yayımlandığında, Node.js uygulaması--örneğin http://localhost: 3000 hizmet bildiriminde girmiş olduğunuz bağlantı noktasında Node.js uygulaması erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-156">Once the application is successfully published to the local cluster, you can access the Node.js application on the port that we have entered in the service manifest of the Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="0eca1-157">Bu öğreticide, kolayca bir Service Fabric uygulaması olarak iki uygulamalarınız için nasıl gördünüz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-157">In this tutorial, you have seen how to easily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="0eca1-158">Aynı zamanda yüksek kullanılabilirlik ve sistem durumu sistem tümleştirme gibi Service Fabric özelliklerinden bazıları yararlanabilir böylece Service Fabric dağıtmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0eca1-158">You have also learned how to deploy it to Service Fabric so that it can benefit from some of the Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-to-an-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="0eca1-159">Yeoman Linux'ta kullanarak var olan bir uygulamaya daha fazla Konuk yürütülebilir dosyaları ekleme</span><span class="sxs-lookup"><span data-stu-id="0eca1-159">Adding more guest executables to an existing application using Yeoman on Linux</span></span>

<span data-ttu-id="0eca1-160">`yo` kullanılarak oluşturulmuş bir uygulamaya başka bir hizmet eklemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="0eca1-160">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="0eca1-161">Dizini mevcut uygulamanın kök dizinine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0eca1-161">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="0eca1-162">Örneğin Yeoman tarafından oluşturulan uygulama `MyApplication` ise `cd ~/YeomanSamples/MyApplication` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0eca1-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="0eca1-163">Çalıştırma `yo azuresfguest:AddService` ve gerekli ayrıntıları sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0eca1-163">Run `yo azuresfguest:AddService` and provide the necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0eca1-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0eca1-164">Next steps</span></span>
* <span data-ttu-id="0eca1-165">İle kapsayıcıları dağıtma hakkında bilgi edinin [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0eca1-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="0eca1-166">Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek</span><span class="sxs-lookup"><span data-stu-id="0eca1-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="0eca1-167">İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak Adlandırma Hizmeti örnek</span><span class="sxs-lookup"><span data-stu-id="0eca1-167">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
