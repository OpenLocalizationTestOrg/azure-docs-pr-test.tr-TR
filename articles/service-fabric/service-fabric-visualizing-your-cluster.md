---
title: "Azure Service Fabric Explorer kullanarak kümenizi Görselleştirme | Microsoft Docs"
description: "Service Fabric Explorer inceleme ve bulut uygulamaları ve Microsoft Azure Service Fabric kümesindeki düğümler yönetmek için bir uygulamadır."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/08/2018
ms.author: mikhegn
ms.openlocfilehash: 34e00058591bc5a0a02bc408cfc3fcc11010f17c
ms.sourcegitcommit: 384d2ec82214e8af0fc4891f9f840fb7cf89ef59
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/16/2018
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Service Fabric Explorer ile kümenizi görselleştirme

Service Fabric Explorer (SFX) inceleme ve Azure Service Fabric kümeleri yönetmek için bir açık kaynak aracıdır. Service Fabric Explorer, Windows ve Linux için bir masaüstü uygulamasıdır. MacOS desteği yakında geliyor.

## <a name="service-fabric-explorer-download"></a>Service Fabric Explorer indirme

Service Fabric Explorer masaüstü uygulaması olarak indirmek için aşağıdaki bağlantıları kullanın:

- Windows
  - https://aka.ms/sfx-windows

- Linux
  - https://aka.ms/sfx-linux-x86
  - https://aka.ms/sfx-linux-x64

> [!NOTE]
> Service Fabric Explorer'ın Masaüstü sürümünü küme desteği az veya daha fazla özelliğe sahip olabilir. Tam özellik uyumluluğundan emin olmak için kümeye dağıtılan Service Fabric Explorer sürümüne geri dönebilir.
>
>

### <a name="running-service-fabric-explorer-from-the-cluster"></a>Service Fabric Explorer kümeden çalıştırma

Service Fabric Explorer ayrıca bir Service Fabric kümenin HTTP yönetim uç barındırılır. Kümenin HTTP yönetim uç noktasına SFX bir web tarayıcısında başlatın, herhangi bir tarayıcıdan - örneğin https://clusterFQDN:19080 göz atın.

Geliştirici iş istasyonu kurulumu için http://localhost: 19080/Explorer giderek yerel kümenizde Service Fabric Explorer başlatabilirsiniz. Bu makalede bakabilir [geliştirme ortamınızı hazırlama](service-fabric-get-started.md).

## <a name="connect-to-a-service-fabric-cluster"></a>Service Fabric kümeye bağlanın
Bir Service Fabric kümeye bağlanmak için küme yönetim uç noktası'nı (FQDN/IP) ve HTTP yönetim uç nokta bağlantı noktası (varsayılan olarak 19080) gerekir. Örneğin https://mysfcluster.westus.cloudapp.azure.com:19080. İstasyonunuzda yerel kümeye bağlanmak için "Localhost'a Bağlan" onay kutusunu kullanın.

### <a name="connect-to-a-secure-cluster"></a>Güvenli bir kümeye bağlanma
Service Fabric kümenize, sertifikalar veya Azure Active Directory (AAD) kullanarak, istemci erişimi denetleyebilirsiniz.

Güvenli bir kümeye bağlanmaya çalışırsanız, sonra küme yapılandırmasına bağlı olarak, bir istemci sertifikası sunan veya AAD kullanarak oturum gerekecektir.

## <a name="video-tutorial"></a>Video öğretici

Service Fabric Explorer kullanmayı öğrenmek için aşağıdaki Microsoft Virtual Academy videoyu izleyin:

> [!NOTE]
> Bu videoda, Service Fabric Explorer değil Masaüstü sürümünü bir Service Fabric kümesi içinde barındırılan gösterir.
>
>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="understand-the-service-fabric-explorer-layout"></a>Service Fabric Explorer düzeni anlama
Soldaki ağaç kullanarak Service Fabric Explorer gidebilirsiniz. Ağaç kökünde küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.

![Service Fabric Explorer küme Panosu][sfx-cluster-dashboard]

### <a name="view-the-clusters-layout"></a>Kümenin düzeni görüntüleyin
Bir Service Fabric kümesindeki düğümler hata etki alanı arasında iki boyutlu bir kılavuz yerleştirilir ve etki alanlarını yükseltme. Bu yerleştirme uygulamalarınızı donanım hataları ve uygulama yükseltmelerini varlığında kullanılabilir kalmasını sağlar. Nasıl geçerli Küme Küme eşlemesi kullanarak düzenlendiğini görüntüleyebilirsiniz.

![Service Fabric Explorer küme eşleme][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Görünüm uygulamaları ve Hizmetleri
Küme iki alt ağaçları içerir: biri uygulamaları ve diğer düğümleri için.

Service Fabric'ın mantıksal hiyerarşide gezinmek için uygulama görünümü kullanabilirsiniz: uygulamaları, hizmetleri, bölümler ve çoğaltmalar.

Uygulama aşağıdaki örnekte **Uygulamam** iki hizmetinden, oluşan **Mystatefulservice'ten** ve **WebService**. Bu yana **Mystatefulservice'ten** durum bilgisi olan bir birincil ve iki ikincil çoğaltma sahip bir bölüm içerir. Bunun aksine, WebSvcService durum bilgisiz ve tek bir örnek içerir.

![Service Fabric Explorer uygulama görünümü][sfx-application-tree]

Her ağacı düzeyinde ana bölmede öğe hakkında bilgileri gösterir. Örneğin, belirli bir hizmet için sürüm ve sistem durumunu görebilirsiniz.

![Service Fabric Explorer essentials bölmesi][sfx-service-essentials]

### <a name="view-the-clusters-nodes"></a>Küme düğümlerini görüntüleme
Düğüm görünümü, kümenin fiziksel düzenini gösterir. Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz. Daha açık belirtmek gerekirse, çoğaltmalar var. çalışmakta görebilirsiniz.

## <a name="actions"></a>Eylemler
Service Fabric Explorer düğümleri, uygulamaları ve Hizmetleri, küme içindeki eylemleri çağırmak için hızlı bir yol sunar.

Örneğin, bir uygulama örneği silmek için soldaki ağaç uygulamayı seçin ve ardından **Eylemler** > **uygulama Sil**.

![Bir Service Fabric Explorer'da uygulama silme][sfx-delete-application]

> [!TIP]
> Her öğe yanındaki üç nokta işaretine tıklayarak aynı eylemleri gerçekleştirebilirsiniz.
>
> Service Fabric Explorer gerçekleştirilebilir her eylem otomasyonunu sağlamak için PowerShell veya bir REST API'si gerçekleştirilebilir.
>
>

Service Fabric Explorer, verilen uygulama türü ve sürümü için uygulama örnekleri oluşturmak için de kullanabilirsiniz. Ağaç görünümünde uygulama türünü seçin ve ardından **oluşturma uygulama örneği** gibi sağ bölmede sürüm yanındaki bağlantı.

![Service Fabric Explorer'da uygulama örneğini oluşturma][sfx-create-app-instance]

> [!NOTE]
> Uygulama örnekleri oluştururken Service Fabric Explorer parametreleri desteklemez. Uygulama örnekleri varsayılan parametre değerlerini kullanın.
>
>

## <a name="next-steps"></a>Sonraki adımlar
* [Visual Studio'da, Service Fabric uygulamaları yönetme](service-fabric-manage-application-in-visual-studio.md)
* [PowerShell kullanarak Service Fabric uygulama dağıtımı](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png