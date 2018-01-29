---
title: Azure Data Factory kullanarak SAP BW veri kopyalama | Microsoft Docs
description: "Veri kopyalama etkinliği Azure Data Factory ardışık düzeninde kullanarak SAP Business Warehouse desteklenen havuz veri depolarına kopyalama öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: jingwang
ms.openlocfilehash: 7f494cff1e8dc57a41467cd722fdf224e10c9dec
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-from-sap-business-warehouse-using-azure-data-factory"></a>Azure Data Factory kullanarak SAP Business Warehouse verilerini
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Sürüm 1 - Genel Kullanım](v1/data-factory-sap-business-warehouse-connector.md)
> * [Sürüm 2 - Önizleme](connector-sap-business-warehouse.md)

Bu makalede kopya etkinliği Azure Data Factory'de bir SAP Business Warehouse (BW) gelen verileri kopyalamak için nasıl kullanılacağı açıklanmaktadır. Derlemeler [etkinlik genel bakış kopyalama](copy-activity-overview.md) makale kopyalama etkinliği genel bir bakış sunar.

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Genel olarak kullanılabilir (GA) Data Factory Hizmeti'ne 1 sürümünü kullanıyorsanız bkz [V1 SAP BW Bağlayıcısı](v1/data-factory-sap-business-warehouse-connector.md).

## <a name="supported-capabilities"></a>Desteklenen özellikler

