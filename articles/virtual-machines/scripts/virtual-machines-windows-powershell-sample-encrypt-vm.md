---
title: "PowerShell komut dosyası örneği - aaaAzure şifrelemek Windows VM | Microsoft Docs"
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
ms.openlocfilehash: 80c52a0b734a52a051ed30026b294840fd521143
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="26e5a-103">Azure PowerShell ile Windows sanal makine şifrele</span><span class="sxs-lookup"><span data-stu-id="26e5a-103">Encrypt a Windows virtual machine with Azure PowerShell</span></span>

<span data-ttu-id="26e5a-104">Bu komut dosyasını güvenli bir Azure anahtar kasası, şifreleme anahtarları, Azure Active Directory Hizmet sorumlusu ve bir Windows sanal makine (VM) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="26e5a-105">Merhaba VM hello şifreleme anahtarı anahtar kasası ve hizmet asıl kimlik bilgileri kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="26e5a-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="26e5a-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="26e5a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/encrypt-vm/encrypt-windows-vm.ps1 "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="26e5a-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="26e5a-107">Clean up deployment</span></span> 

<span data-ttu-id="26e5a-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="26e5a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="26e5a-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="26e5a-109">Script explanation</span></span>

<span data-ttu-id="26e5a-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="26e5a-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="26e5a-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="26e5a-112">Komut</span><span class="sxs-lookup"><span data-stu-id="26e5a-112">Command</span></span> | <span data-ttu-id="26e5a-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="26e5a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26e5a-114">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="26e5a-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="26e5a-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26e5a-116">Yeni-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="26e5a-116">New-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/new-azurermkeyvault) | <span data-ttu-id="26e5a-117">Azure anahtar kasası bir toostore güvenli veri şifreleme anahtarları gibi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="26e5a-118">Add-AzureKeyVaultKey</span><span class="sxs-lookup"><span data-stu-id="26e5a-118">Add-AzureKeyVaultKey</span></span>](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) | <span data-ttu-id="26e5a-119">Bir şifreleme anahtarı anahtar kasası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="26e5a-120">AzureRmADServicePrincipal yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-120">New-AzureRmADServicePrincipal</span></span>](/powershell/module/azurerm.resources/new-azurermadserviceprincipal) | <span data-ttu-id="26e5a-121">Bir Azure Active Directory hizmet asıl toosecurely kimlik doğrulaması ve Denetim erişim tooencryption tuşları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="26e5a-122">Set AzureRmKeyVaultAccessPolicy</span><span class="sxs-lookup"><span data-stu-id="26e5a-122">Set-AzureRmKeyVaultAccessPolicy</span></span>](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) | <span data-ttu-id="26e5a-123">İzinleri hello anahtar kasası toogrant üzerinde hello hizmet asıl erişim tooencryption anahtarları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="26e5a-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="26e5a-124">AzureRmVirtualNetworkSubnetConfig yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-124">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="26e5a-125">Bir alt ağ yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-125">Creates a subnet configuration.</span></span> <span data-ttu-id="26e5a-126">Bu yapılandırma ile Merhaba sanal ağ oluşturma işleminde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-126">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="26e5a-127">Yeni-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="26e5a-127">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="26e5a-128">Sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-128">Creates a virtual network.</span></span> |
| [<span data-ttu-id="26e5a-129">AzureRmPublicIpAddress yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="26e5a-130">Bir ortak IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-130">Creates a public IP address.</span></span> |
| [<span data-ttu-id="26e5a-131">AzureRmNetworkSecurityRuleConfig yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-131">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="26e5a-132">Bir ağ güvenlik grubu kural yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-132">Creates a network security group rule configuration.</span></span> <span data-ttu-id="26e5a-133">Merhaba NSG oluşturulduğunda bu kullanılan toocreate bir NSG kuralı yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-133">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="26e5a-134">AzureRmNetworkSecurityGroup yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-134">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="26e5a-135">Bir ağ güvenlik grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-135">Creates a network security group.</span></span> |
| [<span data-ttu-id="26e5a-136">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="26e5a-136">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="26e5a-137">Alt ağ bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-137">Gets subnet information.</span></span> <span data-ttu-id="26e5a-138">Bu bilgiler, bir ağ arabirimi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-138">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="26e5a-139">AzureRmNetworkInterface yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-139">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="26e5a-140">Bir ağ arabirimi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-140">Creates a network interface.</span></span> |
| [<span data-ttu-id="26e5a-141">AzureRmVMConfig yeni</span><span class="sxs-lookup"><span data-stu-id="26e5a-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="26e5a-142">Bir VM yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="26e5a-142">Creates a VM configuration.</span></span> <span data-ttu-id="26e5a-143">Bu yapılandırma VM adı, işletim sistemi ve yönetici kimlik bilgileri gibi bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="26e5a-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="26e5a-144">Merhaba yapılandırma VM oluşturma sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="26e5a-145">Yeni-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="26e5a-145">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="26e5a-146">Bir sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e5a-146">Create a virtual machine.</span></span> |
| [<span data-ttu-id="26e5a-147">Get-AzureRmKeyVault</span><span class="sxs-lookup"><span data-stu-id="26e5a-147">Get-AzureRmKeyVault</span></span>](/powershell/module/azurerm.keyvault/get-azurermkeyvault) | <span data-ttu-id="26e5a-148">Merhaba anahtar kasası hakkında bilgi alır gereken</span><span class="sxs-lookup"><span data-stu-id="26e5a-148">Gets required information on hello Key Vault</span></span> |
| [<span data-ttu-id="26e5a-149">Set-AzureRmVMDiskEncryptionExtension</span><span class="sxs-lookup"><span data-stu-id="26e5a-149">Set-AzureRmVMDiskEncryptionExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) | <span data-ttu-id="26e5a-150">Merhaba hizmet asıl kimlik bilgilerini ve şifreleme anahtarı kullanarak bir VM üzerinde şifrelemeyi etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="26e5a-150">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="26e5a-151">Get-AzureRmVmDiskEncryptionStatus</span><span class="sxs-lookup"><span data-stu-id="26e5a-151">Get-AzureRmVmDiskEncryptionStatus</span></span>](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) | <span data-ttu-id="26e5a-152">Merhaba VM şifreleme işlemi Hello durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="26e5a-152">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="26e5a-153">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="26e5a-153">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="26e5a-154">Bir kaynak grubu ve içerdiği tüm kaynaklar kaldırır.</span><span class="sxs-lookup"><span data-stu-id="26e5a-154">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26e5a-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26e5a-155">Next steps</span></span>

<span data-ttu-id="26e5a-156">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="26e5a-156">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="26e5a-157">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="26e5a-157">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
