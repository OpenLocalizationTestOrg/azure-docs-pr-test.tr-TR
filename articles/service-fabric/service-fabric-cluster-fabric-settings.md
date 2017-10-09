---
title: "aaaChange Azure Service Fabric kümesi ayarlarını | Microsoft Docs"
description: "Bu makalede hello yapı ayarları ve özelleştirebileceğiniz hello doku yükseltme ilkeleri açıklanır."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: 
ms.assetid: 7ced36bf-bd3f-474f-a03a-6ebdbc9677e2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: chackdan
ms.openlocfilehash: a8b125f7b4a02547cf4bcf2c936d0c7f1686c1a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-service-fabric-cluster-settings-and-fabric-upgrade-policy"></a>Service Fabric kümesi ayarlarını ve yapı yükseltme İlkesi özelleştirme
Bu belge toocustomize nasıl hello çeşitli yapı ayarları ve hello doku yükseltme ilkesi için Service Fabric kümesi söyler. Bunları hello portalı veya bir Azure Resource Manager şablonu kullanarak özelleştirebilirsiniz.

> [!NOTE]
> Tüm ayarları hello portalı yoluyla kullanılabilir. Aşağıda listelenen bir ayar hello portalı yoluyla kullanılamaz durumda bir Azure Resource Manager şablonu kullanarak özelleştirin.
> 

## <a name="customizing-service-fabric-cluster-settings-using-azure-resource-manager-templates"></a>Azure Resource Manager şablonları kullanarak Service Fabric kümesi ayarlarını özelleştirme
Merhaba adımları göstermek nasıl tooadd yeni bir ayar *MaxDiskQuotaInMB* toohello *tanılama* bölümü.

1. Toohttps://resources.Azure.com gidin
2. Genişleterek tooyour abonelik gidin abonelikleri -> kaynak grupları -> Microsoft.ServiceFabric -> Küme adı
3. Merhaba sağ üst köşede, "Okuma/yazma" seçin
4. Düzenle'yi seçin ve güncelleştirme hello `fabricSettings` JSON öğesi ve yeni bir öğe ekleyin

```
      {
        "name": "Diagnostics",
        "parameters": [
          {
            "name": "MaxDiskQuotaInMB",
            "value": "65536"
          }
        ]
      }
```

## <a name="fabric-settings-that-you-can-customize"></a>Özelleştirebileceğiniz yapı ayarları
Özelleştirebileceğiniz hello yapı ayarları şunlardır:

### <a name="section-name-diagnostics"></a>Bölüm adı: Tanılama
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ConsumerInstances |Dize |Merhaba DCA tüketici örneklerinin listesi. |
| ProducerInstances |Dize |Merhaba DCA üretici örneklerinin listesi. |
| AppEtwTraceDeletionAgeInDays |Int, varsayılan 3. |Daha sonra şu uygulama ETW izlemelerini içeren eski ETL dosyaları silmek gün sayısı. |
| AppDiagnosticStoreAccessRequiresImpersonation |Bool, varsayılan değer true şeklindedir |Desteklemediğini tanılama erişme hello uygulama adına depoladığında kimliğe bürünme gereklidir. |
| MaxDiskQuotaInMB |Int, 65536 varsayılandır |Disk kotası Windows Fabric MB günlük dosyalarında. |
| DiskFullSafetySpaceInMB |Int, varsayılan 1024'tür. |MB tooprotect DCA tarafından kullanımdan kalan disk alanı. |
| ApplicationLogsFormatVersion |Int, varsayılan 0'dır |Uygulama için sürüm biçimi günlüğe kaydeder. 0 ve 1 değerleri desteklenir. Sürüm 1, 0 sürümden daha fazla hello ETW olay kaydı alanları içerir. |
| ClusterId |Dize |Merhaba hello kümenin benzersiz kimliği. Merhaba küme oluşturulduğunda oluşturulur. |
| EnableTelemetry |Bool, varsayılan değer true şeklindedir |Bu tooenable giderek veya telemetri devre dışı bırakın. |
| EnableCircularTraceSession |Bool, varsayılan false |Bayrak döngüsel izleme oturumlarını kullanılması gerekip gerekmediğini belirtir. |

### <a name="section-name-traceetw"></a>Bölüm adı: İzleme/Etw
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| Düzey |Int, varsayılan 4'tür |Değerler 1, izleme etw düzey alabilir 2, 3, 4. desteklenen toobe konumundaki 4 hello izleme düzeyi tutmanız gerekir |

### <a name="section-name-performancecounterlocalstore"></a>Bölüm adı: PerformanceCounterLocalStore
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| IsEnabled |Bool, varsayılan değer true şeklindedir |Bayrağı, performans sayacı toplama yerel düğümünde etkinleştirilip etkinleştirilmeyeceğini gösterir. |
| SamplingIntervalInSeconds |Int, 60 varsayılandır |Toplanmakta olan performans sayaçları için örnekleme aralığı. |
| Sayaçları |Dize |Performans sayaçları toocollect virgülle ayrılmış listesi. |
| MaxCounterBinaryFileSizeInMB |Int, varsayılan 1. |Her performans sayacı ikili dosya için maksimum boyut (MB cinsinden). |
| NewCounterBinaryFileCreationIntervalInMinutes |Int, varsayılan 10'dur |Daha sonra yeni bir performans sayacı ikili dosyası oluşturulur üst aralığı (saniye cinsinden). |

### <a name="section-name-setup"></a>Bölüm adı: Kurulumu
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| FabricDataRoot |Dize |Service Fabric veri kök dizini. Varsayılan Azure d:\svcfab için |
| FabricLogRoot |Dize |Service fabric günlük kök dizini. BT günlüklerine ve izlemelere yerleştirildiği budur. |
| ServiceRunAsAccountName |Dize |Merhaba hesap adı altında hangi toorun doku ana bilgisayar hizmeti. |
| ServiceStartupType |Dize |Merhaba hello doku ana bilgisayar hizmeti başlangıç türü. |
| SkipFirewallConfiguration |Bool, varsayılan false |Güvenlik Duvarı ayarlarını toobe gerekip gerekmediğini belirtir veya hello sistemi tarafından ayarlanmış. Bu, yalnızca windows güvenlik duvarı kullanıyorsanız geçerlidir. Ardından üçüncü taraf güvenlik duvarları kullanıyorsanız, hello sistemi ve uygulamalar toouse hello bağlantı noktalarını açmanız gerekir |

### <a name="section-name-transactionalreplicator"></a>Bölüm adı: TransactionalReplicator
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| MaxCopyQueueSize |Uint, 16384 varsayılandır |Bu hello en büyük değer olan çoğaltma işlemleri tutar hello sıranın hello ilk boyutunu tanımlar. 2'in üssü olması gerektiğini unutmayın. Çalışma zamanı sırasında hello sıra büyürse toothis boyutu işlemleri arasında hello birincil ve ikincil çoğaltıcılar kısıtlanacak. |
| BatchAcknowledgementInterval | Zamanı saniye cinsinden 0,015 varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba geri onay göndermeden önce bir işlem aldıktan sonra çoğaltıcı bekler hello süre miktarını belirler. Bu süre içinde alınan diğer işlemleri azalan ağ trafiğini ancak hello çoğaltıcı potansiyel olarak azalan hello verimini -> tek bir iletide gönderilen kendi onayları sahip olur. |
| MaxReplicationMessageSize |Uint 52428800 varsayılandır | Çoğaltma işlemleri maksimum ileti boyutu. Varsayılan 50 MB'dir. |
| ReplicatorAddress |Varsayılan "localhost:0" dizesidir | bir dize-'hello Windows Fabric çoğaltması tooestablish bağlantılar diğer yinelemelerle sıralı toosend/alma işlemler tarafından kullanılan IP: BağlantıNoktası' biçiminde Hello uç noktası. |
| InitialPrimaryReplicationQueueSize |Uint, varsayılan 64'tür. | Bu değer hello başlangıç boyutu hello hello çoğaltma işlemleri birincil tutar hello sırasının olarak tanımlar. 2'in üssü olması gerektiğini unutmayın.|
| MaxPrimaryReplicationQueueSize |Uint, 8192 varsayılandır |Bu hello maksimum hello birincil çoğaltma sırada mevcut işlemleri sayısıdır. 2'in üssü olması gerektiğini unutmayın. |
| MaxPrimaryReplicationQueueMemorySize |Uint, varsayılan 0'dır |Merhaba birincil çoğaltma sırası bayt cinsinden en büyük değerini hello budur. |
| InitialSecondaryReplicationQueueSize |Uint, varsayılan 64'tür. |Bu değer hello başlangıç boyutu hello hello çoğaltma işlemleri İkincil tutar hello sırasının olarak tanımlar. 2'in üssü olması gerektiğini unutmayın. |
| MaxSecondaryReplicationQueueSize |Uint, 16384 varsayılandır |Bu hello maksimum hello ikincil çoğaltma sırada mevcut işlemleri sayısıdır. 2'in üssü olması gerektiğini unutmayın. |
| MaxSecondaryReplicationQueueMemorySize |Uint, varsayılan 0'dır |Merhaba ikincil çoğaltma sırası bayt cinsinden en büyük değerini hello budur. |
| SecondaryClearAcknowledgedOperations |Bool, varsayılan false |Bunlar toohello birincil (temizlenmiş toohello disk) onaylanan sonra hello ikincil çoğaltıcı hello işlemleri kaldırdıysanız, denetimleri Bool. Ayarları bu tooTRUE bir yük devretme sonrasında çoğaltmaları yedeklemek yakalama sırasında hello yeni birincil üzerinde ek disk okuma neden olabilir. |
| MaxMetadataSizeInKB |Int, varsayılan 4'tür |Merhaba günlük akışı meta verisi en büyük boyutu. |
| MaxRecordSizeInKB |Uint, varsayılan 1024'tür. | Bir günlük akışı kaydı en büyük boyutu. |
| CheckpointThresholdInMB |Int, varsayılan 50'dir |Merhaba günlük kullanımı bu değeri aştığında bir denetim noktası başlatılmayacak. |
| MaxAccumulatedBackupLogSizeInMB |Int, 800 varsayılandır |En büyük boyutunu (MB) verilen yedek günlüğü zinciri yedekleme günlüklerinde toplanan. Merhaba artımlı yedekleme birikmiş hello yedekleme günlükleri hello ilgili tam yedekleme toobe bu boyuttan daha büyük itibaren neden olacak bir yedekleme günlüğü oluşturur bir artımlı yedekleme istekleri başarısız olur. Böyle durumlarda, kullanıcı gerekli tootake tam yedekleme ' dir. |
| MaxWriteQueueDepthInKB |Int, varsayılan 0'dır | Maksimum Int yazma sıra derinliği bu hello çekirdek Günlükçü Bu çoğaltma ile ilişkili hello günlüğü için kilobayt cinsinden belirtilen olarak kullanabilirsiniz. Bu değer hello maksimum çekirdek Günlükçü güncelleştirmeleri sırasında bekleyen bayt sayısıdır. Merhaba çekirdek için Günlükçü toocompute uygun bir değer veya 4 birden fazla 0 olabilir. |
| SharedLogId |Dize |Paylaşılan günlük tanımlayıcısı. Bu bir GUID ve paylaşılan her oturum için benzersiz olmalıdır. |
| SharedLogPath |Dize |Yol toohello paylaşılan günlüğü. Bu değer boş ise hello varsayılan paylaşılan günlüğü kullanılır. |
| SlowApiMonitoringDuration |Zaman içinde varsayılan 300 saniyedir | Uyarı sistem durumu olayı tetiklenir önce API için süreyi belirtin.|
| MinLogSizeInMB |Int, varsayılan 0'dır |Merhaba işlem günlüğü minimum boyutu. Merhaba günlük tootruncate tooa boyutunun bu ayarı altında izin verilmiyor. 0, o hello çoğaltıcı tooother ayarları göre hello en küçük günlük boyutu belirleyecek gösterir. Bu değer artırıldığında kısmi kopyalar ve artımlı yedeklemeler kesilmesine azaltıldığı ilgili günlük kayıtları olasılığını itibaren yapmanın hello olasılığı artar. |

