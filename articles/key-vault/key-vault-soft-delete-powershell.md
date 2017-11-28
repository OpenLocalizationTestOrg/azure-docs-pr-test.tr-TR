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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="c9bad-103">Nasıl toouse anahtar kasası soft-delete PowerShell ile</span><span class="sxs-lookup"><span data-stu-id="c9bad-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="c9bad-104">Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9bad-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="c9bad-105">Özellikle, soft-senaryoları aşağıdaki adresleri hello Sil:</span><span class="sxs-lookup"><span data-stu-id="c9bad-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="c9bad-106">Bir anahtar kasası kurtarılabilir silinmesini desteği</span><span class="sxs-lookup"><span data-stu-id="c9bad-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="c9bad-107">Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları</span><span class="sxs-lookup"><span data-stu-id="c9bad-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9bad-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c9bad-108">Prerequisites</span></span>

- <span data-ttu-id="c9bad-109">Azure PowerShell 4.0.0 veya yoksa zaten bu Kurulum, Azure PowerShell'i yükleme ve Azure aboneliğinizle ilişkilendirmek, daha sonra - bkz. [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9bad-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="c9bad-110">Yoktur, anahtar kasası PowerShell çıktı biçimlendirmesi eski bir sürümü dosya **olabilir** hello doğru sürümü yerine ortamınıza yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="c9bad-111">Biz PowerShell toocontain hello güncelleştirilmiş bir sürümünü düzeltme hello çıktı biçimlendirmesi için gereken bekleme ve bu konuda, o anda güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="c9bad-112">Merhaba geçerli geçici çözüm, karşılaştığınız biçimlendirme bu sorunu olan:</span><span class="sxs-lookup"><span data-stu-id="c9bad-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="c9bad-113">Sorgu değil gördüğünüz hello soft-delete fark ederseniz aşağıdaki kullanım hello bu konuda açıklanan özelliği etkin: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="c9bad-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="c9bad-114">Anahtar kasası belirli referans için PowerShell bilgi [Azure anahtar kasası PowerShell başvurusu](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="c9bad-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="c9bad-115">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="c9bad-115">Required permissions</span></span>

<span data-ttu-id="c9bad-116">Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:</span><span class="sxs-lookup"><span data-stu-id="c9bad-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="c9bad-117">İşlem</span><span class="sxs-lookup"><span data-stu-id="c9bad-117">Operation</span></span> | <span data-ttu-id="c9bad-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c9bad-118">Description</span></span> | <span data-ttu-id="c9bad-119">Kullanıcı izni</span><span class="sxs-lookup"><span data-stu-id="c9bad-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="c9bad-120">Liste</span><span class="sxs-lookup"><span data-stu-id="c9bad-120">List</span></span>|<span data-ttu-id="c9bad-121">Listeleri anahtar kasalarını silindi.</span><span class="sxs-lookup"><span data-stu-id="c9bad-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="c9bad-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="c9bad-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="c9bad-123">Kurtar</span><span class="sxs-lookup"><span data-stu-id="c9bad-123">Recover</span></span>|<span data-ttu-id="c9bad-124">Silinen bir anahtar kasası geri yükler.</span><span class="sxs-lookup"><span data-stu-id="c9bad-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="c9bad-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="c9bad-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="c9bad-126">Temizle</span><span class="sxs-lookup"><span data-stu-id="c9bad-126">Purge</span></span>|<span data-ttu-id="c9bad-127">Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="c9bad-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="c9bad-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="c9bad-129">İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c9bad-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="c9bad-130">Etkinleştirme soft-Sil</span><span class="sxs-lookup"><span data-stu-id="c9bad-130">Enabling soft-delete</span></span>

<span data-ttu-id="c9bad-131">Silinen bir anahtar kasası ya da bir anahtar olarak depolanan nesneler toobe mümkün toorecover kasa, önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="c9bad-132">Varolan anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="c9bad-132">Existing key vault</span></span>

<span data-ttu-id="c9bad-133">ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c9bad-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="c9bad-134">Şu anda toouse Azure Resource Manager kaynak işleme toodirectly yazma hello gereksiniminiz *enableSoftDelete* özelliği toohello anahtar kasası kaynak.</span><span class="sxs-lookup"><span data-stu-id="c9bad-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="c9bad-135">Yeni anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="c9bad-135">New key vault</span></span>

