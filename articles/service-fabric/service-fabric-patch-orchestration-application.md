---
title: "Azure Service Fabric düzeltme orchestration uygulaması | Microsoft Docs"
description: "Service Fabric kümesi üzerinde işletim sistemi düzeltme eki uygulama otomatikleştirmek için uygulama."
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
ms.openlocfilehash: 2c5842822e347113e388d570f6ae603a313944d6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="patch-the-windows-operating-system-in-your-service-fabric-cluster"></a>Service Fabric kümesi Windows işletim sistemi düzeltme eki

Düzeltme eki orchestration uygulama kapalı kalma süresi olmadan Azure üzerinde bir Service Fabric kümesindeki düzeltme eki uygulama işletim sistemi otomatikleştiren bir Azure Service Fabric uygulamasıdır.

Düzeltme eki orchestration uygulama aşağıdakileri sağlar:

- **Otomatik işletim sistemi güncelleştirme yüklemesini**. İşletim sistemi güncelleştirmeleri otomatik olarak karşıdan yüklenir ve. Küme düğümleri küme kapalı kalma süresi olmadan gerektiği gibi yeniden başlatılır.

- **Küme durumunu algılayan düzeltme eki uygulama ve sistem durumu tümleştirme**. Güncelleştirmeler uygulanırken düzeltme eki orchestration uygulama küme düğümlerinin sistem durumunu izler. Küme düğümü yükseltilmiş bir düğümde aynı anda bir saat ya da bir yükseltme etki alanı olan. Küme durumunu düzeltme eki uygulama işlemi nedeniyle kullanılamaz hale gelirse, düzeltme eki uygulama sorun aggravating önlemek için durduruldu.

## <a name="internal-details-of-the-app"></a>Uygulamanın iç ayrıntıları

Düzeltme eki orchestration uygulama aşağıdaki bileşenleri oluşur:

- **Düzenleyicisi hizmeti**: Bu durum bilgisi olan hizmet sorumludur:
    - Windows güncelleştirme işi tüm küme üzerinde Eşgüdümleme.
    - Tamamlanmış Windows Update işlemlerin sonucunu depolamak.
- **Düğüm Aracısı hizmeti**: Bu durum bilgisiz hizmet tüm Service Fabric küme düğümleri üzerinde çalışır. Hizmet için sorumludur:
    - Düğüm Aracısı NTService önyükleme.
    - Düğüm Aracısı NTService izleme.
- **Düğüm Aracısı NTService**: Bu Windows NT hizmeti, üst düzey bir ayrıcalık (Sistem) çalışır. Buna karşılık, düğüm Aracısı hizmeti ve Coordinator hizmeti bir alt düzey önceliği (ağ hizmeti) çalıştırın. Hizmet, tüm küme düğümleri üzerinde aşağıdaki Windows Update işlerini gerçekleştirmek için sorumludur:
    - Düğümde otomatik Windows Update devre dışı bırakılıyor.
    - Karşıdan yükleme ve Windows Update ilkesine göre kullanıcı sağlamıştır.
    - Makine post Windows Güncelleştirme yüklemesini yeniden başlatılıyor.
    - Windows güncelleştirmelerini sonuçlarını Coordinator hizmeti yükleniyor.
    - Tüm yeniden denemeler tükenmesinden sonra bir işlem başarısız oldu durumda raporlama durumu raporları.

> [!NOTE]
> Düzeltme eki orchestration app Service Fabric onarım Yöneticisi sistem hizmeti devre dışı bırakın veya düğüm etkinleştirmek ve sistem durumu denetimleri gerçekleştirmek için kullanır. Düzeltme eki orchestration uygulama tarafından oluşturulan onarım görevi her düğüm için Windows Update ilerleme durumunu izler.

## <a name="prerequisites"></a>Ön koşullar

### <a name="minimum-supported-service-fabric-runtime-version"></a>Service Fabric çalışma zamanı sürümü desteklenen en düşük

#### <a name="azure-clusters"></a>Azure kümeleri
Düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.5 sahip Azure kümelerinde çalıştırılması gerekir ya da daha sonra.