### <a name="section-name-fabricclient"></a>Bölüm adı: FabricClient
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| NodeAddresses |dize, varsayılan değer "" |Adresleri (bağlantı dizeleri) hello hello Naming Service ile kullanılan toocommunicate olabilir farklı düğümlerde koleksiyonu. Başlangıçta hello adresleri birini rastgele seçerek istemci bağlanır hello. Birden fazla bağlantı dizesi tarafından sağlanan ve bir bağlantı iletişimi veya zaman aşımı hatası nedeniyle başarısız olursa; Merhaba istemci toouse hello sonraki adresi sıralı olarak geçer. Ayrıntılar için Hello adlandırma hizmeti adresi yeniden deneme bölümüne yeniden deneme semantiği üzerinde bakın. |
| ConnectionInitializationTimeout |Zamanı saniye cinsinden varsayılan 2'dir |TimeSpan saniye cinsinden belirtin. Bağlantı zaman aşımı aralığı her zaman istemci tooopen bir bağlantı toohello ağ geçidi çalışır. |
| PartitionLocationCacheLimit |Int, 100000 varsayılandır |Hizmet çözümlemesi için önbelleğe alınmış bölüm sayısı (sınır too0 ayarlayın). |
| ServiceChangePollInterval |Zamanı saniye cinsinden varsayılan 120'dir |TimeSpan saniye cinsinden belirtin. hizmet için ardışık yoklamalar Hello aralığını hello istemci toohello kayıtlı hizmet değişiklik bildirimleri geri aramalar için ağ geçidi değiştirilir. |
| KeepAliveIntervalInSeconds |Int, varsayılan 20'dir |Merhaba aralığı FabricClient hangi hello taşıma etkin tutma iletileri toohello ağ geçidi gönderir. İçin 0; keepAlive devre dışı bırakılır. Pozitif bir değer olmalıdır. |
| HealthOperationTimeout |Zamanı saniye cinsinden varsayılan 120'dir |TimeSpan saniye cinsinden belirtin. bir rapor iletisi için Hello zaman aşımı tooHealth Yöneticisi gönderdi. |
| HealthReportSendInterval |Zamanı saniye cinsinden varsayılan 30'dur |TimeSpan saniye cinsinden belirtin. hangi Raporlama bileşeni gönderir birikmiş sistem durumu raporları tooHealth Yöneticisi Hello aralık. |
| HealthReportRetrySendInterval |Zamanı saniye cinsinden varsayılan 30'dur |TimeSpan saniye cinsinden belirtin. hangi Raporlama bileşeni birikmiş yeniden gönderir sistem durumu raporları tooHealth Yöneticisi Hello aralık. |
| RetryBackoffInterval |Zamanı saniye cinsinden varsayılan 3. |TimeSpan saniye cinsinden belirtin. Merhaba işlemi yeniden denemeden önce hello geri alma aralığı. |
| MaxFileSenderThreads |Uint, varsayılan 10'dur |Merhaba max paralel olarak aktarılan dosya sayısı. |

### <a name="section-name-common"></a>Bölüm adı: Genel
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| PerfMonitorInterval |Zamanı saniye olarak varsayılan 1. |TimeSpan saniye cinsinden belirtin. Performans izleme aralığı. Ayar too0 veya negatif değer izlemeyi devre dışı bırakır. |

### <a name="section-name-healthmanager"></a>Bölüm adı: HealthManager
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| EnableApplicationTypeHealthEvaluation |Bool, varsayılan false |Küme sistem durumu değerlendirme İlkesi: uygulama türünü sistem durumu değerlendirmesi etkinleştirin. |

### <a name="section-name-fabricnode"></a>Bölüm adı: FabricNode
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| StateTraceInterval |Zaman içinde varsayılan 300 saniyedir |TimeSpan saniye cinsinden belirtin. İzleme düğümü durumu her düğümde ve FM/FMM düğümlerinde yedeklemek için hello aralığı. |

### <a name="section-name-nodedomainids"></a>Bölüm adı: NodeDomainIds
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| UpgradeDomainId |dize, varsayılan değer "" |Bir düğüm hello yükseltme etki alanına ait açıklar. |
| PropertyGroup |NodeFaultDomainIdCollection |Bir düğüme ait hello hata etki alanlarını açıklar. Merhaba hata etki alanı hello datacenter hello düğümünde hello konumunu tanımlayan bir URI ile tanımlanır.  Hata etki alanı URI'ler olan Merhaba fd biçimlendirmek: / fd/ardından tarafından URI yol kesimi.|

### <a name="section-name-nodeproperties"></a>Bölüm adı: NodeProperties
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| PropertyGroup |NodePropertyCollectionMap |Düğüm özellikleri anahtar-değer çiftleri koleksiyonu. |

### <a name="section-name-nodecapacities"></a>Bölüm adı: NodeCapacities
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| PropertyGroup |NodeCapacityCollectionMap |Farklı ölçümleri için düğüm kapasiteler koleksiyonu. |

### <a name="section-name-fabricnode"></a>Bölüm adı: FabricNode
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| StartApplicationPortRange |Int, varsayılan 0'dır |Alt sistemi barındırma tarafından yönetilen hello uygulama bağlantı noktalarını başlangıcı. EndpointFilteringEnabled içinde barındırma true ise gereklidir. |
| EndApplicationPortRange |Int, varsayılan 0'dır |Merhaba uygulama bağlantı noktalarının alt sistemi barındırma tarafından yönetilen son (Hayır dahil). EndpointFilteringEnabled içinde barındırma true ise gereklidir. |
| ClusterX509StoreName |dize, varsayılan değer "Benim" |Küme içi iletişimi korumak için küme sertifikasını içeren X.509 Sertifika deposu adı. |
| ClusterX509FindType |Varsayılan "FindByThumbprint" dizesidir |Nasıl ClusterX509StoreName desteklenen değerlerle toosearch hello deposunda küme sertifikası için belirtilen belirtir: "FindByThumbprint"; "FindBySubjectName" ile "FindBySubjectName"; birden çok eşleşme; olduğunda Merhaba en son kullanma tarihi olan Hello kullanılır. |
| ClusterX509FindValue |dize, varsayılan değer "" |Arama filtresi değeri toolocate küme sertifika kullanılır. |
| ClusterX509FindValueSecondary |dize, varsayılan değer "" |Arama filtresi değeri toolocate küme sertifika kullanılır. |
| ServerAuthX509StoreName |dize, varsayılan değer "Benim" |Başlangıç hizmeti için sunucu sertifikası içeriyor X.509 Sertifika deposu adı. |
| ServerAuthX509FindType |Varsayılan "FindByThumbprint" dizesidir |Nasıl ServerAuthX509StoreName desteklenen değeriyle toosearch hello deposunda sunucu sertifikası için belirtilen gösterir: FindByThumbprint; FindBySubjectName. |
| ServerAuthX509FindValue |dize, varsayılan değer "" |Arama filtresi değeri toolocate sunucu sertifikası kullanılır. |
| ServerAuthX509FindValueSecondary |dize, varsayılan değer "" |Arama filtresi değeri toolocate sunucu sertifikası kullanılır. |
| ClientAuthX509StoreName |dize, varsayılan değer "Benim" |Varsayılan Yönetici rolü FabricClient sertifikasını içeren hello X.509 Sertifika deposu adı. |
| ClientAuthX509FindType |Varsayılan "FindByThumbprint" dizesidir |Nasıl hello deposundaki sertifikayı toosearch ClientAuthX509StoreName desteklenen değeri tarafından belirtilen gösterir: FindByThumbprint; FindBySubjectName. |
| ClientAuthX509FindValue |dize, varsayılan değer "" | Arama filtresi değeri toolocate sertifika varsayılan Yönetici rolü FabricClient için kullanılır. |
| ClientAuthX509FindValueSecondary |dize, varsayılan değer "" |Arama filtresi değeri toolocate sertifika varsayılan Yönetici rolü FabricClient için kullanılır. |
| UserRoleClientX509StoreName |dize, varsayılan değer "Benim" |Varsayılan kullanıcı rolü FabricClient sertifikasını içeren hello X.509 Sertifika deposu adı. |
| UserRoleClientX509FindType |Varsayılan "FindByThumbprint" dizesidir |Nasıl hello deposundaki sertifikayı toosearch UserRoleClientX509StoreName desteklenen değeri tarafından belirtilen gösterir: FindByThumbprint; FindBySubjectName. |
| UserRoleClientX509FindValue |dize, varsayılan değer "" |Arama filtresi değeri için varsayılan kullanıcı rolü FabricClient toolocate sertifika kullanılır. |
| UserRoleClientX509FindValueSecondary |dize, varsayılan değer "" |Arama filtresi değeri için varsayılan kullanıcı rolü FabricClient toolocate sertifika kullanılır. |

### <a name="section-name-paas"></a>Bölüm adı: Paas
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ClusterId |dize, varsayılan değer "" |X509 sertifika deposunu yapılandırma koruması fabric tarafından kullanılır. |

### <a name="section-name-fabrichost"></a>Bölüm adı: FabricHost
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| StopTimeout |Zaman içinde varsayılan 300 saniyedir |TimeSpan saniye cinsinden belirtin. barındırılan hizmet etkinleştirme için zaman aşımı hello; devre dışı bırakma ve yükseltme. |
| StartTimeout |Zaman içinde varsayılan 300 saniyedir |TimeSpan saniye cinsinden belirtin. Fabricactivationmanager başlangıç için zaman aşımı. |
| ActivationRetryBackoffInterval |Zamanı saniye cinsinden varsayılan 5'tir |TimeSpan saniye cinsinden belirtin. Geri Çekilme aralığı her etkinleştirme hatası; her sürekli etkinleştirme hatası hello sistem toohello MaxActivationFailureCount yukarı hello etkinleştirme için yeniden deneyecek. Merhaba yeniden deneme aralığı her deneyin, sürekli etkinleştirme hatası ve hello etkinleştirme geri alma aralığı için kullanılan bir üründür. |
| ActivationMaxRetryInterval |Zaman içinde varsayılan 300 saniyedir |TimeSpan saniye cinsinden belirtin. Etkinleştirme için en fazla yeniden deneme aralığı. Her sürekli hatası hello yeniden deneme aralığı (ActivationMaxRetryInterval; Min hesaplanır Sürekli hata sayısı * ActivationRetryBackoffInterval). |
| ActivationMaxFailureCount |Int, varsayılan 10'dur |Bu sistem vazgeçmeden önce başarısız etkinleştirme deneyecek hello en büyük sayı değil. |
| EnableServiceFabricAutomaticUpdates |Bool, varsayılan false |Windows Update aracılığıyla tooenable doku otomatik güncelleştirme budur. |
| EnableServiceFabricBaseUpgrade |Bool, varsayılan false |Bu sunucu için tooenable temel güncelleştirme içerir. |
| EnableRestartManagement |Bool, varsayılan false |Tooenable sunucunun yeniden başlatılmasını budur. |


