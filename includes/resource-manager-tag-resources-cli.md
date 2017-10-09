<span data-ttu-id="825e2-101">tooadd bir etiket tooa kaynak grubu kullanmak **azure Grup kümesini**.</span><span class="sxs-lookup"><span data-stu-id="825e2-101">tooadd a tag tooa resource group, use **azure group set**.</span></span> <span data-ttu-id="825e2-102">Merhaba kaynak grubu varolan etiketleri yoksa hello etiketinde geçirin.</span><span class="sxs-lookup"><span data-stu-id="825e2-102">If hello resource group does not have any existing tags, pass in hello tag.</span></span>

```azurecli
azure group set -n tag-demo-group -t Dept=Finance
```

<span data-ttu-id="825e2-103">Etiketler, bir bütün olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="825e2-103">Tags are updated as a whole.</span></span> <span data-ttu-id="825e2-104">Tooadd varolan etiketleri olan bir etiketi tooa kaynak grubu istiyorsanız, tüm hello etiketleri geçirin.</span><span class="sxs-lookup"><span data-stu-id="825e2-104">If you want tooadd a tag tooa resource group that has existing tags, pass all hello tags.</span></span> 

```azurecli
azure group set -n tag-demo-group -t Dept=Finance;Environment=Production;Project=Upgrade
```

<span data-ttu-id="825e2-105">Etiketler, bir kaynak grubunda kaynaklar tarafından devralınmaz.</span><span class="sxs-lookup"><span data-stu-id="825e2-105">Tags are not inherited by resources in a resource group.</span></span> <span data-ttu-id="825e2-106">tooadd etiketi tooa kaynak kullanmak **azure kaynak kümesi**.</span><span class="sxs-lookup"><span data-stu-id="825e2-106">tooadd a tag tooa resource, use **azure resource set**.</span></span> <span data-ttu-id="825e2-107">Merhaba hello etiket ekleme hello kaynak türü için API sürüm numarası geçirin.</span><span class="sxs-lookup"><span data-stu-id="825e2-107">Pass hello API version number for hello resource type that you are adding hello tag to.</span></span> <span data-ttu-id="825e2-108">Tooretrieve hello API sürümü gerekiyorsa, hello kaynak sağlayıcısı hello türü için ayarladığınız komutuyla aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="825e2-108">If you need tooretrieve hello API version, use hello following command with hello resource provider for hello type you are setting:</span></span>

```azurecli
azure provider show -n Microsoft.Storage --json
```

<span data-ttu-id="825e2-109">Merhaba sonuçlarında hello kaynak türü için istediğiniz arayın.</span><span class="sxs-lookup"><span data-stu-id="825e2-109">In hello results, look for hello resource type you want.</span></span>

```azurecli
"resourceTypes": [
{
  "resourceType": "storageAccounts",
  ...
  "apiVersions": [
    "2016-01-01",
    "2015-06-15",
    "2015-05-01-preview"
  ]
}
...
```

<span data-ttu-id="825e2-110">Şimdi, bu API sürümü sağlayın kaynak grubu adı, kaynak adı, kaynak türü ve parametreler olarak etiket değeri.</span><span class="sxs-lookup"><span data-stu-id="825e2-110">Now, provide that API version, resource group name, resource name, resource type, and tag value as parameters.</span></span>

```azurecli
azure resource set -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -t Dept=Finance -o 2016-01-01
```

<span data-ttu-id="825e2-111">Etiketler, doğrudan kaynakları ve kaynak gruplarını yok.</span><span class="sxs-lookup"><span data-stu-id="825e2-111">Tags exist directly on resources and resource groups.</span></span> <span data-ttu-id="825e2-112">bir kaynak grubu ve kaynaklarını ile toosee hello varolan etiketleri, Al **azure Grup Göster**.</span><span class="sxs-lookup"><span data-stu-id="825e2-112">toosee hello existing tags, get a resource group and its resources with **azure group show**.</span></span>

```azurecli
azure group show -n tag-demo-group --json
```

<span data-ttu-id="825e2-113">Hangi hello kaynak grubu, tüm uygulanan etiketleri tooit dahil olmak üzere ilgili meta verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="825e2-113">Which returns metadata about hello resource group, including any tags applied tooit.</span></span>

```azurecli
{
  "id": "/subscriptions/4705409c-9372-42f0-914c-64a504530837/resourceGroups/tag-demo-group",
  "name": "tag-demo-group",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "location": "southcentralus",
  "tags": {
    "Dept": "Finance",
    "Environment": "Production",
    "Project": "Upgrade"
  },
  ...
}
```

<span data-ttu-id="825e2-114">Belirli bir kaynak için hello etiketleri kullanarak görüntüleme **azure kaynak Göster**.</span><span class="sxs-lookup"><span data-stu-id="825e2-114">You view hello tags for a particular resource by using **azure resource show**.</span></span>

```azurecli
azure resource show -g tag-demo-group -n storagetagdemo -r Microsoft.Storage/storageAccounts -o 2016-01-01 --json
```

<span data-ttu-id="825e2-115">tooretrieve bir etiket değeri ile tüm hello kaynakları kullanın:</span><span class="sxs-lookup"><span data-stu-id="825e2-115">tooretrieve all hello resources with a tag value, use:</span></span>

```azurecli
azure resource list -t Dept=Finance --json
```

<span data-ttu-id="825e2-116">tooretrieve bir etiket değeri tüm hello kaynak gruplarıyla kullanın:</span><span class="sxs-lookup"><span data-stu-id="825e2-116">tooretrieve all hello resource groups with a tag value, use:</span></span>

```azurecli
azure group list -t Dept=Finance
```

<span data-ttu-id="825e2-117">Komutu aşağıdaki hello ile aboneliğinizde hello varolan etiketleri görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="825e2-117">You can view hello existing tags in your subscription with hello following command:</span></span>

```azurecli
azure tag list
```
