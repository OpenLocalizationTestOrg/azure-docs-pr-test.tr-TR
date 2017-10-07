---
title: "aaaAdd izleme ve tanılama tooan Azure sanal makinesi | Microsoft Docs"
description: "Bir Azure Kaynak Yöneticisi şablonu toocreate yeni bir Windows sanal makine ile Azure tanılama uzantısını kullanır."
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>İzleme ve tanılama Windows VM ve Azure Resource Manager şablonları ile kullanın.
Hello Azure tanılama uzantısını hello izleme sağlar ve tanılama yetenekleri bir Windows Azure sanal makine tabanlı. Bu özellikler hello sanal makineye hello azure resource manager şablonu bir parçası olarak hello uzantısı dahil olmak üzere etkinleştirebilirsiniz. Bkz: [VM uzantıları ile Azure Resource Manager şablonları yazma](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) uzantıyı bir sanal makine şablonunun parçası olarak dahil olmak üzere daha fazla bilgi. Bu makalede hello Azure tanılama uzantısını tooa windows sanal makine şablonu nasıl ekleyebileceğiniz açıklanmaktadır.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Hello Azure tanılama toohello VM kaynak tanımı uzantısı Ekle
tooenable hello tanılama uzantısını üzerinde bir Windows sanal bir VM kaynak olarak tooadd hello uzantısı gerekir makine Resource manager şablonu hello.

İçin basit bir Resource Manager tabanlı sanal makine Ekle hello uzantısı yapılandırma toohello *kaynakları* dizi hello sanal makine için: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Başka bir ortak kuralı ekleyin hello uzantı yapılandırması hello kök kaynakları düğümde hello sanal makinenin kaynakları düğümünde tanımlama yerine hello şablonunun. Bu yaklaşımda hello uzantısı ile Merhaba sanal makine arasındaki hiyerarşik bir ilişki ile Merhaba belirtin tooexplicitly sahip *adı* ve *türü* değerleri. Örneğin: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

Merhaba uzantısı hello sanal makineyle ilişkili her zaman, ya da doğrudan hello sanal makinenin kaynak düğümünde doğrudan tanımlayın veya hello temel düzeyde tanımlamak ve hello hiyerarşik adlandırma kuralı tooassociate kullanmak hello sanal ile Makine.

Sanal makine ölçek kümeleri hello uzantıları hello belirtilen yapılandırma *extensionProfile* hello özelliğinin *VirtualMachineProfile*.

Merhaba *yayımcı* hello değerini özelliğiyle **Microsoft.Azure.Diagnostics** ve hello *türü* hello değerini özelliğiyle **IaaSDiagnostics** hello Azure tanılama uzantısını benzersiz şekilde tanımlar.

Merhaba hello değerini *adı* özelliği kullanılan toorefer toohello uzantısı hello kaynak grubunda olması olabilir. Özellikle çok ayarı**Microsoft.Insights.VMDiagnosticsSettings** kolayca izleme grafikleri Göster yukarı doğru hello Azure portal hello Azure portal sağlama hello tarafından tanımlanan toobe olanak sağlar.

Merhaba *typeHandlerVersion* hello sürümünü belirten hello uzantısı toouse istersiniz. Ayarı *autoUpgradeMinorVersion* çok ikincil sürüm**true** kullanılabilir hello uzantısı'nın en son alt sürüm hello alırsınız sağlar. Her zaman ayarlamanız önerilir *autoUpgradeMinorVersion* tooalways olması **true** böylece her zaman toouse hello tüm hello yeni özellikler ve hata ile en son kullanılabilir tanılama uzantısını Al giderir. 

