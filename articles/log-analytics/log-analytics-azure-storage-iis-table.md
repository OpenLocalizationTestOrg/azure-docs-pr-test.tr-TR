---
title: "Azure günlük analizi olayları için IIS ve tablo depolama için aaaUse blob depolama | Microsoft Docs"
description: "Günlük analizi tanılama tootable depolama yazma Azure Hizmetleri için hello günlüklerini veya tooblob depolama yazılmış IIS günlüklerini okuyabilir."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Günlük analizi olan olaylar için IIS ve Azure tablo depolaması için Azure blob storage kullanma

Günlük analizi depolama veya IIS yazılı tooblob depolama oturum tanılama tootable yazma Hizmetleri aşağıdaki hello hello günlüklerini okuyabilirsiniz:

* Service Fabric kümeleri (Önizleme)
* Virtual Machines
* Web/çalışan rolleri

Azure tanılama günlük analizi bu kaynakları için veri toplayabilmek için önce etkinleştirilmesi gerekir.

Tanılama etkinleştirildikten sonra hello Azure portalını kullanabilirsiniz veya PowerShell günlük analizi toocollect hello günlükleri yapılandırın.

Azure tanılama toocollect Tanılama verileri çalışan rolü, web rolü veya Azure'da çalışan sanal makine sağlayan Azure uzantısıdır. Merhaba veriler bir Azure depolama hesabında depolanır ve günlük analizi tarafından toplanabilir.

Günlük analizi toocollect için bu Azure tanılama günlükleri, aşağıdaki konumlardan hello hello günlükleri olması gerekir:

| Günlük türü | Kaynak Türü | Konum |
| --- | --- | --- |
| IIS günlükleri |Virtual Machines <br> Web rolleri <br> Çalışan rolleri |wad IIS logfiles (Blob Depolama) |
| Syslog |Virtual Machines |LinuxsyslogVer2v0 (Tablo depolama) |
| Service Fabric çalışma olayları |Service Fabric düğümler |WADServiceFabricSystemEventTable |
| Service Fabric güvenilir aktör olayları |Service Fabric düğümler |WADServiceFabricReliableActorEventTable |
| Service Fabric güvenilir hizmeti olayları |Service Fabric düğümler |WADServiceFabricReliableServiceEventTable |
| Windows olay günlükleri |Service Fabric düğümler <br> Virtual Machines <br> Web rolleri <br> Çalışan rolleri |WADWindowsEventLogsTable (Tablo depolama) |
| Windows ETW günlükleri |Service Fabric düğümler <br> Virtual Machines <br> Web rolleri <br> Çalışan rolleri |WADETWEventTable (Tablo depolama) |

> [!NOTE]
> Azure Web siteleri IIS günlükleri şu anda desteklenmemektedir.
>
>

Sanal makineler için hello yükleme hello seçeneğiniz [günlük analizi aracı](log-analytics-azure-vm-extension.md) sanal makine tooenable ek Öngörüler içine. Ayrıca toobeing mümkün tooanalyze IIS günlüklerini ve olay günlüklerini, yapılandırma değişiklik izleme, SQL değerlendirmesi ve güncelleştirme değerlendirme dahil olmak üzere ek analiz gerçekleştirebilirsiniz.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu olay günlüğünü ve IIS günlüğü için
Koleksiyon hello Microsoft Azure portal kullanarak olay günlüğünü ve IIS günlüğü için aşağıdaki yordamı tooenable bir sanal makinede Azure tanılama kullanım hello.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable Azure Tanılama'hello Azure portal ile bir sanal makine
1. Bir sanal makine oluşturduğunuzda hello VM aracısı yükleyin. Merhaba sanal makine zaten varsa, VM aracısının yüklü olduğundan bu hello doğrulayın.

   * İçinde Azure portal Merhaba, toohello sanal makine gidin, seçin **isteğe bağlı yapılandırma**, ardından **tanılama** ve **durum** çok**üzerinde**.

     Tamamlandıktan sonra hello VM yüklü ve çalışan hello Azure tanılama uzantısına sahiptir. Tanılama verilerinin toplanması için bu uzantıyı sorumludur.
2. İzlemeyi etkinleştirmek ve olay günlüğü var olan bir VM yapılandırın. Tanılama hello VM düzeyi adresindeki etkinleştirebilirsiniz. tooenable tanılama ve olay günlüğünü yapılandırmak, hello aşağıdaki adımları gerçekleştirin:

   1. Merhaba VM seçin.
   2. Tıklatın **izleme**.
   3. Tıklatın **tanılama**.
   4. Set hello **durum** çok**ON**.
   5. Toocollect istediğiniz her tanılama günlük seçin.
   6. **Tamam** düğmesine tıklayın.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Web rolü IIS günlüğü ve olay toplama için Azure tanılama etkinleştir
Çok başvuran[nasıl tooEnable bir bulut hizmetinde tanılama](../cloud-services/cloud-services-dotnet-diagnostics.md) Azure tanılama etkinleştirme genel adımlar için. Merhaba yönergelerde bu bilgileri kullanın ve günlük analizi ile kullanılmak üzere özelleştirin.