#### <a name="standalone-on-premises-clusters"></a>Tek başına şirket içi kümeleri
Düzeltme eki orchestration app Service Fabric çalışma zamanı sürümü v5.6 sahip tek başına kümelerinde çalıştırılması gerekir ya da daha sonra.

### <a name="enable-the-repair-manager-service-if-its-not-running-already"></a>(Bu zaten çalışmıyorsa) onarım Yöneticisi hizmetini etkinleştirme

Düzeltme eki orchestration uygulama kümede etkinleştirilmesi için onarım Yöneticisi sistem hizmeti gerektirir.

#### <a name="azure-clusters"></a>Azure kümeleri

Gümüş dayanıklılık katmanı Azure kümelerinde varsayılan olarak etkin onarım Yöneticisi hizmeti sahip. Altın dayanıklılık katmanı Azure kümelerde olabilir ya da bu kümeleri oluşturulduğu bağlı olarak, etkin onarım Yöneticisi hizmeti sahip olmayabilir. Varsayılan olarak, Bronz dayanıklılık katmanı Azure kümelerde etkin onarım Yöneticisi hizmeti yok. Hizmet zaten etkin değilse, Service Fabric Explorer Sistem Hizmetleri bölümünde çalışmasını görebilirsiniz.

##### <a name="azure-portal"></a>Azure portalına
Kümenin kurma sırasında onarım Yöneticisi Azure portalından etkinleştirebilirsiniz. Seçin `Include Repair Manager` altında seçeneği `Add on features` küme yapılandırması zaman.
![Azure portalından etkinleştirme onarım Yöneticisi'nin resmi](media/service-fabric-patch-orchestration-application/EnableRepairManager.png)

##### <a name="azure-resource-manager-template"></a>Azure Resource Manager şablonu
Alternatif olarak kullanabileceğiniz [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm) yeni ve mevcut Service Fabric kümeleri üzerinde onarım Yöneticisi hizmeti etkinleştirmek için. Şablonu dağıtmak istediğiniz kümenin alın. Örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun. 

Onarım Yöneticisi hizmetini kullanarak etkinleştirmek için [Azure Resource Manager şablonu](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-via-arm):

1. İlk denetleyin `apiversion` ayarlanır `2017-07-01-preview` için `Microsoft.ServiceFabric/clusters` aşağıdaki kod parçacığında gösterildiği gibi kaynak. Farklı sonra güncelleştirmek gereken `apiVersion` değerine `2017-07-01-preview`:

    ```json
    {
        "apiVersion": "2017-07-01-preview",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
    }
    ```

2. Aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeatures` sonra bölümünde `fabricSettings` bölümü:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Bu değişikliklerle küme şablonunuzu güncelleştirildikten sonra bunları uygulamak ve son yükseltme sağlayabilirsiniz. Kümenizde çalışan onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz. Çağrılır `fabric:/System/RepairManagerService` Service Fabric Explorer Sistem Hizmetleri bölümünde. 

### <a name="standalone-on-premises-clusters"></a>Tek başına şirket içi kümeleri

Kullanabileceğiniz [tek başına Windows kümesi için yapılandırma ayarlarını](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest) yeni ve mevcut Service Fabric kümesi üzerinde onarım Yöneticisi hizmeti etkinleştirmek için.

Onarım Yöneticisi hizmeti etkinleştirmek için:

1. İlk denetleyin `apiversion` içinde [genel küme yapılandırmaları](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-manifest#general-cluster-configurations) ayarlanır `04-2017` veya üstü:

    ```json
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "04-2017",
        ...
    }
    ```

2. Aşağıdakileri ekleyerek onarım Yöneticisi hizmeti şimdi etkinleştirmek `addonFeaturres` sonra bölümünde `fabricSettings` bölümünde aşağıda gösterildiği gibi:

    ```json
    "fabricSettings": [
        ...      
        ],
        "addonFeatures": [
            "RepairManager"
        ],
    ```

3. Küme bildiriminizi güncelleştirilmiş küme bildirimini kullanarak bu değişikliklerle güncelleştirmek [yeni küme oluşturma](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-creation-for-windows-server) veya [küme yapılandırmasını yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-cluster-upgrade-windows-server#Upgrade-the-cluster-configuration). Küme güncelleştirilmiş küme bildirimini ile çalışmaya başladıktan sonra olarak adlandırılır, kümede çalışan onarım Yöneticisi sistem hizmeti şimdi görebilirsiniz `fabric:/System/RepairManagerService`altında sistem hizmetleri Service Fabric explorer bölümünde.

### <a name="disable-automatic-windows-update-on-all-nodes"></a>Tüm düğümlerde otomatik Windows Update devre dışı bırak

Aynı anda birden çok küme düğümüne yeniden başlatabilirsiniz olduğundan otomatik Windows güncelleştirmelerini kullanılabilirlik kaybına neden olabilir. Düzeltme eki orchestration uygulama varsayılan olarak, her küme düğümünde otomatik Windows Update devre dışı bırakmak çalışır. Ancak, ayarları Grup İlkesi veya bir yönetici tarafından yönetiliyorsa, "Bildirim önce karşıdan" Windows Update ilke açık olarak ayarlanması önerilir.

### <a name="optional-enable-azure-diagnostics"></a>İsteğe bağlı: Azure tanılamayı etkinleştirin

Service Fabric çalışma zamanı sürümü çalıştıran kümeler `5.6.220.9494` ve yukarıdaki toplama düzeltme eki orchestration uygulama günlükleri Service Fabric bir parçası olarak günlüğe kaydeder.
Kümenizi Service Fabric çalışma zamanı sürümünde çalışıyorsa, bu adımı atlayabilirsiniz `5.6.220.9494` ve üstü.

Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, düzeltme eki orchestration uygulama günlüklerini toplanan yerel olarak her küme düğümü.
Merkezi bir konuma tüm düğümlerdeki günlükleri karşıya yüklemek için Azure tanılama yapılandırmanızı öneririz.

Azure Tanılama'yı etkinleştirme hakkında daha fazla bilgi için bkz: [Azure tanılama kullanarak günlükleri toplamak](https://docs.microsoft.com/azure/service-fabric/service-fabric-diagnostics-how-to-setup-wad).

Düzeltme eki orchestration uygulama günlüklerini aşağıdaki sabit sağlayıcısında kimlikleri oluşturulur:

- e39b723c-590c-4090-abb0-11e3e6616346
- fc0028ff-bfdc-499f-80dc-ed922c52c5e9
- 24afa313-0d3b-4c7c-b485-1047fd964b60
- 05dc046c-60e9-4ef7-965e-91660adffa68

Resource Manager şablonu goto içinde `EtwEventSourceProviderConfiguration` altında bölümünde `WadCfg` ve aşağıdaki girdileri ekleyin:

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
> Birden çok düğüm türleri, Service Fabric kümesi var. sonra önceki bölümde tüm eklenmelidir `WadCfg` bölümler.

## <a name="download-the-app-package"></a>Uygulama paketi yükle

Uygulamayı karşıdan [bağlantı karşıdan](https://go.microsoft.com/fwlink/P/?linkid=849590).

## <a name="configure-the-app"></a>Uygulamayı yapılandırma

Düzeltme eki orchestration uygulamanın davranışı gereksinimlerinizi karşılayacak şekilde yapılandırılabilir. Uygulama oluşturma veya güncelleştirme işlemi sırasında uygulama parametresini geçirerek varsayılan değerleri geçersiz. Uygulama parametreleri belirterek sağlanabilir `ApplicationParameter` için `Start-ServiceFabricApplicationUpgrade` veya `New-ServiceFabricApplication` cmdlet'leri.

|**Parametre**        |**Tür**                          | **Ayrıntılar**|
|:-|-|-|
|MaxResultsToCache    |Uzun                              | Önbelleğe alınması gereken Windows Update sonuçlarının maksimum sayısı. <br>Varsayılan değer 3000 varsayılır: <br> -Düğüm sayısı 20'dir. <br> -Ayda bir düğümde gerçekleştiği güncelleştirme sayısı beştir. <br> -İşlemi başına sonuç sayısı 10 olabilir. <br> -Son üç ay için sonuçları depolanması gerekir. |
|TaskApprovalPolicy   |Enum <br> {NodeWise, UpgradeDomainWise}                          |Service Fabric küme düğümleri arasında Windows güncelleştirmelerini yüklemek için Koordinatör hizmeti tarafından kullanılacak ilkeyi TaskApprovalPolicy gösterir.<br>                         İzin verilen değerler: <br>                                                           <b>NodeWise</b>. Windows Update yüklü bir aynı anda düğümdür. <br>                                                           <b>UpgradeDomainWise</b>. Windows Update aynı anda yüklü bir yükseltme etki alanıdır. (Üst sınırda bir yükseltme etki alanına ait tüm düğümlerde Windows güncelleştirmesi gidebilirsiniz.)
|LogsDiskQuotaInMB   |Uzun  <br> (Varsayılan: 1024)               |Yerel olarak düğümlerinde kalıcı MB cinsinden en büyük boyutunu düzeltme eki orchestration uygulama kaydeder.
| WUQuery               | Dize<br>(Varsayılan: "IsInstalled = 0")                | Windows güncelleştirmelerini almak için sorgu. Daha fazla bilgi için bkz: [WuQuery.](https://msdn.microsoft.com/library/windows/desktop/aa386526(v=vs.85).aspx)
| InstallWindowsOSOnlyUpdates | bool <br> (varsayılan: True)                 | Bu bayrak Windows işletim sistemi güncelleştirmelerinin yüklenmesine izin verir.            |
| WUOperationTimeOutInMinutes | Int <br>(Varsayılan: 90).                   | (Arama veya indirme veya yükleme) herhangi bir Windows Update işlemi için zaman aşımını belirtir. İşlemi belirtilen zaman aşımı süresi içinde tamamlanmazsa durdurulur.       |
| WURescheduleCount     | Int <br> (Varsayılan: 5).                  | Bir işlem kalıcı olarak başarısız olursa en fazla kaç kez Windows hizmet reschedules güncelleştirin.          |
| WURescheduleTimeInMinutes | Int <br>(Varsayılan: 30). | Hata devam ederse durumunda, hizmet Windows update reschedules aralığı. |
| WUFrequency           | Virgülle ayrılmış dize (varsayılan: "Haftalık, Çarşamba, 7:00:00")     | Windows Update yükleme sıklığı. Biçim ve olası değerler şunlardır: <br>-Örneğin, aylık, 5, 12 aylık, gg ss: 22:32. <br> -Örneğin, haftalık, Salı, 12:22:32 için haftalık, gün, ss.  <br> -Örneğin, günlük, 12:22:32 günlük, ss.  <br> -Hiçbiri, Windows Update yapılması döndürmemelidir gösterir.  <br><br> Tüm saatler UTC biçiminde olduğunu unutmayın.|
| AcceptWindowsUpdateEula | bool <br>(Varsayılan: true) | Bu bayrak ayarlayarak, uygulamanın Windows Update için son kullanıcı lisans sözleşmesi makine sahibi adına kabul eder.              |

> [!TIP]
> Windows Update hemen olmasını istiyorsanız, ayarlayın `WUFrequency` uygulama dağıtım süresini göre. Örneğin, beş düğümlü test kümesi olduğunu ve yaklaşık 5: 00'da uygulama dağıtmayı planladığınız varsayalım UTC. Uygulama yükseltme veya dağıtım en 30 dakika sürer olduğunu varsayarsak, WUFrequency "Günlük, 17:30:00." ayarlayın.

## <a name="deploy-the-app"></a>Uygulamayı dağıtma

1. Küme hazırlama tüm önkoşul adımlarını tamamlayın.
2. Düzeltme eki orchestration uygulamayı başka bir Service Fabric uygulaması gibi dağıtın. PowerShell kullanarak uygulamayı dağıtabilirsiniz. Adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).
3. Geçişi dağıtım zamanında uygulama yapılandırmak için `ApplicationParamater` için `New-ServiceFabricApplication` cmdlet'i. Size kolaylık olması için uygulamanın yanı sıra Deploy.ps1 komut dosyası sağladık. Betik kullanmak için:

    - Bir Service Fabric kümeye bağlanırken `Connect-ServiceFabricCluster`.
    - Uygun olan Deploy.ps1 PowerShell betiğini yürütün `ApplicationParameter` değeri.

> [!NOTE]
> Komut dosyası ve uygulama klasörü PatchOrchestrationApplication aynı dizinde tutun.

## <a name="upgrade-the-app"></a>Uygulama yükseltme

PowerShell kullanarak var olan bir düzeltme eki orchestration uygulamaya yükseltmek için adımları [PowerShell kullanarak Service Fabric uygulama yükseltme](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-upgrade-tutorial-powershell).

## <a name="remove-the-app"></a>Uygulamayı kaldırma

Uygulamayı kaldırmak için adımları [PowerShell kullanarak uygulamaları dağıtma ve Kaldır](https://docs.microsoft.com/azure/service-fabric/service-fabric-deploy-remove-applications).

Size kolaylık olması için uygulamanın yanı sıra Undeploy.ps1 komut dosyası sağladık. Betik kullanmak için:

  - Bir Service Fabric kümeye bağlanırken ```Connect-ServiceFabricCluster```.

  - Undeploy.ps1 PowerShell betiğini yürütün.

> [!NOTE]
> Komut dosyası ve uygulama klasörü PatchOrchestrationApplication aynı dizinde tutun.

## <a name="view-the-windows-update-results"></a>Windows Update sonuçları görüntüleme

Düzeltme eki orchestration uygulama kullanıcıya geçmiş sonuçlarını görüntülemek için REST API'lerini kullanıma sunar. JSON sonuç örneği:
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
            "Description": "A security issue has been identified in a Microsoft software product that could affect your system. You can help protect your system by installing this update from Microsoft. For a complete listing of the issues that are included in this update, see the associated Microsoft Knowledge Base article. After you install this update, you may have to restart your system.",
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
Hiçbir güncelleştirme henüz zamanladıysanız JSON sonuç boştur.

Sorgu Windows Update kümeye sonuçları oturum açın. Ardından Coordinator hizmeti birincil çoğaltma adresi bulmak ve tarayıcı URL'den isabet: http://&lt;çoğaltma IP&gt;:&lt;ApplicationPort&gt;/PatchOrchestrationApplication/v1 / GetWindowsUpdateResults.

REST uç noktası Coordinator hizmeti için dinamik bir bağlantı noktası var. Tam URL'yi denetlemek için Service Fabric Explorer bakın. Örneğin, sonuçların kullanılabilir `http://10.0.0.7:20000/PatchOrchestrationApplication/v1/GetWindowsUpdateResults`.