<span data-ttu-id="c9bad-136">Yeni bir anahtar kasası için geçici silmeyi etkinleştirme yapılır tooyour hello soft-delete etkinleştirme bayrağını ekleyerek oluşturma zamanında komutu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c9bad-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="c9bad-137">Soft-delete etkinleştirme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c9bad-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="c9bad-138">bir anahtar kasası soft-delete etkin olan tooverify çalışma hello *almak* komut ve Merhaba 'Yumuşak silme etkin?' arayın</span><span class="sxs-lookup"><span data-stu-id="c9bad-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="c9bad-139">özniteliği ve onun ayarı true veya false.</span><span class="sxs-lookup"><span data-stu-id="c9bad-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="c9bad-140">Soft-delete tarafından korunan bir anahtar kasasını silme</span><span class="sxs-lookup"><span data-stu-id="c9bad-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="c9bad-141">Merhaba komutu toodelete (veya kaldırma) bir anahtar kasası aynı ancak etkinleştirilip bağlı olarak, davranış değişiklikleri yumuşak veya silme hello kalır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="c9bad-142">Soft-delete etkin olmayan bir anahtar kasası için hello önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.</span><span class="sxs-lookup"><span data-stu-id="c9bad-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="c9bad-143">Soft-delete anahtar kasalarınıza nasıl korur</span><span class="sxs-lookup"><span data-stu-id="c9bad-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="c9bad-144">Soft-delete ile etkin:</span><span class="sxs-lookup"><span data-stu-id="c9bad-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="c9bad-145">Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu hello konumu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="c9bad-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="c9bad-146">Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş hello durumundayken bunu kalır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="c9bad-147">aynı ada sahip yeni bir anahtar kasası oluşturulamıyor şekilde hello DNS adı silinmiş bir durumda bir anahtar kasası için ayrılmış olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="c9bad-148">Merhaba aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c9bad-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="c9bad-149">Merhaba *kaynak kimliği* hello çıktı toohello özgün kaynak kimliği bu kasasının başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="c9bad-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="c9bad-150">Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok</span><span class="sxs-lookup"><span data-stu-id="c9bad-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="c9bad-151">Merhaba *kimliği* alan kurtarma ya da temizleme kullanılan tooidentify hello kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="c9bad-152">Merhaba *temizleme tarih zamanlanmış* alan gösterir hello kasası zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa.</span><span class="sxs-lookup"><span data-stu-id="c9bad-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="c9bad-153">Merhaba varsayılan saklama dönemi, kullanılan toocalculate hello *temizleme tarih zamanlanmış*, 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="c9bad-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="c9bad-154">Bir anahtar kasası kurtarma</span><span class="sxs-lookup"><span data-stu-id="c9bad-154">Recovering a key vault</span></span>

<span data-ttu-id="c9bad-155">toorecover bir anahtar kasası, toospecify hello anahtar kasası adı, kaynak grubunu ve konumu gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="c9bad-156">Bu bir anahtar kasası kurtarma işlemi için gerek duyduğunuz hello konum ve hello kaynak grubu silinmiş hello anahtar kasasının unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c9bad-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="c9bad-157">Bir anahtar kasası kurtarıldığında hello sonuç hello anahtar kasasının özgün kaynak kimliğiyle yeni bir kaynak değildir</span><span class="sxs-lookup"><span data-stu-id="c9bad-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="c9bad-158">Burada hello anahtar kasası var hello kaynak grubu kaldırdıysanız hello anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="c9bad-159">Anahtar kasası nesneleri ve soft-Sil</span><span class="sxs-lookup"><span data-stu-id="c9bad-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="c9bad-160">İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.</span><span class="sxs-lookup"><span data-stu-id="c9bad-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="c9bad-161">İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma.</span><span class="sxs-lookup"><span data-stu-id="c9bad-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="c9bad-162">Merhaba silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c9bad-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="c9bad-163">Örneğin, toorequest silinmiş toolist anahtarları bir anahtar Kasası'hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c9bad-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="c9bad-164">Durum geçişi</span><span class="sxs-lookup"><span data-stu-id="c9bad-164">Transition state</span></span> 

<span data-ttu-id="c9bad-165">Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, hello geçiş toocomplete birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="c9bad-166">Bu durum geçişi sırasında bu hello anahtarı hello etkin veya hello silinmiş durumda değil görünebilir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="c9bad-167">Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.</span><span class="sxs-lookup"><span data-stu-id="c9bad-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="c9bad-168">Anahtar kasası nesneleriyle Soft-delete kullanma</span><span class="sxs-lookup"><span data-stu-id="c9bad-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="c9bad-169">Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika too90 günlerini silinmiş durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="c9bad-170">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="c9bad-170">Keys</span></span>

