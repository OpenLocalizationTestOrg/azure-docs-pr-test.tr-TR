---
title: "Azure Service Fabric CLI kullanarak aaaManage Azure Service Fabric uygulamaları"
description: "Azure Service Fabric CLI kullanarak bir Azure Service Fabric toodeploy ekleme ve kaldırma uygulamalardan nasıl küme öğrenin"
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: d9f98cee1d70f71a2aab68ff556956619910e4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-service-fabric-application-by-using-azure-service-fabric-cli"></a>Azure Service Fabric uygulaması Azure Service Fabric CLI kullanarak yönetme

Bilgi nasıl bir Azure Service Fabric kümede çalışan toocreate ve delete uygulamaları.

## <a name="prerequisites"></a>Ön koşullar

* Service Fabric CLI yükleyin. Ardından, Service Fabric kümesi seçin. Daha fazla bilgi için bkz: [Service Fabric CLI ile çalışmaya başlama](service-fabric-cli.md).

* Dağıtılan bir Service Fabric uygulama paketi hazır toobe sahip. Hakkında daha fazla bilgi için tooauthor ve bir uygulama paketi okuma hakkında hello [Service Fabric uygulama modeli](service-fabric-application-model.md).

## <a name="overview"></a>Genel Bakış

toodeploy yeni bir uygulama, aşağıdaki adımları tamamlayın:

1. Bir uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.
2. Uygulama türü sağlayın.
3. Bir uygulama oluşturmak ve belirtin.
4. Hizmetleri oluşturmak ve belirtin.

tooremove varolan bir uygulamayı aşağıdaki adımları tamamlayın:

1. Merhaba uygulaması silin.
2. Sağlamayı kaldırma hello ilişkili uygulama türü.
3. Merhaba görüntü deposu içeriğini silin.

## <a name="deploy-a-new-application"></a>Yeni bir uygulama dağıtma

toodeploy yeni bir uygulama görevleri aşağıdaki tam hello:

### <a name="upload-a-new-application-package-toohello-image-store"></a>Yeni bir uygulama paketi toohello görüntü deposu karşıya yükle

Bir uygulamayı oluşturmadan önce hello uygulama paketi toohello Service Fabric görüntü deposuna karşıya yükleyin.

Örneğin, uygulama paketinizi hello ise `app_package_dir` dizin, aşağıdaki komutları tooupload hello dizin kullanım hello:

```azurecli
sfctl application upload --path ~/app_package_dir
```

Büyük uygulama paketlerini hello belirtebilirsiniz `--show-progress` seçeneği toodisplay hello hello karşıya yükleme ilerlemesini.

### <a name="provision-hello-application-type"></a>Sağlama hello uygulama türü

Merhaba karşıya yükleme tamamlandığında, hello uygulaması sağlayın. tooprovision hello uygulama, komutu aşağıdaki kullanım hello:

```azurecli
sfctl application provision --application-type-build-path app_package_dir
```

Merhaba değeri `application-type-build-path` uygulama paketinizi karşıya burada hello dizin hello adıdır.

### <a name="create-an-application-from-an-application-type"></a>Bir uygulama türü ile uygulama oluşturma

Merhaba uygulaması sağlama sonra komut tooname aşağıdaki hello kullanın ve uygulamanızı oluşturun:

```azurecli
sfctl application create --app-name fabric:/TestApp --app-type TestAppType --app-version 1.0
```

`app-name`Merhaba'a kadar olan hello uygulama örneğini toouse istediğiniz addır. Daha önceden hazırlanan uygulama bildirimden ek parametreler elde edebilirsiniz.

Merhaba uygulama adı, hello önek ile başlamalı `fabric:/`.

### <a name="create-services-for-hello-new-application"></a>Merhaba yeni uygulama hizmetleri oluşturma

Bir uygulama oluşturduktan sonra hizmetleri hello uygulama oluşturun. Aşağıdaki örneğine hello bizim uygulamadan yeni bir durum bilgisiz hizmet oluşturuyoruz. bir uygulama oluşturun hello Hizmetleri hizmet bildirimi hello daha önceden hazırlanan uygulama paketinde tanımlanır.

```azurecli
sfctl service create --app-id TestApp --name fabric:/TestApp/TestSvc --service-type TestServiceType \
--stateless --instance-count 1 --singleton-scheme
```