### <a name="section-name-failovermanager"></a>Bölüm adı: FailoverManager
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| UserReplicaRestartWaitDuration |Zamanı saniye cinsinden varsayılan 60,0 * 30'dur |TimeSpan saniye cinsinden belirtin. Kalıcı çoğaltma gittiğinde; Windows Fabric hello çoğaltma toocome bu süresince (hangi hello durumu bir kopyasını gerektirir) yeni değiştirme çoğaltmaları oluşturmadan önce bekler yedekleyin. |
| QuorumLossWaitDuration |Zamanı saniye cinsinden MaxValue varsayılandır |TimeSpan saniye cinsinden belirtin. Bu bölüm toobe çekirdek kayıp durumuna izin veriyoruz hello max aralıktır. Merhaba bölüm bu süreden sonra hala çekirdek kaybında ise; Merhaba bölüm çekirdek kaybına karşı çoğaltmaları kayıp olarak aşağı dikkate alarak hello kullanılarak kurtarılır. Bu olası veri kaybına neden olduğunu unutmayın. |
| UserStandByReplicaKeepDuration |Zamanı saniye cinsinden varsayılan 3600.0 * 24 * 7'dir |TimeSpan saniye cinsinden belirtin. Kalıcı çoğaltma olduğunuzda geri aşağı durumundan; zaten değiştirilmiş. Bu zamanlayıcı FM atılmadan önce hello bekleme çoğaltma tutar ne kadar süreyle hello belirler. |
| UserMaxStandByReplicaCount |Int, varsayılan 1. |Merhaba varsayılan en fazla kullanıcı Hizmetleri için hello sistem tutan StandBy çoğaltmalarının sayısı. |

### <a name="section-name-namingservice"></a>Bölüm adı: NamingService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, 7 varsayılandır |Çoğaltma Hello sayısı hello adlandırma hizmeti deposu her bir bölüm için ayarlar. Çoğaltma kümeleri artar hello hello bilgileri hello adlandırma hizmeti depolama için güvenilirlik düzeyini Hello sayısını artırmayı; bilgi hello hello değişiklik azalan düğüm hatalarını sonucunda kaybolacak; Windows Fabric ve hello süreyi artan iş yükünün maliyetle tooperform güncelleştirmeleri toohello adlandırma veri alır.|
|MinReplicaSetSize | Int, varsayılan 3. | Adlandırma Hizmeti çoğaltmaları en az sayıda Hello toowrite toocomplete bir güncelleştirme gerekli. Daha az çoğaltmalar varsa çoğaltmaları geri yüklenene kadar bu etkin hello sistem hello güvenilirlik sistem güncelleştirmeleri toohello adlandırma hizmeti depolama reddeder. Bu değer hiçbir zaman birden çok hello TargetReplicaSetSize olmalıdır. |
|ReplicaRestartWaitDuration | Saat (60,0 * 30) saniye cinsinden varsayılandır| TimeSpan saniye cinsinden belirtin. Adlandırma Hizmeti çoğaltma gittiğinde; Bu süreölçer başlatır.  Merhaba FM dolduğunda aşağı olan tooreplace hello çoğaltmaları başlar (Bu henüz bunları kayıp dikkate almaz). |
|QuorumLossWaitDuration | Zamanı saniye cinsinden MaxValue varsayılandır | TimeSpan saniye cinsinden belirtin. Ne zaman bir adlandırma hizmeti çekirdek kayıp alır; Bu süreölçer başlatır.  Merhaba FM dolduğunda hello aşağı çoğaltmaları kayıp olarak kabul eder; ve toorecover çekirdek çalışın. Bu veri kaybına neden olabilir değil. |
|StandByReplicaKeepDuration | Zamanı saniye cinsinden varsayılan 3600.0 * 2'dir | TimeSpan saniye cinsinden belirtin. Ne zaman bir adlandırma hizmeti çoğaltmaları aşağı durumundan döndürülmesini; zaten değiştirilmiş.  Bu zamanlayıcı FM atılmadan önce hello bekleme çoğaltma tutar ne kadar süreyle hello belirler. |
|PlacementConstraints | dize, varsayılan değer "" | Yerleştirme kısıtlaması için adlandırma hizmeti hello. |
|ServiceDescriptionCacheLimit | Int, varsayılan 0'dır | Merhaba giriş sayısı üst sınırı hello LRU hizmet açıklaması önbellek tutulur hello adlandırma Deposu hizmetini (sınır too0 ayarlayın). |
|RepairInterval | Zamanı saniye cinsinden varsayılan 5'tir | TimeSpan saniye cinsinden belirtin. Aralık hangi hello hello yetkilisi sahibi ve ad sahibi arasında adlandırma tutarsızlık onarım başlar. |
|MaxNamingServiceHealthReports | Int, varsayılan 10'dur | Adlandırma depolamak yavaş işlemleri Hello sayısının raporları sağlıksız bir kerede hizmet. 0; Tüm yavaş işlemleri gönderilir. |
| MaxMessageSize |Int, varsayılan değer 4*1024*1024 |adlandırma kullanırken istemci düğümü iletişimi için Hello maksimum ileti boyutu. DOS saldırısı alleviation; Varsayılan değer 4 MB'tır. |
| MaxFileOperationTimeout |Zamanı saniye cinsinden varsayılan 30'dur |TimeSpan saniye cinsinden belirtin. dosya depolama hizmeti işlem için izin hello en uzun zaman aşımı. Daha büyük bir zaman aşımı belirtme istekleri kabul edilmeyecek. |
| MaxOperationTimeout |Zamanı saniye cinsinden 600 varsayılandır |TimeSpan saniye cinsinden belirtin. İstemci işlemleri için izin verilen hello en uzun zaman aşımı. Daha büyük bir zaman aşımı belirtme istekleri kabul edilmeyecek. |
| MaxClientConnections |Int, varsayılan 1000'dir |ağ geçidi başına istemci bağlantılarının sayısı izin verilen Hello en fazla. |
| ServiceNotificationTimeout |Zamanı saniye cinsinden varsayılan 30'dur |TimeSpan saniye cinsinden belirtin. Hizmet bildirim toohello istemci teslim edilirken kullanılan hello zaman aşımı. |
| MaxOutstandingNotificationsPerClient |Int, varsayılan 1000'dir |bir istemci kaydı yapmadan önce bekleyen bildirimleri Hello sayısının zorla hello ağ geçidi tarafından kapatıldı. |
| MaxIndexedEmptyPartitions |Int, varsayılan 1000'dir |yeniden bağlanan istemciler eşitlemek için hello bildirim önbelleğindeki kalacak boş bölümler Hello sayısının dizin. Bu sayı yukarıda boş bölümler, arama sürüm artan hello dizinden kaldırılır. İstemcileri yeniden bağlanmayı hala eşitlemek ve kaçırılan boş bölüm güncelleştirmeleri almak; ancak hello eşitleme protokolü daha pahalı hale gelir. |
| GatewayServiceDescriptionCacheLimit |Int, varsayılan 0'dır |Merhaba giriş sayısı üst sınırı hello LRU hizmet açıklaması önbellek tutulur hello adlandırma ağ geçidi (sınır too0 ayarlayın). |
| bölüm sayısı |Int, varsayılan 3. |oluşturulan hello adlandırma hizmeti deposu toobe bölümlerini Hello sayısı. Her bölüm tooits dizin karşılık gelen bir tek bölüm anahtarı sahibi; Bu bölüm anahtarlarını [0; Bölüm sayısı) yok. Adlandırma Hizmeti hello hello ölçek adresindeki hello ortalama herhangi bir yedekleme çoğaltma tarafından tutulan verileri miktarını azaltarak gerçekleştirebilirsiniz adlandırma hizmeti bölümleri artar artan hello sayısını ayarlayın; kaynakların artan kullanımı maliyetle (PartitionCount itibaren * ReplicaSetSize hizmet çoğaltmaları saklanabilir).|

### <a name="section-name-runas"></a>Bölüm adı: RunAs
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| RunAsAccountName |dize, varsayılan değer "" |Merhaba RunAs hesap adını gösterir. Bu yalnızca "DomainUser" veya "Olarak" hesabı için gerekli türü. Geçerli değerler: "etki alanı\kullanıcı" veya "user@domain". |
|RunAsAccountType|dize, varsayılan değer "" |Merhaba RunAs hesap türünü gösterir. Tüm RunAs bölümü geçerli değerler "DomainUser/NetworkService/olarak/LocalSystem" için bu gereklidir.|
|Frk.Çal.parolası|dize, varsayılan değer "" |Merhaba RunAs hesabının parolasını belirtir. Bu, yalnızca "DomainUser" hesap türü için gereklidir. |

### <a name="section-name-runasfabric"></a>Bölüm adı: RunAs_Fabric
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| RunAsAccountName |dize, varsayılan değer "" |Merhaba RunAs hesap adını gösterir. Bu yalnızca "DomainUser" veya "Olarak" hesabı için gerekli türü. Geçerli değerler: "etki alanı\kullanıcı" veya "user@domain". |
|RunAsAccountType|dize, varsayılan değer "" |Merhaba RunAs hesap türünü gösterir. Tüm RunAs bölümü geçerli değerler "YerelKullanıcı/DomainUser/NetworkService/olarak/LocalSystem" için bu gereklidir. |
|Frk.Çal.parolası|dize, varsayılan değer "" |Merhaba RunAs hesabının parolasını belirtir. Bu, yalnızca "DomainUser" hesap türü için gereklidir. |

### <a name="section-name-runashttpgateway"></a>Bölüm adı: RunAs_HttpGateway
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| RunAsAccountName |dize, varsayılan değer "" |Merhaba RunAs hesap adını gösterir. Bu yalnızca "DomainUser" veya "Olarak" hesabı için gerekli türü. Geçerli değerler: "etki alanı\kullanıcı" veya "user@domain". |
|RunAsAccountType|dize, varsayılan değer "" |Merhaba RunAs hesap türünü gösterir. Tüm RunAs bölümü geçerli değerler "YerelKullanıcı/DomainUser/NetworkService/olarak/LocalSystem" için bu gereklidir. |
|Frk.Çal.parolası|dize, varsayılan değer "" |Merhaba RunAs hesabının parolasını belirtir. Bu, yalnızca "DomainUser" hesap türü için gereklidir. |

### <a name="section-name-runasdca"></a>Bölüm adı: RunAs_DCA
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| RunAsAccountName |dize, varsayılan değer "" |Merhaba RunAs hesap adını gösterir. Bu yalnızca "DomainUser" veya "Olarak" hesabı için gerekli türü. Geçerli değerler: "etki alanı\kullanıcı" veya "user@domain". |
|RunAsAccountType|dize, varsayılan değer "" |Merhaba RunAs hesap türünü gösterir. Tüm RunAs bölümü geçerli değerler "YerelKullanıcı/DomainUser/NetworkService/olarak/LocalSystem" için bu gereklidir. |
|Frk.Çal.parolası|dize, varsayılan değer "" |Merhaba RunAs hesabının parolasını belirtir. Bu, yalnızca "DomainUser" hesap türü için gereklidir. |

### <a name="section-name-httpgateway"></a>Bölüm adı: HttpGateway
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
|IsEnabled|Bool, varsayılan false | Etkinleştirir/devre dışı bırakır httpgateway hello. Httpgateway varsayılan olarak devre dışıdır ve bu yapılandırma toobe kümesi tooenable gerekiyor. |
|ActiveListeners |Uint, varsayılan 50'dir | Okuma toopost toohello http sunucusu sıra sayısı. Merhaba HttpGateway hello tarafından karşılanan eşzamanlı istek sayısını denetler. |
|MaxEntityBodySize |Uint 4194304 varsayılandır |  Bir http isteğinden beklenebilir hello gövde en büyük boyutunu Hello sağlar. Varsayılan değer 4 MB'tır. Httpgateway boyutu gövdesi varsa istek başarısız olur > Bu değer. En az okuma öbek boyutu 4096 bayt'tır. Bu toobe nedenle > 4096 =. |
|HttpGatewayHealthReportSendInterval |Zamanı saniye cinsinden varsayılan 30'dur | TimeSpan saniye cinsinden belirtin. başlangıç aralığı sırasında hangi hello Http ağ geçidi gönderir sistem durumu raporları tooHealth Yöneticisi toplanır. |