<span data-ttu-id="c9bad-171">Silinen bir anahtar toorecover:</span><span class="sxs-lookup"><span data-stu-id="c9bad-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="c9bad-172">toopermanently bir anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="c9bad-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="c9bad-173">Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="c9bad-174">Merhaba **kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="c9bad-175">Kullanıcı veya hizmet asıl toobe mümkün tooexecute için bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları hello ilgili (anahtar veya gizli) Bu nesne için hello anahtar kasası erişim ilkesinde eylem.</span><span class="sxs-lookup"><span data-stu-id="c9bad-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="c9bad-176">Varsayılan olarak, hello **Temizleme** izni hello 'all' kısayol kullanılan toogrant olduğunda tooa anahtar kasasının erişim ilkesi eklenmez tüm izinleri tooa kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c9bad-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="c9bad-177">Açıkça vermelidir **Temizleme** izni.</span><span class="sxs-lookup"><span data-stu-id="c9bad-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="c9bad-178">Örneğin, aşağıdaki komut verir hello user@contoso.com izin tooperform anahtarlarında üzerinde çeşitli işlemler *ContosoVault* dahil olmak üzere **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="c9bad-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="c9bad-179">Bir anahtar kasası erişim ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="c9bad-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="c9bad-180">Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="c9bad-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="c9bad-181">Gizli Diziler</span><span class="sxs-lookup"><span data-stu-id="c9bad-181">Secrets</span></span>

<span data-ttu-id="c9bad-182">Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="c9bad-183">Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için hello komutlardır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="c9bad-184">SQLPassword adlı bir gizli anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="c9bad-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="c9bad-185">Tüm silinen gizli bir anahtar kasasına listesi:</span><span class="sxs-lookup"><span data-stu-id="c9bad-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="c9bad-186">Bir gizli anahtar hello silinmiş durumda kurtarma:</span><span class="sxs-lookup"><span data-stu-id="c9bad-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="c9bad-187">Bir gizli anahtar silinmiş durumda temizleme:</span><span class="sxs-lookup"><span data-stu-id="c9bad-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="c9bad-188">Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="c9bad-189">Temizleme ve anahtar kasalarını</span><span class="sxs-lookup"><span data-stu-id="c9bad-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="c9bad-190">Anahtar kasası nesneleri</span><span class="sxs-lookup"><span data-stu-id="c9bad-190">Key vault objects</span></span>

<span data-ttu-id="c9bad-191">Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="c9bad-192">Merhaba anahtar Kasası'nda tüm diğer nesnelerin gibi hello Silinmiş nesne içeriyor hello anahtar kasası ancak değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="c9bad-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="c9bad-193">Anahtar kapsayıcıları kasaları</span><span class="sxs-lookup"><span data-stu-id="c9bad-193">Key vaults as containers</span></span>
<span data-ttu-id="c9bad-194">Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="c9bad-195">toopurge bir anahtar kasası kullanan hello `Remove-AzureRmKeyVault` hello seçeneğiyle komut `-InRemovedState` ve Silinen hello anahtar kasası hello konumu ile Merhaba belirterek `-Location location` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="c9bad-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="c9bad-196">Merhaba komutunu kullanarak silinmiş bir kasa hello konumunu bulabilirsiniz `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="c9bad-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="c9bad-197">Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="c9bad-198">Gerekli izinler Temizle</span><span class="sxs-lookup"><span data-stu-id="c9bad-198">Purge permissions required</span></span>
- <span data-ttu-id="c9bad-199">toopurge silinmiş bir anahtar kasası, hello kasası ve tüm içeriğini kalıcı olarak kaldırılır şekilde hello kullanıcının ihtiyacı RBAC izni tooperform bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi.</span><span class="sxs-lookup"><span data-stu-id="c9bad-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="c9bad-200">toolist silinmiş hello anahtar hello kasası kullanıcı gereken RBAC izni tooperform *Microsoft.KeyVault/deletedVaults/read* izni.</span><span class="sxs-lookup"><span data-stu-id="c9bad-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="c9bad-201">Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="c9bad-202">Zamanlanmış temizleme</span><span class="sxs-lookup"><span data-stu-id="c9bad-202">Scheduled purge</span></span>

<span data-ttu-id="c9bad-203">Silinen anahtar kasası nesneleri listeleme anahtar kasası tarafından temizlendi schedled toobe olduklarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="c9bad-204">Merhaba *temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="c9bad-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="c9bad-205">Varsayılan olarak, silinen anahtar kasası nesne hello saklama süresi 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="c9bad-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="c9bad-206">Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="c9bad-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="c9bad-207">Kurtarılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="c9bad-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="c9bad-208">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c9bad-208">Other resources</span></span>

- <span data-ttu-id="c9bad-209">Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="c9bad-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="c9bad-210">Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c9bad-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

