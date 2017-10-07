---
title: "aaaVisualizing Service Fabric Explorer kullanarak kümenizi | Microsoft Docs"
description: "Service Fabric Explorer inceleme ve bulut uygulamaları ve Microsoft Azure Service Fabric kümesindeki düğümler yönetmek için bir web tabanlı araçtır."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Service Fabric Explorer ile kümenizi görselleştirme
Service Fabric Explorer inceleme ve uygulamaları ve bir Azure Service Fabric kümesindeki düğümler yönetmek için bir web tabanlı araçtır. Her zaman kümenizi nerede çalıştığına bakmaksızın kullanılabilir olması için Service Fabric Explorer doğrudan hello küme içinde barındırılır.

## <a name="video-tutorial"></a>Video öğretici

nasıl toouse Service Fabric Explorer izleme toolearn Microsoft Virtual Academy video aşağıdaki hello:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>TooService Fabric Explorer Bağlan
Çok hello yönergeleri izlediyseniz[geliştirme ortamınızı hazırlama](service-fabric-get-started.md), toohttp://localhost:19080 giderek yerel kümenizde Service Fabric Explorer başlatabilirsiniz / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Merhaba Service Fabric Explorer düzeni anlama
Service Fabric Explorer ile Merhaba solda hello ağacını kullanarak gidebilirsiniz. Merhaba ağaç Hello kökünde, hello küme Panosu uygulama ve düğüm durumu özetini dahil olmak üzere kümenizi genel bir bakış sağlar.

