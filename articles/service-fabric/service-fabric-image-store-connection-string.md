---
title: "Service Fabric görüntü Mağazası'ndan dize aaaAzure | Microsoft Docs"
description: "Merhaba görüntü deposu bağlantı dizesi anlama"
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: 
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: alexwun
ms.openlocfilehash: 83f5ad75b5df07726997da3173722028255b8cae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-imagestoreconnectionstring-setting"></a>Merhaba ImageStoreConnectionString ayarı anlama

Bazı Belgelerimizi biz kısaca "ImageStoreConnectionString" parametresi hello varlığını gerçekten anlamını açıklayan olmadan Bahsediyor. Ve bir makale gibi aracılığıyla olduktan sonra [PowerShell kullanarak uygulamaları dağıtma ve Kaldır][10], bunu tüm gibi görünüyor hello küme bildiriminde hello hedefinin göründüğü gibi kopyala/yapıştır hello değerdir Küme. Merhaba ayarı küme yapılandırılabilir olması gerekir, ancak hello aracılığıyla bir küme oluştururken [Azure portal][11], hiçbir seçeneği tooconfigure Bu ayar ve buna ait her zaman "fabric: görüntü" yoktur. Bu ayarın hello amacı nedir?

![Küme bildirimi][img_cm]

Service Fabric dahili Microsoft tüketim için bir platform olarak birçok farklı ekip tarafından başlatılan bazı yönlerini büyük ölçüde özelleştirilebilir - hello "Image Store" gibi bir yönü için. Esas olarak, hello Image Store takılabilir uygulama paketleri depolamak için deposudur. Uygulamanızı dağıtılan tooa hello küme düğümünde olduğunda, o düğümde uygulama paketinizi Merhaba içeriğine hello Image Store indirir. Merhaba ImageStoreConnectionString istemcileri ve düğümleri toofind hello doğru görüntü deposu için verilmiş bir küme için tüm hello gerekli bilgileri içeren bir ayardır.

Şu anda görüntü deposu sağlayıcıları üç olası tür vardır ve bunların karşılık gelen bağlantı dizeleri aşağıdaki gibidir:

1. Image Store hizmeti: "fabric: görüntü"

2. Dosya sistemi: "file:[file sistem path]"

3. Azure Storage: "xstore:DefaultEndpointsProtocol = https; AccountName = [...]; AccountKey = [...]; Kapsayıcı = [...] "

Üretimde kullanılan hello sağlayıcısı hello görüntü Deposu hizmetini Service Fabric Explorer'dan gördüğünüz bir durum bilgisi olan kalıcı sistem hizmeti olduğu türüdür. 

![Image Store hizmeti][img_is]

Barındırma hello Image Store hello kümenin kendisi içinde bir sistem hizmeti hello paket deposu için dış bağımlılıklar ortadan kaldırır ve bize hello yere göre depolama üzerinde daha fazla denetim sağlar. Gelecekteki hello Image Store geçici büyük olasılıkla tootarget hello Image Store sağlayıcısını ilk olarak, yoksa yalnızca geliştirmeleridir. Merhaba istemci zaten bağlı toohello hedef küme olduğundan hello bağlantı dizesi hello görüntü deposu hizmet sağlayıcısı için herhangi bir benzersiz bilgi yok. Merhaba istemci hello sistem hizmeti hedefleme protokolleri kullanılması gereken tooknow yeterlidir.

Merhaba dosya sistemi sağlayıcısı görüntü Deposu hizmetini hello yerine yerel bir kutusunu kümeleri için geliştirme toobootstrap hello küme sırasında biraz daha hızlı kullanılır. Merhaba fark genellikle küçük, ancak çoğu terimleri için yararlı bir iyileştirme geliştirme sırasında gelir. Bir yerel bir kutusu küme ile olası toodeploy hello diğer depolama sağlayıcısı türlerinin de, ancak genellikle bir neden yoktur toodo şekilde hello geliştirmek ve test iş akışı kalır beri hello aynı bağımsız olarak sağlayıcısı. Bu kullanım dışında hello dosya sistemi ve Azure depolama sağlayıcıları için eski destek yalnızca mevcut.

Merhaba ImageStoreConnectionString yapılandırılabilir olsa da, bu nedenle, genellikle yalnızca hello varsayılan ayarı kullanın. TooAzure üzerinden yayımlarken [Visual Studio][12], hello parametresi otomatik olarak ayarlanırsa sizin için uygun şekilde. Azure üzerinde barındırılan programlamayla dağıtımı tooclusters için hello bağlantı dizesi her zaman "fabric: görüntü" dir. Şüpheli zaman değeri her zaman hello küme bildirimi tarafından alarak doğrulanabilir olsa [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), veya [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Her iki şirket içi test ve üretim kümelerine her zaman yapılandırılmış toouse hello görüntü deposu hizmet sağlayıcısı da olmalıdır.

### <a name="next-steps"></a>Sonraki adımlar
[Dağıtma ve PowerShell kullanarak uygulamaları kaldırma][10]

<!--Image references-->
[img_is]: ./media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: ./media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md
