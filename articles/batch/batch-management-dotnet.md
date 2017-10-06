---
title: "aaaManage toplu işlem hesabı hello istemci kitaplığı için .NET - Azure kaynaklarıyla | Microsoft Docs"
description: "Oluşturma, silme ve Azure Batch hesabı kaynaklarını hello Batch yönetimi .NET kitaplığı ile değiştirin."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 16279b23-60ff-4b16-b308-5de000e4c028
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/24/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 638d8129f3841ffcfb2e10f5d531a319bcbb7701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-accounts-and-quotas-with-hello-batch-management-client-library-for-net"></a><span data-ttu-id="29086-103">.NET için Batch hesaplarını ve kotalarını hello Batch Yönetimi istemci kitaplığı ile yönetme</span><span class="sxs-lookup"><span data-stu-id="29086-103">Manage Batch accounts and quotas with hello Batch Management client library for .NET</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="29086-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="29086-104">Azure portal</span></span>](batch-account-create-portal.md)
> * [<span data-ttu-id="29086-105">Batch Yönetimi .NET</span><span class="sxs-lookup"><span data-stu-id="29086-105">Batch Management .NET</span></span>](batch-management-dotnet.md)
> 
> 

<span data-ttu-id="29086-106">Bakım yükü Azure Batch uygulamalarınızda hello kullanarak düşürün [Batch yönetimi .NET] [ api_mgmt_net] kitaplığı tooautomate Batch hesabı oluşturma, silme, anahtar yönetimi ve kota bulma.</span><span class="sxs-lookup"><span data-stu-id="29086-106">You can lower maintenance overhead in your Azure Batch applications by using hello [Batch Management .NET][api_mgmt_net] library tooautomate Batch account creation, deletion, key management, and quota discovery.</span></span>

* <span data-ttu-id="29086-107">**Oluşturma ve toplu işlem hesaplarını silme** hiçbir bölge içinde.</span><span class="sxs-lookup"><span data-stu-id="29086-107">**Create and delete Batch accounts** within any region.</span></span> <span data-ttu-id="29086-108">İçinde her ayrı bir toplu işlem hesabı faturalama amacıyla atanır, istemciler için bir hizmet, örneğin, bir bağımsız yazılım satıcısı (ISV) sağlarsanız, hesap oluşturma ve silme özellikleri tooyour müşteri portalı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-108">If, as an independent software vendor (ISV) for example, you provide a service for your clients in which each is assigned a separate Batch account for billing purposes, you can add account creation and deletion capabilities tooyour customer portal.</span></span>
* <span data-ttu-id="29086-109">**Almak ve hesabı anahtarlarını yeniden** program aracılığıyla toplu hesaplarınızdan herhangi birinin için.</span><span class="sxs-lookup"><span data-stu-id="29086-109">**Retrieve and regenerate account keys** programmatically for any of your Batch accounts.</span></span> <span data-ttu-id="29086-110">Düzenli geçiş veya hesabı anahtarları süre sonu zorlayan güvenlik ilkeleriyle uyumlu yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="29086-110">This can help you comply with security policies that enforce periodic rollover or expiry of account keys.</span></span> <span data-ttu-id="29086-111">Çeşitli Azure bölgelerinde birçok Batch hesapları varsa, bu geçiş işlemi Otomasyon çözümünüzün verimliliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="29086-111">When you have several Batch accounts in various Azure regions, automation of this rollover process increases your solution's efficiency.</span></span>
* <span data-ttu-id="29086-112">**Hesap kotalarını denetleyin** ve hangi sınırları hangi Batch hesaplarınızın belirleme dışında hello deneme yanılma konusunda güvenilir bilgiler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="29086-112">**Check account quotas** and take hello trial-and-error guesswork out of determining which Batch accounts have what limits.</span></span> <span data-ttu-id="29086-113">İşler başlamadan önce hesap kotalarını denetleyerek, havuzları oluşturma veya işlem düğümleri eklemek, where proaktif olarak ayarlayabilir veya bu işlem kaynakları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="29086-113">By checking your account quotas before starting jobs, creating pools, or adding compute nodes, you can proactively adjust where or when these compute resources are created.</span></span> <span data-ttu-id="29086-114">Bu hesapların ek kaynakları ayırma önce kota artırır hangi hesapların gerektirdiği belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-114">You can determine which accounts require quota increases before allocating additional resources in those accounts.</span></span>
* <span data-ttu-id="29086-115">**Diğer Azure hizmetleriyle özelliklerini birleştirme** Batch yönetimi .NET kullanarak tam özellikli yönetim deneyimi-- [Azure Active Directory][aad_about]ve hello [Azure Resource Manager] [ resman_overview] hello bir araya aynı uygulama.</span><span class="sxs-lookup"><span data-stu-id="29086-115">**Combine features of other Azure services** for a full-featured management experience--by using Batch Management .NET, [Azure Active Directory][aad_about], and hello [Azure Resource Manager][resman_overview] together in hello same application.</span></span> <span data-ttu-id="29086-116">Bu özellikler ve bunların API'lerini kullanarak, uyumlu kimlik doğrulama deneyimi sağlamak, özelliği toocreate hello ve kaynak grupları ve uçtan uca yönetim çözümünü için yukarıda açıklanan hello özellikleri silin.</span><span class="sxs-lookup"><span data-stu-id="29086-116">By using these features and their APIs, you can provide a frictionless authentication experience, hello ability toocreate and delete resource groups, and hello capabilities that are described above for an end-to-end management solution.</span></span>

