---
title: "Parola veya uzak masaüstü yapılandırmasının Azure Windows VM üzerinde sıfırlama | Microsoft Docs"
description: "Bir hesap parolası sıfırlama öğrenin veya bir Windows VM üzerinde Uzak Masaüstü Hizmetleri Azure portalında veya Azure PowerShell kullanarak Klasik dağıtım modeli kullanılarak oluşturulmuş."
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
ms.openlocfilehash: 43e5cf1ab3bc3121d7e3915ea0785998e0ee2fc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-the-classic-deployment-model"></a><span data-ttu-id="d9bfc-103">Uzak Masaüstü hizmetini veya Windows Klasik dağıtım modeli kullanılarak oluşturulan bir VM'de oturum açma parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d9bfc-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d9bfc-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d9bfc-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d9bfc-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d9bfc-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d9bfc-107">Ayrıca [Resource Manager dağıtım modeliyle oluşturulan VM'ler için bu adımları uygulamadan](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="d9bfc-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="d9bfc-108">Bir Windows sanal makine (VM) bağlanamıyorsanız, yerel yönetici parolasını sıfırlama veya Uzak Masaüstü hizmet yapılandırmasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="d9bfc-109">Parola sıfırlama için Azure PowerShell'de Azure portalından veya VM erişim uzantısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="d9bfc-110">Yapılandırma veya kimlik bilgilerini sıfırlama yolları</span><span class="sxs-lookup"><span data-stu-id="d9bfc-110">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="d9bfc-111">Gereksinimlerinize bağlı olarak birkaç farklı şekilde, Uzak Masaüstü Hizmetleri ve kimlik bilgilerini sıfırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="d9bfc-112">Azure portalını kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="d9bfc-112">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="d9bfc-113">Azure PowerShell kullanarak Sıfırla</span><span class="sxs-lookup"><span data-stu-id="d9bfc-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="d9bfc-114">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="d9bfc-114">Azure portal</span></span>
<span data-ttu-id="d9bfc-115">Kullanabileceğiniz [Azure portal](https://portal.azure.com) Uzak Masaüstü hizmetini sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span></span> <span data-ttu-id="d9bfc-116">Portal menü genişletmek için sol üst köşedeki üç çubuklarında'ı tıklatın ve ardından **sanal makineleri (Klasik)**:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span></span>

![Azure VM için Gözat](./media/reset-rdp/Portal-Select-Classic-VM.png)

<span data-ttu-id="d9bfc-118">Windows sanal makineyi seçin ve ardından **uzaktan Sıfırla...** .</span><span class="sxs-lookup"><span data-stu-id="d9bfc-118">Select your Windows virtual machine and then click **Reset Remote...**.</span></span> <span data-ttu-id="d9bfc-119">Uzak Masaüstü yapılandırmasının sıfırlamak için aşağıdaki iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-119">The following dialog appears to reset the Remote Desktop configuration:</span></span>

![Sıfırlama RDP yapılandırma sayfası](./media/reset-rdp/Portal-RDP-Reset-Windows.png)

<span data-ttu-id="d9bfc-121">Kullanıcı adı ve parola yerel yönetici hesabının da sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-121">You can also reset the username and password of the local administrator account.</span></span> <span data-ttu-id="d9bfc-122">Sanal makineden tıklatın **destek + sorun giderme** > **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-122">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="d9bfc-123">Parola sıfırlama dikey penceresinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-123">The password reset blade is displayed:</span></span>

![Parola sıfırlama sayfası](./media/reset-rdp/Portal-PW-Reset-Windows.png)

<span data-ttu-id="d9bfc-125">Yeni bir kullanıcı adı ve parolanızı girdikten sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-125">After you enter the new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="d9bfc-126">VMAccess uzantısını ve PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9bfc-126">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="d9bfc-127">VM aracısının sanal makinede yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-127">Make sure the VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="d9bfc-128">VMAccess uzantısını VM Aracısı kullanılabilir olduğu sürece, kullanmadan önce yüklü olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-128">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span></span> <span data-ttu-id="d9bfc-129">VM Aracısı zaten aşağıdaki komutu kullanarak yüklü olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-129">Verify that the VM Agent is already installed by using the following command.</span></span> <span data-ttu-id="d9bfc-130">("MyCloudService" ve "myVM" bulut hizmetiniz ve, VM adlarıyla sırasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-130">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="d9bfc-131">Çalıştırarak bu adları öğrenebilirsiniz `Get-AzureVM` hiçbir parametre olmadan.)</span><span class="sxs-lookup"><span data-stu-id="d9bfc-131">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="d9bfc-132">Varsa **write-host** komutu görüntüler **doğru**, VM aracısının yüklü olduğundan.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-132">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="d9bfc-133">Görüntüler, **False**, yönergeler ve karşıdan yükleme bağlantısı bkz [VM aracısı ve uzantılar - 2. parça](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog gönderisi.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-133">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="d9bfc-134">Portalı kullanarak sanal makine oluşturduysanız denetleyin olup olmadığını `$vm.GetInstance().ProvisionGuestAgent` döndürür **doğru**.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-134">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="d9bfc-135">Aksi halde, bu komutu kullanarak ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-135">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="d9bfc-136">Çalıştırdığınız zaman bu komutu aşağıdaki hata engeller **kümesi AzureVMExtension** sonraki adımlarda komutu: "Sağlama Konuk Aracısı etkinleştirilmelidir VM nesnesinde Iaas VM erişim uzantısı ayarlamadan önce."</span><span class="sxs-lookup"><span data-stu-id="d9bfc-136">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="d9bfc-137">**Yerel yönetici hesabı parolasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="d9bfc-137">**Reset the local administrator account password**</span></span>
<span data-ttu-id="d9bfc-138">Geçerli yerel yönetici hesabı adı ve yeni bir parola ile oturum açma kimlik bilgileri oluşturun ve çalıştırın `Set-AzureVMAccessExtension` gibi.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-138">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="d9bfc-139">Geçerli hesabından farklı bir ad yazın, VMAccess uzantısını yerel yönetici hesabı yeniden adlandırır, o hesabı için parola atar ve Uzak Masaüstü oturumu kapatma sorunlarını.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-139">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out.</span></span> <span data-ttu-id="d9bfc-140">Yerel yönetici hesabı devre dışı bırakılırsa, VMAccess uzantısını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-140">If the local administrator account is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="d9bfc-141">Bu komutlar da Uzak Masaüstü hizmet yapılandırmasını sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-141">These commands also reset the Remote Desktop service configuration.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="d9bfc-142">**Uzak Masaüstü hizmet yapılandırmasını sıfırlama**</span><span class="sxs-lookup"><span data-stu-id="d9bfc-142">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="d9bfc-143">Uzak Masaüstü hizmet yapılandırmasını sıfırlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-143">To reset the Remote Desktop service configuration, run the following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="d9bfc-144">VMAccess uzantısını sanal makinede iki komutu çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="d9bfc-144">The VMAccess extension runs two commands on the virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="d9bfc-145">Bu komut 3389 numaralı TCP bağlantı noktasını kullanır gelen Uzak Masaüstü trafiğe izin veren yerleşik Windows Güvenlik Duvarı Grup etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-145">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="d9bfc-146">Bu komut fDenyTSConnections Uzak Masaüstü bağlantıları etkinleştirme 0 için kayıt defteri değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-146">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9bfc-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d9bfc-147">Next steps</span></span>
<span data-ttu-id="d9bfc-148">Azure VM erişim uzantısı yanıt vermiyor ve parola sıfırlamaya yoksa, şunları yapabilirsiniz [çevrimdışı yerel Windows parola sıfırlama](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9bfc-148">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d9bfc-149">Bu yöntem daha gelişmiş bir işlemdir ve başka bir VM için sanal sabit disk sorunlu VM bağlanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-149">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="d9bfc-150">Bu makalede ilk belgelenen adımları izleyin ve yalnızca son çare olarak çevrimdışı parola sıfırlama yöntemi deneyin.</span><span class="sxs-lookup"><span data-stu-id="d9bfc-150">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="d9bfc-151">Azure VM uzantıları ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="d9bfc-151">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="d9bfc-152">RDP veya SSH ile bir Azure sanal makineye bağlanmak</span><span class="sxs-lookup"><span data-stu-id="d9bfc-152">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="d9bfc-153">Windows tabanlı bir Azure sanal makine için Uzak Masaüstü bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="d9bfc-153">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

