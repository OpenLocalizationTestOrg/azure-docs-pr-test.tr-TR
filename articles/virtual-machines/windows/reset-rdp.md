---
title: "aaaReset hello parola veya bir Windows VM üzerinde Uzak Masaüstü yapılandırması | Microsoft Docs"
description: "Azure portal ya da Azure PowerShell nasıl tooreset bir hesap parolası veya Uzak Masaüstü Hizmetleri kullanarak bir Windows VM üzerinde hello öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 5258df7196621f0adb50debd08dd248922a966de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>Tooreset nasıl hello Uzak Masaüstü hizmet veya oturum açma parolasını bir Windows VM
Tooa Windows sanal makine (VM) bağlanamıyorsanız, hello yerel yönetici parolasını sıfırlama veya hello Uzak Masaüstü hizmet yapılandırmasını. Azure PowerShell tooreset hello Parolada ya da hello Azure portal veya hello VM erişim uzantısını kullanabilirsiniz. PowerShell kullanıyorsanız, hello olduğundan emin olun [yüklenmiş ve yapılandırılmış en son PowerShell Modülü](/powershell/azure/overview) ve tooyour Azure aboneliği imzalanmıştır. Ayrıca [hello Klasik dağıtım modeliyle oluşturulan VM'ler için bu adımları uygulamadan](reset-rdp.md).

## <a name="ways-tooreset-configuration-or-credentials"></a>Yolları tooreset yapılandırma veya kimlik bilgileri
Gereksinimlerinize bağlı olarak birkaç farklı şekilde, Uzak Masaüstü Hizmetleri ve kimlik bilgilerini sıfırlayabilirsiniz:

- [Hello Azure portal kullanarak Sıfırla](#azure-portal)
- [Azure PowerShell kullanarak Sıfırla](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure portalına
tooexpand hello portal menüsünde hello sol üst köşedeki hello üç çubuklarında tıklayın ve ardından **sanal makineleri**:

![Azure VM için Gözat](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a>**Merhaba yerel yönetici hesabı parolasını sıfırlama**

Windows sanal makinenizi seçip'i tıklatın **destek + sorun giderme** > **parola sıfırlama**. Merhaba parola sıfırlama dikey penceresinde görüntülenir:

![Parola sıfırlama sayfası](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

Merhaba kullanıcı adı ve yeni bir parola girin ve ardından **güncelleştirme**. Tooyour VM yeniden bağlanmayı deneyin.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**

Windows sanal makinenizi seçip'i tıklatın **destek + sorun giderme** > **parola sıfırlama**. Merhaba parola sıfırlama dikey penceresinde görüntülenir. 

![RDP yapılandırması sıfırlandı](./media/reset-rdp/Portal-RM-RDP-Reset.png)

Seçin **yalnızca sıfırlama yapılandırma** hello açılan menüsünden ardından **güncelleştirme**. Tooyour VM yeniden bağlanmayı deneyin.


## <a name="vmaccess-extension-and-powershell"></a>VMAccess uzantısını ve PowerShell
Merhaba sahip olduğunuzdan emin olun [yüklenmiş ve yapılandırılmış en son PowerShell Modülü](/powershell/azure/overview) ve tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` cmdlet'i.

### <a name="reset-hello-local-administrator-account-password"></a>**Merhaba yerel yönetici hesabı parolasını sıfırlama**
Sıfırlama hello yönetici parola veya kullanıcı adı ile Merhaba [kümesi AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet'i. Hesap kimlik bilgilerinizi gibi oluşturun:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> VM üzerinde hello geçerli yerel yönetici hesabından farklı bir ad yazın, hello VMAccess uzantısını hello yerel yönetici hesabı yeniden adlandırır, belirtilen parola toothat hesabınızı atar ve bir Uzak Masaüstü oturumu kapatma olayı verir. Merhaba VMAccess uzantısını VM Hello yerel yönetici hesabını devre dışı bırakılırsa sağlar.

Şu örnek güncelleştirmeleri hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup` toohello kimlik bilgileri belirtildi.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**
Merhaba ile uzaktan erişim tooyour VM sıfırlama [kümesi AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet'i. Merhaba aşağıdaki örnek sıfırlar adlı hello erişim uzantısı `myVMAccess` hello adlı VM üzerinde `myVM` hello içinde `myResourceGroup` kaynak grubu:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> Herhangi bir noktada bir VM yalnızca bir VM erişim aracıyı olabilir. tooset hello VM erişim Aracısı özellikleri başarıyla hello `-ForceRerun` seçeneği kullanılabilir. Kullanırken `-ForceRerun`, toouse hello olarak herhangi bir önceki komut kullanılan hello VM erişim aracısı için aynı adı olduğundan emin olun.

Hala uzaktan tooyour sanal makineye bağlanamıyorsanız, daha fazla adımları tootry adresindeki bkz [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Sonraki adımlar
Hello Azure VM erişim uzantısı yanıt vermiyor ve oluşturamıyor tooreset hello parola eminseniz yapabilecekleriniz [hello yerel Windows parola sıfırlama çevrimdışı](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu yöntem daha gelişmiş bir işlemdir ve hello sorunlu VM tooanother VM tooconnect hello sanal sabit diskin gerektirir. Bu makalede anlatıldığı ilk hello adımları izleyin ve yalnızca hello çevrimdışı parola sıfırlama yöntemi son çare olarak çalışır.

[Azure VM uzantıları ve özellikleri](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[RDP veya SSH ile tooan Azure sanal makinesine bağlanma](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

