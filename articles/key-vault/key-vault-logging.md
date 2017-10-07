---
title: "aaaAzure anahtar kasası günlüğü | Microsoft Docs"
description: "Azure anahtar kasası kullanmaya başlama Öğreticisi bu toohelp kullanmak günlüğü."
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
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="d6621-103">Azure Anahtar Kasası Günlüğü</span><span class="sxs-lookup"><span data-stu-id="d6621-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="d6621-104">Azure Anahtar Kasası çoğu bölgede kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d6621-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="d6621-105">Daha fazla bilgi için bkz: Merhaba [anahtar kasası fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="d6621-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="d6621-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="d6621-106">Introduction</span></span>
<span data-ttu-id="d6621-107">Bir veya daha fazla anahtar kasası oluşturduktan sonra büyük olasılıkla erişilen ve kim tarafından ne zaman ve nasıl anahtarınızı kasaları toomonitor isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="d6621-108">Anahtar Kasası için günlüğe kaydetmeyi etkinleştirerek bunu yapabilirsiniz; böylece sağladığınız Azure depolama hesabında bilgiler kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d6621-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="d6621-109">Belirttiğiniz depolama hesabı için **insights-logs-auditevent** adlı yeni bir kapsayıcı oluşturulur ve birden çok anahtar kasasının günlüklerini toplamak için bu depolama hesabını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="d6621-110">En fazla günlük bilgilerinize erişebilir, 10 dakika sonra hello anahtar kasası işleminden.</span><span class="sxs-lookup"><span data-stu-id="d6621-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="d6621-111">Çoğu durumda, bundan daha hızlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d6621-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="d6621-112">Depolama hesabınızdaki günlüklerinizi tooyou toomanage öyledir:</span><span class="sxs-lookup"><span data-stu-id="d6621-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="d6621-113">Standart Azure erişim denetimi yöntemlerini toosecure günlüklerinize erişebilecek kişileri kısıtlayarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6621-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="d6621-114">Artık depolama hesabınız tookeep, istediğiniz günlükleri silin.</span><span class="sxs-lookup"><span data-stu-id="d6621-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="d6621-115">Azure anahtar, kasası günlüğü ile toocreate Başlarken Bu öğretici toohelp kullanmak depolama hesabınızın günlüğe yazılmasını etkinleştirmek ve toplanan hello günlük bilgilerini yorumlamak.</span><span class="sxs-lookup"><span data-stu-id="d6621-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="d6621-116">Bu öğretici toocreate nasıl anahtar kasalarının, anahtarların veya gizli için yönergeler içermez.</span><span class="sxs-lookup"><span data-stu-id="d6621-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="d6621-117">Bu bilgi için bkz. [Azure Anahtar Kasası ile çalışmaya başlama](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d6621-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="d6621-118">Alternatif olarak, Platformlar Arası Komut Satırı Arabirimi yönergeleri için [bu eşdeğer öğreticiye](key-vault-manage-with-cli2.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="d6621-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="d6621-119">Şu anda hello Azure portalında Azure anahtar kasası yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="d6621-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="d6621-120">Bunun yerine, bu Azure PowerShell yönergelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6621-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="d6621-121">Azure Anahtar Kasası genel bakış bilgileri için bkz. [Azure Anahtar Kasası nedir?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="d6621-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6621-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d6621-122">Prerequisites</span></span>
<span data-ttu-id="d6621-123">toocomplete Bu öğreticiyi izleyerek hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="d6621-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d6621-124">Kullanmakta olduğunuz var olan bir anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="d6621-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="d6621-125">Azure PowerShell'in, **en az 1.0.1 sürümü**.</span><span class="sxs-lookup"><span data-stu-id="d6621-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="d6621-126">tooinstall Azure PowerShell ve Azure aboneliğinizle ilişkilendirmek için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6621-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="d6621-127">Azure PowerShell'i zaten yüklediyseniz ve hello sürüm hello Azure PowerShell konsolundan bilmiyorsanız, çalışamazsa `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="d6621-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="d6621-128">Anahtar Kasası günlükleriniz için Azure'da yeterli depolama.</span><span class="sxs-lookup"><span data-stu-id="d6621-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="d6621-129"><a id="connect"></a>Tooyour abonelikleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="d6621-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="d6621-130">Bir Azure PowerShell oturumu Başlat ve tooyour Azure hesabı komutu aşağıdaki hello ile oturum açın:</span><span class="sxs-lookup"><span data-stu-id="d6621-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="d6621-131">Merhaba açılır tarayıcı penceresinde Azure hesabı kullanıcı adınızı ve parolanızı girin.</span><span class="sxs-lookup"><span data-stu-id="d6621-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="d6621-132">Azure PowerShell varsayılan olarak bu hesap ile ilişkilendirilmiş tüm hello abonelikleri alır, birinci kullanır hello.</span><span class="sxs-lookup"><span data-stu-id="d6621-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="d6621-133">Birden çok aboneliğiniz varsa, kullanılan toocreate olan belirli bir toospecify olabilir, Azure anahtar kasası.</span><span class="sxs-lookup"><span data-stu-id="d6621-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="d6621-134">Merhaba toosee hello abonelikleri hesabınız için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d6621-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="d6621-135">Günlüğünü tutacağınız, anahtar kasasıyla türü ilişkili ardından toospecify hello abonelik:</span><span class="sxs-lookup"><span data-stu-id="d6621-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="d6621-136">Bu önemli bir adımdır ve hesabınızla ilişkili birden çok abonelik varsa özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="d6621-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="d6621-137">Bu adım atlanır içeriyorsa bir hata tooregister Microsoft.ınsights alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="d6621-138">Azure PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6621-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="d6621-139"><a id="storage"></a>Günlükleriniz için yeni bir depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6621-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="d6621-140">Günlükleriniz için var olan depolama hesabını kullanabilmenize karşın, ayrılmış tooKey kasası günlükleri olacak yeni bir depolama hesabı oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="d6621-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="d6621-141">Ne zaman toospecify bu sahibiz kolaylık sağlamak için daha sonra biz adlı bir değişkende hello ayrıntıları depolayacağınız **sa**.</span><span class="sxs-lookup"><span data-stu-id="d6621-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="d6621-142">Ek yönetim kolaylığı için aynı zamanda kullanacağız anahtar kasamızı içeren bir hello gibi hello aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="d6621-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="d6621-143">Merhaba gelen [başlama Öğreticisi](key-vault-get-started.md), bu kaynak grubu adında **ContosoResourceGroup** ve toouse hello Doğu Asya konumunu devam edeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d6621-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="d6621-144">Bunları uygun şekilde kendi değerlerinizle değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d6621-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="d6621-145">Toouse mevcut bir depolama hesabını karar verirseniz, kullanmanız gereken anahtar kasanızı ve hello Klasik dağıtım modeli yerine hello Resource Manager dağıtım modeli kullanmanız gerektiği gibi aynı abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="d6621-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="d6621-146"><a id="identify"></a>Merhaba anahtar kasası günlükleriniz için tanımlayın</span><span class="sxs-lookup"><span data-stu-id="d6621-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="d6621-147">Bizim alma başlatılan öğreticide öğreticimizde anahtar kasamızın adı olan **ContosoKeyVault**, ad ve hello ayrıntıları adlı bir değişkende depolamaya toouse devam edeceğiz **kv**:</span><span class="sxs-lookup"><span data-stu-id="d6621-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="d6621-148"><a id="enable"></a>Günlüğe kaydetmeyi etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d6621-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="d6621-149">tooenable anahtar kasası için günlüğe kaydetme, hello Set-AzureRmDiagnosticSetting cmdlet'ini kullanacağız, hello değişkenleri ile birlikte yeni depolama hesabımız ve anahtar kasamız için oluşturduğumuz.</span><span class="sxs-lookup"><span data-stu-id="d6621-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="d6621-150">Merhaba ayrıca yaparız **-etkin** çok bayrak**$true** ve hello kategori tooAuditEvent (Merhaba yalnızca kategori anahtar kasası günlüğü için) olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d6621-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="d6621-151">Bunun için Hello çıkış şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="d6621-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="d6621-152">Bu günlük kaydı bilgileri tooyour depolama hesabı kaydedilirken anahtar kasanız için şimdi etkin olduğunu doğrular.</span><span class="sxs-lookup"><span data-stu-id="d6621-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="d6621-153">İsteğe bağlı olarak günlükleriniz için eski günlüklerin otomatik olarak silinmesi gibi bir bekletme ilkesi de ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="d6621-154">Örneğin, bekletme ilkesi kullanılarak ayarlanan **- RetentionEnabled** çok bayrak**$true** ve **- RetentionInDays** parametresi çok**90** şekilde 90 günden daha eski günlükleri otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="d6621-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="d6621-155">Günlüğe kaydedilenler:</span><span class="sxs-lookup"><span data-stu-id="d6621-155">What's logged:</span></span>

