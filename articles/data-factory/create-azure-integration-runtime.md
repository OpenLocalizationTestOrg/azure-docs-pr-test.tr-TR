---
title: "Azure Data Factory'de Azure tümleştirme çalışma zamanı oluşturma | Microsoft Docs"
description: "Azure veri veri kopyalamak ve dönüştürme etkinlikleri gönderme için kullanılan fabrikada Azure tümleştirme çalışma zamanı oluşturmayı öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: spelluru
ms.openlocfilehash: b48e08233fb6457c180b280af1076838845fcc94
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="how-to-create-and-configure-azure-integration-runtime"></a>Oluşturma ve Azure tümleştirmesi çalışma zamanı yapılandırma
Tümleştirme çalışma zamanı (IR), farklı ağ ortamlar genelinde veri tümleştirme özellikleri sağlamak için Azure Data Factory tarafından kullanılan işlem altyapısıdır. IR hakkında daha fazla bilgi için bkz: [tümleştirmesi çalışma zamanı](concepts-integration-runtime.md).

> [!NOTE]
> Bu makale şu anda önizleme sürümünde olan Data Factory sürüm 2 için geçerlidir. Genel olarak kullanılabilir (GA) Data Factory Hizmeti'ne 1 sürümünü kullanıyorsanız bkz [veri fabrikası V1 belgelerine](v1/data-factory-introduction.md).

Azure IR yerel işlem Hdınsight gibi hizmetleri için veri hareketlerini ve gönderme veri dönüştürme etkinlikleri gerçekleştirmek için tam olarak yönetilen bir işlem sağlar. Azure Ortamı'nda barındırılan ve ortak erişilebilir uç noktaları ortak ağ ortamında kaynaklara bağlanmayı destekler.

Bu belge nasıl oluşturma ve Azure tümleştirmesi çalışma zamanı yapılandırma tanıtır. 

## <a name="default-azure-ir"></a>Varsayılan Azure IR
Varsayılan olarak, her veri fabrikası Azure IR verileri depolar ve ortak ağ Hizmetleri'nde işlem buluttaki işlemlerini destekleyen arka uç vardır. Bu Azure IR otomatik Çözümle konumdur. Varsa **connectVia** özelliği belirtilmedi bağlantılı hizmet tanımında belirtilen Azure IR kullanılır. Yalnızca bir Azure IR açıkça IR konumunu tanımlamak istersiniz veya neredeyse yönetim amaçla farklı IRS üzerinde etkinlik yürütmeleri Grup istiyorsanız açıkça oluşturmanız gerekir. 

## <a name="create-azure-ir"></a>Azure IR oluşturma
Tümleştirme çalışma zamanı kullanılarak oluşturulabilir **kümesi AzureRmDataFactoryV2IntegrationRuntime** PowerShell cmdlet'i. Bir Azure IR oluşturmak için ad, konum ve türünü komutu belirtin. Bir Azure IR "Batı Avrupa" ayarladığınız konumu oluşturmak için bir örnek komut şöyledir:

```powershell
Set-AzureRmDataFactoryV2IntegrationRuntime -DataFactoryName "SampleV2DataFactory1" -Name "MySampleAzureIR" -ResourceGroupName "ADFV2SampleRG" -Type Managed -Location "West Europe"
```  
Azure IR türü ayarlamak **yönetilen**. Bu tam olarak özellikler esnek bulutta yönetildiğinden dolayı işlem ayrıntılarını belirtmek gerekmez. İşlem belirtin zaman Azure SSIS IR oluşturmak istediğinizi düğüm boyutu ve düğüm sayısı gibi ayrıntıları Daha fazla bilgi için bkz: [oluşturma ve yapılandırma Azure SSIS IR](create-azure-ssis-integration-runtime.md).

Set-AzureRmDataFactoryV2IntegrationRuntime PowerShell cmdlet'ini kullanarak konumunu değiştirmek için varolan bir Azure IR yapılandırabilirsiniz. Bir Azure IR konumu hakkında daha fazla bilgi için bkz: [tümleştirmesi çalışma zamanı giriş](concepts-integration-runtime.md).

## <a name="use-azure-ir"></a>Azure IR kullanın

Bir Azure IR oluşturulduktan sonra bağlantılı hizmet tanımında başvuruda bulunabilir. Aşağıda Azure tümleştirmesi çalışma zamanı nasıl başvurabilir, bir örnek yukarıda Azure depolama bağlantılı hizmetinden oluşturulur:  

```json
{
    "name": "MyStorageLinkedService",
    "properties": {
      "type": "AzureStorage",
      "typeProperties": {
        "connectionString": {
          "value": "DefaultEndpointsProtocol=https;AccountName=myaccountname;AccountKey=...",
          "type": "SecureString"
        }
      },
      "connectVia": {
        "referenceName": "MySampleAzureIR",
        "type": "IntegrationRuntimeReference"
      }   
    }
}

```

## <a name="next-steps"></a>Sonraki adımlar
Tümleştirme çalışma zamanları diğer türleri oluşturma konusunda aşağıdaki makalelere bakın:

- [Kendinden konak tümleştirme çalışma zamanı oluşturma](create-self-hosted-integration-runtime.md)
- [Azure SSIS tümleştirmesi çalışma zamanı oluşturma](create-azure-ssis-integration-runtime.md)
 
