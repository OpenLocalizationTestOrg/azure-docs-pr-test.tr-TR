---
title: "SQL bağlantı hatası, geçici hata düzeltme | Microsoft Docs"
description: "Sorun giderme, tanılama ve SQL bağlantı hatası veya Azure SQL veritabanındaki geçici hata önlemek öğrenin. "
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
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="95c56-104">SQL Database için SQL bağlantı hatalarını ve geçici hataları giderme, tanılama ve önleme</span><span class="sxs-lookup"><span data-stu-id="95c56-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="95c56-105">Bu makalede, engellemek, sorun giderme, tanılama ve bağlantı hataları ve Azure SQL veritabanı ile etkileşim kurarken, istemci uygulamanız karşılaştığında geçici hataları etkisini açıklar.</span><span class="sxs-lookup"><span data-stu-id="95c56-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="95c56-106">Yeniden deneme mantığı yapılandırmak, bağlantı dizesi oluşturma ve diğer bağlantı ayarlarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="95c56-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="95c56-107">Geçici hataları geçici</span><span class="sxs-lookup"><span data-stu-id="95c56-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="95c56-108">Geçici bir hata - Ayrıca, geçici hata - kendisini yakında çözümleyecek bir temel nedeni vardır.</span><span class="sxs-lookup"><span data-stu-id="95c56-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="95c56-109">Azure sistem hızla donanım kaynakları daha iyi yük dengelemek için çeşitli iş yükleri geçtiğinde geçici hataları zaman zaman bir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="95c56-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="95c56-110">Bu yeniden yapılandırma olayları çoğunu genellikle 60 saniyeden daha kısa bir süre içinde tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="95c56-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="95c56-111">Bu yeniden yapılandırma zaman aralığı sırasında Azure SQL veritabanı için bağlantı sorunu olabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="95c56-112">Azure SQL veritabanına bağlanma uygulamaları yerleşik bu geçici hataları beklediğiniz, bunları kullanıcılara uygulama hataları olarak görünmesini yerine kendi kodunda yeniden deneme mantığı uygulayarak işlemek için.</span><span class="sxs-lookup"><span data-stu-id="95c56-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="95c56-113">İstemci programınızı ADO.NET kullanarak, programınızı throw tarafından geçici hata hakkında işe bir **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="95c56-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="95c56-114">**Numarası** özelliği, üst konu kısmına yakın geçici hataları listesine karşı karşılaştırılabilir: [SQL Database istemci uygulamaları için SQL hata kodları](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="95c56-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="95c56-115">Bağlantı komutu karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="95c56-115">Connection versus command</span></span>
<span data-ttu-id="95c56-116">SQL bağlantısı yeniden deneme veya yeniden bağlı olarak aşağıdaki kurmak:</span><span class="sxs-lookup"><span data-stu-id="95c56-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="95c56-117">**Bir bağlantı try sırasında geçici bir hata oluşur**: bağlantı geciktirme birkaç saniye sonra yeniden denenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="95c56-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="95c56-118">**Bir SQL sorgu komutu sırasında geçici bir hata oluşur**: komutu değil hemen yeniden denenmesi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="95c56-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="95c56-119">Bunun yerine, bir gecikmeden sonra istemcinin yeniden bağlantı.</span><span class="sxs-lookup"><span data-stu-id="95c56-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="95c56-120">Sonra komutu yeniden denenebilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="95c56-121">Geçici hatalar için yeniden deneme mantığı</span><span class="sxs-lookup"><span data-stu-id="95c56-121">Retry logic for transient errors</span></span>
<span data-ttu-id="95c56-122">Yeniden deneme mantığı içerdiğinde bazen geçici bir hatayla karşılaşırsanız istemci programları daha sağlamdır.</span><span class="sxs-lookup"><span data-stu-id="95c56-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="95c56-123">Programınızı 3 bir taraf ara yazılımı Azure SQL veritabanı ile iletişim kurduğunda, geçici hataları yeniden deneme mantığı ara yazılım içerip içermediğini satıcıyla sorgulayın.</span><span class="sxs-lookup"><span data-stu-id="95c56-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="95c56-124">Yeniden deneme ilkelerini</span><span class="sxs-lookup"><span data-stu-id="95c56-124">Principles for retry</span></span>
* <span data-ttu-id="95c56-125">Geçici bir hatadır, bir bağlantı açmak için girişiminde denenmeli.</span><span class="sxs-lookup"><span data-stu-id="95c56-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="95c56-126">Geçici bir hata ile başarısız olan bir SQL SELECT deyimi doğrudan denenmeli değil.</span><span class="sxs-lookup"><span data-stu-id="95c56-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="95c56-127">Bunun yerine, yeni bir bağlantı kurarak Seç yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="95c56-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="95c56-128">Bir SQL UPDATE deyimi geçici bir hata ile başarısız olduğunda, güncelleştirme denenen önce yeni bir bağlantı kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95c56-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="95c56-129">Yeniden deneme mantığı, tüm veritabanı işlem tamamlandı ya da, tüm işlem geri alındı emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="95c56-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="95c56-130">Yeniden deneme ile diğer değerlendirmeler</span><span class="sxs-lookup"><span data-stu-id="95c56-130">Other considerations for retry</span></span>
* <span data-ttu-id="95c56-131">Çalışma saatlerinden sonra otomatik olarak başlatılır ve sabah önce tamamlanır toplu iş programı uzun zaman aralıklarına kendi yeniden deneme girişimleri arasındaki ile çok hasta destekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="95c56-132">Bir kullanıcı arabirimi programı sonra çok uzun bekleme vermek İnsan eğilimi hesabı.</span><span class="sxs-lookup"><span data-stu-id="95c56-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="95c56-133">Ancak, bu ilkeyi istekleri sistemiyle bölgesini doldurmak için birkaç saniyede yeniden denemek için çözüm olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="95c56-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="95c56-134">Denemeler arasındaki aralığı artırma</span><span class="sxs-lookup"><span data-stu-id="95c56-134">Interval increase between retries</span></span>
<span data-ttu-id="95c56-135">İlk, yeniden denemeden önce 5 saniye gecikme öneririz.</span><span class="sxs-lookup"><span data-stu-id="95c56-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="95c56-136">Bulut hizmeti aşırı 5 saniye riskleri kısa bir gecikme sonrasında yeniden deneniyor.</span><span class="sxs-lookup"><span data-stu-id="95c56-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="95c56-137">Gecikme büyümesine katlanarak, her sonraki yeniden deneme için en fazla 60 saniye.</span><span class="sxs-lookup"><span data-stu-id="95c56-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="95c56-138">Bir tartışma *engelleme süresi* ADO.NET kullanan istemciler için kullanılabilir [SQL Server bağlantı havuzu (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="95c56-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="95c56-139">Program otomatik olarak kapatılmadan önce yeniden deneme sayısı üst ayarlamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c56-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="95c56-140">Yeniden deneme mantığı ile kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="95c56-140">Code samples with retry logic</span></span>
<span data-ttu-id="95c56-141">Kod örnekleri programlama dilleri, çeşitli yeniden deneme mantığı ile şu konumda mevcuttur:</span><span class="sxs-lookup"><span data-stu-id="95c56-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="95c56-142">SQL Database ve SQL Server için bağlantı kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="95c56-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="95c56-143">Yeniden deneme mantığı test</span><span class="sxs-lookup"><span data-stu-id="95c56-143">Test your retry logic</span></span>
<span data-ttu-id="95c56-144">Yeniden deneme mantığı sınamak için benzetimini yapmak veya programınız çalışmaya devam ederken düzeltilebilir daha hataya neden gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c56-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="95c56-145">Ağ bağlantısını keserek test</span><span class="sxs-lookup"><span data-stu-id="95c56-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="95c56-146">Yeniden deneme mantığı sınayabilirsiniz bir program çalışırken, istemci bilgisayar ağ bağlantısını kesmek için yoludur.</span><span class="sxs-lookup"><span data-stu-id="95c56-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="95c56-147">Hata olacaktır:</span><span class="sxs-lookup"><span data-stu-id="95c56-147">The error will be:</span></span>