* <span data-ttu-id="d6621-156">Erişim izinleri, sistem hataları veya hatalı istekler sonucunda başarısız olan istekleri içeren tüm kimliği doğrulanmış REST API istekleri günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d6621-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="d6621-157">Operations hello anahtarı oluşturma, silme, ayarı anahtar kasası erişim ilkelerini içeren, kendi, kasa ve etiketler gibi anahtar kasası öznitelikler güncelleştiriliyor.</span><span class="sxs-lookup"><span data-stu-id="d6621-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="d6621-158">Anahtarları ve gizli anahtarları oluşturma, değiştirme veya bu bir anahtar veya gizli anahtarları silme içerir hello anahtar kasasında işlemleri; oturum gibi işlemleri doğrulayın, şifrelemek, şifresini, sarmalama ve anahtarları kaydırma, gizli, anahtarları ve gizli anahtarları ve sürümlerine Al.</span><span class="sxs-lookup"><span data-stu-id="d6621-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="d6621-159">Bir 401 yanıtına neden olan kimliği doğrulanmamış istekler.</span><span class="sxs-lookup"><span data-stu-id="d6621-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="d6621-160">Örneğin, bir taşıyıcı belirtecine sahip olmayan veya hatalı biçimlendirilmiş ya da süresi dolmuş veya geçersiz bir belirtece sahip olan istekler.</span><span class="sxs-lookup"><span data-stu-id="d6621-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="d6621-161"><a id="access"></a>Günlüklerinize erişme</span><span class="sxs-lookup"><span data-stu-id="d6621-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="d6621-162">Anahtar kasası günlükleri hello depolanan **insights-logs-auditevent** hello depolama hesabı sağladığınız kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="d6621-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="d6621-163">toolist bu kapsayıcıdaki tüm hello BLOB'lar yazın:</span><span class="sxs-lookup"><span data-stu-id="d6621-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="d6621-164">İlk olarak hello kapsayıcı adı için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6621-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="d6621-165">Merhaba ilerlemesi hello kalanı boyunca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d6621-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="d6621-166">toolist bu kapsayıcıdaki tüm hello BLOB'lar yazın:</span><span class="sxs-lookup"><span data-stu-id="d6621-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="d6621-167">Merhaba çıkış benzeri toothis görünür:</span><span class="sxs-lookup"><span data-stu-id="d6621-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="d6621-168">**Kapsayıcı Uri'si: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="d6621-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="d6621-169">**Ad**</span><span class="sxs-lookup"><span data-stu-id="d6621-169">**Name**</span></span>