### <a name="section-name-ktllogger"></a>Bölüm adı: KtlLogger
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
|AutomaticMemoryConfiguration |Int, varsayılan 1. | Merhaba bellek ayarlarını otomatik olarak ve dinamik olarak yapılandırılması gerekip gerekmediğini belirten bayrak. Sıfır sonra hello bellek yapılandırma ayarları doğrudan kullandıysanız ve değiştirmeyin sistem koşullara göre. Varsa ayarları otomatik olarak yapılandırılır ve değişebilir hello bellek sistem koşullara göre. |
|WriteBufferMemoryPoolMinimumInKB |Int, 8388608 varsayılandır |KB tooinitially Hello sayısı hello yazma arabelleği bellek havuzu için ayırın. 0 kullanın tooindicate varsayılan sınır SharedLogSizeInMB aşağıdaki ile tutarlı olmalıdır. |
|WriteBufferMemoryPoolMaximumInKB | Int, varsayılan 0'dır |KB tooallow hello Hello sayısı arabellek bellek havuzu toogrow kadar yazma. 0 tooindicate sınır kullanın. |
|MaximumDestagingWriteOutstandingInKB | Int, varsayılan 0'dır | KB tooallow hello Hello sayısı günlük tooadvance hello ayrılmış günlük öncesinde paylaşılan. 0 tooindicate sınır kullanın.
|SharedLogPath |dize, varsayılan değer "" | Yol ve dosya adı toolocation tooplace paylaşılan günlük kapsayıcı. Kullan "" fabric veri kökü altındaki varsayılan yolu kullanma. |
|SharedLogId |dize, varsayılan değer "" |Paylaşılan günlük kapsayıcısı için benzersiz GUID. Kullan "" fabric veri kökü altındaki varsayılan yolu kullanıyorsanız. |
|SharedLogSizeInMB |Int, 8192 varsayılandır | Merhaba paylaşılan günlük kapsayıcısında MB tooallocate Hello sayısı. |

### <a name="section-name-applicationgatewayhttp"></a>Bölüm adı: ApplicationGateway/Http
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
|IsEnabled |Bool, varsayılan false | Etkinleştirir/devre dışı bırakır HttpApplicationGateway hello. HttpApplicationGateway varsayılan olarak devre dışıdır ve bu yapılandırma toobe kümesi tooenable gerekiyor. |
|NumberOfParallelOperations | Uint, varsayılan 5000'dir | Okuma toopost toohello http sunucusu sıra sayısı. Merhaba HttpGateway hello tarafından karşılanan eşzamanlı istek sayısını denetler. |
|DefaultHttpRequestTimeout |Saniye cinsinden süre. Varsayılan 120'dir |TimeSpan saniye cinsinden belirtin.  Merhaba http uygulama ağ geçidi işlenmekte olan hello http isteklerini Hello varsayılan istek zaman aşımı süresi sağlar. |
|ResolveServiceBackoffInterval |Zamanı saniye cinsinden varsayılan 5'tir |TimeSpan saniye cinsinden belirtin.  Geri alma Hello varsayılan aralığı başarısız çözümleme hizmeti işlemi yeniden denemeden önce sağlar. |
|BodyChunkSize |Uint, 16384 varsayılandır |  Verir hello boyutunu bayt cinsinden hello öbek tooread hello gövde kullanılır. |
|GatewayAuthCredentialType |dize, varsayılan "Hiçbiri": | Güvenlik kimlik bilgileri toouse hello http uygulama ağ geçidi uç nokta geçerli değerleri Hello türünü gösterir "hiçbiri / X 509. |
|GatewayX509CertificateStoreName |dize, varsayılan değer "Benim" | Http uygulama ağ geçidi sertifikasını içeren X.509 Sertifika deposu adı. |
|GatewayX509CertificateFindType |Varsayılan "FindByThumbprint" dizesidir | Nasıl hello deposundaki sertifikayı toosearch GatewayX509CertificateStoreName desteklenen değeri tarafından belirtilen gösterir: FindByThumbprint; FindBySubjectName. |
|GatewayX509CertificateFindValue | dize, varsayılan değer "" | Arama filtresi değeri toolocate hello http uygulama ağ geçidi sertifikası kullanılır. Bu sertifika hello https uç yapılandırılır ve hello Hizmetleri tarafından gerekirse kullanılan tooverify hello hello uygulama kimliğini de olabilir. FindValue ilk Aranan; ve yoksa; FindValueSecondary aranır. |
|GatewayX509CertificateFindValueSecondary | dize, varsayılan değer "" |Arama filtresi değeri toolocate hello http uygulama ağ geçidi sertifikası kullanılır. Bu sertifika hello https uç yapılandırılır ve hello Hizmetleri tarafından gerekirse kullanılan tooverify hello hello uygulama kimliğini de olabilir. FindValue ilk Aranan; ve yoksa; FindValueSecondary aranır.|

### <a name="section-name-management"></a>Bölüm adı: Yönetimi
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ImageStoreConnectionString |SecureString | Bağlantı dizesi toohello görüntü için kök. |
| ImageStoreMinimumTransferBPS | Int, varsayılan 1024'tür. |Merhaba küme görüntü arasındaki Hello minimum aktarım hızı. Erişme hello bu değeri dış görüntü kullanılan toodetermine hello zaman aşımı olur. Merhaba gecikme hello küme ve görüntü arasında yüksek tooallow ise hello küme toodownload daha fazla süre hello yalnızca dış görüntü bu değeri değiştirin. |
|AzureStorageMaxWorkerThreads | Int, varsayılan 25'tir | Merhaba en fazla paralel çalışan iş parçacığı sayısı. |
|AzureStorageMaxConnections | Int, varsayılan 5000'dir | Merhaba en fazla eşzamanlı bağlantı tooazure depolama sayısı. |
|AzureStorageOperationTimeout | Zamanı saniye cinsinden 6000 varsayılandır | TimeSpan saniye cinsinden belirtin. Xstore işlemi toocomplete için zaman aşımı. |
|ImageCachingEnabled | Bool, varsayılan değer true şeklindedir | Bu yapılandırma bize tooenable veya devre dışı bırak önbelleğe alma sağlar. |
|DisableChecksumValidation | Bool, varsayılan false | Bu yapılandırma bize tooenable izin verir veya uygulama sağlama sırasında sağlama toplamı doğrulaması devre dışı bırakın. |
|DisableServerSideCopy | Bool, varsayılan false | Bu yapılandırma etkinleştirir veya sunucu tarafı uygulama paketini hello görüntü kopyası uygulama sağlama sırasında devre dışı bırakır. |

### <a name="section-name-healthmanagerclusterhealthpolicy"></a>Bölüm adı: HealthManager/ClusterHealthPolicy
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ConsiderWarningAsError |Bool, varsayılan false |Küme sistem durumu değerlendirme İlkesi: uyarıları hata olarak kabul edilir. |
| MaxPercentUnhealthyNodes | Int, varsayılan 0'dır |Küme sistem durumu değerlendirme İlkesi: en yüksek yüzde sağlıksız düğümleri hello küme toobe için sağlıklı izin. |
| MaxPercentUnhealthyApplications | Int, varsayılan 0'dır |Küme sistem durumu değerlendirme İlkesi: en yüksek yüzde sağlıksız uygulamaların hello küme toobe için sağlıklı izin. |
|MaxPercentDeltaUnhealthyNodes | Int, varsayılan 10'dur |Küme yükseltme sistem durumu değerlendirme İlkesi: delta sağlıksız düğümleri maksimum yüzdesi hello küme toobe için sağlıklı izin. |
|MaxPercentUpgradeDomainDeltaUnhealthyNodes | Int, varsayılan değer 15 dakikadır. |Küme yükseltme sistem durumu değerlendirme İlkesi: en fazla bir yükseltme etki alanındaki sağlıksız düğümleri delta yüzdesi hello küme toobe için sağlıklı izin.|

### <a name="section-name-faultanalysisservice"></a>Bölüm adı: FaultAnalysisService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, varsayılan 0'dır |NOT_PLATFORM_UNIX_START hello FaultAnalysisService TargetReplicaSetSize. |
| MinReplicaSetSize |Int, varsayılan 0'dır |Merhaba FaultAnalysisService MinReplicaSetSize. |
| ReplicaRestartWaitDuration |Zamanı saniye cinsinden, varsayılan değer 60 dakikadır|TimeSpan saniye cinsinden belirtin. Merhaba FaultAnalysisService ReplicaRestartWaitDuration. |
| QuorumLossWaitDuration | Zamanı saniye cinsinden MaxValue varsayılandır |TimeSpan saniye cinsinden belirtin. Merhaba FaultAnalysisService QuorumLossWaitDuration. |
| StandByReplicaKeepDuration| Zamanı saniye cinsinden varsayılandır (60*24*7) dakika |TimeSpan saniye cinsinden belirtin. Merhaba FaultAnalysisService StandByReplicaKeepDuration. |
| PlacementConstraints | dize, varsayılan değer ""| Merhaba FaultAnalysisService PlacementConstraints. |
| StoredActionCleanupIntervalInSeconds | Int, 3600 varsayılandır |Ne sıklıkta hello deposu temizlenecek budur.  Yalnızca eylemleri bir terminal durumda; ve en az tamamlandı CompletedActionKeepDurationInSeconds önce olacaktır kaldırıldı. |
| CompletedActionKeepDurationInSeconds | Int, 604800 varsayılandır | Yaklaşık terminal durumda ne kadar süreyle tookeep Eylemler budur.  Bu aynı zamanda üzerinde StoredActionCleanupIntervalInSeconds bağlıdır; bu yana Hello iş toocleanup yalnızca bu aralıkta yapılır. 604800 7 gündür. |
| StoredChaosEventCleanupIntervalInSeconds | Int, 3600 varsayılandır |Ne sıklıkta hello deposu Temizleme için denetlenecektir budur; Merhaba olay birden fazla 30000 sayısıdır Merhaba temizleme tetiklersiniz olarak. |