![REST uç noktasını görüntüsü](media/service-fabric-patch-orchestration-application/Rest_Endpoint.png)


Ters proxy kümede etkinleştirilirse, küme de dışındaki URL'yi erişebilir.
Http:// isabet gereken uç noktadır&lt;SERVERURL&gt;:&lt;REVERSEPROXYPORT&gt;/PatchOrchestrationApplication/CoordinatorService/v1/GetWindowsUpdateResults.

Ters proxy küme üzerinde etkinleştirmek için adımları [ters proxy Azure Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-reverseproxy). 

> 
> [!WARNING]
> Ters proxy yapılandırıldıktan sonra bir HTTP uç noktası kullanıma tüm mikro hizmetler kümedeki küme dışında adreslenebilir.

## <a name="diagnosticshealth-events"></a>Tanılama/sistem durumu olayları

### <a name="collect-patch-orchestration-app-logs"></a>Toplama düzeltme eki orchestration uygulama günlükleri

Düzeltme eki orchestration uygulama günlükleri, çalışma zamanı sürümünden Service Fabric günlükleri bir parçası olarak toplanır `5.6.220.9494` ve üstü.
Service Fabric çalışma zamanı sürümü çalıştıran kümeler için değerinden `5.6.220.9494`, günlükleri aşağıdaki yöntemlerden birini kullanarak toplanmasını.

