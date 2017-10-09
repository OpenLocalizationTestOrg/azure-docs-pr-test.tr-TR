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
# <a name="deploy-multiple-guest-executables"></a>Konuk tarafından yürütülebilir birden çok uygulama dağıtma
Bu makalede gösterilmektedir nasıl toopackage ve birden çok Konuk yürütülebilir dosyalar tooAzure Service Fabric dağıtın. Oluşturma ve tek bir Service Fabric paketi dağıtma nasıl çok okumak için[Konuk yürütülebilir tooService doku dağıtmak](service-fabric-deploy-existing-app.md).

Bu kılavuzda nasıl toodeploy MongoDB hello veri deposu olarak kullanan bir Node.js ön ucuna sahip bir uygulama, başka bir uygulama bağımlılıkları olan hello adımları tooany uygulama uygulayabileceğiniz gösterirken.   

Birden çok Konuk yürütülebilir dosyaları içeren Visual Studio tooproduce hello uygulama paketi kullanabilirsiniz. Bkz: [kullanarak Visual Studio toopackage varolan bir uygulama](service-fabric-deploy-existing-app.md). Merhaba ilk Konuk yürütülebilir ekledikten sonra sağ hello uygulama projesi seçin hello tıklayın ve **Ekle -> Yeni Service Fabric hizmet** tooadd hello ikinci Konuk yürütülebilir proje toohello çözüm. Not: hello hello Visual Studio çözümü oluşturma, Visual Studio projesi toolink hello kaynağında, emin olmanızı sağlayacak seçerseniz, uygulama paketinizi hello kaynağındaki değişikliklerle toodate çalışıyor. 

