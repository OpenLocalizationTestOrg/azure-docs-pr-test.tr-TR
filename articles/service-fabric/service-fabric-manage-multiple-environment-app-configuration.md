---
title: "aaaManage birden çok ortamlarda Service Fabric | Microsoft Docs"
description: "Service Fabric uygulamaları bir makine toothousands makinelerin boyutu aralık kümeleri üzerinde çalıştırılabilir. Bazı durumlarda, uygulamanız bu çeşitli ortamlar için farklı tooconfigure isteyeceksiniz. Bu makalede yer almaktadır nasıl ortamı başına toodefine farklı uygulama parametreleri."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Birden çok ortamlar için uygulama parametreleri yönetme
Herhangi bir yerden bir toomany makinelerin binlerce kullanarak Azure Service Fabric kümeleri oluşturabilirsiniz. Uygulama ikili dosyaları değişiklik yapmadan bu paylaşılabilen çok sayıda ortamlar arasında çalıştırılabilir olsa da, genellikle tooconfigure Merhaba uygulaması farklı makineler için dağıtıyorsunuz hello sayısı bağlı olarak istediğiniz.

Basit bir örnek olarak göz önünde bulundurun `InstanceCount` durumsuz bir hizmet için. Azure uygulamalarını çalıştırırken bu parametre toohello özel "-1 değeri" genellikle tooset istersiniz. Bu yapılandırma, hizmetiniz hello küme (veya bir yerleştirme kısıtlaması ayarlarsanız hello düğüm türü kümedeki her düğüm) kümedeki her düğüm üzerinde çalıştığını sağlar. Birden çok işlem aynı hello üzerinde dinleme olamaz bu yana ancak, bu yapılandırma bir tek makineli küme için uygun değil tek bir makinede uç noktası. Bunun yerine, genellikle ayarladığınız `InstanceCount` çok "1".

## <a name="specifying-environment-specific-parameters"></a>Ortama özgü parametrelerini belirtme
Merhaba çözüm toothis yapılandırma sorunu parametreli varsayılan Hizmetleri ve belirli bir ortam için bu parametre değerlerini doldurun uygulama parametreleri dosyalarını kümesidir. Varsayılan hizmet ve uygulama parametreleri hello uygulamada yapılandırılır ve bildirimleri hizmet. Merhaba hello ServiceManifest.xml ve ApplicationManifest.xml dosyaları için şema tanımı hello Service Fabric SDK ile yüklenir ve çok Araçları*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Varsayılan Hizmetleri
Service Fabric uygulamaları hizmet örnekleri koleksiyonu yapılır. Toocreate için boş bir uygulama mümkündür ve tüm hizmet örnekleri dinamik olarak oluşturmak olsa da, çoğu uygulamayı hello uygulama örneği oluşturulduğunda, her zaman oluşturulması gereken Çekirdek Hizmetleri kümesine sahiptir. Başvurulan tooas "varsayılan Hizmetleri" bunlar. Köşeli parantez içine dahil ortamı başına yapılandırması yer tutucular ile Merhaba uygulama bildiriminde belirtilir:

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Her adlandırılmış parametreleri hello hello uygulama bildiriminin hello parametreleri öğesi içinde tanımlanmış olması gerekir:

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

Daha fazla özel parametre hello olmaması durumunda belirli bir ortam için kullanılan hello değeri toobe Hello DefaultValue özniteliği belirtir.

> [!NOTE]
> Tüm hizmet örneği parametreleri ortamı başına yapılandırması için uygun değildir. Merhaba yukarıdaki örnekte, LowKey hello ve hello bölüm aralığı işlevi hello veri etki alanının değil hello ortamı olduğundan hello hizmetin bölümleme düzeni HighKey değerlerini açıkça hizmetin tüm örneklerine ait hello için tanımlanır.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Ortam başına hizmet yapılandırma ayarları
Merhaba [Service Fabric uygulama modeli](service-fabric-application-model.md) Hizmetleri çalışma zamanında okunabilir özel anahtar-değer çiftleri içeren tooinclude yapılandırma paketlerini etkinleştirir. Bu ayarların Hello değerleri ayrıca Ayrıştırılan ortamı tarafından belirterek bir `ConfigOverride` hello uygulama bildiriminde.

Ayar hello için hello Config\Settings.xml dosyasında aşağıdaki hello olduğunu varsayalım `Stateful1` hizmeti:

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
Bu değer için bir özel uygulama/ortamı çifti toooverride oluşturmak bir `ConfigOverride` hello hizmet bildirimi hello uygulama bildiriminde aktardığınızda.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Bu parametre yukarıda gösterildiği gibi ortamı tarafından sonra yapılandırılabilir. Bunu hello Parametreler bölümünde hello uygulama bildiriminin bildirme ve ortama özgü değerleri hello uygulama parametresi dosyalarında belirterek yapabilirsiniz.