SAP Business Warehouse verileri herhangi bir desteklenen havuz veri deposuna kopyalayabilirsiniz. Kaynakları/havuzlarını kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](copy-activity-overview.md#supported-data-stores-and-formats) tablo.

Özellikle, bu SAP Business Warehouse Bağlayıcısı destekler:

- SAP Business Warehouse **sürümü 7.x**.
- Verileri kopyalama **Infocubes ve QueryCubes** (BEx dahil olmak üzere) MDX sorguları kullanarak sorguları.
- Temel kimlik doğrulaması kullanarak veri kopyalama.

## <a name="prerequisites"></a>Önkoşullar

Bu SAP Business Warehouse Bağlayıcısı'nı kullanmak için aktarmanız gerekir:

- Self-hosted tümleştirme çalışma zamanı ayarlayın. Bkz: [Self-hosted tümleştirmesi çalışma zamanı](create-self-hosted-integration-runtime.md) Ayrıntılar için makale.
- Yükleme **SAP NetWeaver Kitaplığı** tümleştirmesi çalışma zamanı makinede. SAP Netweaver kitaplığı SAP yöneticinizden ya da doğrudan alabilirsiniz [SAP yazılım İndirme Merkezi](https://support.sap.com/swdc). Arama **SAP Not #1025361** en son sürümü karşıdan yükleme konumu alınamıyor. Çekme emin olun **64-bit** tümleştirmesi çalışma zamanı yükleme eşleşen SAP NetWeaver kitaplığı. Daha sonra SAP Not göre SAP NetWeaver RFC SDK'sı bulunan tüm dosyaları yükleyin. SAP NetWeaver kitaplığı SAP istemci araçlarını yükleme de dahil edilir.

> [!TIP]
> NetWeaver RFC SDK'dan system32 klasörüne ayıklanan DLL'leri yerleştirin.

## <a name="getting-started"></a>Başlarken

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Aşağıdaki bölümler için SAP Business Warehouse Bağlayıcısı Data Factory varlıklarını belirli tanımlamak için kullanılan özellikleri hakkında ayrıntılı bilgi sağlar.

## <a name="linked-service-properties"></a>Bağlantılı hizmet özellikleri

Aşağıdaki özellikler SAP Business Warehouse (BW) bağlantılı hizmeti için desteklenir:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Type özelliği ayarlanmalıdır: **SapBw** | Evet |
| sunucu | SAP BW örneği bulunduğu sunucunun adıdır. | Evet |
| systemNumber | SAP BW sisteminin sistem numarası.<br/>İzin verilen değer: dize olarak temsil iki basamaklı bir ondalık sayı. | Evet |
| clientId | SAP W sistem istemcisinde istemci kimliği.<br/>İzin verilen değer: dize olarak temsil üç basamaklı bir ondalık sayı. | Evet |
| Kullanıcı adı | SAP sunucusuna erişimi olan kullanıcı adı. | Evet |
| password | Kullanıcının parolası. Bu alan bir SecureString işaretleyin. | Evet |
| connectVia | [Tümleştirmesi çalışma zamanı](concepts-integration-runtime.md) veri deposuna bağlanmak için kullanılacak. Bölümünde belirtildiği gibi bir Self-hosted tümleştirmesi çalışma zamanı gereklidir [Önkoşullar](#prerequisites). |Evet |

**Örnek:**

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "userName": "<SAP user>",
            "password": {
                "type": "SecureString",
                "value": "<Password for SAP user>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Veri kümesi özellikleri

Bölümleri ve veri kümelerini tanımlamak için kullanılabilen özellikleri tam listesi için veri kümeleri makalesine bakın. Bu bölümde, SAP BW veri kümesi tarafından desteklenen özellikler listesini sağlar.

SAP BW verileri kopyalamak için kümesine tür özelliği ayarlamak **RelationalTable**. SAP BW veri kaynağının veri kümesi için desteklenen hiçbir türüne özgü özellikleri varken RelationalTable yazın.

**Örnek:**

```json
{
    "name": "SAPBWDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<SAP BW linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a>Kopyalama etkinliğinin özellikleri

Bölümleri ve etkinlikleri tanımlamak için kullanılabilen özellikleri tam listesi için bkz: [ardışık düzen](concepts-pipelines-activities.md) makalesi. Bu bölümde, SAP BW kaynak tarafından desteklenen özellikler listesini sağlar.

### <a name="sap-bw-as-source"></a>SAP BW kaynağı olarak

SAP BW verileri kopyalamak için kopyalama etkinliği için kaynak türünü ayarlayın. **RelationalSource**. Aşağıdaki özellikler kopyalama etkinliği desteklenen **kaynak** bölümü:

| Özellik | Açıklama | Gerekli |
|:--- |:--- |:--- |
| type | Kopyalama etkinliği kaynağı tür özelliği ayarlamak: **RelationalSource** | Evet |
| sorgu | SAP BW örneğinden verileri okumak için MDX Sorgusu belirtir. | Evet |

**Örnek:**

```json
"activities":[
    {
        "name": "CopyFromSAPBW",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<SAP BW input dataset name>",
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
                "type": "RelationalSource",
                "query": "<MDX query for SAP BW>"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sap-bw"></a>SAP BW için veri türü eşlemesi

SAP BW veri kopyalama işlemi sırasında aşağıdaki eşlemelerini SAP BW veri türlerinden Azure Data Factory geçici veri türleri için kullanılır. Bkz: [şema ve veri türü eşlemeleri](copy-activity-schema-and-type-mapping.md) nasıl kopyalama etkinliği kaynak şema ve veri türü için havuz eşlemeleri hakkında bilgi edinmek için.

| SAP BW veri türü | Veri Fabrikası geçici veri türü |
|:--- |:--- |
| ACCP | Int |
| CHAR | Dize |
| CLNT | Dize |
| CURR | Ondalık |
| CUKY | Dize |
| DEC | Ondalık |
| FLTP | Çift |
| INT1 | Bayt |
| INT2 | Int16 |
| INT4 | Int |
| DİL | Dize |
| LCHR | Dize |
| LRAW | Byte] |
| PREC | Int16 |
| QUAN | Ondalık |
| RAW | Byte] |
| RAWSTRING | Byte] |
| DİZE | Dize |
| BİRİM | Dize |
| DATS | Dize |
| NUMC | Dize |
| TIMS | Dize |


## <a name="next-steps"></a>Sonraki adımlar
Kaynakları ve havuzlarını Azure Data Factory kopyalama etkinliği tarafından desteklenen veri depoları listesi için bkz: [desteklenen veri depoları](copy-activity-overview.md#supported-data-stores-and-formats).