## <a name="samples"></a>Örnekler
* [Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a>El ile paket hello birden çok Konuk yürütülebilir uygulama
Bunun yerine el ile Merhaba Konuk yürütülebilir paketleyebilirsiniz. Hello için el ile paketleme, bu makalede şu adresten edinilebilir hello Service Fabric paketleme aracı kullanır [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).

### <a name="packaging-hello-nodejs-application"></a>Paketleme hello Node.js uygulaması
Bu makale, Node.js hello Service Fabric kümesindeki hello düğümlerinde yüklü olmadığını varsayar. Sonuç olarak tooadd Node.exe toohello kök dizini paketleme önce düğüm uygulamanız gerekir. Merhaba dizin yapısını (Express web çerçevesi ve Jade şablon motoru kullanarak) Merhaba Node.js uygulaması, aşağıdaki benzer toohello bir görünmelidir:

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

Bir sonraki adım hello Node.js uygulaması için uygulama paketi oluşturun. Aşağıdaki Hello kodu Merhaba Node.js uygulaması içeren bir Service Fabric uygulama paketi oluşturur.

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

Kullanılmakta olan hello parametreleri açıklamasını aşağıdadır:

* **/ source** paketlenmesi Merhaba uygulaması noktaları toohello dizini.
* **/ target** hangi hello paket oluşturulmalıdır hello dizin tanımlar. Bu dizin toobe hello kaynak dizinden farklı sahiptir.
* **Appname** hello uygulama hello var olan uygulamanın adını tanımlar. Bu hello bildiriminde toohello hizmet adı ve değil toohello Service Fabric uygulaması adı dönüşür önemli toounderstand olur.
* **/ exe** hello Service Fabric toolaunch, bu durumda beklenir yürütülebilir tanımlar `node.exe`.
* **/ma** kullanılan toolaunch hello yürütülebilir yüklenmekte olan hello bağımsız değişken tanımlar. Node.js yüklenmemiş gibi Service Fabric toolaunch hello Node.js web sunucusu yürüterek gereken `node.exe bin/www`.  `/ma:'bin/www'`Merhaba paketleme aracı toouse söyler `bin/ma` node.exe hello bağımsız değişken olarak.
* **/ Uygulama türü** hello Service Fabric uygulaması türü adını tanımlar.

Merhaba/target parametresinde belirtilen toohello dizin göz atarsanız, aşağıda gösterildiği gibi hello aracı tam olarak işlevsel bir Service Fabric paketi oluşturdu görebilirsiniz:

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
Merhaba oluşturulan ServiceManifest.xml artık hello aşağıdaki kod parçacığında gösterildiği gibi nasıl hello Node.js web sunucusu başlatılması gerekir, açıklayan bir bölümü vardır:

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
Tooupdate hello uç nokta bilgileri aşağıda gösterildiği gibi hello ServiceManifest.xml dosyasında gerekir böylece bu örnekte, 3000, tooport hello Node.js web sunucusu dinler.   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a>Paketleme hello MongoDB uygulama
Merhaba Node.js uygulaması paketlenmiş, devam edin ve MongoDB paket. Önceden belirtildiği gibi şimdi geçtikleri hello adımları belirli tooNode.js ve MongoDB olup olmadığı. Aslında, bunlar bir Service Fabric uygulaması olarak arada paketlenmiş toobe yöneliktir tooall uygulamalar geçerlidir.  

toopackage MongoDB, toomake Mongod.exe ve Mongo.exe paketi emin istiyor. Her iki ikili dosyaları hello bulunur `bin` , MongoDB yükleme dizininin dizin. Merhaba dizin yapısına benzer toohello biri aşağıda arar.

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
Service Fabric gereken bir komut benzer toohello biri ile toostart MongoDB aşağıdaki toouse hello gereken şekilde `/ma` MongoDB paketleme, parametre.

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> Merhaba düğümünün hello yerel dizin hello MongoDB veri dizini yerleştirirseniz hello veriler bir düğüm hatası hello durumda korunmaz. Dayanıklı depolama kullanabilir veya bir MongoDB çoğaltma sırası tooprevent veri kaybına kümesi uygulamak.  
>
>

PowerShell veya hello komut kabuğunda biz şu parametreler hello ile Merhaba paketleme aracını çalıştırın:

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

Sipariş tooadd MongoDB tooyour Service Fabric uygulama paketinde, toomake o hello/target parametresi toohello işaret ettiğinden emin gereksinim duyduğunuz zaten hello uygulama bildirimini Merhaba Node.js uygulaması ile birlikte içeren aynı dizini. Toomake kullanmakta olduğunuz emin etmeniz aynı ApplicationType adı hello.

Şimdi toohello dizinine göz atın ve incelemek hangi hello aracı oluşturdu.

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
Gördüğünüz gibi hello aracı hello MongoDB ikili dosyaları içeren yeni bir klasör, MongoDB, toohello dizin eklendi. Merhaba açarsanız `ApplicationManifest.xml` dosya, o hello şimdi pakette Merhaba Node.js uygulaması ve MongoDB görebilirsiniz. Aşağıdaki Hello kodu hello hello uygulama bildiriminin içerik gösterir.

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

### <a name="publishing-hello-application"></a>Yayımlama hello uygulama
Merhaba son toopublish hello uygulama toohello yerel Service Fabric kümesi hello PowerShell betikleri kullanılarak adımdır:

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

Merhaba uygulaması başarıyla yayımlanan toohello yerel kümeye eklendiğinde, Merhaba Node.js uygulaması hello hizmet bildiriminde Merhaba Node.js uygulaması--örneğin http://localhost: 3000 girmiş olduğunuz hello bağlantı noktasında erişebilir.

Bu öğreticide, nasıl tooeasily paketini iki varolan uygulamaları bir Service Fabric uygulaması olarak gördünüz. Ayrıca öğrendiniz nasıl toodeploy, tooService şekilde hello bazıları yüksek kullanılabilirlik ve sistem durumu sistem tümleştirme gibi Service Fabric özellikleri korumasından yararlanabilmek için doku.


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a>Yeoman Linux'ta kullanarak daha fazla Konuk yürütülebilir dosyalar tooan varolan uygulama ekleme

tooadd başka bir hizmet tooan uygulaması zaten kullanılarak oluşturulan `yo`, hello aşağıdaki adımları gerçekleştirin: 
1. Merhaba var olan uygulamanın toohello kök dizini değiştirin.  Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.
2. Çalıştırma `yo azuresfguest:AddService` ve hello gerekli ayrıntıları sağlayın.

## <a name="next-steps"></a>Sonraki adımlar
* İle kapsayıcıları dağıtma hakkında bilgi edinin [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)
* [Paketleme ve dağıtma bir konuk yürütülebilir dosyası için örnek](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [İki Konuk yürütülebilir dosyalar (C# ve nodejs) iletişim REST kullanarak hello Adlandırma Hizmeti örnek](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
