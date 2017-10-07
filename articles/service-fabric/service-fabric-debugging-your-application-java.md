---
title: "aaaDebug Azure Service Fabric uygulamanızı eclipse'te | Microsoft Docs"
description: "Merhaba güvenilirliğini ve performansını hizmetlerinizi geliştirmek ve bunları Eclipse'te yerel geliştirme kümede hata ayıklama tarafından geliştirin."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a>Java Service Fabric uygulamanızı Eclipse kullanarak hata ayıklama
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
> 

1. Merhaba adımları izleyerek yerel bir geliştirme kümesi Başlat [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started-linux.md).

2. EntryPoint.sh güncelleştirme hello hizmeti uzaktan hata ayıklama parametrelerle hello java işlemi başlatılır böylece toodebug, istiyor. Bu dosya konumu aşağıdaki hello bulunabilir: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``. Bu örnekte, hata ayıklama için bağlantı noktası 8001 ayarlanır.

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. Merhaba örnek sayısı ayarlayarak Hello uygulama bildirimi güncelleştirin veya hello yüklenmekte olan hello hizmeti için çoğaltma sayısını too1 hata ayıklaması. Bu ayar, hata ayıklama için kullanılan başlangıç bağlantı noktası için çakışmalarını önler. Örneğin, durum bilgisi olmayan hizmetler için ayarlar ``InstanceCount="1"`` ve boyutları too1 kümesi hello hedef ve min çoğaltma durum bilgisi olan hizmetler için aşağıdaki gibi ayarlayın: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.

4. Merhaba uygulamayı dağıtın.

5. Hello Eclipse IDE seçin **Çalıştır -> hata ayıklama yapılandırmaları uzak Java uygulaması -> ve giriş bağlantı özelliklerini** ve hello özelliklerini aşağıdaki gibi ayarlayın:

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  Merhaba uygulamada hata ayıklama ve istenen noktalarda kesme noktaları ayarlayın.

Merhaba uygulaması kilitlenen, tooenable coredumps da isteyebilirsiniz. Yürütme ``ulimit -c`` bir Kabuğu'nda ve 0 döndürür sonra coredumps etkin değil. tooenable sınırsız coredumps yürütme komutu aşağıdaki hello: ``ulimit -c unlimited``. Merhaba durum hello komutunu kullanarak da doğrulayabilirsiniz ``ulimit -a``.  Tooupdate hello coredump oluşturma yolu istediyseniz, yürütme ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``. 

### <a name="next-steps"></a>Sonraki adımlar

* [Linux Azure Tanılama'yı kullanarak günlükleri toplamak](service-fabric-diagnostics-how-to-setup-lad.md).
* [İzleme ve Hizmetleri yerel olarak tanılamak](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).
