---
title: "aaaAzure Service Fabric Docker oluşturan Önizleme"
description: "Azure Service Fabric Docker Compose biçimi toomake kabul eder, Service Fabric kullanarak, daha kolay tooorchestrate varolan kapsayıcıları. Bu destek, şu anda önizlemede değil."
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
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Docker Compose Azure Service Fabric (Önizleme) uygulama desteği

Docker kullanan hello [docker-compose.yml](https://docs.docker.com/compose) çok kapsayıcı uygulamaları tanımlamak için dosya. toomake, müşterilerin Azure Service Fabric Docker tooorchestrate varolan kapsayıcı uygulamaları aşina kolaylaştırır, biz Docker Compose Önizleme desteği yerel olarak hello platformunda eklediniz. Service Fabric sürüm 3 ve sonraki kabul edebileceği `docker-compose.yml` dosyaları. 

Bu destek önizlemede olmadığından, yalnızca bir alt kümesini oluşturma yönergeleri desteklenir. Örneğin, uygulama yükseltmeler desteklenmez. Ancak, istediğiniz zaman kaldırma ve bunları yükseltme yerine uygulamaları dağıtma.

toouse Bu önizleme, 5.7 veya hello Service Fabric çalışma zamanı hello SDK karşılık gelen hello yanı sıra Azure portal aracılığıyla daha büyük sürümüyle kümenizi oluşturun. 

> [!NOTE]
> Bu özellik Önizleme aşamasındadır ve üretimde desteklenmiyor.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Service Fabric Docker Compose bir dosyada dağıtma

Merhaba aşağıdaki komutları bir Service Fabric uygulaması oluşturma (adlı `fabric:/TestContainerApp` örnek önceki hello içinde), hangi izleyebilir ve başka bir Service Fabric uygulaması gibi yönetebilirsiniz. Sistem durumu sorgularının sayısı için belirtilen uygulama adı hello kullanabilirsiniz.

### <a name="use-powershell"></a>PowerShell kullanma

Service Fabric oluşturan bir uygulama hello aşağıdaki PowerShell komutunu çalıştırarak bir docker-compose.yml dosyası oluşturun:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`ve `RegistryPassword` toohello kapsayıcı kayıt defteri kullanıcı adı ve parola bakın. Merhaba uygulaması tamamladıktan sonra komutu aşağıdaki hello kullanarak durumunu denetleyebilirsiniz:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete PowerShell aracılığıyla oluşturma uygulama Merhaba, hello aşağıdaki komutu kullanın:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Azure Service Fabric CLI (sfctl) kullanın

Alternatif olarak, Service Fabric CLI komutu aşağıdaki hello kullanabilirsiniz:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Merhaba uygulaması oluşturduktan sonra komutu aşağıdaki hello kullanarak durumunu denetleyebilirsiniz:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

toodelete hello oluşturma uygulama hello aşağıdaki komutu kullanın:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Desteklenen oluşturma yönergeleri

Bu önizleme hello yapılandırma temelleri aşağıdaki hello dahil olmak üzere, hello Oluştur sürüm 3 biçimini seçeneklerinden kümesini destekler:

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

Bölümünde açıklandığı gibi hello küme kaynak sınırları, zorlama ayarlamak [Service Fabric kaynak İdaresi](service-fabric-resource-governance.md). Tüm diğer Docker Compose yönergeleri Bu önizleme için desteklenmez.

## <a name="servicednsname-computation"></a>ServiceDnsName hesaplama

Oluşturma dosyasında belirttiğiniz hello hizmet adı tam etki alanı adı ise (diğer bir deyişle, bir nokta [.] içerdiği), Service Fabric tarafından kayıtlı hello DNS adı `<ServiceName>` (Merhaba nokta dahil). Aksi durumda, her yol kesimi hello uygulama adı, etki alanı etiketi hello en üst düzey etki alanı etiketi olma hello ilk yol kesimi ile Merhaba hizmeti DNS adı olur.

Örneğin, uygulama adı hello belirtilen ise `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` kayıtlı DNS adı hello olacaktır.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Oluştur (örnek tanım) ve Service Fabric uygulama modeli (tür tanımı) arasındaki farklar

Docker-compose.yml dosyası kapsayıcılar kendi özellikler ve yapılandırmalar da dahil olmak üzere, dağıtılabilir bir dizi açıklar.
Örneğin, ortam değişkenleri ve bağlantı noktaları hello dosyası içerebilir. Merhaba docker-compose.yml dosyası kısıtlamalarından, kaynak sınırları ve DNS adları gibi dağıtım parametreleri de belirtebilirsiniz.

Merhaba [Service Fabric uygulama modeli](service-fabric-application-model.md) kullandığı hizmet türlerini ve uygulama türleri, pek çok uygulama örneğini bulunan hello aynı türde. Örneğin, müşteri başına bir uygulama örneği olabilir. Bu tür tabanlı model hello birden fazla sürümünü destekleyen hello çalışma zamanı ile kayıtlı aynı uygulama türü.

Örneğin, bir müşteri AppTypeA 1.0 türüyle örneği bir uygulama olabilir ve Müşteri B ile Merhaba örneği başka bir uygulama olabilir aynı türü ve sürümü. Merhaba uygulama bildirimleri hello uygulama türlerini tanımlayın ve Merhaba uygulaması oluşturduğunuzda hello uygulama adını ve dağıtım parametreleri belirtin.

Bu model esneklik sunar ancak biz de toosupport türleri hello bildirim dosyasındaki örtük nerede daha basit ve örnek tabanlı dağıtım modeli planladığınıza. Bu modelde, her uygulamanın kendi bağımsız bildirimi alır. Biz bu çalışmaların örneği tabanlı dağıtım biçimi olduğu docker-compose.yml için destek ekleyerek önizlemede.

## <a name="next-steps"></a>Sonraki adımlar

* Merhaba üzerinde okuma [Service Fabric uygulama modeli](service-fabric-application-model.md)
* [Service Fabric CLI kullanmaya başlama](service-fabric-cli.md)
