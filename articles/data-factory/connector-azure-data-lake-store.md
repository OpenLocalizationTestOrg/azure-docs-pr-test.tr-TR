---
title: Veri kopyalama/Data Factory kullanarak Azure Data Lake Store | Microsoft Docs
description: "Azure Data Lake Store için desteklenen kaynak veri depoları (veya) Data Lake Store'a veri kopyalamak için Data Factory kullanarak desteklenen havuz depolarını öğrenin."
services: data-factory
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 12/07/2017
ms.author: jingwang
ms.openlocfilehash: c388fe0cfe85ec2bf2b752f74d39eb2ebe38ceb1
ms.sourcegitcommit: 7edfa9fbed0f9e274209cec6456bf4a689a4c1a6
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/17/2018
---
# <a name="copy-data-to-or-from-azure-data-lake-store-by-using-azure-data-factory"></a>Azure Data Factory kullanarak Azure Data Lake Store bilgisayardan veya veri kopyalama
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Sürüm 1 - Genel Kullanım](v1/data-factory-azure-datalake-connector.md)
> * [Sürüm 2 - Önizleme](connector-azure-data-lake-store.md)

Bu makalede Azure Data Lake Store gelen ve verileri kopyalamak için kopyalama etkinliği Azure Data Factory'de kullanma özetlenmektedir. Derlemeler [etkinlik genel bakış kopyalama](copy-activity-overview.md) makale kopyalama etkinliği genel bir bakış sunar.

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Genel olarak kullanılabilir (GA) Data Factory Hizmeti'ne 1 sürümünü kullanıyorsanız bkz [V1 Azure Data Lake Store Bağlayıcısı](v1/data-factory-azure-datalake-connector.md).

## <a name="supported-capabilities"></a>Desteklenen özellikler

