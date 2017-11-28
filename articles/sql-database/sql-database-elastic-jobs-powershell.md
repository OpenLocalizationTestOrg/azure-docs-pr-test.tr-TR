---
title: "aaaCreate ve esnek işleri PowerShell kullanarak yönetme | Microsoft Docs"
description: "PowerShell toomanage Azure SQL Database havuzları kullanılan"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a><span data-ttu-id="7210f-103">PowerShell (Önizleme) kullanarak SQL Database esnek işleri oluşturmak ve yönetmek</span><span class="sxs-lookup"><span data-stu-id="7210f-103">Create and manage SQL Database elastic jobs using PowerShell (preview)</span></span>

<span data-ttu-id="7210f-104">Merhaba PowerShell API'leri için **esnek veritabanı işleri** (Önizleme) içinde göre betikleri yürütülecek grubu tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7210f-104">hello PowerShell APIs for **Elastic Database jobs** (in preview), let you define a group of databases against which scripts will execute.</span></span> <span data-ttu-id="7210f-105">Bu makalede gösterilmektedir nasıl toocreate ve yönetme **esnek veritabanı işleri** PowerShell cmdlet'lerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7210f-105">This article shows how toocreate and manage **Elastic Database jobs** using PowerShell cmdlets.</span></span> <span data-ttu-id="7210f-106">Bkz: [esnek iş genel bakış](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7210f-106">See [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7210f-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7210f-107">Prerequisites</span></span>
* <span data-ttu-id="7210f-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="7210f-108">An Azure subscription.</span></span> <span data-ttu-id="7210f-109">Ücretsiz deneme için bkz: [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7210f-109">For a free trial, see [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7210f-110">Merhaba esnek veritabanı araçları ile oluşturulmuş bir veritabanları kümesi.</span><span class="sxs-lookup"><span data-stu-id="7210f-110">A set of databases created with hello Elastic Database tools.</span></span> <span data-ttu-id="7210f-111">Bkz: [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7210f-111">See [Get started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span>
* <span data-ttu-id="7210f-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7210f-112">Azure PowerShell.</span></span> <span data-ttu-id="7210f-113">Ayrıntılı bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7210f-113">For detailed information, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
* <span data-ttu-id="7210f-114">**Esnek veritabanı iş** PowerShell paketi: bkz [esnek veritabanı yükleme işleri](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="7210f-114">**Elastic Database jobs** PowerShell package: See [Installing Elastic Database jobs](sql-database-elastic-jobs-service-installation.md)</span></span>

### <a name="select-your-azure-subscription"></a><span data-ttu-id="7210f-115">Azure aboneliğinizi seçin</span><span class="sxs-lookup"><span data-stu-id="7210f-115">Select your Azure subscription</span></span>
<span data-ttu-id="7210f-116">tooselect hello abonelik, abonelik kimliği gerekir (**- Subscriptionıd**) veya abonelik adı (**varlığıyla - SubscriptionName**).</span><span class="sxs-lookup"><span data-stu-id="7210f-116">tooselect hello subscription you need your subscription Id (**-SubscriptionId**) or subscription name (**-SubscriptionName**).</span></span> <span data-ttu-id="7210f-117">Birden çok aboneliğiniz varsa hello çalıştırabilirsiniz **Get-AzureRmSubscription** cmdlet'i ve kopyalama hello istenen hello sonuç kümesinden abonelik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7210f-117">If you have multiple subscriptions you can run hello **Get-AzureRmSubscription** cmdlet and copy hello desired subscription information from hello result set.</span></span> <span data-ttu-id="7210f-118">Abonelik bilgilerinizi olduktan sonra komutunu tooset aşağıdaki hello hello varsayılan olarak bu abonelik çalıştırmak, yani işleri oluşturmaya ve yönetmeye için hedef hello:</span><span class="sxs-lookup"><span data-stu-id="7210f-118">Once you have your subscription information, run hello following commandlet tooset this subscription as hello default, namely hello target for creating and managing jobs:</span></span>

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

<span data-ttu-id="7210f-119">Merhaba [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) kullanım toodevelop için önerilen ve PowerShell betikleri hello esnek veritabanı işleri karşı yürütün.</span><span class="sxs-lookup"><span data-stu-id="7210f-119">hello [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) is recommended for usage toodevelop and execute PowerShell scripts against hello Elastic Database jobs.</span></span>

## <a name="elastic-database-jobs-objects"></a><span data-ttu-id="7210f-120">Esnek veritabanı işleri nesneleri</span><span class="sxs-lookup"><span data-stu-id="7210f-120">Elastic Database jobs objects</span></span>
<span data-ttu-id="7210f-121">Aşağıdaki tabloda tüm hello nesne türlerini Hello **esnek veritabanı işleri** açıklaması ve ilgili PowerShell API'lerinden birlikte.</span><span class="sxs-lookup"><span data-stu-id="7210f-121">hello following table lists out all hello object types of **Elastic Database jobs** along with its description and relevant PowerShell APIs.</span></span>

<table style="width:100%">
  <tr>
    <th><span data-ttu-id="7210f-122">Nesne türü</span><span class="sxs-lookup"><span data-stu-id="7210f-122">Object Type</span></span></th>
    <th><span data-ttu-id="7210f-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7210f-123">Description</span></span></th>
    <th><span data-ttu-id="7210f-124">İlgili PowerShell API'leri</span><span class="sxs-lookup"><span data-stu-id="7210f-124">Related PowerShell APIs</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="7210f-125">Kimlik Bilgisi</span><span class="sxs-lookup"><span data-stu-id="7210f-125">Credential</span></span></td>
    <td><span data-ttu-id="7210f-126">Toodatabases betiklerinin yürütülmesi veya DACPACs uygulamasının bağlanırken kullanıcı adı ve parola toouse.</span><span class="sxs-lookup"><span data-stu-id="7210f-126">Username and password toouse when connecting toodatabases for execution of scripts or application of DACPACs.</span></span> <p><span data-ttu-id="7210f-127">Merhaba parola hello esnek veritabanı iş veritabanında saklamak tooand göndermeden önce şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="7210f-127">hello password is encrypted before sending tooand storing in hello Elastic Database Jobs database.</span></span>  <span data-ttu-id="7210f-128">Merhaba parola hello esnek veritabanı iş hizmeti ile oluşturulan ve hello yükleme betikten karşıya hello kimlik bilgisi tarafından şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="7210f-128">hello password is decrypted by hello Elastic Database Jobs service via hello credential created and uploaded from hello installation script.</span></span></td>
    <td><p><span data-ttu-id="7210f-129">Get-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="7210f-129">Get-AzureSqlJobCredential</span></span></p>
    <p><span data-ttu-id="7210f-130">AzureSqlJobCredential yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-130">New-AzureSqlJobCredential</span></span></p><p><span data-ttu-id="7210f-131">Set-AzureSqlJobCredential</span><span class="sxs-lookup"><span data-stu-id="7210f-131">Set-AzureSqlJobCredential</span></span></p></td></td>
  </tr>

  <tr>
    <td><span data-ttu-id="7210f-132">Betik</span><span class="sxs-lookup"><span data-stu-id="7210f-132">Script</span></span></td>
    <td><span data-ttu-id="7210f-133">Transact-SQL komut dosyası toobe veritabanları arasında yürütme için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7210f-133">Transact-SQL script toobe used for execution across databases.</span></span>  <span data-ttu-id="7210f-134">Merhaba hizmeti hataları bağlı hello betik yürütme işlemi yeniden deneyecek beri hello betik yazarı toobe ıdempotent olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7210f-134">hello script should be authored toobe idempotent since hello service will retry execution of hello script upon failures.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="7210f-135">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="7210f-135">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="7210f-136">Get-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="7210f-136">Get-AzureSqlJobContentDefinition</span></span></p>
    <p><span data-ttu-id="7210f-137">AzureSqlJobContent yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-137">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="7210f-138">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="7210f-138">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>

  <tr>
    <td><span data-ttu-id="7210f-139">DACPAC</span><span class="sxs-lookup"><span data-stu-id="7210f-139">DACPAC</span></span></td>
    <td><span data-ttu-id="7210f-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Veri katmanı uygulaması </a> veritabanları arasında uygulanan toobe paketi.</span><span class="sxs-lookup"><span data-stu-id="7210f-140"><a href="https://msdn.microsoft.com/library/ee210546.aspx">Data-tier application </a> package toobe applied across databases.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="7210f-141">Get-AzureSqlJobContent</span><span class="sxs-lookup"><span data-stu-id="7210f-141">Get-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="7210f-142">AzureSqlJobContent yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-142">New-AzureSqlJobContent</span></span></p>
    <p><span data-ttu-id="7210f-143">Set-AzureSqlJobContentDefinition</span><span class="sxs-lookup"><span data-stu-id="7210f-143">Set-AzureSqlJobContentDefinition</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="7210f-144">Veritabanı hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-144">Database Target</span></span></td>
    <td><span data-ttu-id="7210f-145">Veritabanı ve sunucu işaret tooan Azure SQL veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="7210f-145">Database and server name pointing tooan Azure SQL Database.</span></span>

    </td>
    <td>
    <p><span data-ttu-id="7210f-146">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-146">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="7210f-147">AzureSqlJobTarget yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-147">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
  <tr>
    <td><span data-ttu-id="7210f-148">Parça eşleme hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-148">Shard Map Target</span></span></td>
    <td><span data-ttu-id="7210f-149">Bir veritabanı hedef ve bir kimlik bilgisi toobe birleşimi bir esnek veritabanı parça eşlemesi içinde depolanan toodetermine bilgileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7210f-149">Combination of a database target and a credential toobe used toodetermine information stored within an Elastic Database shard map.</span></span>
    </td>
    <td>
    <p><span data-ttu-id="7210f-150">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-150">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="7210f-151">AzureSqlJobTarget yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-151">New-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="7210f-152">Set-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-152">Set-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="7210f-153">Özel Toplama hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-153">Custom Collection Target</span></span></td>
    <td><span data-ttu-id="7210f-154">Veritabanlarını toocollectively tanımlanan Grup yürütme için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7210f-154">Defined group of databases toocollectively use for execution.</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-155">Get-AzureSqlJobTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-155">Get-AzureSqlJobTarget</span></span></p>
    <p><span data-ttu-id="7210f-156">AzureSqlJobTarget yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-156">New-AzureSqlJobTarget</span></span></p>
    </td>
  </tr>
<tr>
    <td><span data-ttu-id="7210f-157">Özel Toplama alt hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-157">Custom Collection Child Target</span></span></td>
    <td><span data-ttu-id="7210f-158">Özel bir koleksiyondan başvurulan veritabanı hedefi.</span><span class="sxs-lookup"><span data-stu-id="7210f-158">Database target that is referenced from a custom collection.</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-159">Ekleme AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-159">Add-AzureSqlJobChildTarget</span></span></p>
    <p><span data-ttu-id="7210f-160">Remove-AzureSqlJobChildTarget</span><span class="sxs-lookup"><span data-stu-id="7210f-160">Remove-AzureSqlJobChildTarget</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-161">İş</span><span class="sxs-lookup"><span data-stu-id="7210f-161">Job</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-162">Kullanılan tootrigger yürütme veya toofulfill bir zamanlama olabilir bir işin parametrelerini tanımı.</span><span class="sxs-lookup"><span data-stu-id="7210f-162">Definition of parameters for a job that can be used tootrigger execution or toofulfill a schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-163">Get-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="7210f-163">Get-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="7210f-164">AzureSqlJob yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-164">New-AzureSqlJob</span></span></p>
    <p><span data-ttu-id="7210f-165">Set-AzureSqlJob</span><span class="sxs-lookup"><span data-stu-id="7210f-165">Set-AzureSqlJob</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-166">İş yürütme</span><span class="sxs-lookup"><span data-stu-id="7210f-166">Job Execution</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-167">Bir komut dosyası çalıştırma veya hataları olan veritabanı bağlantıları için kimlik bilgilerini kullanarak bir DACPAC tooa hedef uygulama görevleri gerekli toofulfill kapsayıcının uygun tooan yürütme İlkesi işlenir.</span><span class="sxs-lookup"><span data-stu-id="7210f-167">Container of tasks necessary toofulfill either executing a script or applying a DACPAC tooa target using credentials for database connections with failures handled in accordance tooan execution policy.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-168">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-168">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-169">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-169">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-170">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-170">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-171">Bekleme AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-171">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-172">İş görevi yürütmede</span><span class="sxs-lookup"><span data-stu-id="7210f-172">Job Task Execution</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-173">İş toofulfill bir işi tek birimidir.</span><span class="sxs-lookup"><span data-stu-id="7210f-173">Single unit of work toofulfill a job.</span></span></p>
    <p><span data-ttu-id="7210f-174">Bir iş görevi mümkün toosuccessfully değilse yürütmek, hello ortaya çıkan özel durum iletisi oturum açmış olmanız ve yeni bir eşleşen iş görevi oluşturulur ve belirtilen belge toohello içinde yürütülen yürütme ilkesi.</span><span class="sxs-lookup"><span data-stu-id="7210f-174">If a job task is not able toosuccessfully execute, hello resulting exception message will be logged and a new matching job task will be created and executed in accordance toohello specified execution policy.</span></span></p></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-175">Get-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-175">Get-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-176">Start-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-176">Start-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-177">Stop-AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-177">Stop-AzureSqlJobExecution</span></span></p>
    <p><span data-ttu-id="7210f-178">Bekleme AzureSqlJobExecution</span><span class="sxs-lookup"><span data-stu-id="7210f-178">Wait-AzureSqlJobExecution</span></span></p>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-179">İş yürütme İlkesi</span><span class="sxs-lookup"><span data-stu-id="7210f-179">Job Execution Policy</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-180">Yürütme zaman aşımı, yeniden deneme sınırları ve aralıklarla yeniden denemeler arasında denetimleri işi.</span><span class="sxs-lookup"><span data-stu-id="7210f-180">Controls job execution timeouts, retry limits and intervals between retries.</span></span></p>
    <p><span data-ttu-id="7210f-181">Esnek veritabanı iş denemeler arasındaki aralığı üstel geri alma ile temelde sonsuz yeniden deneme iş görevi başarısızlık neden varsayılan iş yürütme İlkesi içerir.</span><span class="sxs-lookup"><span data-stu-id="7210f-181">Elastic Database jobs includes a default job execution policy which cause essentially infinite retries of job task failures with exponential backoff of intervals between each retry.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-182">Get-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="7210f-182">Get-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="7210f-183">AzureSqlJobExecutionPolicy yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-183">New-AzureSqlJobExecutionPolicy</span></span></p>
    <p><span data-ttu-id="7210f-184">Set-AzureSqlJobExecutionPolicy</span><span class="sxs-lookup"><span data-stu-id="7210f-184">Set-AzureSqlJobExecutionPolicy</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-185">Zamanlama</span><span class="sxs-lookup"><span data-stu-id="7210f-185">Schedule</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-186">Zaman belirtimi yürütme tootake bağlantısı yeniden aralığı veya tek bir zaman için temel.</span><span class="sxs-lookup"><span data-stu-id="7210f-186">Time based specification for execution tootake place either on a reoccurring interval or at a single time.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-187">Get-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="7210f-187">Get-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="7210f-188">AzureSqlJobSchedule yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-188">New-AzureSqlJobSchedule</span></span></p>
    <p><span data-ttu-id="7210f-189">Set-AzureSqlJobSchedule</span><span class="sxs-lookup"><span data-stu-id="7210f-189">Set-AzureSqlJobSchedule</span></span></p>
    </td>
  </tr>

<tr>
    <td><span data-ttu-id="7210f-190">İş Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="7210f-190">Job Triggers</span></span></td>
    <td>
    <p><span data-ttu-id="7210f-191">Bir iş ve toohello zamanlamaya göre bir zamanlama tootrigger iş yürütme arasında bir eşleme.</span><span class="sxs-lookup"><span data-stu-id="7210f-191">A mapping between a job and a schedule tootrigger job execution according toohello schedule.</span></span></p>
    </td>
    <td>
    <p><span data-ttu-id="7210f-192">AzureSqlJobTrigger yeni</span><span class="sxs-lookup"><span data-stu-id="7210f-192">New-AzureSqlJobTrigger</span></span></p>
    <p><span data-ttu-id="7210f-193">Remove-AzureSqlJobTrigger</span><span class="sxs-lookup"><span data-stu-id="7210f-193">Remove-AzureSqlJobTrigger</span></span></p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a><span data-ttu-id="7210f-194">Desteklenen esnek veritabanı işleri türleri Grup</span><span class="sxs-lookup"><span data-stu-id="7210f-194">Supported Elastic Database jobs group types</span></span>
<span data-ttu-id="7210f-195">Merhaba iş Transact-SQL (T-SQL) komut dosyaları veya DACPACs uygulama grubu yürütür.</span><span class="sxs-lookup"><span data-stu-id="7210f-195">hello job executes Transact-SQL (T-SQL) scripts or application of DACPACs across a group of databases.</span></span> <span data-ttu-id="7210f-196">Bir iş üzerinde yürütülen gönderilen toobe olduğunda veritabanlarının, hello iş "Merhaba burada her hello gerçekleştirir alt işlere genişletir" bir grup hello grubu tek bir veritabanında karşı yürütme istedi.</span><span class="sxs-lookup"><span data-stu-id="7210f-196">When a job is submitted toobe executed across a group of databases, hello job “expands” hello into child jobs where each performs hello requested execution against a single database in hello group.</span></span> 

<span data-ttu-id="7210f-197">İki tür oluşturabileceğiniz Grup vardır:</span><span class="sxs-lookup"><span data-stu-id="7210f-197">There are two types of groups that you can create:</span></span> 

* <span data-ttu-id="7210f-198">[Parça eşleme](sql-database-elastic-scale-shard-map-management.md) Grup: bir iş gönderilen tootarget parça eşleme olduğunda hello iş parça geçerli kümesini hello parça eşleme toodetermine sorgular ve ardından alt hello parça eşleminde her parça işleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7210f-198">[Shard Map](sql-database-elastic-scale-shard-map-management.md) group: When a job is submitted tootarget a shard map, hello job queries hello shard map toodetermine its current set of shards, and then creates child jobs for each shard in hello shard map.</span></span>
* <span data-ttu-id="7210f-199">Özel Toplama grubu: özel bir veritabanları kümesi tanımlı.</span><span class="sxs-lookup"><span data-stu-id="7210f-199">Custom Collection group: A custom defined set of databases.</span></span> <span data-ttu-id="7210f-200">Bir işi özel bir koleksiyona hedeflediğinde, alt işleri her veritabanı için şu anda hello özel koleksiyonunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7210f-200">When a job targets a custom collection, it creates child jobs for each database currently in hello custom collection.</span></span>

## <a name="tooset-hello-elastic-database-jobs-connection"></a><span data-ttu-id="7210f-201">tooset hello esnek veritabanı iş bağlantısı</span><span class="sxs-lookup"><span data-stu-id="7210f-201">tooset hello Elastic Database jobs connection</span></span>
<span data-ttu-id="7210f-202">Bağlantı toobe kümesi toohello işleri gerekiyor *denetim veritabanı* önceki toousing hello API'leri işler.</span><span class="sxs-lookup"><span data-stu-id="7210f-202">A connection needs toobe set toohello jobs *control database* prior toousing hello jobs APIs.</span></span> <span data-ttu-id="7210f-203">Bu cmdlet'ini çalıştırarak hello kullanıcı adı ve parola esnek veritabanı işleri yüklenirken oluşturulan isteyen oluşturan bir kimlik bilgisi penceresi toopop tetikler.</span><span class="sxs-lookup"><span data-stu-id="7210f-203">Running this cmdlet triggers a credential window toopop up requesting hello user name and password created when installing Elastic Database jobs.</span></span> <span data-ttu-id="7210f-204">Bu konu içinde sağlanan tüm örnekleri bu ilk adımı zaten gerçekleştirilen olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="7210f-204">All examples provided within this topic assume that this first step has already been performed.</span></span>

<span data-ttu-id="7210f-205">Bir bağlantı toohello esnek veritabanı işleri açın:</span><span class="sxs-lookup"><span data-stu-id="7210f-205">Open a connection toohello Elastic Database jobs:</span></span>

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a><span data-ttu-id="7210f-206">Merhaba esnek veritabanı işleri içinde şifrelenmiş kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="7210f-206">Encrypted credentials within hello Elastic Database jobs</span></span>
<span data-ttu-id="7210f-207">Veritabanı kimlik bilgileri hello işlere eklenebilir *denetim veritabanı* şifreli, parola ile.</span><span class="sxs-lookup"><span data-stu-id="7210f-207">Database credentials can be inserted into hello jobs *control database*  with its password encrypted.</span></span> <span data-ttu-id="7210f-208">(İş zamanlamalarını kullanarak) daha sonraki bir zamanda yürütülen gerekli toostore kimlik bilgileri tooenable işleri toobe olur.</span><span class="sxs-lookup"><span data-stu-id="7210f-208">It is necessary toostore credentials tooenable jobs toobe executed at a later time, (using job schedules).</span></span>

<span data-ttu-id="7210f-209">Şifreleme hello yükleme komut dosyasının bir parçası oluşturulan bir sertifika ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="7210f-209">Encryption works through a certificate created as part of hello installation script.</span></span> <span data-ttu-id="7210f-210">Merhaba yükleme betiği oluşturur ve şifrelenmiş parolalar yüklemeleri hello sertifika hello verilerin şifresini çözmek için Azure bulut hizmeti hello içine depolanır.</span><span class="sxs-lookup"><span data-stu-id="7210f-210">hello installation script creates and uploads hello certificate into hello Azure Cloud Service for decryption of hello stored encrypted passwords.</span></span> <span data-ttu-id="7210f-211">Daha sonra Azure bulut hizmeti Hello hello ortak anahtarı hello işleri içinde depolar *denetim veritabanı* hello sertifika gerektirmeden hello PowerShell API'si veya Klasik Azure portalı arabirimi tooencrypt sağlanan parola sağlar yerel olarak yüklenmiş toobe.</span><span class="sxs-lookup"><span data-stu-id="7210f-211">hello Azure Cloud Service later stores hello public key within hello jobs *control database* which enables hello PowerShell API or Azure Classic Portal interface tooencrypt a provided password without requiring hello certificate toobe locally installed.</span></span>

<span data-ttu-id="7210f-212">Merhaba kimlik bilgisi parolaları şifrelenmiş ve salt okunur erişim tooElastic veritabanı işleri nesneleri kullanıcılarla güvenli.</span><span class="sxs-lookup"><span data-stu-id="7210f-212">hello credential passwords are encrypted and secure from users with read-only access tooElastic Database jobs objects.</span></span> <span data-ttu-id="7210f-213">Ancak kötü niyetli bir kullanıcının okuma-yazma erişimi tooElastic veritabanı işlerini nesneleri tooextract bir parola ile mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7210f-213">But it is possible for a malicious user with read-write access tooElastic Database Jobs objects tooextract a password.</span></span> <span data-ttu-id="7210f-214">İş yürütmeleri arasında yeniden tasarlanmış toobe kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="7210f-214">Credentials are designed toobe reused across job executions.</span></span> <span data-ttu-id="7210f-215">Kimlik bilgileri tootarget veritabanları bağlantı kurulurken aktarılır.</span><span class="sxs-lookup"><span data-stu-id="7210f-215">Credentials are passed tootarget databases when establishing connections.</span></span> <span data-ttu-id="7210f-216">Şu anda hello hedef veritabanlarında her kimlik bilgisi için kullanılan bir kısıtlama yoktur, kötü amaçlı kullanıcı hello kötü niyetli bir kullanıcının denetimindeki bir veritabanı için veritabanı hedef ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7210f-216">There are currently no restrictions on hello target databases used for each credential, malicious user could add a database target for a database under hello malicious user's control.</span></span> <span data-ttu-id="7210f-217">Merhaba kullanıcı daha sonra bu veritabanını toogain hello kimlik bilgisi parola hedefleyen bir iş başlayamadı.</span><span class="sxs-lookup"><span data-stu-id="7210f-217">hello user could subsequently start a job targeting this database toogain hello credential's password.</span></span>

<span data-ttu-id="7210f-218">Esnek veritabanı işleri için en iyi yöntemler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7210f-218">Security best practices for Elastic Database jobs include:</span></span>

* <span data-ttu-id="7210f-219">Merhaba API'leri tootrusted kişiler kullanımını sınırlayın.</span><span class="sxs-lookup"><span data-stu-id="7210f-219">Limit usage of hello APIs tootrusted individuals.</span></span>
* <span data-ttu-id="7210f-220">Kimlik bilgileri hello olmalıdır en az ayrıcalık gerekli tooperform hello iş görevi.</span><span class="sxs-lookup"><span data-stu-id="7210f-220">Credentials should have hello least privileges necessary tooperform hello job task.</span></span>  <span data-ttu-id="7210f-221">Daha fazla bilgi bu içinde görülebilir [yetkilendirme ve izinleri](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN makalesi.</span><span class="sxs-lookup"><span data-stu-id="7210f-221">More information can be seen within this [Authorization and Permissions](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN article.</span></span>

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a><span data-ttu-id="7210f-222">toocreate veritabanları arasında iş yürütme için şifrelenmiş bir kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="7210f-222">toocreate an encrypted credential for job execution across databases</span></span>
<span data-ttu-id="7210f-223">Yeni bir şifrelenmiş toocreate kimlik bilgisi, hello [ **Get-Credential cmdlet** ](https://technet.microsoft.com/library/hh849815.aspx) ister bir kullanıcı adı ve toohello geçirilen parolası [ **yeni AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span><span class="sxs-lookup"><span data-stu-id="7210f-223">toocreate a new encrypted credential, hello [**Get-Credential cmdlet**](https://technet.microsoft.com/library/hh849815.aspx) prompts for a user name and password that can be passed toohello [**New-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).</span></span>

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a><span data-ttu-id="7210f-224">tooupdate kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="7210f-224">tooupdate credentials</span></span>
<span data-ttu-id="7210f-225">Parolalar değiştirdiğinizde, hello kullan [ **Set-AzureSqlJobCredential cmdlet'i** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) ve kümesi hello **CredentialName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7210f-225">When passwords change, use hello [**Set-AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) and set hello **CredentialName** parameter.</span></span>

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a><span data-ttu-id="7210f-226">toodefine bir esnek veritabanı parça eşleme hedefi</span><span class="sxs-lookup"><span data-stu-id="7210f-226">toodefine an Elastic Database shard map target</span></span>
<span data-ttu-id="7210f-227">tooexecute parça kümesindeki tüm veritabanlarında bir işi (kullanılarak oluşturulan [esnek veritabanı istemci Kitaplığı](sql-database-elastic-database-client-library.md)), bir parça eşleme hello veritabanı hedefi olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="7210f-227">tooexecute a job against all databases in a shard set (created using [Elastic Database client library](sql-database-elastic-database-client-library.md)), use a shard map as hello database target.</span></span> <span data-ttu-id="7210f-228">Bu örnek hello esnek veritabanı istemci kitaplığı kullanılarak oluşturulmuş bir parçalı uygulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7210f-228">This example requires a sharded application created using hello Elastic Database client library.</span></span> <span data-ttu-id="7210f-229">Bkz: [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7210f-229">See [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

<span data-ttu-id="7210f-230">Hello parça eşleme manager veritabanının veritabanı hedef olarak ayarlanmış olması gerekir ve hello belirli parça eşlemesi hedef olarak belirtildi.</span><span class="sxs-lookup"><span data-stu-id="7210f-230">hello shard map manager database must be set as a database target and then hello specific shard map must be specified as a target.</span></span>

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="7210f-231">Veritabanları arasında yürütme için T-SQL komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7210f-231">Create a T-SQL Script for execution across databases</span></span>
<span data-ttu-id="7210f-232">Yürütme için T-SQL komut dosyalarını oluştururken, toobuild önerilir bunları toobe [ıdempotent](https://en.wikipedia.org/wiki/Idempotence) ve hatalarına karşı dayanıklı.</span><span class="sxs-lookup"><span data-stu-id="7210f-232">When creating T-SQL scripts for execution, it is highly recommended toobuild them toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) and resilient against failures.</span></span> <span data-ttu-id="7210f-233">Esnek veritabanı iş yürütme hello sınıflandırma hello hatanın bağımsız olarak bir hata karşılaştığında bir betik yürütme işlemi yeniden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="7210f-233">Elastic Database jobs will retry execution of a script whenever execution encounters a failure, regardless of hello classification of hello failure.</span></span>

<span data-ttu-id="7210f-234">Kullanım hello [ **yeni AzureSqlJobContent cmdlet** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate yürütme için bir komut dosyasını kaydedin ve ayarlama hello **- ContentName** ve **- CommandText**parametreleri.</span><span class="sxs-lookup"><span data-stu-id="7210f-234">Use hello [**New-AzureSqlJobContent cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate and save a script for execution and set hello **-ContentName** and **-CommandText** parameters.</span></span>

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a><span data-ttu-id="7210f-235">Bir dosyadan yeni bir komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7210f-235">Create a new script from a file</span></span>
<span data-ttu-id="7210f-236">Hello T-SQL komut dosyası içinde tanımlanmış olması durumunda, bu tooimport hello komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="7210f-236">If hello T-SQL script is defined within a file, use this tooimport hello script:</span></span>

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="7210f-237">veritabanları arasında yürütme için tooupdate T-SQL komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7210f-237">tooupdate a T-SQL script for execution across databases</span></span>
<span data-ttu-id="7210f-238">Bu PowerShell Betiği güncelleştirmeleri var olan bir komut dosyası için T-SQL komut metni hello.</span><span class="sxs-lookup"><span data-stu-id="7210f-238">This PowerShell script updates hello T-SQL command text for an existing script.</span></span>

<span data-ttu-id="7210f-239">Değişkenleri tooreflect hello aşağıdaki kümesi hello betik tanım toobe kümesini istenen:</span><span class="sxs-lookup"><span data-stu-id="7210f-239">Set hello following variables tooreflect hello desired script definition toobe set:</span></span>

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a><span data-ttu-id="7210f-240">tooupdate hello tanımı tooan varolan komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7210f-240">tooupdate hello definition tooan existing script</span></span>
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a><span data-ttu-id="7210f-241">toocreate iş tooexecute parça eşleme arasında bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7210f-241">toocreate a job tooexecute a script across a shard map</span></span>
<span data-ttu-id="7210f-242">Bu PowerShell Betiği esnek ölçek parça eşlemesindeki her parça genelinde bir betik yürütme işlemi için bir iş başlatır.</span><span class="sxs-lookup"><span data-stu-id="7210f-242">This PowerShell script starts a job for execution of a script across each shard in an Elastic Scale shard map.</span></span>

<span data-ttu-id="7210f-243">Set hello değişkenleri tooreflect hello aşağıdaki komut dosyası ve hedef istenen:</span><span class="sxs-lookup"><span data-stu-id="7210f-243">Set hello following variables tooreflect hello desired script and target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a><span data-ttu-id="7210f-244">tooexecute bir işi</span><span class="sxs-lookup"><span data-stu-id="7210f-244">tooexecute a job</span></span>
<span data-ttu-id="7210f-245">Bu PowerShell komut dosyası var olan bir işi çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="7210f-245">This PowerShell script executes an existing job:</span></span>

<span data-ttu-id="7210f-246">Değişken tooreflect istenen hello iş adı toohave yürütülen aşağıdaki hello güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="7210f-246">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="7210f-247">tek iş yürütme tooretrieve hello durumu</span><span class="sxs-lookup"><span data-stu-id="7210f-247">tooretrieve hello state of a single job execution</span></span>
<span data-ttu-id="7210f-248">Kullanım hello [ **Get-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) ve kümesi hello **JobExecutionId** parametresi tooview hello iş yürütme durumu.</span><span class="sxs-lookup"><span data-stu-id="7210f-248">Use hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) and set hello **JobExecutionId** parameter tooview hello state of job execution.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

<span data-ttu-id="7210f-249">Kullanım hello aynı **Get-AzureSqlJobExecution** hello cmdlet'iyle **ıncludechildren'ın** parametresi tooview hello alt iş yürütmeleri durumunu öğesine hello her karşı her iş yürütme için belirli bir durumda Merhaba işi tarafından hedef veritabanı.</span><span class="sxs-lookup"><span data-stu-id="7210f-249">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a><span data-ttu-id="7210f-250">birden çok iş yürütmeleri arasında tooview hello durumu</span><span class="sxs-lookup"><span data-stu-id="7210f-250">tooview hello state across multiple job executions</span></span>
<span data-ttu-id="7210f-251">Merhaba [ **Get-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) kullanılan toodisplay olabilecek birden çok isteğe bağlı sağlanan hello parametreleriyle filtre birden çok iş yürütmeleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7210f-251">hello [**Get-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljob) has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="7210f-252">Merhaba aşağıdaki hello olası yolları toouse Get-AzureSqlJobExecution bazılarını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="7210f-252">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="7210f-253">Tüm etkin üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="7210f-253">Retrieve all active top level job executions:</span></span>

    Get-AzureSqlJobExecution

<span data-ttu-id="7210f-254">Etkin olmayan iş yürütmeleri dahil olmak üzere tüm üst düzey iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="7210f-254">Retrieve all top level job executions, including inactive job executions:</span></span>

    Get-AzureSqlJobExecution -IncludeInactive

<span data-ttu-id="7210f-255">Etkin olmayan iş yürütmeleri dahil olmak üzere sağlanan iş yürütme kimliği, tüm alt iş yürütmeleri Al:</span><span class="sxs-lookup"><span data-stu-id="7210f-255">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

<span data-ttu-id="7210f-256">Bir zamanlama kullanılarak oluşturulan tüm iş yürütmeleri almak / birleşimi etkin olmayan işler de dahil olmak üzere, iş:</span><span class="sxs-lookup"><span data-stu-id="7210f-256">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

<span data-ttu-id="7210f-257">Etkin olmayan işler de dahil olmak üzere bir belirtilen parça eşleme hedefleme tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="7210f-257">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="7210f-258">Etkin olmayan işler de dahil olmak üzere belirtilen özel bir koleksiyonu hedefleyen tüm işleri Al:</span><span class="sxs-lookup"><span data-stu-id="7210f-258">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

<span data-ttu-id="7210f-259">Belirli iş yürütme içinde iş görev yürütmeleri Hello listesini al:</span><span class="sxs-lookup"><span data-stu-id="7210f-259">Retrieve hello list of job task executions within a specific job execution:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

<span data-ttu-id="7210f-260">İş görev yürütme ayrıntıları alın:</span><span class="sxs-lookup"><span data-stu-id="7210f-260">Retrieve job task execution details:</span></span>

<span data-ttu-id="7210f-261">PowerShell Betiği aşağıdaki hello kullanılan tooview hello yürütme hatalarını ayıklama özellikle yararlıdır iş görevi yürütmede ayrıntılarını olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-261">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a><span data-ttu-id="7210f-262">iş görevi yürütmeleri içinde tooretrieve hataları</span><span class="sxs-lookup"><span data-stu-id="7210f-262">tooretrieve failures within job task executions</span></span>
<span data-ttu-id="7210f-263">Merhaba **JobTaskExecution nesne** bir ileti özelliği birlikte hello görevinin hello yaşam döngüsü için bir özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="7210f-263">hello **JobTaskExecution object** includes a property for hello lifecycle of hello task along with a message property.</span></span> <span data-ttu-id="7210f-264">Bir iş görevi yürütmede başarısız olursa hello yaşam döngüsü özelliği çok ayarlanacak*başarısız* ve toohello elde edilen özel durum iletisi ve kendi yığını hello ileti özelliği ayarlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="7210f-264">If a job task execution failed, hello lifecycle property will be set too*Failed* and hello message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="7210f-265">Bir işi başarılı olmadı önemli tooview hello için belirli bir işi başarılı olmadı iş görevleri ayrıntılarını olur.</span><span class="sxs-lookup"><span data-stu-id="7210f-265">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a><span data-ttu-id="7210f-266">iş yürütme toocomplete toowait</span><span class="sxs-lookup"><span data-stu-id="7210f-266">toowait for a job execution toocomplete</span></span>
<span data-ttu-id="7210f-267">PowerShell Betiği aşağıdaki hello iş görev toocomplete için kullanılan toowait olabilir:</span><span class="sxs-lookup"><span data-stu-id="7210f-267">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="7210f-268">Özel yürütme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7210f-268">Create a custom execution policy</span></span>
<span data-ttu-id="7210f-269">Esnek veritabanı iş destekler işleri başlatırken uygulanan özel yürütme ilkelerini oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7210f-269">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="7210f-270">Yürütme ilkelerini tanımlamak için şu anda izin ver:</span><span class="sxs-lookup"><span data-stu-id="7210f-270">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="7210f-271">Adı: Merhaba yürütme İlkesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7210f-271">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="7210f-272">İş zaman aşımı: bir iş tarafından esnek veritabanı işi iptal edilecek önce toplam süre.</span><span class="sxs-lookup"><span data-stu-id="7210f-272">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="7210f-273">İlk yeniden deneme aralığı: Aralığı toowait ilk yeniden denemeden önce.</span><span class="sxs-lookup"><span data-stu-id="7210f-273">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="7210f-274">En fazla yeniden deneme aralığı: Yeniden deneme aralıkları toouse Cap.</span><span class="sxs-lookup"><span data-stu-id="7210f-274">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="7210f-275">Yeniden deneme aralığı geri Çekilme katsayısı: Katsayısı toocalculate hello sonraki aralıkta yeniden denemeler arasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7210f-275">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="7210f-276">Merhaba aşağıdaki formül kullanılır: (ilk yeniden deneme aralığı) * Math.pow ((aralığı geri Çekilme katsayısı) (yeniden deneme sayısı) - 2).</span><span class="sxs-lookup"><span data-stu-id="7210f-276">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span> 
* <span data-ttu-id="7210f-277">En fazla deneme: hello sayısının işindeki yeniden deneme girişimleri tooperform.</span><span class="sxs-lookup"><span data-stu-id="7210f-277">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="7210f-278">Merhaba varsayılan yürütme İlkesi hello aşağıdaki değerleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="7210f-278">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="7210f-279">Ad: Varsayılan yürütme İlkesi</span><span class="sxs-lookup"><span data-stu-id="7210f-279">Name: Default execution policy</span></span>
* <span data-ttu-id="7210f-280">İş zaman aşımı: 1 hafta</span><span class="sxs-lookup"><span data-stu-id="7210f-280">Job Timeout: 1 week</span></span>
* <span data-ttu-id="7210f-281">İlk yeniden deneme aralığı: 100 milisaniyede</span><span class="sxs-lookup"><span data-stu-id="7210f-281">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="7210f-282">En fazla yeniden deneme aralığı: 30 dakika</span><span class="sxs-lookup"><span data-stu-id="7210f-282">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="7210f-283">Yeniden deneme aralığı katsayısı: 2</span><span class="sxs-lookup"><span data-stu-id="7210f-283">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="7210f-284">En fazla deneme: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="7210f-284">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="7210f-285">İstenen hello yürütme ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7210f-285">Create hello desired execution policy:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="7210f-286">Özel yürütme ilkesini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="7210f-286">Update a custom execution policy</span></span>
<span data-ttu-id="7210f-287">İstenen hello yürütme İlkesi tooupdate güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="7210f-287">Update hello desired execution policy tooupdate:</span></span>

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a><span data-ttu-id="7210f-288">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="7210f-288">Cancel a job</span></span>
<span data-ttu-id="7210f-289">Esnek veritabanı iş işlerin iptal isteklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="7210f-289">Elastic Database Jobs supports cancellation requests of jobs.</span></span>  <span data-ttu-id="7210f-290">Esnek veritabanı iş şu anda yürütülmekte olan bir işi iptal isteği algılarsa, toostop hello iş deneyecek.</span><span class="sxs-lookup"><span data-stu-id="7210f-290">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="7210f-291">Esnek veritabanı iş iptal gerçekleştirebilirsiniz iki farklı yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="7210f-291">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="7210f-292">Şu anda yürütülmekte olan görevleri iptal: bir görevi şu anda çalışırken iptal algılanırsa, şu anda yürütülmekte olan hello görev yönünü hello içinde iptal denenecek.</span><span class="sxs-lookup"><span data-stu-id="7210f-292">Cancel currently executing tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="7210f-293">Örneğin: iptal çalışırken şu anda gerçekleştirilen uzun süre çalışan bir sorgusu ise, bir deneme toocancel hello sorgu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7210f-293">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="7210f-294">Görev yeniden deneme iptal etme: iptal hello denetimi iş parçacığı tarafından algılanırsa, bir görev için yürütme başlatılmadan önce hello denetimi iş parçacığı hello görev başlatma önlemek ve hello isteği iptal edildi olarak bildirin.</span><span class="sxs-lookup"><span data-stu-id="7210f-294">Canceling task retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="7210f-295">İş iptali için üst iş istediyseniz hello iptal isteği hello üst iş ve tüm alt işlerini uyulacaktır.</span><span class="sxs-lookup"><span data-stu-id="7210f-295">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="7210f-296">toosubmit iptal isteği kullanmak hello [ **Stop-AzureSqlJobExecution cmdlet'i** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) ve kümesi hello **JobExecutionId** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7210f-296">toosubmit a cancellation request, use hello [**Stop-AzureSqlJobExecution cmdlet**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) and set hello **JobExecutionId** parameter.</span></span>

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a><span data-ttu-id="7210f-297">bir iş toodelete ve geçmiş zaman uyumsuz olarak iş</span><span class="sxs-lookup"><span data-stu-id="7210f-297">toodelete a job and job history asynchronously</span></span>
<span data-ttu-id="7210f-298">Esnek veritabanı iş işleri zaman uyumsuz silinmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="7210f-298">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="7210f-299">Bir işi silinmek üzere işaretlenmiş ve tüm iş yürütmeleri için hello işini tamamladıktan sonra hello sistem hello iş ve tüm iş geçmişini siler.</span><span class="sxs-lookup"><span data-stu-id="7210f-299">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="7210f-300">Merhaba sistem etkin iş yürütmeleri otomatik olarak iptal etmek değil.</span><span class="sxs-lookup"><span data-stu-id="7210f-300">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="7210f-301">Çağırma [ **Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel etkin iş yürütmeleri.</span><span class="sxs-lookup"><span data-stu-id="7210f-301">Invoke [**Stop-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel active job executions.</span></span>

<span data-ttu-id="7210f-302">tootrigger iş silme, kullanım hello [ **Kaldır AzureSqlJob cmdlet** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) ve kümesi hello **JobName** parametresi.</span><span class="sxs-lookup"><span data-stu-id="7210f-302">tootrigger job deletion, use hello [**Remove-AzureSqlJob cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljob) and set hello **JobName** parameter.</span></span>

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a><span data-ttu-id="7210f-303">toocreate özel veritabanı hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-303">toocreate a custom database target</span></span>
<span data-ttu-id="7210f-304">Özel veritabanı hedefleri doğrudan yürütme veya eklenmek üzere bir özel veritabanı grubu içinde tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7210f-304">You can define custom database targets either for direct execution or for inclusion within a custom database group.</span></span> <span data-ttu-id="7210f-305">Örneğin, çünkü **esnek havuzlar** olan henüz PowerShell API'lerini kullanarak doğrudan desteklenen, bir özel veritabanı hedef ve hello havuzundaki tüm hello veritabanları kapsayan özel veritabanı koleksiyon hedef oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7210f-305">For example, because **elastic pools** are not yet directly supported using PowerShell APIs, you can create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="7210f-306">Aşağıdaki değişkenleri tooreflect istenen hello veritabanı bilgilerle hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7210f-306">Set hello following variables tooreflect hello desired database information:</span></span>

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a><span data-ttu-id="7210f-307">toocreate özel veritabanı koleksiyon hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-307">toocreate a custom database collection target</span></span>
<span data-ttu-id="7210f-308">Kullanım hello [ **yeni AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine özel veritabanı koleksiyon hedef tooenable yürütme arasında birden çok tanımlanmış veritabanı hedefi.</span><span class="sxs-lookup"><span data-stu-id="7210f-308">Use hello [**New-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine a custom database collection target tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="7210f-309">Bir veritabanı grubu oluşturduktan sonra veritabanları hello özel koleksiyon hedefle ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-309">After creating a database group, databases can be associated with hello custom collection target.</span></span>

<span data-ttu-id="7210f-310">Değişkenleri tooreflect hello istenen özel koleksiyon hedef yapılandırması aşağıdaki hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7210f-310">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="7210f-311">tooadd veritabanları tooa özel veritabanı koleksiyon hedef</span><span class="sxs-lookup"><span data-stu-id="7210f-311">tooadd databases tooa custom database collection target</span></span>
<span data-ttu-id="7210f-312">tooadd veritabanı tooa belirli özel bir koleksiyona kullanmak hello [ **Ekle AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7210f-312">tooadd a database tooa specific custom collection use hello [**Add-AzureSqlJobChildTarget**](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.</span></span>

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="7210f-313">Özel veritabanı koleksiyon hedef içinde Hello veritabanları gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="7210f-313">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="7210f-314">Kullanım hello [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello alt veritabanları özel veritabanı koleksiyon hedef içinde.</span><span class="sxs-lookup"><span data-stu-id="7210f-314">Use hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve hello child databases within a custom database collection target.</span></span> 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="7210f-315">Bir iş tooexecute özel veritabanı koleksiyon hedef arasında bir komut dosyası oluşturun</span><span class="sxs-lookup"><span data-stu-id="7210f-315">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="7210f-316">Kullanım hello [ **yeni AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate özel veritabanı koleksiyon hedef tarafından tanımlanan veritabanlarının bir gruba göre bir işi.</span><span class="sxs-lookup"><span data-stu-id="7210f-316">Use hello [**New-AzureSqlJob**](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="7210f-317">Esnek veritabanı iş karşılık gelen her tooa veritabanı hello özel veritabanı koleksiyon hedefle ilişkili ve hello betik her veritabanına karşı yürütüldüğünden emin olmayı birden çok alt işlere hello iş genişletin.</span><span class="sxs-lookup"><span data-stu-id="7210f-317">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="7210f-318">Yeniden ıdempotent toobe dayanıklı tooretries betiklerdir önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7210f-318">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a><span data-ttu-id="7210f-319">Veritabanları arasında veri toplama</span><span class="sxs-lookup"><span data-stu-id="7210f-319">Data collection across databases</span></span>
<span data-ttu-id="7210f-320">İş tooexecute bir sorgu veritabanları arasında bir grup kullanın ve hello sonuçları tooa belirli tablo gönderin.</span><span class="sxs-lookup"><span data-stu-id="7210f-320">You can use a job tooexecute a query across a group of databases and send hello results tooa specific table.</span></span> <span data-ttu-id="7210f-321">Merhaba tablo, her veritabanı hello olgu toosee hello sorgunun sonuçlarını sonra sorgulanabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-321">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="7210f-322">Bu zaman uyumsuz yöntem tooexecute birçok veritabanı arasında bir sorgu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7210f-322">This provides an asynchronous method tooexecute a query across many databases.</span></span> <span data-ttu-id="7210f-323">Başarısız denemeleri otomatik yeniden denemeler işlenir.</span><span class="sxs-lookup"><span data-stu-id="7210f-323">Failed attempts are handled automatically via retries.</span></span>

<span data-ttu-id="7210f-324">henüz yoksa, hello belirtilen hedef tablo otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7210f-324">hello specified destination table will be automatically created if it does not yet exist.</span></span> <span data-ttu-id="7210f-325">Merhaba yeni tablo sonuç kümesi döndürdü hello hello şeması eşleşir.</span><span class="sxs-lookup"><span data-stu-id="7210f-325">hello new table matches hello schema of hello returned result set.</span></span> <span data-ttu-id="7210f-326">Bir komut dosyası birden çok sonuç kümesi döndürürse, esnek veritabanı işlerini yalnızca hello ilk toohello hedef tablo gönderir.</span><span class="sxs-lookup"><span data-stu-id="7210f-326">If a script returns multiple result sets, Elastic Database jobs will only send hello first toohello destination table.</span></span>

<span data-ttu-id="7210f-327">Merhaba aşağıdaki PowerShell betiğini bir komut dosyası çalıştırır ve sonuçları belirtilen tabloya toplar.</span><span class="sxs-lookup"><span data-stu-id="7210f-327">hello following PowerShell script executes a script and collects its results into a specified table.</span></span> <span data-ttu-id="7210f-328">Bu komut dosyasını bir T-SQL betiği, tek bir sonuç kümesi çıkarır oluşturuldu ve bir özel veritabanı koleksiyon hedef oluşturulduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="7210f-328">This script assumes that a T-SQL script has been created which outputs a single result set and that a custom database collection target has been created.</span></span>

<span data-ttu-id="7210f-329">Bu komut dosyası hello kullanan [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7210f-329">This script uses hello [**Get-AzureSqlJobTarget**](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet.</span></span> <span data-ttu-id="7210f-330">Komut dosyası, kimlik bilgileri ve yürütme hedef Hello parametrelerini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7210f-330">Set hello parameters for script, credentials, and execution target:</span></span>

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="7210f-331">toocreate ve başlangıç bir işi veri toplama senaryoları</span><span class="sxs-lookup"><span data-stu-id="7210f-331">toocreate and start a job for data collection scenarios</span></span>
<span data-ttu-id="7210f-332">Bu komut dosyası hello kullanan [ **başlangıç AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7210f-332">This script uses hello [**Start-AzureSqlJobExecution**](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.</span></span>

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a><span data-ttu-id="7210f-333">tooschedule iş yürütme tetikleyici</span><span class="sxs-lookup"><span data-stu-id="7210f-333">tooschedule a job execution trigger</span></span>
<span data-ttu-id="7210f-334">PowerShell Betiği aşağıdaki hello kullanılan toocreate yinelenen bir zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-334">hello following PowerShell script can be used toocreate a recurring schedule.</span></span> <span data-ttu-id="7210f-335">Bu komut dosyasını bir dakika aralığı kullanır ancak [ **yeni AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) - DayInterval, - HourInterval, - MonthInterval ve - WeekInterval parametreleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="7210f-335">This script uses a minute interval, but [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="7210f-336">Yalnızca bir kez yürütme zamanlamaları oluşturulabilir göre geçirme - kez.</span><span class="sxs-lookup"><span data-stu-id="7210f-336">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="7210f-337">Yeni bir zamanlama oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7210f-337">Create a new schedule:</span></span>

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="7210f-338">tootrigger zaman zamanlamaya göre çalıştırılan bir iş</span><span class="sxs-lookup"><span data-stu-id="7210f-338">tootrigger a job executed on a time schedule</span></span>
<span data-ttu-id="7210f-339">Bir iş Tetikleyici tanımlı toohave yürütülen iş according tooa saat zamanlama olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-339">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="7210f-340">PowerShell Betiği aşağıdaki hello kullanılan toocreate iş tetikleyici olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-340">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="7210f-341">Kullanım [yeni AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) ve kümesi hello aşağıdaki değişkenleri toocorrespond toohello istenen iş ve zamanlaması:</span><span class="sxs-lookup"><span data-stu-id="7210f-341">Use [New-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) and set hello following variables toocorrespond toohello desired job and schedule:</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="7210f-342">tooremove zamanlamaya göre yürütülmesini zamanlanmış ilişkilendirme toostop işi</span><span class="sxs-lookup"><span data-stu-id="7210f-342">tooremove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="7210f-343">iş yürütme iş tetikleyici, hello iş tetikleyici aracılığıyla yinelenmeye toodiscontinue kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-343">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span> <span data-ttu-id="7210f-344">Yürütülmekte olan iş tetikleyici toostop bir işi kaldırma hello kullanarak according tooa zamanlaması [ **Kaldır AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span><span class="sxs-lookup"><span data-stu-id="7210f-344">Remove a job trigger toostop a job from being executed according tooa schedule using hello [**Remove-AzureSqlJobTrigger cmdlet**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).</span></span>

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a><span data-ttu-id="7210f-345">İş Tetikleyicileri ilişkili tooa zamanlama alma</span><span class="sxs-lookup"><span data-stu-id="7210f-345">Retrieve job triggers bound tooa time schedule</span></span>
<span data-ttu-id="7210f-346">PowerShell Betiği aşağıdaki hello kullanılan tooobtain olması ve hello iş Tetikleyicileri kayıtlı tooa belirli zaman planı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7210f-346">hello following PowerShell script can be used tooobtain and display hello job triggers registered tooa particular time schedule.</span></span>

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a><span data-ttu-id="7210f-347">tooretrieve proje Tetikleyicileri ilişkili tooa işi</span><span class="sxs-lookup"><span data-stu-id="7210f-347">tooretrieve job triggers bound tooa job</span></span>
<span data-ttu-id="7210f-348">Kullanım [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) kayıtlı iş içeren tooobtain ve görüntü zamanlamaları.</span><span class="sxs-lookup"><span data-stu-id="7210f-348">Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain and display schedules containing a registered job.</span></span>

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="7210f-349">toocreate veritabanları arasında yürütme için veri katmanı uygulaması (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="7210f-349">toocreate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="7210f-350">toocreate bir DACPAC bkz [veri katmanı uygulamaları](https://msdn.microsoft.com/library/ee210546.aspx).</span><span class="sxs-lookup"><span data-stu-id="7210f-350">toocreate a DACPAC, see [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx).</span></span> <span data-ttu-id="7210f-351">toodeploy bir DACPAC kullanmak hello [yeni AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span><span class="sxs-lookup"><span data-stu-id="7210f-351">toodeploy a DACPAC, use hello [New-AzureSqlJobContent cmdlet](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent).</span></span> <span data-ttu-id="7210f-352">Merhaba DACPAC erişilebilir toohello hizmeti olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7210f-352">hello DACPAC must be accessible toohello service.</span></span> <span data-ttu-id="7210f-353">Bu oluşturmak ve oluşturulan DACPAC tooAzure depolama tooupload önerilen bir [paylaşılan erişim imzası](../storage/common/storage-dotnet-shared-access-signature-part-1.md) hello DACPAC için.</span><span class="sxs-lookup"><span data-stu-id="7210f-353">It is recommended tooupload a created DACPAC tooAzure Storage and create a [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for hello DACPAC.</span></span>

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a><span data-ttu-id="7210f-354">tooupdate veritabanları arasında yürütme için veri katmanı uygulaması (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="7210f-354">tooupdate a data-tier application (DACPAC) for execution across databases</span></span>
<span data-ttu-id="7210f-355">Esnek veritabanı iş içinde kayıtlı varolan DACPACs güncelleştirilmiş toopoint toonew URI'ler olabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-355">Existing DACPACs registered within Elastic Database Jobs can be updated toopoint toonew URIs.</span></span> <span data-ttu-id="7210f-356">Kullanım hello [ **Set-AzureSqlJobContentDefinition cmdlet'i** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) varolan üzerinde tooupdate hello DACPAC URI kayıtlı DACPAC:</span><span class="sxs-lookup"><span data-stu-id="7210f-356">Use hello [**Set-AzureSqlJobContentDefinition cmdlet**](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI on an existing registered DACPAC:</span></span>

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a><span data-ttu-id="7210f-357">toocreate iş tooapply veritabanları arasında veri katmanı uygulaması (DACPAC)</span><span class="sxs-lookup"><span data-stu-id="7210f-357">toocreate a job tooapply a data-tier application (DACPAC) across databases</span></span>
<span data-ttu-id="7210f-358">Esnek veritabanı iş bir DACPAC oluşturulduktan sonra bir iş grubu tooapply hello DACPAC oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="7210f-358">After a DACPAC has been created within Elastic Database Jobs, a job can be created tooapply hello DACPAC across a group of databases.</span></span> <span data-ttu-id="7210f-359">PowerShell Betiği aşağıdaki hello kullanılan toocreate DACPAC iş özel koleksiyonu veritabanları arasında şunlar olabilir:</span><span class="sxs-lookup"><span data-stu-id="7210f-359">hello following PowerShell script can be used toocreate a DACPAC job across a custom collection of databases:</span></span>

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
