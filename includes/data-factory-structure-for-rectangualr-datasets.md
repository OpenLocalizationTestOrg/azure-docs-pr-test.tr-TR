## <a name="specifying-structure-definition-for-rectangular-datasets"></a>Yapı tanımı dikdörtgen veri kümeleri için belirtme
Merhaba hello veri kümeleri JSON yapısı bölümünde olan bir **isteğe bağlı** bölümünde dikdörtgen tablolarla (satırlar ve sütunlar) için ve Merhaba tablonun sütunlarını koleksiyonunu içerir. Merhaba yapısı bölüm iki tür bilgi sağlayan tür dönüştürmeleri için veya sütun eşlemelerini yapmak için kullanır. Aşağıdaki bölümlerde hello bu özellikleri ayrıntılı açıklamaktadır. 

Her sütun, aşağıdaki özelliklere hello içerir:

| Özellik | Açıklama | Gerekli |
| --- | --- | --- |
| ad |Merhaba sütunun adı. |Evet |
| type |Merhaba sütununun veri türü. Zaman tür bilgileri belirtmelisiniz için aşağıdaki türü dönüşümleri bölümüne daha ayrıntılı bakın |Hayır |
| Kültür |.NET türü belirtilir ve .NET türü Datetime veya Datetimeoffset olduğunda kullanılan kültür toobe temel. Varsayılan değer "en-us". |Hayır |
| Biçimi |Dize toobe türü belirtilir ve .NET türü Datetime veya Datetimeoffset olduğunda kullanılan biçim. |Hayır |

Merhaba aşağıdaki örnek üç sütun UserID, adı ve lastlogindate sahip bir tablo için hello yapısı bölümüne JSON gösterir.

```json
"structure": 
[
    { "name": "userid"},
    { "name": "name"},
    { "name": "lastlogindate"}
],
```

Lütfen zaman için yönergeleri izleyerek hello kullanın tooinclude "yapı" bilgileri ve hangi tooinclude hello içinde **yapısı** bölümü.

* **Yapılandırılmış veri kaynakları için** hello veriyle (kaynakları SQL Server, Oracle, Azure tablo vb. gibi), yalnızca belirli bir tanesini sütun eşlemesi istiyorsanız hello "yapı" bölümü belirtmelidir yanı sıra veri şeması ve tür bilgileri depolar Havuz ve adlarını toospecific sütunlar kaynak sütunları aynı (sütun eşleme bölümünde aşağıdaki ayrıntılarına bakın) hello değil. 
  
    Yukarıda belirtildiği gibi hello türü bilgileri "yapısı" bölümünde isteğe bağlıdır. Yapılandırılmış kaynakları için tür bilgileri zaten kullanılabilir veri kümesi tanımı hello veri deposundaki bir parçası olarak, bu nedenle dahil türü bilgileri hello "yapısı" bölümünde eklediğinizde.
* **Şema okuma veri kaynaklarında (özellikle Azure blob) için** herhangi bir şema veya türü bilgi hello verilerle depolamadan toostore veri seçebilirsiniz. Bu veri kaynağı türleri için 2 durumlarda aşağıdaki hello "yapısı" içermelidir:
  * Toodo sütun eşlemesi istiyor.
  * Merhaba veri kümesi kopyalama etkinliği kaynağında olduğunda, "yapısındaki" türü bilgileri sağlayabilir ve veri fabrikası hello havuz için dönüştürme toonative türleri için bu tür bilgileri kullanır. Bkz: [veri tooand Azure Blob'tan taşıma](../articles/data-factory/data-factory-azure-blob-connector.md) daha fazla bilgi için makalenin.

### <a name="supported-net-based-types"></a>Desteklenir. NET tabanlı türleri
Veri Fabrikası destekler hello CLS uyumlu .NET aşağıdaki gibi Azure blob okuma veri kaynaklarında şeması için "yapısındaki" türü bilgileri sağlamak için tür değerleri temel.

* Int16
* Int32 
* Int64
* Tek
* Çift
* Ondalık
* Byte]
* bool
* Dize 
* GUID
* Tarih saat
* Datetimeoffset
* Timespan 

DateTime ve Datetimeoffset için "kültür" & "format" dizesini toofacilitate özel Datetime dizisi ayrıştırma Ayrıca isteğe bağlı olarak belirtebilirsiniz. Tür dönüşümü aşağıdaki örneğe bakın.

