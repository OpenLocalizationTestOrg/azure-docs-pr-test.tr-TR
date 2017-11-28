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
# <a name="require-secure-transfer"></a><span data-ttu-id="912d8-103">Güvenli aktarım gerektir</span><span class="sxs-lookup"><span data-stu-id="912d8-103">Require secure transfer</span></span>

<span data-ttu-id="912d8-104">"Güvenli aktarım gerekli" seçeneği, yalnızca istekleri depolama hesabınıza güvenli bağlantılardan vererek depolama hesabınızın güvenliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="912d8-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="912d8-105">Örneğin, depolama hesabınıza erişmek için REST API'leri çağrılırken, HTTPS kullanarak bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="912d8-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="912d8-106">"Güvenli aktarım gerekli" etkinleştirildiğinde, HTTP kullanarak tüm istekler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="912d8-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="912d8-107">Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="912d8-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="912d8-108">Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve Linux SMB istemcisi bazı özellikleri kullanarak senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="912d8-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="912d8-109">Varsayılan olarak "güvenli aktarım gerekli" seçeneği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="912d8-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="912d8-110">Azure depolama özel etki alanı adları HTTPS desteklemediğinden, bu seçenek özel etki alanı kullanırken uygulanmıyor.</span><span class="sxs-lookup"><span data-stu-id="912d8-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="912d8-111">"Güvenli aktarım gerekli" Azure portalında etkinleştir</span><span class="sxs-lookup"><span data-stu-id="912d8-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="912d8-112">"Depolama hesabı oluşturduğunuzda, her ikisi de ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz [Azure portal](https://portal.azure.com)ve var olan depolama hesapları için.</span><span class="sxs-lookup"><span data-stu-id="912d8-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="912d8-113">Bir depolama hesabı oluşturduğunuzda güvenli aktarımı gerektirir</span><span class="sxs-lookup"><span data-stu-id="912d8-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="912d8-114">Açık **depolama hesabı oluşturma** Azure portaldaki dikey pencere.</span><span class="sxs-lookup"><span data-stu-id="912d8-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="912d8-115">Altında **güvenli aktarımı gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="912d8-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="912d8-117">Güvenli aktarımı için varolan bir depolama hesabı gerektirir</span><span class="sxs-lookup"><span data-stu-id="912d8-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="912d8-118">Azure Portalı'nda mevcut bir depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="912d8-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="912d8-119">Seçin **yapılandırma** altında **ayarları** depolama hesabı menü dikey.</span><span class="sxs-lookup"><span data-stu-id="912d8-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="912d8-120">Altında **güvenli aktarımı gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="912d8-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="912d8-122">"Güvenli aktarım gerekli" etkinleştirmek program aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="912d8-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="912d8-123">Ayar adı şudur _supportsHttpsTrafficOnly_ depolama hesabı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="912d8-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="912d8-124">"REST API, araçları veya kitaplıkları ile ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="912d8-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="912d8-125">**REST API** (sürüm: 2016-12-01): [sürüm paketi](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="912d8-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="912d8-126">**PowerShell** (sürüm: 4.1.0'da): [sürüm paketi](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="912d8-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="912d8-127">**CLI** (sürüm: 2.0.11): [sürüm paketi](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="912d8-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="912d8-128">**NodeJS** (sürüm: 1.1.0): [sürüm paketi](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="912d8-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="912d8-129">**.NET SDK'sı** (sürüm: 6.3.0): [sürüm paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="912d8-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="912d8-130">**Python SDK** (sürüm: 1.1.0): [sürüm paketi](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="912d8-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="912d8-131">**Söyleniş SDK** (sürüm: 0.11.0): [sürüm paketi](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="912d8-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="912d8-132">"REST API'si ile ayarlanması gereken güvenli aktarımı" etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="912d8-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="912d8-133">REST API ile test etmeyi kolaylaştırmak için kullanabileceğiniz [ArmClient](https://github.com/projectkudu/ARMClient) komut satırından çağırmak için.</span><span class="sxs-lookup"><span data-stu-id="912d8-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="912d8-134">REST API ile ayarını denetlemek için komut satırını kullanın:</span><span class="sxs-lookup"><span data-stu-id="912d8-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="912d8-135">Yanıtta, bulduğunuz _supportsHttpsTrafficOnly_ ayarı.</span><span class="sxs-lookup"><span data-stu-id="912d8-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="912d8-136">Örnek:</span><span class="sxs-lookup"><span data-stu-id="912d8-136">Sample:</span></span>

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

<span data-ttu-id="912d8-137">REST API ile ayarı etkinleştirmek için komut satırını kullanın:</span><span class="sxs-lookup"><span data-stu-id="912d8-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="912d8-138">Söz konusu Input.json örneği:</span><span class="sxs-lookup"><span data-stu-id="912d8-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="912d8-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="912d8-139">Next steps</span></span>
<span data-ttu-id="912d8-140">Azure depolama birlikte geliştiricilerin güvenli uygulamalar oluşturmasını sağlama güvenlik özellikleri kapsamlı bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="912d8-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="912d8-141">Daha fazla ayrıntı için ziyaret [depolama Güvenlik Kılavuzu](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="912d8-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
