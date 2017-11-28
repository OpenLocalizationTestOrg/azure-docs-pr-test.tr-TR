---
title: "Linux sanal makineleri Azure üzerinde aaaRun özel komut dosyaları | Microsoft Docs"
description: "Merhaba özel betik uzantısının kullanarak Linux VM yapılandırma görevleri otomatikleştirme"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="fb142-103">Hello Azure özel betik uzantısı ile Linux sanal makineleri kullanma</span><span class="sxs-lookup"><span data-stu-id="fb142-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="fb142-104">Merhaba özel betik uzantısının indirir ve Azure sanal makinelerde komut dosyalarını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="fb142-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="fb142-105">Bu dağıtım yapılandırmaları, yazılım yükleme veya başka bir yapılandırma için yararlı bir uzantısıdır / yönetim görevi.</span><span class="sxs-lookup"><span data-stu-id="fb142-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="fb142-106">Komut dosyaları Azure depolama veya diğer erişilebilir Internet konumdan indirilen veya çalışma zamanı toohello uzantısı sağlanan.</span><span class="sxs-lookup"><span data-stu-id="fb142-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="fb142-107">Merhaba özel betik uzantısı Azure Resource Manager şablonları ile tümleşir ve hello Azure CLI, PowerShell, Azure portal veya hello Azure sanal makine REST API'sini kullanarak da çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="fb142-108">Bu belge ayrıntıları nasıl toouse hello gelen özel betik uzantısının Azure CLI ve Azure Resource Manager şablonu ve ayrıca sorun giderme adımları Linux sistemlerde ayrıntılarını hello.</span><span class="sxs-lookup"><span data-stu-id="fb142-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="fb142-109">Uzantı yapılandırması</span><span class="sxs-lookup"><span data-stu-id="fb142-109">Extension Configuration</span></span>
<span data-ttu-id="fb142-110">Merhaba özel betik uzantısı yapılandırma komut dosyası konumunu ve hello komutu toobe çalıştırmak gibi belirtir.</span><span class="sxs-lookup"><span data-stu-id="fb142-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="fb142-111">Bu yapılandırma hello komut satırında veya bir Azure Resource Manager şablonunda belirtilen yapılandırma dosyalarında depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="fb142-112">Duyarlı veri şifrelenir ve yalnızca hello sanal makine içinde şifresi bir korumalı bir yapılandırma depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="fb142-113">Merhaba korumalı yapılandırma, bir parola gibi gizli Hello yürütme komutu içerir yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb142-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="fb142-114">Genel yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb142-114">Public Configuration</span></span>
<span data-ttu-id="fb142-115">Şema:</span><span class="sxs-lookup"><span data-stu-id="fb142-115">Schema:</span></span>

<span data-ttu-id="fb142-116">**Not** -bu özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb142-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="fb142-117">Merhaba adları tooavoid dağıtım sorunlarını görüldüğü gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb142-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="fb142-118">**commandToExecute**: (gerekli, string) giriş noktası betik tooexecute hello</span><span class="sxs-lookup"><span data-stu-id="fb142-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="fb142-119">**fileUris**: (isteğe bağlı, dize dizisi) dosyaları toobe hello URL'lerini indirilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="fb142-120">**zaman damgası** (isteğe bağlı, tamsayı) bu alanın değerini değiştirerek bu alan yalnızca tootrigger yeniden çalıştır hello komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb142-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="fb142-121">Korumalı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb142-121">Protected Configuration</span></span>
<span data-ttu-id="fb142-122">Şema:</span><span class="sxs-lookup"><span data-stu-id="fb142-122">Schema:</span></span>

