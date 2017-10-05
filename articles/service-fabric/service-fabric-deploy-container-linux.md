---
title: "Service Fabric ve Linux dağıtma kapsayıcılarında | Microsoft Docs"
description: "Service Fabric ve Linux kapsayıcıları kullanımını mikro hizmet uygulamalarını dağıtmak için. Bu makalede kapsayıcıları için Service Fabric sağlayan özellikleri ve bir küme içinde Linux kapsayıcı görüntü dağıtma"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a>Service Fabric Linux kapsayıcı dağıtma
> [!div class="op_single_selector"]
> * [Windows kapsayıcı dağıtma](service-fabric-deploy-container.md)
> * [Linux kapsayıcı dağıtma](service-fabric-deploy-container-linux.md)
>
>

Bu makalede Linux'ta Docker kapsayıcılarında kapsayıcılı hizmetleri oluşturma sürecinde anlatılmaktadır.

Service Fabric oluşan kapsayıcılı, mikro uygulamaları oluşturmaya yardımcı birkaç kapsayıcı özellikleri vardır. Bu hizmetler kapsayıcılı Hizmetleri olarak adlandırılır.

Yetenekler içerir;

* Kapsayıcı görüntü dağıtımı ve etkinleştirme
* Kaynak İdaresi
* Depo kimlik doğrulaması
* Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme
* Kapsayıcıya bulma ve iletişim
* Yapılandırma ve ortam değişkenlerini ayarlama özelliği

