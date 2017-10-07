---
title: "Service Fabric düzeltme eki orchestration uygulama aaaAzure | Microsoft Docs"
description: "Uygulama tooautomate işletim sistemi bir Service Fabric kümesi düzeltme eki uygulama."
services: service-fabric
documentationcenter: .net
author: novino
manager: timlt
editor: 
ms.assetid: de7dacf5-4038-434a-a265-5d0de80a9b1d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/9/2017
ms.author: nachandr
ms.openlocfilehash: fbb89aa2ea418181ee908a01850178c113c462fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="patch-hello-windows-operating-system-in-your-service-fabric-cluster"></a>Service Fabric kümenizdeki Hello Windows işletim sistemi düzeltme eki

Merhaba düzeltme eki orchestration uygulama kapalı kalma süresi olmadan Azure üzerinde bir Service Fabric kümesindeki düzeltme eki uygulama işletim sistemi otomatikleştiren bir Azure Service Fabric uygulamasıdır.

Merhaba düzeltme eki orchestration uygulama hello şunları sağlar:

- **Otomatik işletim sistemi güncelleştirme yüklemesini**. İşletim sistemi güncelleştirmeleri otomatik olarak karşıdan yüklenir ve. Küme düğümleri küme kapalı kalma süresi olmadan gerektiği gibi yeniden başlatılır.

- **Küme durumunu algılayan düzeltme eki uygulama ve sistem durumu tümleştirme**. Güncelleştirmeler uygulanırken hello düzeltme eki orchestration uygulama hello küme düğümleri hello durumunu izler. Küme düğümü yükseltilmiş bir düğümde aynı anda bir saat ya da bir yükseltme etki alanı olan. Hello küme Hello durumunu nedeniyle toohello düzeltme eki uygulama işlemi devre dışı kalırsa, düzeltme eki uygulama hello sorun aggravating durdurulmuş tooprevent ' dir.

## <a name="internal-details-of-hello-app"></a>Merhaba uygulamasının iç ayrıntıları

Merhaba düzeltme eki orchestration uygulama bileşenleri şu Merhaba oluşur:

- **Düzenleyicisi hizmeti**: Bu durum bilgisi olan hizmet sorumludur:
    - Denetleyici hello Windows Update işinde hello tüm küme.
    - Tamamlanan Windows Update işlemleri depolanmasını hello sonucu.
- **Düğüm Aracısı hizmeti**: Bu durum bilgisiz hizmet tüm Service Fabric küme düğümleri üzerinde çalışır. Merhaba hizmet sorumludur:
    - Önyükleme hello düğüm Aracısı NTService.
    - Merhaba düğüm Aracısı NTService izleme.
- **Düğüm Aracısı NTService**: Bu Windows NT hizmeti, üst düzey bir ayrıcalık (Sistem) çalışır. Buna karşılık, hello düğüm Aracısı hizmeti ve hello Düzenleyicisi hizmetindeki bir alt düzey önceliği (ağ hizmeti) çalıştırın. Merhaba hizmet hello tüm küme düğümlerinde Windows Update işleri aşağıdaki hello gerçekleştirmek için sorumludur:
    - Otomatik Windows Update hello düğüm üzerinde devre dışı bırakılıyor.
    - Windows Update yükleyip toohello ilke hello kullanıcı according sağlamıştır.
    - Merhaba makine post Windows Güncelleştirme yüklemesini yeniden başlatılıyor.
    - Windows güncelleştirmeleri toohello Coordinator hizmeti Hello sonuçlarını karşıya yükleniyor.
    - Tüm yeniden denemeler tükenmesinden sonra bir işlem başarısız oldu durumda raporlama durumu raporları.

> [!NOTE]
> Merhaba düzeltme eki orchestration uygulama kullandığı hello Service Fabric Yöneticisi sistem hizmeti toodisable onarmak veya başlangıç düğümü etkinleştirin ve sistem durumu denetimleri gerçekleştirmek. Merhaba onarım görev hello düzeltme eki orchestration uygulama parçaları hello her düğüm için Windows Update ilerleme tarafından oluşturuldu.

## <a name="prerequisites"></a>Ön koşullar

### <a name="minimum-supported-service-fabric-runtime-version"></a>Service Fabric çalışma zamanı sürümü desteklenen en düşük