> [!NOTE]
> Hizmet yapılandırma ayarlarını Hello durumda olduğu bir anahtarın değerini hello ayarlanabilir üç yerde vardır: hello hizmeti yapılandırma paketi, hello uygulama bildirimi ve hello uygulama parametre dosyası. Service Fabric her zaman hello uygulama parametre dosyasından ilk (belirtilmişse) seçin, sonra uygulama bildirimi hello ve son olarak yapılandırma paketi hello.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Ayarlama ve ortam değişkenlerini kullanma 
Belirtin ve hello ServiceManifest.xml dosyasında ortam değişkenlerini ayarlama ve daha sonra bu örneği başına temelinde hello ApplicationManifest.xml dosyasında geçersiz.
bir değerle ayarlayın ve hello diğer geçersiz kılınır Hello örnekte iki ortam değişkenleri gösterir. Tooset ortam değişkenleri değerleri hello aynı şekilde, bu yapılandırma geçersiz kılma işlemleri için kullanılan uygulama parametrelerini kullanabilirsiniz.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
Merhaba ApplicationManifest.xml, başvuru hello kod hello ServiceManifest hello ile paketinde toooverride hello ortam değişkenleri `EnvironmentOverrides` öğesi.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Merhaba adlı hizmet örneği oluşturulduktan sonra koddan hello ortam değişkenlerine erişebilir. Örneğin, C# yapabileceğiniz hello aşağıdaki

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Service Fabric ortam değişkenleri
Service Fabric kümesi her hizmet örneği için ortam değişkenleri içindeki oluşturdu. Merhaba ortam değişkenlerinin tam listesi olduğu aşağıda hello olanları kalın olan, hizmetiniz, kullanacağınız olanları hello burada hello diğer olan Service Fabric çalışma zamanı tarafından kullanılır. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_ [YourServiceName] TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Merhaba kod belows nasıl toolist hello Service Fabric ortam değişkenleri gösterir
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Merhaba adlı bir uygulama türü için ortam değişkenleri örnekleri verilmiştir `GuestExe.Application` hizmet türü ile adlı `FrontEndService` yerel geliştirme makinenizde çalıştırdığınızda.

* **Fabric_ApplicationName fabric:/GuestExe.Application =**
* **Fabric_CodePackageName kodu =**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName _Node_2 =**

### <a name="application-parameter-files"></a>Uygulama parametre dosyaları
Merhaba Service Fabric uygulaması projesi bir veya daha fazla uygulama parametreleri dosyalarını içerebilir. Bunların her birini hello belirli değerleri hello uygulama bildiriminde tanımlanan hello parametreleri tanımlar:

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Varsayılan olarak, yeni bir uygulama Local.1Node.xml, Local.5Node.xml ve Cloud.xml adlı üç uygulama parametreleri dosyalarını içerir:

![Çözüm Gezgini'nde uygulama parametre dosyaları][app-parameters-solution-explorer]

toocreate bir parametre dosyası yalnızca kopyalayın ve mevcut bir yapıştırın ve yeni bir ad verin.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Dağıtım sırasında ortama özgü parametreleri tanımlama
Dağıtım sırasında uygulamanızla toochoose hello uygun parametre dosyası tooapply gerekir. Visual Studio'da hello Yayımla iletişim kutusu veya PowerShell aracılığıyla bunu yapabilirsiniz.

### <a name="deploy-from-visual-studio"></a>Visual Studio'dan dağıtma
Visual Studio'da uygulamanız yayımladığınızda hello kullanılabilir parametre dosyalar listesinden seçebilirsiniz.

![Merhaba Yayımla iletişim kutusunda bir parametre dosyası seçin][publishdialog]

### <a name="deploy-from-powershell"></a>Powershell'den dağıtma
Merhaba `Deploy-FabricApplication.ps1` hello uygulama projesi şablona dahil edilen PowerShell betiğini bir yayımlama profili bir parametre olarak kabul eder ve hello PublishProfile bir başvuru toohello uygulama parametreler dosyası içerir.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Sonraki adımlar
Bu konuda, açıklanan hello temel kavramlar bazıları hakkında daha fazla toolearn hello bkz [Service Fabric teknik genel bakış](service-fabric-technical-overview.md). Visual Studio'da kullanılabilir olan diğer uygulama yönetim özellikleri hakkında daha fazla bilgi için bkz: [Visual Studio'da, Service Fabric uygulamaları yönetmek](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
