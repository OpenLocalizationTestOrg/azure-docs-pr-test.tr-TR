---
title: "aaaRestore anahtar kasası anahtarı ve gizli anahtarı için şifrelenmiş Azure Yedekleme'yi kullanarak sanal makineleri | Microsoft Docs"
description: "Bilgi toorestore anahtar kasası nasıl anahtarı ve gizli Azure PowerShell kullanarak yedekleme"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="13cbf-103">Anahtar kasası anahtarı ve gizli Azure Yedekleme kullanılarak şifrelenmiş VM'ler için geri yükleme</span><span class="sxs-lookup"><span data-stu-id="13cbf-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="13cbf-104">Anahtarı ve gizli hello anahtar kasasına yoksa, bu makalede Azure VM Backup tooperform geri şifrelenmiş Azure sanal makineleri kullanma hakkında alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="13cbf-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="13cbf-105">Bu adımları toomaintain anahtarı (anahtar şifreleme anahtarı) ayrı bir kopyasını istiyorsanız ve VM hello için gizli anahtar (BitLocker şifreleme anahtarı) geri de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="13cbf-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13cbf-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="13cbf-106">Prerequisites</span></span>
* <span data-ttu-id="13cbf-107">**Yedekleme şifrelenmiş VM'ler** - şifrelenmiş Azure VM'ler yedeklenmiş Azure Yedekleme'yi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="13cbf-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="13cbf-108">Merhaba makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md) nasıl toobackup Azure VM'ler şifrelenmiş hakkında ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="13cbf-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="13cbf-109">**Azure anahtar kasası yapılandırma** – bu anahtar kasası toowhich anahtarları emin olun ve gizli anahtarları gerek toobe geri zaten mevcut.</span><span class="sxs-lookup"><span data-stu-id="13cbf-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="13cbf-110">Merhaba makalesine başvurun [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md) anahtar kasası yönetimi hakkında ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="13cbf-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="13cbf-111">**Diski geri** -şifrelenmiş VM kullanma diskleri geri yüklemek için geri yükleme işi tetiklemesi olun [PowerShell adımları](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="13cbf-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="13cbf-112">Bu durum, bu iş, anahtarları ve gizli anahtarları geri şifrelenmiş hello VM toobe için içeren depolama hesabınızdaki bir JSON dosyası oluşturur. çünkü.</span><span class="sxs-lookup"><span data-stu-id="13cbf-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="13cbf-113">Azure yedeklemeden anahtarı ve gizli anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="13cbf-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="13cbf-114">VM Hello şifrelenmiş için disk geri yüklendikten sonra emin olun:</span><span class="sxs-lookup"><span data-stu-id="13cbf-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="13cbf-115">$details bölümünde belirtildiği gibi geri yükleme disk iş ayrıntılarla doldurulmuş [PowerShell adımları geri yükleme hello disk bölümü](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="13cbf-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="13cbf-116">VM yalnızca geri yüklenen disklerden oluşturulmalıdır **anahtarı ve gizli tamamlandıktan sonra geri yüklenen tookey kasa**.</span><span class="sxs-lookup"><span data-stu-id="13cbf-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="13cbf-117">Sorgu hello hello iş ayrıntılarını disk özelliklerini geri.</span><span class="sxs-lookup"><span data-stu-id="13cbf-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="13cbf-118">Hello Azure depolama bağlamını ayarlayın ve şifrelenmiş VM için anahtarı ve gizli bilgi içeren JSON yapılandırma dosyası geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="13cbf-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="13cbf-119">Anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="13cbf-119">Restore key</span></span>
<span data-ttu-id="13cbf-120">Yukarıda belirtilen hello hedef yolunda Hello JSON dosyası oluşturulduktan sonra hello JSON anahtar blob dosyası oluşturun ve hello anahtar kasasına toorestore anahtar cmdlet tooput hello anahtarı (KEK) akış.</span><span class="sxs-lookup"><span data-stu-id="13cbf-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="13cbf-121">Gizli anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="13cbf-121">Restore secret</span></span>
<span data-ttu-id="13cbf-122">Merhaba JSON dosyasını kullan tooget gizli ad ve değer oluşturulan ve hello anahtar kasasına tooset gizli cmdlet tooput hello gizli (BEK) akış.</span><span class="sxs-lookup"><span data-stu-id="13cbf-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="13cbf-123">**VM BEK ve KEK kullanılarak şifrelenir bu cmdlet'leri kullanın.**</span><span class="sxs-lookup"><span data-stu-id="13cbf-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="13cbf-124">VM ise **BEK yalnızca kullanılarak şifrelenmiş**, JSON hello gizli blob dosyası oluşturun ve hello anahtar kasasına toorestore gizli cmdlet tooput hello gizli (BEK) akış.</span><span class="sxs-lookup"><span data-stu-id="13cbf-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="13cbf-125">$Secretname değeri $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl toohello çıktısını başvuran ve sonra gizli metin kullanarak elde edilebilir / ör https://keyvaultname.vault.azure.net/secrets/ çıkış gizli URL'si B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 ve gizli adıdır, B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="13cbf-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="13cbf-126">Merhaba etiketi DiskEncryptionKeyFileName gizli adıyla aynı değeridir.</span><span class="sxs-lookup"><span data-stu-id="13cbf-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="13cbf-127">Geri yüklenen disk, sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="13cbf-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="13cbf-128">Azure VM Backup kullanılarak şifrelenmiş VM yedeklediyseniz, hello PowerShell cmdlet'leri anahtarı ve gizli geri toohello anahtar kasası geri Yardım bahsedilen.</span><span class="sxs-lookup"><span data-stu-id="13cbf-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="13cbf-129">Bunları geri yükledikten sonra hello makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate şifrelenmiş VM'ler geri yüklenen disk, anahtarı ve gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="13cbf-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="13cbf-130">Eski yaklaşımı</span><span class="sxs-lookup"><span data-stu-id="13cbf-130">Legacy approach</span></span>
<span data-ttu-id="13cbf-131">Yukarıda belirtilen hello yaklaşım tüm hello kurtarma noktaları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="13cbf-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="13cbf-132">Ancak, hello anahtarı ve gizli bilgileri kurtarma noktasından alma eski yaklaşım olacaktır 11 Temmuz 2017 BEK ve KEK kullanılarak şifrelenmiş VM'ler için daha eski kurtarma noktaları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="13cbf-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="13cbf-133">Geri Yükleme disk işi tamamlandığında VM şifrelenmiş kullanmak için [PowerShell adımları](backup-azure-vms-automation.md#restore-an-azure-vm), $rp geçerli bir değerle doldurulur emin olun.</span><span class="sxs-lookup"><span data-stu-id="13cbf-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="13cbf-134">Anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="13cbf-134">Restore key</span></span>
<span data-ttu-id="13cbf-135">Merhaba anahtar kasasına geri toorestore anahtar cmdlet tooput akış ve kurtarma noktasından aşağıdaki cmdlet'leri tooget anahtarı (KEK) bilgilerle hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cbf-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="13cbf-136">Gizli anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="13cbf-136">Restore secret</span></span>
<span data-ttu-id="13cbf-137">Merhaba anahtar kasasına geri tooset gizli cmdlet tooput akış ve kurtarma noktasından aşağıdaki cmdlet'leri tooget gizli (BEK) bilgilerle hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="13cbf-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="13cbf-138">$Secretname için değer $rp1 toohello çıktısını başvurarak elde edilebilir. KeyAndSecretDetails.SecretUrl ve sonra gizli metni kullanarak / Örneğin çıkış gizli URL'si https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 ve gizli anahtar adı B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="13cbf-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="13cbf-139">Merhaba etiketi DiskEncryptionKeyFileName gizli adıyla aynı değeridir.</span><span class="sxs-lookup"><span data-stu-id="13cbf-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="13cbf-140">DiskEncryptionKeyEncryptionKeyURL değeri elde edilebilir anahtar Kasası'nı kullanarak ve geri hello anahtarları geri yükleniyor sonra [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="13cbf-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="13cbf-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13cbf-141">Next steps</span></span>
<span data-ttu-id="13cbf-142">Anahtarı ve gizli geri tookey kasa geri yükledikten sonra hello makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate şifrelenmiş VM'ler geri yüklenen disk, anahtarı ve gizli anahtarı.</span><span class="sxs-lookup"><span data-stu-id="13cbf-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
