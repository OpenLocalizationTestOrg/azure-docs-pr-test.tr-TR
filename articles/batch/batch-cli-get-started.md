---
title: "Toplu işlemi için Azure CLI aaaGet Başlarken | Microsoft Docs"
description: "Bir giriş, Azure Batch hizmetinin kaynakları yönetmek için Azure CLI toohello toplu iş komutları Al"
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
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="ab0b3-103">Batch kaynaklarını Azure CLI ile yönetme</span><span class="sxs-lookup"><span data-stu-id="ab0b3-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="ab0b3-104">Hello Azure CLI 2.0 Azure kaynaklarını yönetmek için Azure'nın yeni komut satırı deneyimidir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="ab0b3-105">MacOS, Linux ve Windows’da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="ab0b3-106">Azure CLI 2.0 yönetmek ve hello komut satırından Azure kaynaklarını yönetmek için optimize edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="ab0b3-107">Azure toplu işlem hesaplarını ve havuzlar, işler ve görevler gibi toomanage kaynakları hello Azure CLI toomanage kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="ab0b3-108">Merhaba çoğunu komut Hello Azure CLI, yürütmek ile aynı görevleri hello Batch API'leri, Azure portal ve Batch PowerShell cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="ab0b3-109">Bu makalede Batch ile [Azure CLI sürüm 2.0](https://docs.microsoft.com/cli/azure/overview) kullanımına genel bakışa yer verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="ab0b3-110">Bkz: [Azure CLI 2.0 ile çalışmaya başlama](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Azure ile Merhaba CLI kullanarak genel bir bakış için.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="ab0b3-111">Microsoft hello Azure CLI, sürüm 2.0 hello en son sürümünü kullanmanızı önerir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="ab0b3-112">Sürüm 2.0 hakkında daha fazla bilgi için bkz. [Azure Komut Satırı 2.0 genel kullanıma sunuldu](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="ab0b3-113">Azure CLI Hello ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ab0b3-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="ab0b3-114">tooinstall hello Azure CLI adımları özetlenen hello [yükleme hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="ab0b3-115">Azure CLI yüklemenizi güncelleştirmenizi öneririz sık tootake avantajlarından hizmet güncelleştirmeleri ve geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="ab0b3-116">Komut yardımı</span><span class="sxs-lookup"><span data-stu-id="ab0b3-116">Command help</span></span>

<span data-ttu-id="ab0b3-117">Her komut için Yardım metni hello Azure CLI ekleyerek görüntüleyebileceğiniz `-h` toohello komutu.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="ab0b3-118">Diğer seçenekleri atın.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-118">Omit any other options.</span></span> <span data-ttu-id="ab0b3-119">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-119">For example:</span></span>