Azure Tanılama ile etkin:

* IIS günlüklerini hello scheduledTransferPeriod aktarımı aralıklarla günlük verileri varsayılan olarak depolanır.
* Windows olay günlüklerini varsayılan olarak aktarılmaz.

### <a name="tooenable-diagnostics"></a>tooenable tanılama
Windows olay günlüklerini tooenable veya toochange scheduledTransferPeriod Merhaba, gösterildiği gibi Azure hello XML yapılandırma dosyası (diagnostics.wadcfg) kullanarak tanılama Yapılandır [4. adım: Tanılama yapılandırma dosyanızı oluşturun ve hello yükleyin uzantısı](../cloud-services/cloud-services-dotnet-diagnostics.md)

Merhaba aşağıdaki örnek yapılandırma dosyası IIS günlüklerini ve tüm olayları hello uygulama ve sistem günlüklerini toplar:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

ConfigurationSettings aşağıdaki örneğine hello gibi bir depolama hesabı belirttiğinden emin olun:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Merhaba **AccountName** ve **AccountKey** değerleri hello erişim anahtarlarını Yönet altında hello depolama hesabı Panosu Azure portalında bulundu. Merhaba bağlantı dizesi için Hello Protokolü olmalıdır **https**.

Merhaba güncelleştirilmiş tanılama yapılandırması uygulandıktan sonra tooyour bulut hizmeti ve yazılırken tanılama tooAzure depolama, ardından hazır tooconfigure günlük analizi olur.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Azure depolama biriminden Hello Azure portal toocollect günlüklerini kullanın
Hello Azure portal tooconfigure günlük analizi toocollect hello günlükleri, Azure Hizmetleri aşağıdaki hello için kullanabilirsiniz:

* Service Fabric kümeleri
* Virtual Machines
* Web/çalışan rolleri

Hello Azure portal, tooyour günlük analizi çalışma alanına gidin ve hello aşağıdaki görevleri gerçekleştirin:

1. Tıklatın *depolama hesapları günlükleri*
2. Merhaba tıklatın *Ekle* görevi
3. Merhaba tanılama günlükleri içeren hello depolama hesabı seçin
   * Bu hesap, Klasik depolama hesabı veya bir Azure Resource Manager depolama hesabı olabilir.
4. Merhaba toocollect günlükleri için istediğiniz veri türünü seçin
   * Merhaba, IIS günlüklerini seçimlerdir; Olayları; Syslog (Linux); ETW günlükleri; Hizmeti yapı olayları
5. veri türü ve değiştirilemez hello üzerinde temel kaynak Hello değeri otomatik olarak doldurulur
6. Tamam toosave hello Yapılandırması'nı tıklatın

Günlük analizi toocollect istediğiniz ek depolama hesapları ve veri türleri için 2-6 adımlarını yineleyin.

Günlük analizi depolama hesabında hello mümkün toosee verilerden olduğunuz yaklaşık 30 dakika içinde. Merhaba yapılandırma uygulandıktan sonra toostorage yazılan veriler yalnızca görürsünüz. Günlük analizi hello depolama hesabından hello önceden mevcut verileri okuyamadı.

> [!NOTE]
> Hello portal kaynağı var hello depolama hesabında bu hello doğrulanmadı veya yeni veriler yazılır.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Bir sanal makinede Azure tanılamayı etkinleştirin koleksiyonu PowerShell kullanarak olay günlüğünü ve IIS günlüğü için
Kullanım hello adımları [yapılandırma günlük analizi tooindex Azure tanılama](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse PowerShell tooread tootable depolama yazılır Azure tanılama gelen.

Azure PowerShell kullanarak depolama tooAzure yazılır hello olayları daha kesin olarak belirtebilirsiniz.
Daha fazla bilgi için bkz: [etkinleştirme tanılama Azure Virtual Machines'de](../virtual-machines-dotnet-diagnostics.md).

Etkinleştirmek ve PowerShell Betiği aşağıdaki hello kullanarak Azure tanılama güncelleştirin.
Bu komut dosyasını bir özel günlük kaydı yapılandırmasıyla de kullanabilirsiniz.
Merhaba betik tooset hello depolama hesabı, hizmet adı ve sanal makine adını değiştirin.
Merhaba betik Klasik sanal makineleri için cmdlet'leri kullanır.

Komut dosyası örneği aşağıdaki hello gözden geçirin, kopyalayın, gerektiği şekilde değiştirin, hello örnek bir PowerShell komut dosyası olarak kaydetmek ve hello betiğini çalıştırın.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Sonraki adımlar
* [Günlük ve Azure Hizmetleri için ölçümleri toplamak](log-analytics-azure-storage.md) desteklenen Azure Hizmetleri.
* [Çözümlerle](log-analytics-add-solutions.md) hello veri tooprovide fikirler.
* [Arama sorguları kullanmak](log-analytics-log-searches.md) tooanalyze hello veri.
