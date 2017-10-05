---
title: "Batch için Azure CLI kullanmaya başlama | Microsoft Docs"
description: "Azure Batch hizmet kaynaklarını yönetmek üzere Azure CLI’daki Batch komutlarına hızlı bir giriş yapın"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9bee0344ba70c50cda36a87ea617906283040ff9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="720fe-103">Batch kaynaklarını Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="720fe-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="720fe-104">Azure CLI 2.0, Azure kaynaklarını yönetmek için Azure tarafından sunulan yeni komut satırı deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="720fe-104">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="720fe-105">MacOS, Linux ve Windows’da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="720fe-106">Azure CLI 2.0, Azure kaynaklarını komut satırından yönetmek üzere iyileştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="720fe-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line.</span></span> <span data-ttu-id="720fe-107">Azure CLI kullanarak Azure Batch hesaplarınızın yanı sıra havuzlar, işler ve görevler gibi kaynakları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-107">You can use the Azure CLI to manage your Azure Batch accounts and to manage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="720fe-108">Azure Batch CLI ile Batch API'leri, Azure portalı ve Batch PowerShell cmdlet’leri ile gerçekleştirdiğiniz görevlerin çoğu için betik oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-108">With the Azure CLI, you can script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="720fe-109">Bu makalede Batch ile [Azure CLI sürüm 2.0](https://docs.microsoft.com/cli/azure/overview) kullanımına genel bakışa yer verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="720fe-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="720fe-110">Azure ile CLI kullanımı hakkında bilgi için bkz. [Azure CLI 2.0'ı kullanmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="720fe-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using the CLI with Azure.</span></span>

<span data-ttu-id="720fe-111">Microsoft, en son Azure CLI sürümü olan 2.0'ı kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="720fe-111">Microsoft recommends using the latest version of the Azure CLI, version 2.0.</span></span> <span data-ttu-id="720fe-112">Sürüm 2.0 hakkında daha fazla bilgi için bkz. [Azure Komut Satırı 2.0 genel kullanıma sunuldu](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="720fe-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-the-azure-cli"></a><span data-ttu-id="720fe-113">Azure CLI'yı kurma</span><span class="sxs-lookup"><span data-stu-id="720fe-113">Set up the Azure CLI</span></span>

<span data-ttu-id="720fe-114">Azure CLI'yı yüklemek için [Azure CLI'yı yükleme](https://docs.microsoft.com/cli/azure/install-azure-cli.md) sayfasındaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="720fe-114">To install the Azure CLI, follow the steps outlined in [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="720fe-115">Hizmet güncelleştirmeleri ve geliştirmelerinden yararlanmak için Azure CLI yüklemenizi sık sık güncelleştirmeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-115">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="720fe-116">Komut yardımı</span><span class="sxs-lookup"><span data-stu-id="720fe-116">Command help</span></span>

<span data-ttu-id="720fe-117">Komuttan sonra `-h` ekleyerek Azure CLI'daki her komut için yardım metni görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-117">You can display help text for every command in the Azure CLI by appending `-h` to the command.</span></span> <span data-ttu-id="720fe-118">Diğer seçenekleri atın.</span><span class="sxs-lookup"><span data-stu-id="720fe-118">Omit any other options.</span></span> <span data-ttu-id="720fe-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="720fe-119">For example:</span></span>

* <span data-ttu-id="720fe-120">`az` komutuyla ilgili yardım almak için şunu girin: `az -h`</span><span class="sxs-lookup"><span data-stu-id="720fe-120">To get help for the `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="720fe-121">CLI’daki tüm Batch komutlarının listesini almak için şunu kullanın: `az batch -h`</span><span class="sxs-lookup"><span data-stu-id="720fe-121">To get a list of all Batch commands in the CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="720fe-122">Batch hesabı oluşturmayla ilgili yardım almak için şunu girin: `az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="720fe-122">To get help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="720fe-123">Emin olmadığınızda herhangi bir Azure CLI komutuyla ilgili yardım almak için `-h` komut satırı seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="720fe-123">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="720fe-124">Önceki Azure CLI sürümlerinde CLI komutu yazmaya başlamak için `azure` kullanılıyordu.</span><span class="sxs-lookup"><span data-stu-id="720fe-124">Earlier versions of the Azure CLI used `azure` to preface a CLI command.</span></span> <span data-ttu-id="720fe-125">Sürüm 2.0'da tüm komutlar `az` ile kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="720fe-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="720fe-126">Betiklerinizi sürüm 2.0 ile yeni söz dizimini kullanacak şekilde güncelleştirmeyi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="720fe-126">Be sure to update your scripts to use the new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="720fe-127">Ayrıca [Batch için Azure CLI komutları](https://docs.microsoft.com/cli/azure/batch) hakkında ayrıntılı bilgi için Azure CLI referans belgelerini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="720fe-127">Additionally, refer to the Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="720fe-128">Oturum açma ve kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="720fe-128">Log in and authenticate</span></span>

<span data-ttu-id="720fe-129">Batch ile Azure CLI kullanmak için oturum açmanız ve kimlik doğrulamasından geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="720fe-129">To use the Azure CLI with Batch, you need to log in and authenticate.</span></span> <span data-ttu-id="720fe-130">İzlemeniz gereken iki basit adım vardır:</span><span class="sxs-lookup"><span data-stu-id="720fe-130">There are two simple steps to follow:</span></span>

1. <span data-ttu-id="720fe-131">**Azure'da oturum açın.**</span><span class="sxs-lookup"><span data-stu-id="720fe-131">**Log into Azure.**</span></span> <span data-ttu-id="720fe-132">Azure'da oturum açarak [Batch Management hizmeti](batch-management-dotnet.md) komutları dahil olmak üzere Azure Resource Manager komutlarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-132">Logging into Azure gives you access to Azure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="720fe-133">**Batch hesabınızda oturum açın.**</span><span class="sxs-lookup"><span data-stu-id="720fe-133">**Log into your Batch account.**</span></span> <span data-ttu-id="720fe-134">Batch hesabınızda oturum açarak Batch hizmeti komutlarına erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-134">Logging into your Batch account gives you access to Batch service commands.</span></span>   

### <a name="log-in-to-azure"></a><span data-ttu-id="720fe-135">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="720fe-135">Log in to Azure</span></span>

<span data-ttu-id="720fe-136">Azure'da oturum açmanın birkaç farklı yolu vardır ve hepsi [Azure CLI 2.0 ile oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli) sayfasında ayrıntılı olarak açıklanmıştır:</span><span class="sxs-lookup"><span data-stu-id="720fe-136">There are a few different ways to log into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="720fe-137">[Etkileşimli olarak oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="720fe-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="720fe-138">Azure CLI komutlarını komut satırından çalıştırmak için etkileşimli olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="720fe-138">Log in interactively when you are running Azure CLI commands yourself from the command line.</span></span>
2. <span data-ttu-id="720fe-139">[Hizmet sorumlusu ile oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="720fe-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="720fe-140">Azure CLI komutlarını bir betikten veya uygulamadan çalıştırdığınızda hizmet sorumlusuyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="720fe-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="720fe-141">Bu makalede Azure'da etkileşimli oturum açmayı göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="720fe-141">For the purposes of this article, we show how to log into Azure interactively.</span></span> <span data-ttu-id="720fe-142">Komut satırına [az login](https://docs.microsoft.com/cli/azure/#login) yazın:</span><span class="sxs-lookup"><span data-stu-id="720fe-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on the command line:</span></span>

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

<span data-ttu-id="720fe-143">`az login` komutu, burada gösterildiği gibi kimlik doğrulaması için kullanabileceğiniz bir belirteç döndürür.</span><span class="sxs-lookup"><span data-stu-id="720fe-143">The `az login` command returns a token that you can use to authenticate, as shown here.</span></span> <span data-ttu-id="720fe-144">Bir web sayfası açmak ve belirteci Azure'a göndermek için yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="720fe-144">Follow the instructions provided to open a web page and submit the token to Azure:</span></span>

![Azure'da oturum açma](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="720fe-146">[Örnek kabuk betikleri](#sample-shell-scripts) bölümünde listelenen örnekler de Azure'da etkileşimli olarak oturum açarak Azure CLI oturumunuzu nasıl başlatacağınızı göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="720fe-146">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section also show how to start your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="720fe-147">Oturum açtıktan sonra Batch hesapları, anahtarları, uygulama paketleri ve kotaları dahil olmak üzere Batch Management kaynaklarıyla çalışmak için komutları çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-147">Once you have logged in, you can call commands to work with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-to-your-batch-account"></a><span data-ttu-id="720fe-148">Batch hesabınızda oturum açma</span><span class="sxs-lookup"><span data-stu-id="720fe-148">Log in to your Batch account</span></span>

<span data-ttu-id="720fe-149">Havuzlar, işler ve görevler gibi Batch kaynaklarını yönetmek üzere Azure CLI kullanmak için Batch hesabınızda oturum açıp kimlik doğrulamasından geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="720fe-149">To use the Azure CLI to manage Batch resources, such as pools, jobs, and tasks, you need to log into your Batch account and authenticate.</span></span> <span data-ttu-id="720fe-150">Batch hizmetinde oturum açmak için [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="720fe-150">To log in to the Batch service, use the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="720fe-151">Batch hesabınızla kimlik doğrulamasından geçmek için kullanabileceğiniz iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="720fe-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="720fe-152">**Azure Active Directory (Azure AD) kimlik doğrulamasını kullanmak.**</span><span class="sxs-lookup"><span data-stu-id="720fe-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="720fe-153">Azure AD kimlik doğrulamasını kullanmak, Batch ile Azure CLI kullandığınızda varsayılan ve çoğu senaryo için önerilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="720fe-153">Authenticating with Azure AD is the default when you use the Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="720fe-154">Önceki bölümde anlatıldığı şekilde Azure'da etkileşimli olarak oturum açtığınızda kimlik bilgileriniz önbelleğe alınır ve Azure CLI bu kimlik bilgilerini kullanarak Batch hesabınızda oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-154">When you log in to Azure interactively, as described in the previous section, your credentials are cached, so the Azure CLI can log you in to your Batch account using those same credentials.</span></span> <span data-ttu-id="720fe-155">Azure'da hizmet sorumlusu kullanarak oturum açarsanız o kimlik bilgileri de Batch hesabınıza oturum açmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="720fe-155">If you log in to Azure using a service principal, those credentials are also used to log in to your Batch account.</span></span>

    <span data-ttu-id="720fe-156">Azure AD'nin avantajlarından biri rol tabanlı erişim denetimine (RBAC) sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="720fe-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="720fe-157">RBAC sayesinde kullanıcı erişimi hesap anahtarına sahip olma durumuna göre değil kendisine atanan role göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="720fe-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess the account keys.</span></span> <span data-ttu-id="720fe-158">Hesap anahtarlarını yönetmek yerine RBAC rollerini yönetebilir ve erişimle kimlik doğrulamasını Azure AD'ye bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="720fe-159">Azure Batch hesabınızı havuz ayırma modu "Kullanıcı Aboneliği" olarak ayarlanmış halde oluşturduysanız Azure AD ile kimlik doğrulaması yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="720fe-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set to 'User Subscription'.</span></span> 

    <span data-ttu-id="720fe-160">Azure AD ile Batch hesabınızda oturum açmak için [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) komutunu çağırın:</span><span class="sxs-lookup"><span data-stu-id="720fe-160">To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="720fe-161">**Paylaşılan Anahtar kimlik doğrulamasını kullanarak.**</span><span class="sxs-lookup"><span data-stu-id="720fe-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="720fe-162">[Paylaşılan Anahtar kimlik doğrulaması](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) hesap erişim anahtarlarınızı kullanarak Batch hizmeti için Azure CLI komutlarının kimlik doğrulamasından geçmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="720fe-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys to authenticate Azure CLI commands for the Batch service.</span></span>

    <span data-ttu-id="720fe-163">Batch komutlarını otomatikleştirme amacıyla Azure CLI betikleri oluşturuyorsanız Paylaşılan Anahtar kimlik doğrulaması veya Azure AD hizmet sorumlusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-163">If you are creating Azure CLI scripts to automate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="720fe-164">Bazı senaryolarda Paylaşılan Anahtar ile kimlik doğrulaması, hizmet sorumlusu oluşturmaktan daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="720fe-165">Paylaşılan Anahtar kimlik doğrulamasını kullanarak oturum açmak için komut satırına `--shared-key-auth` seçeneğini dahil edin:</span><span class="sxs-lookup"><span data-stu-id="720fe-165">To log in using Shared Key authentication, include the `--shared-key-auth` option on the command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="720fe-166">[Örnek kabul betikleri](#sample-shell-scripts) bölümünde listelenen örnekler, hem Azure AD hem de Paylaşılan Anahtar kullanarak Azure CLI ile Batch hesabınızda nasıl oturum açacağınızı göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="720fe-166">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section show how to log into your Batch account with the Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="720fe-167">Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="720fe-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="720fe-168">Azure CLI, Batch işlerini kod yazmadan uçtan uca çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-168">You can use the Azure CLI to run Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="720fe-169">Batch şablon dosyaları Azure CLI’da havuz, iş ve görev oluşturmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="720fe-169">Batch template files support creating pools, jobs, and tasks with the Azure CLI.</span></span> <span data-ttu-id="720fe-170">Azure CLI, Batch hesabıyla ilişkilendirilmiş Azure Depolama hesabına işin giriş dosyalarını yüklemek ve bu hesaptan iş çıkış dosyalarını indirmek için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="720fe-170">You can also use the Azure CLI to upload job input files to the Azure Storage account associated with the Batch account, and download job output files from it.</span></span> <span data-ttu-id="720fe-171">Daha fazla bilgi için bkz. [Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="720fe-172">Örnek kabuk betikleri</span><span class="sxs-lookup"><span data-stu-id="720fe-172">Sample shell scripts</span></span>

<span data-ttu-id="720fe-173">Aşağıdaki tabloda yer alan örnek betikler, sık kullanılan görevleri gerçekleştirmek için Azure CLI komutlarını Batch ve Batch Management hizmetiyle birlikte nasıl kullanacağınızı göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="720fe-173">The sample scripts listed in the following table show how to use Azure CLI commands with the Batch service and Batch Management service to accomplish common tasks.</span></span> <span data-ttu-id="720fe-174">Bu örnek betikler Batch için Azure CLI'da yer alan birçok komutu kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="720fe-174">These sample scripts cover many of the commands available in the Azure CLI for Batch.</span></span> 

| <span data-ttu-id="720fe-175">Betik</span><span class="sxs-lookup"><span data-stu-id="720fe-175">Script</span></span> | <span data-ttu-id="720fe-176">Notlar</span><span class="sxs-lookup"><span data-stu-id="720fe-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="720fe-177">Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="720fe-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="720fe-178">Bir Batch hesabı oluşturur ve depolama hesabınızla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="720fe-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="720fe-179">Uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="720fe-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="720fe-180">Bir uygulama ekler ve paketlenmiş ikili dosyalarını karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="720fe-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="720fe-181">Batch havuzlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="720fe-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="720fe-182">Havuzlar için oluşturma, yeniden boyutlandırma ve yönetme işlemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="720fe-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="720fe-183">Batch ile bir iş ve görevlerini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="720fe-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="720fe-184">Bir işi çalıştırmayı ve görev eklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="720fe-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="720fe-185">Kaynak oluşturmak için JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="720fe-185">JSON files for resource creation</span></span>

<span data-ttu-id="720fe-186">Havuzlar ve işler gib Batch kaynakları oluşturduğunuzda parametrelerini komut satırı seçenekleri olarak geçirmek yerine yeni kaynağın yapılandırmasını içeren bir JSON dosyası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="720fe-187">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="720fe-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="720fe-188">Yalnızca komut satırı seçeneklerini kullanarak çoğu Batch kaynağını oluşturabilirsiniz ancak bazı özellikler, kaynak ayrıntılarını içeren JSON biçimli bir dosya belirtmenizi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="720fe-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="720fe-189">Örneğin, bir başlatma görevi için kaynak belirtmek istiyorsanız bir JSON dosyası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="720fe-189">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="720fe-190">Kaynak oluşturmak için gereken JSON söz dizimi dosyasını bulmak üzere [Batch REST API başvurusu][rest_api] belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="720fe-190">To see the JSON syntax required to create a resource, refer to the [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="720fe-191">REST API başvurusundaki her bir "Ekle *kaynak türü*" konusu ilgili kaynağı oluşturmak için örnek JSON betikleri içerir.</span><span class="sxs-lookup"><span data-stu-id="720fe-191">Each "Add *resource type*" topic in the REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="720fe-192">Bu örnek JSON betiklerini Azure CLI ile kullanabileceğiniz JSON dosyası şablonu olarak değerlendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-192">You can use those sample JSON scripts as templates for JSON files to use with the Azure CLI.</span></span> <span data-ttu-id="720fe-193">Örneğin havuz oluşturmak için JSON söz dizimini görmek istiyorsanız bkz. [Bir hesaba havuz ekleme][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="720fe-193">For example, to see the JSON syntax for pool creation, refer to [Add a pool to an account][rest_add_pool].</span></span>

<span data-ttu-id="720fe-194">Bir JSON dosyasını belirten örnek bir betik için bkz. [Batch ile bir iş ve görevlerini çalıştırma](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="720fe-195">Bir kaynak oluştururken JSON dosyası belirtirseniz, komut satırında ilgili kaynak için belirttiğiniz diğer parametreler yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="720fe-195">If you specify a JSON file when you create a resource, any other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="720fe-196">Batch kaynakları için etkili sorgular</span><span class="sxs-lookup"><span data-stu-id="720fe-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="720fe-197">Her Batch kaynak türü, Batch hesabınızı sorgulayan ve bu türdeki kaynakları listeleyen bir `list` komutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="720fe-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="720fe-198">Örneğin, hesabınızdaki havuzları ve bir işteki görevleri listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="720fe-198">For example, you can list the pools in your account and the tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="720fe-199">Batch hizmetini bir `list` işlemiyle sorguladığınızda döndürülen veri miktarını sınırlamak için OData yan tümcesi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-199">When you query the Batch service with a `list` operation, you can specify an OData clause to limit the amount of data returned.</span></span> <span data-ttu-id="720fe-200">Tüm filtreleme sunucu tarafında oluştuğu için yalnızca istediğiniz veriler aktarılır.</span><span class="sxs-lookup"><span data-stu-id="720fe-200">Because all filtering occurs server-side, only the data you request crosses the wire.</span></span> <span data-ttu-id="720fe-201">Liste işlemleri gerçekleştirirken bant genişliğinden (ve böylece zamandan) tasarruf etmek için bu yan tümceleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="720fe-201">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="720fe-202">Aşağıdaki tabloda Batch hizmeti tarafından desteklenen OData yan tümceleri listelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="720fe-202">The following table describes the OData clauses supported by the Batch service:</span></span>

| <span data-ttu-id="720fe-203">Yan Tümce</span><span class="sxs-lookup"><span data-stu-id="720fe-203">Clause</span></span> | <span data-ttu-id="720fe-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="720fe-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="720fe-205">Her varlık için bir özellik alt kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="720fe-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="720fe-206">Yalnızca belirtilen OData ifadesiyle eşleşen varlıklar döndürür.</span><span class="sxs-lookup"><span data-stu-id="720fe-206">Returns only entities that match the specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="720fe-207">Tek bir temel alınan REST çağrısındaki varlık bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="720fe-207">Obtains the entity information in a single underlying REST call.</span></span> <span data-ttu-id="720fe-208">Expand yan tümcesi şu anda yalnızca `stats` özelliğini desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="720fe-208">The expand clause currently supports only the `stats` property.</span></span> |

<span data-ttu-id="720fe-209">Bir OData yan tümcesinin nasıl kullanılacağını gösteren örnek betik için bkz. [Batch ile bir iş ve görevlerini çalıştırma](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-209">For a sample script that shows how to use an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="720fe-210">OData yan tümceleriyle etkili liste sorguları gerçekleştirme hakkında bilgi için bkz. [Azure Batch hizmetini etkili bir şekilde sorgulama](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-210">For more information on performing efficient list queries with OData clauses, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="720fe-211">Sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="720fe-211">Troubleshooting tips</span></span>

<span data-ttu-id="720fe-212">Azure CLI sorunlarını giderirken aşağıdaki ipuçları yardımcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="720fe-212">The following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="720fe-213">Herhangi bir CLI komutu için **yardım metni** almak üzere `-h` kullanın</span><span class="sxs-lookup"><span data-stu-id="720fe-213">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="720fe-214">**Ayrıntılı** komut çıktısını görüntülemek için `-v` ve `-vv` kullanın.</span><span class="sxs-lookup"><span data-stu-id="720fe-214">Use `-v` and `-vv` to display **verbose** command output.</span></span> <span data-ttu-id="720fe-215">`-vv` bayrağı eklendiğinde Azure CLI gerçek REST isteklerini ve yanıtlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="720fe-215">When the `-vv` flag is included, the Azure CLI displays the actual REST requests and responses.</span></span> <span data-ttu-id="720fe-216">Bu anahtarlar tam hata çıktısını görüntülemek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="720fe-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="720fe-217">`--json` seçeneği ile **komut çıktısını JSON olarak** görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-217">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="720fe-218">Örneğin, `az batch pool show pool001 --json` seçeneği pool001'in özelliklerini JSON biçiminde gösterir.</span><span class="sxs-lookup"><span data-stu-id="720fe-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="720fe-219">Bundan sonra bu çıktıyı kopyalayıp bir `--json-file` içinde kullanmak üzere değiştirebilirsiniz (bu makalenin başındaki [JSON dosyaları](#json-files) kısmına bakın).</span><span class="sxs-lookup"><span data-stu-id="720fe-219">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* <span data-ttu-id="720fe-220">[Batch forumu][batch_forum] Batch ekibi üyeleri tarafından takip edilmektedir.</span><span class="sxs-lookup"><span data-stu-id="720fe-220">The [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="720fe-221">Sorun yaşamanız veya belirli bir işlemle ilgili yardım almak istemeniz durumunda sorularınızı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="720fe-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="720fe-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="720fe-222">Next steps</span></span>

* <span data-ttu-id="720fe-223">Azure CLI hakkında daha fazla bilgi için bkz. [Azure CLI belgeleri](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="720fe-223">For more information about the Azure CLI, see the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="720fe-224">Batch kaynakları hakkında daha fazla bilgi için bkz. [Geliştiriciler için Azure Batch'e genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="720fe-225">Batch şablonlarını kullanarak havuz, iş ve görevleri kod yazmadan oluşturma hakkında daha fazla bilgi için bkz. [Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="720fe-225">For more information about using Batch templates to create pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
