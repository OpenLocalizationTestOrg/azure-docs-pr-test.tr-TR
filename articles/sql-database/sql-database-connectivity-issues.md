---
title: "aaaFix SQL bağlantı hatası, geçici hata | Microsoft Docs"
description: "Nasıl tootroubleshoot, tanılama ve SQL bağlantı hatası veya Azure SQL veritabanındaki geçici hata önlemek öğrenin. "
keywords: "SQL bağlantısı, bağlantı dizesi, bağlantı sorunları, geçici bir hata oluştu, bağlantı hatası"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="8313d-104">SQL Database için SQL bağlantı hatalarını ve geçici hataları giderme, tanılama ve önleme</span><span class="sxs-lookup"><span data-stu-id="8313d-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="8313d-105">Bu makalede nasıl tooprevent, sorun giderme, tanılama ve bağlantı hataları ve Azure SQL veritabanı ile etkileşim kurarken, istemci uygulamanız karşılaştığında geçici hataları etkisini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8313d-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="8313d-106">Nasıl tooconfigure mantığı yeniden dene, hello bağlantı dizesi oluşturma ve diğer bağlantı ayarlarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8313d-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="8313d-107">Geçici hataları geçici</span><span class="sxs-lookup"><span data-stu-id="8313d-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="8313d-108">Geçici bir hata - Ayrıca, geçici hata - kendisini yakında çözümleyecek bir temel nedeni vardır.</span><span class="sxs-lookup"><span data-stu-id="8313d-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="8313d-109">Hello Azure sistem çeşitli iş yükleri donanım kaynakları toobetter Yük Dengelemesi hızla geçtiğinde geçici hataları zaman zaman bir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="8313d-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="8313d-110">Bu yeniden yapılandırma olayları çoğunu genellikle 60 saniyeden daha kısa bir süre içinde tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="8313d-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="8313d-111">Bu yeniden yapılandırma zaman aralığı sırasında bağlantısına sahip olabilir tooAzure SQL veritabanı verir.</span><span class="sxs-lookup"><span data-stu-id="8313d-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="8313d-112">SQL veritabanı olmalıdır tooAzure bağlanan uygulamaları yerleşik tooexpect bu geçici hataları işleme mantığı toousers uygulama hataları olarak görünmesini yerine kendi kodunda bunları uygulayarak yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="8313d-113">İstemci programınız ADO.NET kullanıyorsanız, programınız tarafından hello throw hello geçici hata hakkında işe bir **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="8313d-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="8313d-114">Merhaba **numarası** özelliği, geçici hataları hello konunun hello üstüne yakın hello listesi karşı karşılaştırılabilir: [SQL Database istemci uygulamaları için SQL hata kodları](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="8313d-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="8313d-115">Bağlantı komutu karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="8313d-115">Connection versus command</span></span>
<span data-ttu-id="8313d-116">Merhaba SQL bağlantısı yeniden deneyin veya hello aşağıdaki bağlı olarak yeniden kurmak:</span><span class="sxs-lookup"><span data-stu-id="8313d-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="8313d-117">**Bir bağlantı try sırasında geçici bir hata oluşur**: hello bağlantı yeniden geciktirme birkaç saniye sonra.</span><span class="sxs-lookup"><span data-stu-id="8313d-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="8313d-118">**Bir SQL sorgu komutu sırasında geçici bir hata oluşur**: hello komutu değil hemen yeniden.</span><span class="sxs-lookup"><span data-stu-id="8313d-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="8313d-119">Bunun yerine, bir gecikmeden sonra hello bağlantı istemcinin yeniden kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8313d-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="8313d-120">Ardından hello komutu yeniden denenebilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="8313d-121">Geçici hatalar için yeniden deneme mantığı</span><span class="sxs-lookup"><span data-stu-id="8313d-121">Retry logic for transient errors</span></span>
<span data-ttu-id="8313d-122">Yeniden deneme mantığı içerdiğinde bazen geçici bir hatayla karşılaşırsanız istemci programları daha sağlamdır.</span><span class="sxs-lookup"><span data-stu-id="8313d-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="8313d-123">Programınızı 3 bir taraf ara yazılımı Azure SQL veritabanı ile iletişim kurduğunda, geçici hataları yeniden deneme mantığı hello Ara içerip içermediğini hello satıcıyla sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="8313d-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="8313d-124">Yeniden deneme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="8313d-124">Principles for retry</span></span>
* <span data-ttu-id="8313d-125">Merhaba geçici bir hatadır, bir bağlantı girişimi tooopen denenmeli.</span><span class="sxs-lookup"><span data-stu-id="8313d-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="8313d-126">Geçici bir hata ile başarısız olan bir SQL SELECT deyimi doğrudan denenmeli değil.</span><span class="sxs-lookup"><span data-stu-id="8313d-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="8313d-127">Bunun yerine, yeni bir bağlantı kurmak ve hello seçin yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="8313d-128">Bir SQL UPDATE deyimi geçici bir hata ile başarısız olduğunda, güncelleştirme denenen hello önce yeni bir bağlantı kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8313d-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="8313d-129">Merhaba yeniden deneme mantığı hello tüm veritabanı işlem tamamlandı ya da bu hello işlemin tamamını geri alınır emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8313d-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="8313d-130">Yeniden deneme ile diğer değerlendirmeler</span><span class="sxs-lookup"><span data-stu-id="8313d-130">Other considerations for retry</span></span>
* <span data-ttu-id="8313d-131">Çalışma saatlerinden sonra otomatik olarak başlatılır ve sabah önce tamamlanır toplu iş programı toovery hasta uzun zaman aralıklarına kendi yeniden deneme girişimleri arasındaki ile destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="8313d-132">Bir kullanıcı arabirimi programı hello İnsan eğilimi toogive için yukarı sonra çok uzun bekleme hesabı.</span><span class="sxs-lookup"><span data-stu-id="8313d-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="8313d-133">Ancak, bu ilkeyi istekleri hello sistemiyle bölgesini doldurmak için hello çözüm tooretry her birkaç saniyede olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="8313d-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="8313d-134">Denemeler arasındaki aralığı artırma</span><span class="sxs-lookup"><span data-stu-id="8313d-134">Interval increase between retries</span></span>
<span data-ttu-id="8313d-135">İlk, yeniden denemeden önce 5 saniye gecikme öneririz.</span><span class="sxs-lookup"><span data-stu-id="8313d-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="8313d-136">5 saniyeden daha kısa bir gecikme sonrasında yeniden deneniyor zorlamayı hello bulut hizmeti risklerini.</span><span class="sxs-lookup"><span data-stu-id="8313d-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="8313d-137">Sonraki denemeler hello gecikme katlanarak, tooa 60 saniye olarak en fazla büyümesini.</span><span class="sxs-lookup"><span data-stu-id="8313d-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="8313d-138">Merhaba tartışması *engelleme süresi* ADO.NET kullanan istemciler için kullanılabilir [SQL Server bağlantı havuzu (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="8313d-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="8313d-139">Merhaba programı otomatik olarak kapatılmadan önce tooset bir yeniden deneme sayısı da isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8313d-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="8313d-140">Yeniden deneme mantığı ile kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="8313d-140">Code samples with retry logic</span></span>
<span data-ttu-id="8313d-141">Kod örnekleri programlama dilleri, çeşitli yeniden deneme mantığı ile şu konumda mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="8313d-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="8313d-142">SQL Database ve SQL Server için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="8313d-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="8313d-143">Yeniden deneme mantığı test</span><span class="sxs-lookup"><span data-stu-id="8313d-143">Test your retry logic</span></span>
<span data-ttu-id="8313d-144">tootest, yeniden deneme mantığı benzetimini yapmak veya gerekir programınızı çalışmaya devam ederken düzeltilebilir daha hataya neden.</span><span class="sxs-lookup"><span data-stu-id="8313d-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="8313d-145">Merhaba ağ bağlantısını keserek test</span><span class="sxs-lookup"><span data-stu-id="8313d-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="8313d-146">Yeniden deneme mantığı sınayabilirsiniz bir hello istemci bilgisayarından ağ hello program çalışırken toodisconnect yoludur.</span><span class="sxs-lookup"><span data-stu-id="8313d-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="8313d-147">Merhaba hata olacaktır:</span><span class="sxs-lookup"><span data-stu-id="8313d-147">hello error will be:</span></span>

