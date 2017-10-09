---
title: "Service Fabric kümesi güvenlik: istemci rolleri | Microsoft Docs"
description: "Bu makalede hello iki istemci rolleri ve toohello rolleri sağlanan hello izinleri açıklar."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: coreysa
editor: 
ms.assetid: 7bc808d9-3609-46a1-ac12-b4f53bff98dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4a4a9f93e91ea816005b730bebbcb317f8bab255
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-for-service-fabric-clients"></a>Service Fabric istemciler için rol tabanlı erişim denetimi
Azure Service Fabric bağlı tooa Service Fabric kümesi istemciler için iki farklı erişim denetim türlerini destekler: Yönetici ve kullanıcı. Erişim denetimi hello Küme Yöneticisi toolimit erişim toocertain küme işlemleri farklı hello küme daha güvenli hale getirme kullanıcı grupları için sağlar.  

**Yöneticiler** (okuma/yazma özellikleri dahil) tam erişim toomanagement özelliklere sahiptir. Varsayılan olarak, **kullanıcılar** yalnızca okuma erişimi toomanagement özellikleri (örneğin, sorgu özellikleri) ve hello özelliği tooresolve uygulamaları ve Hizmetleri gerekir.

Her biri için ayrı sertifikaların sağlayarak hello küme oluşturma sırasında hello iki istemci rolleri (Yönetici ve istemci) belirtin. Bkz: [Service Fabric kümesi güvenlik](service-fabric-cluster-security.md) güvenli bir Service Fabric kümesi ayarlama hakkında bilgi.

## <a name="default-access-control-settings"></a>Varsayılan erişim denetimi ayarları
Hello Yöneticisi erişim denetimi türünü tam erişim tooall hello FabricClient API'leri sahiptir. Merhaba işlemler aşağıdaki gibi hello Service Fabric kümesi tüm okuma ve yazma işlemleri gerçekleştirebilirsiniz:

### <a name="application-and-service-operations"></a>Uygulama ve hizmet işlemleri
* **CreateService**: hizmet oluşturma                             
* **CreateServiceFromTemplate**: hizmet şablonundan oluşturma                             
* **UpdateService**: hizmet güncelleştirmeleri                             
* **DeleteService**: Hizmet silme                             
* **ProvisionApplicationType**: uygulama sağlama türünü                             
* **CreateApplication**: uygulama oluşturma                               
* **DeleteApplication**: uygulama silme                             
* **UpgradeApplication**: başlatılması veya uygulama yükseltmelerini kesintiye                             
* **UnprovisionApplicationType**: uygulama türü sağlamanın kaldırılması                             
* **MoveNextUpgradeDomain**: uygulama yükseltmelerini açıkça güncelleştirme etki alanı ile sürdürülüyor                             
* **ReportUpgradeHealth**: uygulama yükseltmelerini hello geçerli yükseltme ilerleme durumu ile sürdürülüyor                             
* **ReportHealth**: sistem durumu raporlama                             
* **PredeployPackageToNode**: dağıtım öncesi API                            
* **CodePackageControl**: kod paketler yeniden başlatılıyor                             
* **RecoverPartition**: bir bölüm kurtarma                             
* **RecoverPartitions**: bölümleri kurtarma                             
* **RecoverServicePartitions**: hizmet bölümlerini kurtarma                             
* **RecoverSystemPartitions**: sistem hizmeti bölümleri kurtarma                             

