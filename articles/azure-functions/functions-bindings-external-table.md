---
title: "aaaAzure işlevleri dış tablo bağlama (Önizleme) | Microsoft Docs"
description: "Dış tablo bağlamaları Azure işlevlerini kullanma"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Azure işlevleri dış tablo bağlama (Önizleme)
Bu makalede gösterilmektedir nasıl toomanipulate tablo veri işlevinizi yerleşik bağlamalarla içinde SaaS sağlayıcıları (örneğin, Sharepoint, Dynamics). Azure işlevleri, harici tablolar için girdi ve çıktı bağlamaları destekler.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>API bağlantıları

Tablo bağlamaları ile 3. taraf SaaS sağlayıcılar dış API bağlantıları tooauthenticate yararlanın. 

Bir bağlama atarken, yeni bir API bağlantı oluşturabilir veya var olan bir API bağlantısını hello içinde kullanmak aynı kaynak grubu

### <a name="supported-api-connections-tables"></a>Desteklenen API bağlantıları (tablo) s

|Bağlayıcı|Tetikleyici|Girdi|Çıktı|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 işlemleri için](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google E-Tablolar](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Mali Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle Veritabanı](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Ortak veri hizmeti](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> Dış tablo bağlantıları da kullanılabilir [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

### <a name="creating-an-api-connection-step-by-step"></a>Bir API bağlantı oluşturma: adım adım

1. Bir işlev oluşturun > Özel işlevi ![özel bir işlev oluşturun](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Senaryo `Experimental`  >  `ExternalTable-CSharp` şablonu > Yeni bir `External Table connection` 
 ![Seç tablo giriş şablonu](./media/functions-bindings-storage-table/create-template-table.jpg)
1. SaaS sağlayıcınızı seçin > bir bağlantı seçin/oluşturmak ![yapılandırma SaaS bağlantı](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. API bağlantınızı seçin > merhaba fonksiyon ![Create table işlevi](./media/functions-bindings-storage-table/table-template-options.jpg)
1. seçin`Integrate` > `External Table`
    1. Merhaba bağlantı toouse hedef tablo yapılandırın. Bu ayarlar, SaaS sağlayıcılar arasında çok olur. Aşağıda anahat oldukları [veri kaynağı ayarları](#datasourcesettings)
![yapılandırma tablosu](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Kullanım

Bu örnek kimliği, Soyadı ve FirstName sütunlarla "Başvurun" adlı tooa tablo bağlanır. hello kişi varlıkları hello tablosundaki Hello kodunu listeler ve günlükleri adları ve soyadları hello.

### <a name="bindings"></a>Bağlamalar
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId`Tablo bağlamaları için boş olması gerekir.

`ConnectionAppSettingsKey`Merhaba API bağlantı dizesi depolar hello uygulama ayarı tanımlar. bir API eklediğinizde hello uygulama ayarı otomatik olarak oluşturulan hello bağlantısında UI tümleştirin.

Veri kümeleri tablo Bağlayıcısı sağlar ve her bir veri kümesi tabloları içerir. "varsayılan" Merhaba hello varsayılan veri kümesinin adıdır Merhaba başlıkları bir veri kümesi ve bir tablo çeşitli SaaS sağlayıcıları için aşağıda listelenmiştir:

|Bağlayıcı|Veri kümesi|Tablo|
|:-----|:---|:---| 
|**SharePoint**|Site|SharePoint listesi
|**SQL**|Database|Tablo 
|**Google sayfası**|Elektronik Tablo|Çalışma sayfası 
|**Excel**|Excel dosyası|Sayfası 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>C# kullanımı #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
##Veri kaynağı ayarları

### <a name="sql-server"></a>SQL Server

komut dosyası toocreate hello ve doldurmak hello kişi tablosu aşağıdadır. dataSetName "." varsayılandır

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Google E-Tablolar
Google belgeleri elektronik tablo adında bir çalışma sayfasıyla oluşturmak `Contact`. Merhaba bağlayıcı hello elektronik tablo görünen adı kullanamazsınız. Hello iç adını (kalın) dataSetName örneğin kullanılan toobe gerekiyor: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  hello sütun adları eklemek `Id`, `LastName`, `FirstName` toohello ilk satır, ardından üzerinde veri doldurma sonraki satır.

### <a name="salesforce"></a>Salesforce
dataSetName "." varsayılandır

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
