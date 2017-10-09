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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="2b627-103">Tooreset nasıl hello Uzak Masaüstü hizmet veya oturum açma parolasını bir Windows VM</span><span class="sxs-lookup"><span data-stu-id="2b627-103">How tooreset hello Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="2b627-104">Tooa Windows sanal makine (VM) bağlanamıyorsanız, hello yerel yönetici parolasını sıfırlama veya hello Uzak Masaüstü hizmet yapılandırmasını.</span><span class="sxs-lookup"><span data-stu-id="2b627-104">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="2b627-105">Azure PowerShell tooreset hello Parolada ya da hello Azure portal veya hello VM erişim uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b627-105">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span> <span data-ttu-id="2b627-106">PowerShell kullanıyorsanız, hello olduğundan emin olun [yüklenmiş ve yapılandırılmış en son PowerShell Modülü](/powershell/azure/overview) ve tooyour Azure aboneliği imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2b627-106">If you are using PowerShell, make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription.</span></span> <span data-ttu-id="2b627-107">Ayrıca [hello Klasik dağıtım modeliyle oluşturulan VM'ler için bu adımları uygulamadan](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="2b627-107">You can also [perform these steps for VMs created with hello Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="2b627-108">Yolları tooreset yapılandırma veya kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="2b627-108">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="2b627-109">Gereksinimlerinize bağlı olarak birkaç farklı şekilde, Uzak Masaüstü Hizmetleri ve kimlik bilgilerini sıfırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2b627-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="2b627-110">Hello Azure portal kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="2b627-110">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="2b627-111">Azure PowerShell kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="2b627-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="2b627-112">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="2b627-112">Azure portal</span></span>
<span data-ttu-id="2b627-113">tooexpand hello portal menüsünde hello sol üst köşedeki hello üç çubuklarında tıklayın ve ardından **sanal makineleri**:</span><span class="sxs-lookup"><span data-stu-id="2b627-113">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines**:</span></span>

![Azure VM için Gözat](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="2b627-115">**Merhaba yerel yönetici hesabı parolasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="2b627-115">**Reset hello local administrator account password**</span></span>

<span data-ttu-id="2b627-116">Windows sanal makinenizi seçip'i tıklatın **destek + sorun giderme** > **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="2b627-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="2b627-117">Merhaba parola sıfırlama dikey penceresinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="2b627-117">hello password reset blade is displayed:</span></span>

![Parola sıfırlama sayfası](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="2b627-119">Merhaba kullanıcı adı ve yeni bir parola girin ve ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2b627-119">Enter hello username and a new password, then click **Update**.</span></span> <span data-ttu-id="2b627-120">Tooyour VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="2b627-120">Try connecting tooyour VM again.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="2b627-121">**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="2b627-121">**Reset hello Remote Desktop service configuration**</span></span>

<span data-ttu-id="2b627-122">Windows sanal makinenizi seçip'i tıklatın **destek + sorun giderme** > **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="2b627-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="2b627-123">Merhaba parola sıfırlama dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="2b627-123">hello password reset blade is displayed.</span></span> 

![RDP yapılandırması sıfırlandı](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="2b627-125">Seçin **yalnızca sıfırlama yapılandırma** hello açılan menüsünden ardından **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="2b627-125">Select **Reset configuration only** from hello drop-down menu, then click **Update**.</span></span> <span data-ttu-id="2b627-126">Tooyour VM yeniden bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="2b627-126">Try connecting tooyour VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="2b627-127">VMAccess uzantısını ve PowerShell</span><span class="sxs-lookup"><span data-stu-id="2b627-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="2b627-128">Merhaba sahip olduğunuzdan emin olun [yüklenmiş ve yapılandırılmış en son PowerShell Modülü](/powershell/azure/overview) ve tooyour hello Azure aboneliğiyle oturum `Login-AzureRmAccount` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2b627-128">Make sure that you have hello [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in tooyour Azure subscription with hello `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="2b627-129">**Merhaba yerel yönetici hesabı parolasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="2b627-129">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="2b627-130">Sıfırlama hello yönetici parola veya kullanıcı adı ile Merhaba [kümesi AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2b627-130">Reset hello administrator password or user name with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="2b627-131">Hesap kimlik bilgilerinizi gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="2b627-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="2b627-132">VM üzerinde hello geçerli yerel yönetici hesabından farklı bir ad yazın, hello VMAccess uzantısını hello yerel yönetici hesabı yeniden adlandırır, belirtilen parola toothat hesabınızı atar ve bir Uzak Masaüstü oturumu kapatma olayı verir.</span><span class="sxs-lookup"><span data-stu-id="2b627-132">If you type a different name than hello current local administrator account on your VM, hello VMAccess extension renames hello local administrator account, assigns your specified password toothat account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="2b627-133">Merhaba VMAccess uzantısını VM Hello yerel yönetici hesabını devre dışı bırakılırsa sağlar.</span><span class="sxs-lookup"><span data-stu-id="2b627-133">If hello local administrator account on your VM is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="2b627-134">Şu örnek güncelleştirmeleri hello hello adlı VM `myVM` adlı hello kaynak grubunda `myResourceGroup` toohello kimlik bilgileri belirtildi.</span><span class="sxs-lookup"><span data-stu-id="2b627-134">hello following example updates hello VM named `myVM` in hello resource group named `myResourceGroup` toohello credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="2b627-135">**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="2b627-135">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="2b627-136">Merhaba ile uzaktan erişim tooyour VM sıfırlama [kümesi AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2b627-136">Reset remote access tooyour VM with hello [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="2b627-137">Merhaba aşağıdaki örnek sıfırlar adlı hello erişim uzantısı `myVMAccess` hello adlı VM üzerinde `myVM` hello içinde `myResourceGroup` kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="2b627-137">hello following example resets hello access extension named `myVMAccess` on hello VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="2b627-138">Herhangi bir noktada bir VM yalnızca bir VM erişim aracıyı olabilir.</span><span class="sxs-lookup"><span data-stu-id="2b627-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="2b627-139">tooset hello VM erişim Aracısı özellikleri başarıyla hello `-ForceRerun` seçeneği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b627-139">tooset hello VM access agent properties successfully, hello `-ForceRerun` option can be used.</span></span> <span data-ttu-id="2b627-140">Kullanırken `-ForceRerun`, toouse hello olarak herhangi bir önceki komut kullanılan hello VM erişim aracısı için aynı adı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="2b627-140">When using `-ForceRerun`, make sure toouse hello same name for hello VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="2b627-141">Hala uzaktan tooyour sanal makineye bağlanamıyorsanız, daha fazla adımları tootry adresindeki bkz [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b627-141">If you still can't connect remotely tooyour virtual machine, see more steps tootry at [Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="2b627-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b627-142">Next steps</span></span>
<span data-ttu-id="2b627-143">Hello Azure VM erişim uzantısı yanıt vermiyor ve oluşturamıyor tooreset hello parola eminseniz yapabilecekleriniz [hello yerel Windows parola sıfırlama çevrimdışı](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b627-143">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2b627-144">Bu yöntem daha gelişmiş bir işlemdir ve hello sorunlu VM tooanother VM tooconnect hello sanal sabit diskin gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2b627-144">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="2b627-145">Bu makalede anlatıldığı ilk hello adımları izleyin ve yalnızca hello çevrimdışı parola sıfırlama yöntemi son çare olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="2b627-145">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="2b627-146">Azure VM uzantıları ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="2b627-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="2b627-147">RDP veya SSH ile tooan Azure sanal makinesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="2b627-147">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="2b627-148">Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="2b627-148">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