* <span data-ttu-id="95c56-148">**SqlException.Number** 11001 =</span><span class="sxs-lookup"><span data-stu-id="95c56-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="95c56-149">İleti: "gibi bir ana makine bilinmiyor"</span><span class="sxs-lookup"><span data-stu-id="95c56-149">Message: "No such host is known"</span></span>

<span data-ttu-id="95c56-150">İlk yeniden deneme girişimi bir parçası olarak programınızı yazım hatası düzeltin ve bağlanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="95c56-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="95c56-151">Bu pratik yapmak için program başlamadan önce ağ bilgisayarınızdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="95c56-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="95c56-152">Ardından programınızı programa neden olan bir çalışma zamanı parametre tanır:</span><span class="sxs-lookup"><span data-stu-id="95c56-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="95c56-153">Geçici olarak 11001 geçici dikkate alınması gereken hataları listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="95c56-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="95c56-154">İlk bağlantı her zamanki gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="95c56-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="95c56-155">Hata belirledi sonra 11001 listeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="95c56-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="95c56-156">Bilgisayar ağa takın kullanıcıya söyleyen bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="95c56-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="95c56-157">Daha fazla yürütme kullanarak duraklatmak **Console.ReadLine** yöntemi veya bir iletişim kutusunda Tamam düğmesi.</span><span class="sxs-lookup"><span data-stu-id="95c56-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="95c56-158">Kullanıcı, bilgisayar ağa takılı sonra Enter tuşuna basar.</span><span class="sxs-lookup"><span data-stu-id="95c56-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="95c56-159">Yeniden bağlanma, başarı bekleniyor girişimi.</span><span class="sxs-lookup"><span data-stu-id="95c56-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="95c56-160">Veritabanı adı bağlanırken yazım hatası ile test</span><span class="sxs-lookup"><span data-stu-id="95c56-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="95c56-161">Programınızı kasıtlı olarak, hata ilk bağlantı denemesine önce kullanıcı adı hatalı.</span><span class="sxs-lookup"><span data-stu-id="95c56-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="95c56-162">Hata olacaktır:</span><span class="sxs-lookup"><span data-stu-id="95c56-162">The error will be:</span></span>

