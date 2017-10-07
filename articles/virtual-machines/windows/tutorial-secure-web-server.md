---
title: "aaaSecure IIS ile SSL sertifikaları Azure'da | Microsoft Docs"
description: "Nasıl toosecure hello IIS web sunucusu SSL sertifikalarını Azure Windows VM üzerinde ile bilgi edinin"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/14/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 7a9e0ce07be2f55095fdb5347b64faf5caa4f7e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="07602-103">IIS web sunucusu sanal bir makinede Windows Azure SSL sertifikalarıyla güvenli</span><span class="sxs-lookup"><span data-stu-id="07602-103">Secure IIS web server with SSL certificates on a Windows virtual machine in Azure</span></span>
<span data-ttu-id="07602-104">toosecure web sunucuları, bir Güvenli Yuva daha sonra (SSL) sertifikası olabilir tooencrypt web trafiği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="07602-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="07602-105">Bu SSL sertifikalarını Azure anahtar kasası depolanabilir ve Azure'da sertifikaları tooWindows sanal makineleri (VM'ler) güvenli dağıtımlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="07602-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooWindows virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="07602-106">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="07602-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07602-107">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="07602-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="07602-108">Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="07602-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="07602-109">Bir VM oluşturun ve hello IIS web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="07602-109">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="07602-110">Merhaba sertifika VM hello ekleme ve SSL bağlaması ile IIS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="07602-110">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="07602-111">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="07602-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="07602-112">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="07602-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="07602-113">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="07602-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="overview"></a><span data-ttu-id="07602-114">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="07602-114">Overview</span></span>
<span data-ttu-id="07602-115">Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, bu tür sertifikalar veya parolaları koruma sağlar.</span><span class="sxs-lookup"><span data-stu-id="07602-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="07602-116">Anahtar kasası hello sertifika yönetimi işlemini kolaylaştırmaya yardımcı olur ve bu sertifikaları erişim anahtarlarını toomaintain denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="07602-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="07602-117">Anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturun veya zaten sahip olduğunuz bir varolan, güvenilen bir sertifika yükleyin.</span><span class="sxs-lookup"><span data-stu-id="07602-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="07602-118">Sertifikaları içeren özel bir VM görüntüsü kullanarak yerine desteklenmiş, sertifikaları çalışan VM ekleme.</span><span class="sxs-lookup"><span data-stu-id="07602-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="07602-119">Bu işlem hello en güncel sertifikaları dağıtımı sırasında bir web sunucusunda yüklü olan sağlar.</span><span class="sxs-lookup"><span data-stu-id="07602-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="07602-120">Yenileme veya bir sertifikayı değiştirin, yeni bir özel VM görüntüsü toocreate da yok.</span><span class="sxs-lookup"><span data-stu-id="07602-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="07602-121">Ek VM'ler oluşturmak gibi hello son sertifikaları otomatik olarak eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="07602-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="07602-122">Hello tüm işlem sırasında hiç hello sertifikaları hello Azure platformu bırakın veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.</span><span class="sxs-lookup"><span data-stu-id="07602-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="07602-123">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="07602-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="07602-124">Bir anahtar kasası ve sertifikaları oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="07602-124">Before you can create a Key Vault and certificates, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="07602-125">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupSecureWeb* hello içinde *Doğu ABD* konumu:</span><span class="sxs-lookup"><span data-stu-id="07602-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *East US* location:</span></span>

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

