---
title: "Akış analizi: oturum açma kimlik bilgilerini girişleri ve çıkışları döndürme | Microsoft Docs"
description: "Nasıl tooupdate hello Stream Analytics girişleri ve çıkışları için kimlik bilgileri öğrenin."
keywords: "oturum açma kimlik bilgileri"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="3e226-104">Giriş ve çıkış akış analizi işleri, oturum açma kimlik bilgileri döndürün</span><span class="sxs-lookup"><span data-stu-id="3e226-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="3e226-105">Özet</span><span class="sxs-lookup"><span data-stu-id="3e226-105">Abstract</span></span>
<span data-ttu-id="3e226-106">Azure Stream Analytics, bugün hello iş çalışırken bir giriş/çıkış hello kimlik bilgilerini değiştirme izin vermez.</span><span class="sxs-lookup"><span data-stu-id="3e226-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="3e226-107">Azure Stream Analytics işi son çıktısından desteklerken, biz tooshare hello tüm işlem durdurma hello hello işi başlatılıyor ve hello oturum açma kimlik bilgilerini döndürme arasında hello gecikme en aza indirmek için istedik.</span><span class="sxs-lookup"><span data-stu-id="3e226-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="3e226-108">Bölüm 1 - hello yeni kimlik bilgileri kümesi hazırlama:</span><span class="sxs-lookup"><span data-stu-id="3e226-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="3e226-109">Giriş/Çıkış izleyen geçerli toohello parçasıdır:</span><span class="sxs-lookup"><span data-stu-id="3e226-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="3e226-110">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-110">Blob Storage</span></span>
* <span data-ttu-id="3e226-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3e226-111">Event Hubs</span></span>
* <span data-ttu-id="3e226-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e226-112">SQL Database</span></span>
* <span data-ttu-id="3e226-113">Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-113">Table Storage</span></span>

