---
title: "aaaService doku ve Linux kapsayıcıları dağıtma | Microsoft Docs"
description: "Service Fabric ve hello Linux kapsayıcıları toodeploy mikro hizmet uygulamaları kullanın. Bu makalede kapsayıcıları ve nasıl toodeploy Linux kapsayıcı görüntü bir kümede Service Fabric sağlar hello özellikleri"
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
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Linux kapsayıcı tooService doku dağıtma
> [!div class="op_single_selector"]
> * [Windows kapsayıcı dağıtma](service-fabric-deploy-container.md)
> * [Linux kapsayıcı dağıtma](service-fabric-deploy-container-linux.md)
>
>

Bu makalede Linux'ta Docker kapsayıcılarında kapsayıcılı hizmetleri oluşturma sürecinde anlatılmaktadır.

Service Fabric oluşan kapsayıcılı, mikro uygulamaları oluşturmaya yardımcı birkaç kapsayıcı özellikleri vardır. Bu hizmetler kapsayıcılı Hizmetleri olarak adlandırılır.

Merhaba yeteneklere;

* Kapsayıcı görüntü dağıtımı ve etkinleştirme
* Kaynak İdaresi
* Depo kimlik doğrulaması
* Kapsayıcı bağlantı noktası toohost bağlantı noktası eşleme
* Kapsayıcıya bulma ve iletişim
* Özelliği tooconfigure ve ortam değişkenlerini ayarlama

