## <a name="repeatability-during-copy"></a>Kopyalama sırasında Yinelenebilirlik
Ne zaman veri tooAzure SQL/SQL Server diğer veriler kopyalama depolayan bir gereksinimlerini tookeep Yinelenebilirlik göz tooavoid istenmeyen sonuçları. 

Veri tooAzure SQL/SQL Server veritabanı kopyalama, kopyalama etkinliği varsayılan APPEND hello veri kümesi toohello havuz tablosu tarafından varsayılan olarak kullanacak. Örneğin, iki içeren CSV (virgülle ayrılmış değerler veri) dosya kaynağından veri kopyalama tooAzure SQL/SQL Server veritabanına kaydeder sonra bu gibi görünüyor hangi hello tablo olur:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Hataları kaynak dosyasını ve aşağı boru güncelleştirilmiş hello miktarından 2 too4 itibaren hello kaynak dosyasında bulunan varsayalım. Belirli bir döneme ait yeniden hello veri dilimi çalıştırırsanız, iki yeni kayıt tooAzure SQL/SQL Server veritabanına eklenen bulabilirsiniz. Merhaba aşağıdaki hello tablodaki hello sütun hiçbiri hello birincil anahtar kısıtlaması olduğunu varsayar.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid Bu, aşağıda belirtildiği 2 mekanizmaları aşağıda hello yararlanarak toospecify UPSERT semantiği gerekir.

> [!NOTE]
> Bir dilim otomatik olarak Azure Data Factory içinde belirtilen hello yeniden deneme ilkesi uyarınca yeniden çalıştırılabilir.
> 
> 

### <a name="mechanism-1"></a>Mekanizması 1
Yararlanabileceğiniz **sqlWriterCleanupScript** özelliği toofirst bir dilim çalıştırdığınızda temizleme eylemi gerçekleştirir. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Merhaba temizleme betiğini yürütülmesi, hello veri hello SQL tablosuna karşılık gelen toothat dilimden silebilirsiniz belirli bir dilim için kopyalama sırasında ilk. Merhaba etkinlik sonradan hello veri hello SQL tablosuna ekler. 

Merhaba miktar olarak güncelleştirilir yeniden çalıştırın. ardından, bulur artık hello dilim varsa desired.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Merhaba düz rondela kayıt hello özgün csv kaldırılır varsayalım. Daha sonra yeniden çalıştırarak hello dilim sonuç aşağıdaki hello oluşturur: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Yeni bir şey bitti toobe vardı. Merhaba kopyalama etkinliği hello temizleme betik toodelete hello ilgili verilerini bu dilim verdi. (Bu, daha sonra yer alan yalnızca 1 kaydı) hello csv hello giriş okuyun sonra ve tablo hello eklenir. 

### <a name="mechanism-2"></a>Mekanizması 2
> [!IMPORTANT]
> Sliceıdentifiercolumnname Azure SQL Data Warehouse için şu anda desteklenmiyor. 

Başka bir mekanizma tooachieve Yinelenebilirlik adanmış bir sütun sağlayarak olduğu (**Sliceıdentifiercolumnname**) tablo hello hedefleyin. Bu sütun eşitlenmiş Azure Data Factory tooensure hello kaynak ve hedef Kal tarafından kullanılır. Bu yaklaşım, değiştirme veya hello hedef SQL tablo şemasını tanımlama esneklik olduğunda çalışır. 

Bu sütun Azure Data Factory'nin Yinelenebilirlik amaçlar için kullanılır ve hello işlemde herhangi bir şema Azure Data Factory yapmaz toohello tablo değiştirir. Yol toouse bu yaklaşım:

1. Türünde bir sütun ikili (32) hello hedef SQL tablosu tanımlayın. Bu sütunda hiç bir kısıtlama olması gerekir. Şimdi bu sütun bu örnekte 'ColumnForADFuseOnly' adlandırın.
2. Merhaba kopyalama etkinliği şu şekilde kullanın:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Azure Data Factory bu sütun, gerek göredir doldurmak tooensure hello kaynak ve hedef eşitlenmiş kalır. Bu sütundaki değerleri Hello dışında bu bağlamda hello kullanıcı tarafından kullanılmamalıdır. 

Benzer toomechanism 1, kopyalama etkinliği otomatik olarak ilk dilim hello hedef SQL tablosu verilen ve hello kopyalama etkinliği normalde çalıştırılan hello hello verilerini temizleme, dilim için kaynak toodestination tooinsert hello verileri. 

