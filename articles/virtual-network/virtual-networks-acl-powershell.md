---
title: "aaaManage Azure uç noktası erişim denetim listeleri | PowerShell | Klasik | Microsoft Docs"
description: "Bilgi nasıl toomanage PowerShell ile ACL"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a>Uç noktası erişim denetim listeleri hello Klasik dağıtım modelinde PowerShell kullanarak yönetme
Oluşturun ve ağ erişim denetimi listeleri (ACL'ler) uç noktaları için Azure PowerShell kullanarak veya hello Yönetim Portalı yönetin. Bu konuda, PowerShell kullanarak tamamlayabilirsiniz ACL ortak görevler için yordamlar bulabilirsiniz. Cmdlet'leri Azure PowerShell Hello listesi için bkz [Azure Yönetimi cmdlet'leri](http://go.microsoft.com/fwlink/?LinkId=317721). ACL'ler hakkında daha fazla bilgi için bkz: [bir ağ erişim denetimi listesi (ACL) nedir?](virtual-networks-acl.md). Hello yönetim portalını kullanarak, ACL'ler toomanage istiyorsanız, bkz: [nasıl tooSet yukarı uç noktaları tooa sanal makine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="manage-network-acls-by-using-azure-powershell"></a>Ağ ACL'leri Azure PowerShell kullanarak yönetme
Azure PowerShell cmdlet'leri toocreate kullanabileceğiniz kaldırın ve yapılandırın (küme) ağ erişimi denetim listeleri (ACL'ler). Biz, PowerShell kullanarak bir ACL yapılandırmak hello yollardan bazılarını birkaç örnekleri dahil ettiğiniz.

tooretrieve hello ACL PowerShell cmdlet'lerinin tam bir listesi, hello aşağıdakilerden herhangi birini kullanabilirsiniz:

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a>Uzak bir alt ağ üzerinden erişime kurallarla ağ ACL oluşturma
Merhaba örneği aşağıdaki şekilde toocreate kuralları içeren yeni bir ACL gösterilmektedir. Bu ACL sonra uygulanan tooa sanal makine uç noktası. Aşağıdaki hello örnek Hello ACL kuralları, uzak bir alt ağdan erişimi izin verir. Uzak bir alt ağ için toocreate izin ile yeni bir ağ ACL kuralları bir Azure PowerShell ISE açın. Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.

1. Merhaba yeni ağ ACL nesnesi oluşturun.
   
        $acl1 = New-AzureAclConfig
2. Uzak bir alt ağdan erişimi veren bir kural kümesi. Merhaba aşağıdaki örnekte, kural kümesi *100* (olan öncelik kuralına göre 200 ve üzeri) tooallow hello uzak alt *10.0.0.0/8* toohello sanal makine uç noktası erişim. Merhaba değerleri kendi yapılandırma gereksinimlerine göre değiştirin. Merhaba adı "SharePoint ACL yapılandırma" Merhaba kolay adı bu kuralın toocall istediğiniz ile değiştirilmelidir.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. Ek kurallar için kendi yapılandırma gereksinimlerine göre hello değerleri değiştirerek hello cmdlet'ini tekrarlayın. Uygulanan hello kuralları toobe istediğiniz emin toochange hello kuralı numara tooreflect hello sipariş olması. Merhaba alt kural numarası daha büyük bir sayı hello önceliklidir.
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. Ardından, yeni bir uç noktası (Ekle) oluşturmak veya mevcut bir uç noktası (küme) için ACL hello ayarlayın. Bu örnekte, yeni bir sanal makine uç noktası güncelleştirmesi ile "web" Merhaba sanal makine uç noktası ile Merhaba ACL ayarları adlı ekleyeceğiz.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. Ardından, hello cmdlet'leri birleştirmek ve hello komut dosyasını çalıştırın. Bu örnekte, hello birleşik cmdlet'leri şöyle olabilir:
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a>Uzak bir alt ağdan erişimi veren bir ağ ACL kuralını Kaldır
Merhaba örneği aşağıdaki şekilde tooremove ağ ACL kuralı gösterilmektedir.  tooremove izin ile ağ ACL kuralı için bir uzak alt ağ, kuralları bir Azure PowerShell ISE açın. Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.

1. Tooget hello ağ ACL nesne hello sanal makine uç noktası için ilk adımdır. Ardından hello ACL kuralı kaldırırsınız. Bu durumda, biz bu kural kimliğine göre kaldırıyorsunuz Bu gibi durumlarda bu hello kural kimliği 0 yalnızca hello ACL ' kaldırır. Merhaba ACL nesne hello sanal makine uç noktasından kaldırmaz.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. Ardından, hello ağ ACL nesne toohello sanal makine uç noktası uygulamak ve hello sanal makine güncelleştirin.
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a>Bir sanal makine uç noktasından bir ağ ACL Kaldır
Bazı senaryolarda, bir sanal makine uç noktası bir ağ ACL nesneden tooremove isteyebilirsiniz. bir Azure PowerShell ISE açın, toodo. Kopyalama ve aşağıda kendi değerlerinizle hello komut dosyasını yapılandırarak hello betiğini yapıştırın ve hello betiğini çalıştırın.

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a>Sonraki adımlar
[Bir ağ erişim denetimi listesi (ACL) nedir?](virtual-networks-acl.md)

