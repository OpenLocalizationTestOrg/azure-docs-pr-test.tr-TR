---
title: "Twitter verilerini hdınsight'ta - Azure Hadoop ile aaaAnalyze | Microsoft Docs"
description: "Belirli bir sözcük kullanımı sıklığını toouse Hive tooanalyze Twitter verileri hadoop'ta Hdınsight toofind nasıl hello öğrenin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="e926c-103">Twitter verilerini hdınsight'ta Hive kullanma çözümleme</span><span class="sxs-lookup"><span data-stu-id="e926c-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="e926c-104">Sosyal Web siteleri hello ana yönlendirmeli zorlar, büyük veri benimseme için biridir.</span><span class="sxs-lookup"><span data-stu-id="e926c-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="e926c-105">Twitter gibi siteler tarafından sağlanan ortak API'ler verileri çözümlemek ve popüler eğilimleri anlamak için yararlı bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="e926c-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="e926c-106">Bu öğreticide, API akış Twitter kullanarak tweet'leri alın ve sonra Apache Hive Azure Hdınsight tooget belirli bir sözcük bulunan çoğu tweet'leri hello gönderen Twitter kullanıcıların listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e926c-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e926c-107">Merhaba bu belgedeki adımlar Windows tabanlı Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e926c-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="e926c-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="e926c-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e926c-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e926c-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="e926c-110">Linux tabanlı olan adımları belirli tooa küme için bkz: [(Linux) hdınsight'ta Hive kullanarak Analiz Twitter veri](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e926c-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e926c-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e926c-111">Prerequisites</span></span>
<span data-ttu-id="e926c-112">Bu öğreticiye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e926c-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="e926c-113">**Bir iş istasyonu** Azure yüklenir ve yapılandırılır. PowerShell ile.</span><span class="sxs-lookup"><span data-stu-id="e926c-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="e926c-114">tooexecute Windows PowerShell komut dosyaları, Azure PowerShell'i yönetici olarak çalıştırın ve hello yürütme İlkesi çok ayarlamanız gerekir*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="e926c-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="e926c-115">Bkz: [çalıştırmak Windows PowerShell komut dosyalarını][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="e926c-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="e926c-116">Windows PowerShell komut dosyalarını çalıştırmadan önce aşağıdaki cmdlet'i hello kullanarak bağlı tooyour Azure aboneliği olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e926c-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="e926c-117">Birden çok Azure aboneliğiniz varsa, aşağıdaki cmdlet'i tooset hello geçerli abonelik hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="e926c-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e926c-118">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e926c-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="e926c-119">Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="e926c-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="e926c-120">Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="e926c-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="e926c-121">Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e926c-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="e926c-122">**Azure Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e926c-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="e926c-123">Küme sağlama ile ilgili yönergeler için bkz: [Hdınsight kullanmaya başlama] [ hdinsight-get-started] veya [Hdınsight kümeleri hazırlama][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="e926c-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="e926c-124">Daha sonra hello öğreticide hello küme adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="e926c-125">Merhaba aşağıdaki tabloda Bu öğreticide kullanılan hello dosyaları listeler:</span><span class="sxs-lookup"><span data-stu-id="e926c-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="e926c-126">Dosyalar</span><span class="sxs-lookup"><span data-stu-id="e926c-126">Files</span></span> | <span data-ttu-id="e926c-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e926c-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e926c-128">/Tutorials/twitter/Data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="e926c-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="e926c-129">Merhaba Hive işi için kaynak verilerini Hello.</span><span class="sxs-lookup"><span data-stu-id="e926c-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="e926c-130">/Tutorials/twitter/Output</span><span class="sxs-lookup"><span data-stu-id="e926c-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="e926c-131">Merhaba Hive işi için Hello çıkış klasörü.</span><span class="sxs-lookup"><span data-stu-id="e926c-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="e926c-132">Merhaba varsayılan Hive işi çıkış dosyası adı olan **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="e926c-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="e926c-133">Tutorials/twitter/twitter.hql</span><span class="sxs-lookup"><span data-stu-id="e926c-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="e926c-134">Merhaba HiveQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e926c-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="e926c-135">/Tutorials/twitter/JobStatus</span><span class="sxs-lookup"><span data-stu-id="e926c-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="e926c-136">Merhaba Hadoop iş durumu.</span><span class="sxs-lookup"><span data-stu-id="e926c-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="e926c-137">Get Twitter akışı</span><span class="sxs-lookup"><span data-stu-id="e926c-137">Get Twitter feed</span></span>
<span data-ttu-id="e926c-138">Bu öğreticide, hello kullanacağı [API'leri akış Twitter][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="e926c-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="e926c-139">Merhaba kullanacağınız API akış belirli Twitter olan [durumları/filtre][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="e926c-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="e926c-140">10.000 tweet'leri ve hello Hive betik dosyası (Merhaba sonraki bölümde yer alan) içeren bir dosyayı yüklediğiniz bir ortak Blob kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="e926c-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="e926c-141">Toouse hello karşıya yüklenen dosyaların istiyorsanız bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e926c-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="e926c-142">[Tweet'leri veri](https://dev.twitter.com/docs/platform-objects/tweets) karmaşık bir iç içe geçmiş yapısının hello JavaScript nesne gösterimi (JSON) biçiminde depolanır.</span><span class="sxs-lookup"><span data-stu-id="e926c-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="e926c-143">Böylece bir yapılandırılmış sorgu dili (SQL) tarafından sorgulanabilir geleneksel bir programlama dili kullanarak kod satır sayısını yazmak yerine, iç içe geçmiş bu yapı bir Hive tabloya dönüştürebilirsiniz-HiveQL adında dil ister.</span><span class="sxs-lookup"><span data-stu-id="e926c-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="e926c-144">Twitter OAuth yetkili tooprovide erişim tooits API'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e926c-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="e926c-145">OAuth parolalarını paylaşmadan onların adına kullanıcılar tooapprove uygulamaları tooact sağlayan bir kimlik doğrulama protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="e926c-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="e926c-146">Daha fazla bilgi bulunabilir [oauth.net](http://oauth.net/) veya hello mükemmel [Başlangıç Kılavuzu tooOAuth](http://hueniverse.com/oauth/) Hueniverse gelen.</span><span class="sxs-lookup"><span data-stu-id="e926c-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="e926c-147">Merhaba ilk adım toouse OAuth toocreate hello Twitter Developer sitesinde yeni bir uygulama olur.</span><span class="sxs-lookup"><span data-stu-id="e926c-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="e926c-148">**toocreate Twitter uygulama**</span><span class="sxs-lookup"><span data-stu-id="e926c-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="e926c-149">Çok oturum[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="e926c-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="e926c-150">Merhaba tıklatın **şimdi kaydolun** bir Twitter hesabı yoksa bağlantı.</span><span class="sxs-lookup"><span data-stu-id="e926c-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="e926c-151">Tıklatın **yeni uygulama oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e926c-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="e926c-152">Girin **adı**, **açıklama**, **Web sitesi**.</span><span class="sxs-lookup"><span data-stu-id="e926c-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="e926c-153">Hello için bir URL yukarı yapabileceğiniz **Web sitesi** alan.</span><span class="sxs-lookup"><span data-stu-id="e926c-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="e926c-154">Aşağıdaki tablonun hello bazı örnek değerleri toouse gösterir:</span><span class="sxs-lookup"><span data-stu-id="e926c-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="e926c-155">Alan</span><span class="sxs-lookup"><span data-stu-id="e926c-155">Field</span></span> | <span data-ttu-id="e926c-156">Değer</span><span class="sxs-lookup"><span data-stu-id="e926c-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="e926c-157">Ad</span><span class="sxs-lookup"><span data-stu-id="e926c-157">Name</span></span> |<span data-ttu-id="e926c-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="e926c-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="e926c-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e926c-159">Description</span></span> |<span data-ttu-id="e926c-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="e926c-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="e926c-161">Web sitesi</span><span class="sxs-lookup"><span data-stu-id="e926c-161">Website</span></span> |<span data-ttu-id="e926c-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="e926c-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="e926c-163">Denetleme **Evet, kabul ediyorum**ve ardından **Twitter uygulamanızı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e926c-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="e926c-164">Merhaba tıklatın **izinleri** sekmesini hello varsayılan izni **salt okunur**.</span><span class="sxs-lookup"><span data-stu-id="e926c-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="e926c-165">Bu öğretici için yeterli olur.</span><span class="sxs-lookup"><span data-stu-id="e926c-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="e926c-166">Merhaba tıklatın **anahtarları ve erişim belirteçleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e926c-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="e926c-167">Tıklatın **my erişim belirteci oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e926c-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="e926c-168">Tıklatın **Test OAuth** hello sayfasının hello sağ üst köşesindeki.</span><span class="sxs-lookup"><span data-stu-id="e926c-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="e926c-169">Yazma **tüketici anahtarı**, **tüketici gizli**, **erişim belirteci**, ve **erişim belirteci gizli anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="e926c-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="e926c-170">Daha sonra hello öğreticide hello değerleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="e926c-171">Bu öğreticide, Windows PowerShell toomake hello web hizmeti çağrısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e926c-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="e926c-172">Bir .NET C# örnek için bkz: [hdınsight'ta HBase ile gerçek zamanlı Twitter düşüncelerini çözümleme][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="e926c-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="e926c-173">Merhaba diğer popüler araç toomake web hizmeti çağrıları olan [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="e926c-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="e926c-174">Curl adresinden yüklenebilir [burada][curl-download].</span><span class="sxs-lookup"><span data-stu-id="e926c-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="e926c-175">Windows hello curl komutunu kullandığınızda, çift tırnak işareti yerine tek tırnak hello seçeneği değerleri için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e926c-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="e926c-176">**tooget tweet'leri**</span><span class="sxs-lookup"><span data-stu-id="e926c-176">**tooget tweets**</span></span>

1. <span data-ttu-id="e926c-177">Merhaba Windows PowerShell Tümleşik komut dosyası ortamı (ISE) açın.</span><span class="sxs-lookup"><span data-stu-id="e926c-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="e926c-178">(Merhaba Windows 8 Başlat ekranında, yazın **PowerShell_ISE** ve ardından **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="e926c-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="e926c-179">Bkz: [başlangıç Windows 8'de Windows PowerShell ve Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="e926c-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="e926c-180">Komut dosyası hello betik bölmesine aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="e926c-180">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="e926c-181">Merhaba ilk beş tooeight değişkenleri hello komut dosyasında ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e926c-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="e926c-182">Değişken</span><span class="sxs-lookup"><span data-stu-id="e926c-182">Variable</span></span>|<span data-ttu-id="e926c-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e926c-183">Description</span></span>
    ---|---
    <span data-ttu-id="e926c-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="e926c-184">$clusterName</span></span>|<span data-ttu-id="e926c-185">Bu hello toorun Merhaba uygulaması istediğiniz hello Hdınsight küme adıdır.</span><span class="sxs-lookup"><span data-stu-id="e926c-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="e926c-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="e926c-186">$oauth_consumer_key</span></span>|<span data-ttu-id="e926c-187">Merhaba Twitter uygulaması budur **tüketici anahtarı** Merhaba Twitter uygulaması oluşturduğunuzda, daha önce yazdığınız.</span><span class="sxs-lookup"><span data-stu-id="e926c-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="e926c-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="e926c-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="e926c-189">Merhaba Twitter uygulaması budur **tüketici gizli** daha önce yazmış.</span><span class="sxs-lookup"><span data-stu-id="e926c-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="e926c-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="e926c-190">$oauth_token</span></span>|<span data-ttu-id="e926c-191">Merhaba Twitter uygulaması budur **erişim belirteci** daha önce yazmış.</span><span class="sxs-lookup"><span data-stu-id="e926c-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="e926c-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="e926c-192">$oauth_token_secret</span></span>|<span data-ttu-id="e926c-193">Merhaba Twitter uygulaması budur **erişim belirteci gizli anahtarı** daha önce yazmış.</span><span class="sxs-lookup"><span data-stu-id="e926c-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="e926c-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="e926c-194">$destBlobName</span></span>|<span data-ttu-id="e926c-195">Merhaba çıkış blob adı budur.</span><span class="sxs-lookup"><span data-stu-id="e926c-195">This is hello output blob name.</span></span> <span data-ttu-id="e926c-196">Merhaba varsayılan değer **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="e926c-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="e926c-197">Merhaba varsayılan değeri değiştirirseniz, tooupdate hello Windows PowerShell komut dosyaları uygun şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="e926c-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="e926c-198">$trackString</span></span>|<span data-ttu-id="e926c-199">Merhaba web hizmeti tweet'leri ilgili toothese anahtar sözcükleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="e926c-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="e926c-200">Merhaba varsayılan değer **Azure, bulut, Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="e926c-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="e926c-201">Merhaba varsayılan değeri değiştirirseniz, hello Windows PowerShell komut dosyaları uygun şekilde güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e926c-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="e926c-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="e926c-202">$lineMax</span></span>|<span data-ttu-id="e926c-203">kaç tane tweet'leri hello betik okuma yapacak Hello değeri belirler.</span><span class="sxs-lookup"><span data-stu-id="e926c-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="e926c-204">100 tweet'leri tooread yaklaşık üç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="e926c-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="e926c-205">Daha büyük bir sayı oluşturabilirsiniz ancak daha fazla zaman toodownload olur.</span><span class="sxs-lookup"><span data-stu-id="e926c-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="e926c-206">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e926c-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="e926c-207">Geçici bir çözüm olarak sorunlarla karşılaşırsanız, tüm hello satırları seçin ve sonra basın **F8**.</span><span class="sxs-lookup"><span data-stu-id="e926c-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="e926c-208">"Tam!" göreceksiniz</span><span class="sxs-lookup"><span data-stu-id="e926c-208">You shall see "Complete!"</span></span> <span data-ttu-id="e926c-209">Merhaba Çıktı Hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="e926c-209">at hello end of hello output.</span></span> <span data-ttu-id="e926c-210">Kırmızı olarak herhangi bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e926c-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="e926c-211">Doğrulama yordamı hello çıktı dosyasını kontrol edebilirsiniz **/tutorials/twitter/data/tweets.txt**, bir Azure Depolama Gezgini veya Azure PowerShell kullanarak Azure Blob Depolama alanınızın üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e926c-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="e926c-212">Örnek Windows PowerShell komut dosyaları listeleme için bkz: [kullanım Blob storage Hdınsight ile][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="e926c-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="e926c-213">HiveQL komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e926c-213">Create HiveQL script</span></span>
<span data-ttu-id="e926c-214">Azure PowerShell kullanarak, birden çok HiveQL ifadelerini tek bir saat veya paket hello HiveQL deyimi bir komut dosyasına çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e926c-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="e926c-215">Bu öğreticide, HiveQL betiğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e926c-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="e926c-216">Merhaba komut dosyasını karşıya yüklenen tooAzure Blob Depolama olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="e926c-217">Merhaba sonraki bölümde, Azure PowerShell kullanarak hello komut dosyası çalışır.</span><span class="sxs-lookup"><span data-stu-id="e926c-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e926c-218">bir ortak Blob kapsayıcısında Hello Hive betik dosyası ve 10.000 tweet'leri içeren bir dosyayı karşıya yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="e926c-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="e926c-219">Toouse hello karşıya yüklenen dosyaların istiyorsanız bu bölümü atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e926c-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="e926c-220">Merhaba HiveQL betiğini hello aşağıdakileri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="e926c-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="e926c-221">**Merhaba tweets_raw tablo bırakma** hello tablo zaten mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="e926c-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="e926c-222">**Merhaba tweets_raw Hive tablosu oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="e926c-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="e926c-223">Bu geçici Hive yapılandırılmış tablosu için daha fazla extract hello verileri tutar, dönüştürme ve yükleme (ETL) işleme.</span><span class="sxs-lookup"><span data-stu-id="e926c-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="e926c-224">Bölümleri hakkında daha fazla bilgi için bkz: [Hive öğretici][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="e926c-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="e926c-225">**Veri yükleme** hello kaynak klasörden /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="e926c-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="e926c-226">iç içe geçmiş JSON biçiminde Hello büyük tweet'leri dataset geçici bir Hive tablosu yapısına şimdi dönüştürdü.</span><span class="sxs-lookup"><span data-stu-id="e926c-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="e926c-227">**Açılan hello tweet'leri tablo** hello tablo zaten mevcut durumda.</span><span class="sxs-lookup"><span data-stu-id="e926c-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="e926c-228">**Merhaba tweet'leri tablosu oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="e926c-228">**Create hello tweets table**.</span></span> <span data-ttu-id="e926c-229">Merhaba tweet'leri dataset karşı Hive kullanarak sorgulama yapabilirsiniz önce başka bir ETL işlemi toorun gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="e926c-230">Bu ETL işlemi hello "twitter_raw" tablosunda depolanan hello veriler için daha ayrıntılı bir tablo şemasını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e926c-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="e926c-231">**Üzerine yaz tablo ekleme**.</span><span class="sxs-lookup"><span data-stu-id="e926c-231">**Insert overwrite table**.</span></span> <span data-ttu-id="e926c-232">Bu karmaşık Hive betiğini uzun MapReduce işleri bir dizi hello Hadoop küme tarafından tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="e926c-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="e926c-233">Veri kümesi ve hello boyutunuz kümenizin bağlı olarak, bu yaklaşık 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e926c-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="e926c-234">**INSERT üzerine dizin**.</span><span class="sxs-lookup"><span data-stu-id="e926c-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="e926c-235">Sorgu ve çıktı hello dataset tooa dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e926c-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="e926c-236">Bu sorgu "Azure" Merhaba sözcüğünü içeren çoğu tweet'leri gönderen Twitter kullanıcıların bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="e926c-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="e926c-237">**toocreate bir Hive betiği ve tooAzure yükleyin**</span><span class="sxs-lookup"><span data-stu-id="e926c-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="e926c-238">Windows PowerShell ISE açın.</span><span class="sxs-lookup"><span data-stu-id="e926c-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="e926c-239">Komut dosyası hello betik bölmesine aşağıdaki hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="e926c-239">Copy hello following script into hello script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="e926c-240">Merhaba ilk iki değişkenleri hello komut dosyasında ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="e926c-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="e926c-241">Değişken</span><span class="sxs-lookup"><span data-stu-id="e926c-241">Variable</span></span> | <span data-ttu-id="e926c-242">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e926c-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="e926c-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="e926c-243">$clusterName</span></span> |<span data-ttu-id="e926c-244">Toorun Merhaba uygulaması istediğiniz Hello Hdınsight küme adı girin.</span><span class="sxs-lookup"><span data-stu-id="e926c-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="e926c-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="e926c-245">$subscriptionID</span></span> |<span data-ttu-id="e926c-246">Azure abonelik kimliğinizi girin</span><span class="sxs-lookup"><span data-stu-id="e926c-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="e926c-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="e926c-247">$sourceDataPath</span></span> |<span data-ttu-id="e926c-248">Hello Azure Blob Depolama konumu hello Hive sorguları hello verileri nerede okur.</span><span class="sxs-lookup"><span data-stu-id="e926c-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="e926c-249">Bu değişken toochange gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e926c-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="e926c-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="e926c-250">$outputPath</span></span> |<span data-ttu-id="e926c-251">Hello Azure Blob Depolama konumu hello sonuçları hello Hive sorguları yeri çıkarır.</span><span class="sxs-lookup"><span data-stu-id="e926c-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="e926c-252">Bu değişken toochange gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e926c-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="e926c-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="e926c-253">$hqlScriptFile</span></span> |<span data-ttu-id="e926c-254">Başlangıç konumu ve hello hello HiveQL komut dosyasının dosya adı.</span><span class="sxs-lookup"><span data-stu-id="e926c-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="e926c-255">Bu değişken toochange gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="e926c-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="e926c-256">Tuşuna **F5** toorun hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e926c-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="e926c-257">Geçici bir çözüm olarak sorunlarla karşılaşırsanız, tüm hello satırları seçin ve sonra basın **F8**.</span><span class="sxs-lookup"><span data-stu-id="e926c-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="e926c-258">"Tam!" göreceksiniz</span><span class="sxs-lookup"><span data-stu-id="e926c-258">You shall see "Complete!"</span></span> <span data-ttu-id="e926c-259">Merhaba Çıktı Hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="e926c-259">at hello end of hello output.</span></span> <span data-ttu-id="e926c-260">Kırmızı olarak herhangi bir hata iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e926c-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="e926c-261">Doğrulama yordamı hello çıktı dosyasını kontrol edebilirsiniz **/tutorials/twitter/twitter.hql**, bir Azure Depolama Gezgini veya Azure PowerShell kullanarak Azure Blob Depolama alanınızın üzerinde.</span><span class="sxs-lookup"><span data-stu-id="e926c-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="e926c-262">Örnek Windows PowerShell komut dosyaları listeleme için bkz: [kullanım Blob storage Hdınsight ile][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="e926c-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="e926c-263">Hive kullanarak twitter verilerini işlemek</span><span class="sxs-lookup"><span data-stu-id="e926c-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="e926c-264">Tüm hello hazırlık çalışması tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="e926c-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="e926c-265">Şimdi, hello Hive betiğini çağırma ve hello sonuçlarını kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="e926c-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="e926c-266">Hive işi gönderin</span><span class="sxs-lookup"><span data-stu-id="e926c-266">Submit a Hive job</span></span>
<span data-ttu-id="e926c-267">Windows PowerShell komut dosyası toorun hello Hive betiğini aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="e926c-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="e926c-268">Tooset hello ilk değişken gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="e926c-269">toouse hello tweet'leri ve HiveQL betiğini hello son iki bölümlerde, kümesi $hqlScriptFile too"/tutorials/twitter/twitter.hql karşıya hello".</span><span class="sxs-lookup"><span data-stu-id="e926c-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="e926c-270">toouse hello kaldırılmış olanları karşıya tooa ortak blob sizin için $hqlScriptFile çok Ayarla"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span><span class="sxs-lookup"><span data-stu-id="e926c-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a><span data-ttu-id="e926c-271">Merhaba sonuçları denetleyin</span><span class="sxs-lookup"><span data-stu-id="e926c-271">Check hello results</span></span>
<span data-ttu-id="e926c-272">Windows PowerShell komut dosyası toocheck hello Hive iş çıktısı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="e926c-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="e926c-273">Tooset hello ilk iki değişkenleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="e926c-273">You will need tooset hello first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Merhaba Hive tablosu \001 alan sınırlayıcı hello gibi kullanır. <span data-ttu-id="e926c-275">Merhaba sınırlayıcı hello çıkışında görünür değil.</span><span class="sxs-lookup"><span data-stu-id="e926c-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="e926c-276">Merhaba çözümleme sonuçlarını Azure Blob depolama alanına yerleştirildi sonra verme hello veri tooan Azure SQL veritabanı/SQL sunucusu, Power Query kullanarak hello veri tooExcel dışarı veya hello Hive ODBC sürücüsü kullanarak uygulama toohello verilerinize bağlanın.</span><span class="sxs-lookup"><span data-stu-id="e926c-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="e926c-277">Daha fazla bilgi için bkz: [Hdınsight ile kullanım Sqoop][hdinsight-use-sqoop], [Hdınsight kullanarak uçuş gecikme verileri analiz][hdinsight-analyze-flight-delay-data], [ Power Query ile Excel tooHDInsight bağlanmak][hdinsight-power-query], ve [hello Microsoft Hive ODBC sürücüsü ile bağlanma Excel tooHDInsight][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="e926c-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e926c-278">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e926c-278">Next steps</span></span>
<span data-ttu-id="e926c-279">Bu öğreticide biz nasıl tootransform yapılandırılmamış bir JSON veri kümesi içinde yapılandırılmış bir Hive tablosu tooquery keşfedin ve Twitter verilerini Azure üzerinde Hdınsight kullanarak çözümlemek gördünüz.</span><span class="sxs-lookup"><span data-stu-id="e926c-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="e926c-280">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="e926c-280">toolearn more, see:</span></span>

* <span data-ttu-id="e926c-281">[Hdınsight kullanmaya başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e926c-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="e926c-282">[Hdınsight'ta HBase ile gerçek zamanlı Twitter düşüncelerini çözümleme][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="e926c-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="e926c-283">[Hdınsight kullanma uçuş gecikme verilerini çözümleme][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="e926c-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="e926c-284">[Excel tooHDInsight Power Query ile bağlanma][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="e926c-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="e926c-285">[Excel tooHDInsight hello Microsoft Hive ODBC sürücüsü ile bağlanma][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="e926c-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="e926c-286">[Hdınsight ile Sqoop kullanma][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="e926c-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