#### <a name="locally-on-each-node"></a>Her bir düğümde yerel olarak

Günlükleri toplanır yerel olarak her Service Fabric küme düğümünde Service Fabric çalışma zamanı sürümü ise değerinden `5.6.220.9494`. Günlükleri erişmek için konum \[Service Fabric\_yükleme\_sürücü\]:\\PatchOrchestrationApplication\\günlükleri.

Service Fabric D sürücüsünde yüklüyse, örneğin, D: yoludur\\PatchOrchestrationApplication\\günlükleri.

#### <a name="central-location"></a>Merkezi bir konum

Azure tanılama önkoşul adımlarını bir parçası olarak yapılandırılmışsa, düzeltme eki orchestration uygulama günlüklerini Azure depolama alanında kullanılabilir.

### <a name="health-reports"></a>Sistem durumu raporları

Düzeltme eki orchestration uygulama sistem durumu raporlarının Düzenleyicisi hizmeti veya düğüm Aracısı hizmeti karşı aşağıdaki durumlarda da yayımlar:

#### <a name="a-windows-update-operation-failed"></a>Windows Update işlemi başarısız oldu

Bir düğümde Windows güncelleştirme işlemi başarısız olursa, bir sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur. Sistem Durumu raporu ayrıntılarını sorunlu bir düğüm adı içeriyor.