- - -
<span data-ttu-id="d6621-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="d6621-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="d6621-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="d6621-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="d6621-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="d6621-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="d6621-173">Bu Çıkışta gördüğünüz gibi hello bloblar bir adlandırma kuralını izler: **ResourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m = <minute> /dosya adı.JSON**</span><span class="sxs-lookup"><span data-stu-id="d6621-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="d6621-174">Merhaba tarih ve saat değerleri UTC'yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d6621-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="d6621-175">Merhaba aynı depolama hesabı birden fazla kaynak için kullanılan toocollect günlükleri olabileceğinden, hello hello blob adındaki tam kaynak kimliği çok kullanışlı tooaccess veya gereksinim duyduğunuz indirme yalnızca hello BLOB'lar değil.</span><span class="sxs-lookup"><span data-stu-id="d6621-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="d6621-176">Ancak bunu yapmadan önce biz değineceğiz nasıl toodownload tüm BLOB'ları hello.</span><span class="sxs-lookup"><span data-stu-id="d6621-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="d6621-177">İlk olarak, bir klasör toodownload hello BLOB'lar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6621-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="d6621-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d6621-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="d6621-179">Ardından tüm blobların listesini alın:</span><span class="sxs-lookup"><span data-stu-id="d6621-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="d6621-180">Bu liste 'Get-AzureStorageBlobContent' toodownload hello BLOB'ları aracılığıyla bizim hedef klasöre kanal:</span><span class="sxs-lookup"><span data-stu-id="d6621-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="d6621-181">Bu ikinci komutu çalıştırdığınızda, hello  **/**  hello blob adlarındaki sınırlayıcı hello hedef klasörün altında tam klasör yapısı oluşturun ve bu yapı dosyaları olarak kullanılan toodownload ve deposu hello BLOB'lar olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d6621-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="d6621-182">tooselectively blobları indirmek, joker karakter kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6621-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="d6621-183">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d6621-183">For example:</span></span>