<span data-ttu-id="3e226-114">Diğer giriş/çıkış için bölüm 2 ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="3e226-115">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="3e226-116">Toohello depolama uzantı hello Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="3e226-118">İş tarafından kullanılan hello depolama bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="3e226-120">Merhaba erişim anahtarlarını Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="3e226-122">Merhaba birincil erişim anahtarını hello ikincil erişim anahtarını arasındaki **hello bir iş tarafından kullanılmayan çekme**.</span><span class="sxs-lookup"><span data-stu-id="3e226-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="3e226-123">İsabet yeniden:</span><span class="sxs-lookup"><span data-stu-id="3e226-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="3e226-125">Yeni oluşturulan hello anahtarı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="3e226-127">TooPart 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="3e226-128">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="3e226-128">Event hubs</span></span>
1. <span data-ttu-id="3e226-129">Toohello Service Bus uzantısı hello Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="3e226-131">Hizmet veri yolu, iş tarafından kullanılan Namespace Hello bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="3e226-133">İşinizi Service Bus Namespace hello üzerinde bir paylaşılan erişim ilkesi kullanıyorsa, toostep 6 atlama</span><span class="sxs-lookup"><span data-stu-id="3e226-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="3e226-134">Toohello olay hub'ları sekmesine gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="3e226-136">Merhaba, iş tarafından kullanılan olay hub'ı bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="3e226-138">Toohello yapılandırma sekmesine gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="3e226-140">Hello ilkesi adı açılan, iş tarafından kullanılan hello Paylaşılan Erişim İlkesi'ni bulun:</span><span class="sxs-lookup"><span data-stu-id="3e226-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="3e226-142">Merhaba birincil anahtar ve ikincil anahtar hello arasında **hello bir iş tarafından kullanılmayan çekme**.</span><span class="sxs-lookup"><span data-stu-id="3e226-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="3e226-143">İsabet yeniden:</span><span class="sxs-lookup"><span data-stu-id="3e226-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="3e226-145">Yeni oluşturulan hello anahtarı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="3e226-147">TooPart 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="3e226-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e226-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="3e226-149">Not: tooconnect toohello SQL veritabanı hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e226-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="3e226-150">Biz tooshow kullanarak bu toodo hello nasıl yönetim deneyimi Azure Yönetim Portalı hello ancak SQL Server Management Studio gibi bazı istemci-tarafı aracı da toouse seçebilirsiniz adımıdır.</span><span class="sxs-lookup"><span data-stu-id="3e226-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="3e226-151">Toohello SQL veritabanları uzantısı hello Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="3e226-153">Merhaba, iş tarafından kullanılan SQL veritabanını bulun ve **hello sunucusunda** hello üzerinde aynı bağlantı satır:</span><span class="sxs-lookup"><span data-stu-id="3e226-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="3e226-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="3e226-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="3e226-155">Merhaba Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="3e226-157">Veritabanı Yöneticisi türü:</span><span class="sxs-lookup"><span data-stu-id="3e226-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="3e226-159">Kullanıcı adınızı, parolanızı yazın ve günlük tıklayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="3e226-161">Yeni sorgu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="3e226-163">< Login_name > sorgu değiştirerek aşağıdaki kullanıcı adınızı ve değiştirme hello türü <enterStrongPasswordHere> yeni parolanızla:</span><span class="sxs-lookup"><span data-stu-id="3e226-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="3e226-164">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="3e226-166">Toostep 2 geri dönün ve bu süre, hello veritabanı'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="3e226-168">Merhaba Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="3e226-170">Kullanıcı adınızı, parolanızı girin ve oturum açma'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="3e226-172">Yeni sorgu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="3e226-174">Merhaba < Kullanıcı_adı > sorgu değiştirerek aşağıdaki tooidentify tarafından istediğiniz bir adla hello bağlamında bu veritabanı bu oturum açma yazın (size sağlayabilir hello verdiğiniz < login_name için >, örneğin aynı değere) ve < login_name > ile değiştirme Yeni kullanıcı adı:</span><span class="sxs-lookup"><span data-stu-id="3e226-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="3e226-175">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="3e226-177">Şimdi yeni kullanıcı ile Merhaba sağlamalıdır aynı rolleri ve ayrıcalıkları, özgün kullanıcıya vardı.</span><span class="sxs-lookup"><span data-stu-id="3e226-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="3e226-178">TooPart 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="3e226-179">2. Kısım: Durdurma hello akış analizi işi</span><span class="sxs-lookup"><span data-stu-id="3e226-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="3e226-180">Toohello Stream Analytics uzantısı hello Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="3e226-182">İşinizi bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="3e226-184">Toohello girişleri veya olup bir giriş veya çıkış hello kimlik bilgileri döndürme dayalı hello çıkışları sekmesinde gidin.</span><span class="sxs-lookup"><span data-stu-id="3e226-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="3e226-186">Merhaba Durdur komutu tıklatın ve hello işi durduruldu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="3e226-187">![graphic29][graphic29] hello iş toostop için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3e226-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="3e226-188">Bulun hello giriş/çıkış istediğiniz toorotate kimlik bilgileri açık ve Git içine:</span><span class="sxs-lookup"><span data-stu-id="3e226-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="3e226-190">TooPart 3 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="3e226-191">3. Kısım: Hello akış analizi işi hello kimlik düzenleme</span><span class="sxs-lookup"><span data-stu-id="3e226-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="3e226-192">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="3e226-193">Merhaba depolama hesabı anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="3e226-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="3e226-195">Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="3e226-197">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatacak olan emin olun başarıyla geçti.</span><span class="sxs-lookup"><span data-stu-id="3e226-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="3e226-198">TooPart 4 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="3e226-199">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="3e226-199">Event hubs</span></span>
1. <span data-ttu-id="3e226-200">Merhaba olay hub'ı İlkesi anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="3e226-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="3e226-202">Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="3e226-204">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e226-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="3e226-205">TooPart 4 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="3e226-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="3e226-206">Power BI</span></span>
1. <span data-ttu-id="3e226-207">Merhaba yenileme yetkilendirme tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="3e226-209">Hello aşağıdaki onay iletisini alırsınız:</span><span class="sxs-lookup"><span data-stu-id="3e226-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="3e226-211">Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="3e226-213">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak, emin olun, başarıyla geçti.</span><span class="sxs-lookup"><span data-stu-id="3e226-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="3e226-214">TooPart 4 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="3e226-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e226-215">SQL Database</span></span>
1. <span data-ttu-id="3e226-216">Kullanıcı adı ve parola alanlarına Hello bulur ve yeni oluşturulan kimlik bilgileri kümesini kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="3e226-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="3e226-218">Merhaba Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="3e226-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="3e226-220">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.</span><span class="sxs-lookup"><span data-stu-id="3e226-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="3e226-221">TooPart 4 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="3e226-222">4. Kısım: işinizi son durdurulma saatten başlayarak</span><span class="sxs-lookup"><span data-stu-id="3e226-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="3e226-223">Giriş/Çıkış Hello uzağa doğru gidin:</span><span class="sxs-lookup"><span data-stu-id="3e226-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="3e226-225">Merhaba Başlat komutu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="3e226-227">Merhaba son durdurulma zamanı seçin ve Tamam'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="3e226-229">TooPart 5 devam edin.</span><span class="sxs-lookup"><span data-stu-id="3e226-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="3e226-230">5. Kısım: Kaldırma hello eski kimlik bilgileri kümesi</span><span class="sxs-lookup"><span data-stu-id="3e226-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="3e226-231">Giriş/Çıkış izleyen geçerli toohello parçasıdır:</span><span class="sxs-lookup"><span data-stu-id="3e226-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="3e226-232">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-232">Blob Storage</span></span>
* <span data-ttu-id="3e226-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3e226-233">Event Hubs</span></span>
* <span data-ttu-id="3e226-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e226-234">SQL Database</span></span>
* <span data-ttu-id="3e226-235">Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="3e226-236">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="3e226-236">Blob storage/Table storage</span></span>
<span data-ttu-id="3e226-237">1. Bölüm hello işinizi tarafından daha önce kullanılmış erişim anahtarı için yineleyin toorenew hello artık kullanılmayan erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3e226-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="3e226-238">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="3e226-238">Event hubs</span></span>
<span data-ttu-id="3e226-239">1. Bölüm hello işinizi tarafından daha önce kullanılmış anahtarı için yineleyin toorenew hello artık kullanılmayan anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3e226-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="3e226-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="3e226-240">SQL Database</span></span>
1. <span data-ttu-id="3e226-241">Bölümü 1 adım 7 ve sorgu aşağıdaki, < previous_login_name > Merhaba, iş tarafından daha önce kullanılmış bir kullanıcı adı ile değiştirerek hello türü toohello sorgu penceresine dönün:</span><span class="sxs-lookup"><span data-stu-id="3e226-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="3e226-242">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="3e226-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="3e226-244">Onay aşağıdaki hello almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="3e226-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="3e226-245">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="3e226-245">Get help</span></span>
<span data-ttu-id="3e226-246">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="3e226-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e226-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e226-247">Next steps</span></span>
* [<span data-ttu-id="3e226-248">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="3e226-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3e226-249">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3e226-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3e226-250">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="3e226-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3e226-251">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="3e226-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3e226-252">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="3e226-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