Azure Data Lake Store için tüm desteklenen kaynak veri deposundan veri kopyalama veya verileri Azure Data Lake Store tüm desteklenen havuz veri deposuna kopyalamak. Kaynakları veya havuzlarını kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](copy-activity-overview.md#supported-data-stores-and-formats) tablo.

Özellikle, bu Azure Data Lake Store bağlayıcı destekler:

- Dosya kopyalarken kullanarak **hizmet sorumlusu** veya **yönetilen hizmet kimliği (MSI)** kimlik doğrulaması.
- Dosyaları olarak kopyalama- ya da ayrıştırma/oluşturma dosyalarıyla [desteklenen dosya biçimleri ve sıkıştırma codec](supported-file-formats-and-compression-codecs.md).

## <a name="get-started"></a>başlarken

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Aşağıdaki bölümler, Azure Data lake Store'a Data Factory varlıklarını belirli tanımlamak için kullanılan özellikleri hakkında ayrıntılı bilgi sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri

Azure Data Lake Store bağlantılı hizmetinin aşağıdaki özellikleri desteklenir:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Type özelliği ayarlamak **AzureDataLakeStore**. | Evet |
| dataLakeStoreUri | Azure Data Lake Store hesabı hakkında bilgi. Bu bilgiler aşağıdaki biçimlerden birini alır: `https://[accountname].azuredatalakestore.net/webhdfs/v1` veya `adl://[accountname].azuredatalakestore.net/`. | Evet |
| kiracı | Uygulamanızın bulunduğu altında Kiracı bilgileri (etki alanı adı veya Kiracı kimliği) belirtin. Azure portalının sağ üst köşedeki fare gelerek alabilir. | Evet |
| subscriptionId | Data Lake Store hesabına ait olduğu azure abonelik kimliği. | Havuz için gerekli |
| resourceGroupName | Data Lake Store hesabına ait olduğu azure kaynak grubu adı. | Havuz için gerekli |
| connectVia | [Tümleştirmesi çalışma zamanı](concepts-integration-runtime.md) veri deposuna bağlanmak için kullanılacak. (Veri deposu özel bir ağda yer alıyorsa) Azure tümleştirmesi çalışma zamanı veya Self-hosted tümleştirmesi çalışma zamanı kullanabilirsiniz. Belirtilmezse, varsayılan Azure tümleştirmesi çalışma zamanı kullanır. |Hayır |

Aşağıdaki bölümlerde daha fazla özellikleri ve farklı kimlik doğrulama türü için JSON örnek sırasıyla bakın:

- [Hizmet asıl kimlik doğrulaması kullanma](#using-service-principal-authentication)
- [Yönetilen hizmet kimlik doğrulama kullanılarak](#using-managed-service-identity-authentication)

### <a name="using-service-principal-authentication"></a>Hizmet asıl kimlik doğrulaması kullanma

Hizmet asıl kimlik doğrulaması kullanmak için Azure Active Directory (Azure AD) bir uygulama varlığı kaydetmek ve Data Lake Store'a erişim izni. Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Bağlantılı hizmet tanımlamak için kullandığınız aşağıdaki değerleri not edin:

- Uygulama Kimliği
- Uygulama anahtarı
- Kiracı Kimliği

>[!IMPORTANT]
> Hizmet asıl uygun Azure Data Lake Store'da izni olduğundan emin olun:
>- **Kaynak olarak**, en az izni **okuma + yürütme** veri erişim izni listesi ve bir klasörün içeriğini kopyalayın veya **okuma** tek bir dosya kopyalama izni. Hesap düzeyinde erişim denetimi (IAM) gereksinimi yoktur.
>- **Havuz olarak**, en az izni **yazma + yürütme** veri erişim alt öğeleri klasöründe oluşturma izni. Kopyalamak için Azure IR kullanıyorsanız (kaynak ve havuz olan buluta), veri fabrikası Data Lake Store'nın bölge algılamak izin için en az izni **okuyucu** hesap erişim denetimi (IAM) rolü. Bu IAM rol açıkça önlemek istiyorsanız [Azure IR oluşturmak](create-azure-integration-runtime.md#create-azure-ir) Data Lake Store ve Data Lake Store'da ilişkilendirme konumu ile bağlantılı hizmeti aşağıdaki örnekteki gibi:

Aşağıdaki özellikler desteklenir:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| servicePrincipalId | Uygulamanın istemci kimliği belirtin. | Evet |
| servicePrincipalKey | Uygulamanın anahtarını belirtin. Bu alan bir SecureString işaretleyin. | Evet |

**Örnek:**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": {
                "type": "SecureString",
                "value": "<service principal key>"
            },
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

### <a name="using-managed-service-identity-authentication"></a>Yönetilen hizmet kimlik doğrulama kullanılarak

Data factory ile ilişkilendirilebilir bir [yönetilen hizmet kimliği](data-factory-service-identity.md), bu belirli veri fabrikası temsil eder. Bu hizmet kimliği doğrudan kendi hizmet sorumlusu kullanmaya benzer Data Lake Store kimlik doğrulaması için de kullanabilirsiniz. Bu belirlenen Fabrika verilerine erişim ve kopyalama / Data Lake Store izin verir.

Yönetilen hizmet (MSI) kimlik doğrulama kullanmak için:

1. [Veri Fabrikası hizmet kimliği alma](data-factory-service-identity.md#retrieve-service-identity) "Hizmeti kimliği uygulama Fabrikanızda birlikte oluşturulan kimliği" değerini kopyalayarak.
2. Data Lake Store'a hizmet sorumlusu için yaptığınız gibi hizmet kimliği erişim verin. Ayrıntılı adımlar için bkz: [hizmeti için kimlik doğrulama - Azure Data Lake Store hesabına dosya veya klasöre Ata Azure AD uygulama](../data-lake-store/data-lake-store-service-to-service-authenticate-using-active-directory.md#step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder).

>[!IMPORTANT]
> Veri Fabrikası hizmet kimlik uygun Azure Data Lake Store'da izni olduğundan emin olun:
>- **Kaynak olarak**, en az izni **okuma + yürütme** veri erişim izni listesi ve bir klasörün içeriğini kopyalayın veya **okuma** tek bir dosya kopyalama izni. Hesap düzeyinde erişim denetimi (IAM) gereksinimi yoktur.
>- **Havuz olarak**, en az izni **yazma + yürütme** veri erişim alt öğeleri klasöründe oluşturma izni. Kopyalamak için Azure IR kullanıyorsanız (kaynak ve havuz olan buluta), veri fabrikası Data Lake Store'nın bölge algılamak izin için en az izni **okuyucu** hesap erişim denetimi (IAM) rolü. Bu IAM rol açıkça önlemek istiyorsanız [Azure IR oluşturmak](create-azure-integration-runtime.md#create-azure-ir) Data Lake Store ve Data Lake Store'da ilişkilendirme konumu ile bağlantılı hizmeti aşağıdaki örnekteki gibi:

Azure Data Factory bağlantılı hizmetteki genel Data Lake Store bilgilerin yanı sıra tüm özelliklerini belirtmeniz gerekmez.

**Örnek:**

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri

Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için veri kümeleri makalesine bakın. Bu bölümde Azure Data Lake Store veri kümesi tarafından desteklenen özellikler listesini sağlar.

/ Azure Data Lake Store'a veri kopyalamak için veri kümesi için tür özelliği ayarlamak **AzureDataLakeStoreFile**. Aşağıdaki özellikler desteklenir:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Veri kümesi türü özelliği ayarlamak: **AzureDataLakeStoreFile** |Evet |
| folderPath | Dosya depolama klasöründe ve kapsayıcı yolu. Örnek: rootfolder/alt / |Evet |
| fileName | Dosya adını belirtin **folderPath**  /belirli bir dosya kopyalamak istiyorsanız. Bu özellik için herhangi bir değer belirtmezseniz, veri kümesi klasördeki tüm dosyaları işaret eder.<br/><br/>Dosya adı değil belirtildiğinde bir çıkış veri kümesi için ve **preserveHierarchy** belirtilmedi etkinlik havuzunda kopyalama etkinliği, bir dosya adı şu biçimi ile otomatik olarak oluşturur: `Data.[activity run id GUID].[GUID if FlattenHierarchy].[format if configured].[compression if configured]`. Örneğin: `Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.gz`. |Hayır |
| Biçimi | İsterseniz **olarak dosyaları kopyalama-olduğu** dosya tabanlı depoları arasında (ikili kopya), her iki girdi ve çıktı veri kümesi tanımlarında Biçim bölümü atlayın.<br/><br/>Ayrıştırma veya belirli bir biçime sahip dosyaları oluşturmak istiyorsanız, aşağıdaki dosya biçimi türleri desteklenir: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Ayarlama **türü** şu değerlerden biri biçimine altında özellik. Daha fazla bilgi için bkz: [metin biçimi](supported-file-formats-and-compression-codecs.md#text-format), [Json biçimine](supported-file-formats-and-compression-codecs.md#json-format), [Avro biçimi](supported-file-formats-and-compression-codecs.md#avro-format), [Orc biçimi](supported-file-formats-and-compression-codecs.md#orc-format), ve [Parquet biçimi](supported-file-formats-and-compression-codecs.md#parquet-format) bölümler. |Hayır (yalnızca ikili kopyalama senaryosu) |
| Sıkıştırma | Veri sıkıştırma düzeyini ve türünü belirtin. Daha fazla bilgi için bkz: [desteklenen dosya biçimleri ve sıkıştırma codec](supported-file-formats-and-compression-codecs.md#compression-support).<br/>Desteklenen türler: **GZip**, **Deflate**, **Bzıp2**, ve **ZipDeflate**.<br/>Desteklenen düzeyler: **Optimal** ve **en hızlı**. |Hayır |

**Örnek:**

```json
{
    "name": "ADLSDataset",
    "properties": {
        "type": "AzureDataLakeStoreFile",
        "linkedServiceName":{
            "referenceName": "<ADLS linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "folderPath": "datalake/myfolder/",
            "fileName": "myfile.csv.gz",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            },
            "compression": {
                "type": "GZip",
                "level": "Optimal"
            }
        }
    }
}
```

## <a name="copy-activity-properties"></a>Etkinlik özellikleri Kopyala

Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen](concepts-pipelines-activities.md) makalesi. Bu bölümde Azure Data Lake kaynak ve havuz tarafından desteklenen özellikler listesini sağlar.

### <a name="azure-data-lake-store-as-source"></a>Azure Data Lake Store kaynağı olarak

Azure Data Lake Store verileri kopyalamak için kopyalama etkinliği için kaynak türünü ayarlayın. **AzureDataLakeStoreSource**. Aşağıdaki özellikler kopyalama etkinliği desteklenen **kaynak** bölümü:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Kopyalama etkinliği kaynağı tür özelliği ayarlamak: **AzureDataLakeStoreSource** |Evet |
| Özyinelemeli | Belirtilen klasörün alt klasörleri ya da yalnızca verileri özyinelemeli olarak okunur olup olmadığını gösterir. Özyinelemeli true ve havuz için ayarlandığında Not dosya tabanlı depolama, boş klasör/alt-folder havuz kopyalanır ve oluşturulan olmaz.<br/>İzin verilen değerler: **true** (varsayılan), **false** | Hayır |

**Örnek:**

```json
"activities":[
    {
        "name": "CopyFromADLS",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<ADLS input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "AzureDataLakeStoreSource",
                "recursive": true
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="azure-data-lake-store-as-sink"></a>Azure Data Lake Store havuz olarak

Azure Data Lake Store'a veri kopyalamak için kopyalama etkinliği Havuz türü ayarlayın. **AzureDataLakeStoreSink**. Aşağıdaki özellikler de desteklenen **havuz** bölümü:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Kopya etkinliği havuz tür özelliği ayarlamak: **AzureDataLakeStoreSink** |Evet |
| copyBehavior | Kaynak dosyaları dosya tabanlı veri deposundan olduğunda kopyalama davranışını tanımlar.<br/><br/>İzin verilen değerler:<br/><b>-PreserveHierarchy (varsayılan)</b>: Dosya hiyerarşisi hedef klasördeki korur. Kaynak dosyanın kaynak klasöre göreli yol, hedef dosya hedef klasöre göreli yolunu aynıdır.<br/><b>-FlattenHierarchy</b>: tüm kaynak klasörü hedef klasör ilk düzeyi dosyalarıdır. Hedef dosyalar otomatik adına sahip. <br/><b>-MergeFiles</b>: bir dosya için kaynak klasöründeki tüm dosyaları birleştirir. Birleştirilmiş Dosya adı, dosya/Blob adı belirtilirse, belirtilen ad olur; Aksi takdirde otomatik olarak oluşturulan dosya adı olacaktır. | Hayır |

**Örnek:**

```json
"activities":[
    {
        "name": "CopyToADLS",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<ADLS output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "AzureDataLakeStoreSink",
                "copyBehavior": "PreserveHierarchy"
            }
        }
    }
]
```

### <a name="recursive-and-copybehavior-examples"></a>özyinelemeli ve copyBehavior örnekleri

Bu bölümde, sonuçta elde edilen davranışını özyinelemeli ve copyBehavior değerleri farklı birleşimlerini kopyalama işlemi açıklanmaktadır.

| Özyinelemeli | copyBehavior | Kaynak klasör yapısı | Sonuçta elde edilen hedef |
|:--- |:--- |:--- |:--- |
| doğru |preserveHierarchy | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef klasör Klasör1 kaynak aynı yapısını oluşturulur:<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5. |
| doğru |flattenHierarchy | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef Klasör1 aşağıdaki yapısıyla oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya3 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File4 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;File5 için otomatik olarak oluşturulan adı |
| doğru |mergeFiles | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef Klasör1 aşağıdaki yapısıyla oluşturulur: <br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 + dosya3 + File4 + 5 dosyası içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir |
| yanlış |preserveHierarchy | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |
| yanlış |flattenHierarchy | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya1 için otomatik olarak oluşturulan adı<br/>&nbsp;&nbsp;&nbsp;&nbsp;dosya2 için otomatik olarak oluşturulan adı<br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |
| yanlış |mergeFiles | Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File1<br/>&nbsp;&nbsp;&nbsp;&nbsp;File2<br/>&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5 | Hedef klasör Klasör1 aşağıdaki yapısıyla oluşturulur<br/><br/>Klasör1<br/>&nbsp;&nbsp;&nbsp;&nbsp;Dosya1 + dosya2 içeriği otomatik olarak oluşturulan dosya adında bir dosya halinde birleştirilir. dosya1 için otomatik olarak oluşturulan adı<br/><br/>Dosya3, File4 ve File5 Subfolder1 değil toplanma. |

## <a name="next-steps"></a>Sonraki adımlar
Kaynakları ve havuzlarını Azure Data Factory kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](copy-activity-overview.md##supported-data-stores-and-formats).