### <a name="section-name-filestoreservice"></a>Bölüm adı: FileStoreService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| NamingOperationTimeout |Zaman içinde varsayılan 60 saniyedir |TimeSpan saniye cinsinden belirtin. adlandırma işlemi gerçekleştirmek için hello zaman aşımı. |
| QueryOperationTimeout | Zaman içinde varsayılan 60 saniyedir |TimeSpan saniye cinsinden belirtin. sorgu işlemi gerçekleştirmek için hello zaman aşımı. |
| MaxCopyOperationThreads | Uint, varsayılan 0'dır | Merhaba en fazla paralel dosya sayısı bu ikincil birincil sunucudan kopyalayabilirsiniz. '0' çekirdek sayısı ==. |
| MaxFileOperationThreads | Uint, varsayılan 100'dür | Merhaba en fazla hello birincil olarak tooperform FileOperations (Copy/Move) izin verilen paralel iş parçacığı sayısı. '0' çekirdek sayısı ==. |
| MaxStoreOperations | Uint, varsayılan 4096'dır |Merhaba maksimum birincil üzerinde izin paralel deposu transcation işlemlerinin sayısı. '0' çekirdek sayısı ==. |
| MaxRequestProcessingThreads | Uint, 200 varsayılandır |Paralel iş parçacığı sayısı üst sınırını Hello hello birincil tooprocess isteklerine izin. '0' çekirdek sayısı ==. |
| MaxSecondaryFileCopyFailureThreshold | Uint, varsayılan 25'tir| Hello en fazla dosya hello vazgeçmeden önce ikincil kopya yeniden deneme sayısı. |
| AnonymousAccessEnabled | Bool, varsayılan değer true şeklindedir |Anonim erişim toohello FileStoreService paylaşır etkinleştir/devre dışı bırak. |
| PrimaryAccountType | dize, varsayılan değer "" |Merhaba birincil hello asıl tooACL hello FileStoreService AccountType paylaşır. |
| PrimaryAccountUserName | dize, varsayılan değer "" |Merhaba birincil hesap hello asıl tooACL hello FileStoreService paylaşımları kullanıcı adı. |
| PrimaryAccountUserPassword | SecureString, varsayılan boştur |Merhaba asıl tooACL hello Hello birincil hesap parolasını FileStoreService paylaşır. |
| FileStoreService | PrimaryAccountNTLMPasswordSecret | SecureString, varsayılan boştur | aynı çekirdek toogenerated kullanılan hello parola gizli anahtar NTLM kimlik doğrulaması kullanırken parola. |
| PrimaryAccountNTLMX509StoreLocation | Varsayılan "LocalMachine" dizesidir| Merhaba NTLM kimlik doğrulaması kullanılırken PrimaryAccountNTLMPasswordSecret üzerinde hello X509 kullanılan sertifika toogenerate HMAC Hello depolama konumu. |
| PrimaryAccountNTLMX509StoreName | Varsayılan "MY" dizesidir| Merhaba deposu hello X509 sertifika toogenerate HMAC PrimaryAccountNTLMPasswordSecret hello üzerinde NTLM kimlik doğrulaması kullanılırken kullanılan adı. |
| PrimaryAccountNTLMX509Thumbprint | dize, varsayılan değer ""|Merhaba sertifikanın parmak izini hello X509 toogenerate HMAC NTLM kimlik doğrulaması kullanılırken PrimaryAccountNTLMPasswordSecret hello üzerinde kullanılır. |
| SecondaryAccountType | dize, varsayılan değer ""| Merhaba ikincil hello asıl tooACL hello FileStoreService AccountType paylaşır. |
| SecondaryAccountUserName | dize, varsayılan değer ""| Merhaba ikincil hesap hello asıl tooACL hello FileStoreService paylaşımları kullanıcı adı. |
| SecondaryAccountUserPassword | SecureString, varsayılan boştur |Merhaba asıl tooACL hello Hello ikincil hesap parolasını FileStoreService paylaşır.  |
| SecondaryAccountNTLMPasswordSecret | SecureString, varsayılan boştur | aynı çekirdek toogenerated kullanılan hello parola gizli anahtar NTLM kimlik doğrulaması kullanırken parola. |
| SecondaryAccountNTLMX509StoreLocation | Varsayılan "LocalMachine" dizesidir |Merhaba NTLM kimlik doğrulaması kullanılırken SecondaryAccountNTLMPasswordSecret üzerinde hello X509 kullanılan sertifika toogenerate HMAC Hello depolama konumu. |
| SecondaryAccountNTLMX509StoreName | Varsayılan "MY" dizesidir |Merhaba deposu hello X509 sertifika toogenerate HMAC SecondaryAccountNTLMPasswordSecret hello üzerinde NTLM kimlik doğrulaması kullanılırken kullanılan adı. |
| SecondaryAccountNTLMX509Thumbprint | dize, varsayılan değer ""| Merhaba sertifikanın parmak izini hello X509 toogenerate HMAC NTLM kimlik doğrulaması kullanılırken SecondaryAccountNTLMPasswordSecret hello üzerinde kullanılır. |

### <a name="section-name-imagestoreservice"></a>Bölüm adı: ImageStoreService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| Etkin |Bool, varsayılan false |Merhaba ImageStoreService için etkin bayrağı. |
| TargetReplicaSetSize | Int, 7 varsayılandır |Merhaba ImageStoreService TargetReplicaSetSize. |
| MinReplicaSetSize | Int, varsayılan 3. |Merhaba ImageStoreService MinReplicaSetSize. |
| ReplicaRestartWaitDuration | Zamanı saniye cinsinden varsayılan 60,0 * 30'dur | TimeSpan saniye cinsinden belirtin. Merhaba ImageStoreService ReplicaRestartWaitDuration. |
| QuorumLossWaitDuration | Zamanı saniye cinsinden MaxValue varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba ImageStoreService QuorumLossWaitDuration. |
| StandByReplicaKeepDuration | Zamanı saniye cinsinden varsayılan 3600.0 * 2'dir | TimeSpan saniye cinsinden belirtin. Merhaba ImageStoreService StandByReplicaKeepDuration. |
| PlacementConstraints | dize, varsayılan değer "" | Merhaba ImageStoreService PlacementConstraints. |
| ClientUploadTimeout | Zamanı saniye cinsinden 1800 varsayılandır |TimeSpan saniye cinsinden belirtin. Üst düzey karşıya yükleme için zaman aşımı değeri tooImage depolama hizmeti isteği. |
| ClientCopyTimeout | Zamanı saniye cinsinden 1800 varsayılandır | TimeSpan saniye cinsinden belirtin. Zaman aşımı değerini en üst düzey bir kopya tooImage depolama hizmeti isteği. |
| ClientDownloadTimeout | Zamanı saniye cinsinden 1800 varsayılandır | TimeSpan saniye cinsinden belirtin. Üst düzey indirme için zaman aşımı değeri tooImage depolama hizmeti isteği |
| ClientListTimeout | Zamanı saniye cinsinden 600 varsayılandır | TimeSpan saniye cinsinden belirtin. Üst düzey liste için zaman aşımı değeri tooImage depolama hizmeti isteği. |
| ClientDefaultTimeout | Zamanı saniye cinsinden 180 varsayılandır | TimeSpan saniye cinsinden belirtin. Tüm olmayan-karşıya yükleme/olmayan-indirme isteği için zaman aşımı değerini (örneğin var; Sil) tooImage depolama hizmeti. |

### <a name="section-name-imagestoreclient"></a>Bölüm adı: ImageStoreClient
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ClientUploadTimeout |Zamanı saniye cinsinden 1800 varsayılandır | TimeSpan saniye cinsinden belirtin. Üst düzey karşıya yükleme için zaman aşımı değeri tooImage depolama hizmeti isteği. |
| ClientCopyTimeout | Zamanı saniye cinsinden 1800 varsayılandır | TimeSpan saniye cinsinden belirtin. Zaman aşımı değerini en üst düzey bir kopya tooImage depolama hizmeti isteği. |
|ClientDownloadTimeout | Zamanı saniye cinsinden 1800 varsayılandır | TimeSpan saniye cinsinden belirtin. Üst düzey indirme için zaman aşımı değeri tooImage depolama hizmeti isteği. |
|ClientListTimeout | Zamanı saniye cinsinden 600 varsayılandır |TimeSpan saniye cinsinden belirtin. Üst düzey liste için zaman aşımı değeri tooImage depolama hizmeti isteği. |
|ClientDefaultTimeout | Zamanı saniye cinsinden 180 varsayılandır | TimeSpan saniye cinsinden belirtin. Tüm olmayan-karşıya yükleme/olmayan-indirme isteği için zaman aşımı değerini (örneğin var; Sil) tooImage depolama hizmeti. |

### <a name="section-name-tokenvalidationservice"></a>Bölüm adı: TokenValidationService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| Sağlayıcılar |Varsayılan "DSTS" dizesidir |Belirteç doğrulama sağlayıcıları tooenable virgülle ayrılmış listesi (geçerli sağlayıcıları şunlardır: DSTS; AAD). Şu anda herhangi bir anda yalnızca tek bir sağlayıcı etkinleştirilebilir. |

### <a name="section-name-upgradeorchestrationservice"></a>Bölüm adı: UpgradeOrchestrationService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| TargetReplicaSetSize |Int, varsayılan 0'dır |Merhaba UpgradeOrchestrationService TargetReplicaSetSize. |
| MinReplicaSetSize |Int, varsayılan 0'dır | Merhaba UpgradeOrchestrationService MinReplicaSetSize.
| ReplicaRestartWaitDuration | Zamanı saniye cinsinden, varsayılan değer 60 dakikadır| TimeSpan saniye cinsinden belirtin. Merhaba UpgradeOrchestrationService ReplicaRestartWaitDuration. |
| QuorumLossWaitDuration | Zamanı saniye cinsinden MaxValue varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba UpgradeOrchestrationService QuorumLossWaitDuration. |
| StandByReplicaKeepDuration | Zaman içinde varsayılan 60 saniyedir*24*7 dakika | TimeSpan saniye cinsinden belirtin. Merhaba UpgradeOrchestrationService StandByReplicaKeepDuration. |
| PlacementConstraints | dize, varsayılan değer "" | Merhaba UpgradeOrchestrationService PlacementConstraints. |
| AutoupgradeEnabled | Bool, varsayılan değer true şeklindedir | Otomatik yoklama ve hedef durumu dosyasını temel alarak yükseltme eylemi. |
| UpgradeApprovalRequired | Bool, varsayılan false | Ayar toomake kod yükseltme devam etmeden önce yönetici onayı gerektirir. |

### <a name="section-name-upgradeservice"></a>Bölüm adı: UpgradeService
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| PlacementConstraints |dize, varsayılan değer "" |Yükseltme hizmeti için Hello PlacementConstraints. |
| TargetReplicaSetSize | Int, varsayılan 3. | Merhaba UpgradeService TargetReplicaSetSize. |
| MinReplicaSetSize | Int, varsayılan 2'dir | Merhaba UpgradeService MinReplicaSetSize. |
| CoordinatorType | Varsayılan "WUTest" dizesidir| Merhaba UpgradeService CoordinatorType. |
| BaseUrl | dize, varsayılan değer "" |UpgradeService BaseUrl. |
| ClusterId | dize, varsayılan değer "" | UpgradeService ClusterId. |
| X509StoreName | dize, varsayılan değer "Benim"| UpgradeService X509StoreName. |
| X509StoreLocation | dize, varsayılan değer "" | UpgradeService X509StoreLocation. |
| X509FindType | dize, varsayılan değer ""| UpgradeService X509FindType. |
| X509FindValue | dize, varsayılan değer "" | UpgradeService X509FindValue. |
| X509SecondaryFindValue | dize, varsayılan değer "" | UpgradeService X509SecondaryFindValue. |
| OnlyBaseUpgrade | Bool, varsayılan false | UpgradeService OnlyBaseUpgrade. |
| TestCabFolder | dize, varsayılan değer "" | UpgradeService TestCabFolder. |