* <span data-ttu-id="8313d-148">**SqlException.Number** 11001 =</span><span class="sxs-lookup"><span data-stu-id="8313d-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="8313d-149">İleti: "gibi bir ana makine bilinmiyor"</span><span class="sxs-lookup"><span data-stu-id="8313d-149">Message: "No such host is known"</span></span>

<span data-ttu-id="8313d-150">Merhaba parçası ilk yeniden deneme girişimi gibi programınızı hello yazım hatası düzeltin ve tooconnect dener.</span><span class="sxs-lookup"><span data-stu-id="8313d-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="8313d-151">programınızı başlamadan önce bu pratik toomake, hello ağ bilgisayarınızdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="8313d-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="8313d-152">Ardından, programı hello programına neden olan bir çalışma zamanı parametre tanır:</span><span class="sxs-lookup"><span data-stu-id="8313d-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="8313d-153">Geçici hatalar tooconsider 11001 tooits listesi geçici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="8313d-154">İlk bağlantı her zamanki gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="8313d-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="8313d-155">Merhaba hata belirledi sonra 11001 hello listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8313d-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="8313d-156">Merhaba kullanıcı tooplug hello bilgisayar hello ağınıza anlatan bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8313d-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="8313d-157">Daha fazla yürütme ya da hello kullanarak duraklatmak **Console.ReadLine** yöntemi veya bir iletişim kutusunda Tamam düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8313d-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="8313d-158">Merhaba bilgisayar hello ağa takılı sonra hello kullanıcı hello Enter tuşuna basar.</span><span class="sxs-lookup"><span data-stu-id="8313d-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="8313d-159">Başarı bekleniyor tooconnect, yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="8313d-160">Bağlanırken yazım hatası hello veritabanı adına göre test etme</span><span class="sxs-lookup"><span data-stu-id="8313d-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="8313d-161">Programınızı kasıtlı olarak, hata hello ilk bağlantı denemesine önce hello kullanıcı adı hatalı.</span><span class="sxs-lookup"><span data-stu-id="8313d-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="8313d-162">Merhaba hata olacaktır:</span><span class="sxs-lookup"><span data-stu-id="8313d-162">hello error will be:</span></span>

