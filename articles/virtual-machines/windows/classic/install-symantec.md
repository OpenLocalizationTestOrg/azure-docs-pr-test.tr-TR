---
title: "aaaInstall Azure Windows VM üzerinde Symantec Endpoint Protection | Microsoft Docs"
description: "Bilgi nasıl tooinstall hello Symantec Endpoint Protection güvenlik uzantısı yeni yapılandırma ve mevcut Azure VM hello Klasik dağıtım modeliyle oluşturulan."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>Nasıl tooinstall ve Symantec Endpoint Protection bir Windows VM yapılandırma
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Bu makale size nasıl gösterir tooinstall hello Symantec Endpoint Protection istemci ve var olan sanal Windows Server çalıştıran bir makineyi (VM) yapılandırın. Bu tam istemci virüs ve casus yazılımdan koruma, güvenlik duvarı ve izinsiz giriş önleme gibi hizmetleri içerir. Merhaba istemci hello VM Aracısı'nı kullanarak bir güvenlik uzantısı olarak yüklenir.

Symantec'ten bir şirket içi çözüm için mevcut bir aboneliğiniz varsa, tooprotect kullanabilirsiniz, Azure sanal makineler. Bir müşteri henüz değilseniz, deneme aboneliği için kaydolabilirsiniz. Bu çözüm hakkında daha fazla bilgi için bkz: [Symantec Endpoint Protection Microsoft'un Azure platformunda][Symantec]. Bu sayfa ayrıca bağlantı toolicensing bilgileri ve Symantec müşteri zaten iseniz hello istemcisini yüklemeye yönelik yönergeleri sahiptir.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Var olan bir VM Symantec Endpoint Protection yükle
Başlamadan önce hello aşağıdaki gerekir:

* Hello Azure PowerShell modülü, sürüm 0.8.2 veya daha sonra iş bilgisayarınızın. Merhaba ile yüklediğiniz Azure PowerShell hello sürümü kontrol edebilirsiniz **Get-Module azure | Tablo Biçimlendir sürüm** komutu. Yönergeler ve bir bağlantı toohello en son sürüm için bkz: [nasıl tooInstall ve yapılandırma Azure PowerShell][PS]. Azure aboneliği tooyour kullanarak oturum `Add-AzureAccount`.
* Merhaba VM üzerinde çalışan Aracısı hello Azure sanal makine.

İlk olarak, VM aracısının hello sanal makinede zaten yüklü olduğundan bu hello doğrulayın. Merhaba bulut hizmeti adı ve sanal makine adı girin ve ardından komutlar bir yönetici düzeyi Azure PowerShell komut isteminde aşağıdaki hello çalıştırın. Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi değiştirin.

> [!TIP]
> Merhaba bulut hizmeti ve sanal makine adları bilmiyorsanız, çalıştırmak **Get-AzureVM** toolist hello adları geçerli aboneliğinizde tüm sanal makineler için.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Merhaba, **write-host** komutu görüntüler **doğru**, VM aracısının yüklü hello. Bunu görüntülerse **False**, hello yönergeler ve hello Azure blog gönderisi indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça][Agent].

Merhaba VM Aracısı yüklüyse, bu komutları tooinstall hello Symantec Endpoint Protection Aracısı'nı çalıştırın.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

Symantec güvenlik uzantısı hello tooverify yüklü ve güncel durumda:

1. Toohello sanal makinede oturum açın. Yönergeler için bkz: [nasıl tooa sanal makine çalıştıran Windows Server üzerinde tooLog][Logon].
2. Windows Server 2008 R2 için tıklatın **Başlat > Symantec Endpoint Protection**. Windows Server 2012 veya hello başlangıç ekranından Windows Server 2012 R2 için yazın **Symantec**ve ardından **Symantec Endpoint Protection**.
3. Merhaba gelen **durum** hello sekmesinde **durum Symantec Endpoint Protection** penceresinde, güncelleştirmeleri uygulamak veya gerektiğinde yeniden başlatın.

## <a name="additional-resources"></a>Ek kaynaklar
[Nasıl tooLog tooa sanal makine çalıştıran Windows Server üzerinde][Logon]

[Azure VM uzantıları ve özellikleri][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
