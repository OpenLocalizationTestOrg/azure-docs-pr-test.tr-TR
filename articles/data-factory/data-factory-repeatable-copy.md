---
title: "Azure Data Factory aaaRepeatable kopyasında | Microsoft Docs"
description: "Verileri kopyalayan bir dilim birden çok kez çalıştırma olsa bile nasıl tooavoid yineleyen öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Azure Data Factory yinelenebilir kopyalama

## <a name="repeatable-read-from-relational-sources"></a>İlişkisel kaynaklardan yinelenebilir okuma
İlişkisel veri depoları veri kopyalama işlemi sırasında Yinelenebilirlik göz tooavoid tutmak istenmeyen sonuçları. Azure Data Factory'de bir dilim el ile çalıştırabilirsiniz. Bir hata oluştuğunda bir dilimi yeniden çalıştırmak için bir veri kümesi için yeniden deneme ilkesi de yapılandırabilirsiniz. Bir dilim iki yolla yeniden zaman, aynı veri hello emin toomake nasıl geçtiğinden bağımsız okuma gerekir dilim birçok kez çalıştırın.  
 
> [!NOTE]
> Merhaba aşağıdaki örnekleri için Azure SQL ancak dikdörtgen veri kümeleri destekleyen geçerli tooany veri deposu. Tooadjust hello olabilir **türü** kaynak ve hello **sorgu** özelliği (örneğin: Sorgu sqlReaderQuery yerine) hello verilerini depolamak.   

Genellikle, ilişkisel depoları okunurken toothat dilim karşılık gelen tooread hello veriler yalnızca istiyor. Bir şekilde toodo şekilde Azure Data Factory'de hello WindowStart ve WindowEnd sistem değişkenleri kullanılabilir kullanarak olacaktır. Merhaba değişkenleri ve hello burada Azure Data factory'de işlevleri hakkında bilgi [Azure Data Factory - işlevler ve sistem değişkenleri](data-factory-functions-variables.md) makalesi. Örnek: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Bu sorgu MyTable hello tablosundan hello dilim süresi aralığını (WindowStart -> WindowEnd) içinde kalan verileri okur. Bu dilimin yeniden çalıştırın ayrıca her zaman aynı veri okuma, hello emin. 

Diğer durumlarda, tooread hello tüm tablo isteyebilir ve hello sqlReaderQuery gibi tanımlayın:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>Yinelenebilir yazma tooSqlSink
Veriler çok kopyalarken**Azure SQL/SQL Server** tookeep Yinelenebilirlik göz tooavoid içinde gereken diğer veri depolarına, istenmeyen sonuçları. 

Veri tooAzure SQL/SQL Server veritabanı kopyalama işlemi sırasında hello kopyalama etkinliği varsayılan olarak veri toohello havuz tablosuna ekler. Deyin, aşağıdaki tablonun bir Azure SQL/SQL Server veritabanında bir CSV (virgülle ayrılmış değerler) dosyasını içeren iki kayıt toohello gelen veri kopyalarsınız. Bir dilim çalıştığında hello iki kopyalanan toohello SQL tablosu kayıtlarıdır. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Kaynak dosyasında hata buldu ve aşağı boru hello miktarından 2 too4 itibaren güncelleştirilmiş varsayalım. Merhaba veri dilimi belirli bir döneme ait el ile yeniden, iki yeni kayıt tooAzure SQL/SQL Server veritabanına eklenen bulabilirsiniz. Bu örnek hello tablodaki hello sütun hiçbiri hello birincil anahtar kısıtlaması olduğunu varsayar.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid Bu davranış, toospecify UPSERT semantiği iki mekanizma aşağıdaki hello birini kullanarak gerekir:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Mekanizması 1: sqlWriterCleanupScript kullanma
Merhaba kullanabilirsiniz **sqlWriterCleanupScript** özelliği tooclean bir dilim çalıştırdığınızda hello veri eklemeden önce hello havuz tablodan veri ayarlama. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Bir dilim çalıştığında hello temizleme betiğini toohello dilim hello SQL tablosundan karşılık gelen ilk toodelete veri çalıştırılır. Merhaba kopyalama etkinliği, ardından SQL tablosu hello veri ekler. Merhaba dilimi yeniden çalıştırın, hello miktar güncelleştirilir istenen şekilde.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Merhaba düz rondela kayıt hello özgün csv kaldırılır varsayalım. Yeniden çalıştırma hello dilim sonuç aşağıdaki hello sonra oluşturur: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

Merhaba kopyalama etkinliği hello temizleme betik toodelete hello ilgili verilerini bu dilim verdi. (Bu, daha sonra yer alan yalnızca bir kayıt) hello csv hello giriş okuyun sonra ve tablo hello eklenir. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Mekanizması 2: Sliceıdentifiercolumnname kullanma
> [!IMPORTANT]
> Şu anda Sliceıdentifiercolumnname Azure SQL veri ambarı için desteklenmiyor. 

Merhaba ikinci mekanizması tooachieve Yinelenebilirlik hello hedef tablo ayrılmış sütun (Sliceıdentifiercolumnname) sağlayarak ' dir. Bu sütun eşitlenmiş Azure Data Factory tooensure hello kaynak ve hedef Kal tarafından kullanılır. Bu yaklaşım, değiştirme veya hello hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır. 

Bu sütun Yinelenebilirlik amaçlar için Azure Data Factory tarafından kullanılır ve hello işlemde herhangi bir şema Azure Data Factory yapmaz toohello tablo değiştirir. Yol toouse bu yaklaşım:

1. Türünde bir sütun tanımlamak **ikili (32)** hello hedef SQL tablosu. Bu sütunda hiç bir kısıtlama olması gerekir. Şimdi bu sütun, bu örnek için AdfSliceIdentifier adlandırın.


    Kaynak tablosu:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Hedef Tablo: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Merhaba kopyalama etkinliği şu şekilde kullanın:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory doldurur bu sütun, gerek göredir tooensure hello kaynak ve hedef eşitlenmiş kalır. Bu sütundaki değerleri Hello dışında bu bağlamda kullanılmamalıdır. 

Benzer toomechanism 1, kopyalama etkinliği hello veri dilimi hello hedef SQL tablosu verilen hello için otomatik olarak temizler. Ardından toohello hedef tablodaki kaynaktan veri ekler. 

## <a name="next-steps"></a>Sonraki adımlar
Merhaba, JSON örnekleri tamamlamak için bağlayıcı makaleler gözden geçirin: 

- [Azure SQL Veritabanı](data-factory-azure-sql-connector.md)
- [Azure SQL Veri Ambarı](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)