* <span data-ttu-id="d6621-184">Birden çok anahtar kasanız varsa ve yalnızca bir anahtar kasası için toodownload günlükleri istiyorsanız CONTOSOKEYVAULT3 adlı:</span><span class="sxs-lookup"><span data-stu-id="d6621-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="d6621-185">Birden çok kaynak gruplarınız ve yalnızca bir kaynak grubu için toodownload günlükleri istiyorsanız kullanın `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="d6621-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="d6621-186">Merhaba Ocak 2016 ayı için tüm hello günlüklerini toodownload istiyorsanız, kullanmak `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="d6621-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="d6621-187">Hello neler olduğuna bakmaya hazır toostart oturum artık olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="d6621-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="d6621-188">Ancak, Get-AzureRmDiagnosticSetting tooknow gerekebilecek için iki parametre daha üzerine geçmeden önce:</span><span class="sxs-lookup"><span data-stu-id="d6621-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="d6621-189">anahtar kasası kaynağınızın tanılama ayarlarının tooquery hello durumu:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="d6621-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="d6621-190">anahtar kasası kaynağınızın için toodisable günlüğü:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="d6621-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="d6621-191"><a id="interpret"></a>Anahtar Kasası günlüklerinizi yorumlama</span><span class="sxs-lookup"><span data-stu-id="d6621-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="d6621-192">Tek tek bloblar JSON blobu olarak biçimlendirilip metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="d6621-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="d6621-193">Bu `Get-AzureRmKeyVault -VaultName 'contosokeyvault'` çalıştırılarak oluşturulmuş bir günlük girişi örneğidir:</span><span class="sxs-lookup"><span data-stu-id="d6621-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="d6621-194">Merhaba aşağıdaki tabloda hello alan adları ve açıklamaları listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d6621-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="d6621-195">Alan adı</span><span class="sxs-lookup"><span data-stu-id="d6621-195">Field name</span></span> | <span data-ttu-id="d6621-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d6621-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d6621-197">time</span><span class="sxs-lookup"><span data-stu-id="d6621-197">time</span></span> |<span data-ttu-id="d6621-198">Tarih ve saat (UTC).</span><span class="sxs-lookup"><span data-stu-id="d6621-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="d6621-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="d6621-199">resourceId</span></span> |<span data-ttu-id="d6621-200">Azure Resource Manager Kaynak Kimliği.</span><span class="sxs-lookup"><span data-stu-id="d6621-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="d6621-201">Anahtar kasası günlükleri için bu her zaman hello anahtar kasası kaynak kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="d6621-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="d6621-202">operationName</span><span class="sxs-lookup"><span data-stu-id="d6621-202">operationName</span></span> |<span data-ttu-id="d6621-203">Merhaba sonraki tabloda belirtildiği gibi hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="d6621-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="d6621-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="d6621-204">operationVersion</span></span> |<span data-ttu-id="d6621-205">Bu hello istemci tarafından istenilen hello REST API'si sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="d6621-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="d6621-206">category</span><span class="sxs-lookup"><span data-stu-id="d6621-206">category</span></span> |<span data-ttu-id="d6621-207">Anahtar kasası günlükleri için AuditEvent hello tek ve kullanılabilir bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="d6621-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="d6621-208">resultType</span><span class="sxs-lookup"><span data-stu-id="d6621-208">resultType</span></span> |<span data-ttu-id="d6621-209">REST API'si isteğinin sonucu.</span><span class="sxs-lookup"><span data-stu-id="d6621-209">Result of REST API request.</span></span> |
| <span data-ttu-id="d6621-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="d6621-210">resultSignature</span></span> |<span data-ttu-id="d6621-211">HTTP durumu.</span><span class="sxs-lookup"><span data-stu-id="d6621-211">HTTP status.</span></span> |
| <span data-ttu-id="d6621-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="d6621-212">resultDescription</span></span> |<span data-ttu-id="d6621-213">Kullanılabilir olduğunda hello sonuç hakkında ek açıklama.</span><span class="sxs-lookup"><span data-stu-id="d6621-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="d6621-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="d6621-214">durationMs</span></span> |<span data-ttu-id="d6621-215">Milisaniye cinsinden tooservice hello REST API isteği, geçen süre.</span><span class="sxs-lookup"><span data-stu-id="d6621-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="d6621-216">Hello istemci tarafında ölçmek hello süre bu süreyle eşleşmeyebilir şekilde bu hello ağ gecikmesini içermez.</span><span class="sxs-lookup"><span data-stu-id="d6621-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="d6621-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="d6621-217">callerIpAddress</span></span> |<span data-ttu-id="d6621-218">Merhaba isteği yapan hello istemci IP adresi.</span><span class="sxs-lookup"><span data-stu-id="d6621-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="d6621-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="d6621-219">correlationId</span></span> |<span data-ttu-id="d6621-220">İstemci hello isteğe bağlı bir GUID toocorrelate istemci-tarafı günlüklerini Hizmet tarafı (anahtar kasası) günlükleriyle geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="d6621-221">identity</span><span class="sxs-lookup"><span data-stu-id="d6621-221">identity</span></span> |<span data-ttu-id="d6621-222">Merhaba REST API'si isteği yapılırken sunulan hello belirteç kimlik.</span><span class="sxs-lookup"><span data-stu-id="d6621-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="d6621-223">Bu genellikle bir "kullanıcı", "hizmet sorumlusu" veya bir Azure PowerShell cmdlet'inden kaynaklanan bir istekte olduğu gibi "kullanıcı+uygulama kimliği" birleşimidir.</span><span class="sxs-lookup"><span data-stu-id="d6621-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="d6621-224">properties</span><span class="sxs-lookup"><span data-stu-id="d6621-224">properties</span></span> |<span data-ttu-id="d6621-225">Bu alan hello işleme (operationName) bağlı olarak farklı bilgiler içerir.</span><span class="sxs-lookup"><span data-stu-id="d6621-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="d6621-226">Çoğu durumda, istemci bilgilerini (Merhaba istemci tarafından geçirilen hello useragent dizesi) içeren REST API'SİNİN tam istek URI'sini ve HTTP durum kodu hello.</span><span class="sxs-lookup"><span data-stu-id="d6621-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="d6621-227">Ayrıca, bir nesne bir istek (örneğin, KeyCreate veya VaultGet) nedeniyle döndürüldüğünde anahtar URI'sini ("id") olarak, kasa URI'sini veya gizli anahtar URI'sini hello içerecektir.</span><span class="sxs-lookup"><span data-stu-id="d6621-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="d6621-228">Merhaba **operationName** alan değerleri ObjectVerb biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="d6621-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="d6621-229">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="d6621-229">For example:</span></span>

* <span data-ttu-id="d6621-230">Tüm anahtar kasası işlemleri hello sahip ' kasası`<action>`' gibi biçimde `VaultGet` ve `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="d6621-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="d6621-231">Tüm anahtar işlemleri hello sahip ' anahtar`<action>`' gibi biçimde `KeySign` ve `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="d6621-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="d6621-232">Tüm gizli anahtar işlemleri hello sahip ' gizli`<action>`' gibi biçimde `SecretGet` ve `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="d6621-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="d6621-233">Aşağıdaki tablonun hello hello operationName ve karşılık gelen REST API'si komutu listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d6621-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="d6621-234">operationName</span><span class="sxs-lookup"><span data-stu-id="d6621-234">operationName</span></span> | <span data-ttu-id="d6621-235">REST API'si Komutu</span><span class="sxs-lookup"><span data-stu-id="d6621-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="d6621-236">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="d6621-236">Authentication</span></span> |<span data-ttu-id="d6621-237">Azure Active Directory uç noktası aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="d6621-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="d6621-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="d6621-238">VaultGet</span></span> |[<span data-ttu-id="d6621-239">Bir anahtar kasası hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="d6621-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="d6621-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="d6621-240">VaultPut</span></span> |[<span data-ttu-id="d6621-241">Anahtar kasası oluşturma veya güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6621-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="d6621-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="d6621-242">VaultDelete</span></span> |[<span data-ttu-id="d6621-243">Anahtar kasası silme</span><span class="sxs-lookup"><span data-stu-id="d6621-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="d6621-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="d6621-244">VaultPatch</span></span> |[<span data-ttu-id="d6621-245">Bir anahtar kasasını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6621-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="d6621-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="d6621-246">VaultList</span></span> |[<span data-ttu-id="d6621-247">Bir kaynak grubundaki tüm anahtar kasalarını listeleme</span><span class="sxs-lookup"><span data-stu-id="d6621-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="d6621-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="d6621-248">KeyCreate</span></span> |[<span data-ttu-id="d6621-249">Anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6621-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="d6621-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="d6621-250">KeyGet</span></span> |[<span data-ttu-id="d6621-251">Bir anahtar hakkında bilgi edinme</span><span class="sxs-lookup"><span data-stu-id="d6621-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="d6621-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="d6621-252">KeyImport</span></span> |[<span data-ttu-id="d6621-253">Bir kasaya anahtar aktarma</span><span class="sxs-lookup"><span data-stu-id="d6621-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="d6621-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="d6621-254">KeyBackup</span></span> |<span data-ttu-id="d6621-255">[Bir anahtarı yedekleme](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6621-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="d6621-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="d6621-256">KeyDelete</span></span> |[<span data-ttu-id="d6621-257">Anahtar silme</span><span class="sxs-lookup"><span data-stu-id="d6621-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="d6621-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="d6621-258">KeyRestore</span></span> |[<span data-ttu-id="d6621-259">Bir anahtarı geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d6621-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="d6621-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="d6621-260">KeySign</span></span> |[<span data-ttu-id="d6621-261">Bir anahtar ile oturum açma</span><span class="sxs-lookup"><span data-stu-id="d6621-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="d6621-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="d6621-262">KeyVerify</span></span> |[<span data-ttu-id="d6621-263">Bir anahtar ile doğrulama</span><span class="sxs-lookup"><span data-stu-id="d6621-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="d6621-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="d6621-264">KeyWrap</span></span> |[<span data-ttu-id="d6621-265">Bir anahtarı sarmalama</span><span class="sxs-lookup"><span data-stu-id="d6621-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="d6621-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="d6621-266">KeyUnwrap</span></span> |[<span data-ttu-id="d6621-267">Bir anahtarı kaydırma</span><span class="sxs-lookup"><span data-stu-id="d6621-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="d6621-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="d6621-268">KeyEncrypt</span></span> |[<span data-ttu-id="d6621-269">Bir anahtar ile şifreleme</span><span class="sxs-lookup"><span data-stu-id="d6621-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="d6621-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="d6621-270">KeyDecrypt</span></span> |[<span data-ttu-id="d6621-271">Bir anahtar ile şifre çözme</span><span class="sxs-lookup"><span data-stu-id="d6621-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="d6621-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="d6621-272">KeyUpdate</span></span> |[<span data-ttu-id="d6621-273">Bir anahtarı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6621-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="d6621-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="d6621-274">KeyList</span></span> |[<span data-ttu-id="d6621-275">Bir kasadaki listesi hello anahtarları</span><span class="sxs-lookup"><span data-stu-id="d6621-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="d6621-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="d6621-276">KeyListVersions</span></span> |[<span data-ttu-id="d6621-277">Bir anahtar hello sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="d6621-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="d6621-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="d6621-278">SecretSet</span></span> |[<span data-ttu-id="d6621-279">Gizli anahtar oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6621-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="d6621-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="d6621-280">SecretGet</span></span> |[<span data-ttu-id="d6621-281">Gizli anahtar alma</span><span class="sxs-lookup"><span data-stu-id="d6621-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="d6621-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="d6621-282">SecretUpdate</span></span> |[<span data-ttu-id="d6621-283">Gizli anahtarı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6621-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="d6621-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="d6621-284">SecretDelete</span></span> |[<span data-ttu-id="d6621-285">Gizli anahtarı silme</span><span class="sxs-lookup"><span data-stu-id="d6621-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="d6621-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="d6621-286">SecretList</span></span> |[<span data-ttu-id="d6621-287">Bir kasadaki gizli anahtarları listeleme</span><span class="sxs-lookup"><span data-stu-id="d6621-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="d6621-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="d6621-288">SecretListVersions</span></span> |[<span data-ttu-id="d6621-289">Bir gizli anahtarın sürümlerini listeleme</span><span class="sxs-lookup"><span data-stu-id="d6621-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="d6621-290"><a id="loganalytics"></a>Log Analytics'i kullanma</span><span class="sxs-lookup"><span data-stu-id="d6621-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="d6621-291">Azure anahtar kasası AuditEvent günlüklerini günlük analizi tooreview içinde hello Azure anahtar kasası çözüm kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6621-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="d6621-292">Daha fazla bilgi için bu, nasıl tooset bakın dahil olmak üzere [günlük analizi Azure anahtar kasası çözümde](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="d6621-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="d6621-293">Çözümden burada ilk, günlükleri tooan Azure depolama hesabı yönlendirilir ve buradan günlük analizi tooread yapılandırılmış hello günlük analizi Önizleme sırasında sunulan hello eski anahtar kasası toomigrate gerekiyorsa bu makale yönergeleri de içerir.</span><span class="sxs-lookup"><span data-stu-id="d6621-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="d6621-294"><a id="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6621-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="d6621-295">Azure Anahtar Kasası'nın bir web uygulamasında kullanıldığı bir öğretici için bkz. [Azure Anahtar Kasası'nı bir Web Uygulamasından Kullanma](key-vault-use-from-web-application.md).</span><span class="sxs-lookup"><span data-stu-id="d6621-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="d6621-296">Programlama başvuruları için bkz: [Azure anahtar kasası Geliştirici Kılavuzu hello](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="d6621-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="d6621-297">Azure Anahtar Kasası'na yönelik Azure PowerShell 1.0 cmdlet'leri listesi için bkz. [Azure Anahtar Kasası Cmdlet'leri](/powershell/module/azurerm.keyvault/#key_vault).</span><span class="sxs-lookup"><span data-stu-id="d6621-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="d6621-298">Anahtar döndürme ve Azure anahtar kasası ile günlük denetim bir öğretici için bkz: [toosetup anahtar kasası son tooend ile nasıl anahtar döndürme ve Denetim](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="d6621-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>
