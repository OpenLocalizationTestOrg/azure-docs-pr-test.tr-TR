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
# <a name="how-tooreset-hello-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-hello-classic-deployment-model"></a><span data-ttu-id="8ceee-103">Tooreset hello Uzak Masaüstü hizmet veya oturum açma parolasını bir Windows VM hello Klasik dağıtım modeli kullanılarak oluşturulan nasıl</span><span class="sxs-lookup"><span data-stu-id="8ceee-103">How tooreset hello Remote Desktop service or its login password in a Windows VM created using hello Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ceee-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8ceee-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8ceee-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="8ceee-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8ceee-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="8ceee-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8ceee-107">Ayrıca [hello Resource Manager dağıtım modeli kullanılarak oluşturulmuş VM'ler için bu adımları uygulamadan](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="8ceee-107">You can also [perform these steps for VMs created with hello Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="8ceee-108">Tooa Windows sanal makine (VM) bağlanamıyorsanız, hello yerel yönetici parolasını sıfırlama veya hello Uzak Masaüstü hizmet yapılandırmasını.</span><span class="sxs-lookup"><span data-stu-id="8ceee-108">If you can't connect tooa Windows virtual machine (VM), you can reset hello local administrator password or reset hello Remote Desktop service configuration.</span></span> <span data-ttu-id="8ceee-109">Azure PowerShell tooreset hello Parolada ya da hello Azure portal veya hello VM erişim uzantısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ceee-109">You can use either hello Azure portal or hello VM Access extension in Azure PowerShell tooreset hello password.</span></span>

