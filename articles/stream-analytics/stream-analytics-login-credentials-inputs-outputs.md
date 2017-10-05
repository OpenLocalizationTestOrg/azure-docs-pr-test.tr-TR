---
title: "Akış analizi: oturum açma kimlik bilgilerini girişleri ve çıkışları döndürme | Microsoft Docs"
description: "Stream Analytics girişleri ve çıkışları için kimlik bilgilerini güncelleştirme konusunda bilgi edinin."
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
ms.openlocfilehash: 2cb995a3969a8cb025f371ed0ab160cd04b0454d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="a35da-104">Giriş ve çıkış akış analizi işleri, oturum açma kimlik bilgileri döndürün</span><span class="sxs-lookup"><span data-stu-id="a35da-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="a35da-105">Özet</span><span class="sxs-lookup"><span data-stu-id="a35da-105">Abstract</span></span>
<span data-ttu-id="a35da-106">Azure Stream Analytics işi devam ederken bir giriş/çıkış kimlik bilgilerini değiştirme bugün izin vermez.</span><span class="sxs-lookup"><span data-stu-id="a35da-106">Azure Stream Analytics today doesn’t allow replacing the credentials on an input/output while the job is running.</span></span>

<span data-ttu-id="a35da-107">Azure Stream Analytics işi son çıktısından desteklerken, tüm işlem durdurma arasındaki gecikmesini en aza indirmenizi ve işini başlatma ve oturum açma kimlik bilgilerini döndürme paylaşmak istedi.</span><span class="sxs-lookup"><span data-stu-id="a35da-107">While Azure Stream Analytics does support resuming a job from last output, we wanted to share the entire process for minimizing the lag between the stopping and starting of the job and rotating the login credentials.</span></span>

## <a name="part-1---prepare-the-new-set-of-credentials"></a><span data-ttu-id="a35da-108">Bölüm 1 - yeni kimlik bilgileri kümesi hazırlama:</span><span class="sxs-lookup"><span data-stu-id="a35da-108">Part 1 - Prepare the new set of credentials:</span></span>
<span data-ttu-id="a35da-109">Bu bölümü aşağıdaki girdi/çıktı geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="a35da-109">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="a35da-110">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-110">Blob Storage</span></span>
* <span data-ttu-id="a35da-111">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a35da-111">Event Hubs</span></span>
* <span data-ttu-id="a35da-112">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a35da-112">SQL Database</span></span>
* <span data-ttu-id="a35da-113">Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-113">Table Storage</span></span>

