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
# <a name="troubleshooting-azure-linux-vm-extension-failures"></a>Azure Linux VM uzantısı hataları sorunlarını giderme
[!INCLUDE [virtual-machines-common-extensions-troubleshoot](../../../includes/virtual-machines-common-extensions-troubleshoot.md)]

## <a name="viewing-extension-status"></a>Uzantı durumunu görüntüleme
Azure Resource Manager şablonları hello Azure CLI ' çalıştırılabilir. Merhaba şablon yürütüldükten sonra Azure kaynak Gezgini veya hello komut satırı araçları'ndan hello uzantı durumunu görüntülenebilir.

Örnek aşağıda verilmiştir:

Azure CLI:

      azure vm get-instance-view


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

## <a name="troubleshooting-extenson-failures"></a>Extenson hataları sorunlarını giderme:
### <a name="re-running-hello-extension-on-hello-vm"></a>Merhaba VM yeniden çalıştırarak hello uzantısı
Komut dosyaları hello özel betik uzantısının kullanarak VM üzerinde çalıştırıyorsanız, burada VM başarıyla oluşturuldu, ancak hello komut başarısız oldu bir hatayla bazen çalıştırabilir. Bu conditons altında bu hatadan yolu toorecover önerilen hello tooremove hello uzantısıdır ve hello şablonu yeniden çalıştırın.
Not: gelecekte Gelişmiş tooremove bu işlevselliği olacaktır hello gerek hello uzantısı kaldırmak için.

#### <a name="remove-hello-extension-from-azure-cli"></a>Azure CLI üzerinden Hello uzantısını kaldırma
      azure vm extension set --resource-group "KPRG1" --vm-name "kundanapdemo" --publisher-name "Microsoft.Compute.CustomScriptExtension" --name "myCustomScriptExtension" --version 1.4 --uninstall

Burada "publsher-name" karşılık gelen "azure vm get-örnek-Görünüm" Merhaba çıktısından toohello uzantısı türü ve hello adıdır hello şablondan hello uzantısı kaynağının adı

Merhaba uzantısı kaldırıldıktan sonra hello şablon hello VM yeniden yürütülen toorun hello komut olabilir.

