---
title: "aaaAzure sanal makine Aracısı genel bakış | Microsoft Docs"
description: "Azure sanal makine Aracısı genel bakış"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 0a1f212e-053e-4a39-9910-8d622959f594
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 178766925673419cd661dbb460b8427bbfaf54e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-agent-overview"></a>Azure sanal makine aracısını genel bakış

Merhaba Microsoft Azure sanal makine Aracısı (VM Aracısı) hello Azure yapı denetleyicisi VM etkileşim yöneten güvenli ve basit bir işlemdir. Merhaba VM Aracısı etkinleştirme ve Azure sanal makine uzantıları yürütme birincil bir rolü var. VM uzantıları etkinleştirme, yükleme ve yazılım yapılandırma gibi sanal makine dağıtım yapılandırması gönderin. Sanal makine uzantıları gibi bir sanal makinenin hello yönetici parolasını sıfırlama kurtarma özellikleri de sağlar. Azure VM Aracısı Hello, sanal makine uzantıları çalıştırılamaz.

Bu belge yükleme, algılama ve hello Azure sanal makine Aracısı kaldırılmasını ayrıntıları.

## <a name="install-hello-vm-agent"></a>Merhaba VM Aracısı yükleme

### <a name="azure-gallery-image"></a>Azure galeri görüntüsü

Hello Azure VM Aracısı, Azure Galerisi görüntüden dağıtılmış tüm Windows sanal makine üzerinde varsayılan olarak yüklenir. Azure galerisinde görüntüden hello Portal, PowerShell, komut satırı arabirimini veya bir Azure Resource Manager şablonu dağıtırken de Azure VM Aracısı olduğunu hello yüklenmesi. 

### <a name="manual-installation"></a>El ile yükleme

Merhaba Windows VM Aracısı el ile bir Windows Installer paketi kullanılarak yüklenebilir. Bir özel sanal makine görüntüsü oluşturma Azure'da dağıtılacak zaman el ile yükleme gerekli olabilir. toomanually yükleme hello Windows VM Aracısı, bu konumdan hello VM Aracısı yükleyicisi karşıdan [Windows Azure VM Aracısı indirme](http://go.microsoft.com/fwlink/?LinkID=394789). 

Merhaba VM Aracısı hello windows Installer dosyasını çift tıklatarak yüklenebilir. Bir otomatik olarak veya katılımsız yükleme hello VM Aracısı'nın için komutu aşağıdaki hello çalıştırın.

```cmd
msiexec.exe /i WindowsAzureVmAgent.2.7.1198.778.rd_art_stable.160617-1120.fre /quiet
```

## <a name="detect-hello-vm-agent"></a>Merhaba VM Aracısı Algıla

### <a name="powershell"></a>PowerShell

Hello Azure Resource Manager PowerShell modülü kullanılan tooretrieve bilgiler hakkında Azure sanal makineler olabilir. Çalışan `Get-AzureRmVM` oldukça biraz sağlama durumu hello Azure VM aracısı için hello bilgilerini döndürür.

```PowerShell
Get-AzureRmVM
```

Merhaba yalnızca bir alt kümesini hello aşağıdadır `Get-AzureRmVM` çıktı. Bildirim hello `ProvisionVMAgent` içe özelliği içinde `OSProfile`, bu özellik, dağıtılan toohello sanal makine hello VM Aracısı yüklediyse kullanılan toodetermine olabilir.

```PowerShell
OSProfile                  :
  ComputerName             : myVM
  AdminUsername            : muUserName
  WindowsConfiguration     :
    ProvisionVMAgent       : True
    EnableAutomaticUpdates : True
```

komut dosyası izleyen hello kullanılan tooreturn sanal makine adları ve hello VM Aracısı hello durumunu kısa listesini olabilir.

```PowerShell
$vms = Get-AzureRmVM

foreach ($vm in $vms) {
    $agent = $vm | Select -ExpandProperty OSProfile | Select -ExpandProperty Windowsconfiguration | Select ProvisionVMAgent
    Write-Host $vm.Name $agent.ProvisionVMAgent
}
```

### <a name="manual-detection"></a>El ile algılama

Tooa Windows Azure VM oturum açıldığında, Görev Yöneticisi'ni çalışan işlemlerin kullanılan tooexamine olabilir. toocheck hello Azure VM aracısı için Görev Yöneticisi'ni açın > merhaba Ayrıntılar sekmesini tıklatın ve bir işlem adı arayın `WindowsAzureGuestAgent.exe`. Bu işlemin Hello varlığı bu hello VM aracısının yüklü olduğunu gösterir.

## <a name="upgrade-hello-vm-agent"></a>Yükseltme hello VM Aracısı

Hello Azure VM Aracısı Windows'için otomatik olarak yükseltilir. Yeni sanal makineler dağıtılan tooAzure olduğu gibi hello son VM Aracısı alırlar. Özel VM görüntüleri manuel olarak güncelleştirilen tooinclude hello yeni VM Aracısı olmalıdır.
