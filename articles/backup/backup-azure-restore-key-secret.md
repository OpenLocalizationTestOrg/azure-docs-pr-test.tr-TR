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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Anahtar kasası anahtarı ve gizli Azure Yedekleme kullanılarak şifrelenmiş VM'ler için geri yükleme
Anahtarı ve gizli hello anahtar kasasına yoksa, bu makalede Azure VM Backup tooperform geri şifrelenmiş Azure sanal makineleri kullanma hakkında alınmaktadır. Bu adımları toomaintain anahtarı (anahtar şifreleme anahtarı) ayrı bir kopyasını istiyorsanız ve VM hello için gizli anahtar (BitLocker şifreleme anahtarı) geri de kullanılabilir.

## <a name="prerequisites"></a>Ön koşullar
* **Yedekleme şifrelenmiş VM'ler** - şifrelenmiş Azure VM'ler yedeklenmiş Azure Yedekleme'yi kullanarak. Merhaba makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md) nasıl toobackup Azure VM'ler şifrelenmiş hakkında ayrıntılar için.
* **Azure anahtar kasası yapılandırma** – bu anahtar kasası toowhich anahtarları emin olun ve gizli anahtarları gerek toobe geri zaten mevcut. Merhaba makalesine başvurun [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md) anahtar kasası yönetimi hakkında ayrıntılar için.
* **Diski geri** -şifrelenmiş VM kullanma diskleri geri yüklemek için geri yükleme işi tetiklemesi olun [PowerShell adımları](backup-azure-vms-automation.md#restore-an-azure-vm). Bu durum, bu iş, anahtarları ve gizli anahtarları geri şifrelenmiş hello VM toobe için içeren depolama hesabınızdaki bir JSON dosyası oluşturur. çünkü.

## <a name="get-key-and-secret-from-azure-backup"></a>Azure yedeklemeden anahtarı ve gizli anahtarı alma

> [!NOTE]
> VM Hello şifrelenmiş için disk geri yüklendikten sonra emin olun:
> 1. $details bölümünde belirtildiği gibi geri yükleme disk iş ayrıntılarla doldurulmuş [PowerShell adımları geri yükleme hello disk bölümü](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. VM yalnızca geri yüklenen disklerden oluşturulmalıdır **anahtarı ve gizli tamamlandıktan sonra geri yüklenen tookey kasa**.
>
>

Sorgu hello hello iş ayrıntılarını disk özelliklerini geri.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Hello Azure depolama bağlamını ayarlayın ve şifrelenmiş VM için anahtarı ve gizli bilgi içeren JSON yapılandırma dosyası geri yükleme.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Anahtarı geri yükleme
Yukarıda belirtilen hello hedef yolunda Hello JSON dosyası oluşturulduktan sonra hello JSON anahtar blob dosyası oluşturun ve hello anahtar kasasına toorestore anahtar cmdlet tooput hello anahtarı (KEK) akış.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Gizli anahtarı geri yükleme
Merhaba JSON dosyasını kullan tooget gizli ad ve değer oluşturulan ve hello anahtar kasasına tooset gizli cmdlet tooput hello gizli (BEK) akış. **VM BEK ve KEK kullanılarak şifrelenir bu cmdlet'leri kullanın.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

VM ise **BEK yalnızca kullanılarak şifrelenmiş**, JSON hello gizli blob dosyası oluşturun ve hello anahtar kasasına toorestore gizli cmdlet tooput hello gizli (BEK) akış.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. $Secretname değeri $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl toohello çıktısını başvuran ve sonra gizli metin kullanarak elde edilebilir / ör https://keyvaultname.vault.azure.net/secrets/ çıkış gizli URL'si B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 ve gizli adıdır, B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Merhaba etiketi DiskEncryptionKeyFileName gizli adıyla aynı değeridir.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Geri yüklenen disk, sanal makine oluşturma
Azure VM Backup kullanılarak şifrelenmiş VM yedeklediyseniz, hello PowerShell cmdlet'leri anahtarı ve gizli geri toohello anahtar kasası geri Yardım bahsedilen. Bunları geri yükledikten sonra hello makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate şifrelenmiş VM'ler geri yüklenen disk, anahtarı ve gizli anahtarı.

## <a name="legacy-approach"></a>Eski yaklaşımı
Yukarıda belirtilen hello yaklaşım tüm hello kurtarma noktaları için çalışır. Ancak, hello anahtarı ve gizli bilgileri kurtarma noktasından alma eski yaklaşım olacaktır 11 Temmuz 2017 BEK ve KEK kullanılarak şifrelenmiş VM'ler için daha eski kurtarma noktaları için geçerlidir. Geri Yükleme disk işi tamamlandığında VM şifrelenmiş kullanmak için [PowerShell adımları](backup-azure-vms-automation.md#restore-an-azure-vm), $rp geçerli bir değerle doldurulur emin olun.

### <a name="restore-key"></a>Anahtarı geri yükleme
Merhaba anahtar kasasına geri toorestore anahtar cmdlet tooput akış ve kurtarma noktasından aşağıdaki cmdlet'leri tooget anahtarı (KEK) bilgilerle hello kullanın.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Gizli anahtarı geri yükleme
Merhaba anahtar kasasına geri tooset gizli cmdlet tooput akış ve kurtarma noktasından aşağıdaki cmdlet'leri tooget gizli (BEK) bilgilerle hello kullanın.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. $Secretname için değer $rp1 toohello çıktısını başvurarak elde edilebilir. KeyAndSecretDetails.SecretUrl ve sonra gizli metni kullanarak / Örneğin çıkış gizli URL'si https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 ve gizli anahtar adı B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Merhaba etiketi DiskEncryptionKeyFileName gizli adıyla aynı değeridir.
> 3. DiskEncryptionKeyEncryptionKeyURL değeri elde edilebilir anahtar Kasası'nı kullanarak ve geri hello anahtarları geri yükleniyor sonra [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet'i
>
>

## <a name="next-steps"></a>Sonraki adımlar
Anahtarı ve gizli geri tookey kasa geri yükledikten sonra hello makalesine başvurun [yönetmek yedekleme ve geri yükleme Azure PowerShell kullanarak VM'lerin](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate şifrelenmiş VM'ler geri yüklenen disk, anahtarı ve gizli anahtarı.