Düzeltme eki uygulama sorunlu bir düğüm üzerinde başarıyla tamamlandıktan sonra raporu otomatik olarak temizlenir.

#### <a name="the-node-agent-ntservice-is-down"></a>Düğüm Aracısı NTService çalışmıyor

Düğüm Aracısı NTService bir düğümde çalışmıyorsa, bir uyarı düzeyi sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur.

#### <a name="the-repair-manager-service-is-not-enabled"></a>Onarım Yöneticisi hizmeti etkin değil

Onarım Yöneticisi hizmeti kümede bulunmazsa, bir uyarı düzeyi sistem durumu raporu Düzenleyicisi hizmeti için oluşturulur.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular

Q. **Düzeltme eki orchestration uygulama çalışırken neden bir hata durumuna my küme görüyor?**

A. Yükleme işlemi sırasında düzeltme eki orchestration uygulama devre dışı bırakır veya geçici olarak giderek küme durumunu sonuçlanabilir düğümleri yeniden başlatılır.

İlke uygulama için bağlı olarak, herhangi bir düğümün bir düzeltme eki uygulama işlemi sırasında gidebilirsiniz *veya* tüm yükseltme etki alanı aynı anda Git aşağı.

Windows Update yükleme sonuna düğümlerin yeniden iler hale getirilir yeniden başlatma gönderin.

