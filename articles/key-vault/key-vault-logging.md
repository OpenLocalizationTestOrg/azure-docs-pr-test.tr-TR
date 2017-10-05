---
title: "Azure Anahtar Kasası Günlüğe Kaydetme | Microsoft Belgeleri"
description: "Azure Anahtar Kasası günlüğü ile çalışmaya başlamada yardım almak için bu öğreticiyi kullanın."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="c8b3d-103">Azure Anahtar Kasası Günlüğü</span><span class="sxs-lookup"><span data-stu-id="c8b3d-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="c8b3d-104">Azure Anahtar Kasası çoğu bölgede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="c8b3d-105">Daha fazla bilgi için bkz. [Anahtar Kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="c8b3d-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="c8b3d-106">Introduction</span></span>
<span data-ttu-id="c8b3d-107">Bir veya daha çok anahtar kasası oluşturduktan sonra, anahtar kasalarınıza nasıl, ne zaman ve kim tarafından erişildiğini büyük olasılıkla izlemek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="c8b3d-108">Anahtar Kasası için günlüğe kaydetmeyi etkinleştirerek bunu yapabilirsiniz; böylece sağladığınız Azure depolama hesabında bilgiler kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="c8b3d-109">Belirttiğiniz depolama hesabı için **insights-logs-auditevent** adlı yeni bir kapsayıcı oluşturulur ve birden çok anahtar kasasının günlüklerini toplamak için bu depolama hesabını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="c8b3d-110">Günlük bilgilerinize anahtar kasası işleminden en fazla 10 dakika sonra erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="c8b3d-111">Çoğu durumda, bundan daha hızlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="c8b3d-112">Depolama hesabınızdaki günlüklerinizi yönetmek size bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="c8b3d-113">Günlüklerinize erişebilecek kişileri kısıtlayarak güvenliklerini sağlamak için standart Azure erişim denetimi yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="c8b3d-114">Artık depolama hesabınızda tutmak istemediğiniz günlükleri silin.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="c8b3d-115">Azure Anahtar Kasası günlüğü ile çalışmaya başlamada yardım almak, depolama hesabınızı oluşturmak, günlüğü etkinleştirmek ve toplanan günlük bilgilerini yorumlamak için bu öğreticiyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="c8b3d-116">Bu öğretici anahtar kasalarının, anahtarların veya gizli anahtarların nasıl oluşturulacağı hakkında yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="c8b3d-117">Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="c8b3d-118">Alternatif olarak, Platformlar Arası Komut Satırı Arabirimi yönergeleri için [bu eşdeğer öğreticiye](key-vault-manage-with-cli2.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="c8b3d-119">Şu anda Azure portalında Azure Anahtar Kasası'nı yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="c8b3d-120">Bunun yerine, bu Azure PowerShell yönergelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="c8b3d-121">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c8b3d-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8b3d-122">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c8b3d-122">Prerequisites</span></span>
<span data-ttu-id="c8b3d-123">Bu öğreticiyi tamamlamak için aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="c8b3d-124">Kullanmakta olduğunuz var olan bir anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="c8b3d-125">Azure PowerShell'in, **en az 1.0.1 sürümü**.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="c8b3d-126">Azure PowerShell'i yüklemek ve Azure aboneliğinizle ilişkilendirmek için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="c8b3d-127">Azure PowerShell'i zaten yüklediyseniz ve sürümünü bilmiyorsanız Azure PowerShell konsolunda `(Get-Module azure -ListAvailable).Version` yazın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="c8b3d-128">Anahtar Kasası günlükleriniz için Azure'da yeterli depolama.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="c8b3d-129"><a id="connect"></a>Aboneliklerinize bağlanma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="c8b3d-130">Bir Azure PowerShell oturumu başlatın ve aşağıdaki komutla Azure hesabınızda oturum açın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="c8b3d-131">Açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="c8b3d-132">Azure PowerShell bu hesapla ilişkili tüm abonelikleri alır ve varsayılan olarak birinciyi kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="c8b3d-133">Birden çok aboneliğiniz varsa Azure Anahtar Kasanızı oluşturmak için kullanılan belirli bir tanesini belirtmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="c8b3d-134">Hesabınız için abonelikleri görmek üzere aşağıdakini yazın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="c8b3d-135">Ardından, günlüğünü tutacağınız anahtar kasasıyla ilişkili aboneliği belirtmek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="c8b3d-136">Bu önemli bir adımdır ve hesabınızla ilişkili birden çok abonelik varsa özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="c8b3d-137">Bu adım atlanırsa Microsoft.Insights’ı kaydetme hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="c8b3d-138">Azure Power Shell'i yapılandırma hakkında daha fazla bilgi için bkz. [Azure PowerShell'i yükleme ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="c8b3d-139"><a id="storage"></a>Günlükleriniz için yeni bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="c8b3d-140">Günlükleriniz için var olan depolama hesabını kullanabiliyor olsanız da, Anahtar Kasası günlüklerine özgü yeni bir depolama hesabı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="c8b3d-141">Bunu daha sonra belirtmemiz gerektiğinde kolaylık sağlamak için ayrıntıları **sa** adlı bir değişkende depolayacağız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="c8b3d-142">Ayrıca, ek yönetim kolaylığı için anahtar kasamızı içeren kaynak grubunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="c8b3d-143">[Başlangıç öğreticisi](key-vault-get-started.md)'nde bu kaynak grubu **ContosoResourceGroup** adına sahiptir ve Doğu Asya konumunu kullanmaya devam edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="c8b3d-144">Bunları uygun şekilde kendi değerlerinizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="c8b3d-145">Var olan bir depolama hesabını kullanmaya karar verirseniz anahtar kasanızla aynı aboneliği kullanmanız gerekir ve bunun da Klasik dağıtım modeli yerine Resource Manager dağıtım modelini kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="c8b3d-146"><a id="identify"></a>Günlükleriniz için anahtar kasasını tanımlama</span><span class="sxs-lookup"><span data-stu-id="c8b3d-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="c8b3d-147">Başlama öğreticimizde anahtar kasamızın adı **ContosoKeyVault**'tu; bu nedenle bu adı kullanmaya ve ayrıntıları **kv** adlı bir değişkende depolamaya devam edeceğiz:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="c8b3d-148"><a id="enable"></a>Günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="c8b3d-149">Anahtar Kasası için günlüğü etkinleştirmek üzere, yeni depolama hesabımız ve anahtar kasamız için oluşturduğumuz değişkenlerle birlikte Set-AzureRmDiagnosticSetting cmdlet'ini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="c8b3d-150">Ayrıca, **-Enabled** bayrağını **$true** olarak ve kategoriyi de AuditEvent (Anahtar Kasası günlüğü için tek kategori budur) olarak ayarlayacağız:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="c8b3d-151">Bunun için çıkış şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="c8b3d-152">Böylece anahtar kasanız için günlüğün artık etkinleştirilmiş ve depolama hesabınıza bilgileri kaydediyor olduğu doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="c8b3d-153">İsteğe bağlı olarak günlükleriniz için eski günlüklerin otomatik olarak silinmesi gibi bir bekletme ilkesi de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="c8b3d-154">Örneğin, **-RetentionEnabled** bayrağını kullanarak bekletme ilkesini **$true** olarak ayarlayın ve **-RetentionInDays** parametresini **90**’a ayarlayarak 90 günden eski günlüklerin otomatik olarak silinmesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="c8b3d-155">Günlüğe kaydedilenler:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-155">What's logged:</span></span>

* <span data-ttu-id="c8b3d-156">Erişim izinleri, sistem hataları veya hatalı istekler sonucunda başarısız olan istekleri içeren tüm kimliği doğrulanmış REST API istekleri günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="c8b3d-157">Oluşturma, silme, anahtar kasası erişim ilkelerini ayarlama ve etiketler gibi anahtar kasası özniteliklerini güncelleştirmeyi kapsayan anahtar kasasının kendisine ait işlemler.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="c8b3d-158">Anahtar kasasındaki anahtarlar ve gizli dizelere yönelik oluşturma, değiştirme veya silmeyi, anahtarları imzalama, doğrulama, şifreleme, şifrelerini çözme, sarmalama ve kaydırmayı, gizli dizeleri almayı ve anahtarları, gizli dizeleri ve bunların sürümlerini listelemeyi kapsayan işlemler.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="c8b3d-159">Bir 401 yanıtına neden olan kimliği doğrulanmamış istekler.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="c8b3d-160">Örneğin, bir taşıyıcı belirtecine sahip olmayan veya hatalı biçimlendirilmiş ya da süresi dolmuş veya geçersiz bir belirtece sahip olan istekler.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="c8b3d-161"><a id="access"></a>Günlüklerinize erişme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="c8b3d-162">Anahtar kasası günlükleri, sağladığınız depolama hesabındaki **insights-logs-auditevent** kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="c8b3d-163">Bu kapsayıcıdaki tüm blobları listelemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="c8b3d-164">İlk olarak, kapsayıcı adı için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-164">First, create a variable for the container name.</span></span> <span data-ttu-id="c8b3d-165">Bu, öğreticinin ilerleyen bölümlerinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="c8b3d-166">Bu kapsayıcıdaki tüm blobları listelemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="c8b3d-167">Çıkış buna benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-167">The output will look something similar to this:</span></span>

<span data-ttu-id="c8b3d-168">**Kapsayıcı Uri'si: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="c8b3d-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="c8b3d-169">**Ad**</span><span class="sxs-lookup"><span data-stu-id="c8b3d-169">**Name**</span></span>

- - -
<span data-ttu-id="c8b3d-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="c8b3d-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="c8b3d-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="c8b3d-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="c8b3d-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="c8b3d-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="c8b3d-173">Bu çıkışta gördüğünüz üzere, bloblar bir adlandırma kuralını izler: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/dosya adı.json**</span><span class="sxs-lookup"><span data-stu-id="c8b3d-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="c8b3d-174">Tarih ve saat değerleri UTC'yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-174">The date and time values use UTC.</span></span>

<span data-ttu-id="c8b3d-175">Aynı depolama hesabı birden çok kaynak için günlük toplamak amacıyla kullanılabileceğinden, blob adındaki tam kaynak kimliğine erişmek veya yalnızca gereksinim duyduğunuz blobları indirmek çok kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="c8b3d-176">Ancak bunu yapmadan önce tüm blobların nasıl indirileceğini ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="c8b3d-177">İlk olarak, blobları yüklemek için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="c8b3d-178">Örnek:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="c8b3d-179">Ardından tüm blobların listesini alın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="c8b3d-180">Blobları hedef klasörümüze indirmek için bu listeye 'Get-AzureStorageBlobContent' aracılığıyla kanal oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="c8b3d-181">Bu ikinci komutu çalıştırdığınızda blob adlarındaki **/** sınırlayıcısı hedef klasörün altında tam bir klasör yapısı oluşturur ve blobları dosya olarak indirmek ve depolamak için bu yapı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="c8b3d-182">Blobları seçmeli olarak indirmek için jokerleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="c8b3d-183">Örnek:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-183">For example:</span></span>

* <span data-ttu-id="c8b3d-184">Birden çok anahtar kasanız varsa ve yalnızca CONTOSOKEYVAULT3 adlı bir anahtar kasası için günlük indirmek isterseniz:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="c8b3d-185">Birden çok kaynak grubunuz varsa ve yalnızca bir kaynak grubu için günlük indirmek isterseniz `-Blob '*/RESOURCEGROUPS/<resource group name>/*'` kullanın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="c8b3d-186">Ocak 2016 ayı için tüm günlükleri indirmek isterseniz `-Blob '*/year=2016/m=01/*'` kullanın:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="c8b3d-187">Artık günlüklerin içinde neler olduğuna bakmaya başlamak için hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="c8b3d-188">Ancak buna geçmeden önce Get-AzureRmDiagnosticSetting için bilmeniz gereken iki parametre daha var:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="c8b3d-189">Anahtar kasası kaynağınızın tanılama ayarlarının durumunu sorgulamak için: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="c8b3d-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="c8b3d-190">Anahtar kasası kaynağınızın günlüğe kaydetmesini devre dışı bırakmak için: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="c8b3d-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="c8b3d-191"><a id="interpret"></a>Anahtar Kasası günlüklerinizi yorumlama</span><span class="sxs-lookup"><span data-stu-id="c8b3d-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="c8b3d-192">Tek tek bloblar JSON blobu olarak biçimlendirilip metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="c8b3d-193">Bu `Get-AzureRmKeyVault -VaultName 'contosokeyvault'` çalıştırılarak oluşturulmuş bir günlük girişi örneğidir:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="c8b3d-194">Aşağıdaki tabloda alan adları ve açıklamaları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="c8b3d-195">Alan adı</span><span class="sxs-lookup"><span data-stu-id="c8b3d-195">Field name</span></span> | <span data-ttu-id="c8b3d-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c8b3d-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c8b3d-197">time</span><span class="sxs-lookup"><span data-stu-id="c8b3d-197">time</span></span> |<span data-ttu-id="c8b3d-198">Tarih ve saat (UTC).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="c8b3d-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="c8b3d-199">resourceId</span></span> |<span data-ttu-id="c8b3d-200">Azure Resource Manager Kaynak Kimliği.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="c8b3d-201">Anahtar Kasası günlükleri için bu her zaman Anahtar Kasası kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="c8b3d-202">operationName</span><span class="sxs-lookup"><span data-stu-id="c8b3d-202">operationName</span></span> |<span data-ttu-id="c8b3d-203">Sonraki tabloda belirtildiği gibi işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="c8b3d-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="c8b3d-204">operationVersion</span></span> |<span data-ttu-id="c8b3d-205">Bu, istemci tarafından istenen REST API'si sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="c8b3d-206">category</span><span class="sxs-lookup"><span data-stu-id="c8b3d-206">category</span></span> |<span data-ttu-id="c8b3d-207">Anahtar Kasası günlükleri için AuditEvent kullanılabilen tek değerdir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="c8b3d-208">resultType</span><span class="sxs-lookup"><span data-stu-id="c8b3d-208">resultType</span></span> |<span data-ttu-id="c8b3d-209">REST API'si isteğinin sonucu.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-209">Result of REST API request.</span></span> |
| <span data-ttu-id="c8b3d-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="c8b3d-210">resultSignature</span></span> |<span data-ttu-id="c8b3d-211">HTTP durumu.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-211">HTTP status.</span></span> |
| <span data-ttu-id="c8b3d-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="c8b3d-212">resultDescription</span></span> |<span data-ttu-id="c8b3d-213">Kullanılabilir olduğunda sonuç hakkında ek açıklama.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="c8b3d-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="c8b3d-214">durationMs</span></span> |<span data-ttu-id="c8b3d-215">Milisaniye cinsinden REST API'si isteğini sunmak için geçen süre.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="c8b3d-216">Buna ağ gecikme süresi dahil değildir; bu nedenle istemci tarafında ölçtüğünüz süre bu süreyle eşleşmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="c8b3d-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="c8b3d-217">callerIpAddress</span></span> |<span data-ttu-id="c8b3d-218">İsteği yapan istemcinin IP adresi.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="c8b3d-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="c8b3d-219">correlationId</span></span> |<span data-ttu-id="c8b3d-220">İstemci tarafı günlüklerini hizmet tarafı (Anahtar Kasası) günlükleriyle ilişkilendirmek için istemcinin geçirebileceği isteğe bağlı bir GUID.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="c8b3d-221">identity</span><span class="sxs-lookup"><span data-stu-id="c8b3d-221">identity</span></span> |<span data-ttu-id="c8b3d-222">REST API'si isteği yapılırken sunulan belirteçten gelen kimlik.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="c8b3d-223">Bu genellikle bir "kullanıcı", "hizmet sorumlusu" veya bir Azure PowerShell cmdlet'inden kaynaklanan bir istekte olduğu gibi "kullanıcı+uygulama kimliği" birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="c8b3d-224">properties</span><span class="sxs-lookup"><span data-stu-id="c8b3d-224">properties</span></span> |<span data-ttu-id="c8b3d-225">Bu alan işleme (operationName) bağlı olarak farklı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="c8b3d-226">Çoğu durumda, istemci bilgilerini (istemci tarafından geçirilen useragent dizesi), REST API'sinin tam istek URI'sini ve HTTP durum kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="c8b3d-227">Buna ek olarak, bir nesne bir istek (örneğin, KeyCreate veya VaultGet) nedeniyle döndürüldüğünde, Anahtar URI'sini ("id" olarak), Kasa URI'sini veya Gizli Anahtar URI'sini de içerir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="c8b3d-228">**operationName** alanının değerleri ObjectVerb biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="c8b3d-229">Örnek:</span><span class="sxs-lookup"><span data-stu-id="c8b3d-229">For example:</span></span>

* <span data-ttu-id="c8b3d-230">Tüm anahtar kasası işlemleri `VaultGet` ve `VaultCreate` gibi 'Vault`<action>`' biçimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="c8b3d-231">Tüm anahtar işlemleri `KeySign` ve `KeyList` gibi 'Key`<action>`' biçimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="c8b3d-232">Tüm gizli anahtar işlemleri `SecretGet` ve `SecretListVersions` gibi 'Secret`<action>`' biçimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="c8b3d-233">Aşağıdaki tabloda operationName ve karşılık gelen REST API'si komutu listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="c8b3d-234">operationName</span><span class="sxs-lookup"><span data-stu-id="c8b3d-234">operationName</span></span> | <span data-ttu-id="c8b3d-235">REST API'si Komutu</span><span class="sxs-lookup"><span data-stu-id="c8b3d-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="c8b3d-236">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c8b3d-236">Authentication</span></span> |<span data-ttu-id="c8b3d-237">Azure Active Directory uç noktası aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="c8b3d-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="c8b3d-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="c8b3d-238">VaultGet</span></span> |[<span data-ttu-id="c8b3d-239">Bir anahtar kasası hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="c8b3d-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="c8b3d-240">VaultPut</span></span> |[<span data-ttu-id="c8b3d-241">Anahtar kasası oluşturma veya güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="c8b3d-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="c8b3d-242">VaultDelete</span></span> |[<span data-ttu-id="c8b3d-243">Anahtar kasası silme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="c8b3d-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="c8b3d-244">VaultPatch</span></span> |[<span data-ttu-id="c8b3d-245">Bir anahtar kasasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="c8b3d-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="c8b3d-246">VaultList</span></span> |[<span data-ttu-id="c8b3d-247">Bir kaynak grubundaki tüm anahtar kasalarını listeleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="c8b3d-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="c8b3d-248">KeyCreate</span></span> |[<span data-ttu-id="c8b3d-249">Anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="c8b3d-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="c8b3d-250">KeyGet</span></span> |[<span data-ttu-id="c8b3d-251">Bir anahtar hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="c8b3d-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="c8b3d-252">KeyImport</span></span> |[<span data-ttu-id="c8b3d-253">Bir kasaya anahtar aktarma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="c8b3d-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="c8b3d-254">KeyBackup</span></span> |<span data-ttu-id="c8b3d-255">[Bir anahtarı yedekleme](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="c8b3d-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="c8b3d-256">KeyDelete</span></span> |[<span data-ttu-id="c8b3d-257">Anahtar silme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="c8b3d-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="c8b3d-258">KeyRestore</span></span> |[<span data-ttu-id="c8b3d-259">Bir anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="c8b3d-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="c8b3d-260">KeySign</span></span> |[<span data-ttu-id="c8b3d-261">Bir anahtar ile oturum açma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="c8b3d-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="c8b3d-262">KeyVerify</span></span> |[<span data-ttu-id="c8b3d-263">Bir anahtar ile doğrulama</span><span class="sxs-lookup"><span data-stu-id="c8b3d-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="c8b3d-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="c8b3d-264">KeyWrap</span></span> |[<span data-ttu-id="c8b3d-265">Bir anahtarı sarmalama</span><span class="sxs-lookup"><span data-stu-id="c8b3d-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="c8b3d-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="c8b3d-266">KeyUnwrap</span></span> |[<span data-ttu-id="c8b3d-267">Bir anahtarı kaydırma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="c8b3d-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="c8b3d-268">KeyEncrypt</span></span> |[<span data-ttu-id="c8b3d-269">Bir anahtar ile şifreleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="c8b3d-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="c8b3d-270">KeyDecrypt</span></span> |[<span data-ttu-id="c8b3d-271">Bir anahtar ile şifre çözme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="c8b3d-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="c8b3d-272">KeyUpdate</span></span> |[<span data-ttu-id="c8b3d-273">Bir anahtarı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="c8b3d-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="c8b3d-274">KeyList</span></span> |[<span data-ttu-id="c8b3d-275">Bir kasadaki anahtarları listeleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="c8b3d-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="c8b3d-276">KeyListVersions</span></span> |[<span data-ttu-id="c8b3d-277">Bir anahtarın sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="c8b3d-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="c8b3d-278">SecretSet</span></span> |[<span data-ttu-id="c8b3d-279">Gizli anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="c8b3d-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="c8b3d-280">SecretGet</span></span> |[<span data-ttu-id="c8b3d-281">Gizli anahtar alma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="c8b3d-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="c8b3d-282">SecretUpdate</span></span> |[<span data-ttu-id="c8b3d-283">Gizli anahtarı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="c8b3d-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="c8b3d-284">SecretDelete</span></span> |[<span data-ttu-id="c8b3d-285">Gizli anahtarı silme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="c8b3d-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="c8b3d-286">SecretList</span></span> |[<span data-ttu-id="c8b3d-287">Bir kasadaki gizli anahtarları listeleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="c8b3d-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="c8b3d-288">SecretListVersions</span></span> |[<span data-ttu-id="c8b3d-289">Bir gizli anahtarın sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="c8b3d-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="c8b3d-290"><a id="loganalytics"></a>Log Analytics'i kullanma</span><span class="sxs-lookup"><span data-stu-id="c8b3d-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="c8b3d-291">Azure Key Vault AuditEvent günlüklerini incelemek için Log Analytics içindeki Azure Key Vault çözümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="c8b3d-292">Kurulum adımları ve daha fazla bilgi için bkz. [Log Analytics'te Azure Key Vault çözümü](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="c8b3d-293">Bu makalede ayrıca Log Analytics önizlemesinde sunulan ve günlüklerinizi önce bir Azure Depolama hesabına yönlendirip Log Analytics'i bu konumdan okuyacak şekilde yapılandırdığınız eski Key Vault çözümünden geçiş yapmak için kullanabileceğiniz talimatlara da yer verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c8b3d-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="c8b3d-294"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8b3d-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="c8b3d-295">Azure Anahtar Kasası'nın bir web uygulamasında kullanıldığı bir öğretici için bkz. [Azure Anahtar Kasası'nı bir Web Uygulamasından Kullanma](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="c8b3d-296">Programlama başvuruları için bkz. [Azure Anahtar Kasası geliştirici kılavuzu](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="c8b3d-297">Azure Anahtar Kasası'na yönelik Azure PowerShell 1.0 cmdlet'leri listesi için bkz. [Azure Anahtar Kasası Cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="c8b3d-298">Azure Anahtar Kasası ile anahtar döndürme ve günlük denetimine ilişkin bir öğretici için bkz. [Uçtan uca anahtar döndürme ve denetim ile Anahtar Kasası ayarlama](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="c8b3d-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