## <a name="packaging-a-docker-container-with-yeoman"></a>Docker kapsayıcısı ile yeoman paketleme
Linux üzerinde bir kapsayıcı paketleme, yeoman şablon kullanılacağını seçebilirsiniz veya [uygulama paketini el ile oluşturmak](#manually).

Service Fabric uygulaması her uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla kapsayıcıları içerebilir. Linux için Service Fabric SDK’sı uygulamanızı oluşturmayı ve kapsayıcı görüntüsü eklemeyi kolaylaştıran bir [Yeoman](http://yeoman.io/) oluşturucu içerir. Şimdi Yeoman kullanarak *SimpleContainerApp* adlı tek bir Docker kapsayıcısı olan bir uygulama oluşturalım. Daha fazla hizmet daha sonra oluşturulan düzenleyerek dosyaları bildirim ekleyebilirsiniz.

## <a name="install-docker-on-your-development-box"></a>Docker geliştirme kutunuzun yükleyin

Linux geliştirme kutusundaki docker yüklemek için aşağıdaki komutları çalıştırın (OSX üzerinde vagrant görüntüsü kullanıyorsanız, docker zaten yüklü):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a>Uygulama oluşturma
1. Bir terminal penceresinde `yo azuresfcontainer` yazın.
2. Örneğin, mycontainerap uygulamanızın - adı
3. DockerHub depodaki kapsayıcı görüntüden için URL'sini sağlayın. Görüntü parametresi [repo] biçimini alır / [görüntü adı]
4. Görüntüyü yeniden başlatma işleminden sonra çalışan kapsayıcı tutar kapsayıcı içinde çalıştırılacak komutları virgülle ayrılmış bir dizi giriş komutları açıkça belirtmek gerekiyor bir iş yükü giriş tanımlanmış noktası yoksa.

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="deploy-the-application"></a>Uygulamayı dağıtma

### <a name="using-xplat-cli"></a>XPlat CLI aracını kullanma
Uygulama oluşturulduktan sonra Azure CLI kullanarak yerel kümeye dağıtabilirsiniz.

1. Yerel Service Fabric kümesine bağlanın.

    ```bash
    azure servicefabric cluster connect
    ```

2. Uygulama paketini kümenin görüntü deposuna kopyalamak, uygulama türünü kaydetmek ve uygulamanın bir örneğini oluşturmak için şablonda verilen yükleme betiğini kullanın.

    ```bash
    ./install.sh
    ```

3. Bir tarayıcı açın ve http://localhost:19080/Explorer adresindeki Service Fabric Explorer’a gidin (Vagrant’ı Mac OS X üzerinde kullanıyorsanız localhost ifadesini sanal makinenin özel IP’si ile değiştirin).
4. Uygulamalar düğümünü genişletin ve şu anda uygulamanızın türü için bir giriş ve bu türün ilk örneği için başka bir giriş olduğuna dikkat edin.
5. Uygulama örneğini silin ve uygulama türü kaydını kaldırma için şablonda belirtilen kaldırma komut dosyası kullanın.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Azure CLI 2.0 aracını kullanma

Başvuru belge yönetme hakkında bkz bir [Azure CLI 2.0 kullanan uygulama yaşam döngüsü](service-fabric-application-lifecycle-azure-cli-2-0.md).

Örnek bir uygulama için [checkout Service Fabric kapsayıcı kodu Github'da örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-to-an-existing-application"></a>Mevcut bir uygulamaya daha fazla hizmet ekleme

Başka bir kapsayıcı hizmeti zaten kullanılarak oluşturulmuş bir uygulama eklemek için `yo`, aşağıdaki adımları gerçekleştirin:

1. Dizini mevcut uygulamanın kök dizinine değiştirin.  Örneğin Yeoman tarafından oluşturulan uygulama `MyApplication` ise `cd ~/YeomanSamples/MyApplication` olacaktır.
2. `yo azuresfcontainer:AddService` öğesini çalıştırın

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>El ile paketini ve kapsayıcı görüntüsünü Dağıt
El ile kapsayıcılı hizmet paketleme işlemi aşağıdaki adımları dayanır:

1. Kapsayıcılar deponuza yayımlayın.
2. Paket dizin yapısını oluşturun.
3. Hizmet bildirim dosyasını düzenleyin.
4. Uygulama bildirim dosyasının düzenleyin.

## <a name="deploy-and-activate-a-container-image"></a>Dağıtma ve kapsayıcı görüntü etkinleştirin
Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder. Dağıtma ve bir kapsayıcı etkinleştirmek için kapsayıcı görüntüsüne adını put bir `ContainerHost` hizmet bildiriminde öğesi.

Hizmet bildiriminde eklemek bir `ContainerHost` giriş noktası için. Ardından `ImageName` kapsayıcı depo ve görüntü adı olmalıdır. Aşağıdaki kısmi bildirimi adlı kapsayıcıyı dağıtmak nasıl bir örneği gösterir `myimage:v1` adlı bir depodan `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

İsteğe bağlı belirterek giriş komutları sağlayabilir `Commands` öğe kapsayıcısı içindeki çalıştırılacak komutları virgülle ayrılmış bir dizi.

> [!NOTE]
> Görüntünün bir iş yükü giriş tanımlanmış noktası yok sonra içindeki giriş komutları açıkça belirtmek zorunda `Commands` başlatma işleminden sonra çalışan kapsayıcı tutar kapsayıcı içinde çalıştırılacak komutları virgülle ayrılmış bir dizi öğesi.

## <a name="understand-resource-governance"></a>Kaynak İdaresi anlama
Kaynak İdaresi kapsayıcı konakta kullanabilirsiniz kaynakları kısıtlayan kapsayıcısının bir yetenektir. `ResourceGovernancePolicy`, Bir hizmet kod paketi için kaynak sınırları bildirmek için hangi uygulama bildiriminde belirtilen kullanılır. Aşağıdaki kaynaklar için kaynak sınırlarını ayarlayabilirsiniz:

* Bellek
* MemorySwap
* CpuShares (CPU göreli ağırlık)
* MemoryReservationInMB  
* BlkioWeight (BlockIO göreli ağırlık).

> [!NOTE]
> Gelecekteki bir sürümde, IOPS gibi belirli blok g/ç sınırları belirtmek için destek BPS okuma/yazma ve diğerleri dahil edilir.
>
>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Bir depo kimlik doğrulaması
Bir kapsayıcı indirmek için kapsayıcı deponuza oturum açma kimlik bilgilerini sağlamanız gerekebilir. Uygulama bildiriminde belirtilen oturum açma kimlik bilgileri, oturum açma bilgileri veya kapsayıcı görüntünün görüntü deposundan karşıdan yüklemek için SSH anahtarı belirtmek için kullanılır. Adlı bir hesap aşağıdaki örnekte *TestUser* düz metin parolayı birlikte (*değil* önerilen):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Makineye dağıtılan bir sertifika kullanarak parolayı şifrelemek öneririz.

Adlı bir hesap aşağıdaki örnekte *TestUser*, adı verilen bir sertifikayı kullanarak parolayı nerede şifrelenmiş *MyCert*. Kullanabileceğiniz `Invoke-ServiceFabricEncryptText` gizli şifreli metin parolası oluşturmak için PowerShell komutu. Daha fazla bilgi için bkz: [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).

Parola şifresini çözmek için kullanılan sertifikanın özel anahtarı yerel makinede bir bant dışı yöntem dağıtılması gerekir. (Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric makineye hizmet paketini dağıtırken, gizli şifresini çözebilir. Gizli hesap adı ile birlikte kullanarak, bu kapsayıcı deposuyla sonra doğrulayabilir.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a>Kapsayıcı bağlantı noktası ana bilgisayar bağlantı noktası eşleme yapılandırın
Belirterek kapsayıcı ile iletişim kurmak için kullanılan bir ana bilgisayar bağlantı noktası yapılandırabilirsiniz bir `PortBinding` uygulama bildiriminde. Hizmet bağlantı noktası ana bilgisayardaki kapsayıcıya içinde dinleme yaptığı bağlantı bağlantı noktası bağlamasına eşler.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Kapsayıcıya bulma ve iletişim yapılandırın
Kullanarak `PortBinding` İlkesi, bir kapsayıcı bağlantı noktasına eşlenebilir bir `Endpoint` hizmet bildiriminde. Uç nokta `Endpoint1` sabit bir bağlantı noktası (örneğin, bağlantı noktası 80) belirtebilirsiniz. Kümenin uygulama bağlantı noktası aralığından rastgele bir bağlantı noktası sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.

Bir uç nokta belirtirseniz, kullanarak `Endpoint` Konuk kapsayıcı, Service Fabric hizmet bildirimi etiketinde adlandırma hizmeti bu bitiş noktası otomatik olarak yayımlayabilirsiniz. Kümede çalışan diğer hizmetler, böylece çözümlemek için REST sorgularını kullanarak bu kapsayıcı bulabilir.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Adlandırma Hizmeti ile kaydetme tarafından kolayca kod-kapsayıcıya iletişiminde kapsayıcı içinde kullanarak yapabileceğiniz [ters proxy](service-fabric-reverseproxy.md). İletişim ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak iletişim kurması için istediğiniz hizmetleri adını sağlayarak gerçekleştirilir. Daha fazla bilgi için sonraki bölüme bakın.

## <a name="configure-and-set-environment-variables"></a>Ortam değişkenlerini yapılandırma ve ayarlama
Ortam değişkenleri hizmet bildiriminde hem işlemler/Konuk yürütülebilir dosyaları dağıtılan Hizmetleri veya kapsayıcılarında dağıtılan Hizmetleri için her kod paketi için belirtilebilir. Bu ortam değişkeni değerlerini özellikle uygulama bildiriminde geçersiz veya uygulama parametreleri olarak dağıtım sırasında belirtilen.

Aşağıdaki hizmet bildirimi XML kod parçacığı, kod paketi için ortam değişkenlerinin nasıl belirtileceğini gösteren bir örnektir:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Bu ortam değişkenleri uygulama bildirim düzeyinde geçersiz kılınabilir:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Önceki örnekte, biz açık bir değer için belirtilen `HttpGateway` ortam değişkeni (19000), değeri ayarlarız sırada `BackendServiceName` parametresi ile `[BackendSvc]` uygulama parametresi. Bu ayarları için değer belirtmenizi sağlayan `BackendServiceName`değer uygulamayı dağıttıktan sonra bildiriminde sabit bir değere sahip değil.

## <a name="complete-examples-for-application-and-service-manifest"></a>Uygulama ve hizmet bildirimi için örnekler tamamlayın

Bir örnek uygulama bildirimi aşağıdaki gibidir:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Bir örnek hizmet bildirimi (önceki uygulama bildiriminde belirtilen) aşağıdaki gibidir:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Sonraki adımlar
Kapsayıcılı hizmetini dağıttıysanız, kendi ömrü okuyarak yönetmeyi öğrenin [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).

* [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)
* [Azure CLI kullanarak Service Fabric kümeleriyle etkileşim kurma](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>İlgili makaleler

* [Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama](service-fabric-azure-cli-2-0.md)
* [Service Fabric XPlat CLI ile çalışmaya başlama](service-fabric-azure-cli.md)
