---
title: "Azure Data Factory kopyalama etkinliğinde aaaAdd hata toleransı uyumsuz satır atlanıyor tarafından | Microsoft Docs"
description: "Nasıl tooadd hataya dayanıklılık Azure Data Factory kopyalama etkinliğinde kopyalama sırasında uyumsuz satır atlayarak öğrenin"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Hataya dayanıklılık uyumsuz satır atlayarak kopyalama etkinliği ekleyin.

Azure Data Factory [kopyalama etkinliği](data-factory-data-movement-activities.md) kaynak ve havuz veri depoları arasında veri kopyalama işlemi sırasında iki yolla toohandle uyumsuz satırları sunar:

- İptal etmek ve hello kopya başarısız uyumsuz veriler olduğunda etkinliği karşılaştı (varsayılan davranıştır).
- Toocopy devam edebilmeniz için tüm hata toleransı ekleyerek ve uyumsuz veri satırları atlanıyor hello verileri. Ayrıca, Azure Blob depolama alanına hello uyumsuz satırları oturum açabilir. Merhaba günlük toolearn hello hello başarısızlık nedeni inceleyin hello veri hello veri kaynağında düzeltin ve hello kopyalama etkinliği yeniden deneyin.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Kopyalama etkinliği algılama, atlanıyor ve uyumsuz verilerini günlüğe kaydetme için üç senaryoları destekler:

- **Merhaba kaynak veri türü ve hello havuz yerel türü arasında uyumsuzluk**

    Örneğin: Blob Depolama tooa SQL bir CSV dosyasından veri Kopyala veritabanı üç içeren bir şema tanımı **INT** sütunları yazın. sayısal veri gibi içeren CSV dosyası sıra hello `123,456,789` başarıyla kopyalandı toohello havuz deposu. Ancak, gibi sayısal olmayan değerler içeren satırları hello `123,456,abc` uyumsuz algılanır ve atlanır.

- **Merhaba sütun sayısı olarak hello kaynak ve hello havuz arasında uyuşmazlık**

    Örneğin: Blob Depolama tooa SQL bir CSV dosyasından veri Kopyala veritabanı altı sütunları içeren bir şema tanımı. Merhaba altı sütunlar içeren satırlar CSV dosyası başarıyla toohello havuz saklayın. Daha fazla veya az altı sütunları içeren hello CSV dosyası satırları uyumsuz olarak algılanır ve atlanır.

- **Tooa ilişkisel veritabanı yazılırken birincil anahtar ihlali**

    Örneğin: bir SQL server tooa SQL veritabanından veri kopyalayın. Merhaba havuz SQL veritabanında tanımlı bir birincil anahtara, ancak böyle bir birincil anahtar hello kaynak SQL Server'da tanımlanmadı. Merhaba kaynağında mevcut hello yinelenen satırları kopyalanan toohello havuz olamaz. Kopyalama etkinliği yalnızca hello verilerin ilk satırında hello kaynak hello havuz kopyalar. Merhaba hello yinelenen birincil anahtar değeri içeren sonraki kaynak satırları uyumsuz olarak algılanır ve atlanır.

## <a name="configuration"></a>Yapılandırma
Merhaba aşağıdaki örnek hello uyumsuz satırları kopyalama etkinliğinde atlanıyor JSON tanımı tooconfigure sağlar:

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Özellik | Açıklama | İzin verilen değerler | Gerekli |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Atlanıyor uyumsuz satırları kopyalama sırasında veya etkinleştirin. | True<br/>False (varsayılan) | Hayır |
| **redirectIncompatibleRowSettings** | Bir grup olabilir özellik toolog hello uyumsuz satırları istediğinizde belirtilmiş. | &nbsp; | Hayır |
| **linkedServiceName** | Merhaba bağlı hizmeti Azure Storage toostore hello günlüğünün atlandı hello satırları içeren. | Merhaba adını bir [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) bağlantılı toouse toostore hello günlük dosyası istediğiniz toohello depolama örneğini başvuruyor hizmeti. | Hayır |
| **yol** | Merhaba içeren hello günlük dosyası yolu Hello satır atlandı. | Toouse toolog hello uyumsuz veri istediğiniz hello Blob Depolama Birimi yolu belirtin. Bir yol belirtmezseniz, hello hizmeti sizin için bir kapsayıcı oluşturur. | Hayır |

## <a name="monitoring"></a>İzleme
Çalıştırma hello kopyalama etkinliği tamamlandıktan sonra bölüm izleme hello Atlanan satır sayısı hello görebilirsiniz:

![İzleyici uyumsuz satır atlandı](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Toolog hello uyumsuz satırları yapılandırırsanız, bu yolda hello günlük dosyasını bulabilirsiniz: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` hello günlük dosyasında, atlanan hello satırları görebilir ve hello hello uyumsuzluk kök nedenini.

Merhaba özgün veriler ve hello karşılık gelen hata hello dosyasına kaydedilir. Merhaba günlük dosyası içeriğine bir örnek aşağıdaki gibidir:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Sonraki adımlar
Azure Data Factory kopyalama etkinliği hakkında daha fazla toolearn bkz [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).
