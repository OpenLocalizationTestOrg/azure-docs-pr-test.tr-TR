---
title: "Azure Data Factory aaaTroubleshoot sorunları"
description: "Azure Data Factory kullanarak tootroubleshoot nasıl sorunlar hakkında bilgi edinin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Data Factory'de sorun giderme
Bu makalede Azure Data Factory kullanırken sorunlarıyla ilgili sorun giderme ipuçları sağlar. Bu makalede tüm hello olası sorunları hello hizmetini kullanırken listelenmez, ancak bazı sorunlar ve genel sorun giderme ipuçları kapsar.   

## <a name="troubleshooting-tips"></a>Sorun giderme ipuçları
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Hata: hello abonelik 'Microsoft.DataFactory' kayıtlı toouse ad değil.
Bu hata iletisini alırsanız hello Azure Data Factory kaynak sağlayıcısı makinenizde kayıtlı değil. Aşağıdaki hello:

1. Azure PowerShell’i çalıştırın.
2. Tooyour içinde Azure hesabı komutu aşağıdaki hello kullanarak oturum açın.

    ```powershell
    Login-AzureRmAccount
    ```
3. Komut tooregister hello Azure Data Factory sağlayıcısının aşağıdaki hello çalıştırın.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Sorun: bir Data Factory cmdlet çalıştırıldığında yetkisiz hata
Merhaba sağ Azure hesabı veya abonelik hello Azure PowerShell ile kullanmakta olduğunuz olmayabilir. Cmdlet'leri tooselect hello sağ hello Azure PowerShell ile Azure hesabınızı ve aboneliğinizi toouse aşağıdaki hello kullanın.

1. Login-AzureRmAccount - kullanım hello doğru kullanıcı kimliği ve parolası
2. Get-AzureRmSubscription - tüm hello hello hesabı için abonelik görünümü.
3. Select-AzureRmSubscription &lt;abonelik adı&gt; -hello doğru abonelik seçin. Kullanım hello aynı toocreate data factory hello Azure portalı üzerinde kullanın.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Sorun: Azure portalından toolaunch veri yönetimi ağ geçidi hızlı kurulum başarısız
Merhaba hızlı kurulum hello veri yönetimi ağ geçidi için Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı gerektirir. Toostart Hello hızlı kurulum başarısız olursa hello aşağıdakilerden birini yapın:

* Internet Explorer veya Microsoft ClickOnce uyumlu bir web tarayıcısı kullanın.

    Chrome kullanıyorsanız, toohello Git [Chrome web mağazası](https://chrome.google.com/webstore/), arama "ClickOnce" sözcüğünü, hello ClickOnce uzantıları birini seçin ve yükleyin.

    Firefox (yükleme eklenti) aynı hello. Merhaba araç çubuğu (Merhaba sağ üst köşedeki üç yatay çizgi) menü Aç düğmesini tıklatın, eklentiler'i tıklatın, "ClickOnce" sözcüğünü arama, hello ClickOnce uzantıları birini seçin ve yükleyin.
* Kullanım hello **el ile Kurulum** hello üzerinde gösterilen bağlantı aynı dikey penceresinde hello portal. Bu yaklaşım toodownload yükleme dosyasını kullanın ve el ile çalıştırın. Merhaba yükleme başarılı olduktan sonra hello veri yönetimi ağ geçidi yapılandırması iletişim kutusu görebilirsiniz. Kopya hello **anahtar** hello portal ekran ve hello hizmeti ile Merhaba configuration manager toomanually içinde kaydetmek hello ağ geçidi kullanın.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Sorun: Başarısız tooconnect tooon içi SQL Server
Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** hello ağ geçidi makinesi ve hello kullan **sorun giderme** hello ağ geçidi makineden tootest hello bağlantı tooSQL sunucu sekmesinde. Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) ilgili sorunlar bağlantı/ağ geçidi sorun giderme ipuçları için.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Sorun: Durumu için herhangi bir zamanda bekleyen giriş dilimler olur
Merhaba dilimler olabilir **bekleyen** toovarious nedeniyle son durum. Bu hello hello yaygın nedenlerinden biridir **dış** özelliği çok ayarlanmamışsa**doğru**. Azure Data Factory üretilen dış hello kapsamı herhangi bir veri kümesi ile işaretlenmelidir **dış** özelliği. Bu özellik hello veri dış ve hello veri fabrikası içinde herhangi bir ardışık düzen tarafından yedeklenen olduğunu gösterir. Merhaba veri dilimi olarak işaretlenmiş **hazır** hello veri hello ilgili deposunda kullanılabilir olduğunda.

