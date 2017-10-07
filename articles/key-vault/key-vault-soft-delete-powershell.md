---
ms.assetid: 
title: "aaaAzure anahtar kasası - nasıl toouse soft-delete PowerShell ile"
description: "Kullanım örneği soft-delete PowerShell kod parçalarını ile örnekleri"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Nasıl toouse anahtar kasası soft-delete PowerShell ile

Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar. Özellikle, soft-senaryoları aşağıdaki adresleri hello Sil:

- Bir anahtar kasası kurtarılabilir silinmesini desteği
- Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları

## <a name="prerequisites"></a>Ön koşullar

- Azure PowerShell 4.0.0 veya yoksa zaten bu Kurulum, Azure PowerShell'i yükleme ve Azure aboneliğinizle ilişkilendirmek, daha sonra - bkz. [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Yoktur, anahtar kasası PowerShell çıktı biçimlendirmesi eski bir sürümü dosya **olabilir** hello doğru sürümü yerine ortamınıza yüklü olmalıdır. Biz PowerShell toocontain hello güncelleştirilmiş bir sürümünü düzeltme hello çıktı biçimlendirmesi için gereken bekleme ve bu konuda, o anda güncelleştirir. Merhaba geçerli geçici çözüm, karşılaştığınız biçimlendirme bu sorunu olan:
> - Sorgu değil gördüğünüz hello soft-delete fark ederseniz aşağıdaki kullanım hello bu konuda açıklanan özelliği etkin: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Anahtar kasası belirli referans için PowerShell bilgi [Azure anahtar kasası PowerShell başvurusu](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Gerekli izinler

Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:

| İşlem | Açıklama | Kullanıcı izni |
|:--|:--|:--|
|Liste|Listeleri anahtar kasalarını silindi.|Microsoft.KeyVault/deletedVaults/read|
|Kurtar|Silinen bir anahtar kasası geri yükler.|Microsoft.KeyVault/vaults/write|
|Temizle|Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Etkinleştirme soft-Sil

Silinen bir anahtar kasası ya da bir anahtar olarak depolanan nesneler toobe mümkün toorecover kasa, önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.

### <a name="existing-key-vault"></a>Varolan anahtar kasası

ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin. 

>[!NOTE]
>Şu anda toouse Azure Resource Manager kaynak işleme toodirectly yazma hello gereksiniminiz *enableSoftDelete* özelliği toohello anahtar kasası kaynak.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Yeni anahtar kasası

Yeni bir anahtar kasası için geçici silmeyi etkinleştirme yapılır tooyour hello soft-delete etkinleştirme bayrağını ekleyerek oluşturma zamanında komutu oluşturun.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Soft-delete etkinleştirme doğrulayın

bir anahtar kasası soft-delete etkin olan tooverify çalışma hello *almak* komut ve Merhaba 'Yumuşak silme etkin?' arayın özniteliği ve onun ayarı true veya false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Soft-delete tarafından korunan bir anahtar kasasını silme

Merhaba komutu toodelete (veya kaldırma) bir anahtar kasası aynı ancak etkinleştirilip bağlı olarak, davranış değişiklikleri yumuşak veya silme hello kalır.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Soft-delete etkin olmayan bir anahtar kasası için hello önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Soft-delete anahtar kasalarınıza nasıl korur

Soft-delete ile etkin:

- Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu hello konumu ile ilişkili. 
- Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş hello durumundayken bunu kalır. 
- aynı ada sahip yeni bir anahtar kasası oluşturulamıyor şekilde hello DNS adı silinmiş bir durumda bir anahtar kasası için ayrılmış olarak kalır.  

Merhaba aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Merhaba *kaynak kimliği* hello çıktı toohello özgün kaynak kimliği bu kasasının başvuruyor. Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok Merhaba *kimliği* alan kurtarma ya da temizleme kullanılan tooidentify hello kaynak olabilir. Merhaba *temizleme tarih zamanlanmış* alan gösterir hello kasası zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa. Merhaba varsayılan saklama dönemi, kullanılan toocalculate hello *temizleme tarih zamanlanmış*, 90 gündür.

## <a name="recovering-a-key-vault"></a>Bir anahtar kasası kurtarma

toorecover bir anahtar kasası, toospecify hello anahtar kasası adı, kaynak grubunu ve konumu gerekir. Bu bir anahtar kasası kurtarma işlemi için gerek duyduğunuz hello konum ve hello kaynak grubu silinmiş hello anahtar kasasının unutmayın.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Bir anahtar kasası kurtarıldığında hello sonuç hello anahtar kasasının özgün kaynak kimliğiyle yeni bir kaynak değildir Burada hello anahtar kasası var hello kaynak grubu kaldırdıysanız hello anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.

## <a name="key-vault-objects-and-soft-delete"></a>Anahtar kasası nesneleri ve soft-Sil

İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma. Merhaba silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur. 

Örneğin, toorequest silinmiş toolist anahtarları bir anahtar Kasası'hello aşağıdaki komutu kullanın:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Durum geçişi 

Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, hello geçiş toocomplete birkaç saniye sürebilir. Bu durum geçişi sırasında bu hello anahtarı hello etkin veya hello silinmiş durumda değil görünebilir. Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Anahtar kasası nesneleriyle Soft-delete kullanma

Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika too90 günlerini silinmiş durumda kalır. 

#### <a name="keys"></a>Anahtarlar

Silinen bir anahtar toorecover:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently bir anahtarı silin:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

Merhaba **kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir. Kullanıcı veya hizmet asıl toobe mümkün tooexecute için bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları hello ilgili (anahtar veya gizli) Bu nesne için hello anahtar kasası erişim ilkesinde eylem. Varsayılan olarak, hello **Temizleme** izni hello 'all' kısayol kullanılan toogrant olduğunda tooa anahtar kasasının erişim ilkesi eklenmez tüm izinleri tooa kullanıcı. Açıkça vermelidir **Temizleme** izni. Örneğin, aşağıdaki komut verir hello user@contoso.com izin tooperform anahtarlarında üzerinde çeşitli işlemler *ContosoVault* dahil olmak üzere **Temizleme**.

#### <a name="set-a-key-vault-access-policy"></a>Bir anahtar kasası erişim ilkesi ayarlama

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.

#### <a name="secrets"></a>Gizli Diziler

Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir. Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için hello komutlardır.

- SQLPassword adlı bir gizli anahtarı silin: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Tüm silinen gizli bir anahtar kasasına listesi: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Bir gizli anahtar hello silinmiş durumda kurtarma: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Bir gizli anahtar silinmiş durumda temizleme: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

## <a name="purging-and-key-vaults"></a>Temizleme ve anahtar kasalarını

### <a name="key-vault-objects"></a>Anahtar kasası nesneleri

Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir. Merhaba anahtar Kasası'nda tüm diğer nesnelerin gibi hello Silinmiş nesne içeriyor hello anahtar kasası ancak değişmeden kalır. 

### <a name="key-vaults-as-containers"></a>Anahtar kapsayıcıları kasaları
Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir. toopurge bir anahtar kasası kullanan hello `Remove-AzureRmKeyVault` hello seçeneğiyle komut `-InRemovedState` ve Silinen hello anahtar kasası hello konumu ile Merhaba belirterek `-Location location` bağımsız değişkeni. Merhaba komutunu kullanarak silinmiş bir kasa hello konumunu bulabilirsiniz `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.

### <a name="purge-permissions-required"></a>Gerekli izinler Temizle
- toopurge silinmiş bir anahtar kasası, hello kasası ve tüm içeriğini kalıcı olarak kaldırılır şekilde hello kullanıcının ihtiyacı RBAC izni tooperform bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi. 
- toolist silinmiş hello anahtar hello kasası kullanıcı gereken RBAC izni tooperform *Microsoft.KeyVault/deletedVaults/read* izni. 
- Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir. 

### <a name="scheduled-purge"></a>Zamanlanmış temizleme

Silinen anahtar kasası nesneleri listeleme anahtar kasası tarafından temizlendi schedled toobe olduklarında gösterir. Merhaba *temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı. Varsayılan olarak, silinen anahtar kasası nesne hello saklama süresi 90 gündür.

>[!NOTE]
>Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir. Kurtarılabilir değil.

## <a name="other-resources"></a>Diğer kaynaklar

- Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).
- Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).