### <a name="section-name-securityclientaccess"></a>Bölüm adı: Güvenlik/ClientAccess
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| CreateName |Varsayılan "Yönetici" dizesidir |Güvenlik yapılandırma adlandırma URI'si oluşturma. |
| DeleteName |Varsayılan "Yönetici" dizesidir |Güvenlik yapılandırma adlandırma URI'si silme işlemi için. |
| PropertyWriteBatch |Varsayılan "Yönetici" dizesidir |Güvenlik yapılandırma adlandırma özelliği için yazma işlemlerini. |
| CreateService |Varsayılan "Yönetici" dizesidir | Hizmet oluşturma için güvenlik yapılandırma. |
| CreateServiceFromTemplate |Varsayılan "Yönetici" dizesidir |Şablondan hizmet oluşturma için güvenlik yapılandırma. |
| UpdateService |Varsayılan "Yönetici" dizesidir |Hizmet güncelleştirmeleri için güvenlik yapılandırma. |
| DeleteService  |Varsayılan "Yönetici" dizesidir |Hizmet silinmek güvenlik yapılandırması. |
| ProvisionApplicationType |Varsayılan "Yönetici" dizesidir | Uygulama sağlama türünü için Güvenlik Yapılandırması'nı tıklatın. |
| CreateApplication |Varsayılan "Yönetici" dizesidir | Uygulama oluşturma Güvenlik Yapılandırması. |
| DeleteApplication |Varsayılan "Yönetici" dizesidir | Uygulama silme işlemi için güvenlik yapılandırması. |
| UpgradeApplication |Varsayılan "Yönetici" dizesidir | Başlatılması veya uygulama yükseltmelerini kesintiye Güvenlik Yapılandırması'nı tıklatın. |
| RollbackApplicationUpgrade |Varsayılan "Yönetici" dizesidir | Uygulama yükseltme geri için Güvenlik Yapılandırması'nı tıklatın. |
| UnprovisionApplicationType |Varsayılan "Yönetici" dizesidir | Uygulama türü sağlamanın kaldırılması için Güvenlik Yapılandırması'nı tıklatın. |
| MoveNextUpgradeDomain |Varsayılan "Yönetici" dizesidir | Açık bir yükseltme etki alanı ile uygulama yükseltmelerini sürdürme için Güvenlik Yapılandırması'nı tıklatın. |
| ReportUpgradeHealth |Varsayılan "Yönetici" dizesidir | Uygulama yükseltme hello geçerli yükseltme ilerleme durumu ile sürdürülüyor için Güvenlik Yapılandırması'nı tıklatın. |
| ReportHealth |Varsayılan "Yönetici" dizesidir | Sistem durumu raporlama için Güvenlik Yapılandırması'nı tıklatın. |
| ProvisionFabric |Varsayılan "Yönetici" dizesidir | MSI ve/veya küme bildirimi sağlama Güvenlik Yapılandırması'nı tıklatın. |
| UpgradeFabric |Varsayılan "Yönetici" dizesidir | Küme yükseltme başlatmak için Güvenlik Yapılandırması'nı tıklatın. |
| RollbackFabricUpgrade |Varsayılan "Yönetici" dizesidir | Küme yükseltme geri için Güvenlik Yapılandırması'nı tıklatın. |
| UnprovisionFabric |Varsayılan "Yönetici" dizesidir | MSI ve/veya küme bildirimi sağlamanın kaldırılması için Güvenlik Yapılandırması'nı tıklatın. |
| MoveNextFabricUpgradeDomain |Varsayılan "Yönetici" dizesidir | Küme yükseltme açıkça yükseltme etki alanı ile sürdürülüyor için Güvenlik Yapılandırması'nı tıklatın. |
| ReportFabricUpgradeHealth |Varsayılan "Yönetici" dizesidir | Küme yükseltme hello geçerli yükseltme ilerleme durumu ile sürdürülüyor için Güvenlik Yapılandırması'nı tıklatın. |
| StartInfrastructureTask |Varsayılan "Yönetici" dizesidir | Altyapısı görevlerini başlatmak için Güvenlik Yapılandırması'nı tıklatın. |
| FinishInfrastructureTask |Varsayılan "Yönetici" dizesidir | Sonlandırma altyapı görevleri için güvenlik yapılandırma. |
| ActivateNode |Varsayılan "Yönetici" dizesidir | Bir düğüm etkinleştirme için güvenlik yapılandırma. |
| DeactivateNode |Varsayılan "Yönetici" dizesidir | Bir düğüm devre dışı bırakma için Güvenlik Yapılandırması'nı tıklatın. |
| DeactivateNodesBatch |Varsayılan "Yönetici" dizesidir | Birden çok düğüm devre dışı bırakma için Güvenlik Yapılandırması'nı tıklatın. |
| RemoveNodeDeactivations |Varsayılan "Yönetici" dizesidir | Birden çok düğümde geri alma devre dışı bırakma için güvenlik yapılandırma. |
| GetNodeDeactivationStatus |Varsayılan "Yönetici" dizesidir | Devre dışı bırakma durumunu denetlemek için Güvenlik Yapılandırması'nı tıklatın. |
| NodeStateRemoved |Varsayılan "Yönetici" dizesidir | Kaldırılan düğüm durumu raporlama için Güvenlik Yapılandırması'nı tıklatın. |
| RecoverPartition |Varsayılan "Yönetici" dizesidir | Bir bölüm kurtarmak için Güvenlik Yapılandırması'nı tıklatın. |
| RecoverPartitions |Varsayılan "Yönetici" dizesidir | Bölümler kurtarmak için Güvenlik Yapılandırması'nı tıklatın. |
| RecoverServicePartitions |Varsayılan "Yönetici" dizesidir | Hizmet bölümlerini kurtarmak için Güvenlik Yapılandırması'nı tıklatın. |
| RecoverSystemPartitions |Varsayılan "Yönetici" dizesidir | Sistem hizmeti bölümleri kurtarmak için Güvenlik Yapılandırması'nı tıklatın. |
| ReportFault |Varsayılan "Yönetici" dizesidir | Hata raporlama için Güvenlik Yapılandırması'nı tıklatın. |
| InvokeInfrastructureCommand |Varsayılan "Yönetici" dizesidir | Altyapı görev yönetimi komutları için güvenlik yapılandırma. |
| FileContent |Varsayılan "Yönetici" dizesidir | Görüntü için Güvenlik Yapılandırması istemci dosya aktarımı (Dış toocluster) depolar. |
| FileDownload |Varsayılan "Yönetici" dizesidir | Görüntü deposu istemci dosya indirme başlatma (Dış toocluster) için güvenlik yapılandırma. |
| InternalList |Varsayılan "Yönetici" dizesidir | Görüntü için Güvenlik Yapılandırması istemci dosya listesi işlemi (iç) depolar. |
| Sil |Varsayılan "Yönetici" dizesidir | Görüntü için Güvenlik Yapılandırması istemci silme işlemi depolar. |
| Karşıya Yükle |Varsayılan "Yönetici" dizesidir | Görüntü için güvenlik yapılandırması istemcisi karşıya yükleme işlemi depolar. |
| GetStagingLocation |Varsayılan "Yönetici" dizesidir | Güvenlik Yapılandırma görüntüsü için konum alma hazırlama istemci depolar. |
| GetStoreLocation |Varsayılan "Yönetici" dizesidir | Görüntü için Güvenlik Yapılandırması istemci deposu konum alma depolar. |
| NodeControl |Varsayılan "Yönetici" dizesidir | Başlangıç için Güvenlik Yapılandırması'nı tıklatın; durdurma; ve düğüm yeniden başlatılıyor. |
| CodePackageControl |Varsayılan "Yönetici" dizesidir | Yeniden başlatma kodu paketleri Güvenlik Yapılandırması'nı tıklatın. |
| UnreliableTransportControl |Varsayılan "Yönetici" dizesidir | Ekleme ve kaldırma davranışları için güvenilir olmayan aktarım. |
| MoveReplicaControl |Varsayılan "Yönetici" dizesidir | Çoğaltma taşıyın. |
| PredeployPackageToNode |Varsayılan "Yönetici" dizesidir | Dağıtım öncesi API. |
| StartPartitionDataLoss |Varsayılan "Yönetici" dizesidir | Veri kaybı bir bölüme uygulanmasını. |
| StartPartitionQuorumLoss |Varsayılan "Yönetici" dizesidir | Bir bölüm çekirdek kaybı uygulanmasını. |
| StartPartitionRestart |Varsayılan "Yönetici" dizesidir | Aynı anda bir bölüm, bazı veya tüm hello çoğaltmaları yeniden başlatır. |
| CancelTestCommand |Varsayılan "Yönetici" dizesidir | Uçuş modunda olması durumunda belirli bir TestCommand - iptal eder. |
| StartChaos |Varsayılan "Yönetici" dizesidir | Zaten başlatılmadığında Chaos - başlatır. |
| StopChaos |Varsayılan "Yönetici" dizesidir | Başlatılmış olup olmadığını Chaos - durdurur. |
| StartNodeTransition |Varsayılan "Yönetici" dizesidir | Bir düğüm geçişi başlatmak için Güvenlik Yapılandırması'nı tıklatın. |
| StartClusterConfigurationUpgrade |Varsayılan "Yönetici" dizesidir | StartClusterConfigurationUpgrade bir bölüme uygulanmasını. |
| GetUpgradesPendingApproval |Varsayılan "Yönetici" dizesidir | GetUpgradesPendingApproval bir bölüme uygulanmasını. |
| StartApprovedUpgrades |Varsayılan "Yönetici" dizesidir | StartApprovedUpgrades bir bölüme uygulanmasını. |
| Ping |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | İstemci ping için güvenlik yapılandırma. |
| Sorgu |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Sorgular için güvenlik yapılandırma. |
| NameExists |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Güvenlik yapılandırma adlandırma URI'si varlığı denetler. |
| EnumerateSubnames |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Adlandırma URI'si numaralandırması için güvenlik yapılandırma. |
| EnumerateProperties |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Özellik numaralandırma Adlandırma Güvenlik Yapılandırması'nı tıklatın. |
| PropertyReadBatch |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Güvenlik yapılandırma adlandırma özelliği okuma işlemlerini. |
| GetServiceDescription |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Uzun yoklama hizmet bildirimleri ve hizmeti açıklamaları okumak için güvenlik yapılandırma. |
| ResolveService |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Hizmet uyumlu tabanlı çözümlemesi için güvenlik yapılandırması. |
| ResolveNameOwner |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Adlandırma URI'si sahibi çözmek için Güvenlik Yapılandırması'nı tıklatın. |
| ResolvePartition |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Sistem Hizmetleri çözmek için Güvenlik Yapılandırması'nı tıklatın. |
| ServiceNotifications |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Olay tabanlı hizmet bildirimleri için güvenlik yapılandırma. |
| PrefixResolveService |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Hizmet uyumlu tabanlı ön ek çözümleme için güvenlik yapılandırma. |
| GetUpgradeStatus |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Uygulama yükseltme durumunu yoklama için Güvenlik Yapılandırması'nı tıklatın. |
| GetFabricUpgradeStatus |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Küme yükseltme durumunu yoklama için Güvenlik Yapılandırması'nı tıklatın. |
| InvokeInfrastructureQuery |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Altyapı görevleri sorgulamak için Güvenlik Yapılandırması'nı tıklatın. |
| Liste |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Görüntü için Güvenlik Yapılandırması istemci dosya listesi işlemi depolar. |
| ResetPartitionLoad |Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Bir failoverUnit sıfırlama yük için güvenlik yapılandırma. |
| ToggleVerboseServicePlacementHealthReporting | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Ayrıntılı ServicePlacement HealthReporting geçiş için güvenlik yapılandırma. |
| GetPartitionDataLossProgress | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Bir Invoke veri kaybı API çağrısı için Hello ilerleme getirir. |
| GetPartitionQuorumLossProgress | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Bir Invoke çekirdek kayıp API çağrısı için Hello ilerleme getirir. |
| GetPartitionRestartProgress | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Bir yeniden başlatma bölüm API çağrısı için Hello ilerlemesi getirir. |
| GetChaosReport | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Belirli bir zaman aralığı içinde karmaşık dünyada Hello durum getirir. |
| GetNodeTransitionProgress | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | Bir düğüm geçiş komutunda ilerleme durumunu almak için Güvenlik Yapılandırması'nı tıklatın. |
| GetClusterConfigurationUpgradeStatus | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | GetClusterConfigurationUpgradeStatus bir bölüme uygulanmasını. |
| GetClusterConfiguration | Varsayılan "Admin\ dizesidir|\|Kullanıcı" | GetClusterConfiguration bir bölüme uygulanmasını. |

