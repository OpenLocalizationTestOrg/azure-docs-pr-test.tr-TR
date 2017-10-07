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
# <a name="secure-iis-web-server-with-ssl-certificates-on-a-windows-virtual-machine-in-azure"></a>IIS web sunucusu sanal bir makinede Windows Azure SSL sertifikalarıyla güvenli
toosecure web sunucuları, bir Güvenli Yuva daha sonra (SSL) sertifikası olabilir tooencrypt web trafiği kullanılır. Bu SSL sertifikalarını Azure anahtar kasası depolanabilir ve Azure'da sertifikaları tooWindows sanal makineleri (VM'ler) güvenli dağıtımlar sağlar. Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:

> [!div class="checklist"]
> * Azure anahtar kasası oluşturma
> * Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle
> * Bir VM oluşturun ve hello IIS web sunucusunu yükleme
> * Merhaba sertifika VM hello ekleme ve SSL bağlaması ile IIS yapılandırma

Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor. Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü. Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).


## <a name="overview"></a>Genel Bakış
Azure anahtar kasası, şifreleme anahtarlarını ve gizli anahtarları, bu tür sertifikalar veya parolaları koruma sağlar. Anahtar kasası hello sertifika yönetimi işlemini kolaylaştırmaya yardımcı olur ve bu sertifikaları erişim anahtarlarını toomaintain denetim sağlar. Anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturun veya zaten sahip olduğunuz bir varolan, güvenilen bir sertifika yükleyin.

Sertifikaları içeren özel bir VM görüntüsü kullanarak yerine desteklenmiş, sertifikaları çalışan VM ekleme. Bu işlem hello en güncel sertifikaları dağıtımı sırasında bir web sunucusunda yüklü olan sağlar. Yenileme veya bir sertifikayı değiştirin, yeni bir özel VM görüntüsü toocreate da yok. Ek VM'ler oluşturmak gibi hello son sertifikaları otomatik olarak eklenmiş. Hello tüm işlem sırasında hiç hello sertifikaları hello Azure platformu bırakın veya bir komut dosyası, komut satırı geçmiş veya şablonda sunulur.


## <a name="create-an-azure-key-vault"></a>Azure anahtar kasası oluşturma
Bir anahtar kasası ve sertifikaları oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupSecureWeb* hello içinde *Doğu ABD* konumu:

```powershell
$resourceGroup = "myResourceGroupSecureWeb"
$location = "East US"
New-AzureRmResourceGroup -ResourceGroupName $resourceGroup -Location $location
```

Ardından, bir anahtar kasası ile oluşturma [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault). Her anahtar kasası benzersiz bir ad gerektirir ve tüm küçük olmalıdır. Değiştir `<mykeyvault>` kendi benzersiz bir anahtar kasası ad örnekle aşağıdaki hello içinde:

```powershell
$keyvaultName="<mykeyvault>"
New-AzureRmKeyVault -VaultName $keyvaultName `
    -ResourceGroup $resourceGroup `
    -Location $location `
    -EnabledForDeployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Bir sertifika oluşturmak ve anahtar kasasına depolamak
Üretim kullanımı için güvenilen bir sağlayıcı tarafından imzalanmış geçerli bir sertifika almanız gerekir [alma AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/import-azurekeyvaultcertificate). Bu öğretici için hello aşağıdaki örnek otomatik olarak imzalanan bir sertifika ile nasıl oluşturabileceğiniz gösterir [Ekle AzureKeyVaultCertificate](/powershell/module/azurerm.keyvault/add-azurekeyvaultcertificate) kullandığı varsayılan sertifika ilkesinden hello [ AzureKeyVaultCertificatePolicy yeni](/powershell/module/azurerm.keyvault/new-azurekeyvaultcertificatepolicy). 

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


## <a name="create-a-virtual-machine"></a>Sanal makine oluşturma
Bir yönetici kullanıcı adı ve parola hello VM ile kümesi [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

Oluşturabileceğiniz artık VM ile Merhaba [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm). Merhaba aşağıdaki örnek gerekli hello sanal ağ bileşenleri hello işletim sistemi yapılandırması ve ardından adlı bir VM oluşturur *myVM*:

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

Oluşturulan hello VM toobe birkaç dakika sürer. Merhaba son adımı kullanan hello Azure özel betik uzantısının tooinstall hello IIS web sunucusu ile [kümesi AzureRmVmExtension](/powershell/module/azurerm.compute/set-azurermvmextension).


## <a name="add-a-certificate-toovm-from-key-vault"></a>Anahtar Kasası'nı bir sertifika tooVM Ekle
Anahtar kasası tooa VM tooadd hello sertifika elde sertifikanızla hello Kimliğini [Get-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/get-azurekeyvaultsecret). Merhaba sertifika toohello VM ekleme ile [Ekle AzureRmVMSecret](/powershell/module/azurerm.compute/add-azurermvmsecret):

```powershell
$certURL=(Get-AzureKeyVaultSecret -VaultName $keyvaultName -Name "mycert").id

$vm=Get-AzureRMVM -ResourceGroupName $resourceGroup -Name "myVM"
$vaultId=(Get-AzureRmKeyVault -ResourceGroupName $resourceGroup -VaultName $keyVaultName).ResourceId
$vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $vaultId -CertificateStore "My" -CertificateUrl $certURL

Update-AzureRmVM -ResourceGroupName $resourceGroup -VM $vm
```


## <a name="configure-iis-toouse-hello-certificate"></a>IIS toouse hello sertifika yapılandırma
Kullanım hello özel betik uzantısı'yla yeniden [kümesi AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooupdate hello IIS yapılandırması. Bu güncelleştirme, anahtar kasası tooIIS eklenen hello sertifika uygular ve hello web bağlama yapılandırır:

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


### <a name="test-hello-secure-web-app"></a>Test hello güvenli web uygulaması
Merhaba, VM ile genel IP adresi elde [Get-AzureRmPublicIPAddress](/powershell/resourcemanager/azurerm.network/get-azurermpublicipaddress). Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi `myPublicIP` daha önce oluşturduğunuz:

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName $resourceGroup -Name "myPublicIP" | select "IpAddress"
```

Bir web tarayıcısı açın ve girin artık `https://<myPublicIP>` hello adres çubuğundaki. kendinden imzalı bir sertifika kullanılması durumunda tooaccept hello güvenlik uyarısı seçin **ayrıntıları** ve ardından **toohello Web sayfasındaki Git**:

![Web tarayıcısı güvenlik uyarısını kabul edin](./media/tutorial-secure-web-server/browser-warning.png)

Güvenli, IIS Web sitesi, ardından aşağıdaki örneğine hello olduğu gibi görüntülenir:

![Görünüm çalıştırma güvenli IIS sitesi](./media/tutorial-secure-web-server/secured-iis.png)


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, Azure anahtar kasasında depolanan bir SSL sertifikası ile bir IIS web sunucusu güvenli. Şunları öğrendiniz:

> [!div class="checklist"]
> * Azure anahtar kasası oluşturma
> * Oluşturmak veya bir sertifika toohello anahtar kasası karşıya yükle
> * Bir VM oluşturun ve hello IIS web sunucusunu yükleme
> * Merhaba sertifika VM hello ekleme ve SSL bağlaması ile IIS yapılandırma

Sanal makine kod örnekleri önceden oluşturulmuş Bu bağlantı toosee izleyin.

> [!div class="nextstepaction"]
> [Windows sanal makine kod örnekleri](./powershell-samples.md)