<span data-ttu-id="07602-126">Ardından, bir anahtar kasası ile oluşturma [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span><span class="sxs-lookup"><span data-stu-id="07602-126">Next, create a Key Vault with [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault).</span></span> <span data-ttu-id="07602-127">Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="07602-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="07602-128">Değiştir `<mykeyvault>` kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="07602-128">Replace `<mykeyvault>` in hello following example with your own unique Key Vault name:</span></span>

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="07602-129">Bir sertifika oluşturmak ve anahtar kasasına depolamak</span><span class="sxs-lookup"><span data-stu-id="07602-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="07602-130">Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [alma AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span><span class="sxs-lookup"><span data-stu-id="07602-130">For production use, you should import a valid certificate signed by trusted provider with [Import-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate).</span></span> <span data-ttu-id="07602-131">Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [Ekle AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) kullandığı varsayılan sertifika ilkesinden hello [ AzureKeyVaultCertificatePolicy yeni](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span><span class="sxs-lookup"><span data-stu-id="07602-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [Add-AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) that uses hello default certificate policy from [New-AzureKeyVaultCertificatePolicy](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy).</span></span> 

```powershell
$policy = New-AzureKeyVaultCertificatePolicy `
    -SubjectName "CN=www.contoso.com" `
    -SecretContentType "application/x-pkcs12" `
    -IssuerName Self `
    -ValidityInMonths 12

Add-AzureKeyVaultCertificate `
    -VaultName $keyvaultName `
    -Name "mycert" `
    -CertificatePolicy $policy 
```


## <a name="create-a-virtual-machine"></a><span data-ttu-id="07602-132">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="07602-132">Create a virtual machine</span></span>
<span data-ttu-id="07602-133">Bir yönetici kullanıcı adı ve parola hello VM ile kümesi [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="07602-133">Set an administrator username and password for hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="07602-134">Oluşturabileceğiniz artık VM ile Merhaba [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="07602-134">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="07602-135">Merhaba aşağıdaki örnek gerekli hello sanal ağ bileşenleri hello işletim sistemi yapılandırması ve ardından adlı bir VM oluşturur *myVM*:</span><span class="sxs-lookup"><span data-stu-id="07602-135">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myVnet" `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleRDP"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

# Create an inbound network security group rule for port 443
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRuleWWW"  `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority 1001 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443 `
    -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name "myNic" `
    -ResourceGroupName $resourceGroup `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS2" | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName "myVM" -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName "MicrosoftWindowsServer" `
    -Offer "WindowsServer" -Skus "2016-Datacenter" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create virtual machine
New-AzureRmVM -ResourceGroupName $resourceGroup -Location $location -VM $vmConfig

# Use hello Custom Script Extension tooinstall IIS
Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server -IncludeManagementTools"}'
```

<span data-ttu-id="07602-136">Oluşturulan hello VM toobe birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="07602-136">It takes a few minutes for hello VM toobe created.</span></span> <span data-ttu-id="07602-137">Merhaba son adımı kullanan hello Azure özel betik uzantısının tooinstall hello IIS web sunucusu ile [kümesi AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span><span class="sxs-lookup"><span data-stu-id="07602-137">hello last step uses hello Azure Custom Script Extension tooinstall hello IIS web server with [Set-AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).</span></span>


## <a name="add-a-certificate-toovm-from-key-vault"></a><span data-ttu-id="07602-138">Anahtar Kasası'nı bir sertifika tooVM Ekle</span><span class="sxs-lookup"><span data-stu-id="07602-138">Add a certificate tooVM from Key Vault</span></span>
<span data-ttu-id="07602-139">Anahtar kasası tooa VM tooadd hello sertifika elde sertifikanızla hello Kimliğini [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="07602-139">tooadd hello certificate from Key Vault tooa VM, obtain hello ID of your certificate with [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret).</span></span> <span data-ttu-id="07602-140">Merhaba sertifika toohello VM ekleme ile [Ekle AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span><span class="sxs-lookup"><span data-stu-id="07602-140">Add hello certificate toohello VM with [Add-AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):</span></span>

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a><span data-ttu-id="07602-141">IIS toouse hello sertifika yapılandırma</span><span class="sxs-lookup"><span data-stu-id="07602-141">Configure IIS toouse hello certificate</span></span>
<span data-ttu-id="07602-142">Kullanım hello özel betik uzantısı'yla yeniden [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="07602-142">Use hello Custom Script Extension again with [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS configuration.</span></span> <span data-ttu-id="07602-143">Bu güncelleştirme, anahtar kasası tooIIS eklenen hello sertifika uygular ve hello web bağlama yapılandırır:</span><span class="sxs-lookup"><span data-stu-id="07602-143">This update applies hello certificate injected from Key Vault tooIIS and configures hello web binding:</span></span>

```powershell
$PublicSettings = '{
    "fileUris":["https://raw.githubusercontent.com/iainfoulds/azure-samples/master/secure-iis.ps1"],
    "commandToExecute":"powershell -ExecutionPolicy Unrestricted -File secure-iis.ps1"
}'

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName "IIS" `
    -VMName "myVM" `
    -Location $location `
    -Publisher "Microsoft.Compute" `
    -ExtensionType "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -SettingString $publicSettings
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="07602-144">Test hello güvenli web uygulaması</span><span class="sxs-lookup"><span data-stu-id="07602-144">Test hello secure web app</span></span>
<span data-ttu-id="07602-145">Merhaba, VM ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="07602-145">Obtain hello public IP address of your VM with [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="07602-146">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi `myPublicIP` daha önce oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="07602-146">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

<span data-ttu-id="07602-147">Bir web tarayıcısı açın ve girin artık `https://<myPublicIP>` hello adres çubuğundaki.</span><span class="sxs-lookup"><span data-stu-id="07602-147">Now you can open a web browser and enter `https://<myPublicIP>` in hello address bar.</span></span> <span data-ttu-id="07602-148">kendinden imzalı bir sertifika kullanılması durumunda tooaccept hello güvenlik uyarısı seçin **ayrıntıları** ve ardından **toohello Web sayfasındaki Git**:</span><span class="sxs-lookup"><span data-stu-id="07602-148">tooaccept hello security warning if you used a self-signed certificate, select **Details** and then **Go on toohello webpage**:</span></span>

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="07602-150">Güvenli, IIS Web sitesi, ardından aşağıdaki örneğine hello olduğu gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="07602-150">Your secured IIS website is then displayed as in hello following example:</span></span>

![Görünüm çalıştırma güvenli IIS sitesi](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a><span data-ttu-id="07602-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="07602-152">Next steps</span></span>

<span data-ttu-id="07602-153">Bu öğreticide, Azure anahtar kasasında depolanan bir SSL sertifikası ile bir IIS web sunucusu güvenli.</span><span class="sxs-lookup"><span data-stu-id="07602-153">In this tutorial, you secured an IIS web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="07602-154">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="07602-154">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07602-155">Azure anahtar kasası oluşturma</span><span class="sxs-lookup"><span data-stu-id="07602-155">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="07602-156">Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="07602-156">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="07602-157">Bir VM oluşturun ve hello IIS web sunucusunu yükleme</span><span class="sxs-lookup"><span data-stu-id="07602-157">Create a VM and install hello IIS web server</span></span>
> * <span data-ttu-id="07602-158">Merhaba sertifika VM hello ekleme ve SSL bağlaması ile IIS yapılandırma</span><span class="sxs-lookup"><span data-stu-id="07602-158">Inject hello certificate into hello VM and configure IIS with an SSL binding</span></span>

<span data-ttu-id="07602-159">Sanal makine kod örnekleri önceden oluşturulmuş Bu bağlantı toosee izleyin.</span><span class="sxs-lookup"><span data-stu-id="07602-159">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07602-160">Windows sanal makine kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="07602-160">Windows virtual machine script samples</span></span>](./powershell-samples.md)