## <a name="packaging-a-docker-container-with-yeoman"></a>Docker kapsayıcısı ile yeoman paketleme
Linux üzerinde bir kapsayıcı paketleme, ya da toouse yeoman şablonu seçebilirsiniz veya [hello uygulama paketini el ile oluşturmak](#manually).

Service Fabric uygulaması her hello uygulamanın işlevselliğini aktarma konusunda belirli bir rol ile bir veya daha fazla kapsayıcıları içerebilir. Merhaba Linux için Service Fabric SDK içerir bir [Yeoman](http://yeoman.io/) kolay toocreate kolaylaştırır Oluşturucu uygulamanız ve kapsayıcı görüntü ekleyin. Yeoman tek bir Docker kapsayıcısı uygulamayla adlı toocreate kullanalım *SimpleContainerApp*. Oluşturulan hello bildirim dosyalarını düzenleyerek daha fazla hizmet daha sonra ekleyebilirsiniz.

## <a name="install-docker-on-your-development-box"></a>Docker geliştirme kutunuzun yükleyin

Çalışma hello aşağıdaki komutları Linux geliştirme kutunuzda tooinstall docker (OSX üzerinde hello vagrant görüntüsü kullanıyorsanız, docker zaten yüklü):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma
1. Bir terminal penceresinde `yo azuresfcontainer` yazın.
2. Örneğin, mycontainerap uygulamanızın - adı
3. Merhaba kapsayıcı DockerHub depodaki görüntüden için Hello URL'sini belirtin. Merhaba resim parametresi alır hello formu [repo] / [görüntü adı]
4. Merhaba görüntü bir iş yükü giriş tanımlanmış noktası yok sonra tooexplicitly ihtiyacınız başlatma işleminden sonra çalışan hello kapsayıcı tutar hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi giriş komutları belirtin.

![Kapsayıcılar için Service Fabric Yeoman oluşturucusu][sf-yeoman]

## <a name="deploy-hello-application"></a>Merhaba uygulaması dağıtma

### <a name="using-xplat-cli"></a>XPlat CLI aracını kullanma
Merhaba uygulama oluşturulduktan sonra toohello yerel küme hello Azure CLI kullanarak dağıtabilirsiniz.

1. Toohello yerel Service Fabric kümesi bağlayın.

    ```bash
    azure servicefabric cluster connect
    ```

2. Kullanım hello hello şablonu toocopy Merhaba uygulaması toohello kümenin görüntü deposu paketini, hello uygulama türünü kaydetme ve hello uygulama örneğini oluşturmak sağlanan komut dosyası yükleyin.

    ```bash
    ./install.sh
    ```

3. Bir tarayıcı açın ve http://localhost: 19080/Explorer (Merhaba Vagrant Mac OS X kullanıyorsanız VM hello özel IP ile değiştir localhost) konumunda tooService Fabric Gezgini'ne gidin.
4. Merhaba uygulamaları düğümünü genişletin ve şimdi uygulama türü için bir giriş ve hello bu türünün ilk örneği için başka bir yoktur.
5. Merhaba kaldırma komut dosyası kullan hello şablon toodelete hello uygulama örneği içinde sağlanan ve hello uygulama türü kaydını silin.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Azure CLI 2.0 aracını kullanma

Merhaba başvuru belge yönetme hakkında bkz bir [uygulama yaşam döngüsü kullanmayı hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Örnek bir uygulama için [checkout hello Service Fabric kapsayıcı kodu Github'da örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Daha fazla Hizmetleri tooan varolan uygulama ekleme

tooadd başka bir kapsayıcı hizmet zaten kullanılarak oluşturulan tooan uygulaması `yo`, hello aşağıdaki adımları gerçekleştirin:

1. Merhaba var olan uygulamanın toohello kök dizini değiştirin.  Örneğin, `cd ~/YeomanSamples/MyApplication`, `MyApplication` Yeoman tarafından oluşturulan hello uygulamasıdır.
2. `yo azuresfcontainer:AddService` öğesini çalıştırın

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>El ile paketini ve kapsayıcı görüntüsünü Dağıt
el ile kapsayıcılı hizmet paketleme hello işlemi aşağıdaki adımları hello üzerinde dayanır:

1. Merhaba kapsayıcılara tooyour depo yayımlayın.
2. Merhaba paket dizin yapısını oluşturun.
3. Merhaba hizmet bildirim dosyasını düzenleyin.
4. Merhaba uygulama bildirim dosyasının düzenleyin.

## <a name="deploy-and-activate-a-container-image"></a>Dağıtma ve kapsayıcı görüntü etkinleştirin
Merhaba Service Fabric içinde [uygulama modeli](service-fabric-application-model.md), hangi birden çok çoğaltmaları hizmete bir uygulama konağı bir kapsayıcıyı temsil eder. toodeploy ve etkinleştirme kapsayıcı, put hello adını hello kapsayıcı görüntüsüne bir `ContainerHost` hello hizmet bildirimi öğesinde.

Merhaba hizmet bildiriminde eklemek bir `ContainerHost` hello giriş noktası için. Ardından kümesi hello `ImageName` toobe hello adını hello kapsayıcı depo ve görüntü. Merhaba aşağıdaki kısmi bildirimi gösterir nasıl toodeploy hello kapsayıcı olarak adlandırılan bir örnek `myimage:v1` adlı bir depodan `myrepo`:

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

İsteğe bağlı hello belirterek giriş komutları sağlayabilir `Commands` hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi öğesi.

> [!NOTE]
> Merhaba görüntü bir iş yükü giriş tanımlanmış noktası yok sonra tooexplicitly ihtiyacınız içindeki giriş komutları belirtin `Commands` hello kapsayıcı çalıştırdıktan sonra devam edilecek hello kapsayıcı içindeki komutları toorun virgülle ayrılmış bir dizi öğesi Başlangıç.

## <a name="understand-resource-governance"></a>Kaynak İdaresi anlama
Kaynak İdaresi kapsayıcı hello hello kaynakları kısıtlayan hello kapsayıcı yeteneğini hello konakta kullanabilirsiniz ' dir. Merhaba `ResourceGovernancePolicy`, kendisi hello uygulama bildiriminde belirtilen bir hizmeti kod paketi için kullanılan toodeclare kaynak sınırları olduğu. Kaynak sınırları kaynakları aşağıdaki Merhaba ayarlanabilir:

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
bir kapsayıcı toodownload tooprovide oturum açma kimlik bilgileri toohello kapsayıcı deposu olabilir. Merhaba uygulama bildiriminde belirtilen hello oturum açma kimlik bilgileri, kullanılan toospecify hello oturum açma bilgileri veya hello kapsayıcı görüntü hello görüntü deposundan karşıdan yüklemek için SSH anahtarı, ' dir. Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser* hello parola düz metin birlikte (*değil* önerilen):

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

Toohello makine dağıtmış olan bir sertifikayı kullanarak hello parolayı şifrelemek öneririz.

Merhaba aşağıdaki örnekte gösterilir adlı bir hesap *TestUser*, burada hello parola adı verilen bir sertifika kullanılarak şifrelenmiş *MyCert*. Merhaba kullanabilirsiniz `Invoke-ServiceFabricEncryptText` PowerShell komut toocreate hello gizli şifreli metin hello parolası. Daha fazla bilgi için hello makalesine bakın [Service Fabric uygulamaları parolalarında yönetme](service-fabric-application-secret-management.md).

Merhaba toodecrypt hello parola kullandı hello sertifikasının özel anahtarı yerel makinede bir bant dışı yöntem dağıtılan toohello olması gerekir. (Azure'da, Azure Resource Manager bu yöntem budur.) Ardından, Service Fabric hello hizmet paketi toohello makine dağıtırken hello gizli şifresini çözebilir. Merhaba gizli hello hesap adı ile birlikte kullanarak, onu hello kapsayıcı deposuyla sonra doğrulayabilir.

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
Belirterek hello kapsayıcı ile bir ana bilgisayar kullanılan bağlantı noktası toocommunicate yapılandırabilirsiniz bir `PortBinding` hello uygulama bildiriminde. Merhaba kapsayıcı tooa bağlantı hello konaktaki içinde dinleyen bir Hello bağlantı noktası bağlama eşlemeleri hello bağlantı noktası toowhich hello hizmet.

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
Hello kullanarak `PortBinding` İlkesi, bir kapsayıcı bağlantı noktası tooan eşleyebilirsiniz `Endpoint` hello hizmet bildiriminde. uç nokta hello `Endpoint1` sabit bir bağlantı noktası (örneğin, bağlantı noktası 80) belirtebilirsiniz. Rastgele bir bağlantı noktası hello kümenin uygulama bağlantı noktası aralığından sizin için bu durumda seçilen bağlantı noktası yok hiç da belirtebilir.

Bir uç nokta belirtirseniz, hello kullanarak `Endpoint` hello hizmet bildirimi Konuk kapsayıcı, Service Fabric etiketinde otomatik olarak bu uç nokta toohello adlandırma hizmeti yayımlama. Merhaba kümede çalışan diğer hizmetler, böylece çözümlemek için hello REST sorgularını kullanarak bu kapsayıcı bulabilir.

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

Merhaba Naming service ile kaydederek kolayca hello kod-kapsayıcıya iletişiminde, kapsayıcı içinde hello kullanarak yapabileceğiniz [ters proxy](service-fabric-reverseproxy.md). İletişim hello ters proxy http dinleme bağlantı noktası ve ortam değişkenleri olarak toocommunicate ile istediğiniz hello Hizmetleri hello adını sağlayarak gerçekleştirilir. Daha fazla bilgi için hello sonraki bölüme bakın.

## <a name="configure-and-set-environment-variables"></a>Ortam değişkenlerini yapılandırma ve ayarlama
Ortam değişkenleri, her kod paketi bildiriminde hello hizmet, hem kapsayıcılarında dağıtılan Hizmetleri ya da işlemler/Konuk yürütülebilir dosyaları dağıtılan Hizmetleri için belirtilebilir. Bu ortam değişkeni değerlerini özellikle hello uygulama bildiriminde geçersiz veya uygulama parametreleri olarak dağıtım sırasında belirtilen.

Merhaba aşağıdaki hizmet bildirim XML parçacığını gösterir nasıl bir örneği için bir kod paketi toospecify ortam değişkenleri:

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

Bu ortam değişkenleri hello uygulama bildirim düzeyinde geçersiz kılınabilir:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

Merhaba önceki örnekte, biz hello için açık bir değer belirtilen `HttpGateway` ortam değişkeni (Merhaba değeri ayarlarız sırada 19000) `BackendServiceName` hello parametresi `[BackendSvc]` uygulama parametresi. Bu ayarlar için toospecify hello değer etkinleştirmek `BackendServiceName`değer hello uygulamayı dağıttıktan sonra hello bildiriminde sabit bir değere sahip değil.

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

Bir örnek hizmet bildirimi (uygulama bildirimi önceki hello belirtilen) aşağıdaki gibidir:

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
Kapsayıcılı hizmetini dağıttıysanız, bilgi nasıl toomanage okuyarak kendi ömrü [Service Fabric uygulama yaşam döngüsü](service-fabric-application-lifecycle.md).

* [Service Fabric ve kapsayıcıları genel bakış](service-fabric-containers-overview.md)
* [Hello Azure CLI kullanarak Service Fabric kümeleri ile etkileşim kurma](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>İlgili makaleler

* [Service Fabric ve Azure CLI 2.0 ile çalışmaya başlama](service-fabric-azure-cli-2-0.md)
* [Service Fabric XPlat CLI ile çalışmaya başlama](service-fabric-azure-cli.md)