* <span data-ttu-id="95c56-163">**SqlException.Number** 18456 =</span><span class="sxs-lookup"><span data-stu-id="95c56-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="95c56-164">İleti: "'WRONG_MyUserName' kullanıcı için oturum açma başarısız."</span><span class="sxs-lookup"><span data-stu-id="95c56-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="95c56-165">İlk yeniden deneme girişimi bir parçası olarak programınızı yazım hatası düzeltin ve bağlanmayı dener.</span><span class="sxs-lookup"><span data-stu-id="95c56-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="95c56-166">Bu pratik yapmak için programınızı programa neden olan bir çalışma zamanı parametre tanı:</span><span class="sxs-lookup"><span data-stu-id="95c56-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="95c56-167">Geçici olarak 18456 geçici dikkate alınması gereken hataları listesine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="95c56-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="95c56-168">Kasıtlı olarak 'WRONG_' için kullanıcı adını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="95c56-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="95c56-169">Hata belirledi sonra 18456 listeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="95c56-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="95c56-170">'WRONG_' kullanıcı adını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="95c56-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="95c56-171">Yeniden bağlanma, başarı bekleniyor girişimi.</span><span class="sxs-lookup"><span data-stu-id="95c56-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="95c56-172">Bağlantı yeniden deneme için .NET SqlConnection parametreleri</span><span class="sxs-lookup"><span data-stu-id="95c56-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="95c56-173">İstemci programınız Azure SQL veritabanı için .NET Framework sınıf kullanarak bağlanırsa **System.Data.SqlClient.SqlConnection**, .NET 4.6.1 kullanması gereken veya daha sonra (veya .NET Core), bağlantı yeniden deneme özelliğinden yararlanabilirsiniz şekilde.</span><span class="sxs-lookup"><span data-stu-id="95c56-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="95c56-174">Özelliğin ayrıntıları [burada](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="95c56-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="95c56-175">Oluşturduğunuzda [bağlantı dizesi](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) için **SqlConnection** nesne değerler aşağıdaki parametreleri arasında koordine:</span><span class="sxs-lookup"><span data-stu-id="95c56-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="95c56-176">ConnectRetryCount &nbsp; &nbsp; *(varsayılan değer 1. Aralık 0 ile 255'dır.)*</span><span class="sxs-lookup"><span data-stu-id="95c56-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="95c56-177">ConnectRetryInterval &nbsp; &nbsp; *(varsayılan değer 1 saniye. 1 ile 60 aralıktır.)*</span><span class="sxs-lookup"><span data-stu-id="95c56-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="95c56-178">Bağlantı zaman aşımı &nbsp; &nbsp; *(varsayılan değer 15 saniye. Aralık 0 ile 2147483647'dır)*</span><span class="sxs-lookup"><span data-stu-id="95c56-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="95c56-179">Özellikle, seçilen değerlerinizi aşağıdaki eşitlik true olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="95c56-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="95c56-180">Bağlantı zaman aşımı ConnectRetryCount = * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="95c56-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="95c56-181">Örneğin, varsa sayısı = 3 ve aralığı 29 saniye oldukça sistem kendi 3 ve son yeniden bağlanma sırasında yeterli süre verirsiniz değil yalnızca = 10 saniye, bir zaman aşımı süresi: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="95c56-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="95c56-182">Bağlantı komutu karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="95c56-182">Connection versus command</span></span>
<span data-ttu-id="95c56-183">**ConnectRetryCount** ve **ConnectRetryInterval** parametreleri sağlar, **SqlConnection** nesne söyleyen veya rahatsız etme bağlanma işlemi yeniden deneyin, program, programınıza denetimi döndürme gibi.</span><span class="sxs-lookup"><span data-stu-id="95c56-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="95c56-184">Yeniden deneme aşağıdaki durumlarda oluşabilir:</span><span class="sxs-lookup"><span data-stu-id="95c56-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="95c56-185">mySqlConnection.Open yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="95c56-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="95c56-186">mySqlConnection.Execute yöntem çağrısı</span><span class="sxs-lookup"><span data-stu-id="95c56-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="95c56-187">Bir subtlety yoktur.</span><span class="sxs-lookup"><span data-stu-id="95c56-187">There is a subtlety.</span></span> <span data-ttu-id="95c56-188">Geçici bir hata oluşursa karşın, *sorgu* yürütülmekte olan, **SqlConnection** nesnesi yeniden bağlanma işlemi ve bunu kesinlikle sorgunuzu yeniden denemez.</span><span class="sxs-lookup"><span data-stu-id="95c56-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="95c56-189">Ancak, **SqlConnection** çok hızlı bir şekilde sorgu yürütme için göndermeden önce bağlantıyı denetler.</span><span class="sxs-lookup"><span data-stu-id="95c56-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="95c56-190">Bir bağlantı sorunu hızlı onay algılarsa, **SqlConnection** bağlanma işlemini yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="95c56-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="95c56-191">Yeniden deneme başarılı olursa, sorgu yürütme için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="95c56-192">Uygulama yeniden deneme mantığı ile ConnectRetryCount birleştirilmelidir?</span><span class="sxs-lookup"><span data-stu-id="95c56-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="95c56-193">Güçlü özel yeniden deneme mantığı uygulamanız olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="95c56-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="95c56-194">Bağlanma işlemi 4 kez yeniden deneyebilirler.</span><span class="sxs-lookup"><span data-stu-id="95c56-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="95c56-195">Eklerseniz **ConnectRetryInterval** ve **ConnectRetryCount** = 3 bağlantı dizenizi 4 * 3 = 12 yeniden deneme sayısı artacaktır yeniden deneme sayısı.</span><span class="sxs-lookup"><span data-stu-id="95c56-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="95c56-196">Yeniden deneme yüksek sayı düşündüğünüz değil.</span><span class="sxs-lookup"><span data-stu-id="95c56-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="95c56-197">Azure SQL veritabanı bağlantıları</span><span class="sxs-lookup"><span data-stu-id="95c56-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="95c56-198">Bağlantı: Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="95c56-198">Connection: Connection string</span></span>
<span data-ttu-id="95c56-199">Azure SQL veritabanına bağlanmak için gerekli bağlantı dizesi, Microsoft SQL Server veritabanına bağlanmak için dize biraz farklıdır.</span><span class="sxs-lookup"><span data-stu-id="95c56-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="95c56-200">Veritabanınızdan için bağlantı dizesini kopyalayabilirsiniz [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95c56-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="95c56-201">Bağlantı: IP adresi</span><span class="sxs-lookup"><span data-stu-id="95c56-201">Connection: IP address</span></span>
<span data-ttu-id="95c56-202">SQL veritabanı sunucusu, istemci programınızı barındıran bilgisayarın IP adresinden gelen iletişimi kabul edecek şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c56-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="95c56-203">Güvenlik Duvarı Ayarları'nda düzenleyerek bunu [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="95c56-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="95c56-204">IP adresini yapılandırmak unutursanız, programınızı gerekli IP adresi bildiren bir kullanışlı hata iletisi ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="95c56-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="95c56-205">Daha fazla bilgi için bkz: [nasıl yapılır: SQL veritabanında güvenlik duvarı ayarlarını yapılandırma](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="95c56-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="95c56-206">Bağlantı: bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="95c56-206">Connection: Ports</span></span>
<span data-ttu-id="95c56-207">Genellikle, yalnızca bağlantı noktası 1433 istemci programı barındıran bilgisayarda giden iletişim için açık olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c56-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="95c56-208">İstemci programınızı bir Windows bilgisayarda barındırılıyorsa, örneğin, ana bilgisayardaki Windows Güvenlik Duvarı'nı bağlantı noktası 1433 açmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="95c56-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="95c56-209">Denetim Masası'nı açın</span><span class="sxs-lookup"><span data-stu-id="95c56-209">Open the Control Panel</span></span>
2. <span data-ttu-id="95c56-210">&gt;Tüm Denetim Masası öğeleri</span><span class="sxs-lookup"><span data-stu-id="95c56-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="95c56-211">&gt;Windows Güvenlik Duvarı</span><span class="sxs-lookup"><span data-stu-id="95c56-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="95c56-212">&gt;Gelişmiş ayarlar</span><span class="sxs-lookup"><span data-stu-id="95c56-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="95c56-213">&gt;Giden kuralları</span><span class="sxs-lookup"><span data-stu-id="95c56-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="95c56-214">&gt;Eylemler</span><span class="sxs-lookup"><span data-stu-id="95c56-214">&gt; Actions</span></span>
7. <span data-ttu-id="95c56-215">&gt;Yeni Kural</span><span class="sxs-lookup"><span data-stu-id="95c56-215">&gt; New Rule</span></span>