> [!NOTE]
> <span data-ttu-id="29086-117">Bu makalede toplu hesaplar, anahtarları ve kotalar hello programlı yönetimini odaklanmakla birlikte, birçok bu etkinliklerin hello kullanarak gerçekleştirebilirsiniz [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="29086-117">While this article focuses on hello programmatic management of your Batch accounts, keys, and quotas, you can perform many of these activities by using hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="29086-118">Daha fazla bilgi için bkz: [hello Azure portal kullanarak bir Azure Batch hesabı oluşturma](batch-account-create-portal.md) ve [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="29086-118">For more information, see [Create an Azure Batch account using hello Azure portal](batch-account-create-portal.md) and [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span>
> 
> 

## <a name="create-and-delete-batch-accounts"></a><span data-ttu-id="29086-119">Oluşturma ve toplu işlem hesaplarını silme</span><span class="sxs-lookup"><span data-stu-id="29086-119">Create and delete Batch accounts</span></span>
<span data-ttu-id="29086-120">Belirtildiği gibi hello birincil özelliklerinden biri hello Batch yönetim API'si toocreate olduğundan ve bir Azure bölgesi toplu hesaplarında silin.</span><span class="sxs-lookup"><span data-stu-id="29086-120">As mentioned, one of hello primary features of hello Batch Management API is toocreate and delete Batch accounts in an Azure region.</span></span> <span data-ttu-id="29086-121">Bu nedenle, toodo kullanmak [BatchManagementClient.Account.CreateAsync] [ net_create] ve [DeleteAsync][net_delete], ya da zaman uyumlu dekiler.</span><span class="sxs-lookup"><span data-stu-id="29086-121">toodo so, use [BatchManagementClient.Account.CreateAsync][net_create] and [DeleteAsync][net_delete], or their synchronous counterparts.</span></span>

<span data-ttu-id="29086-122">Merhaba aşağıdaki kod parçacığını bir hesabı oluşturur, yeni hesabı Batch hizmeti hello oluşturulan hello alır ve ardından siler.</span><span class="sxs-lookup"><span data-stu-id="29086-122">hello following code snippet creates an account, obtains hello newly created account from hello Batch service, and then deletes it.</span></span> <span data-ttu-id="29086-123">Bu parçacığında bulunan ve diğerlerinin bu makalede, hello `batchManagementClient` tamamen başlatılmış bir örneğinin [BatchManagementClient][net_mgmt_client].</span><span class="sxs-lookup"><span data-stu-id="29086-123">In this snippet and hello others in this article, `batchManagementClient` is a fully initialized instance of [BatchManagementClient][net_mgmt_client].</span></span>

```csharp
// Create a new Batch account
await batchManagementClient.Account.CreateAsync("MyResourceGroup",
    "mynewaccount",
    new BatchAccountCreateParameters() { Location = "West US" });

// Get hello new account from hello Batch service
AccountResource account = await batchManagementClient.Account.GetAsync(
    "MyResourceGroup",
    "mynewaccount");

// Delete hello account
await batchManagementClient.Account.DeleteAsync("MyResourceGroup", account.Name);
```

> [!NOTE]
> <span data-ttu-id="29086-124">Merhaba Batch yönetimi .NET kitaplığı ve onun BatchManagementClient sınıfını kullanan uygulamaları gerektiren **Hizmet Yöneticisi** veya **Abonelikteki** erişim hello sahibi toohello abonelik Toplu işlem hesabı toobe yönetilen.</span><span class="sxs-lookup"><span data-stu-id="29086-124">Applications that use hello Batch Management .NET library and its BatchManagementClient class require **service administrator** or **coadministrator** access toohello subscription that owns hello Batch account toobe managed.</span></span> <span data-ttu-id="29086-125">Merhaba daha fazla bilgi için bkz: [Azure Active Directory](#azure-active-directory) bölümü ve hello [AccountManagement] [ acct_mgmt_sample] kod örneği.</span><span class="sxs-lookup"><span data-stu-id="29086-125">For more information, see hello [Azure Active Directory](#azure-active-directory) section and hello [AccountManagement][acct_mgmt_sample] code sample.</span></span>
> 
> 

## <a name="retrieve-and-regenerate-account-keys"></a><span data-ttu-id="29086-126">Almak ve hesabı anahtarlarını yeniden oluştur</span><span class="sxs-lookup"><span data-stu-id="29086-126">Retrieve and regenerate account keys</span></span>
<span data-ttu-id="29086-127">Kullanarak birincil ve ikincil hesabı anahtarları, abonelik içindeki herhangi bir toplu işlem hesabı elde [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="29086-127">Obtain primary and secondary account keys from any Batch account within your subscription by using [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="29086-128">Bu anahtarlar kullanarak yeniden [RegenerateKeyAsync][net_regenerate_keys].</span><span class="sxs-lookup"><span data-stu-id="29086-128">You can regenerate those keys by using [RegenerateKeyAsync][net_regenerate_keys].</span></span>

```csharp
// Get and print hello primary and secondary keys
BatchAccountListKeyResult accountKeys =
    await batchManagementClient.Account.ListKeysAsync(
        "MyResourceGroup",
        "mybatchaccount");
Console.WriteLine("Primary key:   {0}", accountKeys.Primary);
Console.WriteLine("Secondary key: {0}", accountKeys.Secondary);

// Regenerate hello primary key
BatchAccountRegenerateKeyResponse newKeys =
    await batchManagementClient.Account.RegenerateKeyAsync(
        "MyResourceGroup",
        "mybatchaccount",
        new BatchAccountRegenerateKeyParameters() {
            KeyName = AccountKeyType.Primary
            });
```

> [!TIP]
> <span data-ttu-id="29086-129">Yönetim uygulamalarınız için kolaylaştırılmış bağlantı iş akışı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-129">You can create a streamlined connection workflow for your management applications.</span></span> <span data-ttu-id="29086-130">İlk olarak, toomanage ile istediğiniz hesap anahtarı hello toplu işlem hesabı için elde [ListKeysAsync][net_list_keys].</span><span class="sxs-lookup"><span data-stu-id="29086-130">First, obtain an account key for hello Batch account you wish toomanage with [ListKeysAsync][net_list_keys].</span></span> <span data-ttu-id="29086-131">Ardından, bu anahtarı hello Batch .NET kitaplığın başlatırken kullanmak [BatchSharedKeyCredentials] [ net_sharedkeycred] başlatılırken kullanılan sınıf [BatchClient] [net_batch_client].</span><span class="sxs-lookup"><span data-stu-id="29086-131">Then, use this key when initializing hello Batch .NET library's [BatchSharedKeyCredentials][net_sharedkeycred] class, which is used when initializing [BatchClient][net_batch_client].</span></span>
> 
> 

## <a name="check-azure-subscription-and-batch-account-quotas"></a><span data-ttu-id="29086-132">Azure aboneliği ve toplu işlem hesabı kotası denetleyin</span><span class="sxs-lookup"><span data-stu-id="29086-132">Check Azure subscription and Batch account quotas</span></span>
<span data-ttu-id="29086-133">Azure abonelikleri ve tüm toplu gibi hello tek tek Azure Hizmetleri belirli varlıkları hello sayısı sınırı varsayılan kotalar sahiptir.</span><span class="sxs-lookup"><span data-stu-id="29086-133">Azure subscriptions and hello individual Azure services like Batch all have default quotas that limit hello number of certain entities within them.</span></span> <span data-ttu-id="29086-134">Azure aboneliklerinin Hello varsayılan kotaları için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="29086-134">For hello default quotas for Azure subscriptions, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="29086-135">Varsayılan kotaları Hello hello Batch hizmeti için bkz: [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md).</span><span class="sxs-lookup"><span data-stu-id="29086-135">For hello default quotas of hello Batch service, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md).</span></span> <span data-ttu-id="29086-136">Merhaba Batch yönetimi .NET kitaplığını kullanarak uygulamalarınızı bu kotalar kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-136">By using hello Batch Management .NET library, you can check these quotas in your applications.</span></span> <span data-ttu-id="29086-137">Hesapları ekleyin veya işlem kaynaklarını havuzları gibi ve işlem düğümleri önce bu toomake ayırma kararları sağlar.</span><span class="sxs-lookup"><span data-stu-id="29086-137">This enables you toomake allocation decisions before you add accounts or compute resources like pools and compute nodes.</span></span>

### <a name="check-an-azure-subscription-for-batch-account-quotas"></a><span data-ttu-id="29086-138">Azure aboneliği toplu işlem hesabı kotası için denetleyin</span><span class="sxs-lookup"><span data-stu-id="29086-138">Check an Azure subscription for Batch account quotas</span></span>
<span data-ttu-id="29086-139">Bir bölgede bir toplu işlem hesabı oluşturmadan önce Azure aboneliği toosee mümkün tooadd bu bölgede bulunan bir hesap olup denetleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-139">Before creating a Batch account in a region, you can check your Azure subscription toosee whether you are able tooadd an account in that region.</span></span>

<span data-ttu-id="29086-140">Merhaba aşağıdaki kod parçacığında, ilk kullanırız [BatchManagementClient.Account.ListAsync] [ net_mgmt_listaccounts] tooget bir abonelik içinde olan tüm Batch hesaplarının bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="29086-140">In hello code snippet below, we first use [BatchManagementClient.Account.ListAsync][net_mgmt_listaccounts] tooget a collection of all Batch accounts that are within a subscription.</span></span> <span data-ttu-id="29086-141">Bu koleksiyon elde sonra hello hedef bölgede kaç hesaplardır belirler.</span><span class="sxs-lookup"><span data-stu-id="29086-141">Once we've obtained this collection, we determine how many accounts are in hello target region.</span></span> <span data-ttu-id="29086-142">Kullanırız sonra [BatchManagementClient.Subscriptions] [ net_mgmt_subscriptions] tooobtain toplu işlem hesabı kotası hello ve bu bölgede kaç hesapları (varsa) oluşturulabilir belirleyin.</span><span class="sxs-lookup"><span data-stu-id="29086-142">Then we use [BatchManagementClient.Subscriptions][net_mgmt_subscriptions] tooobtain hello Batch account quota and determine how many accounts (if any) can be created in that region.</span></span>

```csharp
// Get a collection of all Batch accounts within hello subscription
BatchAccountListResponse listResponse =
        await batchManagementClient.Account.ListAsync(new AccountListParameters());
IList<AccountResource> accounts = listResponse.Accounts;
Console.WriteLine("Total number of Batch accounts under subscription id {0}:  {1}",
    creds.SubscriptionId,
    accounts.Count);

// Get a count of all accounts within hello target region
string region = "westus";
int accountsInRegion = accounts.Count(o => o.Location == region);

// Get hello account quota for hello specified region
SubscriptionQuotasGetResponse quotaResponse = await batchManagementClient.Subscriptions.GetSubscriptionQuotasAsync(region);
Console.WriteLine("Account quota for {0} region: {1}", region, quotaResponse.AccountQuota);

// Determine how many accounts can be created in hello target region
Console.WriteLine("Accounts in {0}: {1}", region, accountsInRegion);
Console.WriteLine("You can create {0} accounts in hello {1} region.", quotaResponse.AccountQuota - accountsInRegion, region);
```

<span data-ttu-id="29086-143">Yukarıdaki hello parçacığında bulunan `creds` örneği [TokenCloudCredentials][azure_tokencreds].</span><span class="sxs-lookup"><span data-stu-id="29086-143">In hello snippet above, `creds` is an instance of [TokenCloudCredentials][azure_tokencreds].</span></span> <span data-ttu-id="29086-144">Bu nesne oluşturma örneği toosee hello bkz [AccountManagement] [ acct_mgmt_sample] kodu örneği github'daki.</span><span class="sxs-lookup"><span data-stu-id="29086-144">toosee an example of creating this object, see hello [AccountManagement][acct_mgmt_sample] code sample on GitHub.</span></span>

### <a name="check-a-batch-account-for-compute-resource-quotas"></a><span data-ttu-id="29086-145">Bir Batch hesabında işlem kaynak kotaları denetleyin</span><span class="sxs-lookup"><span data-stu-id="29086-145">Check a Batch account for compute resource quotas</span></span>
<span data-ttu-id="29086-146">Batch çözümündeki işlem kaynakları artırmadan önce tooallocate hello hesabın kotaları aşan olmaz istediğiniz tooensure hello kaynakların kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-146">Before increasing compute resources in your Batch solution, you can check tooensure hello resources you want tooallocate won't exceed hello account's quotas.</span></span> <span data-ttu-id="29086-147">Merhaba aşağıdaki kod parçacığında, biz hello kota bilgileri hello adlı toplu işlem hesabı için yazdırma `mybatchaccount`.</span><span class="sxs-lookup"><span data-stu-id="29086-147">In hello code snippet below, we print hello quota information for hello Batch account named `mybatchaccount`.</span></span> <span data-ttu-id="29086-148">Kendi uygulamanızda Hello hesap oluşturulan hello ek kaynaklar toobe işleyip işleyemediğine gibi bilgileri toodetermine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-148">In your own application, you could use such information toodetermine whether hello account can handle hello additional resources toobe created.</span></span>

```csharp
// First obtain hello Batch account
BatchAccountGetResponse getResponse =
    await batchManagementClient.Account.GetAsync("MyResourceGroup", "mybatchaccount");
AccountResource account = getResponse.Resource;

// Now print hello compute resource quotas for hello account
Console.WriteLine("Core quota: {0}", account.Properties.CoreQuota);
Console.WriteLine("Pool quota: {0}", account.Properties.PoolQuota);
Console.WriteLine("Active job and job schedule quota: {0}", account.Properties.ActiveJobAndJobScheduleQuota);
```

> [!IMPORTANT]
> <span data-ttu-id="29086-149">Azure abonelikleri ve Hizmetleri için varsayılan kotaları olsa da, bu sınırları çoğunu hello istekte vererek yükseltilebilir [Azure portal][azure_portal].</span><span class="sxs-lookup"><span data-stu-id="29086-149">While there are default quotas for Azure subscriptions and services, many of these limits can be raised by issuing a request in hello [Azure portal][azure_portal].</span></span> <span data-ttu-id="29086-150">Örneğin, [hello Azure Batch hizmeti için kotalar ve sınırlar](batch-quota-limit.md) toplu işlem hesabı kotası artırma hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="29086-150">For example, see [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for instructions on increasing your Batch account quotas.</span></span>
> 
> 

## <a name="use-azure-ad-with-batch-management-net"></a><span data-ttu-id="29086-151">Azure AD Batch yönetimi .NET ile kullanma</span><span class="sxs-lookup"><span data-stu-id="29086-151">Use Azure AD with Batch Management .NET</span></span>

<span data-ttu-id="29086-152">Merhaba Batch yönetimi .NET kitaplığı bir Azure kaynak sağlayıcısı istemci ve ile birlikte kullanılan [Azure Resource Manager] [ resman_overview] toomanage kaynakları program aracılığıyla hesap.</span><span class="sxs-lookup"><span data-stu-id="29086-152">hello Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] toomanage account resources programmatically.</span></span> <span data-ttu-id="29086-153">Azure AD olduğu ve hello Batch yönetimi .NET kitaplığı dahil olmak üzere tüm Azure kaynak sağlayıcısı istemci aracılığıyla yapılan gerekli tooauthenticate istekleri [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="29086-153">Azure AD is required tooauthenticate requests made through any Azure resource provider client, including hello Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span> <span data-ttu-id="29086-154">Azure AD hello Batch yönetimi .NET kitaplığı ile kullanma hakkında daha fazla bilgi için bkz: [kullanım Azure Active Directory tooauthenticate Batch çözümleri](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="29086-154">For information about using Azure AD with hello Batch Management .NET library, see [Use Azure Active Directory tooauthenticate Batch solutions](batch-aad-auth.md).</span></span> 

## <a name="sample-project-on-github"></a><span data-ttu-id="29086-155">Github'da örnek proje</span><span class="sxs-lookup"><span data-stu-id="29086-155">Sample project on GitHub</span></span>

<span data-ttu-id="29086-156">toosee Batch yönetimi .NET eylem denetleyin hello [AccountManagment] [ acct_mgmt_sample] örnek proje github'da.</span><span class="sxs-lookup"><span data-stu-id="29086-156">toosee Batch Management .NET in action, check out hello [AccountManagment][acct_mgmt_sample] sample project on GitHub.</span></span> <span data-ttu-id="29086-157">Merhaba AccountManagment örnek uygulama işlemleri aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="29086-157">hello AccountManagment sample application demonstrates hello following operations:</span></span>

1. <span data-ttu-id="29086-158">Kullanarak Azure AD'den bir güvenlik belirtecini almak [ADAL][aad_adal].</span><span class="sxs-lookup"><span data-stu-id="29086-158">Acquire a security token from Azure AD by using [ADAL][aad_adal].</span></span> <span data-ttu-id="29086-159">Merhaba kullanıcı zaten oturum açmamış varsa, bunlar Azure kullanıcılardan kimlik bilgileri istenir.</span><span class="sxs-lookup"><span data-stu-id="29086-159">If hello user is not already signed in, they are prompted for their Azure credentials.</span></span>
2. <span data-ttu-id="29086-160">Azure AD'den alınan hello güvenlik belirteciyle oluşturma bir [SubscriptionClient] [ resman_subclient] tooquery Azure hello hesabıyla ilişkilendirilmiş abonelik listesi.</span><span class="sxs-lookup"><span data-stu-id="29086-160">With hello security token obtained from Azure AD, create a [SubscriptionClient][resman_subclient] tooquery Azure for a list of subscriptions associated with hello account.</span></span> <span data-ttu-id="29086-161">birden fazla aboneliğiniz varsa hello kullanıcı hello listesinden bir abonelik seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="29086-161">hello user can select a subscription from hello list if it contains more than one subscription.</span></span>
3. <span data-ttu-id="29086-162">Seçili hello abonelikle ilişkili kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="29086-162">Get credentials associated with hello selected subscription.</span></span>
4. <span data-ttu-id="29086-163">Oluşturma bir [ResourceManagementClient] [ resman_client] hello kimlik bilgilerini kullanarak nesne.</span><span class="sxs-lookup"><span data-stu-id="29086-163">Create a [ResourceManagementClient][resman_client] object by using hello credentials.</span></span>
5. <span data-ttu-id="29086-164">Kullanım bir [ResourceManagementClient] [ resman_client] toocreate bir kaynak grubu nesnesi.</span><span class="sxs-lookup"><span data-stu-id="29086-164">Use a [ResourceManagementClient][resman_client] object toocreate a resource group.</span></span>
6. <span data-ttu-id="29086-165">Kullanım bir [BatchManagementClient] [ net_mgmt_client] tooperform birkaç toplu hesap işlemleri nesnesi:</span><span class="sxs-lookup"><span data-stu-id="29086-165">Use a [BatchManagementClient][net_mgmt_client] object tooperform several Batch account operations:</span></span>
   * <span data-ttu-id="29086-166">Toplu işlem hesabı hello yeni kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29086-166">Create a Batch account in hello new resource group.</span></span>
   * <span data-ttu-id="29086-167">Hesabı Batch hizmeti hello yeni oluşturulan hello alın.</span><span class="sxs-lookup"><span data-stu-id="29086-167">Get hello newly created account from hello Batch service.</span></span>
   * <span data-ttu-id="29086-168">Merhaba hesabı anahtarları hello yeni hesap için yazdırın.</span><span class="sxs-lookup"><span data-stu-id="29086-168">Print hello account keys for hello new account.</span></span>
   * <span data-ttu-id="29086-169">Merhaba hesabı için yeni bir birincil anahtar yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="29086-169">Regenerate a new primary key for hello account.</span></span>
   * <span data-ttu-id="29086-170">Merhaba kota bilgileri hello hesabı için yazdırın.</span><span class="sxs-lookup"><span data-stu-id="29086-170">Print hello quota information for hello account.</span></span>
   * <span data-ttu-id="29086-171">Merhaba hello aboneliği için kota bilgilerini yazdırın.</span><span class="sxs-lookup"><span data-stu-id="29086-171">Print hello quota information for hello subscription.</span></span>
   * <span data-ttu-id="29086-172">Merhaba abonelik içindeki tüm hesapları yazdırın.</span><span class="sxs-lookup"><span data-stu-id="29086-172">Print all accounts within hello subscription.</span></span>
   * <span data-ttu-id="29086-173">Yeni oluşturulan hesabı silin.</span><span class="sxs-lookup"><span data-stu-id="29086-173">Delete newly created account.</span></span>
7. <span data-ttu-id="29086-174">Merhaba kaynak grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="29086-174">Delete hello resource group.</span></span>

<span data-ttu-id="29086-175">Yeni oluşturulan hello toplu işlem hesabı ve kaynak grubu silmeden önce bunları hello görüntüleyebileceğiniz [Azure portal][azure_portal]:</span><span class="sxs-lookup"><span data-stu-id="29086-175">Before deleting hello newly created Batch account and resource group, you can view them in hello [Azure portal][azure_portal]:</span></span>

<span data-ttu-id="29086-176">toorun hello örnek uygulama başarıyla öncelikle bunu Azure AD kiracınızda hello Azure portal ve grant izinleri toohello Azure Kaynak Yöneticisi API'si ile kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="29086-176">toorun hello sample application successfully, you must first register it with your Azure AD tenant in hello Azure portal and grant permissions toohello Azure Resource Manager API.</span></span> <span data-ttu-id="29086-177">Sağlanan hello adımları [Active Directory ile kimlik doğrulaması toplu yönetim çözümleri](batch-aad-auth-management.md).</span><span class="sxs-lookup"><span data-stu-id="29086-177">Follow hello steps provided in [Authenticate Batch Management solutions with Active Directory](batch-aad-auth-management.md).</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "Azure Active Directory nedir?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Azure AD için kimlik doğrulama senaryoları"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Uygulamaları Azure Active Directory ile tümleştirme"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_mgmt_net]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[azure_portal]: http://portal.azure.com
[azure_storage]: https://azure.microsoft.com/services/storage/
[azure_tokencreds]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.tokencloudcredentials.aspx
[batch_explorer_project]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_list_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.listkeysasync.aspx
[net_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.createasync.aspx
[net_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.deleteasync.aspx
[net_regenerate_keys]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.accountoperationsextensions.regeneratekeyasync.aspx
[net_sharedkeycred]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.auth.batchsharedkeycredentials.aspx
[net_mgmt_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.aspx
[net_mgmt_subscriptions]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.batchmanagementclient.subscriptions.aspx
[net_mgmt_listaccounts]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.batch.iaccountoperations.listasync.aspx
[resman_api]: https://msdn.microsoft.com/library/azure/mt418626.aspx
[resman_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.resourcemanagementclient.aspx
[resman_subclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.subscriptions.subscriptionclient.aspx
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

[1]: ./media/batch-management-dotnet/portal-01.png
[2]: ./media/batch-management-dotnet/portal-02.png
[3]: ./media/batch-management-dotnet/portal-03.png
