---
title: "Azure storage'da güvenli aktarımı gerektiren | Microsoft Docs"
description: "\"Güvenli aktarımı gerektirir\" özelliği Azure Storage ve bunun nasıl etkinleştirileceğini öğrenin."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="require-secure-transfer"></a>Güvenli aktarım gerektir

"Güvenli aktarım gerekli" seçeneği, yalnızca istekleri depolama hesabınıza güvenli bağlantılardan vererek depolama hesabınızın güvenliğini artırır. Örneğin, depolama hesabınıza erişmek için REST API'leri çağrılırken, HTTPS kullanarak bağlanmanız gerekir. "Güvenli aktarım gerekli" etkinleştirildiğinde, HTTP kullanarak tüm istekler reddedilir.

Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur. Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve Linux SMB istemcisi bazı özellikleri kullanarak senaryolar içerir. 

Varsayılan olarak "güvenli aktarım gerekli" seçeneği devre dışıdır.

> [!NOTE]
> Azure depolama özel etki alanı adları HTTPS desteklemediğinden, bu seçenek özel etki alanı kullanırken uygulanmıyor.

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a>"Güvenli aktarım gerekli" Azure portalında etkinleştir

"Depolama hesabı oluşturduğunuzda, her ikisi de ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz [Azure portal](https://portal.azure.com)ve var olan depolama hesapları için.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Bir depolama hesabı oluşturduğunuzda güvenli aktarımı gerektirir

1. Açık **depolama hesabı oluşturma** Azure portaldaki dikey pencere.
1. Altında **güvenli aktarımı gerekli**seçin **etkin**.

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Güvenli aktarımı için varolan bir depolama hesabı gerektirir

1. Azure Portalı'nda mevcut bir depolama hesabını seçin.
1. Seçin **yapılandırma** altında **ayarları** depolama hesabı menü dikey.
1. Altında **güvenli aktarımı gerekli**seçin **etkin**.

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>"Güvenli aktarım gerekli" etkinleştirmek program aracılığıyla

Ayar adı şudur _supportsHttpsTrafficOnly_ depolama hesabı özellikleri. "REST API, araçları veya kitaplıkları ile ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz:

* **REST API** (sürüm: 2016-12-01): [sürüm paketi](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (sürüm: 4.1.0'da): [sürüm paketi](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (sürüm: 2.0.11): [sürüm paketi](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (sürüm: 1.1.0): [sürüm paketi](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK'sı** (sürüm: 6.3.0): [sürüm paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (sürüm: 1.1.0): [sürüm paketi](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Söyleniş SDK** (sürüm: 0.11.0): [sürüm paketi](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>"REST API'si ile ayarlanması gereken güvenli aktarımı" etkinleştirme

REST API ile test etmeyi kolaylaştırmak için kullanabileceğiniz [ArmClient](https://github.com/projectkudu/ARMClient) komut satırından çağırmak için.

 REST API ile ayarını denetlemek için komut satırını kullanın:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Yanıtta, bulduğunuz _supportsHttpsTrafficOnly_ ayarı. Örnek:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

REST API ile ayarı etkinleştirmek için komut satırını kullanın:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Söz konusu Input.json örneği:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Azure depolama birlikte geliştiricilerin güvenli uygulamalar oluşturmasını sağlama güvenlik özellikleri kapsamlı bir kümesini sağlar. Daha fazla ayrıntı için ziyaret [depolama Güvenlik Kılavuzu](storage-security-guide.md).