<span data-ttu-id="95c56-216">İstemci programınız Azure sanal makine (VM) barındırılıp barındırılmadığını, okumanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="95c56-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="95c56-217">[ADO.NET 4.5 ve SQL veritabanı için 1433 dışındaki bağlantı noktaları](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="95c56-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="95c56-218">Arka plan IP adresi ve bağlantı noktaları hakkında bilgi için cofiguration, bkz: [Azure SQL veritabanı güvenlik duvarı](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="95c56-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="95c56-219">Bağlantı: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="95c56-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="95c56-220">ADO.NET sınıflarını gibi programınızı kullanıyorsa, **System.Data.SqlClient.SqlConnection** Azure SQL veritabanına bağlanmak için .NET Framework 4.6.1 sürümü kullanmanızı öneririz ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="95c56-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="95c56-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="95c56-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="95c56-222">Azure SQL veritabanı için yapıldığında geliştirilmiş güvenilirlik kullanarak bir bağlantı açmak **SqlConnection.Open** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="95c56-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="95c56-223">**Açık** yöntemi şimdi en iyi çaba yeniden deneme geçici hataları için mekanizmaları bağlantı zaman aşımı süresi içinde belirli hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="95c56-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="95c56-224">Bağlantı havuzu destekler.</span><span class="sxs-lookup"><span data-stu-id="95c56-224">Supports connection pooling.</span></span> <span data-ttu-id="95c56-225">Bu, program sunar bağlantı nesnesi çalıştığından verimli bir doğrulama içerir.</span><span class="sxs-lookup"><span data-stu-id="95c56-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="95c56-226">Bir bağlantı havuzundan bir bağlantı nesnesi kullandığınızda, programınızı geçici olarak bağlantı hemen kullanırken, kapatmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="95c56-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="95c56-227">Bir bağlantı yeniden açarak yeni bir bağlantı oluşturma yolu pahalı değil.</span><span class="sxs-lookup"><span data-stu-id="95c56-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="95c56-228">ADO.NET 4.0 kullanıyorsanız isterseniz daha önce en son ADO.NET yükseltmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="95c56-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="95c56-229">Kasım 2015'ten itibaren yapabilecekleriniz [ADO.NET 4.6.1 karşıdan](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="95c56-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="95c56-230">Tanılama</span><span class="sxs-lookup"><span data-stu-id="95c56-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="95c56-231">Tanılama: yardımcı programlar bağlanıp bağlanamadığınızı Test</span><span class="sxs-lookup"><span data-stu-id="95c56-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="95c56-232">Azure SQL veritabanına bağlanmak, program başarısız olduysa, bir tanılama yardımcı programı ile bağlanmayı denemek için seçenektir.</span><span class="sxs-lookup"><span data-stu-id="95c56-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="95c56-233">İdeal olarak yardımcı programı programınızın kullandığı aynı kitaplığı kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="95c56-234">Herhangi bir Windows bilgisayarda bu yardımcı programları deneyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95c56-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="95c56-235">SQL Server Management ADO.NET kullanarak bağlayan Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="95c56-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="95c56-236">kullanarak bağlanan sqlcmd.exe [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="95c56-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="95c56-237">Kısa bir SQL SELECT sorgusu çalışır olup olmadığını bağlandıktan sonra test edin.</span><span class="sxs-lookup"><span data-stu-id="95c56-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="95c56-238">Tanılama: açık bağlantı noktalarını denetleyin</span><span class="sxs-lookup"><span data-stu-id="95c56-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="95c56-239">Bağlantı sorunları nedeniyle bağlantı girişimleri başarısız olduğunu düşündüğünüz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="95c56-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="95c56-240">Bilgisayarınızda, bağlantı noktası yapılandırmalarını raporları bir yardımcı programı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c56-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="95c56-241">Linux üzerinde aşağıdaki yardımcı programlar yararlı olabilir:</span><span class="sxs-lookup"><span data-stu-id="95c56-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="95c56-242">(Örnek değeri, IP adresi olacak şekilde değiştirin.)</span><span class="sxs-lookup"><span data-stu-id="95c56-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="95c56-243">Windows [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) yardımcı programı yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="95c56-244">Azure SQL Database sunucusu bağlantı noktası durumunuza sorgulanan ve, bir dizüstü bilgisayar üzerinde çalıştırıldığı bir örnek yürütme şöyledir:</span><span class="sxs-lookup"><span data-stu-id="95c56-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="95c56-245">Tanılama: hatalarınızı günlük</span><span class="sxs-lookup"><span data-stu-id="95c56-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="95c56-246">Aralıklı bir sorunun bazen en iyi genel bir desen algılanması gün veya hafta üzerinden tanı koydu.</span><span class="sxs-lookup"><span data-stu-id="95c56-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="95c56-247">İstemci, bulduğu tüm hataları günlüğü tarafından bir tanılama yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="95c56-248">Günlük girişlerini dahili olarak kendisini Azure SQL veritabanı günlük hata verileri ile ilişkilendirmek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="95c56-249">Kurumsal kitaplığı 6 (EntLib60) günlük kaydıyla yardımcı olmak için yönetilen .NET sınıfları sunar:</span><span class="sxs-lookup"><span data-stu-id="95c56-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="95c56-250">5 - Oturumu Kapat dönmeden kadar kolay: günlük uygulama bloğu kullanma</span><span class="sxs-lookup"><span data-stu-id="95c56-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="95c56-251">Tanılama: hatalar için sistem günlüklerini inceleyin</span><span class="sxs-lookup"><span data-stu-id="95c56-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="95c56-252">Burada, hata, sorgu günlükleri ve diğer bilgileri bazı Transact-SQL SELECT deyimleri bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95c56-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="95c56-253">Sorgu günlüğü</span><span class="sxs-lookup"><span data-stu-id="95c56-253">Query of log</span></span> | <span data-ttu-id="95c56-254">Açıklama</span><span class="sxs-lookup"><span data-stu-id="95c56-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="95c56-255">[Sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) görünümü geçici hataları veya bağlantısı hataları neden olabilir. bazı dahil olmak üzere ayrı ayrı olaylar hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="95c56-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="95c56-256">İdeal olarak ilişkilendirebilirsiniz **start_time** veya **end_time** ne zaman istemci programınız sorunlarla karşılaştınız hakkında bilgi değerlerle.</span><span class="sxs-lookup"><span data-stu-id="95c56-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="95c56-257">**İpucu:** bağlanmalısınız **ana** bunu çalıştırmak için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="95c56-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="95c56-258">[Sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) görünümü olay türleri, ek tanılama için toplanan sayısını sağlar.</span><span class="sxs-lookup"><span data-stu-id="95c56-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="95c56-259">**İpucu:** bağlanmalısınız **ana** bunu çalıştırmak için veritabanı.</span><span class="sxs-lookup"><span data-stu-id="95c56-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="95c56-260">Tanılama: SQL veritabanı günlük sorun olayları arama</span><span class="sxs-lookup"><span data-stu-id="95c56-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="95c56-261">Azure SQL veritabanı'nın günlükteki sorun olaylarıyla ilgili girdileri arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c56-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="95c56-262">Aşağıdaki Transact-SQL SELECT deyiminde deneyin **ana** veritabanı:</span><span class="sxs-lookup"><span data-stu-id="95c56-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="95c56-263">Sys.fn_xe_telemetry_blob_target_read_file birkaç döndürülen satırları</span><span class="sxs-lookup"><span data-stu-id="95c56-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="95c56-264">Sonraki döndürülen satır aşağıdaki gibi görünmelidir olduğu.</span><span class="sxs-lookup"><span data-stu-id="95c56-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="95c56-265">Gösterilen null değerleri diğer satırlardaki null değildir.</span><span class="sxs-lookup"><span data-stu-id="95c56-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="95c56-266">Kurumsal kitaplığı 6</span><span class="sxs-lookup"><span data-stu-id="95c56-266">Enterprise Library 6</span></span>
<span data-ttu-id="95c56-267">Kurumsal kitaplığı 6 (EntLib60) biri Azure SQL veritabanı hizmeti olan bulut Hizmetleri, sağlam istemcileri uygulamanıza yardımcı olacak bir .NET sınıfları çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="95c56-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="95c56-268">İlk ziyaret ederek EntLib60 yardımcı olabilecek her alanına ayrılmış konuları bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95c56-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="95c56-269">Kurumsal kitaplığı 6 - Nisan 2013</span><span class="sxs-lookup"><span data-stu-id="95c56-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="95c56-270">Geçici hataları işlemek için yeniden deneme mantığı EntLib60 yardımcı olabilecek bir alandır:</span><span class="sxs-lookup"><span data-stu-id="95c56-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="95c56-271">4 - perseverance, tüm Triumphs sırrını: geçici hata işleme uygulama blok kullanma</span><span class="sxs-lookup"><span data-stu-id="95c56-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="95c56-272">Kaynak kodu EntLib60 için kullanılabilir ortak için [karşıdan](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="95c56-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="95c56-273">Microsoft, daha fazla özellik güncelleştirmeleri veya bakım güncelleştirmeleri için EntLib yapmak için herhangi bir plan sahiptir.</span><span class="sxs-lookup"><span data-stu-id="95c56-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="95c56-274">Geçici hataları ve yeniden deneme için EntLib60 sınıfları</span><span class="sxs-lookup"><span data-stu-id="95c56-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="95c56-275">Aşağıdaki EntLib60 sınıfları yeniden deneme mantığı için özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="95c56-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="95c56-276">Tüm bunlar içinde bulunan veya ad alanı altında daha fazla **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="95c56-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="95c56-277">*Ad alanında **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="95c56-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="95c56-278">**RetryPolicy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="95c56-279">**ExecuteAction** yöntemi</span><span class="sxs-lookup"><span data-stu-id="95c56-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="95c56-280">**ExponentialBackoff** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="95c56-281">**SqlDatabaseTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="95c56-282">**ReliableSqlConnection** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="95c56-283">**ExecuteCommand** yöntemi</span><span class="sxs-lookup"><span data-stu-id="95c56-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="95c56-284">Ad alanında **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="95c56-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="95c56-285">**AlwaysTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="95c56-286">**NeverTransientErrorDetectionStrategy** sınıfı</span><span class="sxs-lookup"><span data-stu-id="95c56-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="95c56-287">Aşağıda, EntLib60 hakkında bilgilere bağlantılar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="95c56-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="95c56-288">Ücretsiz [kitap indirme: Microsoft Enterprise kitaplığa 2 sürümü Geliştirici Kılavuzu](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="95c56-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="95c56-289">En iyi uygulamalar: [yeniden genel rehberlik](../best-practices-retry-general.md) mükemmel ayrıntılı incelemesi yeniden deneme mantığı vardır.</span><span class="sxs-lookup"><span data-stu-id="95c56-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="95c56-290">NuGet yüklenmesini [Kurumsal Library - uygulama bloğu 6.0 geçici hata işleme](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="95c56-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="95c56-291">EntLib60: Günlük bloğu</span><span class="sxs-lookup"><span data-stu-id="95c56-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="95c56-292">Günlük bloğu izin veren oldukça esnek ve yapılandırılabilir bir çözümdür:</span><span class="sxs-lookup"><span data-stu-id="95c56-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="95c56-293">Oluşturabilir ve çok çeşitli konumları günlük iletilerini depolayabilir.</span><span class="sxs-lookup"><span data-stu-id="95c56-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="95c56-294">Kategorilere ayırmak ve iletilerini filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c56-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="95c56-295">Hata ayıklama ve izlemenin yanı sıra denetlemek için kullanışlı ve genel günlüğü gereksinimleri bağlamsal bilgi toplayın.</span><span class="sxs-lookup"><span data-stu-id="95c56-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="95c56-296">Uygulama kodu, konum ve türünü hedef günlük deposu bağımsız olarak tutarlı olmasını sağlamak günlük bloğu günlük hedefi günlüğe kaydetme işlevlerini soyutlar.</span><span class="sxs-lookup"><span data-stu-id="95c56-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="95c56-297">Ayrıntılar için bkz: [5 - olarak kolay olarak dönmeden kapalı bir günlük: günlük uygulama bloğu kullanma](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="95c56-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="95c56-298">EntLib60 IsTransient yöntemi kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="95c56-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="95c56-299">Öğesinden sonraki **SqlDatabaseTransientErrorDetectionStrategy** sınıfı, C# kaynak kodu **IsTransient** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="95c56-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="95c56-300">Kaynak kodu hangi hataları geçici ve Yeniden Dene'yi, Nisan 2013'ten itibaren worthy olarak kabul açıklar.</span><span class="sxs-lookup"><span data-stu-id="95c56-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="95c56-301">Çok sayıda **//comment** satırları okunabilirlik vurgulamak için bu kopyadan kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="95c56-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
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
            // The instance of SQL Server you attempted to connect to
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


## <a name="next-steps"></a><span data-ttu-id="95c56-302">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95c56-302">Next steps</span></span>
* <span data-ttu-id="95c56-303">Diğer ortak Azure SQL veritabanı bağlantı sorunlarını gidermek için ziyaret [Azure SQL veritabanı bağlantı sorunlarını giderme](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="95c56-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="95c56-304">SQL Server bağlantı (ADO.NET) havuzu</span><span class="sxs-lookup"><span data-stu-id="95c56-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="95c56-305">*Yeniden deneniyor* lisanslı bir Apache 2.0 yazılan kitaplığı yeniden deneniyor genel amaçlı olduğundan getirin **Python**, yeniden deneme davranışı için neredeyse her şeyi ekleme görevini kolaylaştırmak için.</span><span class="sxs-lookup"><span data-stu-id="95c56-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

