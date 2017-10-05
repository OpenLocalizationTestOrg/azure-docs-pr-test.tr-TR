---
ms.assetid: 
title: "Azure anahtar kasası - soft-delete PowerShell ile kullanma"
description: "Kullanım örneği soft-delete PowerShell kod parçalarını ile örnekleri"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="8f6b4-103">Anahtar kasası soft-delete PowerShell ile kullanma</span><span class="sxs-lookup"><span data-stu-id="8f6b4-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="8f6b4-104">Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="8f6b4-105">Özellikle, soft-adresleri aşağıdaki senaryolarda Sil:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="8f6b4-106">Bir anahtar kasası kurtarılabilir silinmesini desteği</span><span class="sxs-lookup"><span data-stu-id="8f6b4-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="8f6b4-107">Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları</span><span class="sxs-lookup"><span data-stu-id="8f6b4-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f6b4-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8f6b4-108">Prerequisites</span></span>

- <span data-ttu-id="8f6b4-109">Azure PowerShell 4.0.0 veya yoksa zaten bu Kurulum, Azure PowerShell'i yükleme ve Azure aboneliğinizle ilişkilendirmek, daha sonra - bkz. [Azure PowerShell'i yükleme ve yapılandırma nasıl](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8f6b4-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="8f6b4-110">Yoktur, anahtar kasası PowerShell çıktı biçimlendirmesi eski bir sürümü dosya **olabilir** doğru sürümü yerine ortamınıza yüklü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="8f6b4-111">Biz PowerShell çıktıyı biçimlendirmek için gereken düzeltme içerecek şekilde güncelleştirilmiş bir sürümünü bekleme ve bu konuda, o anda güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="8f6b4-112">Geçerli geçici çözüm bu biçimlendirme sorunla karşılaştığınızda değil:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="8f6b4-113">Aşağıdaki sorgu değil gördüğünüz soft-delete fark ederseniz bu konuda açıklanan özelliği etkin kullanın: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="8f6b4-114">Anahtar kasası belirli referans için PowerShell bilgi [Azure anahtar kasası PowerShell başvurusu](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="8f6b4-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="8f6b4-115">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="8f6b4-115">Required permissions</span></span>

<span data-ttu-id="8f6b4-116">Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="8f6b4-117">İşlem</span><span class="sxs-lookup"><span data-stu-id="8f6b4-117">Operation</span></span> | <span data-ttu-id="8f6b4-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8f6b4-118">Description</span></span> | <span data-ttu-id="8f6b4-119">Kullanıcı izni</span><span class="sxs-lookup"><span data-stu-id="8f6b4-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="8f6b4-120">Liste</span><span class="sxs-lookup"><span data-stu-id="8f6b4-120">List</span></span>|<span data-ttu-id="8f6b4-121">Listeleri anahtar kasalarını silindi.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="8f6b4-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="8f6b4-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="8f6b4-123">Kurtar</span><span class="sxs-lookup"><span data-stu-id="8f6b4-123">Recover</span></span>|<span data-ttu-id="8f6b4-124">Silinen bir anahtar kasası geri yükler.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="8f6b4-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="8f6b4-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="8f6b4-126">Temizle</span><span class="sxs-lookup"><span data-stu-id="8f6b4-126">Purge</span></span>|<span data-ttu-id="8f6b4-127">Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="8f6b4-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="8f6b4-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="8f6b4-129">İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8f6b4-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="8f6b4-130">Etkinleştirme soft-Sil</span><span class="sxs-lookup"><span data-stu-id="8f6b4-130">Enabling soft-delete</span></span>

<span data-ttu-id="8f6b4-131">Silinen bir anahtar kasası veya anahtar kasasında depolanan nesneler kurtarmanız mümkün olması için önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="8f6b4-132">Varolan anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="8f6b4-132">Existing key vault</span></span>

<span data-ttu-id="8f6b4-133">ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="8f6b4-134">Doğrudan yazmak için Azure Resource Manager kaynak işleme kullanmanıza gerek şu anda *enableSoftDelete* anahtar kasası kaynak özelliğine.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="8f6b4-135">Yeni anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="8f6b4-135">New key vault</span></span>

<span data-ttu-id="8f6b4-136">Yeni bir anahtar kasası için geçici silmeyi etkinleştirme oluşturma zamanında soft-delete etkinleştirme bayrağını ekleyerek yapılır, bir komut oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="8f6b4-137">Soft-delete etkinleştirme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8f6b4-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="8f6b4-138">Bir anahtar kasası soft-delete etkin olduğunu doğrulamak için çalıştırın *almak* komut ve 'yumuşak silmek için etkin?' arayın</span><span class="sxs-lookup"><span data-stu-id="8f6b4-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="8f6b4-139">özniteliği ve onun ayarı true veya false.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="8f6b4-140">Soft-delete tarafından korunan bir anahtar kasasını silme</span><span class="sxs-lookup"><span data-stu-id="8f6b4-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="8f6b4-141">Bir anahtar kasasını silme (veya kaldırma için) komutu aynı kalır, ancak davranışını olup soft-delete veya etkinleştirdiğiniz bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="8f6b4-142">Soft-delete etkin olmayan bir anahtar kasası için önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="8f6b4-143">Soft-delete anahtar kasalarınıza nasıl korur</span><span class="sxs-lookup"><span data-stu-id="8f6b4-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="8f6b4-144">Soft-delete ile etkin:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="8f6b4-145">Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu konumu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="8f6b4-146">Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş durumda olsa da bunu kalır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="8f6b4-147">Silinmiş bir durumda bir anahtar kasası için DNS adını hala aynı ada sahip yeni bir anahtar kasası oluşturulamıyor için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="8f6b4-148">Aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

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

<span data-ttu-id="8f6b4-149">*Kaynak kimliği* çıktıda bu kasaya özgün kaynak Kimliğine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="8f6b4-150">Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok</span><span class="sxs-lookup"><span data-stu-id="8f6b4-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="8f6b4-151">*Kimliği* alan, Kurtarma ya da temizleme kaynağı tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="8f6b4-152">*Temizleme tarih zamanlanmış* alan gösterir kasanın ne zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="8f6b4-153">Hesaplamak için kullanılan varsayılan saklama dönemi *temizleme tarih zamanlanmış*, 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="8f6b4-154">Bir anahtar kasası kurtarma</span><span class="sxs-lookup"><span data-stu-id="8f6b4-154">Recovering a key vault</span></span>

<span data-ttu-id="8f6b4-155">Bir anahtar kasası kurtarmak için anahtar kasası adı, kaynak grubunu ve konumu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="8f6b4-156">Bu bir anahtar kasası kurtarma işlemi için gereken konum ve silinen anahtar kasasının kaynak grubu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="8f6b4-157">Bir anahtar kasası kurtarıldığında, yeni bir kaynak anahtar kasasının özgün kaynak kimliğiyle oluşur</span><span class="sxs-lookup"><span data-stu-id="8f6b4-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="8f6b4-158">Burada anahtar kasası varolan kaynak grubu kaldırdıysanız anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="8f6b4-159">Anahtar kasası nesneleri ve soft-Sil</span><span class="sxs-lookup"><span data-stu-id="8f6b4-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="8f6b4-160">İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="8f6b4-161">İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="8f6b4-162">Silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="8f6b4-163">Örneğin, bir anahtar kasası silinmiş listesi anahtarlarında istemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="8f6b4-164">Durum geçişi</span><span class="sxs-lookup"><span data-stu-id="8f6b4-164">Transition state</span></span> 

<span data-ttu-id="8f6b4-165">Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, geçişi tamamlamak için birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="8f6b4-166">Bu geçiş aşamasında, anahtarı etkin veya silinmiş durumda değil görünebilir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="8f6b4-167">Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="8f6b4-168">Anahtar kasası nesneleriyle Soft-delete kullanma</span><span class="sxs-lookup"><span data-stu-id="8f6b4-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="8f6b4-169">Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika silinmiş durumda 90 gün boyunca kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="8f6b4-170">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="8f6b4-170">Keys</span></span>

<span data-ttu-id="8f6b4-171">Silinen bir anahtarı kurtarmak için:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="8f6b4-172">Bir anahtar kalıcı olarak silmek için:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="8f6b4-173">Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="8f6b4-174">**Kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="8f6b4-175">Bir kullanıcı veya hizmet sorumlusu yürütmek bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları ilgili (anahtar veya gizli) Bu nesne için anahtar kasası erişim ilkesinde eylem.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="8f6b4-176">Varsayılan olarak, **Temizleme** izni 'all' kısayol bir kullanıcı için tüm izinleri vermek için kullanıldığında, bir anahtar kasasının erişim ilkesine eklenmez.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="8f6b4-177">Açıkça vermelidir **Temizleme** izni.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="8f6b4-178">Örneğin, aşağıdaki verir komut user@contoso.com anahtarlarında çeşitli işlemleri gerçekleştirmek için izni *ContosoVault* dahil olmak üzere **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="8f6b4-179">Bir anahtar kasası erişim ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="8f6b4-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="8f6b4-180">Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="8f6b4-181">Gizli Diziler</span><span class="sxs-lookup"><span data-stu-id="8f6b4-181">Secrets</span></span>

<span data-ttu-id="8f6b4-182">Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="8f6b4-183">Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için komutlardır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="8f6b4-184">SQLPassword adlı bir gizli anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="8f6b4-185">Tüm silinen gizli bir anahtar kasasına listesi:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="8f6b4-186">Bir gizli anahtar silinmiş durumda kurtarma:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="8f6b4-187">Bir gizli anahtar silinmiş durumda temizleme:</span><span class="sxs-lookup"><span data-stu-id="8f6b4-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="8f6b4-188">Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="8f6b4-189">Temizleme ve anahtar kasalarını</span><span class="sxs-lookup"><span data-stu-id="8f6b4-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="8f6b4-190">Anahtar kasası nesneleri</span><span class="sxs-lookup"><span data-stu-id="8f6b4-190">Key vault objects</span></span>

<span data-ttu-id="8f6b4-191">Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="8f6b4-192">Anahtar Kasası'nda tüm diğer nesnelerin olarak Silinmiş nesne bulunan anahtar kasası ancak değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="8f6b4-193">Anahtar kapsayıcıları kasaları</span><span class="sxs-lookup"><span data-stu-id="8f6b4-193">Key vaults as containers</span></span>
<span data-ttu-id="8f6b4-194">Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="8f6b4-195">Bir anahtar kasası temizlenecek kullanmak `Remove-AzureRmKeyVault` seçeneği ile komut `-InRemovedState` ve silinen anahtar kasası ile konumunu belirterek `-Location location` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="8f6b4-196">Komutunu kullanarak silinmiş bir kasa konumunu bulabilirsiniz `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="8f6b4-197">Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="8f6b4-198">Gerekli izinler Temizle</span><span class="sxs-lookup"><span data-stu-id="8f6b4-198">Purge permissions required</span></span>
- <span data-ttu-id="8f6b4-199">Kasa ve tüm içeriğini kalıcı olarak kaldırılır, silinen bir anahtar kasası temizlemek için kullanıcının RBAC gerçekleştirme izni gerekiyor bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="8f6b4-200">Kasa silinen anahtar listelemek için RBAC gerçekleştirme izni kullanıcının ihtiyacı *Microsoft.KeyVault/deletedVaults/read* izni.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="8f6b4-201">Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="8f6b4-202">Zamanlanmış temizleme</span><span class="sxs-lookup"><span data-stu-id="8f6b4-202">Scheduled purge</span></span>

<span data-ttu-id="8f6b4-203">Silinen anahtar kasası nesneleri listeleme schedled anahtar kasası tarafından temizlenecek olduklarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="8f6b4-204">*Temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="8f6b4-205">Varsayılan olarak, silinen anahtar kasası nesne saklama süresi 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="8f6b4-206">Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="8f6b4-207">Kurtarılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="8f6b4-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="8f6b4-208">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="8f6b4-208">Other resources</span></span>

- <span data-ttu-id="8f6b4-209">Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="8f6b4-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="8f6b4-210">Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f6b4-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

