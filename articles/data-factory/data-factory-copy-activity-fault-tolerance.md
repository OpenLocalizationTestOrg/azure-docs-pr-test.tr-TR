---
title: "Hataya dayanıklılık uyumsuz satır atlayarak Azure Data Factory kopyalama etkinliği ekleyin | Microsoft Docs"
description: "Kopyalama sırasında uyumsuz satır atlayarak hata toleransı Azure Data Factory kopyalama etkinliği eklemeyi öğrenin"
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
ms.openlocfilehash: e2a108752259d5da3b401666c6bdbaad13b7ea90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Hataya dayanıklılık uyumsuz satır atlayarak kopyalama etkinliği ekleyin.

Azure Data Factory [kopyalama etkinliği](data-factory-data-movement-activities.md) uyumsuz satırları kaynak ve havuz veri depoları arasında veri kopyalama işlemi sırasında işleme için iki yol sunar:

- İptal etmek ve kopyalama başarısız uyumsuz veriler olduğunda etkinliği karşılaştı (varsayılan davranıştır).
- Tüm verileri hata toleransı ekleme ve uyumsuz veri satırları atlanıyor kopyalama devam edebilirsiniz. Ayrıca, Azure Blob depolama alanına uyumsuz satırları oturum açabilir. Ardından, hatanın nedenini öğrenmek, veri kaynağındaki verileri düzeltin ve kopyalama etkinliği yeniden deneme için günlüğünü de inceleyebilirsiniz.

## <a name="supported-scenarios"></a>Desteklenen senaryolar
Kopyalama etkinliği algılama, atlanıyor ve uyumsuz verilerini günlüğe kaydetme için üç senaryoları destekler:

- **Kaynak veri türü ve havuz yerel türü arasında uyumsuzluk**

    Örneğin: veri kopyalama bir Blob depolamada CSV dosyasından üç içeren bir şema tanımı olan bir SQL veritabanına **INT** sütunları yazın. Sayısal veri gibi içeren CSV dosyası satırları `123,456,789` havuz deposuna başarıyla kopyalandı. Ancak, satırları içeren sayısal olmayan değerleri gibi `123,456,abc` uyumsuz algılanır ve atlanır.

- **Kaynak ve havuz arasında sütun sayısı uyuşmazlığı**

    Örneğin: veri kopyalama bir Blob depolamada CSV dosyasından altı sütunları içeren bir şema tanımı olan bir SQL veritabanına. Altı sütunları içeren CSV dosyası satırları başarıyla havuz deposuna kopyalanır. Daha fazla veya az altı sütunları içeren CSV dosyası satırları uyumsuz olarak algılanır ve atlanır.

- **İlişkisel bir veritabanına yazılırken birincil anahtar ihlali**

    Örneğin: veri kopyalama SQL Server'dan SQL veritabanına. Havuz SQL veritabanında tanımlı bir birincil anahtara, ancak böyle bir birincil anahtar kaynak SQL Server'da tanımlanmadı. Havuz için kaynak olarak mevcut yinelenen satırları kopyalanamaz. Kopyalama etkinliği yalnızca ilk satır kaynak verilerin havuz kopyalar. Yinelenen birincil anahtar değeri içeren sonraki kaynak satırları uyumsuz olarak algılanır ve atlanır.

## <a name="configuration"></a>Yapılandırma
Aşağıdaki örnek kopyalama etkinliği uyumsuz satırları atlanıyor yapılandırmak için JSON tanımını sağlar:

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
| **redirectIncompatibleRowSettings** | Zaman uyumsuz satırları günlüğe kaydetmek istediğiniz bir grup olabilir özellik belirtilmiş. | &nbsp; | Hayır |
| **linkedServiceName** | Atlanan satırları içeren günlüğü depolamak için Azure Storage bağlı hizmeti. | Adı bir [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) veya [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) bağlantılı günlük dosyasını depolamak için kullanmak istediğiniz depolama örneğine başvurur hizmeti. | Hayır |
| **yol** | Atlanan satır içeren bir günlük dosyası yolu. | Uyumsuz verileri günlüğe kaydetmek için kullanmak istediğiniz Blob Depolama yolunu belirtin. Bir yol belirtmezseniz, hizmet bir kapsayıcı oluşturur. | Hayır |

## <a name="monitoring"></a>İzleme
Çalıştırma kopyalama etkinliği tamamlandıktan sonra izleme bölümünde Atlanan satır sayısını görebilirsiniz:

![İzleyici uyumsuz satır atlandı](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Uyumsuz satırları oturum yapılandırırsanız, günlük dosyası bu yolunda bulabilirsiniz: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` günlük dosyasında, atlanan satır ve uyumsuzluk kök nedenini görebilirsiniz.

Özgün veriler ve karşılık gelen hata dosyasına kaydedilir. Günlük dosyası içeriğine bir örnek aşağıdaki gibidir:
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a>Sonraki adımlar
Azure Data Factory kopyalama etkinliği hakkında daha fazla bilgi için bkz: [Kopyala etkinliğini kullanarak veri taşıma](data-factory-data-movement-activities.md).