<span data-ttu-id="fb142-123">**Not** -bu özellik adları büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb142-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="fb142-124">Merhaba adları tooavoid dağıtım sorunlarını görüldüğü gibi kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb142-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="fb142-125">**commandToExecute**: (isteğe bağlı, dize) giriş noktası betik tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="fb142-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="fb142-126">Parolalar gibi gizli komutunuzu içeriyorsa, bu alan kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb142-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="fb142-127">**storageAccountName**: (isteğe bağlı, dize) depolama hesabının hello adı.</span><span class="sxs-lookup"><span data-stu-id="fb142-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="fb142-128">Depolama kimlik belirtirseniz, tüm fileUris Azure BLOB'ları için URL'leri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb142-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="fb142-129">**storageAccountKey**: (isteğe bağlı, dize) hello depolama hesabının erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="fb142-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="fb142-130">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fb142-130">Azure CLI</span></span>
<span data-ttu-id="fb142-131">Hello Azure CLI toorun hello özel betik uzantısının kullanırken, bir yapılandırma dosyası veya en düşük hello dosya URI'si ve hello komut yürütme içeren dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fb142-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="fb142-132">İsteğe bağlı olarak hello ayarları hello komutta JSON biçimli dize olarak belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="fb142-133">Belirtilen yürütme sırasında ve ayrı yapılandırma dosyası olmadan hello yapılandırma toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb142-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="fb142-134">Azure CLI örnekleri</span><span class="sxs-lookup"><span data-stu-id="fb142-134">Azure CLI Examples</span></span>

<span data-ttu-id="fb142-135">**Örnek 1** -komut dosyası ile genel yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="fb142-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="fb142-136">Azure CLI komutu:</span><span class="sxs-lookup"><span data-stu-id="fb142-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="fb142-137">**Örnek 2** -herhangi bir komut dosyası ile genel yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="fb142-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="fb142-138">Azure CLI komutu:</span><span class="sxs-lookup"><span data-stu-id="fb142-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="fb142-139">**Örnek 3** - bir ortak yapılandırma dosyası kullanılan toospecify hello komut dosyası URI ve bir korumalı yapılandırma dosyası kullanılan toospecify hello komutu toobe yürütülür.</span><span class="sxs-lookup"><span data-stu-id="fb142-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="fb142-140">Genel yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="fb142-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="fb142-141">Korumalı yapılandırma dosyası:</span><span class="sxs-lookup"><span data-stu-id="fb142-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="fb142-142">Azure CLI komutu:</span><span class="sxs-lookup"><span data-stu-id="fb142-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="fb142-143">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="fb142-143">Resource Manager Template</span></span>
<span data-ttu-id="fb142-144">Hello Azure özel betik uzantısının Resource Manager şablonu kullanarak sanal makine dağıtımı aynı anda çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb142-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="fb142-145">toodo, bu nedenle, doğru biçimlendirilmiş JSON toohello Dağıtım şablonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fb142-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="fb142-146">Resource Manager örnekleri</span><span class="sxs-lookup"><span data-stu-id="fb142-146">Resource Manager Examples</span></span>
<span data-ttu-id="fb142-147">**Örnek 1** -genel yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="fb142-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="fb142-148">**Örnek 2** -korumalı yapılandırmasında yürütme komutu.</span><span class="sxs-lookup"><span data-stu-id="fb142-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="fb142-149">Hello .net Core müzik deposu görmek için tam bir örnek - Demo [müzik deposu Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="fb142-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fb142-150">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="fb142-150">Troubleshooting</span></span>
<span data-ttu-id="fb142-151">Hello özel betik uzantısının çalıştığında, hello komut dosyası oluşturulur veya aşağıdaki örneğine bir dizin benzer toohello indirilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="fb142-152">Merhaba komutu çıktısı bu dizindeki INTO kaydedilmiş de `stdout` ve `stderr` dosya.</span><span class="sxs-lookup"><span data-stu-id="fb142-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="fb142-153">Hello Azure betik uzantısı burada bulunabilir bir günlük üretir.</span><span class="sxs-lookup"><span data-stu-id="fb142-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="fb142-154">Merhaba özel betik uzantısının Hello yürütme durumu da hello Azure CLI ile alınabilir.</span><span class="sxs-lookup"><span data-stu-id="fb142-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="fb142-155">Merhaba çıktı hello metin aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="fb142-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="fb142-156">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="fb142-156">Next Steps</span></span>
<span data-ttu-id="fb142-157">Diğer VM betik uzantıları hakkında daha fazla bilgi için bkz: [Linux için Azure betik uzantısı genel bakış](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb142-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