![Service Fabric Explorer küme Panosu][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Merhaba kümenin düzeni görüntüleyin
Bir Service Fabric kümesindeki düğümler hata etki alanı arasında iki boyutlu bir kılavuz yerleştirilir ve etki alanlarını yükseltme. Bu yerleştirme uygulamalarınızı ve donanım hatalarına uygulama yükseltmeleri hello bulunması kullanılabilir kalmasını sağlar. Nasıl hello geçerli küme hello küme eşlemesi kullanarak düzenlendiğini görüntüleyebilirsiniz.

![Service Fabric Explorer küme eşleme][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Görünüm uygulamaları ve Hizmetleri
Merhaba küme iki alt ağaçları içerir: biri uygulamaları ve diğer düğümleri için.

Service Fabric'ın mantıksal hiyerarşisi aracılığıyla hello uygulama görünümü toonavigate kullanabilirsiniz: uygulamaları, hizmetleri, bölümler ve çoğaltmalar.

Merhaba aşağıdaki örnekte, uygulama hello **Uygulamam** iki hizmetinden, oluşan **Mystatefulservice'ten** ve **WebService**. Bu yana **Mystatefulservice'ten** durum bilgisi olan bir birincil ve iki ikincil çoğaltma sahip bir bölüm içerir. Bunun aksine, WebSvcService durum bilgisiz ve tek bir örnek içerir.

![Service Fabric Explorer uygulama görünümü][sfx-application-tree]

Her hello ağacı düzeyinde hello ana bölmede hello öğe hakkında bilgileri gösterir. Örneğin, hello sistem durumunu ve belirli bir hizmet için sürüm görebilirsiniz.

![Service Fabric Explorer essentials bölmesi][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Merhaba kümenin düğümlerini görüntüleme
Merhaba düğümü görünüm hello küme hello fiziksel düzenini gösterir. Belirli bir düğümde, hangi uygulamalara kod dağıtıldığını denetleyebilirsiniz. Daha açık belirtmek gerekirse, çoğaltmalar var. çalışmakta görebilirsiniz.

## <a name="actions"></a>Eylemler
Service Fabric Explorer Eylemler düğümleri, uygulamaları ve Hizmetleri, küme içindeki bir hızlı yol tooinvoke sunar.

Örneğin, toodelete uygulama örneğini hello soldaki hello ağacından hello uygulamayı seçin ve ardından **Eylemler** > **uygulama Sil**.

![Bir Service Fabric Explorer'da uygulama silme][sfx-delete-application]

> [!TIP]
> Gerçekleştirebileceğiniz hello aynı eylemleri hello üç nokta sonraki tooeach öğeye tıklayarak.
>
>

Merhaba aşağıdaki tabloda her bir varlık için kullanılabilir hello eylemleri listeler:

| **Varlık** | **Eylem** | **Açıklama** |
| --- | --- | --- |
| Uygulama türü |Sağlamayı kaldırma türü |Merhaba uygulama paketi hello kümenin görüntü deposundan kaldırır. Bu tür toobe önce kaldırılan tüm uygulamaları gerektirir. |
| Uygulama |Uygulamayı Silme |Merhaba uygulaması, tüm hizmetler ve durumlarına (varsa) dahil olmak üzere silin. |
| Hizmet |Hizmet silme |Merhaba hizmeti ve durumuna (varsa) silin. |
| Node |Etkinleştir |Merhaba düğümü etkinleştirin. |
| Node | (Ara) devre dışı bırakma | Duraklatma hello düğüm, geçerli durumunda. Hizmetleri toorun devam ancak gerekli tooprevent kesinti veya veri tutarsızlığına olmadığı sürece Service Fabric proaktif olarak herhangi bir şey üzerine veya onu devre dışı taşımaz. İnceleme sırasında taşımayın belirli düğüm tooensure hizmetlerinde hata ayıklama genellikle kullanılan tooenable eylemdir. | |
| Node | (Yeniden) devre dışı bırakma | Güvenli bir şekilde tüm bellek içi Hizmetleri bir düğümü kapalı ve kalıcı Hizmetleri kapatın taşıyın. Genellikle, Hello ana bilgisayar işlemlerini veya makine gerek toobe başlatıldığında kullanılır. | |
| Node | (Verileri Kaldır) devre dışı bırakma | Güvenli bir şekilde yeterli yedek çoğaltmaları oluşturduktan sonra hello düğüm üzerinde çalışan tüm hizmetleri kapatın. Genellikle bir düğümü kullanılır (veya en az depolama alanı) dışında Komisyonu kalıcı olarak kullanıldığını. | |
| Node | Düğüm durumu Kaldır | Bir düğümün çoğaltmaları bilgisi hello kümeden kaldırın. Genellikle, zaten başarısız olan bir düğümün kurtarılamaz kabul edilir olduğunda kullanılır. | |
| Node | Yeniden Başlatma | Bir düğüm hello düğümü yeniden başlatarak arızanın benzetimini gerçekleştirin. Daha fazla bilgi [burada](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Birçok Eylemler bozucu olduğundan, olabilir hello işlem tamamlanmadan önce tooconfirm maksadınızı istedi.

> [!TIP]
> Service Fabric Explorer gerçekleştirilebilir her eylem, PowerShell veya tooenable Otomasyon bir REST API'si gerçekleştirilebilir.
>
>

Service Fabric Explorer toocreate uygulama örnekleri, verilen uygulama türü ve sürümü için de kullanabilirsiniz. Merhaba ağaç görünümünde Hello uygulama türünü seçin ve ardından hello **oluşturma uygulama örneği** gibi hello sağ bölmede bağlantı sonraki toohello sürümü.

![Service Fabric Explorer'da uygulama örneğini oluşturma][sfx-create-app-instance]

> [!NOTE]
> Service Fabric Explorer ile oluşturulan uygulama örnekleri şu anda parametreli olamaz. Bunlar, varsayılan parametre değerleri kullanılarak oluşturulur.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Tooa uzak Service Fabric kümesi Bağlan
Merhaba kümenin endpoint biliyor ve yeterli izinlere sahip herhangi bir tarayıcıdan Service Fabric Explorer erişebilir. Service Fabric Explorer hello kümede çalışan başka bir hizmete olmasıdır.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Uzak bir küme için Hello Service Fabric Explorer uç noktası bulunamadı
belirli bir küme için Service Fabric Explorer tooreach tarayıcınıza noktası:

http://&lt;küme endpoint bilgisayarınızı&gt;: 19080/Explorer

Azure kümeleri için hello tam URL'yi de hello küme essentials bölmesinde hello Azure portalında kullanılabilir.

### <a name="connect-tooa-secure-cluster"></a>Tooa güvenli kümesine bağlanın
İstemci erişim tooyour Service Fabric kümesi, sertifikalar veya Azure Active Directory (AAD) kullanarak kontrol edebilirsiniz.

Güvenli bir kümede tooconnect tooService Fabric Explorer çalışırsanız, sonra hello kümenin yapılandırmasına bağlı olarak, gerekli toopresent bir istemci sertifikası veya AAD kullanarak oturum açın.

## <a name="next-steps"></a>Sonraki adımlar
* [Test Edilebilirlik genel bakış](service-fabric-testability-overview.md)
* [Visual Studio'da, Service Fabric uygulamaları yönetme](service-fabric-manage-application-in-visual-studio.md)
* [PowerShell kullanarak Service Fabric uygulama dağıtımı](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