### <a name="section-name-reconfigurationagent"></a>Bölüm adı: ReconfigurationAgent
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ApplicationUpgradeMaxReplicaCloseDuration | Zamanı saniye cinsinden 900 varsayılandır |TimeSpan saniye cinsinden belirtin. Merhaba süresi hangi hello için Kapat'takılmış çoğaltmaları olan hizmet ana bilgisayarlar sonlandırmadan önce sistem bekler. |
| ServiceApiHealthDuration | Zamanı saniye cinsinden, varsayılan değer 30 dakikadır | TimeSpan saniye cinsinden belirtin. Biz sağlıksız raporu önce ne kadar süreyle biz hizmeti API toorun için bekleme ServiceApiHealthDuration tanımlar. |
| ServiceReconfigurationApiHealthDuration | Zamanı saniye cinsinden varsayılan 30'dur | TimeSpan saniye cinsinden belirtin. ServiceReconfigurationApiHealthDuration hello yeniden yapılandırma hizmetinde önce ne kadar süreyle sorunlu olarak bildirildi tanımlar. |
| PeriodicApiSlowTraceInterval | Zamanı saniye cinsinden, varsayılan değer 5 dakikadır | TimeSpan saniye cinsinden belirtin. PeriodicApiSlowTraceInterval üzerinden yavaş API çağrıları hello API İzleyici tarafından yeniden taranma başlangıç aralığı tanımlar. |
| NodeDeactivationMaxReplicaCloseDuration | Zamanı saniye cinsinden 900 varsayılandır | TimeSpan saniye cinsinden belirtin. en uzun süre toowait düğümü devre dışı bırakma engelleyen bir hizmet ana bilgisayarı sonlandırmadan önce hello. |
| FabricUpgradeMaxReplicaCloseDuration | Zamanı saniye cinsinden 900 varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba en uzun süre RA hizmeti ana bilgisayarı değil kapatılıyor çoğaltma sonlandırmadan önce bekler. |
| IsDeactivationInfoEnabled | Bool, varsayılan değer true şeklindedir | Bu yapılandırma tootrue yükseltilen var olan kümeleri için ayarlanmalıdır yeni kümeleri için birincil yeniden seçim gerçekleştirmek için RA devre dışı bırakma bilgileri kullanıp kullanmayacağını belirler Lütfen nasıl hello sürüm notlarına bakın tooenable bu. |

### <a name="section-name-placementandloadbalancing"></a>Bölüm adı: PlacementAndLoadBalancing
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| TraceCRMReasons |Bool, varsayılan değer true şeklindedir |CRM tootrace nedenlerle hareketleri toohello çalışma olaylarını kanal verilmiş olup olmadığını belirtir. |
| ValidatePlacementConstraint | Bool, varsayılan değer true şeklindedir | Bir hizmetin ServiceDescription güncelleştirildiğinde hello PlacementConstraint ifadesi bir hizmet için doğrulanmış olup olmadığını belirtir. |
| PlacementConstraintValidationCacheSize | Int, varsayılan 10000 arasıdır | Sınırları hızlı doğrulama için kullanılan ve yerleştirme kısıtlaması ifadeler, önbelleğe alma Merhaba tablonun boyutunu hello. |
|VerboseHealthReportLimit | Int, varsayılan 20'dir | Merhaba sayısı (ayrıntılı sistem durumu raporlama etkinse) sistem durumu uyarısı için bildirilen önce bir çoğaltma toogo yerleştirilmemiş olduğunu tanımlar. |
|ConstraintViolationHealthReportLimit | Int, varsayılan 50'dir | Merhaba kaç kez kalıcı olarak tanılama yürütülür ve sistem durumu raporlarını yayınlaması önce Düzeltilmeyen toobe çoğaltma ihlal kısıtlamasına sahip tanımlar. |
|DetailedConstraintViolationHealthReportLimit | Int, 200 varsayılandır | Merhaba kaç kez kalıcı olarak tanılama yürütülür ve ayrıntılı sistem durumu raporlarını yayınlaması önce Düzeltilmeyen toobe çoğaltma ihlal kısıtlamasına sahip tanımlar. |
|DetailedVerboseHealthReportLimit | Int, 200 varsayılandır | Merhaba kaç kez toobe raporlarını yayınlaması ayrıntılı durum önce kalıcı olarak yerleştirilmemiş yerleştirilmemiş bir çoğaltmaya sahip tanımlar. |
|ConsecutiveDroppedMovementsHealthReportLimit | Int, varsayılan 20'dir | Merhaba, ResourceBalancer verilen hareketleri tanılama yürütülür ve sistem durumu uyarıları yayılan önce bırakılan arda kaç kez tanımlar. Negatif: Hiçbir uyarı yayılan bu koşul altında. |
|DetailedNodeListLimit | Int, varsayılan değer 15 dakikadır. | Merhaba başına düğüm sayısını sınırlama tooinclude kesilmesi önce yerleştirilmemiş çoğaltma raporları hello tanımlar. |
|DetailedPartitionListLimit | Int, varsayılan değer 15 dakikadır. | Merhaba kesilmesi önce kısıtlaması tooinclude için tanı girdisi başına bölüm sayısını tanılamada tanımlar. |
|DetailedDiagnosticsInfoListLimit | Int, varsayılan değer 15 dakikadır. | Tanılama kesilmesi önce kısıtlaması tooinclude başına Hello sayıda tanı girdisi (ayrıntılı bilgilerle) tanımlar.|
|PLBRefreshGap | Zamanı saniye olarak varsayılan 1. | TimeSpan saniye cinsinden belirtin. Merhaba minimum PLB durumu yeniden yeniler önce geçmesi gereken süre miktarını tanımlar. |
|Minplacementınterval | Zamanı saniye olarak varsayılan 1. | TimeSpan saniye cinsinden belirtin. Merhaba en az iki ardışık yerleştirme yuvarlar önce geçmesi gereken süre miktarını tanımlar. |
|Minconstraintcheckınterval | Zamanı saniye olarak varsayılan 1. | TimeSpan saniye cinsinden belirtin. Merhaba minimum yuvarlar denetim iki ardışık kısıtlaması önce geçmesi gereken süre miktarını tanımlar. |
|MinLoadBalancingInterval | Zamanı saniye cinsinden varsayılan 5'tir | TimeSpan saniye cinsinden belirtin. Merhaba en az iki ardışık karşı yuvarlar önce geçmesi gereken süre miktarını tanımlar. |
|BalancingDelayAfterNodeDown | Zamanı saniye cinsinden varsayılan 120'dir |TimeSpan saniye cinsinden belirtin. Bir düğüm aşağı olayını bu süre içinde etkinlikleri Dengeleme başlatmayın. |
|BalancingDelayAfterNewNode | Zamanı saniye cinsinden varsayılan 120'dir |TimeSpan saniye cinsinden belirtin. Yeni bir düğüm ekledikten sonra bu süre içinde etkinlikleri Dengeleme başlatmayın. |
|ConstraintFixPartialDelayAfterNodeDown | Zamanı saniye cinsinden varsayılan 120'dir | TimeSpan saniye cinsinden belirtin. Bir düğüm aşağı olayını bu süre içinde değil FaultDomain düzeltin ve UpgradeDomain sabiti ihlallerini yapın. |
|ConstraintFixPartialDelayAfterNewNode | Zamanı saniye cinsinden varsayılan 120'dir | TimeSpan saniye cinsinden belirtin. DDo FaultDomain değil düzeltin ve yeni bir düğüm ekledikten sonra bu süre içinde UpgradeDomain kısıtlaması ihlali. |
|GlobalMovementThrottleThreshold | Uint, varsayılan 1000'dir | İzin hareketlerinin sayısının hello son aşaması Dengeleme hello aralığı GlobalMovementThrottleCountingInterval tarafından belirtilir. |
|GlobalMovementThrottleThresholdForPlacement | Uint, varsayılan 0'dır | Hareketleri yerleştirme aşamasında hello geçmiş GlobalMovementThrottleCountingInterval.0 tarafından gösterilen aralığı sınır belirten verilen.|
|GlobalMovementThrottleThresholdForBalancing | Uint, varsayılan 0'dır | Merhaba geçmiş Dengeleme aşamasında izin hareketlerinin sayısının aralığı GlobalMovementThrottleCountingInterval tarafından belirtilir. 0 sınır gösterir. |
|GlobalMovementThrottleCountingInterval | Zamanı saniye cinsinden 600 varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba Hello uzunluğunu belirtmek aralığı (GlobalMovementThrottleThreshold birlikte kullanılan) etki alanı çoğaltma hareketleri başına hangi tootrack için geçmiş. Too0 tooignore genel tamamen azaltma ayarlanabilir. |
|MovementPerPartitionThrottleThreshold | Uint, varsayılan 50'dir | Merhaba sayısı, bu bölümün çoğaltmalar için ilgili hareketleri Dengeleme ulaşıldı veya MovementPerFailoverUnitThrottleThreshold hello geçmiş aşıldı taşıma için bir bölüm gerçekleşeceği ilgili hiçbir Dengeleme aralığı belirtilen tarafından MovementPerPartitionThrottleCountingInterval. |
|MovementPerPartitionThrottleCountingInterval | Zamanı saniye cinsinden 600 varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba Hello uzunluğunu belirtmek hangi tootrack çoğaltma hareketleri için bir aralığı (MovementPerPartitionThrottleThreshold birlikte kullanılan) her bölüm için geçmiş. |
|PlacementSearchTimeout | Zamanı saniye cinsinden 0,5 varsayılandır | TimeSpan saniye cinsinden belirtin. Hizmetleri yerleştirirken; Bu süre için en çok bir sonuç döndürmeden önce arayın. |
|UseMoveCostReports | Bool, varsayılan false | Merhaba LB tooignore hello maliyet öğesi işlevi Puanlama hello söyler; Sonuçta elde edilen çok sayıda olasılığı daha iyi dengelenmiş yerleştirme için taşır. |
|PreventTransientOvercommit | Bool, varsayılan false | PLB tarafından başlatılan hello taşır önbellekten kaynaklar hemen saymak belirler. Varsayılan olarak; PLB taşıma çıkışı başlatabilir ve geçici oluşturabilirsiniz aynı düğüm bilgisayar hello taşıyın. Bu parametre tootrue engelleyecek ayar bu tür overcommits ve isteğe bağlı birleştirme (diğer adıyla placementWithMove) devre dışı bırakılacak. |
|InBuildThrottlingEnabled | Bool, varsayılan false | Yapı Hello azaltma etkin olup olmadığını belirler. |
|InBuildThrottlingAssociatedMetric | dize, varsayılan değer "" | Merhaba bu azaltma için ölçüm adı ilişkili. |
|InBuildThrottlingGlobalMaxValue | Int, varsayılan 0'dır |Merhaba sayısı üst sınırından yapı çoğaltmaları küresel olarak izin verilir. |
|SwapPrimaryThrottlingEnabled | Bool, varsayılan false| Takas birincil Hello azaltma etkin olup olmadığını belirler. |
|SwapPrimaryThrottlingAssociatedMetric | dize, varsayılan değer ""| Merhaba bu azaltma için ölçüm adı ilişkili. |
|SwapPrimaryThrottlingGlobalMaxValue | Int, varsayılan 0'dır | Merhaba sayısı üst sınırından takas birincil çoğaltmaları küresel olarak izin verilir. |
|PlacementConstraintPriority | Int, varsayılan 0'dır | Yerleştirme kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|PreferredLocationConstraintPriority | Int, varsayılan 2'dir| Tercih edilen konum kısıtlaması Hello önceliğini belirler: 0: sabit; 1: yazılım; 2: en iyi duruma getirme; Negatif: yoksay |
|CapacityConstraintPriority | Int, varsayılan 0'dır | Kapasite kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|AffinityConstraintPriority | Int, varsayılan 0'dır | Benzeşim kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|FaultDomainConstraintPriority | Int, varsayılan 0'dır | Hata etki alanı kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|UpgradeDomainConstraintPriority | Int, varsayılan 1.| Yükseltme etki alanı kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|ScaleoutCountConstraintPriority | Int, varsayılan 0'dır | Genişletme sayısı kısıtlaması Hello önceliğini belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|ApplicationCapacityConstraintPriority | Int, varsayılan 0'dır | Kapasite kısıtlamasının Hello öncelik belirler: 0: sabit; 1: yazılım; Negatif: yoksay. |
|MoveParentToFixAffinityViolation | Bool, varsayılan false | Üst çoğaltmaları olabiliyorsa belirleyen ayarı toofix benzeşim kısıtlamaları taşındı.|
|MoveExistingReplicaForPlacement | Bool, varsayılan değer true şeklindedir |Belirler ayarını yerleştirme sırasında toomove mevcut çoğaltma. |
|UseSeparateSecondaryLoad | Bool, varsayılan değer true şeklindedir | Varsa belirleyen ayarı farklı ikincil yük kullanın. |
|PlaceChildWithoutParent | Bool, varsayılan değer true şeklindedir | Hiçbir üst çoğaltma yukarı ise alt çoğaltma hizmeti belirleyen ayarı yerleştirilebilir. |
|PartiallyPlaceServices | Bool, varsayılan değer true şeklindedir | Kümedeki tüm hizmet çoğaltmaları "tümü veya hiçbiri" yerleştirilip yerleştirilmeyeceğini sınırlı uygun düğümler için bunları belirler.|
|InterruptBalancingForAllFailoverUnitUpdates | Bool, varsayılan false | Yük devretme birimi güncelleştirme herhangi bir türde veya hızlı kesme çalıştırmak Dengeleme yavaş belirler. "False" Çalıştır Dengeleme kesilmesi durumunda ile belirtilen FailoverUnit: oluşturulan/silinir; çoğaltmalar eksik; Birincil çoğaltma konumu veya değiştirilen çoğaltmaların sayısı değiştirildi. Çalıştırma Dengeleme kesintiye diğer durumlarda - varsa FailoverUnit: ek çoğaltmalarına; sahip tüm çoğaltma bayrağı değiştirildi; yalnızca bölüm sürümü veya diğer herhangi bir durumu değişti. |

