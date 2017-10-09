---
title: "aaaAzure kapsayıcı kayıt defteri depoları | Microsoft Docs"
description: "Nasıl toouse Azure kapsayıcı kayıt defteri depoları Docker görüntüleri"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="0a523-103">Hello Azure PowerShell kullanarak özel bir Docker kapsayıcısı kayıt oluşturun</span><span class="sxs-lookup"><span data-stu-id="0a523-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="0a523-104">Komutlarda kullanmak [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate bir kapsayıcı kayıt defteri ve ayarlarını Windows bilgisayarınızdan yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a523-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="0a523-105">Ayrıca oluşturmak ve kapsayıcı kayıt defterleri hello kullanarak yönetmek [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), veya program aracılığıyla hello kapsayıcı kayıt defteri [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="0a523-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="0a523-106">Arka plan ve kavramları için bkz: [hello genel bakış](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="0a523-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="0a523-107">Desteklenen cmdlet'leri tam bir listesi için bkz: [Azure kapsayıcı kayıt defteri yönetimi cmdlet'leri](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="0a523-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0a523-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0a523-108">Prerequisites</span></span>
* <span data-ttu-id="0a523-109">**Azure PowerShell**: tooinstall ve Azure PowerShell ile çalışmaya başlama bkz hello [yükleme yönergeleri](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0a523-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="0a523-110">Çalıştırarak tooyour Azure aboneliği oturum `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="0a523-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="0a523-111">Daha fazla bilgi için bkz: [Azure PowerShell ile çalışmaya başlama](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="0a523-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="0a523-112">**Kaynak grubu**: Kapsayıcı kayıt defteri oluşturmadan önce bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups) oluşturun veya mevcut bir kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a523-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="0a523-113">Merhaba kaynak grubu hello kapsayıcı kayıt defteri hizmeti olduğu bir konumda olduğundan emin olun [kullanılabilir](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="0a523-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="0a523-114">toocreate Azure PowerShell kullanarak bir kaynak grubu bkz [PowerShell başvurusu hello](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="0a523-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="0a523-115">**Depolama hesabı** (isteğe bağlı): bir standart Azure oluşturma [depolama hesabı](../storage/common/storage-introduction.md) tooback hello kapsayıcı hello kayıt defterinde aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="0a523-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="0a523-116">Kayıt defteri ile oluştururken, bir depolama hesabı belirtmezseniz `New-AzureRMContainerRegistry`, hello komut sizin için bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a523-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="0a523-117">bir depolama toocreate PowerShell kullanarak hesap için bkz: [PowerShell başvurusu hello](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="0a523-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="0a523-118">Premium Depolama şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="0a523-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="0a523-119">**Hizmet sorumlusu** (isteğe bağlı): bir kayıt defteri PowerShell ile oluşturduğunuzda, varsayılan olarak, erişim için kurulu değil.</span><span class="sxs-lookup"><span data-stu-id="0a523-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="0a523-120">Gereksinimlerinize bağlı olarak, varolan bir Azure Active Directory hizmet asıl tooa kayıt atayın veya oluşturun ve yeni bir tane atayın.</span><span class="sxs-lookup"><span data-stu-id="0a523-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="0a523-121">Alternatif olarak, hello kayıt defterindeki yönetici kullanıcı hesabı etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a523-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="0a523-122">Bu makalenin sonraki bölümlerinde Hello bölümlere bakın.</span><span class="sxs-lookup"><span data-stu-id="0a523-122">See hello sections later in this article.</span></span> <span data-ttu-id="0a523-123">Kayıt defteri erişim hakkında daha fazla bilgi için bkz: [hello kapsayıcı kayıt defteri ile kimlik doğrulama](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0a523-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="0a523-124">Kapsayıcı kayıt defteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a523-124">Create a container registry</span></span>
<span data-ttu-id="0a523-125">Merhaba çalıştırmak `New-AzureRMContainerRegistry` komutu toocreate bir kapsayıcı kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="0a523-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="0a523-126">Bir kayıt defteri oluştururken yalnızca harf ve sayı içeren genel olarak benzersiz bir üst düzey etki alanı adı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="0a523-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="0a523-127">Merhaba kayıt defteri adı hello örneklerde `MyRegistry`, ancak kendi benzersiz adı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0a523-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="0a523-128">kullandığı hello en az parametreleri toocreate kapsayıcı kayıt defteri komutu aşağıdaki hello `MyRegistry` hello kaynak grubunda `MyResourceGroup` hello Orta Güney ABD konum içinde:</span><span class="sxs-lookup"><span data-stu-id="0a523-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="0a523-129">`-StorageAccountName` isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0a523-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="0a523-130">Yoksa belirtilen hello kayıt defteri adını oluşan bir ada sahip bir depolama hesabı oluşturulur ve kaynak grubu bir zaman damgasına hello belirtilen.</span><span class="sxs-lookup"><span data-stu-id="0a523-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="0a523-131">Hizmet sorumlusu atama</span><span class="sxs-lookup"><span data-stu-id="0a523-131">Assign a service principal</span></span>
<span data-ttu-id="0a523-132">PowerShell komutları tooassign bir Azure Active Directory kullanmak [hizmet sorumlusu](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa kayıt defteri.</span><span class="sxs-lookup"><span data-stu-id="0a523-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="0a523-133">Merhaba hizmet sorumlusu Bu örneklerde hello sahibi rolü atanmış, ancak atayabilirsiniz [diğer rolleri](../active-directory/role-based-access-control-configure.md) istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="0a523-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="0a523-134">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a523-134">Create a service principal</span></span>
<span data-ttu-id="0a523-135">Komutu aşağıdaki hello, yeni bir hizmet sorumlusu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0a523-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="0a523-136">Güçlü bir parola ile Merhaba belirtin `-Password` parametresi.</span><span class="sxs-lookup"><span data-stu-id="0a523-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="0a523-137">Yeni veya var olan hizmet sorumlusu atayın</span><span class="sxs-lookup"><span data-stu-id="0a523-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="0a523-138">Yeni veya varolan bir hizmet asıl tooa kayıt atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a523-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="0a523-139">tooassign, örneğin aşağıdaki komut benzer toohello çalıştırmak sahibi rolü erişim toohello kayıt defteri,:</span><span class="sxs-lookup"><span data-stu-id="0a523-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="0a523-140">Oturum açma toohello kayıt defteri hello hizmet sorumlusu ile</span><span class="sxs-lookup"><span data-stu-id="0a523-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="0a523-141">Merhaba hizmet asıl toohello kayıt defteri atadıktan sonra komutu aşağıdaki hello kullanarak oturum açabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0a523-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="0a523-142">Yönetici kimlik bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="0a523-142">Manage admin credentials</span></span>
<span data-ttu-id="0a523-143">Her kapsayıcı kayıt defteri için otomatik olarak bir yönetici hesabı oluşturulur ve varsayılan olarak devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="0a523-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="0a523-144">Merhaba aşağıdaki PowerShell komutlarını toomanage hello yönetici kimlik bilgilerini kapsayıcı kaydınız örnekler.</span><span class="sxs-lookup"><span data-stu-id="0a523-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="0a523-145">Yönetici kullanıcı kimlik bilgileri edinme</span><span class="sxs-lookup"><span data-stu-id="0a523-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="0a523-146">Mevcut bir kayıt defteri için yönetici kullanıcıyı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="0a523-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="0a523-147">Mevcut bir kayıt defteri için yönetici kullanıcıyı devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="0a523-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="0a523-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0a523-148">Next steps</span></span>
* [<span data-ttu-id="0a523-149">Merhaba Docker CLI kullanarak ilk görüntünüzü bildirme</span><span class="sxs-lookup"><span data-stu-id="0a523-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
