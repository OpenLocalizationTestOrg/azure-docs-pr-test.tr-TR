---
title: "aaaManage Azure PowerShell ile çözümleri | Microsoft Docs"
description: "Azure PowerShell ve Resource Manager toomanage kaynaklarınızı kullanın."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="32ccf-103">Azure PowerShell ve Resource Manager ile kaynakları yönetme</span><span class="sxs-lookup"><span data-stu-id="32ccf-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="32ccf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="32ccf-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="32ccf-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="32ccf-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="32ccf-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="32ccf-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="32ccf-107">REST API</span><span class="sxs-lookup"><span data-stu-id="32ccf-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="32ccf-108">Bu makalede, bilgi nasıl toomanage, Azure PowerShell ve Azure Resource Manager çözümlerinizi.</span><span class="sxs-lookup"><span data-stu-id="32ccf-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="32ccf-109">Resource Manager ile bilmiyorsanız bkz [Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="32ccf-110">Bu konu, yönetim görevlerine odaklanır.</span><span class="sxs-lookup"><span data-stu-id="32ccf-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="32ccf-111">Yapacaklarınız:</span><span class="sxs-lookup"><span data-stu-id="32ccf-111">You will:</span></span>

1. <span data-ttu-id="32ccf-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="32ccf-112">Create a resource group</span></span>
2. <span data-ttu-id="32ccf-113">Bir kaynak toohello kaynak grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="32ccf-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="32ccf-114">Bir etiketi toohello kaynak ekleyin</span><span class="sxs-lookup"><span data-stu-id="32ccf-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="32ccf-115">Adlarını veya etiket değerlerine göre kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="32ccf-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="32ccf-116">Uygulama ve hello kaynak üzerinde bir kilit kaldırın</span><span class="sxs-lookup"><span data-stu-id="32ccf-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="32ccf-117">Bir kaynak grubu Sil</span><span class="sxs-lookup"><span data-stu-id="32ccf-117">Delete a resource group</span></span>