## <a name="ways-tooreset-configuration-or-credentials"></a><span data-ttu-id="8ceee-110">Yolları tooreset yapılandırma veya kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="8ceee-110">Ways tooreset configuration or credentials</span></span>
<span data-ttu-id="8ceee-111">Gereksinimlerinize bağlı olarak birkaç farklı şekilde, Uzak Masaüstü Hizmetleri ve kimlik bilgilerini sıfırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ceee-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="8ceee-112">Hello Azure portal kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="8ceee-112">Reset using hello Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="8ceee-113">Azure PowerShell kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="8ceee-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="8ceee-114">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="8ceee-114">Azure portal</span></span>
<span data-ttu-id="8ceee-115">Merhaba kullanabilirsiniz [Azure portal](https://portal.azure.com) tooreset hello Uzak Masaüstü hizmet.</span><span class="sxs-lookup"><span data-stu-id="8ceee-115">You can use hello [Azure portal](https://portal.azure.com) tooreset hello Remote Desktop service.</span></span> <span data-ttu-id="8ceee-116">tooexpand hello portal menüsünde hello sol üst köşedeki hello üç çubuklarında tıklayın ve ardından **sanal makineleri (Klasik)**:</span><span class="sxs-lookup"><span data-stu-id="8ceee-116">tooexpand hello portal menu, click hello three bars in hello upper left corner and then click **Virtual machines (classic)**:</span></span>

![Azure VM için Gözat](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="8ceee-118">Windows sanal makineyi seçin ve ardından **uzaktan Sıfırla...** . hello aşağıdaki iletişim kutusu belirir tooreset hello uzak masaüstü yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="8ceee-118">Select your Windows virtual machine and then click **Reset Remote...**. hello following dialog appears tooreset hello Remote Desktop configuration:</span></span>

![Sıfırlama RDP yapılandırma sayfası](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="8ceee-120">Merhaba kullanıcı adı ve parola hello yerel yönetici hesabının da sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8ceee-120">You can also reset hello username and password of hello local administrator account.</span></span> <span data-ttu-id="8ceee-121">Sanal makineden tıklatın **destek + sorun giderme** > **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="8ceee-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="8ceee-122">Merhaba parola sıfırlama dikey penceresinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="8ceee-122">hello password reset blade is displayed:</span></span>

![Parola sıfırlama sayfası](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="8ceee-124">Merhaba yeni bir kullanıcı adı ve parolanızı girdikten sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8ceee-124">After you enter hello new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="8ceee-125">VMAccess uzantısını ve PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ceee-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="8ceee-126">VM aracısının hello sanal makinede yüklü olduğundan emin hello olun.</span><span class="sxs-lookup"><span data-stu-id="8ceee-126">Make sure hello VM Agent is installed on hello virtual machine.</span></span> <span data-ttu-id="8ceee-127">Merhaba VMAccess uzantısını hello VM Aracısı kullanılabilir olduğu sürece, kullanmadan önce yüklü toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8ceee-127">hello VMAccess extension doesn't need toobe installed before you can use it, as long as hello VM Agent is available.</span></span> <span data-ttu-id="8ceee-128">VM aracısının komutu aşağıdaki hello kullanarak zaten yüklü olduğundan bu hello doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8ceee-128">Verify that hello VM Agent is already installed by using hello following command.</span></span> <span data-ttu-id="8ceee-129">("MyCloudService" ve "myVM" bulut hizmetiniz ve, VM tarafından hello adları sırasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8ceee-129">(Replace "myCloudService" and "myVM" by hello names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="8ceee-130">Çalıştırarak bu adları öğrenebilirsiniz `Get-AzureVM` hiçbir parametre olmadan.)</span><span class="sxs-lookup"><span data-stu-id="8ceee-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="8ceee-131">Merhaba, **write-host** komutu görüntüler **doğru**, VM aracısının yüklü hello.</span><span class="sxs-lookup"><span data-stu-id="8ceee-131">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="8ceee-132">Görüntüler, **False**, hello yönergeler ve hello indirme bağlantısı toohello bkz [VM aracısı ve uzantılar - 2. parça](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog postası.</span><span class="sxs-lookup"><span data-stu-id="8ceee-132">If it displays **False**, see hello instructions and a link toohello download in hello [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="8ceee-133">Merhaba sanal makine hello portalını kullanarak oluşturduysanız, denetleyin olup olmadığını `$vm.GetInstance().ProvisionGuestAgent` döndürür **doğru**.</span><span class="sxs-lookup"><span data-stu-id="8ceee-133">If you created hello virtual machine by using hello portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="8ceee-134">Aksi halde, bu komutu kullanarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8ceee-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="8ceee-135">Bu komut hello çalıştırırken aşağıdaki hata hello engeller **kümesi AzureVMExtension** komutunu hello sonraki adımlar: "Sağlama Konuk Aracısı etkinleştirilmelidir hello VM nesnesinde Iaas VM erişim uzantısı ayarlamadan önce."</span><span class="sxs-lookup"><span data-stu-id="8ceee-135">This command prevents hello following error when you're running hello **Set-AzureVMExtension** command in hello next steps: “Provision Guest Agent must be enabled on hello VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-hello-local-administrator-account-password"></a><span data-ttu-id="8ceee-136">**Merhaba yerel yönetici hesabı parolasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="8ceee-136">**Reset hello local administrator account password**</span></span>
<span data-ttu-id="8ceee-137">Merhaba geçerli yerel yönetici hesabı adı ve yeni bir parola ile oturum açma kimlik bilgileri oluşturun ve hello çalıştırın `Set-AzureVMAccessExtension` gibi.</span><span class="sxs-lookup"><span data-stu-id="8ceee-137">Create a sign-in credential with hello current local administrator account name and a new password, and then run hello `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="8ceee-138">Merhaba geçerli hesabından farklı bir ad yazın, hello VMAccess uzantısını hello yerel yönetici hesabı yeniden adlandırır, hello parola toothat hesabı atar ve Uzak Masaüstü oturumu kapatma sorunlarını. Merhaba VMAccess uzantısını Hello yerel yönetici hesabı devre dışı bırakılırsa sağlar.</span><span class="sxs-lookup"><span data-stu-id="8ceee-138">If you type a different name than hello current account, hello VMAccess extension renames hello local administrator account, assigns hello password toothat account, and issues a Remote Desktop sign-out. If hello local administrator account is disabled, hello VMAccess extension enables it.</span></span>

<span data-ttu-id="8ceee-139">Bu komutlar da hello Uzak Masaüstü hizmet yapılandırmasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="8ceee-139">These commands also reset hello Remote Desktop service configuration.</span></span>

### <a name="reset-hello-remote-desktop-service-configuration"></a><span data-ttu-id="8ceee-140">**Merhaba Uzak Masaüstü hizmet yapılandırmasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="8ceee-140">**Reset hello Remote Desktop service configuration**</span></span>
<span data-ttu-id="8ceee-141">komutu aşağıdaki hello çalıştırmak tooreset hello Uzak Masaüstü hizmet yapılandırmasını:</span><span class="sxs-lookup"><span data-stu-id="8ceee-141">tooreset hello Remote Desktop service configuration, run hello following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="8ceee-142">Merhaba VMAccess uzantısını hello sanal makinede iki komutu çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="8ceee-142">hello VMAccess extension runs two commands on hello virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="8ceee-143">Bu komut 3389 numaralı TCP bağlantı noktasını kullanır gelen Uzak Masaüstü trafiğe izin veren hello yerleşik Windows Güvenlik Duvarı Grup etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8ceee-143">This command enables hello built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="8ceee-144">Bu komut, Uzak Masaüstü bağlantıları etkinleştirme hello fDenyTSConnections kayıt defteri değeri too0, ayarlar.</span><span class="sxs-lookup"><span data-stu-id="8ceee-144">This command sets hello fDenyTSConnections registry value too0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ceee-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8ceee-145">Next steps</span></span>
<span data-ttu-id="8ceee-146">Hello Azure VM erişim uzantısı yanıt vermiyor ve oluşturamıyor tooreset hello parola eminseniz yapabilecekleriniz [hello yerel Windows parola sıfırlama çevrimdışı](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ceee-146">If hello Azure VM access extension does not respond and you are unable tooreset hello password, you can [reset hello local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8ceee-147">Bu yöntem daha gelişmiş bir işlemdir ve hello sorunlu VM tooanother VM tooconnect hello sanal sabit diskin gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8ceee-147">This method is a more advanced process and requires you tooconnect hello virtual hard disk of hello problematic VM tooanother VM.</span></span> <span data-ttu-id="8ceee-148">Bu makalede anlatıldığı ilk hello adımları izleyin ve yalnızca hello çevrimdışı parola sıfırlama yöntemi son çare olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="8ceee-148">Follow hello steps documented in this article first, and only attempt hello offline password reset method as a last resort.</span></span>

[<span data-ttu-id="8ceee-149">Azure VM uzantıları ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="8ceee-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="8ceee-150">RDP veya SSH ile tooan Azure sanal makinesine bağlanma</span><span class="sxs-lookup"><span data-stu-id="8ceee-150">Connect tooan Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="8ceee-151">Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="8ceee-151">Troubleshoot Remote Desktop connections tooa Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