### <a name="section-name-security"></a>Bölüm adı: güvenlik
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ClusterProtectionLevel |Yok ya da EncryptAndSign |Hiçbiri (varsayılan) güvenli olmayan kümeler, da EncryptAndSign güvenli kümeleri için. |

### <a name="section-name-hosting"></a>Bölüm adı: barındırma
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| ServiceTypeRegistrationTimeout |Zaman içinde varsayılan 300 saniyedir |Doku ile kayıtlı hello ServiceType toobe için izin verilen en uzun süre |
| ServiceTypeDisableFailureThreshold |Tam sayı olarak varsayılan 1. |Merhaba FailoverManager (FM) sonra olduğu hatası sayısını bildirim bu düğüm ve yerleştirme için farklı bir düğüme try toodisable hello hizmet türü için hello eşik budur. |
| ActivationRetryBackoffInterval |Zamanı saniye cinsinden varsayılan 5'tir |Her etkinleştirme hatasında geri Çekilme aralığı; Her sürekli etkinleştirme hatasında hello sistem yeniden deneme etkinleştirme için toohello MaxActivationFailureCount yukarı hello. Merhaba yeniden deneme aralığı her deneyin, sürekli etkinleştirme hatası ve hello etkinleştirme geri alma aralığı için kullanılan bir üründür. |
| ActivationMaxRetryInterval |Zaman içinde varsayılan 300 saniyedir |Her sürekli etkinleştirme hatasında hello sistem yeniden deneme tooActivationMaxFailureCount yukarı etkinleştirme için hello. ActivationMaxRetryInterval her etkinleştirme hatası sonrasında yeniden deneme bekleme zaman aralığını belirtir |
| ActivationMaxFailureCount |Tam sayı olarak varsayılan 10'dur |Sistem yeniden deneme sayısı vazgeçmeden önce etkinleştirme başarısız oldu |

### <a name="section-name-failovermanager"></a>Bölüm adı: FailoverManager
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| PeriodicLoadPersistInterval |Zamanı saniye cinsinden varsayılan 10'dur |Bu ne sıklıkta belirler Yeni Yük raporları FM denetle hello |

### <a name="section-name-federation"></a>Bölüm adı: Federasyon
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| Kirasüresi |Zamanı saniye cinsinden varsayılan 30'dur |Bir düğüm ile komşularına arasında bir kira süresi süresi. |
| LeaseDurationAcrossFaultDomain |Zamanı saniye cinsinden varsayılan 30'dur |Hata etki alanlarında bir düğüm ile komşularına arasında bir kira süresi süresi. |

### <a name="section-name-clustermanager"></a>Bölüm adı: ClusterManager
| **Parametre** | **İzin verilen değerler** | **Kılavuz veya kısa bir açıklama** |
| --- | --- | --- |
| UpgradeStatusPollInterval |Zaman içinde varsayılan 60 saniyedir |Uygulama yükseltme durumu için yoklama sıklığı Hello. Bu değer, herhangi bir GetApplicationUpgradeProgress çağrısına güncelleştirmesi hello oranını belirler. |
| UpgradeHealthCheckInterval |Zaman içinde varsayılan 60 saniyedir |izlenen uygulama yükseltmeler sırasında Hello sıklığı sistem durumunu denetler |
| FabricUpgradeStatusPollInterval |Zaman içinde varsayılan 60 saniyedir |Fabric yükseltme durumu için yoklama sıklığı Hello. Bu değer, herhangi bir GetFabricUpgradeProgress çağrısına güncelleştirmesi hello oranını belirler. |
| FabricUpgradeHealthCheckInterval |Zaman içinde varsayılan 60 saniyedir |izlenen bir Fabric yükseltmesi sırasında sistem surumu denetimi Hello sıklığı |
|InfrastructureTaskProcessingInterval | Zamanı saniye cinsinden varsayılan 10'dur |TimeSpan saniye cinsinden belirtin. Merhaba altyapı görev işleme durumu makine tarafından kullanılan hello işleme aralığı. |
|TargetReplicaSetSize |Int, 7 varsayılandır |Merhaba ClusterManager TargetReplicaSetSize. |
|MinReplicaSetSize |Int, varsayılan 3. |Merhaba ClusterManager MinReplicaSetSize. |
|ReplicaRestartWaitDuration |Saat (60,0 * 30) saniye cinsinden varsayılandır|TimeSpan saniye cinsinden belirtin. Merhaba ClusterManager ReplicaRestartWaitDuration. |
|QuorumLossWaitDuration |Zamanı saniye cinsinden MaxValue varsayılandır | TimeSpan saniye cinsinden belirtin. Merhaba ClusterManager QuorumLossWaitDuration. |
|StandByReplicaKeepDuration | Zamanı saniye cinsinden varsayılan (3600.0 * 2).|TimeSpan saniye cinsinden belirtin. Merhaba ClusterManager StandByReplicaKeepDuration. |
|PlacementConstraints | dize, varsayılan değer "" |Merhaba ClusterManager PlacementConstraints. |
|SkipRollbackUpdateDefaultService | Bool, varsayılan false |Merhaba CM dönüştürülüyor güncelleştirilmiş varsayılan Hizmetleri Uygulama yükseltme geri alma sırasında atlar. |
|EnableDefaultServicesUpgrade | Bool, varsayılan false |Uygulama yükseltme sırasında yükseltme varsayılan hizmetleri sağlar. Varsayılan hizmet açıklamaları yükseltme sonrasında üzerine. |
|InfrastructureTaskHealthCheckWaitDuration |Zamanı saniye cinsinden varsayılan 0'dır| TimeSpan saniye cinsinden belirtin. bir altyapı görevi sonrası işledikten sonra sistem durumu başlatmadan önce zaman toowait Hello miktarını denetler. |
|InfrastructureTaskHealthCheckStableDuration | Zamanı saniye cinsinden varsayılan 0'dır| TimeSpan saniye cinsinden belirtin. bir altyapı görevi sonrası işlenmesini başarıyla tamamlanmadan önce zaman tooobserve ardışık geçirilen durum hello miktarını denetler. Başarısız sistem durumu denetimi Gözlemleme bu süreölçer sıfırlanır. |
|InfrastructureTaskHealthCheckRetryTimeout | Zaman içinde varsayılan 60 saniyedir |TimeSpan saniye cinsinden belirtin. Merhaba miktarda zaman toospend yeniden deneniyor bir altyapı görevi sonrası işlerken sistem durumu denetimleri başarısız oldu. Geçirilen sistem durumu denetimi Gözlemleme bu süreölçer sıfırlanır. |
|ImageBuilderTimeoutBuffer |Zamanı saniye cinsinden varsayılan 3. |TimeSpan saniye cinsinden belirtin. Image Builder belirli zaman aşımı hataları tooreturn toohello istemcisi için zaman tooallow Hello miktarı. Bu arabellek çok küçük ise; ardından hello istemci hello sunucusu önce zaman aşımına uğradı ve genel zaman aşımı hatası alır. |
|MinOperationTimeout | Zaman içinde varsayılan 60 saniyedir |TimeSpan saniye cinsinden belirtin. dahili olarak ClusterManager işlemlerini işlemek için hello minimum genel zaman aşımı. |
|MaxOperationTimeout |Zamanı saniye cinsinden MaxValue varsayılandır | TimeSpan saniye cinsinden belirtin. dahili olarak ClusterManager işlemlerini işlemek için hello maksimum genel zaman aşımı. |
|MaxTimeoutRetryBuffer | Zamanı saniye cinsinden 600 varsayılandır |TimeSpan saniye cinsinden belirtin. en fazla işlem zaman aşımı hello dahili olarak son denenirken tootimeouts olan <Original Timeout>  +  <MaxTimeoutRetryBuffer>. Ek zaman aşımı MinOperationTimeout artışlarla eklenir. |
|MaxCommunicationTimeout |Zamanı saniye cinsinden 600 varsayılandır |TimeSpan saniye cinsinden belirtin. ClusterManager ve diğer sistem hizmetleri arasında iç iletişim için en büyük zaman aşımı (yani; hello Adlandırma Hizmeti; Yük Devretme Yöneticisi ve vb.). Bu zaman aşımı (olabilir gibi her bir istemci işlemin sistem bileşenleri arasında birden çok iletişim) genel MaxOperationTimeout küçük olmalıdır. |
|MaxDataMigrationTimeout |Zamanı saniye cinsinden 600 varsayılandır |TimeSpan saniye cinsinden belirtin. Fabric yükseltmesi gerçekleştikten sonra veri geçiş kurtarma işlemleri için en uzun zaman aşımı hello. |
|MaxOperationRetryDelay |Zamanı saniye cinsinden varsayılan 5'tir| TimeSpan saniye cinsinden belirtin. Merhaba hataları karşılaştığında iç deneme için en büyük gecikme. |
|ReplicaSetCheckTimeoutRollbackOverride |Zamanı saniye cinsinden varsayılan 1200'dür | TimeSpan saniye cinsinden belirtin. ReplicaSetCheckTimeout toohello maksimum DWORD değerini ayarlarsanız; Ardından, bu yapılandırma geri alma hello amacıyla hello değeriyle geçersiz kılındı. İleri için kullanılan hello değeri hiçbir zaman geçersiz kılındı. |
|ImageBuilderJobQueueThrottle |Int, varsayılan 10'dur |Uygulama isteklerinden Image Builder proxy işi sıra sayısı azaltma iş parçacığı. |

## <a name="next-steps"></a>Sonraki adımlar
Küme yönetimi hakkında daha fazla bilgi için bu makaleler okuyun:

[Eklemek için değil, UTC'ye, Azure kümenizden sertifikaları kaldırın](service-fabric-cluster-security-update-certs-azure.md) 

