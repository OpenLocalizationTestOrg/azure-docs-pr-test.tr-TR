---
title: "Azure PowerShell Betiği örnek - Windows VM şifrelemek | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Windows VM şifrele"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9279fea482fcd8716bcd996985e10f500a4775ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="b042d-103">Azure PowerShell ile Windows sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="b042d-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="b042d-104">Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory Hizmet sorumlusu ve bir Windows sanal makine (VM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="b042d-105">VM şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="b042d-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b042d-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="b042d-106">Sample script</span></span>

<span data-ttu-id="b042d-107">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "şifrelemek VM diskleri")]</span><span class="sxs-lookup"><span data-stu-id="b042d-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b042d-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="b042d-108">Clean up deployment</span></span> 

<span data-ttu-id="b042d-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b042d-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b042d-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="b042d-110">Script explanation</span></span>

<span data-ttu-id="b042d-111">Bu komut dosyası dağıtımı oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="b042d-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="b042d-112">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="b042d-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b042d-113">Komut</span><span class="sxs-lookup"><span data-stu-id="b042d-113">Command</span></span> | <span data-ttu-id="b042d-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="b042d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b042d-115">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b042d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b042d-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b042d-117">Yeni-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="b042d-117">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="b042d-118">Şifreleme anahtarları gibi güvenli veri depolamak için bir Azure anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="b042d-119">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="b042d-119">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="b042d-120">Bir şifreleme anahtarı anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="b042d-121">AzureRmADServicePrincipal yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-121">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="b042d-122">Bir Azure Active Directory güvenli bir şekilde kimlik doğrulaması ve şifreleme anahtarlarının erişimi denetlemek için hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="b042d-123">Set AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="b042d-123">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="b042d-124">Şifreleme anahtarları için hizmet asıl erişim vermek için bu anahtar kasası üzerinde izinlerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="b042d-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="b042d-125">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b042d-126">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-126">Creates a subnet configuration.</span></span> <span data-ttu-id="b042d-127">Bu yapılandırma sanal ağ oluşturma işlemine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b042d-127">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="b042d-128">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b042d-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b042d-129">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-129">Creates a virtual network.</span></span> |
| [<span data-ttu-id="b042d-130">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="b042d-131">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-131">Creates a public IP address.</span></span> |
| [<span data-ttu-id="b042d-132">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-132">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="b042d-133">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-133">Creates a network security group rule configuration.</span></span> <span data-ttu-id="b042d-134">Bu yapılandırma, NSG oluşturulduğunda bir NSG kuralı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b042d-134">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="b042d-135">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-135">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="b042d-136">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-136">Creates a network security group.</span></span> |
| [<span data-ttu-id="b042d-137">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b042d-137">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b042d-138">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="b042d-138">Gets subnet information.</span></span> <span data-ttu-id="b042d-139">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b042d-139">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="b042d-140">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-140">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b042d-141">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-141">Creates a network interface.</span></span> |
| [<span data-ttu-id="b042d-142">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="b042d-142">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b042d-143">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b042d-143">Creates a VM configuration.</span></span> <span data-ttu-id="b042d-144">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="b042d-144">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b042d-145">Yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b042d-145">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b042d-146">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b042d-146">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="b042d-147">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b042d-147">Create a virtual machine.</span></span> |
| [<span data-ttu-id="b042d-148">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="b042d-148">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="b042d-149">Anahtar kasası hakkında bilgi alır gereken</span><span class="sxs-lookup"><span data-stu-id="b042d-149">Gets required information on the Key Vault</span></span> |
| [<span data-ttu-id="b042d-150">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="b042d-150">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="b042d-151">Hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b042d-151">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="b042d-152">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="b042d-152">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="b042d-153">VM şifreleme işleminin durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b042d-153">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="b042d-154">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b042d-154">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b042d-155">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="b042d-155">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b042d-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b042d-156">Next steps</span></span>

<span data-ttu-id="b042d-157">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b042d-157">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b042d-158">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b042d-158">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