* <span data-ttu-id="8313d-163">**SqlException.Number** 18456 =</span><span class="sxs-lookup"><span data-stu-id="8313d-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="8313d-164">İleti: "'WRONG_MyUserName' kullanıcı için oturum açma başarısız."</span><span class="sxs-lookup"><span data-stu-id="8313d-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="8313d-165">Merhaba parçası ilk yeniden deneme girişimi gibi programınızı hello yazım hatası düzeltin ve tooconnect dener.</span><span class="sxs-lookup"><span data-stu-id="8313d-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="8313d-166">Bu pratik toomake, programınızı hello programına neden olan bir çalışma zamanı parametre tanı:</span><span class="sxs-lookup"><span data-stu-id="8313d-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="8313d-167">Geçici hatalar tooconsider 18456 tooits listesi geçici ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="8313d-168">Kasıtlı olarak 'WRONG_' toohello kullanıcı adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="8313d-169">Merhaba hata belirledi sonra 18456 hello listesinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="8313d-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="8313d-170">'WRONG_' hello kullanıcı adından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8313d-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="8313d-171">Başarı bekleniyor tooconnect, yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="8313d-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="8313d-172">Bağlantı yeniden deneme için .NET SqlConnection parametreleri</span><span class="sxs-lookup"><span data-stu-id="8313d-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="8313d-173">İstemci programınız tootooAzure SQL veritabanı hello .NET Framework sınıf kullanarak bağlanıyorsa **System.Data.SqlClient.SqlConnection**, .NET 4.6.1 kullanması gereken veya daha sonra (veya .NET Core), bağlantı yeniden deneme özelliğinden yararlanabilirsiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="8313d-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="8313d-174">Merhaba özelliğinin ayrıntıları [burada](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="8313d-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="8313d-175">Merhaba oluşturduğunuzda [bağlantı dizesi](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) için **SqlConnection** nesne hello değerler şu parametreler hello arasında koordine:</span><span class="sxs-lookup"><span data-stu-id="8313d-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="8313d-176">ConnectRetryCount &nbsp; &nbsp; *(varsayılan değer 1. Aralık 0 ile 255'dır.)*</span><span class="sxs-lookup"><span data-stu-id="8313d-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="8313d-177">ConnectRetryInterval &nbsp; &nbsp; *(varsayılan değer 1 saniye. 1 ile 60 aralıktır.)*</span><span class="sxs-lookup"><span data-stu-id="8313d-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="8313d-178">Bağlantı zaman aşımı &nbsp; &nbsp; *(varsayılan değer 15 saniye. Aralık 0 ile 2147483647'dır)*</span><span class="sxs-lookup"><span data-stu-id="8313d-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="8313d-179">Özellikle, seçilen değerlerinizi eşitlik true aşağıdaki hello olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8313d-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="8313d-180">Bağlantı zaman aşımı ConnectRetryCount = * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="8313d-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="8313d-181">Örneğin, hello sayılacak = 3 ve aralığı 29 saniye oldukça hello sistem kendi 3 ve son yeniden bağlanma sırasında yeterli süre verirsiniz değil yalnızca = 10 saniye, bir zaman aşımı süresi: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="8313d-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="8313d-182">Bağlantı komutu karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="8313d-182">Connection versus command</span></span>
<span data-ttu-id="8313d-183">Merhaba **ConnectRetryCount** ve **ConnectRetryInterval** parametreleri sağlar, **SqlConnection** nesnesi yeniden deneme hello bağlantı işlemini belirten veya rahatsız etme, program, Denetim tooyour programı döndürme gibi.</span><span class="sxs-lookup"><span data-stu-id="8313d-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="8313d-184">Merhaba deneme hello aşağıdaki durumlarda oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="8313d-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="8313d-185">mySqlConnection.Open yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="8313d-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="8313d-186">mySqlConnection.Execute yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="8313d-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="8313d-187">Bir subtlety yoktur.</span><span class="sxs-lookup"><span data-stu-id="8313d-187">There is a subtlety.</span></span> <span data-ttu-id="8313d-188">Geçici bir hata oluşursa karşın, *sorgu* yürütülmekte olan, **SqlConnection** nesne değil yeniden deneme hello işlemi bağlanıyor ve bunu kesinlikle sorgunuzu yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="8313d-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="8313d-189">Ancak, **SqlConnection** denetimleri sorgu yürütme için göndermeden önce bağlantı çok hızlı bir şekilde hello.</span><span class="sxs-lookup"><span data-stu-id="8313d-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="8313d-190">Bir bağlantı sorunu Hello hızlı onay algılarsa, **SqlConnection** yeniden deneme hello bağlanma işlemi.</span><span class="sxs-lookup"><span data-stu-id="8313d-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="8313d-191">Merhaba yeniden deneme başarılı olursa, sorgu yürütme için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="8313d-192">Uygulama yeniden deneme mantığı ile ConnectRetryCount birleştirilmelidir?</span><span class="sxs-lookup"><span data-stu-id="8313d-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="8313d-193">Güçlü özel yeniden deneme mantığı uygulamanız olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8313d-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="8313d-194">Merhaba yeniden deneyebilirler işlemi 4 kez bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8313d-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="8313d-195">Eklerseniz **ConnectRetryInterval** ve **ConnectRetryCount** 3 tooyour bağlantı dizesi = hello yeniden deneme sayısı too4 artıracaktır * 3 = 12 yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="8313d-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="8313d-196">Yeniden deneme yüksek sayı düşündüğünüz değil.</span><span class="sxs-lookup"><span data-stu-id="8313d-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="8313d-197">Bağlantıları tooAzure SQL veritabanı</span><span class="sxs-lookup"><span data-stu-id="8313d-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="8313d-198">Bağlantı: Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="8313d-198">Connection: Connection string</span></span>
<span data-ttu-id="8313d-199">Merhaba bağlantı dizesi tooAzure bağlanmak için gerekli SQL veritabanı hello dizesinden tooMicrosoft SQL Server bağlamak için biraz farklı olur.</span><span class="sxs-lookup"><span data-stu-id="8313d-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="8313d-200">Veritabanınız için hello hello bağlantı dizesini kopyalayabilirsiniz [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8313d-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="8313d-201">Bağlantı: IP adresi</span><span class="sxs-lookup"><span data-stu-id="8313d-201">Connection: IP address</span></span>
<span data-ttu-id="8313d-202">Merhaba SQL veritabanı sunucusu tooaccept iletişimi hello IP adresinden istemci programınızı barındıran hello bilgisayarın yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8313d-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="8313d-203">Merhaba aracılığıyla hello güvenlik duvarı ayarlarını düzenleyerek bunu [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8313d-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="8313d-204">Tooconfigure başlangıç IP adresi unutursanız, programınızı hello gerekli IP adresi bildiren bir kullanışlı hata iletisi ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8313d-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="8313d-205">Daha fazla bilgi için bkz: [nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="8313d-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="8313d-206">Bağlantı: bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="8313d-206">Connection: Ports</span></span>
<span data-ttu-id="8313d-207">Genellikle, yalnızca bağlantı noktası 1433 istemci programı barındıran hello bilgisayarda giden iletişim için açık olduğunu tooensure gerekir.</span><span class="sxs-lookup"><span data-stu-id="8313d-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="8313d-208">İstemci programınızı bir Windows bilgisayarda barındırılıyorsa, örneğin, hello ana bilgisayardaki Windows Güvenlik Duvarı hello tooopen bağlantı noktası 1433 sağlar:</span><span class="sxs-lookup"><span data-stu-id="8313d-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="8313d-209">Açık hello Denetim Masası</span><span class="sxs-lookup"><span data-stu-id="8313d-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="8313d-210">&gt;Tüm Denetim Masası öğeleri</span><span class="sxs-lookup"><span data-stu-id="8313d-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="8313d-211">&gt;Windows Güvenlik Duvarı</span><span class="sxs-lookup"><span data-stu-id="8313d-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="8313d-212">&gt;Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="8313d-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="8313d-213">&gt;Giden kuralları</span><span class="sxs-lookup"><span data-stu-id="8313d-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="8313d-214">&gt;Eylemler</span><span class="sxs-lookup"><span data-stu-id="8313d-214">&gt; Actions</span></span>
7. <span data-ttu-id="8313d-215">&gt;Yeni Kural</span><span class="sxs-lookup"><span data-stu-id="8313d-215">&gt; New Rule</span></span>

<span data-ttu-id="8313d-216">İstemci programınız Azure sanal makine (VM) barındırılıp barındırılmadığını, okumanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8313d-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="8313d-217">[ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="8313d-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="8313d-218">Arka plan IP adresi ve bağlantı noktaları hakkında bilgi için cofiguration, bkz: [Azure SQL veritabanı güvenlik duvarı](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="8313d-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="8313d-219">Bağlantı: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="8313d-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="8313d-220">ADO.NET sınıflarını gibi programınızı kullanıyorsa, **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL veritabanı, öneririz .NET Framework sürüm 4.6.1 kullanın ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="8313d-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="8313d-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="8313d-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="8313d-222">Azure SQL veritabanı için yapıldığında geliştirilmiş güvenilirlik hello kullanarak bir bağlantı açmak **SqlConnection.Open** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8313d-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="8313d-223">Merhaba **açık** yöntemi şimdi en iyi çaba yeniden deneme de mekanizmaları yanıt tootransient hataları hello bağlantı zaman aşımı süresi içinde belirli hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="8313d-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="8313d-224">Bağlantı havuzu destekler.</span><span class="sxs-lookup"><span data-stu-id="8313d-224">Supports connection pooling.</span></span> <span data-ttu-id="8313d-225">Bu bağlantı hello verimli bir doğrulama içerir programınızı verir nesne çalışmasını.</span><span class="sxs-lookup"><span data-stu-id="8313d-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="8313d-226">Bir bağlantı havuzundan bir bağlantı nesnesi kullandığınızda, programınızı geçici olarak hello bağlantı hemen kullanırken, kapatmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="8313d-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="8313d-227">Bir bağlantısı'nı yeniden açmayı pahalı olmayan yeni bir bağlantı oluşturma hello yoludur.</span><span class="sxs-lookup"><span data-stu-id="8313d-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="8313d-228">ADO.NET 4.0 kullanıyorsanız veya daha önce toohello yükseltmenizi öneririz son ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="8313d-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="8313d-229">Kasım 2015'ten itibaren yapabilecekleriniz [ADO.NET 4.6.1 karşıdan](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="8313d-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="8313d-230">Tanılama</span><span class="sxs-lookup"><span data-stu-id="8313d-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="8313d-231">Tanılama: yardımcı programlar bağlanıp bağlanamadığınızı Test</span><span class="sxs-lookup"><span data-stu-id="8313d-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="8313d-232">Programınızı tooconnect tooAzure SQL veritabanı başarısız olduysa, bir tanılama yardımcı programı ile tootry tooconnect seçenektir.</span><span class="sxs-lookup"><span data-stu-id="8313d-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="8313d-233">İdeal olarak hello yardımcı programı hello kullanarak bağlanması programınızın kullandığı aynı kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="8313d-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="8313d-234">Herhangi bir Windows bilgisayarda bu yardımcı programları deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8313d-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="8313d-235">SQL Server Management ADO.NET kullanarak bağlayan Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="8313d-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="8313d-236">kullanarak bağlanan sqlcmd.exe [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="8313d-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="8313d-237">Kısa bir SQL SELECT sorgusu çalışır olup olmadığını bağlandıktan sonra test edin.</span><span class="sxs-lookup"><span data-stu-id="8313d-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="8313d-238">Tanılama: Onay hello açık bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="8313d-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="8313d-239">Bağlantı denemeleri tooport sorunları başarısız olan şüpheleniyorsanız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="8313d-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="8313d-240">Bilgisayarınızda hello bağlantı noktası yapılandırmalarını raporları bir yardımcı programı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8313d-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="8313d-241">Linux hello üzerinde aşağıdaki yardımcı programlar yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="8313d-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="8313d-242">(Merhaba örnek değer toobe, IP adresini değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="8313d-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="8313d-243">Windows hello üzerinde [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) yardımcı programı yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="8313d-244">Başlangıç bağlantı noktası durumu bir Azure SQL veritabanı sunucusunda sorgulanan ve, bir dizüstü bilgisayar üzerinde çalıştırıldığı bir örnek yürütme şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8313d-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="8313d-245">Tanılama: hatalarınızı günlük</span><span class="sxs-lookup"><span data-stu-id="8313d-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="8313d-246">Aralıklı bir sorunun bazen en iyi genel bir desen algılanması gün veya hafta üzerinden tanı koydu.</span><span class="sxs-lookup"><span data-stu-id="8313d-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="8313d-247">İstemci, bulduğu tüm hataları günlüğü tarafından bir tanılama yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="8313d-248">Dahili olarak kendisini Azure SQL veritabanı günlük hata verilerle mümkün toocorrelate hello günlük girişlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="8313d-249">Kurumsal kitaplığı 6 (EntLib60) günlük ile yönetilen .NET sınıfları tooassist sunar:</span><span class="sxs-lookup"><span data-stu-id="8313d-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="8313d-250">5 - olarak kolay olarak dönmeden kapalı bir günlük: hello günlük uygulama bloğu kullanma</span><span class="sxs-lookup"><span data-stu-id="8313d-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="8313d-251">Tanılama: hatalar için sistem günlüklerini inceleyin</span><span class="sxs-lookup"><span data-stu-id="8313d-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="8313d-252">Burada, hata, sorgu günlükleri ve diğer bilgileri bazı Transact-SQL SELECT deyimleri bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8313d-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="8313d-253">Sorgu günlüğü</span><span class="sxs-lookup"><span data-stu-id="8313d-253">Query of log</span></span> | <span data-ttu-id="8313d-254">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8313d-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="8313d-255">Merhaba [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) görünümü geçici hataları veya bağlantısı hataları neden olabilir. bazı dahil olmak üzere ayrı ayrı olaylar hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="8313d-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="8313d-256">İdeal olarak hello ilişkilendirebilirsiniz **start_time** veya **end_time** ne zaman istemci programınız sorunlarla karşılaştınız hakkında bilgi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="8313d-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="8313d-257">**İpucu:** toohello bağlanmalısınız **ana** toorun bu veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8313d-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="8313d-258">Merhaba [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) görünümü olay türleri, ek tanılama için toplanan sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="8313d-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="8313d-259">**İpucu:** toohello bağlanmalısınız **ana** toorun bu veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8313d-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="8313d-260">Tanılama: Arama hello SQL veritabanı günlük sorun olayları için</span><span class="sxs-lookup"><span data-stu-id="8313d-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="8313d-261">Azure SQL veritabanı'nın hello günlüğüne sorun olaylarıyla ilgili girdileri arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8313d-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="8313d-262">Merhaba Transact-SQL SELECT deyiminde aşağıdaki hello deneyin **ana** veritabanı:</span><span class="sxs-lookup"><span data-stu-id="8313d-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="8313d-263">Sys.fn_xe_telemetry_blob_target_read_file birkaç döndürülen satırları</span><span class="sxs-lookup"><span data-stu-id="8313d-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="8313d-264">Sonraki döndürülen satır aşağıdaki gibi görünmelidir olduğu.</span><span class="sxs-lookup"><span data-stu-id="8313d-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="8313d-265">hello null değerler gösterilen diğer satırlardaki null olması genellikle gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8313d-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="8313d-266">Kurumsal kitaplığı 6</span><span class="sxs-lookup"><span data-stu-id="8313d-266">Enterprise Library 6</span></span>
<span data-ttu-id="8313d-267">Kurumsal kitaplığı 6 (EntLib60) biri hello Azure SQL veritabanı hizmetinin olan bulut Hizmetleri, sağlam istemcileri uygulamanıza yardımcı olacak bir .NET sınıfları çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="8313d-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="8313d-268">EntLib60 ilk ziyaret ederek yardımcı olabilecek konular ayrılmış tooeach alanı bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8313d-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="8313d-269">Kurumsal kitaplığı 6 - Nisan 2013</span><span class="sxs-lookup"><span data-stu-id="8313d-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="8313d-270">Geçici hataları işlemek için yeniden deneme mantığı EntLib60 yardımcı olabilecek bir alandır:</span><span class="sxs-lookup"><span data-stu-id="8313d-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="8313d-271">4 - perseverance, tüm Triumphs sırrını: hello geçici hata işleme uygulama blok kullanma</span><span class="sxs-lookup"><span data-stu-id="8313d-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="8313d-272">Merhaba kaynak kodu EntLib60 kullanılabilir ortak için [karşıdan](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="8313d-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="8313d-273">Microsoft hiçbir planları toomake daha fazla özelliği olan güncelleştirmeler ve Bakım tooEntLib güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="8313d-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="8313d-274">Geçici hataları ve yeniden deneme için EntLib60 sınıfları</span><span class="sxs-lookup"><span data-stu-id="8313d-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="8313d-275">EntLib60 sınıfları aşağıdaki hello yeniden deneme mantığı için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="8313d-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="8313d-276">Tüm bunlar içinde bulunan veya altında daha fazla ad alanı hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="8313d-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="8313d-277">*Merhaba ad alanındaki **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="8313d-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="8313d-278">**RetryPolicy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="8313d-279">**ExecuteAction** yöntemi</span><span class="sxs-lookup"><span data-stu-id="8313d-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="8313d-280">**ExponentialBackoff** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="8313d-281">**SqlDatabaseTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="8313d-282">**ReliableSqlConnection** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="8313d-283">**ExecuteCommand** yöntemi</span><span class="sxs-lookup"><span data-stu-id="8313d-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="8313d-284">Merhaba ad alanındaki **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="8313d-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="8313d-285">**AlwaysTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="8313d-286">**NeverTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="8313d-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="8313d-287">Bağlantılar tooinformation EntLib60 hakkında şunlardır:</span><span class="sxs-lookup"><span data-stu-id="8313d-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="8313d-288">Ücretsiz [defteri indirin: Geliştirici Kılavuzu tooMicrosoft Kurumsal kitaplığı 2 sürümü](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="8313d-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="8313d-289">En iyi uygulamalar: [yeniden genel rehberlik](../best-practices-retry-general.md) mükemmel ayrıntılı incelemesi yeniden deneme mantığı vardır.</span><span class="sxs-lookup"><span data-stu-id="8313d-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="8313d-290">NuGet yüklenmesini [Kurumsal Library - uygulama bloğu 6.0 geçici hata işleme](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="8313d-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="8313d-291">EntLib60: hello günlük bloğu</span><span class="sxs-lookup"><span data-stu-id="8313d-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="8313d-292">Merhaba günlük bloğu izin veren oldukça esnek ve yapılandırılabilir bir çözümdür:</span><span class="sxs-lookup"><span data-stu-id="8313d-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="8313d-293">Oluşturabilir ve çok çeşitli konumları günlük iletilerini depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="8313d-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="8313d-294">Kategorilere ayırmak ve iletilerini filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8313d-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="8313d-295">Hata ayıklama ve izlemenin yanı sıra denetlemek için kullanışlı ve genel günlüğü gereksinimleri bağlamsal bilgi toplayın.</span><span class="sxs-lookup"><span data-stu-id="8313d-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="8313d-296">Merhaba günlük bloğu hello uygulama kodu hello konumu ve tür hello hedef günlük deposu bağımsız olarak tutarlı olmasını sağlamak işlevselliği hello günlük hedeften günlüğü hello soyutlar.</span><span class="sxs-lookup"><span data-stu-id="8313d-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="8313d-297">Ayrıntılar için bkz: [5 - olarak kolay olarak dönmeden kapalı bir günlük: hello günlük uygulama bloğu kullanma](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="8313d-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="8313d-298">EntLib60 IsTransient yöntemi kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="8313d-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="8313d-299">Merhaba gelen sonraki **SqlDatabaseTransientErrorDetectionStrategy** sınıfı, hello hello C# kaynak kodu **IsTransient** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8313d-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="8313d-300">Merhaba kaynak kodu hangi hatalarını toobe geçici ve Nisan 2013'ten itibaren yeniden deneme worthy kabul açıklar.</span><span class="sxs-lookup"><span data-stu-id="8313d-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="8313d-301">Çok sayıda **//comment** satırları bu kopya tooemphasize okunabilirlik kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="8313d-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="8313d-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8313d-302">Next steps</span></span>
* <span data-ttu-id="8313d-303">Diğer ortak Azure SQL veritabanı bağlantı sorunlarını gidermek için ziyaret [sorun giderme bağlantı sorunları tooAzure SQL veritabanı](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="8313d-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="8313d-304">SQL Server bağlantı (ADO.NET) havuzu</span><span class="sxs-lookup"><span data-stu-id="8313d-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="8313d-305">*Yeniden deneniyor* lisanslı bir Apache 2.0 yazılan kitaplığı yeniden deneniyor genel amaçlı olduğundan getirin **Python**, toosimplify hello görev yeniden deneme davranışı toojust hakkında hiçbir şey ekleme.</span><span class="sxs-lookup"><span data-stu-id="8313d-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