Merhaba hello kullanım için örneği aşağıdaki hello bkz **dış** özelliği. İsteğe bağlı olarak belirtebilirsiniz **externalData*** dış tootrue ayarlandığında.

Bkz: [veri kümeleri](data-factory-create-datasets.md) bu özellik hakkında daha fazla ayrıntı için makale.

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

tooresolve Merhaba hata, hello eklemek **dış** özelliği ve isteğe bağlı hello **externalData** bölümünde toohello JSON hello giriş tablosu tanımını ve hello tablo oluşturun.

### <a name="problem-hybrid-copy-operation-fails"></a>Sorun: Karma kopyalama işlemi başarısız
Bkz: [ağ geçidi sorunlarını giderme](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) adımları tootroubleshoot sorunlar kopyalama/şirket içi veri depolama kullanarak veri yönetimi ağ geçidi hello için.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Sorun: başarısız sağlama isteğe bağlı Hdınsight
Bağlı hizmet türü HDInsightOnDemand kullanırken toospecify tooan Azure Blob Storage işaret eden bir linkedServiceName gerekir. Data Factory Hizmeti'ne isteğe bağlı Hdınsight kümeniz için bu depolama toostore günlüklerine ve Destek dosyalarını kullanır.  Bazen isteğe bağlı Hdınsight kümesi sağlama hello aşağıdaki hata ile başarısız olur:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Bu hata genellikle hello linkedServiceName belirtilen hello depolama hesabı hello konumunu hello olmadığını gösterir aynı veri merkezi nerede Hdınsight hello sağlama gerçekleştiği konum. Örnek: varsa, veri fabrikası Batı ABD ve hello Azure depolama Doğu ABD, Batı ABD isteğe bağlı sağlama başarısız hello.

Buna ek olarak, isteğe bağlı HDInsight içinde ek depolama hesaplarının belirlenebileceği ikinci bir JSON özelliği (additionalLinkedServiceNames) bulunmaktadır. Bu ek bağlantılı depolama hesapları hello ile Merhaba hello Hdınsight kümesi veya aynı konumda başarısız olması gerektiğini aynı hata.

### <a name="problem-custom-net-activity-fails"></a>Sorun: Özel .NET etkinliği başarısız
Bkz: [özel etkinliği ile işlem hattı Debug](data-factory-use-custom-activities.md#troubleshoot-failures) ayrıntılı adımlar için.

## <a name="use-azure-portal-tootroubleshoot"></a>Azure portal tootroubleshoot kullanın
### <a name="using-portal-blades"></a>Portal dikey penceresi kullanılarak
Bkz: [işlem hattını izleme](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) adımlar için.

### <a name="using-monitor-and-manage-app"></a>İzleme ve Yönetme Uygulamasını kullanma
Bkz: [İzleyici ve data factory işlem hatlarını izleme ve yönetme uygulaması kullanarak yönetmek](data-factory-monitor-manage-app.md) Ayrıntılar için.

## <a name="use-azure-powershell-tootroubleshoot"></a>Azure PowerShell tootroubleshoot kullanın
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Azure PowerShell tootroubleshoot hata kullanın
Bkz: [İzleyicisi veri fabrikasında ardışık düzenleri Azure PowerShell kullanarak](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) Ayrıntılar için.

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
