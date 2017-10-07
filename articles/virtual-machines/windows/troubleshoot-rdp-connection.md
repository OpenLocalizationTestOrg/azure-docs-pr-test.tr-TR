---
title: "aaaCannot bağlantı RDP tooa Azure Windows VM ile | Microsoft Docs"
description: "Uzak Masaüstü'nü kullanarak azure'daki tooyour Windows sanal makine bağlanamadığında sorunlarını giderme"
keywords: "Uzak Masaüstü hata, Uzak Masaüstü Bağlantısı hatası tooVM, bağlanamıyor Uzak Masaüstü sorunlarını giderme"
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: 0d740f8e-98b8-4e55-bb02-520f604f5b18
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: support-article
ms.date: 07/25/2017
ms.author: genli
ms.openlocfilehash: bbb36136e7a4b187fe8deea621d2b8d46d8aa102
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-remote-desktop-connections-tooan-azure-virtual-machine"></a>Uzak Masaüstü bağlantıları tooan Azure sanal makine sorunlarını giderme
Merhaba Uzak Masaüstü Protokolü (RDP) bağlantısı tooyour Windows tabanlı Azure sanal makine (VM), VM oluşturulamıyor tooaccess bırakarak çeşitli nedenlerle başarısız olabilir. Merhaba hello VM, hello ağ bağlantısı veya hello Uzak Masaüstü İstemcisi ana bilgisayarınızda Uzak Masaüstü hizmeti ile Merhaba sorun olabilir. Bu makalede, bazı hello en yaygın yöntemleri tooresolve RDP bağlantı sorunlarını size yol gösterir. 

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) seçip **alma desteği**.

<a id="quickfixrdp"></a>

## <a name="quick-troubleshooting-steps"></a>Hızlı sorun giderme adımları
Sorun giderme her adımdan sonra toohello VM yeniden bağlanmayı deneyin:

1. Uzak Masaüstü yapılandırmasının sıfırlayın.
2. Ağ güvenlik grubu denetleme kuralları / bulut Hizmetleri uç noktaları.
3. VM Konsolu günlüklerini gözden geçirin.
4. Merhaba NIC hello VM sıfırlayın.
5. Merhaba VM kaynak durumu denetleyin.
6. VM parolanızı sıfırlayın.
7. VM'yi yeniden başlatın.
8. VM'yi yeniden dağıtın.

Ayrıntılı adımları ve açıklamalar gerekiyorsa okuma devam edin. Bu yerel ağ ekipmanları yönlendiriciler gibi doğrulayın ve güvenlik duvarları engellemediğini giden TCP bağlantı noktası 3389, içinde belirtildiği gibi [sorun giderme senaryoları RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!TIP]
> Merhaba, **Bağlan** VM'yi kapatma hello Portalı'nda gri ve aracılığıyla bağlı tooAzure olmayan düğmesini bir [hızlı rota](../../expressroute/expressroute-introduction.md) veya [siteden siteye VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) bağlantısı gerekir toocreate ve VM'nize genel bir IP adresi önce Ata RDP kullanabilirsiniz. [Azure’da genel IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) hakkında daha fazlasını okuyabilirsiniz.


## <a name="ways-tootroubleshoot-rdp-issues"></a>RDP yolları tootroubleshoot sorunları
Yöntemler aşağıdaki hello birini kullanarak hello Resource Manager dağıtım modeli kullanılarak oluşturulan sanal makineleri giderebilirsiniz:

* [Azure portal](#using-the-azure-portal) - tooquickly gerekiyorsa mükemmel hello RDP yapılandırması veya kullanıcı kimlik bilgilerini sıfırlama ve, yok sahip hello Azure Araçları yüklü.
* [Azure PowerShell](#using-azure-powershell) -, hızlı bir şekilde hello Azure PowerShell cmdlet'lerini kullanarak sıfırlama hello RDP yapılandırması veya kullanıcı kimlik bilgilerini bir PowerShell İstemi ile kullanabiliyorsanız.

Merhaba kullanılarak oluşturulan sanal makineleri sorun giderme adımları bulabileceğiniz [Klasik dağıtım modeli](#troubleshoot-vms-created-using-the-classic-deployment-model).

<a id="fix-common-remote-desktop-errors"></a>

## <a name="troubleshoot-using-hello-azure-portal"></a>Hello Azure portal kullanarak sorun giderme
Sorun giderme her adımdan sonra tooyour VM yeniden bağlanmayı deneyin. Hala bağlanamıyorsanız, sonraki adıma hello deneyin.

1. **RDP bağlantınızı sıfırlama**. Sorun giderme Bu adım, uzak bağlantıları devre dışı bırakıldığında veya Windows Güvenlik duvarı kurallarını RDP, örneğin engelliyor hello RDP yapılandırmasını sıfırlar.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **parola sıfırlama** düğmesi. Set hello **modu** çok**yalnızca sıfırlama yapılandırma** ve hello ardından **güncelleştirme** düğmesi:
   
    ![Merhaba RDP hello Azure portal yapılandırmasında Sıfırla](./media/troubleshoot-rdp-connection/reset-rdp.png)
2. **Doğrulama ağ güvenlik grubu kuralları**. Kullanım [IP akış doğrulayın](../../network-watcher/network-watcher-check-ip-flow-verify-portal.md) trafiği tooor bir sanal makineden bir ağ güvenlik grubu kural engelliyorsa tooconfirm. Ayrıca, etkin güvenlik grubu kuralları tooensure gelen "NSG izin ver" kuralı var ve RDP bağlantı noktası (varsayılan 3389) öncelik gözden geçirebilirsiniz. Daha fazla bilgi için bkz: [kullanarak etkili güvenlik kuralları tootroubleshoot VM trafiğinin akmasını](../../virtual-network/virtual-network-nsg-troubleshoot-portal.md#using-effective-security-rules-to-troubleshoot-vm-traffic-flow).

3. **VM önyükleme tanılaması gözden**. Merhaba VM bir sorun raporlama söz konusu ise bu sorun giderme adımı hello VM konsol günlükleri toodetermine inceler. Tüm sanal makineleri önyükleme tanılaması etkin, sahip, bu nedenle sorun giderme Bu adım isteğe bağlı olabilir.
   
    Özel sorun giderme adımları hello bu makalenin kapsamı dışındadır, ancak RDP bağlantı etkileyen daha geniş bir sorunu gösterebilir. Merhaba konsol günlükleri ve VM ekran görüntüsünü gözden geçirme hakkında daha fazla bilgi için bkz: [VM'ler için önyükleme tanılaması](boot-diagnostics.md).

4. **Merhaba VM için sıfırlama hello NIC**. Daha fazla bilgi için bkz: [nasıl tooreset Azure Windows VM için NIC](reset-network-interface.md).
5. **Merhaba VM kaynak durumu denetleme**. Bu sorun giderme adımı hello bağlantı toohello VM etkileyebilir Azure platformu ile bilinen bir sorun doğrular.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **kaynak durumu** düğmesi. Sağlıklı bir VM raporları olarak **kullanılabilir**:
   
    ![VM kaynak durumu hello Azure portal denetleyin](./media/troubleshoot-rdp-connection/check-resource-health.png)
6. **Kullanıcı kimlik bilgilerini sıfırlama**. Emin değilseniz veya hello kimlik unutmuş Bu sorun giderme adımı bir yerel yönetici hesabına hello parolasını sıfırlar.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **parola sıfırlama** düğmesi. Merhaba emin olun **modu** çok ayarlanır**parola sıfırlama** ve kullanıcı adınızı ve yeni bir parola girin. Son olarak, hello tıklatın **güncelleştirme** düğmesi:
   
    ![Hello Azure portal Hello kullanıcı kimlik bilgilerini sıfırlama](./media/troubleshoot-rdp-connection/reset-password.png)
7. **VM'yi yeniden**. Bu sorun giderme adımı temel sorunları düzeltebilir hello VM kendisini sahip.
   
    Hello Azure portal, VM seçin ve hello tıklatın **genel bakış** sekmesi. Merhaba tıklatın **yeniden** düğmesi:
   
    ![Merhaba VM hello Azure portalında yeniden başlatın](./media/troubleshoot-rdp-connection/restart-vm.png)
8. **VM'yi yeniden**. Bu sorun giderme adımı Azure toocorrect içinde VM tooanother konağınız temel platform ya da ağ sorunları yeniden dağıtır.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **dağıtmanız** düğmesine tıklayın ve ardından **dağıtmanız**:
   
    ![Hello VM hello Azure portalında yeniden dağıtın](./media/troubleshoot-rdp-connection/redeploy-vm.png)
   
    Bu işlem tamamlandıktan sonra kısa ömürlü disk VM güncelleştirilir hello ile ilişkili kayıp ve dinamik IP adreslerini verilerdir.

Hala RDP sorunlarla karşılaşıyorsanız, şunları yapabilirsiniz [bir destek isteği açın](https://azure.microsoft.com/support/options/) veya okuma [kavramlar ve adımlar sorun giderme RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-using-azure-powershell"></a>Azure PowerShell kullanarak sorun giderme
Henüz yapmadıysanız [yükleme ve yapılandırma en son Azure PowerShell hello](/powershell/azure/overview).

Merhaba aşağıdaki örneklerde değişkenler gibi kullandığınız `myResourceGroup`, `myVM`, ve `myVMAccessExtension`. Bu değişken adları ve konumları kendi değerlerinizle değiştirin.

> [!NOTE]
> Merhaba kullanıcı kimlik bilgilerini ve hello RDP yapılandırması hello kullanarak sıfırlama [kümesi AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet'i. Örnekler, aşağıdaki hello içinde `myVMAccessExtension` hello işleminin bir parçası belirttiğiniz bir addır. Merhaba VMAccessAgent ile daha önce çalıştıysa kullanarak hello varolan uzantısının hello adını alabilirsiniz `Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"` toocheck hello hello VM özelliklerini. tooview hello adı altında hello çıktı hello 'Uzantılar' bölümüne bakın.

Sorun giderme her adımdan sonra tooyour VM yeniden bağlanmayı deneyin. Hala bağlanamıyorsanız, sonraki adıma hello deneyin.

1. **RDP bağlantınızı sıfırlama**. Sorun giderme Bu adım, uzak bağlantıları devre dışı bırakıldığında veya Windows Güvenlik duvarı kurallarını RDP, örneğin engelliyor hello RDP yapılandırmasını sıfırlar.
   
    Merhaba izleyin örnek sıfırlar hello RDP bağlantısı adlı bir VM üzerinde `myVM` hello içinde `WestUS` konumu ve adlı hello kaynak grubunda `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location Westus -Name "myVMAccessExtension"
    ```
2. **Doğrulama ağ güvenlik grubu kuralları**. Bu sorun giderme adımı ağ güvenlik grubu toopermit RDP trafiğinizi bir kural sahip olduğunu doğrular. RDP Hello varsayılan bağlantı noktası 3389 numaralı TCP bağlantı noktası var. VM'nizi oluşturduğunuzda, kural toopermit RDP trafiğine otomatik olarak oluşturulabilir değil.
   
    Ağ güvenlik grubu toohello tüm hello yapılandırma verileri ilk olarak, Ata `$rules` değişkeni. Merhaba aşağıdaki örnek alacağı hello adlı ağ güvenlik grubu hakkında bilgi `myNetworkSecurityGroup` adlı hello kaynak grubunda `myResourceGroup`:
   
    ```powershell
    $rules = Get-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
        -Name "myNetworkSecurityGroup"
    ```
   
    Şimdi, bu ağ güvenlik grubu için yapılandırılmış olan hello kuralları görüntüleyin. Bir kural gelen bağlantılar için tooallow TCP bağlantı noktası 3389 gibi var olduğundan emin olun:
   
    ```powershell
    $rules.SecurityRules
    ```
   
    Merhaba aşağıdaki örnek RDP trafiğine izin verir. geçerli güvenlik kuralı gösterir. Gördüğünüz `Protocol`, `DestinationPortRange`, `Access`, ve `Direction` doğru şekilde yapılandırılır:
   
    ```powershell
    Name                     : default-allow-rdp
    Id                       : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/default-allow-rdp
    Etag                     : 
    ProvisioningState        : Succeeded
    Description              : 
    Protocol                 : TCP
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : *
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 1000
    Direction                : Inbound
    ```
   
    RDP trafiğine izin veren bir kural yoksa [ağ güvenlik grubu kural oluşturma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). TCP bağlantı noktası 3389 izin verin.
3. **Kullanıcı kimlik bilgilerini sıfırlama**. Bu sorun giderme adımı hello emin değilseniz, ya da unutulursa, hello kimlik belirttiğiniz hello yerel yönetici hesabının parolasını sıfırlar.
   
    İlk olarak, kullanıcı adı hello ve atayarak yeni bir parola toohello kimlik bilgilerini belirtin `$cred` şekilde değişkeni:
   
    ```powershell
    $cred=Get-Credential
    ```
   
    Şimdi, VM'yi hello kimlik bilgilerini güncelleştirin. Merhaba aşağıdaki örnek güncelleştirmeleri adlı bir VM hello kimlik bilgisi `myVM` hello içinde `WestUS` konumu ve adlı hello kaynak grubunda `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" `
        -VMName "myVM" -Location WestUS -Name "myVMAccessExtension" `
        -UserName $cred.GetNetworkCredential().Username `
        -Password $cred.GetNetworkCredential().Password
    ```
4. **VM'yi yeniden**. Bu sorun giderme adımı temel sorunları düzeltebilir hello VM kendisini sahip.
   
    Aşağıdaki örnek yeniden hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup`:
   
    ```powershell
    Restart-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
    ```
5. **VM'yi yeniden**. Bu sorun giderme adımı Azure toocorrect içinde VM tooanother konağınız temel platform ya da ağ sorunları yeniden dağıtır.
   
    Örnek yeniden dağıtır aşağıdaki hello hello adlı VM `myVM` hello içinde `WestUS` konumu ve adlı hello kaynak grubunda `myResourceGroup`:
   
    ```powershell
    Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

Hala RDP sorunlarla karşılaşıyorsanız, şunları yapabilirsiniz [bir destek isteği açın](https://azure.microsoft.com/support/options/) veya okuma [kavramlar ve adımlar sorun giderme RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-vms-created-using-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modeli kullanılarak oluşturulan sanal makineleri sorun giderme
Sorun giderme her adımdan sonra toohello VM yeniden bağlanmayı deneyin.

1. **RDP bağlantınızı sıfırlama**. Sorun giderme Bu adım, uzak bağlantıları devre dışı bırakıldığında veya Windows Güvenlik duvarı kurallarını RDP, örneğin engelliyor hello RDP yapılandırmasını sıfırlar.
   
    VM hello Azure portal'ı seçin. Merhaba tıklatın **... Daha fazla** düğmesine ve ardından **sıfırlama uzaktan erişim**:
   
    ![Merhaba RDP hello Azure portal yapılandırmasında Sıfırla](./media/troubleshoot-rdp-connection/classic-reset-rdp.png)
2. **Bulut Hizmetleri bitiş noktalarını doğrulama**. Bu sorun giderme adımı bulut Hizmetleri toopermit RDP trafiğinizi uç noktaları sahip olduğunu doğrular. RDP Hello varsayılan bağlantı noktası 3389 numaralı TCP bağlantı noktası var. VM'nizi oluşturduğunuzda, kural toopermit RDP trafiğine otomatik olarak oluşturulabilir değil.
   
   VM hello Azure portal'ı seçin. Merhaba tıklatın **uç noktaları** düğmesini tooview hello uç noktaları, VM için yapılandırılmış. Uç noktaları TCP bağlantı noktası 3389 üzerinde RDP trafiğine izin veren var olduğunu doğrulayın.
   
   Aşağıdaki örnek hello RDP trafiğine izin vermek geçerli uç nokta gösterir:
   
   ![Hello Azure portal'ın bulut Hizmetleri bitiş noktalarını doğrulama](./media/troubleshoot-rdp-connection/classic-verify-cloud-services-endpoints.png)
   
   RDP trafiğine izin veren bir uç nokta yoksa [bulut Hizmetleri uç noktası oluşturma](classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). TCP tooprivate 3389 numaralı bağlantı noktasına izin verin.
3. **VM önyükleme tanılaması gözden**. Merhaba VM bir sorun raporlama söz konusu ise bu sorun giderme adımı hello VM konsol günlükleri toodetermine inceler. Tüm sanal makineleri önyükleme tanılaması etkin, sahip, bu nedenle sorun giderme Bu adım isteğe bağlı olabilir.
   
    Özel sorun giderme adımları hello bu makalenin kapsamı dışındadır, ancak RDP bağlantı etkileyen daha geniş bir sorunu gösterebilir. Merhaba konsol günlükleri ve VM ekran görüntüsünü gözden geçirme hakkında daha fazla bilgi için bkz: [VM'ler için önyükleme tanılaması](https://azure.microsoft.com/blog/boot-diagnostics-for-virtual-machines-v2/).
4. **Merhaba VM kaynak durumu denetleme**. Bu sorun giderme adımı hello bağlantı toohello VM etkileyebilir Azure platformu ile bilinen bir sorun doğrular.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **kaynak durumu** düğmesi. Sağlıklı bir VM raporları olarak **kullanılabilir**:
   
    ![VM kaynak durumu hello Azure portal denetleyin](./media/troubleshoot-rdp-connection/classic-check-resource-health.png)
5. **Kullanıcı kimlik bilgilerini sıfırlama**. Bu sorun giderme adımı emin değilseniz veya hello kimlik unutmuş olduğunda belirtin hello yerel yönetici hesabının hello parolasını sıfırlar.
   
    VM hello Azure portal'ı seçin. Hello ayarları bölmesi toohello aşağı **destek + sorun giderme** hello listenin alt kısmına. Merhaba tıklatın **parola sıfırlama** düğmesi. Kullanıcı adınızı ve yeni bir parola girin. Son olarak, hello tıklatın **kaydetmek** düğmesi:
   
    ![Hello Azure portal Hello kullanıcı kimlik bilgilerini sıfırlama](./media/troubleshoot-rdp-connection/classic-reset-password.png)
6. **VM'yi yeniden**. Bu sorun giderme adımı temel sorunları düzeltebilir hello VM kendisini sahip.
   
    Hello Azure portal, VM seçin ve hello tıklatın **genel bakış** sekmesi. Merhaba tıklatın **yeniden** düğmesi:
   
    ![Merhaba VM hello Azure portalında yeniden başlatın](./media/troubleshoot-rdp-connection/classic-restart-vm.png)

Hala RDP sorunlarla karşılaşıyorsanız, şunları yapabilirsiniz [bir destek isteği açın](https://azure.microsoft.com/support/options/) veya okuma [kavramlar ve adımlar sorun giderme RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="troubleshoot-specific-rdp-errors"></a>Özel RDP hatalarında sorun giderme
Belirli bir hata iletisi tooconnect tooyour RDP aracılığıyla VM çalışırken karşılaşabilirsiniz. Merhaba, hello en sık karşılaşılan hata iletileri şunlardır:

* [bir lisans yok Uzak Masaüstü lisans sunucularını kullanılabilir tooprovide olduğundan Hello uzak oturum kesildi](troubleshoot-specific-rdp-errors.md#rdplicense).
* [Uzak Masaüstü bilgisayar "name" Merhaba bulamıyor](troubleshoot-specific-rdp-errors.md#rdpname).
* [Bir kimlik doğrulama hatası oluştu. Merhaba yerel güvenlik yetkilisi kurulamıyor](troubleshoot-specific-rdp-errors.md#rdpauth).
* [Windows güvenlik hatası: kimlik bilgilerinizi çalışmama](troubleshoot-specific-rdp-errors.md#wincred).
* [Bu bilgisayar toohello uzak bilgisayara bağlanamıyor](troubleshoot-specific-rdp-errors.md#rdpconnect).

## <a name="additional-resources"></a>Ek kaynaklar
Hiçbiri bu hatalar oluştu ve toohello Uzak Masaüstü VM yine bağlanamıyorsanız, ayrıntılı hello okuma [Uzak Masaüstü için sorun giderme kılavuzu](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Bir VM üzerinde çalışan uygulamalar erişimde adımları sorun giderme için bkz: [bir Azure VM üzerinde çalışan sorun giderme erişim tooan uygulama](../linux/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Azure'da güvenli Kabuk (SSH) tooconnect tooa Linux VM kullanma sorunu yaşıyor olup [sorun giderme SSH bağlantıları tooa Azure Linux VM'de](../linux/troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

