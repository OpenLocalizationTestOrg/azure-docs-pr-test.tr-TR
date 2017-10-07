---
title: "aaaAzure kapsayıcı örnekleri kapsayıcı grupları"
description: "Kapsayıcı grupları Azure kapsayıcı durumlarda nasıl çalıştığını anlamak"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2b0e784609979045c8f77d7b6d0987ec3fee714c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="container-groups-in-azure-container-instances"></a>Azure kapsayıcı durumlarda kapsayıcı grupları

Merhaba en üst düzey Azure kapsayıcı durumlarda bir kapsayıcı grubu kaynaktır. Bu makalede, kapsayıcı grupları nedir ve ne tür senaryoların bunlar etkinleştirmek açıklanmaktadır.

## <a name="how-a-container-group-works"></a>Kapsayıcı grubu nasıl çalışır?

Bir kapsayıcı grubun bir koleksiyondur hello üzerinde zamanlanmış kapsayıcıların aynı ana bilgisayar makine ve bir yaşam döngüsü, yerel ağ ve depolama birimleri paylaşın. Benzer toohello kavramı olan bir *pod* içinde [Kubernetes](https://kubernetes.io/docs/concepts/workloads/pods/pod/) ve [DC/OS](https://dcos.io/docs/1.9/deploying-services/pods/).

Merhaba Aşağıdaki diyagramda birden çok kapsayıcı içeren bir kapsayıcı grubu örneği gösterilmektedir.

![Kapsayıcı grupları örneği][container-groups-example]

Şunlara dikkat edin:

- Merhaba Grup tek ana makinede zamanlandı.
- Merhaba grubu tek bir ortak IP adresi, bir kullanıma sunulan bağlantı noktası ile kullanıma sunar.
- Merhaba Grup iki kapsayıcıları için yapılır. Merhaba diğer 5000 bağlantı noktasını dinler sırasında bir kapsayıcı bağlantı noktası 80 üzerinde dinler.
- iki Azure dosya paylaşımları birim başlatmalar olarak Hello grubu içerir ve her kapsayıcı yerel olarak hello paylaşımları birini bağlar.

### <a name="networking"></a>Ağ

Kapsayıcı grupları, bir IP adresi ve bağlantı noktası ad alanı, IP adresi üzerinde paylaşır. tooenable dış istemcilere tooreach hello grup içindeki bir kapsayıcı, başlangıç bağlantı noktası başlangıç IP adresi ve hello kapsayıcısından kullanıma gerekir. Grup Merhaba kapsayıcılara bir bağlantı noktası ad alanı paylaştığından, bağlantı noktası eşlemesi desteklenmiyor. Bu bağlantı noktalarını hello grubun IP adresinde dışarıdan gösterilmeyen olsa bile bir grup kapsayıcılara birbirine hello üzerinde localhost aracılığıyla bunlar açık bağlantı noktaları ulaşabilirsiniz.

### <a name="storage"></a>Depolama

Bir kapsayıcı grubundaki dış birimleri toomount belirtebilirsiniz. Bu birimlerin hello tek tek bir grup kapsayıcılarında içindeki belirli yollara içine eşleyebilirsiniz.

## <a name="common-scenarios"></a>Genel senaryolar

Birden çok kapsayıcı grupları tek bir işlev görev yukarı toodivide küçük bir sayıya farklı ekip tarafından alınabilir ve ayrı kaynak gereksinimlerini kapsayıcı görüntülerinin istediğiniz durumlarda kullanışlıdır. Örnek Kullanım dahil olabilir:

- Bir uygulama kapsayıcısı ve günlüğe kaydetme kapsayıcı. Merhaba günlük kapsayıcı hello günlükleri ve ölçümleri çıktı hello ana uygulama tarafından toplar ve toolong vadeli depolama yazar.
- Bir uygulama ve izleme kapsayıcı. kapsayıcı düzenli aralıklarla izleme hello çalıştığını ve düzgün yanıt ve değilse bir uyarı başlatır bir istek toohello uygulama tooensure yapar.
- Bir web uygulaması hizmet veren bir kapsayıcı ve kaynak denetiminden hello son içerik çekme kapsayıcı.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[çok kapsayıcı grubu dağıtma](container-instances-multi-container-group.md) bir Azure Resource Manager şablonu ile.

<!-- IMAGES -->

[container-groups-example]: ./media/container-instances-container-groups/container-groups-example.png