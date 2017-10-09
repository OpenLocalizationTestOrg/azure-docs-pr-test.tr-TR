---
title: Azure Windows VM aaaEncrypt disklerde | Microsoft Docs
description: "Nasıl tooencrypt sanal diskler için bir Windows VM üzerinde Gelişmiş Güvenlik Azure PowerShell'i kullanma"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/10/2017
ms.author: iainfou
ms.openlocfilehash: 77c42a67cb57a9dc5fe3159fce0be75e3a965be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-windows-vm"></a>Nasıl bir Windows VM üzerindeki tooencrypt sanal diskler
Geliştirilmiş sanal makine (VM) güvenlik ve uyumluluk için Azure sanal diskleri şifrelenebilir. Diskleri, bir Azure anahtar kasası güvenli şifreleme anahtarları kullanılarak şifrelenir. Bu şifreleme anahtarları denetlemek ve bunların kullanılması denetleyebilirsiniz. Bu makale ayrıntıları nasıl Windows Azure PowerShell kullanarak bir VM sanal disklerde tooencrypt. Ayrıca [hello Azure CLI 2.0 kullanarak bir Linux VM şifrelemek](../linux/encrypt-disks.md).

## <a name="overview-of-disk-encryption"></a>Disk şifrelemesi'ne genel bakış
Windows sanal makineleri sanal disklerde Bitlocker kullanılarak bekleme sırasında şifrelenir. Azure sanal diskleri şifreleme ücretsizdir. Şifreleme anahtarları yazılım koruması'nı kullanarak Azure anahtar kasası içinde depolanır veya içe aktarmak ya da anahtarlarınızı tooFIPS sertifikalı donanım güvenlik modüllerinde (HSM'ler) 140-2 Düzey 2 standartları oluşturur. Bu şifreleme anahtarlar kullanılan tooencrypt ve sanal diskleri ekli tooyour VM şifresini. Bu şifreleme anahtarları denetimin korumak ve kullanımlarını denetleyebilirsiniz. Bir Azure Active Directory Hizmet sorumlusu VM'ler açma ve kapatma gücü gibi bu şifreleme anahtarları verme için güvenli bir mekanizma sağlar.

bir VM şifrelemek için hello işlem aşağıdaki gibidir:

1. Bir şifreleme anahtarının bir Azure anahtar kasası oluşturun.
2. Merhaba şifreleme anahtar toobe diskleri şifrelemek için kullanılabilir yapılandırın.
3. tooread hello şifreleme anahtarını hello Azure anahtar kasası oluşturma bir Azure Active Directory hizmet asıl hello uygun izinlere sahip.
4. Merhaba komutu tooencrypt hello Azure Active Directory hizmet asıl ve uygun şifreleme anahtar toobe kullanılan belirtme, sanal diskler gönderin.
5. Hello Azure Active Directory hizmet asıl istekleri Azure anahtar kasası gerekli şifreleme anahtarından hello.
6. Merhaba sanal diskler sağlanan hello şifreleme anahtarı kullanılarak şifrelenir.

## <a name="encryption-process"></a>Şifreleme işlemi
Disk şifrelemesi ek bileşenler aşağıdaki hello üzerinde dayanır:

* **Azure anahtar kasası** -kullanılan toosafeguard şifreleme anahtarları ve gizli anahtarları hello disk şifreleme/şifre çözme işlemi için kullanılır. 
  * Varsa, mevcut bir Azure anahtar kasası kullanabilirsiniz. Bir anahtar kasası tooencrypting disk toodedicate sahip değildir.
  * tooseparate yönetim sınırlarını ve anahtar görünürlük, ayrılmış bir anahtar kasası oluşturabilirsiniz.
* **Azure Active Directory** - tanıtıcıları hello gerekli şifreleme anahtarlarını güvenli değişimi ve kimlik doğrulaması için istenen eylemler. 
  * Genellikle, uygulamanızı barındırmak için var olan bir Azure Active Directory örneğini kullanabilirsiniz.
  * Merhaba hizmet sorumlusu hello uygun şifreleme anahtarları verilmesi ve güvenli mekanizması toorequest sağlar. Azure Active Directory ile tümleşen gerçek uygulama geliştirme değil.

## <a name="requirements-and-limitations"></a>Gereksinimler ve sınırlamalar
Desteklenen senaryolar ve disk şifrelemesi için gereksinimleri:

* Yeni Windows sanal makineleri Azure Market görüntülerini veya özel VHD görüntüsü üzerinde şifrelemeyi etkinleştirme.
* Var olan Windows sanal makineleri Azure üzerinde şifrelemeyi etkinleştirme.
* Depolama alanları kullanılarak yapılandırılan Windows VM'ler üzerinde şifrelemeyi etkinleştirme.
* İşletim sistemi ve veri şifreleme devre dışı bırakma Windows VM'ler için sürücüleri.
* Tüm kaynaklar (örneğin, anahtar kasası, depolama hesabı ve VM) hello olmalıdır aynı Azure bölgesinde ve abonelik.
* Standart katmanı VM'ler D, DS, G ve GS serisi VM'ler gibi.

Disk şifrelemesi senaryoları aşağıdaki hello şu anda desteklenmiyor:

* Temel katman VM'ler.
* Merhaba Klasik dağıtım modeli kullanılarak oluşturulan VM'ler.
* Merhaba şifreleme anahtarları zaten şifrelenmiş VM'de güncelleştiriliyor.
* Şirket içi anahtar yönetimi hizmeti ile tümleştirme.

## <a name="create-azure-key-vault-and-keys"></a>Azure anahtar kasası ve anahtarları oluşturma
Başlamadan önce o hello en son sürümünü hello Azure PowerShell modülünün yüklü emin olun. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Merhaba komut örnekleri tüm örnek parametreleri kendi adları, konum ve anahtar değerlerini değiştirin. Merhaba aşağıdaki örnekleri kullanmak, bir kural *myResourceGroup*, *myKeyVault*, *myVM*, vb..

Merhaba ilk adımı şifreleme anahtarlarınızı toocreate Azure anahtar kasası toostore değil. Azure anahtar kasası anahtarları, gizli depolayabilir veya toosecurely izin parolalar, uygulama ve hizmetlerinize uygulamadan. Sanal disk şifrelemesi için bir anahtar kasası toostore kullanılan tooencrypt bir şifreleme anahtarı oluşturun veya sanal diskleri şifresini. 

Azure aboneliğinizle içinde Hello Azure anahtar kasası sağlayıcısını etkinleştir [Register-AzureRmResourceProvider](/powershell/module/azurerm.resources/register-azurermresourceprovider), sahip bir kaynak grubu oluşturma [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup). Merhaba aşağıdaki örnekte oluşturur bir kaynak grubu adı *myResourceGroup* hello içinde *Doğu ABD* konumu:

```powershell
$rgName = "myResourceGroup"
$location = "East US"

Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.KeyVault"
New-AzureRmResourceGroup -Location $location -Name $rgName
```

depolama ve hello VM kendisini gibi kaynakları bulunmalıdır Hello Azure anahtar kasası içeren hello şifreleme anahtarlarını ve ilişkili işlem aynı bölgede hello. Bir Azure anahtar kasası ile oluşturma [New-AzureRmKeyVault](/powershell/module/azurerm.keyvault/new-azurermkeyvault) ve hello anahtar kasası disk şifrelemesi ile kullanılmak üzere etkinleştirin. İçin benzersiz bir anahtar kasası adı belirtmeniz *keyVaultName* gibi:

```powershell
$keyVaultName = "myUniqueKeyVaultName"
New-AzureRmKeyVault -Location $location `
    -ResourceGroupName $rgName `
    -VaultName $keyVaultName `
    -EnabledForDiskEncryption
```

Yazılım veya donanım güvenlik modeli (HSM) koruması kullanarak şifreleme anahtarlarını depolayabilirsiniz. HSM kullanmanın premium anahtar kasası gerektirir. Premium yazılım korumalı anahtarlar depolar standart anahtar kasası yerine anahtar kasası ek maliyet toocreating yoktur. toocreate adım önceki hello bir Premium'da anahtar kasası eklemek hello *- Sku "Premium"* parametreleri. Standart bir anahtar kasası oluşturduğumuz beri hello aşağıdaki örnek yazılım korumalı anahtarlar kullanır. 

Her iki koruma modelleri için erişim toorequest hello şifreleme anahtarları hello VM toodecrypt hello sanal diskler önyüklendiğinde verilen toobe hello Azure platformu gerekir. Anahtar kasası ile bir şifreleme anahtarı oluşturmak [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey). Merhaba aşağıdaki örnekte oluşturur adlı bir anahtar *myKey*:

```powershell
Add-AzureKeyVaultKey -VaultName $keyVaultName `
    -Name "myKey" `
    -Destination "Software"
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Azure Active Directory hizmet asıl Hello oluşturma
Sanal diskler şifrelenmiş veya şifresi olduğunda bir hesabı toohandle hello kimlik doğrulaması ve şifreleme anahtarlarının anahtar Kasası'ndan değişimi belirtin. Bu hesabı, bir Azure Active Directory hizmet asıl hello Azure platformu toorequest hello uygun şifreleme anahtarları hello VM adına izin verir. Birçok kuruluş Azure Active Directory dizinleri ayrılmış olsa, aboneliğinizde varsayılan Azure Active Directory örneği kullanılabilir.

