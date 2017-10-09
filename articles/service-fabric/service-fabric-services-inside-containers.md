---
title: "aaaHow toocontainerize, Azure Service Fabric mikro (Önizleme)"
description: "Azure Service Fabric yeni işlevsellik toocontainerize Service Fabric mikro ekledi. Bu özellik şu anda önizleme sürümündedir."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: anmolah
editor: anmolah
ms.assetid: 0b41efb3-4063-4600-89f5-b077ea81fa3a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/04/2017
ms.author: anmola
ms.openlocfilehash: 6edaff73c0828707c7fa736669ba8084663d31ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontainerize-your-service-fabric-reliable-services-and-reliable-actors-preview"></a>Nasıl toocontainerize Service Fabric güvenilir Services ve Reliable Actors (Önizleme)

Service Fabric containerizing Service Fabric mikro (Reliable Services ve güvenilir dayalı aktör Hizmetleri) destekler. Daha fazla bilgi için bkz: [service fabric kapsayıcıları](service-fabric-containers-overview.md).


 Bu özellik Önizleme sürümünde olduğu ve bu makalede, bir kapsayıcı içinde çalışan hizmetinizi çeşitli adımları tooget hello sağlanmaktadır.  

> [!NOTE]
> Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor. Şu anda bu özellik yalnızca Windows için çalışır.

## <a name="steps-toocontainerize-your-service-fabric-application"></a>Service Fabric uygulamanızı toocontainerize adımları

1. Service Fabric uygulamanızı Visual Studio'da açın.

2. Sınıf ekleme [SFBinaryLoader.cs](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/code/SFBinaryLoaderForContainers/SFBinaryLoader.cs) tooyour projesi. Merhaba bu sınıftaki bir yardımcı toocorrectly yük hello Service Fabric çalışma zamanı ikili dosyaları, uygulamanızın içinde bir kapsayıcı içinde çalışırken kodudur.

3. Her kod paketi için toocontainerize, başlatma hello yükleyicisi hello program Giriş noktasına ister. Aşağıdaki kod parçacığını tooyour program giriş noktası dosyasına hello gösterilen hello statik oluşturucu ekleyin.

  ```csharp
  namespace MyApplication
  {
      internal static class Program
      {
          static Program()
          {
              SFBinaryLoader.Initialize();
          }

          /// <summary>
          /// This is hello entry point of hello service host process.
          /// </summary>
          private static void Main()
          {
  ```

4. Derleme ve [paket](service-fabric-package-apps.md#Package-App) projenizi. toobuild ve bir paket oluşturun, Çözüm Gezgini'nde hello uygulama projesine sağ tıklayın ve hello seçin **paket** komutu.

5. Her kod paketi için ihtiyacınız toocontainerize, PowerShell Betiği çalıştırma hello [CreateDockerPackage.ps1](https://github.com/Azure/service-fabric-scripts-and-templates/blob/master/scripts/CodePackageToDockerPackage/CreateDockerPackage.ps1). Merhaba kullanım aşağıdaki gibidir:
  ```powershell
    $codePackagePath = 'Path toohello code package toocontainerize.'
    $dockerPackageOutputDirectoryPath = 'Output path for hello generated docker folder.'
    $applicationExeName = 'Name of hello ode package executable.'
    CreateDockerPackage.ps1 -CodePackageDirectoryPath $codePackagePath -DockerPackageOutputDirectoryPath $dockerPackageOutputDirectoryPath -ApplicationExeName $applicationExeName
 ```
  Hello betik $dockerPackageOutputDirectoryPath adresindeki Docker yapıları içeren bir klasör oluşturur. Oluşturulan hello Dockerfile tooexpose Kurulum betikleri gereksinimlerinize göre vb. çalıştıran herhangi bir bağlantı değiştirin.

6. Sonraki çok ihtiyacınız[yapı](service-fabric-get-started-containers.md#Build-Containers) ve [itme](service-fabric-get-started-containers.md#Push-Containers) , Docker kapsayıcısı paket tooyour deposu.

7. Merhaba ApplicationManifest.xml ve ServiceManifest.xml tooadd kapsayıcı görüntü, havuz bilgileri, kayıt defteri kimlik doğrulaması ve bağlantı noktası ana bilgisayar eşleme değiştirin. Merhaba bildirimleri değiştirmek için bkz: [Azure Service Fabric kapsayıcı uygulama oluşturma](service-fabric-get-started-containers.md). Merhaba kod paketi tanımında hello hizmet bildirimi gereksinimlerini toobe karşılık gelen kapsayıcı görüntü ile değiştirilir. Emin toochange hello EntryPoint tooa ContainerHost türü olun.

  ```xml
<!-- Code package is your service executable. -->
<CodePackage Name="Code" Version="1.0.0">
  <EntryPoint>
    <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
    <ContainerHost>
      <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
    </ContainerHost>
  </EntryPoint>
  <!-- Pass environment variables tooyour container: -->    
</CodePackage>
  ```

8. Çoğaltıcı ve hizmet uç noktası başlangıç bağlantı noktası ana bilgisayar eşlemesi ekleyin. Her iki, bu bağlantı noktalarına çalışma zamanında Service Fabric tarafından atanmış olduğundan, bağlantı noktası eşlemesi için atanmış toozero toouse hello hello ContainerPort ayarlanır.

 ```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="0" EndpointRef="ServiceEndpoint"/>
    <PortBinding ContainerPort="0" EndpointRef="ReplicatorEndpoint"/>
  </ContainerHostPolicies>
</Policies>
 ```

9. tootest bu uygulama toodeploy gerekir, 5.7 veya daha yüksek sürümünü çalıştıran tooa küme. Ayrıca, tooedit gerekir ve bu önizleme özelliği hello küme ayarları tooenable güncelleştirin. Bu başlangıç adımları [makale](service-fabric-cluster-fabric-settings.md) sonraki gösterilen tooadd hello ayarı.
```
      {
        "name": "Hosting",
        "parameters": [
          {
            "name": "FabricContainerAppsEnabled",
            "value": "true"
          }
        ]
      }
```
10. Sonraki [dağıtmak](service-fabric-deploy-remove-applications.md) hello uygulama paketi toothis küme düzenlenemez.

Şimdi, küme çalışmayı kapsayıcılı Service Fabric uygulaması olmalıdır.

## <a name="next-steps"></a>Sonraki adımlar
* [Service Fabric’te kapsayıcı](service-fabric-get-started-containers.md) çalıştırma hakkında daha fazla bilgi edinin.
* Service Fabric Hello hakkında bilgi edinin [uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).
