---
title: "parola veya uzak masaüstü yapılandırmasının Azure Windows VM üzerinde aaaReset hello | Microsoft Docs"
description: "Merhaba Klasik dağıtım modeli kullanarak bir hesap parolası veya Uzak Masaüstü Hizmetleri Windows VM üzerinde oluşturulan tooreset nasıl hello Azure portalında veya Azure PowerShell öğrenin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1721a91fc6c89b46df74e76dfcf918b1c4c77a4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a>Tooreset hello Uzak Masaüstü hizmet veya oturum açma parolasını bir Windows VM hello Klasik dağıtım modeli kullanılarak oluşturulan nasıl
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Ayrıca [hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş VM'ler için bu adımları uygulamadan](../reset-rdp.md).

Tooa Windows sanal makine (VM) bağlanamıyorsanız, hello yerel yönetici parolasını sıfırlama veya hello Uzak Masaüstü hizmet yapılandırmasını. Azure PowerShell tooreset hello Parolada ya da hello Azure portal veya hello VM erişim uzantısını kullanabilirsiniz.

## <a name="ways-tooreset-configuration-or-credentials"></a>Yolları tooreset yapılandırma veya kimlik bilgileri
Gereksinimlerinize bağlı olarak birkaç farklı şekilde, Uzak Masaüstü Hizmetleri ve kimlik bilgilerini sıfırlayabilirsiniz:

- [Hello Azure portal kullanarak Sıfırla](#azure-portal)
- [Azure PowerShell kullanarak Sıfırla](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure portalına
Merhaba kullanabilirsiniz [Azure portal](https://portal.azure.com) tooreset hello Uzak Masaüstü hizmet. tooexpand hello portal menüsünde hello sol üst köşedeki hello üç çubuklarında tıklayın ve ardından **sanal makineleri (Klasik)**:

![Azure VM için Gözat](./media/reset-rdp/Portal-Select-Classic-VM.png)

Windows sanal makineyi seçin ve ardından **uzaktan Sıfırla...** . hello aşağıdaki iletişim kutusu belirir tooreset hello uzak masaüstü yapılandırması:

![Sıfırlama RDP yapılandırma sayfası](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

Merhaba kullanıcı adı ve parola hello yerel yönetici hesabının da sıfırlayabilirsiniz. Sanal makineden tıklatın **destek + sorun giderme** > **parola sıfırlama**. Merhaba parola sıfırlama dikey penceresinde görüntülenir:

![Parola sıfırlama sayfası](./media/reset-rdp/Portal-PW-Reset-Windows.png)

Merhaba yeni bir kullanıcı adı ve parolanızı girdikten sonra tıklatın **kaydetmek**.

## <a name="vmaccess-extension-and-powershell"></a>VMAccess uzantısını ve PowerShell
VM aracısının hello sanal makinede yüklü olduğundan emin hello olun. Merhaba VMAccess uzantısını hello VM Aracısı kullanılabilir olduğu sürece, kullanmadan önce yüklü toobe gerekmez. VM aracısının komutu aşağıdaki hello kullanarak zaten yüklü olduğundan bu hello doğrulayın. ("MyCloudService" ve "myVM" bulut hizmetiniz ve, VM tarafından hello adları sırasıyla değiştirin. Çalıştırarak bu adları öğrenebilirsiniz `Get-AzureVM` hiçbir parametre olmadan.)

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

Merhaba, **write-host** komutu görüntüler **doğru**, VM aracısının yüklü hello. Görüntüler, **False**, hello yönergeler ve hello indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog postası.

Merhaba sanal makine hello portalını kullanarak oluşturduysanız, denetleyin olup olmadığını `$vm.GetInstance().ProvisionGuestAgent` döndürür **doğru**. Aksi halde, bu komutu kullanarak ayarlayabilirsiniz:

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

Bu komut hello çalıştırırken aşağıdaki hata hello engeller **kümesi AzureVMExtension** komutunu hello sonraki adımlar: "Sağlama Konuk Aracısı etkinleştirilmelidir hello VM nesnesinde Iaas VM erişim uzantısı ayarlamadan önce."

### <a name="reset-hello-local-administrator-account-password"></a>**Merhaba yerel yönetici hesabı parolasını sıfırlama**
Merhaba geçerli yerel yönetici hesabı adı ve yeni bir parola ile oturum açma kimlik bilgileri oluşturun ve hello çalıştırın `Set-AzureVMAccessExtension` gibi.

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

Merhaba geçerli hesabından farklı bir ad yazın, hello VMAccess uzantısını hello yerel yönetici hesabı yeniden adlandırır, hello parola toothat hesabı atar ve Uzak Masaüstü oturumu kapatma sorunlarını. Merhaba VMAccess uzantısını Hello yerel yönetici hesabı devre dışı bırakılırsa sağlar.

Bu komutlar da hello Uzak Masaüstü hizmet yapılandırmasını sıfırlayın.

### <a name="reset-hello-remote-desktop-service-configuration"></a>**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**
komutu aşağıdaki hello çalıştırmak tooreset hello Uzak Masaüstü hizmet yapılandırmasını:

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

Merhaba VMAccess uzantısını hello sanal makinede iki komutu çalıştırır:

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

Bu komut 3389 numaralı TCP bağlantı noktasını kullanır gelen Uzak Masaüstü trafiğe izin veren hello yerleşik Windows Güvenlik Duvarı Grup etkinleştirir.

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

Bu komut, Uzak Masaüstü bağlantıları etkinleştirme hello fDenyTSConnections kayıt defteri değeri too0, ayarlar.

## <a name="next-steps"></a>Sonraki adımlar
Hello Azure VM erişim uzantısı yanıt vermiyor ve oluşturamıyor tooreset hello parola eminseniz yapabilecekleriniz [hello yerel Windows parola sıfırlama çevrimdışı](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bu yöntem daha gelişmiş bir işlemdir ve hello sorunlu VM tooanother VM tooconnect hello sanal sabit diskin gerektirir. Bu makalede anlatıldığı ilk hello adımları izleyin ve yalnızca hello çevrimdışı parola sıfırlama yöntemi son çare olarak çalışır.

[Azure VM uzantıları ve özellikleri](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[RDP veya SSH ile tooan Azure sanal makinesine bağlanma](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

