---
title: "aaaDefinine ve Azure mikro durumunu yönetmek | Microsoft Docs"
description: "Nasıl toodefine ve Service Fabric hizmet durumunda yönetme"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Hizmet durumu
**Hizmet durumu** toohello bellek içi ya da hizmet toofunction gerektirdiğini disk verilerini gösterir. İçerir, örneğin, hello veri yapılarını ve üye değişkenleri hello hizmet okur ve toodo iş yazar. Merhaba hizmeti nasıl geliştirilmiştir bağlı olarak dosyalara veya diskte depolanan diğer kaynaklara de içerebilir. Örneğin, bir veritabanı hello dosyaları toostore veri ve işlem günlüklerini kullanırsınız.

Bir örnek hizmeti olarak şimdi bir hesap makinesi göz önünde bulundurun. Temel hesaplayıcı hizmet iki sayıyı alır ve bunların toplamı döndürür. Bu hesaplamayı gerçekleştiren hiç üye değişkeni veya diğer bilgileri içerir.

Şimdi düşünün hello aynı hesaplayıcı ancak depolamak ve hello son toplam döndürmek için ek bir yöntem ile hesaplanan. Bu hizmet durum bilgisi olan sunulmuştur. Durum bilgisi olan yeni bir toplam hesaplar ve tooreturn hello son hesaplanan toplam söylediğinizde okur toowhen Yazar bazı durumu içerdiği anlamına gelir.

Azure Service Fabric içinde hello ilk hizmeti durumsuz bir hizmet olarak adlandırılır. Merhaba ikinci hizmeti durum bilgisi olan bir hizmet olarak adlandırılır.

## <a name="storing-service-state"></a>Hizmetinin durumunu saklama
Durum ya da externalized veya hello durumu düzenleme hello koduyla birlikte bulunabilir. Externalization durumunun, genellikle bir dış veritabanı kullanılarak yapılır veya hello ağ üzerinden veya işlemi dışında farklı makinelerde çalıştırır aynı makine hello diğer veri depolayın. Hesaplayıcı örneğimizde hello veri deposu bir SQL veritabanına veya Azure tablo deposu örneği olabilir. Her istek toocompute hello toplam bu veriler üzerinde bir güncelleştirme gerçekleştirir ve toohello hizmet tooreturn hello değeri sonucu hello deposundan çekilen hello geçerli değeri ister. 

Durum ayrıca hello durumu işleyen hello kodu ile birlikte bulunabilir. Durum bilgisi olan Service Fabric Hizmetleri'nde genellikle bu modeli kullanılarak oluşturulur. Service Fabric bu durum yüksek oranda kullanılabilir, tutarlı ve sürekli ve hello Hizmetleri bu şekilde yerleşik kolayca ölçeklendirebilirsiniz hello altyapı tooensure sağlar.

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kavramlarla ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:

* [Service Fabric hizmetlerin kullanılabilirliğini](service-fabric-availability-services.md)
* [Service Fabric Hizmetleri ölçeklenebilirliği](service-fabric-concepts-scalability.md)
* [Service Fabric Hizmetleri bölümlendirme](service-fabric-concepts-partitioning.md)
* [Service Fabric güvenilir hizmetler](service-fabric-reliable-services-introduction.md)
