### <a name="azure-storage-linked-service"></a>Azure Storage Bağlı Hizmeti
Merhaba **Azure depolama bağlantılı hizmeti** hello kullanılarak toolink bir Azure depolama hesabı tooan Azure data factory verir **hesap anahtarı**, genel erişim toohello Azure hello veri fabrikası sağlar Depolama alanı. Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure depolama bağlı hizmeti için bir açıklama sağlar.

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureStorage** |Evet |
| connectionString |Tooconnect tooAzure depolama hello connectionString özelliği için gerekli bilgiler belirtin. |Evet |

Hello aşağıdaki makaleye bakın adımları tooview/kopyalama hello hesap anahtarı için bir Azure depolama için bkz: [görüntüleme, kopyalama ve erişim anahtarları yeniden oluşturma depolama](../articles/storage/common/storage-create-storage-account.md#manage-your-storage-account).

**Örnek:**  

```json
{  
    "name": "StorageLinkedService",  
    "properties": {  
        "type": "AzureStorage",  
        "typeProperties": {  
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"  
        }  
    }  
}  
```

### <a name="azure-storage-sas-linked-service"></a>Azure depolama Sas bağlantılı hizmetinin
Paylaşılan erişim imzası (SAS) depolama hesabınızda atanmış erişim tooresources sağlar. Bir istemci toogrant depolama hesabınızdaki izinleri tooobjects süre ve belirtilen bir izin kümesi ile belirli bir süre için hesap erişim tuşlarınızı tooshare gerek kalmadan sınırlı sağlar. Merhaba SAS kimlik doğrulamalı erişim tooa depolama kaynağı için gerekli olan tüm hello bilgileri kendi sorgu parametrelerini kapsayan bir URI değil. tooaccess depolama kaynaklarını hello SAS ile Merhaba istemci hello SAS toohello uygun Oluşturucusu veya yöntemi toopass yeterlidir. SAS hakkında ayrıntılı bilgi için bkz: [paylaşılan erişim imzaları: SAS modelini anlama hello](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md)

> [!IMPORTANT]
> Azure Data Factory artık yalnızca destekler **hizmet SAS** ancak hesap SAS. Bkz: [türleri, paylaşılan erişim imzaları](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md#types-of-shared-access-signatures) bu iki türleri hakkında ayrıntılar için ve nasıl tooconstruct. SAS URL Azure portalından generable hello veya desteklenmeyen bir hesap SAS, Depolama Gezgini olduğunu unutmayın.
> 

Hello Azure depolama bağlı SAS hizmeti bir paylaşılan erişim imzası (SAS) kullanarak toolink bir Azure depolama hesabı tooan Azure data factory sağlar. Kısıtlanmış/zaman sınırlı erişimi hello veri fabrikası hello depolama tooall/özel kaynakları (blob/kapsayıcısı) sağlar. Aşağıdaki tablonun hello JSON öğeleri belirli tooAzure depolama SAS bağlantılı hizmeti için bir açıklama sağlar. 

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type |Merhaba type özelliği ayarlanmalıdır: **AzureStorageSas** |Evet |
| sasUri |Blob, kapsayıcı ya da tablo gibi paylaşılan erişim imzası URI toohello Azure Storage kaynakları belirtin.  |Evet |

**Örnek:**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<Specify SAS URI of hello Azure Storage resource>"   
        }  
    }  
}  
```

Oluştururken bir **SAS URI'sini**, hello aşağıdakileri göz önünde bulunduruyor:  

* Ayarlama uygun okuma/yazma **izinleri** göre nesneler üzerinde nasıl hello hizmeti (okuma, yazma, okuma/yazma) bağlı veri Fabrikanızda kullanılır.
* Ayarlama **sona erme saati** uygun şekilde. Merhaba erişim tooAzure depolama nesneleri değil dolacağını hello etkin hello ardışık düzen döneminde emin olun.
* URI hello sağ kapsayıcı/blob oluşturulmalıdır veya hello üzerinde temel tablo düzeyi gerekir. SAS URI'sini tooan Azure blob hello Data Factory hizmeti tooaccess bu belirli blob sağlar. Bir SAS URI'sini tooan Azure blob kapsayıcısı hello Data Factory hizmeti tooiterate bu kapsayıcıdaki blobları aracılığıyla sağlar. Tooprovide daha erişmeniz/SAS URI, daha az nesneleri daha sonra ya da güncelleştirme hello tooupdate hello bağlı hizmetiyle unutmayın, yeni bir URI hello.   

