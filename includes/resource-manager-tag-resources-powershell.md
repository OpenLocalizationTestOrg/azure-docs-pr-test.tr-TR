<span data-ttu-id="f474b-101">Merhaba AzureRm.Resources modülü 3.0 sürümü etiketleriyle nasıl çalıştığını önemli değişiklikler dahil.</span><span class="sxs-lookup"><span data-stu-id="f474b-101">Version 3.0 of hello AzureRm.Resources module included significant changes in how you work with tags.</span></span> <span data-ttu-id="f474b-102">Devam etmeden önce sürümünüzü kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="f474b-102">Before you proceed, check your version:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="f474b-103">Sonuçlarınızı sürüm 3.0 veya üstü gösteriyorsa, bu konudaki hello örnekleri ortamınız ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="f474b-103">If your results show version 3.0 or later, hello examples in this topic work with your environment.</span></span> <span data-ttu-id="f474b-104">3.0 veya sonraki sürüme sahip değilseniz, bu konu başlığına devam etmeden önce PowerShell Galerisi veya Web Platform Yükleyicisi’ni kullanarak [sürümünüzü güncelleştirin](/powershell/azureps-cmdlets-docs/).</span><span class="sxs-lookup"><span data-stu-id="f474b-104">If you do not have version 3.0 or later, [update your version](/powershell/azureps-cmdlets-docs/) by using PowerShell Gallery or Web Platform Installer before you proceed with this topic.</span></span>

```powershell
Version
-------
3.5.0
```

<span data-ttu-id="f474b-105">toosee hello için varolan etiketleri bir *kaynak grubu*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-105">toosee hello existing tags for a *resource group*, use:</span></span>

```powershell
(Get-AzureRmResourceGroup -Name examplegroup).Tags
```

<span data-ttu-id="f474b-106">Bu komut dosyası biçimini izleyen hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="f474b-106">That script returns hello following format:</span></span>

```powershell
Name                           Value
----                           -----
Dept                           IT
Environment                    Test
```

<span data-ttu-id="f474b-107">toosee hello için varolan etiketleri bir *belirtilen kaynak Kimliğine sahip kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-107">toosee hello existing tags for a *resource that has a specified resource ID*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceId {resource-id}).Tags
```

<span data-ttu-id="f474b-108">Ya da toosee hello için varolan etiketleri bir *belirtilen ad ve kaynak grubuna sahip kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-108">Or, toosee hello existing tags for a *resource that has a specified name and resource group*, use:</span></span>

```powershell
(Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
```

<span data-ttu-id="f474b-109">tooget *belirli bir etikete sahip kaynak gruplarını*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-109">tooget *resource groups that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResourceGroup -Tag @{ Dept="Finance" }).Name 
```

<span data-ttu-id="f474b-110">tooget *, belirli bir etikete sahip kaynaklar*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-110">tooget *resources that have a specific tag*, use:</span></span>

```powershell
(Find-AzureRmResource -TagName Dept -TagValue Finance).Name
```

<span data-ttu-id="f474b-111">Etiketler tooa kaynağa veya bir kaynak grubuna uygulamak her zaman, o kaynak veya kaynak grubu hello varolan etiketleri üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="f474b-111">Every time you apply tags tooa resource or a resource group, you overwrite hello existing tags on that resource or resource group.</span></span> <span data-ttu-id="f474b-112">Bu nedenle, olup hello kaynağı veya kaynak grubunu varolan etiketleri temel alarak farklı bir yaklaşım kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f474b-112">Therefore, you must use a different approach based on whether hello resource or resource group has existing tags.</span></span> 

<span data-ttu-id="f474b-113">tooadd etiketler tooa *kaynak grubu mevcut etiketleri olmadan*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-113">tooadd tags tooa *resource group without existing tags*, use:</span></span>

```powershell
Set-AzureRmResourceGroup -Name examplegroup -Tag @{ Dept="IT"; Environment="Test" }
```

<span data-ttu-id="f474b-114">tooadd etiketler tooa *varolan etiketleri olan kaynak grubuna*hello varolan etiketleri almak, hello yeni etiket eklemek ve hello etiketler yeniden uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f474b-114">tooadd tags tooa *resource group that has existing tags*, retrieve hello existing tags, add hello new tag, and reapply hello tags:</span></span>

```powershell
$tags = (Get-AzureRmResourceGroup -Name examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResourceGroup -Tag $tags -Name examplegroup
```

<span data-ttu-id="f474b-115">tooadd etiketler tooa *varolan etiketleri olmadan kaynak*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-115">tooadd tags tooa *resource without existing tags*, use:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="f474b-116">tooadd etiketler tooa *varolan etiketleri olan kaynağın*, kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-116">tooadd tags tooa *resource that has existing tags*, use:</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName examplevnet -ResourceGroupName examplegroup).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName examplevnet -ResourceGroupName examplegroup
```

<span data-ttu-id="f474b-117">tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *hello kaynaklardaki varolan etiketleri korumuyor*, komut dosyası izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-117">tooapply all tags from a resource group tooits resources, and *not retain existing tags on hello resources*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName | ForEach-Object {Set-AzureRmResource -ResourceId $_.ResourceId -Tag $g.Tags -Force } 
}
```

<span data-ttu-id="f474b-118">tooapply tüm etiketleri bir kaynak grubu tooits kaynakları ve *tekrarı olmayan kaynaklar varolan etiketleri korumak*, komut dosyası izleyen hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="f474b-118">tooapply all tags from a resource group tooits resources, and *retain existing tags on resources that are not duplicates*, use hello following script:</span></span>

```powershell
$groups = Get-AzureRmResourceGroup
foreach ($g in $groups) 
{
    if ($g.Tags -ne $null) {
        $resources = Find-AzureRmResource -ResourceGroupNameEquals $g.ResourceGroupName 
        foreach ($r in $resources)
        {
            $resourcetags = (Get-AzureRmResource -ResourceId $r.ResourceId).Tags
            foreach ($key in $g.Tags.Keys)
            {
                if ($resourcetags.ContainsKey($key)) { $resourcetags.Remove($key) }
            }
            $resourcetags += $g.Tags
            Set-AzureRmResource -Tag $resourcetags -ResourceId $r.ResourceId -Force
        }
    }
}
```

<span data-ttu-id="f474b-119">Tüm etiketleri tooremove boş karma tablosu geçirin:</span><span class="sxs-lookup"><span data-stu-id="f474b-119">tooremove all tags, pass an empty hash table:</span></span>

```powershell
Set-AzureRmResourceGroup -Tag @{} -Name examplegroup
```