#### <a name="azure-clusters"></a>Azure kümeleri
Merhaba düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.5 sahip Azure kümelerinde çalıştırılması gerekir ya da daha sonra.

#### <a name="standalone-on-premises-clusters"></a>Tek başına şirket içi kümeleri
Merhaba düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.6 sahip tek başına kümelerinde çalıştırılması gerekir ya da daha sonra.

### <a name="enable-hello-repair-manager-service-if-its-not-running-already"></a>(Bu zaten çalışmıyorsa) hello onarım Yöneticisi hizmetini etkinleştirme

Merhaba düzeltme eki orchestration uygulama hello kümede etkin hello onarım Yöneticisi sistem hizmeti toobe gerektirir.

#### <a name="azure-clusters"></a>Azure kümeleri

Hello Yöneticisi hizmeti varsayılan olarak etkinleştirilmiş onarmaya hello Gümüş dayanıklılık katmanındaki Azure kümeniz vardır. Merhaba altın dayanıklılık katmanı Azure kümelerde sahip olabilir veya hello onarım Yöneticisi hizmeti bu kümeleri oluşturulduğu bağlı olarak, etkin değil. Varsayılan olarak, hello Bronz dayanıklılık katmanı Azure kümelerde hello Yöneticisi hizmetinin etkinleştirilmiş onarmaya gerekmez. Merhaba hizmet zaten etkinleştirilmişse hello Sistem Hizmetleri bölümünde hello Service Fabric Explorer çalışmasını görebilirsiniz.