* <span data-ttu-id="ab0b3-120">Merhaba tooget yardımını `az` komutu, girin:`az -h`</span><span class="sxs-lookup"><span data-stu-id="ab0b3-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="ab0b3-121">tooget hello CLI, tüm toplu komutlarda listesini kullanın:`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="ab0b3-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="ab0b3-122">bir Batch hesabı oluşturma tooget Yardım girin:`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="ab0b3-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="ab0b3-123">Şüpheli zaman hello kullan `-h` komut satırı seçeneği tooget Yardım herhangi bir Azure CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="ab0b3-124">Merhaba kullanılan Azure CLI'ın önceki sürümlerini `azure` toopreface CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="ab0b3-125">Sürüm 2.0'da tüm komutlar `az` ile kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="ab0b3-126">Sürüm 2.0, komut dosyaları toouse hello yeni sözdizimi emin tooupdate olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="ab0b3-127">Ayrıca, hakkında ayrıntılar için toohello Azure CLI başvuru belgelerine başvurun [toplu için Azure CLI komutları](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="ab0b3-128">Oturum açma ve kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="ab0b3-128">Log in and authenticate</span></span>

<span data-ttu-id="ab0b3-129">toouse hello Azure CLI toplu işlem ile içinde toolog gerekir ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="ab0b3-130">İki basit adımları toofollow vardır:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="ab0b3-131">**Azure'da oturum açın.**</span><span class="sxs-lookup"><span data-stu-id="ab0b3-131">**Log into Azure.**</span></span> <span data-ttu-id="ab0b3-132">Azure verir oturum dahil olmak üzere, tooAzure Resource Manager komutlara erişmek [toplu yönetim hizmeti](batch-management-dotnet.md) komutları.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="ab0b3-133">**Batch hesabınızda oturum açın.**</span><span class="sxs-lookup"><span data-stu-id="ab0b3-133">**Log into your Batch account.**</span></span> <span data-ttu-id="ab0b3-134">Toplu işlem hesabı verir oturum tooBatch hizmeti komutları erişin.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="ab0b3-135">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="ab0b3-135">Log in tooAzure</span></span>

<span data-ttu-id="ab0b3-136">Azure, ayrıntılı olarak açıklanmıştır içine birkaç farklı şekilde toolog vardır [oturum Azure CLI 2.0 oturum](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="ab0b3-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="ab0b3-137">[Etkileşimli olarak oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="ab0b3-138">Azure CLI komutları kendiniz hello komut satırından çalıştırırken etkileşimli olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="ab0b3-139">[Hizmet sorumlusu ile oturum açma](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="ab0b3-140">Azure CLI komutlarını bir betikten veya uygulamadan çalıştırdığınızda hizmet sorumlusuyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="ab0b3-141">Bu makalede Hello amaçlarla gösteriyoruz nasıl toolog Azure içine etkileşimli olarak.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="ab0b3-142">Tür [az oturum açma](https://docs.microsoft.com/cli/azure/#login) hello komut satırında:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="ab0b3-143">Merhaba `az login` tooauthenticate, aşağıda gösterildiği gibi kullanabileceğiniz belirteci komutu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="ab0b3-144">Hello sağlanan yönergeleri tooopen bir web sayfası izleyin ve hello belirteci tooAzure gönderin:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![İçinde tooAzure oturum](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="ab0b3-146">Merhaba örnekler listelenen hello [örnek Kabuk komut dosyalarını](#sample-shell-scripts) de Göster nasıl bölümünde toostart Azure'da etkileşimli olarak oturum açarak, Azure CLI oturumunuz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="ab0b3-147">Oturum açtıktan sonra toplu hesaplar, anahtarları, uygulama paketleri ve kotalar dahil olmak üzere Batch Yönetimi kaynaklarla komutları toowork çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="ab0b3-148">Toplu işlem hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="ab0b3-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="ab0b3-149">toouse hello Azure CLI toomanage toplu gibi kaynaklar havuzlar, işler ve görevler, Batch hesabınızda toolog gerekir ve kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="ab0b3-150">toohello Batch hizmeti toolog kullanmak hello [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) komutu.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="ab0b3-151">Batch hesabınızla kimlik doğrulamasından geçmek için kullanabileceğiniz iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="ab0b3-152">**Azure Active Directory (Azure AD) kimlik doğrulamasını kullanmak.**</span><span class="sxs-lookup"><span data-stu-id="ab0b3-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="ab0b3-153">Azure AD ile kimlik doğrulaması toplu işlemle hello Azure CLI kullandığınızda hello varsayılan ayardır ve çoğu senaryolar için önerilir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="ab0b3-154">İçinde tooAzure hello önceki bölümde açıklandığı gibi etkileşimli olarak oturum açtığınızda hello Azure CLI tooyour toplu işlem hesabı bu kimlik bilgilerini kullanarak oturum için kimlik bilgilerinizi, önbelleğe alınır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="ab0b3-155">Bir hizmet sorumlusunu kullanarak tooAzure içinde oturum açarsanız, bu kimlik bilgilerini tooyour toplu işlem hesabı içinde kullanılan toolog ayrıca değildir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="ab0b3-156">Azure AD'nin avantajlarından biri rol tabanlı erişim denetimine (RBAC) sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="ab0b3-157">Bunlar hello hesabı anahtarları sahip olup olmadığına yerine RBAC ile bir kullanıcının erişimi kendilerine atanmış rolün bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="ab0b3-158">Hesap anahtarlarını yönetmek yerine RBAC rollerini yönetebilir ve erişimle kimlik doğrulamasını Azure AD'ye bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="ab0b3-159">Azure AD ile kimlik doğrulaması gereklidir oluşturduysanız Azure Batch hesabınızla kendi havuzu ayırma modu ayarlamak too'User abonelik '.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="ab0b3-160">toolog tooyour toplu olarak Azure AD kullanarak hesap, çağrı hello [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) komutu:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="ab0b3-161">**Paylaşılan Anahtar kimlik doğrulamasını kullanarak.**</span><span class="sxs-lookup"><span data-stu-id="ab0b3-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="ab0b3-162">[Paylaşılan anahtar kimlik doğrulaması](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) kullanır, hesabınız erişim tuşları tooauthenticate Azure CLI komutları hello için Batch hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="ab0b3-163">Azure CLI betikleri tooautomate çağıran toplu iş komutları oluşturuyorsanız, paylaşılan anahtar kimlik doğrulaması veya bir Azure AD hizmet sorumlusu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="ab0b3-164">Bazı senaryolarda Paylaşılan Anahtar ile kimlik doğrulaması, hizmet sorumlusu oluşturmaktan daha kolay olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="ab0b3-165">Paylaşılan anahtar kimlik doğrulaması kullanarak toolog dahil hello `--shared-key-auth` hello komut satırı seçeneği:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="ab0b3-166">Merhaba örnekler listelenen hello [örnek Kabuk komut dosyalarını](#sample-shell-scripts) bölüm Göster nasıl toolog Batch hesabınızla içine hello Azure CLI her ikisini de kullanarak Azure AD ve paylaşılan anahtar.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="ab0b3-167">Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma</span><span class="sxs-lookup"><span data-stu-id="ab0b3-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="ab0b3-168">Kod yazmadan hello Azure CLI toorun toplu işleri uçtan uca kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="ab0b3-169">Toplu işlem şablonu dosyaları oluşturma havuzlar, işler ve görevler hello Azure CLI ile destekler.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="ab0b3-170">Hello Azure CLI tooupload iş girdi dosyalarını da kullanabilirsiniz hello ile ilişkili toohello Azure depolama hesabı Batch hesabı ve proje çıktı dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="ab0b3-171">Daha fazla bilgi için bkz. [Azure Batch CLI Şablonlarını ve Dosya Aktarımı (Önizleme) özelliğini kullanma](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="ab0b3-172">Örnek kabuk betikleri</span><span class="sxs-lookup"><span data-stu-id="ab0b3-172">Sample shell scripts</span></span>

<span data-ttu-id="ab0b3-173">Merhaba örnek komut dosyaları, toplu yönetim hizmeti tooaccomplish ortak görevleri hello Batch hizmeti ile nasıl toouse Azure CLI komutları Tablo Göster aşağıdaki hello listelenir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="ab0b3-174">Bu örnek komut dosyalarını hello toplu işlemi için Azure CLI bulunan hello komutların çoğu kapsar.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="ab0b3-175">Betik</span><span class="sxs-lookup"><span data-stu-id="ab0b3-175">Script</span></span> | <span data-ttu-id="ab0b3-176">Notlar</span><span class="sxs-lookup"><span data-stu-id="ab0b3-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab0b3-177">Batch hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab0b3-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="ab0b3-178">Bir Batch hesabı oluşturur ve depolama hesabınızla ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="ab0b3-179">Uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="ab0b3-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="ab0b3-180">Bir uygulama ekler ve paketlenmiş ikili dosyalarını karşıya yükler.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="ab0b3-181">Batch havuzlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="ab0b3-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="ab0b3-182">Havuzlar için oluşturma, yeniden boyutlandırma ve yönetme işlemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="ab0b3-183">Batch ile bir iş ve görevlerini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ab0b3-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="ab0b3-184">Bir işi çalıştırmayı ve görev eklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="ab0b3-185">Kaynak oluşturmak için JSON dosyaları</span><span class="sxs-lookup"><span data-stu-id="ab0b3-185">JSON files for resource creation</span></span>

<span data-ttu-id="ab0b3-186">Havuzlar ve işler gibi Batch kaynaklarını oluşturduğunuzda, komut satırı seçeneklerini parametrelerini geçirme yerine hello yeni kaynağın yapılandırmasını içeren bir JSON dosyası belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="ab0b3-187">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="ab0b3-188">Yalnızca komut satırı seçeneklerini kullanarak birçok Batch kaynaklarını oluşturabilirsiniz, ancak bazı özellikler hello kaynak ayrıntılarını içeren bir JSON biçimli dosya belirttiğiniz gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="ab0b3-189">Örneğin, toospecify kaynak dosyaları için bir başlangıç görevi istiyorsanız bir JSON dosyası kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="ab0b3-190">bir kaynak toosee hello JSON söz dizimi gerekli toocreate, toohello başvuran [Batch REST API'si başvurusu] [ rest_api] belgeleri.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="ab0b3-191">Her "Ekle *kaynak türü*" Merhaba REST API Başvurusu konudaki bu kaynağı oluşturmak için örnek JSON komut dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="ab0b3-192">JSON dosyaları toouse hello Azure CLI ile için bu örnek JSON komutlar şablon olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="ab0b3-193">Toosee hello JSON söz dizimi havuzu oluşturma, örneğin, başvuran çok[bir havuz tooan hesabı eklemek][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="ab0b3-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="ab0b3-194">Bir JSON dosyasını belirten örnek bir betik için bkz. [Batch ile bir iş ve görevlerini çalıştırma](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ab0b3-195">Bir kaynak oluşturduğunuzda bir JSON dosyası belirtirseniz, bu kaynak için hello komut satırında belirttiğiniz herhangi bir parametre yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="ab0b3-196">Batch kaynakları için etkili sorgular</span><span class="sxs-lookup"><span data-stu-id="ab0b3-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="ab0b3-197">Her Batch kaynak türü, Batch hesabınızı sorgulayan ve bu türdeki kaynakları listeleyen bir `list` komutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="ab0b3-198">Örneğin, bir iş hesabı ve hello görevleri de hello havuzları listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="ab0b3-199">Merhaba Batch hizmetiyle sorguladığınızda bir `list` işlemi, döndürülen veriler, bir OData yan tümcesi toolimit hello miktarını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="ab0b3-200">Filtre işleminin tümü sunucu tarafında oluştuğundan, yalnızca, istek hello verileri hello kablo kestiği.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="ab0b3-201">Bu yan tümceleri toosave bant genişliğini kullan (ve bu nedenle saat) listeleme işlemleri gerçekleştirdiğinizde.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="ab0b3-202">Merhaba aşağıdaki tabloda hello OData yan tümceleri hello Batch hizmeti tarafından desteklenen açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="ab0b3-203">Yan Tümce</span><span class="sxs-lookup"><span data-stu-id="ab0b3-203">Clause</span></span> | <span data-ttu-id="ab0b3-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ab0b3-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="ab0b3-205">Her varlık için bir özellik alt kümesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="ab0b3-206">Merhaba eşleşen döndürür yalnızca varlıklar OData ifade belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="ab0b3-207">Tek bir temel REST çağrısı Hello varlık bilgileri alır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="ab0b3-208">Merhaba genişletin destekler yalnızca hello yan tümcesi şu anda `stats` özelliği.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="ab0b3-209">Bir örnek komut dosyası için nasıl toouse bir OData yan tümcesi bkz gösteren [toplu işlemle bir işi ve görevleri çalıştırmak](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="ab0b3-210">OData yan tümceleri içeren verimli listesi sorguları gerçekleştirme hakkında daha fazla bilgi için bkz: [hello Azure Batch hizmetinin verimli bir şekilde sorgu](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="ab0b3-211">Sorun giderme ipuçları</span><span class="sxs-lookup"><span data-stu-id="ab0b3-211">Troubleshooting tips</span></span>

<span data-ttu-id="ab0b3-212">Azure CLI sorunlarını giderirken hello aşağıdaki ipuçları yardımcı olabilir:</span><span class="sxs-lookup"><span data-stu-id="ab0b3-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="ab0b3-213">Kullanım `-h` tooget **Yardım metni** için herhangi bir CLI komutu</span><span class="sxs-lookup"><span data-stu-id="ab0b3-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="ab0b3-214">Kullanım `-v` ve `-vv` toodisplay **ayrıntılı** komut çıktı.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="ab0b3-215">Ne zaman hello `-vv` bayrağı dahil, hello Azure CLI hello gerçek REST isteklerinin ve yanıtlarının görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="ab0b3-216">Bu anahtarlar tam hata çıktısını görüntülemek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="ab0b3-217">Görüntüleyebileceğiniz **komutu çıktıyı JSON olarak** hello ile `--json` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="ab0b3-218">Örneğin, `az batch pool show pool001 --json` seçeneği pool001'in özelliklerini JSON biçiminde gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="ab0b3-219">Daha sonra kopyalayın ve bu çıkış toouse değiştirme bir `--json-file` (bkz [JSON dosyaları](#json-files) bu makalenin önceki).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="ab0b3-220">Merhaba [toplu işlem Forumu] [ batch_forum] Batch ekip üyeleri tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="ab0b3-221">Sorun yaşamanız veya belirli bir işlemle ilgili yardım almak istemeniz durumunda sorularınızı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab0b3-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab0b3-222">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab0b3-222">Next steps</span></span>

* <span data-ttu-id="ab0b3-223">Merhaba hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="ab0b3-224">Batch kaynakları hakkında daha fazla bilgi için bkz. [Geliştiriciler için Azure Batch'e genel bakış](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="ab0b3-225">Kod yazmadan toplu şablonları toocreate havuzlar, işler ve görevler kullanma hakkında daha fazla bilgi için bkz: [kullanım Azure Batch CLI şablonları ve dosya aktarımı (Önizleme)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ab0b3-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
