---
ms.assetid: 
title: "aaaAzure anahtar kasası - toouse yumuşak delete CLI ile nasıl"
description: "Kullanım örneği soft-delete CLI kod parçalarını ile örnekleri"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="4a670-103">Nasıl toouse anahtar kasası soft-delete CLI ile</span><span class="sxs-lookup"><span data-stu-id="4a670-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="4a670-104">Azure anahtar Kasası'nın geçici silme özelliği silinen kasalarını ve kasa nesneleri kurtarılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a670-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="4a670-105">Özellikle, soft-senaryoları aşağıdaki adresleri hello Sil:</span><span class="sxs-lookup"><span data-stu-id="4a670-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="4a670-106">Bir anahtar kasası kurtarılabilir silinmesini desteği</span><span class="sxs-lookup"><span data-stu-id="4a670-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="4a670-107">Anahtar kasası nesnelerin kurtarılabilir silinmesi desteği; , gizli anahtarları ve sertifikaları</span><span class="sxs-lookup"><span data-stu-id="4a670-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a670-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4a670-108">Prerequisites</span></span>

- <span data-ttu-id="4a670-109">Azure CLI, ortamınız için bu kurulumu yoksa 2.0 - bkz [yönetmek anahtar CLI 2.0 kullanan kasası](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="4a670-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="4a670-110">CLI için anahtar kasası belirli başvuru bilgileri için bkz: [Azure CLI 2.0 anahtar kasası başvuru](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="4a670-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="4a670-111">Gerekli izinler</span><span class="sxs-lookup"><span data-stu-id="4a670-111">Required permissions</span></span>

<span data-ttu-id="4a670-112">Anahtar kasası işlemleri ayrı olarak aracılığıyla rol tabanlı erişim denetimi (RBAC) izinleri gibi yönetilen:</span><span class="sxs-lookup"><span data-stu-id="4a670-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="4a670-113">İşlem</span><span class="sxs-lookup"><span data-stu-id="4a670-113">Operation</span></span> | <span data-ttu-id="4a670-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4a670-114">Description</span></span> | <span data-ttu-id="4a670-115">Kullanıcı izni</span><span class="sxs-lookup"><span data-stu-id="4a670-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="4a670-116">Liste</span><span class="sxs-lookup"><span data-stu-id="4a670-116">List</span></span>|<span data-ttu-id="4a670-117">Listeleri anahtar kasalarını silindi.</span><span class="sxs-lookup"><span data-stu-id="4a670-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="4a670-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="4a670-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="4a670-119">Kurtar</span><span class="sxs-lookup"><span data-stu-id="4a670-119">Recover</span></span>|<span data-ttu-id="4a670-120">Silinen bir anahtar kasası geri yükler.</span><span class="sxs-lookup"><span data-stu-id="4a670-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="4a670-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="4a670-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="4a670-122">Temizle</span><span class="sxs-lookup"><span data-stu-id="4a670-122">Purge</span></span>|<span data-ttu-id="4a670-123">Kalıcı olarak silinmiş bir anahtar kasası ve tüm içeriğini kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4a670-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="4a670-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="4a670-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="4a670-125">İzinler ve erişim denetimi hakkında daha fazla bilgi için bkz: [anahtar kasanızı güvenli](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="4a670-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="4a670-126">Etkinleştirme soft-Sil</span><span class="sxs-lookup"><span data-stu-id="4a670-126">Enabling soft-delete</span></span>

<span data-ttu-id="4a670-127">Silinen bir anahtar kasası ya da bir anahtar olarak depolanan nesneler toobe mümkün toorecover kasa, önce bu anahtar kasası için geçici silme etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a670-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="4a670-128">Varolan anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="4a670-128">Existing key vault</span></span>

<span data-ttu-id="4a670-129">ContosoVault adlı bir var olan anahtar kasasının için geçici silme gibi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4a670-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="4a670-130">Şu anda toouse Azure Resource Manager kaynak işleme toodirectly yazma hello gereksiniminiz *enableSoftDelete* özelliği toohello anahtar kasası kaynak.</span><span class="sxs-lookup"><span data-stu-id="4a670-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="4a670-131">Yeni anahtar kasası</span><span class="sxs-lookup"><span data-stu-id="4a670-131">New key vault</span></span>

<span data-ttu-id="4a670-132">Yeni bir anahtar kasası için geçici silmeyi etkinleştirme yapılır tooyour hello soft-delete etkinleştirme bayrağını ekleyerek oluşturma zamanında komutu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a670-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="4a670-133">Soft-delete etkinleştirme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="4a670-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="4a670-134">bir anahtar kasası soft-delete etkin olan tooverify çalışma hello *Göster* komut ve Merhaba 'Yumuşak silme etkin?' arayın</span><span class="sxs-lookup"><span data-stu-id="4a670-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="4a670-135">özniteliği ve onun ayarı true veya false.</span><span class="sxs-lookup"><span data-stu-id="4a670-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="4a670-136">Soft-delete tarafından korunan bir anahtar kasasını silme</span><span class="sxs-lookup"><span data-stu-id="4a670-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="4a670-137">Merhaba komutu toodelete (veya kaldırma) bir anahtar kasası aynı ancak etkinleştirilip bağlı olarak, davranış değişiklikleri yumuşak veya silme hello kalır.</span><span class="sxs-lookup"><span data-stu-id="4a670-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="4a670-138">Soft-delete etkin olmayan bir anahtar kasası için hello önceki komutu çalıştırırsanız, bu anahtar kasası ve tüm içeriğini kurtarma seçenekleri olmadan kalıcı olarak siler.</span><span class="sxs-lookup"><span data-stu-id="4a670-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="4a670-139">Soft-delete anahtar kasalarınıza nasıl korur</span><span class="sxs-lookup"><span data-stu-id="4a670-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="4a670-140">Soft-delete ile etkin:</span><span class="sxs-lookup"><span data-stu-id="4a670-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="4a670-141">Bir anahtar kasası silindiğinde, kendi kaynak grubundan kaldırılmış olduğundan ve yalnızca ayrılmış bir ad alanında yerleştirildiğinden onu oluşturulduğu hello konumu ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4a670-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="4a670-142">Silinen anahtar nesneleri gibi anahtarları, gizli ve sertifikalar erişilemeyen kasa ve bunların içeren anahtar kasası silinmiş hello durumundayken bunu kalır.</span><span class="sxs-lookup"><span data-stu-id="4a670-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="4a670-143">aynı ada sahip yeni bir anahtar kasası oluşturulamıyor şekilde hello DNS adı silinmiş bir durumda bir anahtar kasası için ayrılmış olarak kalır.</span><span class="sxs-lookup"><span data-stu-id="4a670-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="4a670-144">Merhaba aşağıdaki komutu kullanarak, aboneliğinizle ilişkili silinen durumu anahtar kasalarını görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4a670-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="4a670-145">Merhaba *kaynak kimliği* hello çıktı toohello özgün kaynak kimliği bu kasasının başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="4a670-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="4a670-146">Bu anahtar kasasında şimdi silinmiş durumda olduğundan, bu kaynak kimliği ile hiçbir kaynak yok</span><span class="sxs-lookup"><span data-stu-id="4a670-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="4a670-147">Merhaba *kimliği* alan kurtarma ya da temizleme kullanılan tooidentify hello kaynak olabilir.</span><span class="sxs-lookup"><span data-stu-id="4a670-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="4a670-148">Merhaba *temizleme tarih zamanlanmış* alan gösterir hello kasası zaman kalıcı olarak silinecek (temizlendi) bu silinen kasa için bir eylem varsa.</span><span class="sxs-lookup"><span data-stu-id="4a670-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="4a670-149">Merhaba varsayılan saklama dönemi, kullanılan toocalculate hello *temizleme tarih zamanlanmış*, 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="4a670-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="4a670-150">Bir anahtar kasası kurtarma</span><span class="sxs-lookup"><span data-stu-id="4a670-150">Recovering a key vault</span></span>

<span data-ttu-id="4a670-151">toorecover bir anahtar kasası, toospecify hello anahtar kasası adı, kaynak grubunu ve konumu gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a670-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="4a670-152">Bu bir anahtar kasası kurtarma işlemi için gerek duyduğunuz hello konum ve hello kaynak grubu silinmiş hello anahtar kasasının unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4a670-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="4a670-153">Bir anahtar kasası kurtarıldığında hello sonuç hello anahtar kasasının özgün kaynak kimliğiyle yeni bir kaynak değildir</span><span class="sxs-lookup"><span data-stu-id="4a670-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="4a670-154">Burada hello anahtar kasası var hello kaynak grubu kaldırdıysanız hello anahtar kasası kurtarılabilir önce aynı ada sahip yeni bir kaynak grubu oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a670-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="4a670-155">Anahtar kasası nesneleri ve soft-Sil</span><span class="sxs-lookup"><span data-stu-id="4a670-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="4a670-156">İçin bir anahtar, 'ContosoFirstKey' yumuşak Sil ' ContosoVault etkin' adlı bir anahtar kasasının içinde burada nasıl, bu anahtarı silmeniz.</span><span class="sxs-lookup"><span data-stu-id="4a670-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="4a670-157">İçin geçici silme etkin anahtar kasanız ile silinen anahtar görünmeye devam eder dışında silinmiş gibi açıkça listelemek veya silinen anahtarlarını alma.</span><span class="sxs-lookup"><span data-stu-id="4a670-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="4a670-158">Merhaba silinmiş durumda bir anahtar üzerindeki çoğu işlemi silinen anahtar listeleme, bu kurtarma veya onu temizleme dışında başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="4a670-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="4a670-159">Örneğin, toorequest silinmiş toolist anahtarları bir anahtar Kasası'hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4a670-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="4a670-160">Durum geçişi</span><span class="sxs-lookup"><span data-stu-id="4a670-160">Transition state</span></span> 

<span data-ttu-id="4a670-161">Bir anahtar kasasına bir anahtar soft-etkin delete ile sildiğinizde, hello geçiş toocomplete birkaç saniye sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4a670-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="4a670-162">Bu durum geçişi sırasında bu hello anahtarı hello etkin veya hello silinmiş durumda değil görünebilir.</span><span class="sxs-lookup"><span data-stu-id="4a670-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="4a670-163">Bu komut tüm silinen anahtarlarında 'ContosoVault' adlı anahtar kasanızı listeler.</span><span class="sxs-lookup"><span data-stu-id="4a670-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="4a670-164">Anahtar kasası nesneleriyle Soft-delete kullanma</span><span class="sxs-lookup"><span data-stu-id="4a670-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="4a670-165">Kurtarma ya da onu temizleyebilirsiniz sürece yalnızca anahtar kasalarını, silinen bir anahtar gibi gizli veya, sertifika too90 günlerini silinmiş durumda kalır.</span><span class="sxs-lookup"><span data-stu-id="4a670-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="4a670-166">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="4a670-166">Keys</span></span>

<span data-ttu-id="4a670-167">Silinen bir anahtar toorecover:</span><span class="sxs-lookup"><span data-stu-id="4a670-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="4a670-168">toopermanently bir anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="4a670-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4a670-169">Bir anahtar temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="4a670-170">Merhaba **kurtarmak** ve **Temizleme** Eylemler bir anahtar kasası erişim ilkesinde ilişkili kendi izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a670-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="4a670-171">Kullanıcı veya hizmet asıl toobe mümkün tooexecute için bir **kurtarmak** veya **Temizleme** gerekir iznine sahip oldukları hello ilgili (anahtar veya gizli) Bu nesne için hello anahtar kasası erişim ilkesinde eylem.</span><span class="sxs-lookup"><span data-stu-id="4a670-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="4a670-172">Varsayılan olarak, hello **Temizleme** izni hello 'all' kısayol kullanılan toogrant olduğunda tooa anahtar kasasının erişim ilkesi eklenmez tüm izinleri tooa kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="4a670-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="4a670-173">Açıkça vermelidir **Temizleme** izni.</span><span class="sxs-lookup"><span data-stu-id="4a670-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="4a670-174">Örneğin, aşağıdaki komut verir hello user@contoso.com izin tooperform anahtarlarında üzerinde çeşitli işlemler *ContosoVault* dahil olmak üzere **Temizleme**.</span><span class="sxs-lookup"><span data-stu-id="4a670-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="4a670-175">Bir anahtar kasası erişim ilkesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="4a670-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="4a670-176">Yalnızca etkin soft-delete oluşmuş olan bir anahtar kasası varsa, olmayabilir **kurtarmak** ve **Temizleme** izinleri.</span><span class="sxs-lookup"><span data-stu-id="4a670-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="4a670-177">Gizli Diziler</span><span class="sxs-lookup"><span data-stu-id="4a670-177">Secrets</span></span>

<span data-ttu-id="4a670-178">Anahtarları gibi bir anahtar kasasına gizli anahtarları üzerinde kendi komutları ile çalıştırılan örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="4a670-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="4a670-179">Aşağıdaki, silme, listeleme, kurtarma ve gizli anahtarları Temizleme için hello komutlardır.</span><span class="sxs-lookup"><span data-stu-id="4a670-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="4a670-180">SQLPassword adlı bir gizli anahtarı silin:</span><span class="sxs-lookup"><span data-stu-id="4a670-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="4a670-181">Tüm silinen gizli bir anahtar kasasına listesi:</span><span class="sxs-lookup"><span data-stu-id="4a670-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="4a670-182">Bir gizli anahtar hello silinmiş durumda kurtarma:</span><span class="sxs-lookup"><span data-stu-id="4a670-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="4a670-183">Bir gizli anahtar silinmiş durumda temizleme:</span><span class="sxs-lookup"><span data-stu-id="4a670-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4a670-184">Gizli temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="4a670-185">Temizleme ve anahtar kasalarını</span><span class="sxs-lookup"><span data-stu-id="4a670-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="4a670-186">Anahtar kasası nesneleri</span><span class="sxs-lookup"><span data-stu-id="4a670-186">Key vault objects</span></span>

<span data-ttu-id="4a670-187">Bir anahtar temizleme, gizli veya, sertifika kalıcı olarak, kurtarılabilir olmaz anlamına silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="4a670-188">Merhaba anahtar Kasası'nda tüm diğer nesnelerin gibi hello Silinmiş nesne içeriyor hello anahtar kasası ancak değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="4a670-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="4a670-189">Anahtar kapsayıcıları kasaları</span><span class="sxs-lookup"><span data-stu-id="4a670-189">Key vaults as containers</span></span>
<span data-ttu-id="4a670-190">Bir anahtar kasası temizlenir, tüm içeriğini anahtarları, gizli ve sertifikalar dahil olmak üzere kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="4a670-191">toopurge bir anahtar kasası kullanan hello `az keyvault purge` komutu.</span><span class="sxs-lookup"><span data-stu-id="4a670-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="4a670-192">Aboneliğinizin silinen anahtar kasalarını hello komutunu kullanarak hello konum bulabilir `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="4a670-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="4a670-193">Bir anahtar kasası temizleme kalıcı olarak, kurtarılabilir olmaz anlamı silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="4a670-194">Gerekli izinler Temizle</span><span class="sxs-lookup"><span data-stu-id="4a670-194">Purge permissions required</span></span>
- <span data-ttu-id="4a670-195">toopurge silinmiş bir anahtar kasası, hello kasası ve tüm içeriğini kalıcı olarak kaldırılır şekilde hello kullanıcının ihtiyacı RBAC izni tooperform bir *Microsoft.KeyVault/locations/deletedVaults/purge/action* işlemi.</span><span class="sxs-lookup"><span data-stu-id="4a670-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="4a670-196">toolist silinmiş hello anahtar hello kasası kullanıcı gereken RBAC izni tooperform *Microsoft.KeyVault/deletedVaults/read* izni.</span><span class="sxs-lookup"><span data-stu-id="4a670-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="4a670-197">Varsayılan olarak yalnızca bir abonelik yöneticisinin bu izinlere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="4a670-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="4a670-198">Zamanlanmış temizleme</span><span class="sxs-lookup"><span data-stu-id="4a670-198">Scheduled purge</span></span>

<span data-ttu-id="4a670-199">Silinen anahtar kasası nesneleri listeleme anahtar kasası tarafından temizlendi schedled toobe olduklarında gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a670-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="4a670-200">Merhaba *temizleme tarih zamanlanmış* alan gösterir ne zaman bir anahtar kasası nesnesi kalıcı olarak silinecek, hiçbir işlem yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="4a670-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="4a670-201">Varsayılan olarak, silinen anahtar kasası nesne hello saklama süresi 90 gündür.</span><span class="sxs-lookup"><span data-stu-id="4a670-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="4a670-202">Tarafından tetiklenen silinen kasası nesne, kendi *temizleme tarih zamanlanmış* alan, kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="4a670-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="4a670-203">Kurtarılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="4a670-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="4a670-204">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4a670-204">Other resources</span></span>

- <span data-ttu-id="4a670-205">Anahtar Kasası'nın soft-delete özelliğine genel bakış için bkz: [Azure anahtar kasası soft-delete genel bakış](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="4a670-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="4a670-206">Azure anahtar kasası kullanımı genel bir bakış için bkz: [Azure anahtar kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4a670-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