##### <a name="azure-portal"></a>Azure portalına
Onarım Yöneticisi Azure portalından kümesinin kurma hello zaman etkinleştirebilirsiniz. Seçin `Include Repair Manager` altında seçeneği `Add on features` küme yapılandırmasının hello zaman.
![Azure portalından etkinleştirme onarım Yöneticisi'nin resmi](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager şablonu
Alternatif olarak, hello kullanabilirsiniz [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) tooenable hello onarım Yöneticisi hizmetine yeni ve mevcut Service Fabric kümeleri. Merhaba şablonu toodeploy istediğiniz hello küme için alın. Merhaba örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun. 

tooenable hello onarım Yöneticisi hizmetini kullanarak [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. İlk olarak bu hello denetleyin `apiversion` çok ayarlanır`2017-07-01-preview` hello için `Microsoft.ServiceFabric/clusters` hello aşağıdaki kod parçacığında gösterildiği gibi kaynak. Farklı sonra tooupdate hello gereksinim `apiVersion` toohello değeri `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Merhaba aşağıdakileri ekleyerek hello onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeatures` bölümünden hello sonra `fabricSettings` bölümü:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Bu değişikliklerle küme şablonunuzu güncelleştirildikten sonra bunları uygulamak ve son hello yükseltme sağlayabilirsiniz. Kümenizde çalışan hello onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz. Çağrılır `fabric:/System/RepairManagerService` hello Sistem Hizmetleri bölümünde hello Service Fabric Explorer. 

### <a name="standalone-on-premises-clusters"></a>Tek başına şirket içi kümeleri

Merhaba kullanabilirsiniz [tek başına Windows kümesi için yapılandırma ayarlarını](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) tooenable hello onarım Yöneticisi hizmetine yeni ve mevcut Service Fabric kümesi.

tooenable hello onarım Yöneticisi hizmeti:

1. İlk olarak bu hello denetleyin `apiversion` içinde [genel küme yapılandırmaları](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) çok ayarlanır`04-2017` veya üstü:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Merhaba aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeaturres` bölümünden hello sonra `fabricSettings` bölümünde aşağıda gösterildiği gibi:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Küme bildiriminizi güncelleştirilmiş hello küme bildirimini kullanarak bu değişikliklerle güncelleştirmek [yeni küme oluşturma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) veya [yükseltme hello küme yapılandırması](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Merhaba küme güncelleştirilmiş küme bildirimini ile çalışmaya başladıktan sonra artık hello onarım Yöneticisi sistem hizmeti olarak adlandırılır, kümede çalışan görebilirsiniz `fabric:/System/RepairManagerService`altında sistem hizmetleri hello Service Fabric explorer bölümünde.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Tüm düğümlerde otomatik Windows Update devre dışı bırak

Birden çok küme düğümleri aynı hello yeniden başlatarak, otomatik Windows güncelleştirmelerini tooavailability kaybına neden zaman. Varsayılan olarak, çalıştığında toodisable Hello düzeltme eki orchestration uygulama, her küme düğümünde otomatik Windows Update hello. Ancak, Hello ayarları Grup İlkesi veya bir yönetici tarafından yönetiliyorsa, ayarı hello Windows Update ilke çok "bildir önce yükleme" açıkça öneririz.

### <a name="optional-enable-azure-diagnostics"></a>İsteğe bağlı: Azure tanılamayı etkinleştirin

Service Fabric çalışma zamanı sürümü çalıştıran kümeler `5.6.220.9494` ve yukarıdaki toplama düzeltme eki orchestration uygulama günlükleri Service Fabric bir parçası olarak günlüğe kaydeder.
Kümenizi Service Fabric çalışma zamanı sürümünde çalışıyorsa, bu adımı atlayabilirsiniz `5.6.220.9494` ve üstü.

Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri hello düzeltme eki orchestration uygulama için toplanan yerel olarak her hello küme düğümleri üzerinde.
Azure tanılama tooupload günlükleri tüm düğümleri tooa merkezi konumdan yapılandırmanızı öneririz.

Azure Tanılama'yı etkinleştirme hakkında daha fazla bilgi için bkz: [Azure tanılama kullanarak günlükleri toplamak](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Merhaba düzeltme eki orchestration uygulama günlüklerini sabit sağlayıcısı kimlikleri aşağıdaki hello üzerinde oluşturulur:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

Resource Manager şablonu goto içinde `EtwEventSourceProviderConfiguration` altında bölümünde `WadCfg` ve girişleri aşağıdaki hello ekleyin:

```json
  {
    "provider": "e39b723c-590c-4090-abb0-11e3e6616346",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
      "eventDestination": "PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "fc0028ff-bfdc-499f-80dc-ed922c52c5e9",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "24afa313-0d3b-4c7c-b485-1047fd964b60",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  },
  {
    "provider": "05dc046c-60e9-4ef7-965e-91660adffa68",
    "scheduledTransferPeriod": "PT5M",
    "DefaultEvents": {
    "eventDestination": " PatchOrchestrationApplicationTable"
    }
  }
```

> [!NOTE]
> Birden çok düğüm türleri, Service Fabric kümesi var. sonra tüm Merhaba hello önceki bölümde eklediğiniz `WadCfg` bölümler.

## <a name="download-hello-app-package"></a>Merhaba uygulama paketini indirin

Hello Hello uygulamayı karşıdan [bağlantı karşıdan](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-hello-app"></a>Merhaba uygulamayı yapılandırma

Merhaba hello düzeltme eki orchestration uygulamanın davranışı yapılandırılmış toomeet gereksinimlerinizi olabilir. Uygulama oluşturma veya güncelleştirme işlemi sırasında hello uygulama parametresini geçirerek Hello varsayılan değerlerini geçersiz kılar. Uygulama parametreleri belirterek sağlanabilir `ApplicationParameter` toohello `Start-ServiceFabricApplicationUpgrade` veya `New-ServiceFabricApplication` cmdlet'leri.

|**Parametre**        |**Tür**                          | **Ayrıntılar**|
|:-|-|-|
|MaxResultsToCache    |Uzun                              | Önbelleğe alınması gereken Windows Update sonuçlarının maksimum sayısı. <br>Varsayılan değer 3000 varsayılır: <br> -Düğüm sayısı 20'dir. <br> -Ayda bir düğümde gerçekleştiği güncelleştirme sayısı beştir. <br> -İşlemi başına sonuç sayısı 10 olabilir. <br> -Sonuçlar hello son üç ay için depolanması gerekir. |
|TaskApprovalPolicy   |Enum <br> {NodeWise, UpgradeDomainWise}                          |TaskApprovalPolicy hello Service Fabric küme düğümleri arasında hello Coordinator hizmeti tooinstall Windows güncelleştirmelerini tarafından kullanılan toobe hello İlkesi gösterir.<br>                         İzin verilen değerler: <br>                                                           <b>NodeWise</b>. Windows Update yüklü bir aynı anda düğümdür. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update aynı anda yüklü bir yükseltme etki alanıdır. (En fazla hello sırasında Windows Update tooan yükseltme etki alanına ait tüm hello düğümleri gidebilirsiniz.)
|LogsDiskQuotaInMB   |Uzun  <br> (Varsayılan: 1024)               |Yerel olarak düğümlerinde kalıcı MB cinsinden en büyük boyutunu düzeltme eki orchestration uygulama kaydeder.
| WUQuery               | Dize<br>(Varsayılan: "IsInstalled = 0")                | Sorgu tooget Windows güncelleştirir. Daha fazla bilgi için bkz: [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | bool <br> (varsayılan: True)                 | Bu bayrak, Windows işletim sistemi güncelleştirmeleri toobe yüklü sağlar.            |
| WUOperationTimeOutInMinutes | Int <br>(Varsayılan: 90).                   | Herhangi bir Windows Update işlemi (arama veya indirme veya yükleme) için Hello zaman aşımını belirtir. İçinde Hello işlemi tamamlanmazsa Merhaba belirtilen zaman aşımı, iptal edilir.       |
| WURescheduleCount     | Int <br> (Varsayılan: 5).                  | bir işlem kalıcı olarak başarısız olursa Windows hello en fazla kaç kez hello hello hizmet reschedules güncelleştirin.          |
| WURescheduleTimeInMinutes | Int <br>(Varsayılan: 30). | Hata devam ederse durumunda Windows güncelleştirme sırasında hangi hello hizmet hello reschedules hello aralığı. |
| WUFrequency           | Virgülle ayrılmış dize (varsayılan: "Haftalık, Çarşamba, 7:00:00")     | Windows Update yükleme hello sıklığı. Merhaba biçimi ve olası değerler şunlardır: <br>-Örneğin, aylık, 5, 12 aylık, gg ss: 22:32. <br> -Örneğin, haftalık, Salı, 12:22:32 için haftalık, gün, ss.  <br> -Örneğin, günlük, 12:22:32 günlük, ss.  <br> -Hiçbiri, Windows Update yapılması döndürmemelidir gösterir.  <br><br> Tüm hello saatler UTC biçiminde olduğunu unutmayın.|
| AcceptWindowsUpdateEula | bool <br>(Varsayılan: true) | Bu bayrak ayarlayarak Merhaba uygulaması hello Windows Update için son kullanıcı lisans sözleşmesi hello makine hello sahibi adına kabul eder.              |

> [!TIP]
> Windows Update toohappen hemen istiyorsanız ayarlayın `WUFrequency` göreli toohello uygulama dağıtım süresini. Örneğin, bir beş düğümlü test kümesi ve planı toodeploy hello uygulaması yaklaşık 5: 00'da olduğunu varsayalım UTC. Merhaba uygulama yükseltme veya dağıtım sırasında 30 dakika sürer olduğunu varsayarsak, en fazla, ayarlanmış hello WUFrequency "Günlük, 17:30:00." Merhaba

## <a name="deploy-hello-app"></a>Merhaba uygulama dağıtma

1. Tüm hello önkoşul adımlarını tooprepare hello küme tamamlayın.
2. Başka bir Service Fabric uygulaması gibi Hello düzeltme eki orchestration uygulamasını dağıtın. PowerShell kullanarak hello uygulama dağıtabilirsiniz. Merhaba adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. tooconfigure hello Uygulama dağıtımının geçişi hello hello zamanında `ApplicationParamater` toohello `New-ServiceFabricApplication` cmdlet'i. Size kolaylık olması için hello betik Deploy.ps1 Merhaba uygulaması birlikte sağladık. toouse hello komut dosyası:

    - Tooa Service Fabric kümesi kullanarak bağlanmak `Connect-ServiceFabricCluster`.
    - Merhaba PowerShell betiğini Deploy.ps1 hello uygun yürütün `ApplicationParameter` değeri.

> [!NOTE]
> Merhaba komut dosyası ve hello uygulama klasörü PatchOrchestrationApplication hello tutmak aynı dizin.

## <a name="upgrade-hello-app"></a>Merhaba uygulama yükseltme

tooupgrade PowerShell kullanarak mevcut bir düzeltme eki orchestration uygulamayı izleyin hello adımlarda [PowerShell kullanarak Service Fabric uygulama yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-hello-app"></a>Merhaba uygulamasını kaldırın

tooremove hello uygulama izleme hello adımlarda [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Size kolaylık olması için hello betik Undeploy.ps1 Merhaba uygulaması birlikte sağladık. toouse hello komut dosyası:

  - Tooa Service Fabric kümesi kullanarak bağlanmak ```Connect-ServiceFabricCluster```.

  - Merhaba PowerShell betiğini Undeploy.ps1 yürütün.

> [!NOTE]
> Merhaba komut dosyası ve hello uygulama klasörü PatchOrchestrationApplication hello tutmak aynı dizin.

## <a name="view-hello-windows-update-results"></a>Merhaba Windows Update sonuçları görüntüleme

Merhaba düzeltme eki orchestration uygulama REST API'leri toodisplay hello geçmiş sonuçlarını toohello kullanıcı kullanıma sunar. Merhaba sonuç JSON örneği:
```json
[
  {
    "NodeName": "_stg1vm_1",
    "WindowsUpdateOperationResults": [
      {
        "OperationResult": 0,
        "NodeName": "_stg1vm_1",
        "OperationTime": "2017-05-21T11:46:52.1953713Z",
        "UpdateDetails": [
          {
            "UpdateId": "7392acaf-6a85-427c-8a8d-058c25beb0d6",
            "Title": "Cumulative Security Update for Internet Explorer 11 for Windows Server 2012 R2 (KB3185319)",
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of hello issues that are included in this update, see hello associated Microsoft Knowledge Base article. After you install this update, you may have toorestart your system.",
            "ResultCode": 0
          }
        ],
        "OperationType": 1,
        "WindowsUpdateQuery": "IsInstalled=0",
        "WindowsUpdateFrequency": "Daily,10:00:00",
        "RebootRequired": false
      }
    ]
  },
  ...
]
```
Hiçbir güncelleştirme henüz planlandıysa hello sonuç JSON boştur.

Toohello küme tooquery Windows Update sonuçları günlüğü. Ardından hello Coordinator hizmeti hello birincil hello çoğaltma adresini bulmak ve hello tarayıcı hello URL'den isabet: http://&lt;çoğaltma IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

Merhaba REST uç noktasını hello Coordinator hizmeti için dinamik bir bağlantı noktası var. toocheck tam URL'yi Merhaba, toohello Service Fabric Explorer bakın. Örneğin, hello sonuçları kullanılabilir `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![REST uç noktasını görüntüsü](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Merhaba ters proxy hello kümede etkinleştirilirse, hello küme dışındaki hello URL'den erişebilir.
toobe gereken uç nokta hello isabet olduğu http://&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

tooenable hello ters proxy hello kümede izleyin hello adımlarda [ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Hello ters proxy yapılandırıldıktan sonra bir HTTP uç noktası kullanıma tüm mikro hizmetler hello kümedeki hello küme dışında adreslenebilir.

## <a name="diagnosticshealth-events"></a>Tanılama/sistem durumu olayları

### <a name="collect-patch-orchestration-app-logs"></a>Toplama düzeltme eki orchestration uygulama günlükleri

Düzeltme eki orchestration uygulama günlükleri, çalışma zamanı sürümünden Service Fabric günlükleri bir parçası olarak toplanır `5.6.220.9494` ve üstü.
Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri yöntemler aşağıdaki hello birini kullanarak toplanmasını.

#### <a name="locally-on-each-node"></a>Her bir düğümde yerel olarak

Günlükleri toplanır yerel olarak her Service Fabric küme düğümünde Service Fabric çalışma zamanı sürümü ise değerinden `5.6.220.9494`. Merhaba konumu tooaccess hello günlükleri olan \[Service Fabric\_yükleme\_sürücü\]:\\PatchOrchestrationApplication\\günlükleri.

Service Fabric D sürücüsünde yüklüyse, örneğin, hello D: yoludur\\PatchOrchestrationApplication\\günlükleri.

#### <a name="central-location"></a>Merkezi bir konum

Azure tanılama önkoşul adımlarını bir parçası olarak yapılandırılmışsa, hello düzeltme eki orchestration uygulama günlüklerini Azure depolama alanında kullanılabilir.

### <a name="health-reports"></a>Sistem durumu raporları

Merhaba düzeltme eki orchestration uygulama sistem durumu raporlarının hello Coordinator hizmetini veya hello düğüm Aracısı hizmeti karşı durumlarda aşağıdaki hello de yayımlar:

#### <a name="a-windows-update-operation-failed"></a>Windows Update işlemi başarısız oldu

Bir düğümde Windows güncelleştirme işlemi başarısız olursa, bir sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur. Merhaba sistem durumu raporu ayrıntılarını hello sorunlu bir düğüm adı içeriyor.

Düzeltme eki uygulama hello sorunlu düğümde başarıyla tamamlandıktan sonra hello rapor otomatik olarak temizlenir.

#### <a name="hello-node-agent-ntservice-is-down"></a>Merhaba düğüm Aracısı NTService çalışmıyor

Merhaba düğüm Aracısı NTService bir düğümde çalışmıyorsa, bir uyarı düzeyi sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur.

#### <a name="hello-repair-manager-service-is-not-enabled"></a>Merhaba onarım Yöneticisi hizmeti etkin değil

Merhaba onarım Yöneticisi hizmeti hello kümede bulunmazsa, bir uyarı düzeyi sistem durumu raporu Merhaba Coordinator hizmeti oluşturulur.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

Q. **Merhaba düzeltme eki orchestration uygulama çalışırken neden bir hata durumuna my küme görüyor?**

A. Merhaba yükleme işlemi sırasında hello düzeltme eki orchestration uygulama devre dışı bırakır veya geçici olarak giderek hello küme hello durumunu sonuçlanabilir düğümleri yeniden başlatılır.

Hello İlkesi hello uygulama için bağlı olarak, herhangi bir düğümün bir düzeltme eki uygulama işlemi sırasında gidebilirsiniz *veya* tüm yükseltme etki alanı aynı anda Git aşağı.

Merhaba Windows Update yükleme Hello sonuna düğümler yeniden iler hale hello yeniden gönderin.

Aşağıdaki örneğine hello tooan hata durumu geçici olarak iki düğüm aşağı olan ve MaxPercentageUnhealthNodes İlkesi hello çünkü ihlal edildiğini hello küme geçti. devam eden işlemi düzeltme eki uygulama hello olana kadar hello hata geçicidir.

![Sağlıksız küme görüntüsü](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Merhaba sorun devam ederse toohello sorun giderme bölümüne bakın.

Q. **Düzeltme eki orchestration uygulama uyarı durumunda**

A. Merhaba uygulamaya karşı gönderilen bir sistem durumu raporu hello kök nedeni toosee kontrol edin. Genellikle, hello uyarı hello sorunun ayrıntılarını içerir. Merhaba sorun geçici ise, hello beklenen tooauto kurtarma bu durumdan uygulamasıdır.

Q. **My küme sağlıksız ise ve toodo Acil işletim sistemi güncelleştirmesi gerekir ne yapabilirim?**

A. Merhaba küme sağlıksız durumdayken hello düzeltme eki orchestration uygulama güncelleştirmelerini yüklemez. Toobring küme tooa sağlıklı duruma toounblock hello düzeltme eki orchestration uygulama iş akışınızı deneyin.

Q. **Neden kümelerinde düzeltme eki uygulama çok uzun toorun sürer?**

A. Merhaba düzeltme eki orchestration uygulama tarafından gerekli hello zaman çoğunlukla Etkenler aşağıdaki hello üzerinde bağlıdır:

- Merhaba Coordinator hizmeti Hello ilkesi. 
  - Merhaba varsayılan ilke, `NodeWise`, sonuçlarını aynı anda yalnızca tek bir düğüme düzeltme eki uygulama içinde. Merhaba kullanmanızı tavsiye ederiz özellikle hello durumda daha büyük kümeleri `UpgradeDomainWise` İlkesi tooachieve kümeler arasında düzeltme eki uygulama daha hızlı.
- indirme ve yükleme için kullanılabilir güncelleştirmeleri Hello sayısı. 
- gerekli ortalama süre toodownload hello ve birkaç saat aşmamalıdır bir güncelleştirme yükleyin.
- Merhaba performans hello VM ve ağ bant genişliği.

Q. **Bazı güncelleştirmeler Windows Update sonuçlarında REST API'nin aracılığıyla ancak hello makinede Windows Update geçmişi altında elde neden görüyor musunuz?**

A. Bazı ürün güncelleştirmelerini ilgili güncelleştirme/düzeltme eki geçmişlerini işaretli toobe gerekir. Örneğin: Windows Defender'ın güncelleştirmeleri Windows Update geçmişinde Windows Server 2016 görünmüyor.

## <a name="disclaimers"></a>Bildirimler

- Merhaba düzeltme eki orchestration uygulama hello Windows Update, son kullanıcı lisans sözleşmesi hello kullanıcı adına kabul eder. İsteğe bağlı olarak, hello ayarı hello hello uygulama yapılandırmasında kapatılabilir.

- Merhaba düzeltme eki orchestration uygulama telemetri tootrack kullanımını ve performansını toplar. Merhaba uygulamanın telemetri (varsayılan olarak etkindir) hello Service Fabric çalışma zamanı telemetri ayarını hello ayarı izler.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="a-node-is-not-coming-back-tooup-state"></a>Bir düğüme geri tooup durumu gelmelerini değil

**Merhaba düğümü takılmış devre dışı bırakma durumunda olduğundan**:

Güvenlik onay bekliyor. tooremedy bu durum iyi durumda yeterli düğüm kullanılabilir olduğundan emin olun.

**Merhaba düğümü takılmış devre dışı durumda olduğundan**:

- Merhaba düğümü el ile devre dışı bırakıldı.
- Merhaba düğümü vade tooan devam eden Azure altyapı işini devre dışı bırakıldı.
- Merhaba düğümü hello düzeltme eki orchestration uygulama toopatch hello düğümü tarafından geçici olarak devre dışı bırakıldı.

**Merhaba düğümü aşağı bir durumda olduğundan takılmış olabilir**:

- Merhaba düğümü aşağı durumda el ile askıya alınmış.
- Merhaba düğümü (hangi hello düzeltme eki orchestration uygulama tarafından tetiklenen) yeniden yapılıyor.
- tooa hatalı VM veya makine ya da ağ bağlantısı sorunları Hello düğümü çalışmıyor.

### <a name="updates-were-skipped-on-some-nodes"></a>Güncelleştirmeleri bazı düğümler üzerinde atlandı

Merhaba düzeltme eki orchestration uygulama tooinstall Windows update according toohello yeniden zamanlama ilkesi çalışır. Merhaba hizmeti toorecover hello düğümü çalışır ve hello güncelleştirme according toohello uygulama ilkesi atlayın.

Böyle bir durumda, bir uyarı düzeyi sistem durumu raporu düğüm Aracısı hizmeti hello karşı oluşturulur. Windows Update için Hello sonuç hello olası hello başarısızlık nedeni de içerir.

### <a name="hello-health-of-hello-cluster-goes-tooerror-while-hello-update-installs"></a>Merhaba güncelleştirmeyi yüklerken hello küme hello durumunu tooerror gider.

Bir uygulama veya belirli düğüme veya yükseltme etki alanı küme hello durumunu aşağı hatalı bir Windows güncelleştirmesi kullanıma sunabilirsiniz. Merhaba küme yeniden sağlıklı duruma gelene kadar hello düzeltme eki orchestration uygulama sonraki tüm Windows Update işlemi sona erdirir.

Bir yönetici müdahale ve Merhaba uygulaması ya da küme neden nedeniyle sağlıksız olduğunu belirlemek tooWindows güncelleştirme.

## <a name="release-notes-"></a>Sürüm Notları:

### <a name="version-110"></a>Sürüm 1.1.0
- Ortak sürüm

### <a name="version-111"></a>Sürüm 1.1.1
- Bir hata SetupEntryPoint, NodeAgentNTService yüklemesini engelleyen NodeAgentService içinde sabit.

### <a name="version-120-latest"></a>Sürüm 1.2.0 (en yeni)

- Hata düzeltmeleri sistem geçici iş akışını yeniden başlatın.
- Onarım görevlerin hazırlanması sırasında toowhich sistem durumu denetimi RM görevlerin oluşturulmasını hata düzeltme beklendiği gibi gerçekleştiği değildi.
- Windows hizmet POANodeSvc otomatik toodelayed-otomatik değiştirilen hello başlangıç modu.
