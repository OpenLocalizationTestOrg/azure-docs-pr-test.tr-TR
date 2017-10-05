---
title: "Windows VM uzantısı hataları sorunlarını giderme | Microsoft Docs"
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
ms.openlocfilehash: 4dba196e1b838f2092b30972fb070514bd2a4b25
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a><span data-ttu-id="9ad6d-103">Azure Windows VM uzantısı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9ad6d-103">Troubleshooting Azure Windows VM extension failures</span></span>
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a><span data-ttu-id="9ad6d-104">Uzantı durumunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9ad6d-104">Viewing extension status</span></span>
<span data-ttu-id="9ad6d-105">Azure Resource Manager şablonları Azure Powershell'den çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-105">Azure Resource Manager templates can be executed from Azure PowerShell.</span></span> <span data-ttu-id="9ad6d-106">Şablon yürütüldükten sonra uzantı durumunu Azure kaynak Gezgini veya komut satırı araçları üzerinden görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-106">Once the template is executed, the extension status can be viewed from Azure Resource Explorer or the command line tools.</span></span>

<span data-ttu-id="9ad6d-107">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9ad6d-107">Here is an example:</span></span>

<span data-ttu-id="9ad6d-108">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9ad6d-108">Azure PowerShell:</span></span>

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

<span data-ttu-id="9ad6d-109">Örnek çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9ad6d-109">Here is the sample output:</span></span>

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
  <span data-ttu-id="9ad6d-110">]</span><span class="sxs-lookup"><span data-stu-id="9ad6d-110">]</span></span>

## <a name="troubleshooting-extension-failures"></a><span data-ttu-id="9ad6d-111">Uzantı hataları sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9ad6d-111">Troubleshooting extension failures</span></span>
### <a name="re-running-the-extension-on-the-vm"></a><span data-ttu-id="9ad6d-112">VM uzantısı yeniden çalıştırmayı</span><span class="sxs-lookup"><span data-stu-id="9ad6d-112">Re-running the extension on the VM</span></span>
<span data-ttu-id="9ad6d-113">Özel betik uzantısının kullanarak VM betikleri çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak komut başarısız oldu bir hatayla bazen çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-113">If you are running scripts on the VM using Custom Script Extension, you could sometimes run into an error where VM was created successfully but the script has failed.</span></span> <span data-ttu-id="9ad6d-114">Bu conditons altında bu hatadan kurtarmak için önerilen uzantıyı kaldırmak ve şablonu yeniden çalıştırın yoldur.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-114">Under these conditons, the recommended way to recover from this error is to remove the extension and rerun the template again.</span></span>
<span data-ttu-id="9ad6d-115">Not: ileride bu işlevselliği uzantısını kaldırma gereksinimini kaldırmak için Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-115">Note: In future, this functionality would be enhanced to remove the need for uninstalling the extension.</span></span>

#### <a name="remove-the-extension-from-azure-powershell"></a><span data-ttu-id="9ad6d-116">Azure PowerShell uzantısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="9ad6d-116">Remove the extension from Azure PowerShell</span></span>
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

<span data-ttu-id="9ad6d-117">Uzantı kaldırıldıktan sonra şablonu VM komut dosyalarını çalıştırmak için yeniden yürütülen olabilir.</span><span class="sxs-lookup"><span data-stu-id="9ad6d-117">Once the extension has been removed, the template can be re-executed to run the scripts on the VM.</span></span>

