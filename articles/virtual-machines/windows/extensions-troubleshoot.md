---
title: "aaaTroubleshooting Windows VM uzantısı hataları | Microsoft Docs"
description: "Azure Windows VM uzantısı hatalarını giderme hakkında bilgi edinin"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: top-support-issue,azure-resource-manager
ms.assetid: 878ab9b6-c3e6-40be-82d4-d77fecd5030f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: d24544743d9e0cb1a68ec9ab7718716f918054f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="d6b77-103">Azure Windows VM uzantısı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d6b77-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="d6b77-104">Uzantı durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d6b77-104">Viewing extension status</span></span>
<span data-ttu-id="d6b77-105">Azure Resource Manager şablonları Azure Powershell'den çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6b77-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="d6b77-106">Merhaba şablon yürütüldükten sonra Azure kaynak Gezgini veya hello komut satırı araçları'ndan hello uzantı durumunu görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="d6b77-106">Once hello template is executed, hello extension status can be viewed from Azure Resource Explorer or hello command line tools.</span></span>

<span data-ttu-id="d6b77-107">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d6b77-107">Here is an example:</span></span>

<span data-ttu-id="d6b77-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d6b77-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="d6b77-109">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d6b77-109">Here is hello sample output:</span></span>

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
  <span data-ttu-id="d6b77-110">]</span><span class="sxs-lookup"><span data-stu-id="d6b77-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="d6b77-111">Uzantı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d6b77-111">Troubleshooting extension failures</span></span>
### <a name="re-running-hello-extension-on-hello-vm"></a><span data-ttu-id="d6b77-112">Merhaba VM yeniden çalıştırarak hello uzantısı</span><span class="sxs-lookup"><span data-stu-id="d6b77-112">Re-running hello extension on hello VM</span></span>
<span data-ttu-id="d6b77-113">Komut dosyaları hello özel betik uzantısının kullanarak VM üzerinde çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak hello komut başarısız oldu bir hatayla bazen çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="d6b77-113">If you are running scripts on hello VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but hello script has failed.</span></span> <span data-ttu-id="d6b77-114">Bu conditons altında bu hatadan yolu toorecover önerilen hello tooremove hello uzantısıdır ve hello şablonu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6b77-114">Under these conditons, hello recommended way toorecover from this error is tooremove hello extension and rerun hello template again.</span></span>
<span data-ttu-id="d6b77-115">Not: gelecekte Gelişmiş tooremove bu işlevselliği olacaktır hello gerek hello uzantısı kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="d6b77-115">Note: In future, this functionality would be enhanced tooremove hello need for uninstalling hello extension.</span></span>

#### <a name="remove-hello-extension-from-azure-powershell"></a><span data-ttu-id="d6b77-116">Azure PowerShell Hello uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="d6b77-116">Remove hello extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="d6b77-117">Merhaba uzantısı kaldırıldıktan sonra hello şablon hello VM yeniden yürütülen toorun hello komut olabilir.</span><span class="sxs-lookup"><span data-stu-id="d6b77-117">Once hello extension has been removed, hello template can be re-executed toorun hello scripts on hello VM.</span></span>