<span data-ttu-id="a35da-114">Diğer giriş/çıkış için bölüm 2 ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="a35da-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="a35da-115">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="a35da-116">Depolama uzantı Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-116">Go to the Storage extention on the Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="a35da-118">İş tarafından kullanılan depolama alanını bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-118">Locate the storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="a35da-120">Erişim anahtarlarını Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-120">Click the Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="a35da-122">Birincil erişim anahtarı ve ikincil erişim tuşunu arasında **işinizi tarafından kullanılmayan bir çekme**.</span><span class="sxs-lookup"><span data-stu-id="a35da-122">Between the Primary Access Key and the Secondary Access Key, **pick the one not used by your job**.</span></span>
5. <span data-ttu-id="a35da-123">İsabet yeniden:</span><span class="sxs-lookup"><span data-stu-id="a35da-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="a35da-125">Yeni oluşturulan anahtarı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-125">Copy the newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="a35da-127">Bölüm 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="a35da-127">Continue to Part 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a35da-128">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="a35da-128">Event hubs</span></span>
1. <span data-ttu-id="a35da-129">Hizmet veri yolu uzantısı Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-129">Go to the Service Bus extension on the Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="a35da-131">Hizmet veri yolu, iş tarafından kullanılan Namespace bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-131">Locate the Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="a35da-133">İşinizi üzerinde hizmet veri yolu Namespace bir paylaşılan erişim ilkesi kullanıyorsa, adım 6 atlama</span><span class="sxs-lookup"><span data-stu-id="a35da-133">If your job uses a shared access policy on the Service Bus Namespace, jump to step 6</span></span>  
4. <span data-ttu-id="a35da-134">Olay hub'ları sekmesine gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-134">Go to the Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="a35da-136">İş tarafından kullanılan olay hub'ı bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-136">Locate the Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="a35da-138">Yapılandırma sekmesine gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-138">Go to the Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="a35da-140">İlke adı açılan üzerinde iş tarafından kullanılan paylaşılan erişim ilkesi'ni bulun:</span><span class="sxs-lookup"><span data-stu-id="a35da-140">On the Policy Name drop-down, locate the shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="a35da-142">Birincil anahtar ve ikincil anahtar arasındaki **işinizi tarafından kullanılmayan bir çekme**.</span><span class="sxs-lookup"><span data-stu-id="a35da-142">Between the Primary Key and the Secondary Key, **pick the one not used by your job**.</span></span>  
9. <span data-ttu-id="a35da-143">İsabet yeniden:</span><span class="sxs-lookup"><span data-stu-id="a35da-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="a35da-145">Yeni oluşturulan anahtarı kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-145">Copy the newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="a35da-147">Bölüm 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="a35da-147">Continue to Part 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="a35da-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a35da-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="a35da-149">Not: SQL veritabanı hizmetine bağlanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="a35da-149">Note: you will need to connect to the SQL Database Service.</span></span> <span data-ttu-id="a35da-150">Biz yönetim deneyimi üzerinde Azure Yönetim Portalı'nı kullanarak bunu göstermek için kullanacaksanız, ancak SQL Server Management Studio gibi bazı istemci-tarafı aracı da kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a35da-150">We are going to show how to do this using the management experience on the Azure Management portal but you may choose to use some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="a35da-151">SQL veritabanları uzantısı Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-151">Go to the SQL Databases extension on the Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="a35da-153">İş tarafından kullanılan SQL veritabanını bulun ve **sunucusunda** aynı satırda bağlantı:</span><span class="sxs-lookup"><span data-stu-id="a35da-153">Locate the SQL Database used by your job and **click on the server** link on the same line:</span></span>  
   <span data-ttu-id="a35da-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="a35da-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="a35da-155">Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-155">Click the Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="a35da-157">Veritabanı Yöneticisi türü:</span><span class="sxs-lookup"><span data-stu-id="a35da-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="a35da-159">Kullanıcı adınızı, parolanızı yazın ve günlük tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="a35da-161">Yeni sorgu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="a35da-163">Aşağıdaki sorguda < login_name >, kullanıcı adıyla değiştirerek ve değiştirme türü <enterStrongPasswordHere> yeni parolanızla:</span><span class="sxs-lookup"><span data-stu-id="a35da-163">Type in the following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="a35da-164">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="a35da-166">Adım 2 ve bu süre tıklatın veritabanı dönün:</span><span class="sxs-lookup"><span data-stu-id="a35da-166">Go back to step 2 and this time click the database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="a35da-168">Yönet komutuna tıklayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-168">Click the Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="a35da-170">Kullanıcı adınızı, parolanızı girin ve oturum açma'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="a35da-172">Yeni sorgu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="a35da-174">Bu oturum açma (örneğin verdiğiniz < login_name > için aynı değer sağlayabilir) Bu veritabanı bağlamında tanımlamak istediğiniz bir adla < Kullanıcı_adı > değiştiriliyor ve değiştirerek aşağıdaki sorguyla < login_name > Yeni yazın Kullanıcı adı:</span><span class="sxs-lookup"><span data-stu-id="a35da-174">Type in the following query replacing <user_name> with a name by which you want to identify this login in the context of this database (you can provide the same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="a35da-175">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="a35da-177">Şimdi yeni kullanıcı aynı rolleri ve ayrıcalıkları, özgün kullanıcıya sahip sağlaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a35da-177">You should now provide your new user with the same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="a35da-178">Bölüm 2 devam edin.</span><span class="sxs-lookup"><span data-stu-id="a35da-178">Continue to Part 2.</span></span>