Bir hata durumu kümeyi aşağıdaki örnekte, geçici olarak oluştu çünkü iki düğüm olan aşağı ve MaxPercentageUnhealthNodes ilke ihlal. Düzeltme eki uygulama işlemi devam eden olana kadar geçici bir hatadır.

![Sağlıksız küme görüntüsü](media/service-fabric-patch-orchestration-application/MaxPercentage_causing_unhealthy_cluster.png)

Sorun devam ederse, sorun giderme bölümüne bakın.

Q. **Düzeltme eki orchestration uygulama uyarı durumunda**

A. Uygulamaya karşı gönderilen bir sistem durumu raporu kök neden olup olmadığını denetleyin. Genellikle, uyarı sorunun ayrıntılarını içerir. Sorun geçici ise, uygulama otomatik kurtarma bu durumdan olması beklenir.

Q. **My küme sağlıksız ise ve Acil işletim sistemi güncelleştirmesi yapmanız ne yapabilirim?**

A. Küme sağlıksız durumdayken düzeltme eki orchestration uygulama güncelleştirmelerini yüklemez. Kümenizi düzeltme eki orchestration uygulama iş akışı engellemesini kaldırmak için sağlıklı bir duruma getirmek deneyin.

Q. **Neden kümelerinde düzeltme eki uygulama kadar çalıştırmak için sürer?**

A. Düzeltme eki orchestration uygulama tarafından gereken süre genellikle aşağıdaki etkenlere bağlıdır:

- Düzenleyici hizmet ilkesi. 
  - Varsayılan ilke `NodeWise`, sonuçlarını aynı anda yalnızca tek bir düğüme düzeltme eki uygulama içinde. Özellikle büyük kümeleri söz konusu olduğunda, kullanmanızı öneririz `UpgradeDomainWise` kümeler arasında daha hızlı düzeltme eki uygulama elde etmek için ilke.
- İndirme ve yükleme için kullanılabilir güncelleştirmeleri sayısı. 
- Karşıdan yüklemek ve bir güncelleştirmeyi yüklemek için gereken ortalama süre, birkaç saat aşamaz.
- VM ve ağ bant genişliği performans.