### <a name="cluster-operations"></a>Küme işlemleri
* **ProvisionFabric**: MSI ve/veya küme bildirim sağlama                             
* **UpgradeFabric**: Küme yükseltme başlatılıyor                             
* **UnprovisionFabric**: MSI ve/veya küme bildirimi sağlamanın kaldırılması                         
* **MoveNextFabricUpgradeDomain**: Küme yükseltme açıkça güncelleştirme etki alanı ile sürdürülüyor                             
* **ReportFabricUpgradeHealth**: Küme yükseltme hello geçerli yükseltme ilerleme durumu ile sürdürülüyor                             
* **StartInfrastructureTask**: altyapı görevleri başlatma                             
* **FinishInfrastructureTask**: altyapı görevleri tamamlama                             
* **InvokeInfrastructureCommand**: altyapı görev yönetimi komutları                              
* **ActivateNode**: bir düğümü etkinleştirme                             
* **DeactivateNode**: bir düğümü devre dışı bırakma                             
* **DeactivateNodesBatch**: birden çok düğüm devre dışı bırakma                             
* **RemoveNodeDeactivations**: birden çok düğümde geri alma devre dışı bırakma                             
* **GetNodeDeactivationStatus**: devre dışı bırakma durumu denetleniyor                             
* **NodeStateRemoved**: düğüm durumu raporlama kaldırıldı                             
* **ReportFault**: hata raporlama                             
* **FileContent**: Image store istemcisi dosya aktarımı (Dış toocluster)                             
* **FileDownload**: Image store istemcisi dosya indirme başlatma (Dış toocluster)                             
* **InternalList**: görüntü deposu istemci dosya listesi işlemi (iç)                             
* **Silme**: görüntü deposu istemci silme işlemi                              
* **Karşıya yükleme**: Image store istemcisi karşıya yükleme işlemi                             
* **NodeControl**: başlatma, durdurma ve düğüm yeniden başlatma                             
* **MoveReplicaControl**: bir düğümü tooanother çoğaltmaları taşıma                             

### <a name="miscellaneous-operations"></a>Çeşitli işlemler
* **Ping**: istemci ping isteği                             
* **Sorgu**: izin verilen tüm sorgular
* **NameExists**: URI varlığı denetimleri adlandırma                             

Merhaba kullanıcı erişim denetimi türü varsayılan olarak, aşağıdaki işlemleri sınırlı toohello verilmiştir: 

* **EnumerateSubnames**: URI numaralandırması adlandırma                             
* **EnumerateProperties**: özellik numaralandırma adlandırma                             
* **PropertyReadBatch**: özellik adlandırma okuma işlemleri                             
* **GetServiceDescription**: uzun yoklama hizmet bildirimleri ve okuma hizmeti açıklamaları                             
* **ResolveService**: hizmet uyumlu tabanlı çözümleme                             
* **ResolveNameOwner**: çözümleme adlandırma URI'si sahibi                             
* **ResolvePartition**: Sistem Hizmetleri çözme                             
* **ServiceNotifications**: olay tabanlı hizmet bildirimleri                             
* **GetUpgradeStatus**: Uygulama yükseltme durumunu yoklama                             
* **GetFabricUpgradeStatus**: Küme yükseltme durumunu yoklama                             
* **InvokeInfrastructureQuery**: altyapısı görevlerini sorgulama                             
* **Liste**: görüntü deposu istemci dosya listesi işlemi                             
* **ResetPartitionLoad**: bir yük devretme biriminin yükünü sıfırlama                             
* **ToggleVerboseServicePlacementHealthReporting**: ayrıntılı hizmet sistem durumu yerleştirme raporlama geçiş                             

Merhaba yönetici erişim denetimi işlemleri önceki erişim toohello de vardır.

## <a name="changing-default-settings-for-client-roles"></a>İstemci rolleri için varsayılan ayarlarını değiştirme
Merhaba küme bildirim dosyasında, gerekirse, yönetim yetenekleri toohello istemci sağlayabilirsiniz. Giden toohello tarafından hello Varsayılanları değiştirebilirsiniz **yapı ayarları** sırasında seçeneği [küme oluşturma](service-fabric-cluster-creation-via-portal.md), hello ayarları önceki hello sağlayarak ve **adı**, **yönetici**, **kullanıcı**, ve **değeri** alanları.

## <a name="next-steps"></a>Sonraki adımlar
[Service Fabric kümesi güvenliği](service-fabric-cluster-security.md)

[Service Fabric kümesi oluşturma](service-fabric-cluster-creation-via-portal.md)

