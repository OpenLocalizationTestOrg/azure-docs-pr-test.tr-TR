---
title: "Linux VM uzantısı hataları sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 589890de379d0b729de1f1ba9e604e0ec0496f50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a><span data-ttu-id="770a5-103">Azure Linux VM uzantısı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="770a5-103">Troubleshooting Azure Linux VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="770a5-104">Uzantı durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="770a5-104">Viewing extension status</span></span>
<span data-ttu-id="770a5-105">Azure Resource Manager şablonları Azure CLI üzerinden çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="770a5-105">Azure Resource Manager templates can be executed from the  Azure CLI.</span></span> <span data-ttu-id="770a5-106">Şablon yürütüldükten sonra uzantı durumunu Azure kaynak Gezgini veya komut satırı araçları üzerinden görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="770a5-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="770a5-107">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="770a5-107">Here is an example:</span></span>

<span data-ttu-id="770a5-108">Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="770a5-108">Azure CLI:</span></span>

      azure vm get-instance-view


<span data-ttu-id="770a5-109">Örnek çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="770a5-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="770a5-110">]</span><span class="sxs-lookup"><span data-stu-id="770a5-110">]</span></span>

## <a name="troubleshooting-extenson-failures"></a><span data-ttu-id="770a5-111">Extenson hataları sorunlarını giderme:</span><span class="sxs-lookup"><span data-stu-id="770a5-111">Troubleshooting Extenson failures:</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="770a5-112">VM uzantısı yeniden çalıştırmayı</span><span class="sxs-lookup"><span data-stu-id="770a5-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="770a5-113">Özel betik uzantısının kullanarak VM betikleri çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak komut başarısız oldu bir hatayla bazen çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="770a5-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="770a5-114">Bu conditons altında bu hatadan kurtarmak için önerilen uzantıyı kaldırmak ve şablonu yeniden çalıştırın yoldur.</span><span class="sxs-lookup"><span data-stu-id="770a5-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="770a5-115">Not: ileride bu işlevselliği uzantısını kaldırma gereksinimini kaldırmak için Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="770a5-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-cli"></a><span data-ttu-id="770a5-116">Azure CLI üzerinden uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="770a5-116">Remove the extension from Azure CLI</span></span>
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

<span data-ttu-id="770a5-117">Burada "publsher-name", "azure vm get-örnek-Görünüm" çıktısından uzantı türü için karşılık gelen ve şablondan uzantısı kaynağın adını adıdır</span><span class="sxs-lookup"><span data-stu-id="770a5-117">Where "publsher-name" corresponds to the extension type from the output of "azure vm get-instance-view" and name is the name of the extension resource from the template</span></span>

<span data-ttu-id="770a5-118">Uzantı kaldırıldıktan sonra şablonu VM komut dosyalarını çalıştırmak için yeniden yürütülen olabilir.</span><span class="sxs-lookup"><span data-stu-id="770a5-118">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