Q. **Bazı güncelleştirmeler Windows Update sonuçlarında REST API'nin aracılığıyla ancak makinede Windows Update geçmişi altında elde neden görüyor musunuz?**

A. Bazı ürün güncelleştirmelerini ilgili güncelleştirme/düzeltme eki geçmişlerini denetlenmesi gerekir. Örneğin: Windows Defender'ın güncelleştirmeleri Windows Update geçmişinde Windows Server 2016 görünmüyor.

## <a name="disclaimers"></a>Bildirimler

- Düzeltme eki orchestration uygulama Windows Update, son kullanıcı lisans sözleşmesi kullanıcı adına kabul eder. İsteğe bağlı olarak, ayar uygulama yapılandırmasında kapatılabilir.

- Düzeltme eki orchestration uygulama kullanımını ve performansını izlemek için telemetri toplar. Uygulamanın telemetri (varsayılan olarak etkindir) Service Fabric çalışma zamanı telemetri ayarını ayarı izler.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="a-node-is-not-coming-back-to-up-state"></a>Bir düğüm geri durumu yukarı geliyor değil

**Düğümü devre dışı bırakma durumunda olduğundan takılmış olabilir**:

Güvenlik onay bekliyor. Bu durumu düzeltmek için sağlam bir durumda yeterli düğüm kullanılabilir olduğundan emin olun.

**Düğümü devre dışı durumda olduğundan takılmış olabilir**:

- Düğüm el ile devre dışı bırakıldı.
- Düğüm, devam eden Azure altyapı iş nedeniyle devre dışı bırakıldı.
- Düğüm düğüm düzeltme eki için düzeltme eki orchestration uygulama tarafından geçici olarak devre dışı bırakıldı.

**Düğüm aşağı bir durumda olduğundan takılmış olabilir**:

- Düğüm aşağı durumda el ile askıya alınmış.
- Düğüm (hangi düzeltme eki orchestration uygulama tarafından tetiklenen) yeniden yapılıyor.
- Düğümü hatalı VM veya makine ya da ağ bağlantısı sorunları nedeniyle çalışmıyor.

### <a name="updates-were-skipped-on-some-nodes"></a>Güncelleştirmeleri bazı düğümler üzerinde atlandı

Düzeltme eki orchestration uygulama bir Windows güncelleştirmesi yeniden zamanlama ilkesine göre yüklemeye çalışır. Düğüm kurtarmak ve uygulama ilkesi göre güncelleştirme atlamak hizmeti çalışır.

Böyle bir durumda, bir uyarı düzeyi sistem durumu raporu karşı düğüm Aracısı hizmeti oluşturulur. Windows Update için sonucu hatanın olası nedenini de içerir.

### <a name="the-health-of-the-cluster-goes-to-error-while-the-update-installs"></a>Güncelleştirmeyi yüklerken küme durumunu hata durumuna geçer

Bir uygulama veya belirli düğüme veya yükseltme etki alanı küme durumunu aşağı hatalı bir Windows güncelleştirmesi kullanıma sunabilirsiniz. Düzeltme eki orchestration uygulama kümeye yeniden sağlıklı duruma gelene kadar sonraki tüm Windows Update işlemi sona erdirir.

Bir yönetici, müdahale ve uygulama ya da küme neden nedeniyle Windows Update sağlıksız olduğunu belirler.

## <a name="release-notes-"></a>Sürüm Notları:

### <a name="version-110"></a>Sürüm 1.1.0
- Ortak sürüm

### <a name="version-111"></a>Sürüm 1.1.1
- Bir hata SetupEntryPoint, NodeAgentNTService yüklemesini engelleyen NodeAgentService içinde sabit.

### <a name="version-120-latest"></a>Sürüm 1.2.0 (en yeni)

- Hata düzeltmeleri sistem geçici iş akışını yeniden başlatın.
- Hangi sistem durumu nedeniyle, beklendiği gibi onarım görevlerin hazırlanması sırasında onay gerçekleştiği değildi RM görevler oluşturma hata düzeltmesi.
- Windows POANodeSvc otomatik otomatik Gecikmeli hizmetinin başlangıç modu değiştirildi.