<span data-ttu-id="32ccf-118">Bu makalede gösterme nasıl toodeploy bir Resource Manager şablonu tooyour abonelik.</span><span class="sxs-lookup"><span data-stu-id="32ccf-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="32ccf-119">Bu bilgi için bkz: [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="32ccf-120">Azure PowerShell ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="32ccf-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="32ccf-121">Azure PowerShell yüklü değilse bkz [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32ccf-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="32ccf-122">Azure PowerShell hello geçmiş yüklü, ancak bu kısa süre önce güncelleştirdiniz değil, hello en son sürümünü yüklemeyi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="32ccf-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="32ccf-123">Merhaba sürüm hello aracılığıyla güncelleştirebilirsiniz tooinstall kullanılan aynı yöntemi.</span><span class="sxs-lookup"><span data-stu-id="32ccf-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="32ccf-124">Örneğin, Web Platformu yükleyicisi hello kullandıysanız, yeniden başlatın ve bir güncelleştirme için bakın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="32ccf-125">hello Azure kaynakları modülü sürümünüz toocheck kullanmak hello aşağıdaki cmdlet'i:</span><span class="sxs-lookup"><span data-stu-id="32ccf-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="32ccf-126">Bu konuda 3.3.0 sürümü için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="32ccf-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="32ccf-127">Önceki bir sürümü varsa, deneyiminiz Bu konu başlığı altında gösterilen hello adımlar eşleşmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="32ccf-128">Bu sürümde hello cmdlet'ler hakkında daha fazla belgeler için bkz: [AzureRM.Resources Modülü](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="32ccf-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="32ccf-129">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="32ccf-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="32ccf-130">Çözümünüzü üzerinde çalışmaya başlamadan önce tooyour hesabında oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="32ccf-131">Azure hesabı tooyour toolog kullanmak hello **Login-AzureRmAccount** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="32ccf-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="32ccf-132">Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="32ccf-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="32ccf-133">Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="32ccf-134">Merhaba cmdlet, hesap ve hello abonelik toouse hello görevler hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="32ccf-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="32ccf-135">Birden fazla aboneliğiniz varsa, tooa farklı aboneliğe geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="32ccf-136">İlk olarak, hesabınız için tüm hello abonelikleri görelim.</span><span class="sxs-lookup"><span data-stu-id="32ccf-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="32ccf-137">Etkin ve devre dışı abonelikler döndürür.</span><span class="sxs-lookup"><span data-stu-id="32ccf-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="32ccf-138">tooswitch tooa farklı abonelik ile Merhaba hello abonelik adını sağlayın **Set-AzureRmContext** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="32ccf-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="32ccf-139">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="32ccf-139">Create a resource group</span></span>
<span data-ttu-id="32ccf-140">Tüm kaynaklar tooyour abonelik dağıtmadan önce hello kaynakları içeren bir kaynak grubu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="32ccf-141">toocreate bir kaynak grubu kullanmak hello **New-AzureRmResourceGroup** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="32ccf-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="32ccf-142">Merhaba komutunu kullanan hello **adı** parametresi toospecify hello kaynak grubu ve hello için bir ad **konumu** parametresi toospecify konumu.</span><span class="sxs-lookup"><span data-stu-id="32ccf-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="32ccf-143">Hello çıktı hello biçimi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="32ccf-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="32ccf-144">Tooretrieve hello kaynak grubu daha sonra gerekirse hello aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="32ccf-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="32ccf-145">tooget tüm kaynak grupları aboneliğinizde Merhaba, bir ad belirtmezseniz:</span><span class="sxs-lookup"><span data-stu-id="32ccf-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="32ccf-146">Kaynakları tooa kaynak grubu Ekle</span><span class="sxs-lookup"><span data-stu-id="32ccf-146">Add resources tooa resource group</span></span>
<span data-ttu-id="32ccf-147">tooadd kaynak toohello kaynak grubu, kullanabileceğiniz hello **yeni AzureRmResource** cmdlet veya kaynak belirli toohello türünde bir cmdlet oluşturmakta (gibi **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="32ccf-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="32ccf-148">Daha kolay toouse hello yeni kaynağı için gerekli hello özellikleri için parametreler içerdiğinden, belirli tooa kaynak türü olan bir cmdlet bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="32ccf-149">toouse **yeni AzureRmResource**, bunlar için istenmeden tüm hello özellikleri tooset bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="32ccf-150">Ancak, Hello yeni kaynak bir Resource Manager şablonu mevcut olmadığından kaynak cmdlet'leri aracılığıyla ekleme gelecekteki karışıklığa neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="32ccf-151">Microsoft Azure, çözümünüz için altyapıyı hello Resource Manager şablonunda tanımlama önerir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="32ccf-152">Şablonları tooreliably etkinleştirin ve tekrar tekrar çözümünüzü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="32ccf-153">Bu konu, bir PowerShell cmdlet'i ile depolama hesabı oluşturma, ancak daha sonra kaynak grubundan bir şablon oluştur.</span><span class="sxs-lookup"><span data-stu-id="32ccf-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="32ccf-154">cmdlet aşağıdaki hello bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="32ccf-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="32ccf-155">Merhaba örnekte gösterilen hello adını kullanmak yerine, hello depolama hesabı için benzersiz bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="32ccf-156">Merhaba adı uzunluğu 3 ile 24 karakter arasında olmalı ve yalnızca rakamlar ve küçük harfler kullanın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="32ccf-157">Merhaba örnekte gösterilen hello adı kullanırsanız, bu ad zaten kullanımda olduğundan, bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="32ccf-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="32ccf-158">Bu kaynak daha sonra tooretrieve gerekirse cmdlet'i aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="32ccf-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="32ccf-159">Etiket ekleme</span><span class="sxs-lookup"><span data-stu-id="32ccf-159">Add a tag</span></span>

<span data-ttu-id="32ccf-160">Etiketler toodifferent özellikleri göre kaynaklarınızı tooorganize etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="32ccf-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="32ccf-161">Örneğin, bazı kaynaklar toohello ait farklı kaynak gruplarında olabilir aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="32ccf-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="32ccf-162">Bir bölüm etiketi ve değer toothose kaynakları toomark uygulayabilirsiniz ait toohello olarak bunları aynı kategori.</span><span class="sxs-lookup"><span data-stu-id="32ccf-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="32ccf-163">Veya, bir kaynak bir üretim veya test ortamında kullanılıp kullanılmadığını işaretleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="32ccf-164">Bu konuda etiketleri tooonly bir kaynak geçerli, ancak ortamınızda büyük olasılıkla tooapply tooall kaynaklarınıza etiketler mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="32ccf-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="32ccf-165">cmdlet aşağıdaki hello iki etiketleri tooyour depolama hesabı geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="32ccf-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="32ccf-166">Etiketler tek bir nesne olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-166">Tags are updated as a single object.</span></span> <span data-ttu-id="32ccf-167">tooadd zaten etiketlerini içeren bir etiket tooa kaynak ilk hello varolan etiketleri alın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="32ccf-168">Merhaba varolan etiketleri içeren hello yeni etiket toohello nesne ekleyin ve tüm hello etiketleri toohello kaynak yeniden uygulayın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="32ccf-169">Kaynakları Ara</span><span class="sxs-lookup"><span data-stu-id="32ccf-169">Search for resources</span></span>

<span data-ttu-id="32ccf-170">Kullanım hello **Bul AzureRmResource** farklı arama koşulu için cmdlet tooretrieve kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="32ccf-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="32ccf-171">tooget adıyla bir kaynak sağlayın hello **ResourceNameContains** parametre:</span><span class="sxs-lookup"><span data-stu-id="32ccf-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="32ccf-172">tooget bir kaynak grubundaki tüm hello kaynaklar sağlar hello **ResourceGroupNameContains** parametre:</span><span class="sxs-lookup"><span data-stu-id="32ccf-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="32ccf-173">tooget bir etiket adı ve değeri, tüm hello kaynaklarla sağlamak hello **TagName** ve **TagValue** Parametreler:</span><span class="sxs-lookup"><span data-stu-id="32ccf-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="32ccf-174">belirli bir kaynak türü, tooall hello kaynaklarla sağlamak hello **ResourceType** parametre:</span><span class="sxs-lookup"><span data-stu-id="32ccf-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="32ccf-175">Bir kaynak Kilitle</span><span class="sxs-lookup"><span data-stu-id="32ccf-175">Lock a resource</span></span>

<span data-ttu-id="32ccf-176">Kritik bir kaynak yanlışlıkla silinmiş veya değiştirilmiş emin toomake gerektiğinde, bir kilit toohello kaynak uygulayın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="32ccf-177">Ya da belirtebilirsiniz bir **CanNotDelete** veya **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="32ccf-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="32ccf-178">Yönetim kilit toocreate ya da delete gerekir erişiminiz çok`Microsoft.Authorization/*` veya `Microsoft.Authorization/locks/*` eylemler.</span><span class="sxs-lookup"><span data-stu-id="32ccf-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="32ccf-179">Merhaba yerleşik rolleri, bu eylemleri yalnızca sahip ve kullanıcı erişimi Yöneticisi verilir.</span><span class="sxs-lookup"><span data-stu-id="32ccf-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="32ccf-180">tooapply bir kilit hello aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="32ccf-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="32ccf-181">Merhaba kilit kaldırılana kadar hello örnek önceki hello kilitli kaynak silinemiyor.</span><span class="sxs-lookup"><span data-stu-id="32ccf-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="32ccf-182">tooremove bir kilit kullanın:</span><span class="sxs-lookup"><span data-stu-id="32ccf-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="32ccf-183">Ayar kilitleri hakkında daha fazla bilgi için bkz: [Azure Resource Manager ile kaynakları kilitleme](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="32ccf-184">Kaynakları veya kaynak grubunu Kaldır</span><span class="sxs-lookup"><span data-stu-id="32ccf-184">Remove resources or resource group</span></span>
<span data-ttu-id="32ccf-185">Bir kaynak veya kaynak grubu kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="32ccf-186">Bir kaynak grubu kaldırdığınızda, bu kaynak grubu içindeki tüm hello kaynaklar da kaldırın.</span><span class="sxs-lookup"><span data-stu-id="32ccf-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="32ccf-187">toodelete hello kaynak grubu, kullanım hello kaynaktan **Kaldır AzureRmResource** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="32ccf-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="32ccf-188">Bu cmdlet hello kaynak siler, ancak hello kaynak grubu silmez.</span><span class="sxs-lookup"><span data-stu-id="32ccf-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="32ccf-189">toodelete bir kaynak grubu ve kendi kaynaklarını kullanmak hello **Remove-AzureRmResourceGroup** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="32ccf-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="32ccf-190">Her iki cmdlet'leri için tooconfirm sorulur tooremove hello kaynağı veya kaynak grubunu istiyor.</span><span class="sxs-lookup"><span data-stu-id="32ccf-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="32ccf-191">Merhaba işlemi başarılı bir şekilde hello kaynağı veya kaynak grubunu silip silmediğini, döndürür **doğru**.</span><span class="sxs-lookup"><span data-stu-id="32ccf-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="32ccf-192">Azure Automation ile Kaynak Yöneticisi komut dosyalarını çalıştır</span><span class="sxs-lookup"><span data-stu-id="32ccf-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="32ccf-193">Bu konu, nasıl gösterir tooperform temel işlemleri kaynaklarınız Azure PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="32ccf-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="32ccf-194">Daha gelişmiş yönetim senaryoları için genellikle toocreate bir komut dosyası istediğiniz ve komut dosyaları gerektiğinde veya bir zamanlamaya göre yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="32ccf-195">[Azure Otomasyonu](../automation/automation-intro.md) Azure çözümleri yönetmek sık kullanılan tooautomate betikleri sizin için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="32ccf-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="32ccf-196">Merhaba aşağıdaki konular, nasıl toouse Azure Otomasyonu, Resource Manager ve PowerShell tooeffectively yönetim görevlerini gerçekleştirme gösterir:</span><span class="sxs-lookup"><span data-stu-id="32ccf-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="32ccf-197">Bir runbook oluşturma hakkında daha fazla bilgi için bkz: [ilk PowerShell runbook'um](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="32ccf-198">Komut dosyaları galerileri ile çalışma hakkında daha fazla bilgi için bkz [Azure Otomasyonu Runbook ve modül galerileri](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="32ccf-199">Başlatma ve durdurma sanal makineleri runbook'lar için bkz: [Azure otomasyonu senaryosu: kullanarak JSON biçimli etiketler toocreate Azure VM başlatma ve kapatma için bir zamanlama](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="32ccf-200">Başlatma ve durdurma sanal makineleri yoğun olmayan saatlerde runbook'lar için bkz: [Başlat/Durdur VM'ler Otomasyon yoğun olmayan saatlerde çözümde sırasında](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="32ccf-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32ccf-201">Next steps</span></span>
* <span data-ttu-id="32ccf-202">Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="32ccf-203">Şablonlar, dağıtımı hakkında toolearn bkz [Azure Resource Manager şablonu ile bir uygulamayı dağıtmak](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="32ccf-204">Mevcut kaynaklar tooa yeni kaynak grubu taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="32ccf-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="32ccf-205">Örnekler için bkz: [kaynakları taşıma tooNew kaynak grubu veya abonelik](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="32ccf-206">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="32ccf-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