Azure Active Directory ile bir hizmet sorumlusu oluşturma [yeni AzureRmADServicePrincipal](/powershell/module/azurerm.resources/new-azurermadserviceprincipal). toospecify güvenli bir parola izleyin hello [parola ilkeleri ve kısıtlamaları Azure Active Directory'de](../../active-directory/active-directory-passwords-policy.md):

```powershell
$appName = "My App"
$securePassword = "P@ssword!"
$app = New-AzureRmADApplication -DisplayName $appName `
    -HomePage "https://myapp.contoso.com" `
    -IdentifierUris "https://contoso.com/myapp" `
    -Password $securePassword
New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
```

toosuccessfully şifrelemek veya şifresini sanal diskler, anahtar kasasında depolanan hello şifreleme anahtarı üzerindeki izinleri kümesi toopermit hello Azure Active Directory hizmet asıl tooread hello anahtarları olmalıdır. Anahtar kasası ile üzerindeki izinleri ayarla [kümesi AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy):

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName $keyvaultName `
    -ServicePrincipalName $app.ApplicationId `
    -PermissionsToKeys "WrapKey" `
    -PermissionsToSecrets "Set"
```


## <a name="create-virtual-machine"></a>Sanal makine oluşturma
tootest Merhaba şifreleme işlemi, bir VM oluşturalım. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* kullanarak bir *Windows Server 2016 Datacenter* görüntü:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName `
    -Location $location `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress -ResourceGroupName $rgName `
    -Location $location `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "mypublicdns$(Get-Random)"

$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName `
    -Location $location `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface -Name myNic `
    -ResourceGroupName $rgName `
    -Location $location `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$cred = Get-Credential

$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vmConfig
```


## <a name="encrypt-virtual-machine"></a>Sanal makine şifrele
tooencrypt hello sanal diskler, tüm hello önceki bileşenleri birlikte getirin:

1. Hello Azure Active Directory hizmet asıl ve parola belirtin.
2. Şifrelenmiş disklerinizi Hello anahtar kasası toostore hello meta verileri belirtin.
3. Merhaba şifreleme anahtarları toouse hello gerçek şifreleme ve şifre çözme için belirtin.
4. Tooencrypt hello işletim sistemi diski, hello veri diskleri veya tüm isteyip istemediğinizi belirtin.

VM ile şifrelemek [kümesi AzureRmVMDiskEncryptionExtension](/powershell/module/azurerm.compute/set-azurermvmdiskencryptionextension) hello Azure anahtar kasası anahtar ve Azure Active Directory hizmet asıl kimlik bilgilerini kullanarak. Merhaba aşağıdaki örnekte tüm hello anahtar bilgilerini alır sonra hello adlı VM şifreler *myVM*:

```powershell
$keyVault = Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $rgName;
$diskEncryptionKeyVaultUrl = $keyVault.VaultUri;
$keyVaultResourceId = $keyVault.ResourceId;
$keyEncryptionKeyUrl = (Get-AzureKeyVaultKey -VaultName $keyVaultName -Name myKey).Key.kid;

Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $rgName `
    -VMName $vmName `
    -AadClientID $app.ApplicationId `
    -AadClientSecret $securePassword `
    -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl `
    -DiskEncryptionKeyVaultId $keyVaultResourceId `
    -KeyEncryptionKeyUrl $keyEncryptionKeyUrl `
    -KeyEncryptionKeyVaultId $keyVaultResourceId
```

Merhaba komut istemi toocontinue hello VM şifrelemeli kabul edin. Merhaba VM hello işlemi sırasında yeniden başlatır. Merhaba şifreleme işlemi tamamlandıktan sonra hello VM yeniden başlattı, hello şifreleme durumuna sahip gözden [Get-AzureRmVmDiskEncryptionStatus](/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus):

```powershell
Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $rgName -VMName $vmName
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```powershell
OsVolumeEncrypted          : Encrypted
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OsVolume: Encrypted, DataVolumes: Encrypted
```

## <a name="next-steps"></a>Sonraki adımlar
* Azure anahtar kasası yönetme hakkında daha fazla bilgi için bkz: [sanal makineler için anahtar kasasını oluşturup](key-vault-setup.md).
* Bir şifrelenmiş özel VM tooupload tooAzure, hazırlama gibi disk şifrelemesi hakkında daha fazla bilgi için bkz: [Azure Disk şifrelemesi](../../security/azure-security-disk-encryption.md).
