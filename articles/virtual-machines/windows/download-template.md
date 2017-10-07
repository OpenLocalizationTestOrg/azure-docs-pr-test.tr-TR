---
title: "bir Azure VM için aaaDownload hello şablonu | Microsoft Docs"
description: "Merhaba templatefor hello Resource Manager dağıtım modeli dağıtımlarda otomatikleştirmede VM toohelp indirin"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a>Bir VM için Hello şablonunu yükle
Azure'da VM oluşturduğunuzda hello portalı veya bir Resource Manager PowerShell kullanarak şablonu otomatik olarak sizin için oluşturulur. Bu şablon tooquickly yinelenen bir dağıtım kullanabilirsiniz. Merhaba şablonu bir kaynak grubunda hello kaynakların tümünü hakkında bilgiler içerir. Bir sanal makine için bu hello şablonu hello VM hello ağ kaynaklarını dahil olmak üzere bu kaynak grubundaki desteklenmesi amacıyla oluşturulan her şeyi içeren anlamına gelir.

## <a name="download-hello-template-using-hello-portal"></a>Merhaba portal kullanarak hello şablonunu yükle
1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Bir hello hub menüsünde, select **sanal makineleri**.
3. Merhaba sanal makine hello listeden seçin.
4. Seçin **Otomasyon betiğini**.
5. Seçin **karşıdan** ve hello .zip dosya tooyour yerel bilgisayara kaydedin.
6. Merhaba .zip dosyasını açın ve hello dosyaları tooa klasörüne ayıklayın. Merhaba .zip dosyası içerir:
   
   * Deploy.ps1
   * Deploy.sh 
   * deployer.RB
   * DeploymentHelper.cs
   * Parameters.JSON
   * Template.JSON

Merhaba template.json dosyasını hello şablonudur.

## <a name="download-hello-template-using-powershell"></a>PowerShell kullanarak hello şablonunu yükle
Ayrıca hello kullanarak hello .json şablon dosyası indirebilirsiniz [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet'i. Merhaba kullanabilirsiniz `-path` tooprovide hello filename parametresi ve hello .json dosyası için yol. Bu örnek nasıl hello kaynak grubu için toodownload hello şablonu adlı gösterir **myResourceGroup** toohello **C:\users\public\downloads** klasör, yerel bilgisayarınızda.

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a>Sonraki adımlar
şablonları kullanarak kaynakları dağıtma hakkında daha fazla toolearn bkz [Resource Manager şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md).

