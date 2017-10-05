---
title: "Azure Service Fabric Docker Compose Önizleme"
description: "Azure Service Fabric Service Fabric kullanarak var olan kapsayıcıları düzenlemek kolay hale getirmek için Docker Compose'u biçimi kabul eder. Bu destek, şu anda önizlemede değil."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e05d1a3d6111e3bbc34008226bcd1fdf35935450
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Docker Compose Azure Service Fabric (Önizleme) uygulama desteği

Docker kullanan [docker-compose.yml](https://docs.docker.com/compose) çok kapsayıcı uygulamaları tanımlamak için dosya. Müşteriler için Azure Service Fabric varolan kapsayıcı uygulamaları düzenlemek için Docker aşina kolaylaştırmak için biz Docker Compose Önizleme desteği yerel olarak platform eklediniz. Service Fabric sürüm 3 ve sonraki kabul edebileceği `docker-compose.yml` dosyaları. 

Bu destek önizlemede olmadığından, yalnızca bir alt kümesini oluşturma yönergeleri desteklenir. Örneğin, uygulama yükseltmeler desteklenmez. Ancak, istediğiniz zaman kaldırma ve bunları yükseltme yerine uygulamaları dağıtma.

Bu önizleme özelliğini kullanmak için 5.7 veya büyük karşılık gelen SDK ile birlikte Azure portalı üzerinden Service Fabric çalışma zamanı sürümü ile kümenizi oluşturun. 

> [!NOTE]
> Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Service Fabric Docker Compose bir dosyada dağıtma

Aşağıdaki komutlar bir Service Fabric uygulaması oluşturma (adlı `fabric:/TestContainerApp` önceki örnekte), hangi izleyebilir ve başka bir Service Fabric uygulaması gibi yönetebilirsiniz. Sistem durumu sorgularının sayısı için belirtilen uygulama adı kullanabilirsiniz.

### <a name="use-powershell"></a>PowerShell kullanma

Service Fabric oluşturan bir uygulama, PowerShell içinde aşağıdaki komutu çalıştırarak bir docker-compose.yml dosyası oluşturun:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`ve `RegistryPassword` kapsayıcı kayıt defteri kullanıcı adı ve parola bakın. Uygulama tamamladıktan sonra aşağıdaki komutu kullanarak durumunu denetleyebilirsiniz:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

PowerShell aracılığıyla oluşturma uygulamayı silmek için aşağıdaki komutu kullanın:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Azure Service Fabric CLI (sfctl) kullanın

Alternatif olarak, aşağıdaki Service Fabric CLI komutu kullanabilirsiniz:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Uygulamayı oluşturduktan sonra aşağıdaki komutu kullanarak durumunu denetleyebilirsiniz:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Oluşturma uygulamayı silmek için aşağıdaki komutu kullanın:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Desteklenen oluşturma yönergeleri

Bu önizleme bir alt kümesini aşağıdaki temelleri dahil olmak üzere Oluştur sürüm 3 biçiminden yapılandırma seçeneklerini destekler:

* Hizmetleri > dağıtmak > çoğaltmaları
* Hizmetleri > dağıtmak > yerleştirme > kısıtlamaları
* Hizmetleri > dağıtmak > kaynak > sınırları
    * cpu-paylaşımları
    * -bellek
    * -bellek-değiştirme
* Hizmetleri > komutları
* Hizmetleri > ortamı
* Hizmetleri > bağlantı noktaları
* Hizmetleri > görüntüsü
* Hizmetleri > yalıtımını (yalnızca Windows)
* Hizmetleri > günlüğü > sürücüsü
* Hizmetleri > günlüğü > sürücü > Seçenekleri
* Birim & dağıtmak > birim

Bölümünde açıklandığı gibi kaynak sınırları, zorlama küme ayarlamak [Service Fabric kaynak İdaresi](service-fabric-resource-governance.md). Tüm diğer Docker Compose yönergeleri Bu önizleme için desteklenmez.

## <a name="servicednsname-computation"></a>ServiceDnsName hesaplama

Bir oluşturma dosyasında belirttiğiniz hizmet adını bir tam etki alanı adı ise (diğer bir deyişle, bir nokta [.] içerdiği), Service Fabric tarafından kayıtlı DNS adı `<ServiceName>` (nokta dahil). Aksi durumda, her yol kesimi uygulama ad hizmeti DNS adı, üst düzey etki alanı etiketi olma ilk yol kesimi ile etki alanı etiketi olur.

Örneğin, belirtilen uygulama adı ise `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` kayıtlı DNS adı olacaktır.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Oluştur (örnek tanım) ve Service Fabric uygulama modeli (tür tanımı) arasındaki farklar

Docker-compose.yml dosyası kapsayıcılar kendi özellikler ve yapılandırmalar da dahil olmak üzere, dağıtılabilir bir dizi açıklar.
Örneğin, dosyayı ortam değişkenleri ve bağlantı noktası içerebilir. Docker-compose.yml dosyası kısıtlamalarından, kaynak sınırları ve DNS adları gibi dağıtım parametreleri de belirtebilirsiniz.

[Service Fabric uygulama modeli](service-fabric-application-model.md) kullandığı hizmet türlerini ve aynı türde pek çok uygulama örnekleri bulunan uygulama türleri. Örneğin, müşteri başına bir uygulama örneği olabilir. Bu tür tabanlı modeli, çalışma zamanı ile kayıtlı aynı uygulama türünün birden fazla sürümünü destekler.

Örneğin, bir müşterinin AppTypeA 1.0 türüyle örneği bir uygulama olabilir ve Müşteri B aynı türü ve sürümü örneği başka bir uygulama olabilir. Uygulama bildirimleri uygulama türlerini tanımlayın ve uygulama oluşturduğunuzda uygulama adı ve dağıtım parametrelerini belirtin.

Bu model esneklik sunar ancak biz de türleri bildirim dosyasından örtük nerede daha basit ve örnek tabanlı dağıtım modelini destekleyen planlıyorsanız. Bu modelde, her uygulamanın kendi bağımsız bildirimi alır. Biz bu çalışmaların örneği tabanlı dağıtım biçimi olduğu docker-compose.yml için destek ekleyerek önizlemede.

## <a name="next-steps"></a>Sonraki adımlar

* Üzerinde okuma [Service Fabric uygulama modeli](service-fabric-application-model.md)
* [Service Fabric CLI kullanmaya başlama](service-fabric-cli.md)