Merhaba *ayarları* öğesi ayarlayın ve geri hello uzantısı (bazen başvurulan tooas ortak yapılandırma) okuma hello uzantısı yapılandırmaları özelliklerini içerir. Merhaba *xmlcfg* özelliği içeren xml tabanlı yapılandırma hello tanılama günlükleri, performans sayaçları hello tanılama aracısı tarafından toplanan vs. Bkz: [tanılama yapılandırma şeması](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello xml şeması kendisi hakkında daha fazla bilgi. Değişkeni hello Azure Resource Manager şablonu ve ardından Birleştir ve base64 bunları tooset hello değeri için kodlama gibi yaygın bir toostore hello gerçek xml yapılandırması uygulamadır *xmlcfg*. Merhaba bölümüne bakarak [tanılama yapılandırma değişkenleri](#diagnostics-configuration-variables) toounderstand nasıl toostore hello değişkenleri XML'de hakkında daha fazla bilgi. Merhaba *storageAccount* özellik belirtir hello depolama hesabı toowhich tanılama verilerini hello adını aktarılmayacak. 

Merhaba özelliklerinde *protectedSettings* (bazen başvurulan tooas özel yapılandırma) ayarlanabilir, ancak geri ayarlanmasından sonra okunamıyor. salt yazılır yapısını Hello *protectedSettings* hello depolama hesabı anahtarı gibi parolaları depolamak için yararlı hello tanılama verilerini yazılacağı kolaylaştırır.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Parametre olarak tanılama depolama hesabı belirtme
Merhaba tanılama uzantısını json parçacığı Yukarıdaki iki parametre varsayar *existingdiagnosticsStorageAccountName* ve *existingdiagnosticsStorageResourceGroup* toospecify hello tanılama Tanılama verilerini depolanacağı depolama hesabı. Merhaba tanılama depolama hesabı belirten isteğe bağlı olarak bir parametreyi kolay toochange hello tanılama depolama hesabı yapar gibi farklı ortamlar genelinde örn, toouse farklı tanılama depolama hesabı için farklı bir test ve için isteyebilirsiniz, Üretim dağıtımı.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

En iyi yöntem toospecify tanılama depolama hesabı hello kaynak grubundan hello sanal makine için farklı bir kaynak grubunda değil. Bir kaynak grubu toobe kendi ömrü sahip bir dağıtım birimi kabul edilebilir, bir sanal makine dağıtılabilir ve yeni yapılandırmaları güncelleştirmeleri gerçekleştirilmediğinden imzalanmasını tooit ancak hello hello tanılama veri depolama toocontinue isteyebilir aynı depolama hesabı Bu sanal makine dağıtımlar arasında. Farklı kaynak etkinleştirir hello depolama hesabı tooaccept veri kolay tootroubleshoot yapmadan çeşitli sanal makine dağıtımlarından Hello depolama hesabına sahip olunması çeşitli sürümler arasında sorunları hello.

> [!NOTE]
> Merhaba varsayılan depolama hesabı ayarlayabilirsiniz Visual Studio'dan bir windows sanal makine şablonu oluşturursanız toouse hello sanal makine VHD burada karşıya aynı depolama hesabındaki hello. Merhaba VM ilk kurulumu toosimplify budur. Merhaba şablonu toouse parametre olarak geçirilebilir farklı depolama hesabı yeniden bulundurmanız gerekir. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Tanılama yapılandırma değişkenleri
Merhaba tanılama uzantısını json parçacığı yukarıdaki tanımlayan bir *AccountID* değişken toosimplify hello depolama hesabı anahtarı hello tanılama depolama alınıyor:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Merhaba *xmlcfg* hello tanılama uzantısını özelliği birlikte birleştirilmiş birden çok değişkenleri kullanılarak tanımlanır. Merhaba json değişkenleri ayarlarken doğru bir şekilde Atlanan toobe ihtiyaç duydukları şekilde hello bu değişkenlerin XML'de değerlerdir.

Bazı windows olay günlüklerini ve tanılama altyapı günlükleri ile birlikte standart sistem düzeyinde performans sayaçlarını toplar hello tanılama yapılandırması xml Hello açıklanmıştır. Bunu olduğundan kaçışlı ve böylece hello yapılandırma doğrudan şablonunuzun değişkenleri bölüme hello yapıştırılabilmesi için doğru biçimlendirilmiş. Merhaba bkz [tanılama yapılandırma şeması](https://msdn.microsoft.com/library/azure/dn782207.aspx) hello yapılandırma xml İnsan daha okunabilir bir örneğin.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

Hello ölçümleri tanım xml yapılandırma yukarıda hello düğümünde olduğu önemli yapılandırma öğesi nasıl hello performans sayaçları önceki hello xml dosyasında tanımlanan tanımlar gibi *PerformanceCounter* düğüm araya getirilir ve depolanır. 

> [!IMPORTANT]
> Bu ölçümler grafikler ve hello Azure portalında uyarılar izleme hello sürücü.  Merhaba **ölçümleri** hello düğümle *ResourceId* ve **MetricAggregation** toosee hello VM istiyorsanız, VM için hello tanılama yapılandırmasında eklenmelidir hello Azure portal izleme verileri. 
> 
> 

Merhaba, ölçüm tanımlarını hello xml örneği aşağıdadır: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Merhaba *ResourceId* özniteliği benzersiz olarak tanımlayan aboneliğinizde hello sanal makine. Toouse hello subscription() emin olun ve hello şablonu otomatik olarak dağıttığınız hello abonelik ve kaynak grubuna göre bu değerleri güncelleştirilebilmesi için resourceGroup() çalışır.

Birden çok sanal makine bir döngüde oluşturmakta olduğunuz sonra toopopulate hello olacaktır *ResourceId* copyındex () işlevini toocorrectly değerle birbirinden ayrı ayrı her VM. Merhaba *xmlCfg* değeri güncelleştirilmiş toosupport bu aşağıdaki gibi olabilir:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

MetricAggregation değerini hello *PT1H* ve *PT1M* bir dakika içinde bir toplama ve bir saat içinde bir toplama türünü belirtir.

## <a name="wadmetrics-tables-in-storage"></a>Depolama WADMetrics tabloları
Hello ölçümleri yapılandırma yukarıdaki tablolarda tanılama depolama hesabınızdaki adlandırma kurallarına hello ile üretir:

* **WADMetrics** : tüm WADMetrics tablolar için standart bir önek
* **PT1H** veya **PT1M** : hello tablosunun içeren veri toplama üzerinde 1 saat veya 1 dakika belirtir
* **P10D** : hello tablo hello tablo veri toplama başladığında gelen 10 gün için veri içerecek belirtir
* **V2S** : dize sabiti
* **yyyyaagg** : hello tarih hangi hello başlatıldı verileri toplama

Örnek: *WADMetricsPT1HP10DV2S20151108* 11-Kas-2015 tarihinde başlayan 10 günlük bir saate üzerinden toplanan ölçümleri veri içermez    

Her WADMetrics tablo sütunları aşağıdaki hello içerir:

* **PartitionKey**: Merhaba partitionkey üzerinde hello göre yapılandırılmıştır *ResourceId* değeri toouniquely hello VM kaynak belirleyin. için örn: 002Fsubscriptions:<subscriptionID>: 002FresourceGroups:002F<ResourceGroupName>: 002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : aşağıdaki hello biçimi <Descending time tick>:<Performance Counter Name>. süresi onay hesaplaması azalan hello hello toplama dönemi hello başlangıcından hello süresini eksi max zaman ticks ' dir. Örneğin Merhaba örnek süresi 10-Kas-2015 tarihinde başlatılır ve 00:00Hrs UTC sonra hello hesaplama olacaktır: DateTime.MaxValue.Ticks - (yeni DateTime(2015,11,10,0,0,0,DateTimeKind.Utc). Ticks). Merhaba bellek kullanılabilir bayt sayısı performans sayacı hello satır anahtarını görüneceğini için ister: 2519551871999999999__:005CMemory:005CAvailable:0020 bayt
* **CounterName** : hello performans sayacı hello adıdır. Bu hello eşleşen *counterSpecifier* hello xml yapılandırma dosyasında tanımlanmış.
* **En fazla** : Merhaba hello performans sayacı en büyük değerini hello toplama süresi içinde.
* **En düşük** : hello toplama süresi içinde hello hello performans sayacı en küçük değeri.
* **Toplam** : hello hello performans sayacı tüm değerlerin toplamını hello toplama süresi içinde bildirdi.
* **Count** : hello performans sayacı için bildirilen hello değerleri toplam sayısı.
* **Ortalama** : hello toplama süresi içinde hello hello performans sayacının ortalama (toplam/sayısı) değeri.

## <a name="next-steps"></a>Sonraki Adımlar
* Windows sanal makinesi tanılama uzantısını içeren tam örnek şablonu için bkz: [201-vm-monitoring-tanılama-uzantısı](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Merhaba resource manager şablonunu kullanarak dağıtın [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Azure komut satırı](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Daha fazla bilgi edinmek [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md)

