---
title: "aaaTroubleshooting Linux VM uzantısı hataları | Microsoft Docs"
description: "Azure Linux VM uzantısı hatalarını giderme hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: f05d93f3-42fc-4a09-9798-d92f7929c417
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: 29a0ca34207421e0014380000a313d3c44e7e594
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="d2fd4-103">Azure Linux VM uzantısı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d2fd4-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="d2fd4-104">Uzantı durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d2fd4-104">Viewing extension status</span></span>
<span data-ttu-id="d2fd4-105">Azure Resource Manager şablonları hello Azure CLI ' çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-105">Azure Resource Manager templates can be executed from hello  Azure CLI.</span></span> <span data-ttu-id="d2fd4-106">Merhaba şablon yürütüldükten sonra Azure kaynak Gezgini veya hello komut satırı araçları'ndan hello uzantı durumunu görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="d2fd4-107">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d2fd4-107">Here is an example:</span></span>

<span data-ttu-id="d2fd4-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="d2fd4-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="d2fd4-109">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d2fd4-109">Here is hello sample output:</span></span>

      Extensions:  {
      "ExtensionType": "Microsoft.Compute.CustomScriptExtension",
      "Name": "myCustomScriptExtension",
      "SubStatuses": [
        {
          "Code": "ComponentStatus/StdOut/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "    Directory: C:\\temp\\n\\n\\nMode                LastWriteTime     Length Name
              \\n----                -------------     ------ ----                              \\n-a---          9/1/2015   2:03 AM         11
              test.txt                          \\n\\n",
                      "Time": null
          },
        {
          "Code": "ComponentStatus/StdErr/succeeded",
          "DisplayStatus": "Provisioning succeeded",
          "Level": "Info",
          "Message": "",
          "Time": null
        }
    }
  <span data-ttu-id="d2fd4-110">]</span><span class="sxs-lookup"><span data-stu-id="d2fd4-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="d2fd4-111">Extenson hataları sorunlarını giderme:</span><span class="sxs-lookup"><span data-stu-id="d2fd4-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="d2fd4-112">Merhaba VM yeniden çalıştırarak hello uzantısı</span><span class="sxs-lookup"><span data-stu-id="d2fd4-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="d2fd4-113">Komut dosyaları hello özel betik uzantısının kullanarak VM üzerinde çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak hello komut başarısız oldu bir hatayla bazen çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="d2fd4-114">Bu conditons altında bu hatadan yolu toorecover önerilen hello tooremove hello uzantısıdır ve hello şablonu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="d2fd4-115">Not: gelecekte Gelişmiş tooremove bu işlevselliği olacaktır hello gerek hello uzantısı kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-cli"></a><span data-ttu-id="d2fd4-116">Azure CLI üzerinden Hello uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="d2fd4-116">Remove hello extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="d2fd4-117">Burada "publsher-name" karşılık gelen "azure vm get-örnek-Görünüm" Merhaba çıktısından toohello uzantısı türü ve hello adıdır hello şablondan hello uzantısı kaynağının adı</span><span class="sxs-lookup"><span data-stu-id="d2fd4-117">Where "publsher-name" corresponds toohello extension type from hello output of "azure vm get-instance-view" and name is hello name of hello extension resource from hello template</span></span>

<span data-ttu-id="d2fd4-118">Merhaba uzantısı kaldırıldıktan sonra hello şablon hello VM yeniden yürütülen toorun hello komut olabilir.</span><span class="sxs-lookup"><span data-stu-id="d2fd4-118">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

