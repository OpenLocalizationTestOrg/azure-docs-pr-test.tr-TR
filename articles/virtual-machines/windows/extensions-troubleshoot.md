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
# <a name="troubleshooting-azure-windows-vm-extension-failures"></a>Azure Windows VM uzantısı hataları sorunlarını giderme
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Uzantı durumunu görüntüleme
Azure Resource Manager şablonları Azure Powershell'den çalıştırılabilir. Merhaba şablon yürütüldükten sonra Azure kaynak Gezgini veya hello komut satırı araçları'ndan hello uzantı durumunu görüntülenebilir.

Örnek aşağıda verilmiştir:

Azure PowerShell:

      Get-AzureRmVM -ResourceGroupName $RGName -Name $vmName -Status

Merhaba örnek çıktı aşağıda verilmiştir:

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
  ]

## <a name="troubleshooting-extension-failures"></a>Uzantı hataları sorunlarını giderme
### <a name="re-running-hello-extension-on-hello-vm"></a>Merhaba VM yeniden çalıştırarak hello uzantısı
Komut dosyaları hello özel betik uzantısının kullanarak VM üzerinde çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak hello komut başarısız oldu bir hatayla bazen çalıştırabilir. Bu conditons altında bu hatadan yolu toorecover önerilen hello tooremove hello uzantısıdır ve hello şablonu yeniden çalıştırın.
Not: gelecekte Gelişmiş tooremove bu işlevselliği olacaktır hello gerek hello uzantısı kaldırmak için.

#### <a name="remove-hello-extension-from-azure-powershell"></a>Azure PowerShell Hello uzantısını kaldırma
    Remove-AzureRmVMExtension -ResourceGroupName $RGName -VMName $vmName -Name "myCustomScriptExtension"

Merhaba uzantısı kaldırıldıktan sonra hello şablon hello VM yeniden yürütülen toorun hello komut olabilir.