## <a name="part-2-stopping-the-stream-analytics-job"></a><span data-ttu-id="a35da-179">2. Kısım: akış analizi işi durdurma</span><span class="sxs-lookup"><span data-stu-id="a35da-179">Part 2: Stopping the Stream Analytics Job</span></span>
1. <span data-ttu-id="a35da-180">Stream Analytics uzantısı Azure yönetim portalında gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-180">Go to the Stream Analytics extension on the Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="a35da-182">İşinizi bulun ve uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="a35da-184">Girişleri sekmesini veya olup bir giriş veya çıkış kimlik bilgileri döndürme dayalı çıkışları gidin.</span><span class="sxs-lookup"><span data-stu-id="a35da-184">Go to the Inputs tab or the Outputs tab based on whether you are rotating the credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="a35da-186">Stop komutu tıklayın ve iş durduruldu onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-186">Click the Stop command and confirm the job has stopped:</span></span>  
   <span data-ttu-id="a35da-187">![graphic29][graphic29] işi durdurmak bekleyin.</span><span class="sxs-lookup"><span data-stu-id="a35da-187">![graphic29][graphic29] Wait for the job to stop.</span></span>
5. <span data-ttu-id="a35da-188">Kimlik bilgileri üzerindeki döndürün ve içine gitmek için istediğiniz giriş/çıkış bulun:</span><span class="sxs-lookup"><span data-stu-id="a35da-188">Locate the input/output you want to rotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="a35da-190">Bölüm 3 devam edin.</span><span class="sxs-lookup"><span data-stu-id="a35da-190">Proceed to Part 3.</span></span>

## <a name="part-3-editing-the-credentials-on-the-stream-analytics-job"></a><span data-ttu-id="a35da-191">3. Kısım: akış analizi işi kimlik bilgilerine düzenleme</span><span class="sxs-lookup"><span data-stu-id="a35da-191">Part 3: Editing the credentials on the Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="a35da-192">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="a35da-193">Depolama hesabı anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="a35da-193">Find the Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="a35da-195">Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-195">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="a35da-197">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatacak olan emin olun başarıyla geçti.</span><span class="sxs-lookup"><span data-stu-id="a35da-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="a35da-198">4 bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="a35da-198">Proceed to Part 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a35da-199">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="a35da-199">Event hubs</span></span>
1. <span data-ttu-id="a35da-200">Olay hub'ı İlkesi anahtarı alanını bulun ve yeni oluşturulan anahtarınızı yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="a35da-200">Find the Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="a35da-202">Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-202">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="a35da-204">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.</span><span class="sxs-lookup"><span data-stu-id="a35da-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="a35da-205">4 bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="a35da-205">Proceed to Part 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="a35da-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="a35da-206">Power BI</span></span>
1. <span data-ttu-id="a35da-207">Yenileme yetkilendirme tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-207">Click the Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="a35da-209">Aşağıdaki onay iletisini alırsınız:</span><span class="sxs-lookup"><span data-stu-id="a35da-209">You will get the following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="a35da-211">Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-211">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="a35da-213">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak, emin olun, başarıyla geçti.</span><span class="sxs-lookup"><span data-stu-id="a35da-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="a35da-214">4 bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="a35da-214">Proceed to Part 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="a35da-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a35da-215">SQL Database</span></span>
1. <span data-ttu-id="a35da-216">Kullanıcı adı ve parola alanlarına bulmak ve yeni oluşturulan kimlik bilgileri kümesini kopyalayıp yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="a35da-216">Find the User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="a35da-218">Kaydet komutuna tıklayın ve Değişikliklerinizi kaydetmeden onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a35da-218">Click the Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="a35da-220">Yaptığınız değişiklikleri kaydederken bir bağlantı testi otomatik olarak başlatılacak başarıyla geçti emin olun.</span><span class="sxs-lookup"><span data-stu-id="a35da-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="a35da-221">4 bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="a35da-221">Proceed to Part 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="a35da-222">4. Kısım: işinizi son durdurulma saatten başlayarak</span><span class="sxs-lookup"><span data-stu-id="a35da-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="a35da-223">Giriş/Çıkış uzağa doğru gidin:</span><span class="sxs-lookup"><span data-stu-id="a35da-223">Navigate away from the Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="a35da-225">Başlat komutu tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-225">Click the Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="a35da-227">Son durdurulma zamanı seçin ve Tamam'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-227">Pick the Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="a35da-229">5 bölümüne geçin.</span><span class="sxs-lookup"><span data-stu-id="a35da-229">Proceed to Part 5.</span></span>  