## <a name="verify-application-deployment-and-health"></a>Uygulama dağıtımı ve durumunu doğrulayın

tooverify her şeyi sağlıklı olduğundan, sistem durumu komutları aşağıdaki hello kullanın:

```azurecli
sfctl application list
sfctl service list --application-id TestApp
```

Merhaba hizmetin sistem durumunun iyi olduğundan tooverify benzer komutları tooretrieve hello sistem hello hizmet ve uygulama durumunu kullanın:

```azurecli
sfctl application health --application-id TestApp
sfctl service health --service-id TestApp/TestSvc
```

Sağlıklı hizmetler ve uygulamalar sahip bir `HealthState` değerini `Ok`.

## <a name="remove-an-existing-application"></a>Varolan bir uygulamayı kaldırma

tooremove bir uygulama görevleri aşağıdaki tam hello:

### <a name="delete-hello-application"></a>Merhaba uygulamayı Sil

toodelete hello uygulama, komutu aşağıdaki kullanım hello:

```azurecli
sfctl application delete --application-id TestEdApp
```

### <a name="unprovision-hello-application-type"></a>Merhaba uygulama türü sağlama

Merhaba uygulaması sildikten sonra artık ihtiyacınız varsa hello uygulama türü sağlamasını. toounprovision hello uygulama türü, komutu aşağıdaki kullanım hello:

```azurecli
sfctl application unprovision --application-type-name TestAppTye --application-type-version 1.0
```

Merhaba türü adını ve türünü sürümü hello adı ve sürümü hello daha önceden hazırlanan uygulama bildiriminde eşleşmesi gerekir.

### <a name="delete-hello-application-package"></a>Merhaba uygulama paketini silmeniz

Merhaba uygulama türü sağlamasını sonra artık ihtiyacınız varsa, hello uygulama paketi hello görüntü deposundan silebilirsiniz. Uygulama paketleri silme, disk alanını boşaltmak yardımcı olur. 

Merhaba görüntü deposundan komutu aşağıdaki kullanım hello toodelete hello uygulama paketi:

```azurecli
sfctl store delete --content-path app_package_dir
```

`content-path`Merhaba uygulaması oluşturduğunuzda yüklediğiniz hello dizinin Hello adı olmalıdır.

## <a name="upgrade-application"></a>Uygulama yükseltme

Uygulamanızı oluşturduktan sonra bunu yineleyebilir hello aynı adımları tooprovision ikinci sürümü, uygulamanızın kümesi. Ardından, Service Fabric uygulama yükseltme işlemine toorunning hello ikinci sürümü Merhaba uygulaması geçiş yapabilir. Daha fazla bilgi için üzerinde hello belgelerine bakın. [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).

tooperform, yükseltme uygulama hello kullanarak ilk sağlama hello ileri sürümünü aynı komutları önceki gibi hello:

```azurecli
sfctl application upload --path ~/app_package_dir_2
sfctl application provision --application-type-build-path app_package_dir_2
```

Tooperform izlenen otomatik yükseltmeyi başlatın ardından hello yükseltme hello aşağıdaki komutu çalıştırarak önerilir:

```azurecli
sfctl application upgrade --app-id TestApp --app-version 2.0.0 --parameters "{\"test\":\"value\"}" --mode Monitored
```

Yükseltmeler ne olursa olsun kümesi belirtilen ile varolan parametreler geçersiz. Uygulama parametreleri bağımsız değişkenleri toohello yükseltme komutu, gerekirse geçirilmesi gerekir. Uygulama parametreleri bir JSON nesnesi olarak kodlanmış.

tooretrieve herhangi bir parametre daha önce belirtilen, hello kullanabilirsiniz `sfctl application info` komutu.

Uygulama yükseltme devam ederken, hello durum kullanılarak alınabilir `sfctl application upgrade-status` komutu.

Son olarak, bir yükseltme devam ediyor ve iptal toobe gerekirse hello kullanabilirsiniz `sfctl application upgrade-rollback` geri tooroll hello yükseltme.

## <a name="next-steps"></a>Sonraki adımlar

* [Service Fabric CLI temelleri](service-fabric-cli.md)
* [Service Fabric Linux'ta ile çalışmaya başlama](service-fabric-get-started-linux.md)
* [Service Fabric uygulama yükseltme başlatma](service-fabric-application-upgrade.md)
