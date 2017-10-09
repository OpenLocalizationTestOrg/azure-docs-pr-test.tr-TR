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
# <a name="require-secure-transfer"></a><span data-ttu-id="ab6c9-103">Güvenli aktarım gerektir</span><span class="sxs-lookup"><span data-stu-id="ab6c9-103">Require secure transfer</span></span>

<span data-ttu-id="ab6c9-104">"Merhaba güvenli aktarımı gerekli" seçeneği, yalnızca istekleri güvenli bağlantılar toohello depolama hesabından izin vererek depolama hesabınız hello güvenliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="ab6c9-105">Örneğin, REST API'leri tooaccess depolama hesabınız çağrılırken, HTTPS kullanarak bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="ab6c9-106">"Güvenli aktarım gerekli" etkinleştirildiğinde, HTTP kullanarak tüm istekler reddedilir.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="ab6c9-107">Hello Azure dosyaları hizmetini kullanırken, "güvenli aktarım gerekli" etkinleştirilmişse, şifreleme olmadan herhangi bir bağlantı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="ab6c9-108">Bu, SMB 2.1, SMB 3.0 şifreleme olmadan ve bazı özellikleri hello Linux SMB istemcisi kullanarak senaryolar içerir.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="ab6c9-109">Varsayılan olarak, "Merhaba güvenli aktarımı gerekli" seçenek devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="ab6c9-110">Azure depolama özel etki alanı adları HTTPS desteklemediğinden, bu seçenek özel etki alanı kullanırken uygulanmıyor.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="ab6c9-111">"Güvenli aktarımı gerekli" Merhaba Azure portal etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ab6c9-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="ab6c9-112">"Hello bir depolama hesabı oluşturduğunuzda, her ikisi de ayarlanması gereken hello güvenli aktarımı" etkinleştirebilirsiniz [Azure portal](https://portal.azure.com)ve var olan depolama hesapları için.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="ab6c9-113">Bir depolama hesabı oluşturduğunuzda güvenli aktarımı gerektirir</span><span class="sxs-lookup"><span data-stu-id="ab6c9-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="ab6c9-114">Açık hello **depolama hesabı oluşturma** dikey penceresinde hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="ab6c9-115">Altında **güvenli aktarımı gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="ab6c9-117">Güvenli aktarımı için varolan bir depolama hesabı gerektirir</span><span class="sxs-lookup"><span data-stu-id="ab6c9-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="ab6c9-118">Mevcut bir depolama hesabını hello Azure portal'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="ab6c9-119">Seçin **yapılandırma** altında **ayarları** hello depolama hesabı menü dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="ab6c9-120">Altında **güvenli aktarımı gerekli**seçin **etkin**.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![ekran görüntüsü](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="ab6c9-122">"Güvenli aktarım gerekli" etkinleştirmek program aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="ab6c9-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="ab6c9-123">Merhaba ayarı adı _supportsHttpsTrafficOnly_ depolama hesabı özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="ab6c9-124">"REST API, araçları veya kitaplıkları ile ayarlanması gereken güvenli aktarımı" etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab6c9-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="ab6c9-125">**REST API** (sürüm: 2016-12-01): [sürüm paketi](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="ab6c9-126">**PowerShell** (sürüm: 4.1.0'da): [sürüm paketi](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="ab6c9-127">**CLI** (sürüm: 2.0.11): [sürüm paketi](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="ab6c9-128">**NodeJS** (sürüm: 1.1.0): [sürüm paketi](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="ab6c9-129">**.NET SDK'sı** (sürüm: 6.3.0): [sürüm paketi](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="ab6c9-130">**Python SDK** (sürüm: 1.1.0): [sürüm paketi](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="ab6c9-131">**Söyleniş SDK** (sürüm: 0.11.0): [sürüm paketi](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="ab6c9-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="ab6c9-132">"REST API'si ile ayarlanması gereken güvenli aktarımı" etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ab6c9-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="ab6c9-133">REST API ile test toosimplify kullanabileceğiniz [ArmClient](https://github.com/projectkudu/ARMClient) komut satırından toocall.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="ab6c9-134">Komut satırı toocheck hello hello REST API ayarıyla aşağıda kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab6c9-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="ab6c9-135">Merhaba yanıtta bulduğunuz _supportsHttpsTrafficOnly_ ayarı.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="ab6c9-136">Örnek:</span><span class="sxs-lookup"><span data-stu-id="ab6c9-136">Sample:</span></span>

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

<span data-ttu-id="ab6c9-137">Komut satırı tooenable hello hello REST API ayarıyla aşağıda kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab6c9-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="ab6c9-138">Söz konusu Input.json örneği:</span><span class="sxs-lookup"><span data-stu-id="ab6c9-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="ab6c9-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab6c9-139">Next steps</span></span>
<span data-ttu-id="ab6c9-140">Azure depolama toobuild güvenli uygulamalar birlikte, geliştiricilerin güvenlik özellikleri kapsamlı bir kümesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab6c9-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="ab6c9-141">Daha fazla ayrıntı için hello ziyaret [depolama Güvenlik Kılavuzu](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ab6c9-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