## <a name="part-5-removing-the-old-set-of-credentials"></a><span data-ttu-id="a35da-230">5. Kısım: eski kimlik bilgileri kümesi kaldırılıyor</span><span class="sxs-lookup"><span data-stu-id="a35da-230">Part 5: Removing the old set of credentials</span></span>
<span data-ttu-id="a35da-231">Bu bölümü aşağıdaki girdi/çıktı geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="a35da-231">This part is applicable to the following inputs/outputs:</span></span>

* <span data-ttu-id="a35da-232">Blob Depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-232">Blob Storage</span></span>
* <span data-ttu-id="a35da-233">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a35da-233">Event Hubs</span></span>
* <span data-ttu-id="a35da-234">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a35da-234">SQL Database</span></span>
* <span data-ttu-id="a35da-235">Tablo Depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="a35da-236">BLOB Depolama/tablo depolama</span><span class="sxs-lookup"><span data-stu-id="a35da-236">Blob storage/Table storage</span></span>
<span data-ttu-id="a35da-237">1. Bölüm artık kullanılmayan erişim anahtarını yenilemek için iş tarafından daha önce kullanılmış erişim anahtarı için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a35da-237">Repeat Part 1 for the Access Key that was previously used by your job to renew the now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="a35da-238">Olay hub'ları</span><span class="sxs-lookup"><span data-stu-id="a35da-238">Event hubs</span></span>
<span data-ttu-id="a35da-239">1. Bölüm artık kullanılmayan anahtarını yenilemek için iş tarafından daha önce kullanılmış anahtarı için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a35da-239">Repeat Part 1 for the Key that was previously used by your job to renew the now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="a35da-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="a35da-240">SQL Database</span></span>
1. <span data-ttu-id="a35da-241">Bölümü 1 adım 7 ve daha önce iş tarafından kullanılan kullanıcı adı < previous_login_name > yerine türü aşağıdaki sorguda, sorgu penceresine geri dönün:</span><span class="sxs-lookup"><span data-stu-id="a35da-241">Go back to the query window from Part 1 Step 7 and type in the following query, replacing <previous_login_name> with the User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="a35da-242">Çalıştır'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a35da-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="a35da-244">Aşağıdaki onay almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a35da-244">You should get the following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="a35da-245">Yardım alın</span><span class="sxs-lookup"><span data-stu-id="a35da-245">Get help</span></span>
<span data-ttu-id="a35da-246">Daha fazla yardım için [Azure Stream Analytics forumumuzu](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) deneyin.</span><span class="sxs-lookup"><span data-stu-id="a35da-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a35da-247">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a35da-247">Next steps</span></span>
* [<span data-ttu-id="a35da-248">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="a35da-248">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a35da-249">Azure Akış Analizi'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a35da-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a35da-250">Azure Akış Analizi işlerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a35da-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a35da-251">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a35da-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a35da-252">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a35da-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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

