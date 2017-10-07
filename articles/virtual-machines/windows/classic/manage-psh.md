---
title: aaaManage Azure PowerShell kullanarak sanal makinelerinizin | Microsoft Docs
description: "Sanal makinelerinizi yönetme tooautomate görevleri kullanabileceğiniz komutlar hakkında bilgi edinin."
services: virtual-machines-windows
documentationcenter: windows
author: singhkays
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 7cdf9bd3-6578-4069-8a95-e8585f04a394
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 10/12/2016
ms.author: kasing
ms.openlocfilehash: e4ca6f098519243a321eac98b6692790fe18c22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-virtual-machines-by-using-azure-powershell"></a>Azure PowerShell kullanarak sanal makinelerinizi yönetme
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Merhaba Resource Manager modelini kullanarak ortak PowerShell komutları için bkz: [burada](../../virtual-machines-windows-ps-common-ref.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Birçok görevi her gün toomanage Vm'leriniz bunu Azure PowerShell cmdlet'lerini kullanarak otomatik olarak. Bu makalede daha basit görevler ve daha karmaşık görevleri için hello komutları göster bağlantılar tooarticles için örnek komutlar verir.

> [!NOTE]
> Azure PowerShell'i yükleyip henüz henüz hello makaledeki yönergeleri alabilir, [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
> 
> 

## <a name="how-toouse-hello-example-commands"></a>Nasıl toouse hello örnek komutları
Merhaba hello metinde bazıları komutları ortamınız için uygun metinle tooreplace gerekir. Merhaba < ve > sembolleri tooreplace gereksinim metin gösterir. Merhaba metin değiştirdiğinizde hello simgeleri Kaldır ancak hello tırnak işaretleri bırakın.

## <a name="get-a-vm"></a>VM Al
Bu, genellikle kullanacağınız temel bir görevdir. VM tooget bilgilerini kullanmak, bir VM görevler gerçekleştiren veya çıktı toostore bir değişkende alın.

Merhaba VM tooget bilgilerini hello tırnak merhaba < ve > karakterleri dahil olmak üzere, her şeyi değiştirerek bu komutu çalıştırın:

     Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

bir $vm değişkende çıktı toostore hello çalıştırın:

    $vm = Get-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="log-on-tooa-windows-based-vm"></a>Windows tabanlı VM üzerinde tooa oturum
Şu komutları çalıştırın:

> [!NOTE]
> Merhaba hello görüntüden hello sanal makine ve bulut hizmeti adı alabilirsiniz **Get-AzureVM** komutu.
> 
> $svcName = "<cloud service name>" $vmName = "<virtual machine name>" $localPath = "< sürücü ve klasör konumu toostore indirilen hello RDP dosyası, örneğin: c:\temp >" $localFile $localPath = + "\" $vmname +".rdp"Get-AzureRemoteDesktopFile - ServiceName $svcName-$vmName - LocalPath $localFile ad-Başlat
> 
> 

## <a name="stop-a-vm"></a>VM durdurma
Şu komutu çalıştırın:

    Stop-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

> [!IMPORTANT]
> Sanal IP (VIP) hello bulut hizmeti olduğu durumda bu parametre tookeep hello kullanmak son VM bu bulut hizmeti ile Merhaba. <br><br> Merhaba StayProvisioned parametreyi kullanırsanız, VM hello için fatura.
> 
> 

## <a name="start-a-vm"></a>VM başlatma
Şu komutu çalıştırın:

    Start-AzureVM -ServiceName "<cloud service name>" -Name "<virtual machine name>"

## <a name="attach-a-data-disk"></a>Veri diski ekleme
Bu görev birkaç adımı gerektirir. Merhaba ilk olarak, kullandığınız *** Ekle-AzureDataDisk *** cmdlet tooadd hello disk toohello $vm nesnesi. Ardından, kullandığınız **güncelleştirme-AzureVM** hello VM cmdlet tooupdate hello yapılandırması.

Ayrıca tooattach yeni bir disk veya bir içeren olup olmadığını toodecide gerekir veri. Yeni bir disk için hello komut hello .vhd dosyası oluşturur ve bunları ekler.

Yeni bir disk tooattach bu komutu çalıştırın:

    Add-AzureDataDisk -CreateNew -DiskSizeInGB 128 -DiskLabel "<main>" -LUN <0> -VM $vm | Update-AzureVM

Varolan bir veri diski tooattach bu komutu çalıştırın:

    Add-AzureDataDisk -Import -DiskName "<MyExistingDisk>" -LUN <0> | Update-AzureVM

var olan .vhd dosyasına blob storage'da tooattach veri disklerinden bu komutu çalıştırın:

    Add-AzureDataDisk -ImportFrom -MediaLocation `
              "<https://mystorage.blob.core.windows.net/mycontainer/MyExistingDisk.vhd>" `
              -DiskLabel "<main>" -LUN <0> |
              Update-AzureVM

## <a name="create-a-windows-based-vm"></a>Windows tabanlı bir VM oluşturma
toocreate yeni bir Windows tabanlı sanal makine azure'da kullanım hello yönergeleri [Azure PowerShell kullanma toocreate ve Windows tabanlı sanal makineleri önceden](create-powershell.md). Bu konuda adım adım komut kümesi bir Azure PowerShell hello oluşturulmasını size önceden yapılandırılabilir Windows tabanlı bir VM oluşturur:

* Active Directory etki alanı üyeliği ile.
* Ek disklerle.
* Varolan yük dengeli bir üye olarak ayarlayın.
* Statik bir IP adresine sahip.

