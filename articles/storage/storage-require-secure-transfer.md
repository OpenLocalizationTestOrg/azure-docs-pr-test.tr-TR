---
title: "Azure storage'da aaaRequire güvenli aktarımı | Microsoft Docs"
description: "Azure Storage için Hello \"güvenli aktarımı gerektirir\" özelliği hakkında bilgi edinmek ve nasıl tooenable onu."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Güvenli aktarım gerektir

"Merhaba güvenli aktarımı gerekli" seçeneği, yalnızca istekleri güvenli bağlantılar toohello depolama hesabından izin vererek depolama hesabınız hello güvenliğini artırır. Örneğin, REST API'leri tooaccess depolama hesabınız çağrılırken, HTTPS kullanarak bağlanmanız gerekir. "Güvenli aktarım gerekli" etkinleştirildiğinde, HTTP kullanarak tüm istekler reddedilir.

Hello Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur. Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve bazı özellikleri hello Linux SMB istemcisi kullanarak senaryolar içerir. 

Varsayılan olarak, "Merhaba güvenli aktarımı gerekli" seçenek devre dışıdır.

> [!NOTE]
> Azure depolama özel etki alanı adları HTTPS desteklemediğinden, bu seçenek özel etki alanı kullanırken uygulanmıyor.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>"Güvenli aktarımı gerekli" Merhaba Azure portal etkinleştir

"Hello bir depolama hesabı oluşturduğunuzda, her ikisi de ayarlanması gereken hello güvenli aktarımı" etkinleştirebilirsiniz [Azure portal](https://portal.azure.com)ve var olan depolama hesapları için.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Bir depolama hesabı oluşturduğunuzda güvenli aktarımı gerektirir

1. Açık hello **depolama hesabı oluşturma** dikey penceresinde hello Azure portalı.
1. Altında **güvenli aktarımı gerekli**seçin **etkin**.

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Güvenli aktarımı için varolan bir depolama hesabı gerektirir

1. Mevcut bir depolama hesabını hello Azure portal'ı seçin.
1. Seçin **yapılandırma** altında **ayarları** hello depolama hesabı menü dikey penceresinde.
1. Altında **güvenli aktarımı gerekli**seçin **etkin**.

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>"Güvenli aktarım gerekli" etkinleştirmek program aracılığıyla

Merhaba ayarı adı _supportsHttpsTrafficOnly_ depolama hesabı özellikleri. "REST API, araçları veya kitaplıkları ile ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz:

* **REST API** (sürüm: 2016-12-01): [sürüm paketi](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (sürüm: 4.1.0'da): [sürüm paketi](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (sürüm: 2.0.11): [sürüm paketi](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (sürüm: 1.1.0): [sürüm paketi](https://www.npmjs.com/package/azure-arm-storage/)
* **.NET SDK'sı** (sürüm: 6.3.0): [sürüm paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **Python SDK** (sürüm: 1.1.0): [sürüm paketi](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **Söyleniş SDK** (sürüm: 0.11.0): [sürüm paketi](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>"REST API'si ile ayarlanması gereken güvenli aktarımı" etkinleştirme

REST API ile test toosimplify kullanabileceğiniz [ArmClient](https://github.com/projectkudu/ARMClient) komut satırından toocall.

 Komut satırı toocheck hello hello REST API ayarıyla aşağıda kullanabilirsiniz:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Merhaba yanıtta bulduğunuz _supportsHttpsTrafficOnly_ ayarı. Örnek:

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

Komut satırı tooenable hello hello REST API ayarıyla aşağıda kullanabilirsiniz:

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
Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar. Daha fazla ayrıntı için hello ziyaret [depolama Güvenlik Kılavuzu](storage-security-guide.md).
