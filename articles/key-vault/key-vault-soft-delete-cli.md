---
ms.assetid: 
title: "Azure anahtar kasası - geçici silme CLI ile kullanma"
description: "Kullanım örneği soft-delete CLI kod parçalarını ile örnekleri"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="bdad9-103">Anahtar kasası soft-delete CLI ile kullanma</span><span class="sxs-lookup"><span data-stu-id="bdad9-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="bdad9-104">Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdad9-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="bdad9-105">Özellikle, soft-adresleri aşağıdaki senaryolarda Sil:</span><span class="sxs-lookup"><span data-stu-id="bdad9-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="bdad9-106">Bir anahtar kasası kurtarılabilir silinmesini desteği</span><span class="sxs-lookup"><span data-stu-id="bdad9-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="bdad9-107">Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları</span><span class="sxs-lookup"><span data-stu-id="bdad9-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdad9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bdad9-108">Prerequisites</span></span>

- <span data-ttu-id="bdad9-109">Azure CLI, ortamınız için bu kurulumu yoksa 2.0 - bkz [yönetmek anahtar CLI 2.0 kullanan kasası](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="bdad9-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="bdad9-110">CLI için anahtar kasası belirli başvuru bilgileri için bkz: [Azure CLI 2.0 anahtar kasası başvuru](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="bdad9-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="bdad9-111">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="bdad9-111">Required permissions</span></span>

<span data-ttu-id="bdad9-112">Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:</span><span class="sxs-lookup"><span data-stu-id="bdad9-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="bdad9-113">İşlem</span><span class="sxs-lookup"><span data-stu-id="bdad9-113">Operation</span></span> | <span data-ttu-id="bdad9-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bdad9-114">Description</span></span> | <span data-ttu-id="bdad9-115">Kullanıcı izni</span><span class="sxs-lookup"><span data-stu-id="bdad9-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="bdad9-116">Liste</span><span class="sxs-lookup"><span data-stu-id="bdad9-116">List</span></span>|<span data-ttu-id="bdad9-117">Listeleri anahtar kasalarını silindi.</span><span class="sxs-lookup"><span data-stu-id="bdad9-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="bdad9-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="bdad9-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="bdad9-119">Kurtar</span><span class="sxs-lookup"><span data-stu-id="bdad9-119">Recover</span></span>|<span data-ttu-id="bdad9-120">Silinen bir anahtar kasası geri yükler.</span><span class="sxs-lookup"><span data-stu-id="bdad9-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="bdad9-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="bdad9-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="bdad9-122">Temizle</span><span class="sxs-lookup"><span data-stu-id="bdad9-122">Purge</span></span>|<span data-ttu-id="bdad9-123">Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="bdad9-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="bdad9-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="bdad9-125">İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="bdad9-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="bdad9-126">Etkinleştirme soft-Sil</span><span class="sxs-lookup"><span data-stu-id="bdad9-126">Enabling soft-delete</span></span>

<span data-ttu-id="bdad9-127">Silinen bir anahtar kasası veya anahtar kasasında depolanan nesneler kurtarmanız mümkün olması için önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="bdad9-128">Varolan anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="bdad9-128">Existing key vault</span></span>

<span data-ttu-id="bdad9-129">ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="bdad9-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="bdad9-130">Doğrudan yazmak için Azure Resource Manager kaynak işleme kullanmanıza gerek şu anda *enableSoftDelete* anahtar kasası kaynak özelliğine.</span><span class="sxs-lookup"><span data-stu-id="bdad9-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="bdad9-131">Yeni anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="bdad9-131">New key vault</span></span>

<span data-ttu-id="bdad9-132">Yeni bir anahtar kasası için geçici silmeyi etkinleştirme oluşturma zamanında soft-delete etkinleştirme bayrağını ekleyerek yapılır, bir komut oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bdad9-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="bdad9-133">Soft-delete etkinleştirme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bdad9-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="bdad9-134">Bir anahtar kasası soft-delete etkin olduğunu doğrulamak için çalıştırın *Göster* komut ve 'yumuşak silmek için etkin?' arayın</span><span class="sxs-lookup"><span data-stu-id="bdad9-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="bdad9-135">özniteliği ve onun ayarı true veya false.</span><span class="sxs-lookup"><span data-stu-id="bdad9-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="bdad9-136">Soft-delete tarafından korunan bir anahtar kasasını silme</span><span class="sxs-lookup"><span data-stu-id="bdad9-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="bdad9-137">Bir anahtar kasasını silme (veya kaldırma için) komutu aynı kalır, ancak davranışını olup soft-delete veya etkinleştirdiğiniz bağlı olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="bdad9-138">Soft-delete etkin olmayan bir anahtar kasası için önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.</span><span class="sxs-lookup"><span data-stu-id="bdad9-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="bdad9-139">Soft-delete anahtar kasalarınıza nasıl korur</span><span class="sxs-lookup"><span data-stu-id="bdad9-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="bdad9-140">Soft-delete ile etkin:</span><span class="sxs-lookup"><span data-stu-id="bdad9-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="bdad9-141">Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu konumu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="bdad9-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="bdad9-142">Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş durumda olsa da bunu kalır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="bdad9-143">Silinmiş bir durumda bir anahtar kasası için DNS adını hala aynı ada sahip yeni bir anahtar kasası oluşturulamıyor için ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="bdad9-144">Aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bdad9-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="bdad9-145">*Kaynak kimliği* çıktıda bu kasaya özgün kaynak Kimliğine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="bdad9-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="bdad9-146">Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok</span><span class="sxs-lookup"><span data-stu-id="bdad9-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="bdad9-147">*Kimliği* alan, Kurtarma ya da temizleme kaynağı tanımlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="bdad9-148">*Temizleme tarih zamanlanmış* alan gösterir kasanın ne zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa.</span><span class="sxs-lookup"><span data-stu-id="bdad9-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="bdad9-149">Hesaplamak için kullanılan varsayılan saklama dönemi *temizleme tarih zamanlanmış*, 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="bdad9-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="bdad9-150">Bir anahtar kasası kurtarma</span><span class="sxs-lookup"><span data-stu-id="bdad9-150">Recovering a key vault</span></span>

<span data-ttu-id="bdad9-151">Bir anahtar kasası kurtarmak için anahtar kasası adı, kaynak grubunu ve konumu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="bdad9-152">Bu bir anahtar kasası kurtarma işlemi için gereken konum ve silinen anahtar kasasının kaynak grubu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bdad9-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="bdad9-153">Bir anahtar kasası kurtarıldığında, yeni bir kaynak anahtar kasasının özgün kaynak kimliğiyle oluşur</span><span class="sxs-lookup"><span data-stu-id="bdad9-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="bdad9-154">Burada anahtar kasası varolan kaynak grubu kaldırdıysanız anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="bdad9-155">Anahtar kasası nesneleri ve soft-Sil</span><span class="sxs-lookup"><span data-stu-id="bdad9-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="bdad9-156">İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.</span><span class="sxs-lookup"><span data-stu-id="bdad9-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="bdad9-157">İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma.</span><span class="sxs-lookup"><span data-stu-id="bdad9-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="bdad9-158">Silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="bdad9-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="bdad9-159">Örneğin, bir anahtar kasası silinmiş listesi anahtarlarında istemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="bdad9-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="bdad9-160">Durum geçişi</span><span class="sxs-lookup"><span data-stu-id="bdad9-160">Transition state</span></span> 

<span data-ttu-id="bdad9-161">Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, geçişi tamamlamak için birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="bdad9-162">Bu geçiş aşamasında, anahtarı etkin veya silinmiş durumda değil görünebilir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="bdad9-163">Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.</span><span class="sxs-lookup"><span data-stu-id="bdad9-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="bdad9-164">Anahtar kasası nesneleriyle Soft-delete kullanma</span><span class="sxs-lookup"><span data-stu-id="bdad9-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="bdad9-165">Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika silinmiş durumda 90 gün boyunca kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="bdad9-166">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="bdad9-166">Keys</span></span>

<span data-ttu-id="bdad9-167">Silinen bir anahtarı kurtarmak için:</span><span class="sxs-lookup"><span data-stu-id="bdad9-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="bdad9-168">Bir anahtar kalıcı olarak silmek için:</span><span class="sxs-lookup"><span data-stu-id="bdad9-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="bdad9-169">Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="bdad9-170">**Kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="bdad9-171">Bir kullanıcı veya hizmet sorumlusu yürütmek bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları ilgili (anahtar veya gizli) Bu nesne için anahtar kasası erişim ilkesinde eylem.</span><span class="sxs-lookup"><span data-stu-id="bdad9-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="bdad9-172">Varsayılan olarak, **Temizleme** izni 'all' kısayol bir kullanıcı için tüm izinleri vermek için kullanıldığında, bir anahtar kasasının erişim ilkesine eklenmez.</span><span class="sxs-lookup"><span data-stu-id="bdad9-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="bdad9-173">Açıkça vermelidir **Temizleme** izni.</span><span class="sxs-lookup"><span data-stu-id="bdad9-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="bdad9-174">Örneğin, aşağıdaki verir komut user@contoso.com anahtarlarında çeşitli işlemleri gerçekleştirmek için izni *ContosoVault* dahil olmak üzere **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="bdad9-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="bdad9-175">Bir anahtar kasası erişim ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="bdad9-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="bdad9-176">Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="bdad9-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="bdad9-177">Gizli Diziler</span><span class="sxs-lookup"><span data-stu-id="bdad9-177">Secrets</span></span>

<span data-ttu-id="bdad9-178">Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="bdad9-179">Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için komutlardır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="bdad9-180">SQLPassword adlı bir gizli anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="bdad9-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="bdad9-181">Tüm silinen gizli bir anahtar kasasına listesi:</span><span class="sxs-lookup"><span data-stu-id="bdad9-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="bdad9-182">Bir gizli anahtar silinmiş durumda kurtarma:</span><span class="sxs-lookup"><span data-stu-id="bdad9-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="bdad9-183">Bir gizli anahtar silinmiş durumda temizleme:</span><span class="sxs-lookup"><span data-stu-id="bdad9-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="bdad9-184">Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="bdad9-185">Temizleme ve anahtar kasalarını</span><span class="sxs-lookup"><span data-stu-id="bdad9-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="bdad9-186">Anahtar kasası nesneleri</span><span class="sxs-lookup"><span data-stu-id="bdad9-186">Key vault objects</span></span>

<span data-ttu-id="bdad9-187">Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="bdad9-188">Anahtar Kasası'nda tüm diğer nesnelerin olarak Silinmiş nesne bulunan anahtar kasası ancak değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="bdad9-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="bdad9-189">Anahtar kapsayıcıları kasaları</span><span class="sxs-lookup"><span data-stu-id="bdad9-189">Key vaults as containers</span></span>
<span data-ttu-id="bdad9-190">Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="bdad9-191">Bir anahtar kasası temizlenecek kullanmak `az keyvault purge` komutu.</span><span class="sxs-lookup"><span data-stu-id="bdad9-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="bdad9-192">Konum aboneliğiniz silinen anahtar kasalarını komutunu kullanarak bulabilir `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="bdad9-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="bdad9-193">Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="bdad9-194">Gerekli izinler Temizle</span><span class="sxs-lookup"><span data-stu-id="bdad9-194">Purge permissions required</span></span>
- <span data-ttu-id="bdad9-195">Kasa ve tüm içeriğini kalıcı olarak kaldırılır, silinen bir anahtar kasası temizlemek için kullanıcının RBAC gerçekleştirme izni gerekiyor bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi.</span><span class="sxs-lookup"><span data-stu-id="bdad9-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="bdad9-196">Kasa silinen anahtar listelemek için RBAC gerçekleştirme izni kullanıcının ihtiyacı *Microsoft.KeyVault/deletedVaults/read* izni.</span><span class="sxs-lookup"><span data-stu-id="bdad9-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="bdad9-197">Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="bdad9-198">Zamanlanmış temizleme</span><span class="sxs-lookup"><span data-stu-id="bdad9-198">Scheduled purge</span></span>

<span data-ttu-id="bdad9-199">Silinen anahtar kasası nesneleri listeleme schedled anahtar kasası tarafından temizlenecek olduklarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="bdad9-200">*Temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="bdad9-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="bdad9-201">Varsayılan olarak, silinen anahtar kasası nesne saklama süresi 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="bdad9-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="bdad9-202">Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="bdad9-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="bdad9-203">Kurtarılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="bdad9-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="bdad9-204">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bdad9-204">Other resources</span></span>

- <span data-ttu-id="bdad9-205">Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="bdad9-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="bdad9-206">Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="bdad9-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

