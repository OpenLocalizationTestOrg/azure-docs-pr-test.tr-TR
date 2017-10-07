---
title: "aaaResize hello Klasik dağıtım modelinde - Azure Windows VM | Microsoft Docs"
description: "Azure Powershell kullanarak hello Klasik dağıtım modelinde oluşturulmuş bir Windows sanal makine yeniden boyutlandırın."
services: virtual-machines-windows
documentationcenter: 
author: Drewm3
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e3038215-001c-406e-904d-e0f4e326a4c7
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 10/19/2016
ms.author: drewm
ms.openlocfilehash: 39fab14431e2351c9515b0611e850eccfec7a798
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-windows-vm-created-in-hello-classic-deployment-model"></a>Windows hello Klasik dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın
Bu makalede nasıl tooresize bir Windows VM oluşturulan Azure Powershell kullanarak hello Klasik dağıtım modelinde gösterilmektedir.

Merhaba özelliği tooresize VM değerlendirirken denetlemenize hello boyutları kullanılabilir tooresize hello sanal makine iki kavram vardır. Merhaba ilk kavram, VM dağıtıldığı hello bölgedir. Merhaba bölgede kullanılabilir VM boyutları hello Hizmetleri sekmesinde hello Azure bölgeleri web sayfasının altında listesidir. Merhaba ikinci hello fiziksel donanım şu anda, VM barındırma kavramdır. sanal makineleri barındıran hello fiziksel sunucuları ortak fiziksel donanım kümelerde birlikte gruplandırılır. Merhaba istenen yeni VM boyutu şu anda hello VM barındırma hello donanım küme tarafından desteklenip desteklenmediğini VM boyutunu değiştirme hello yöntemi bağlı olarak farklılık gösterir.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Ayrıca [hello Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="add-your-account"></a>Hesabınızı ekleme
Klasik Azure kaynakları ile Azure PowerShell toowork yapılandırmanız gerekir. Tooconfigure Azure PowerShell toomanage Klasik kaynakları Hello adımları izleyin.

1. Merhaba PowerShell isteminde `Add-AzureAccount` tıklatıp **Enter**. 
2. Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**. 
3. Merhaba hesabınızın parolasını yazın. 
4. Tıklatın **oturum**. 

## <a name="resize-in-hello-same-hardware-cluster"></a>Hello aynı yeniden boyutlandırma donanım küme
tooresize hello VM, barındırma hello donanım kümede kullanılabilir VM tooa boyutunu hello aşağıdaki adımları gerçekleştirin.

1. Aşağıdaki PowerShell komutunu toolist hello VM boyutlarını içeren hello bulut hizmetini barındıran hello donanım kümede kullanılabilir VM hello hello çalıştırın.
   
    ```powershell
    Get-AzureService | where {$_.ServiceName -eq "<cloudServiceName>"}
    ```
2. Aşağıdaki komutları tooresize hello VM hello çalıştırın.
   
    ```powershell
    Get-AzureVM -ServiceName <cloudServiceName> -Name <vmName> | Set-AzureVMSize -InstanceSize <newVMSize> | Update-AzureVM
    ```

## <a name="resize-on-a-new-hardware-cluster"></a>Yeni bir donanım kümede yeniden boyutlandırma
tooresize VM tooa boyut hello donanım küme barındırma kullanılamıyor Merhaba VM, hello bulut hizmeti ve hello bulut hizmetindeki tüm sanal makineleri yeniden oluşturulmalıdır. Merhaba bulut hizmetindeki tüm sanal makineleri bir donanım kümesine desteklenen bir boyutta olması gerekir böylece her bir bulut hizmeti bir tek bir donanım kümesine barındırılır. Merhaba aşağıdaki adımları nasıl tooresize VM silerek ve sonra yeniden hello bulut anlatmaktadır hizmet.

1. PowerShell komut toolist hello VM boyutları kullanılabilir hello bölgede aşağıdaki hello çalıştırın. 
   
    ```powershell
    Get-AzureLocation | where {$_.Name -eq "<locationName>"}
    ```
2. Yeniden boyutlandırılabilir hello VM toobe içeren hello bulut hizmetinde her VM için tüm yapılandırma ayarlarını not edin. 
3. Her VM için hello seçeneği tooretain hello diskleri seçerek hello bulut hizmetindeki tüm sanal makineleri silin.
4. Merhaba istenen VM boyutu kullanarak yeniden boyutlandırılabilir hello VM toobe yeniden oluşturun.
5. Şimdi hello bulut hizmetini barındıran hello donanım kümede bir VM boyutu kullanarak hello bulut hizmeti olan diğer tüm VM'ler yeniden oluşturun.

Silme ve yeni bir VM boyutu kullanarak bir bulut hizmeti yeniden oluşturmak için örnek betik bulunabilir [burada](https://github.com/Azure/azure-vm-scripts). 

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba Resource Manager dağıtım modelinde oluşturulan bir VM'yi yeniden boyutlandırın](../resize-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

