---
title: Notification Hubs Java ile kullanma
description: "Bir Java arka ucunu Azure bildirim hub'ları kullanmayı öğrenin."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 41f978750ddef9f7e878c65b0017e909720154aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-notification-hubs-from-java"></a><span data-ttu-id="ab4a4-103">Java'dan Notification Hubs kullanma</span><span class="sxs-lookup"><span data-stu-id="ab4a4-103">How to use Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="ab4a4-104">Bu konu, yeni tam olarak desteklenen resmi Azure Notification Hub Java SDK'sı anahtar özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-104">This topic describes the key features of the new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="ab4a4-105">Bu açık kaynaklı proje ve tüm SDK koda görüntüleyebilirsiniz [Java SDK'sı].</span><span class="sxs-lookup"><span data-stu-id="ab4a4-105">This is an open source project and you can view the entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="ab4a4-106">Genel olarak, bir Java/PHP/Python/Ruby MSDN konusunda açıklandığı gibi bildirim hub'ı REST arabirimini kullanarak uç tüm bildirim hub'ları özellikleri erişebileceğiniz [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab4a4-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using the Notification Hub REST interface as described in the MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="ab4a4-107">Bu Java SDK'sı, Java bu REST arabirimleri üzerinden ince sarmalayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="ab4a4-108">SDK'sı şu anda destekler:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-108">The SDK supports currently:</span></span>

* <span data-ttu-id="ab4a4-109">Bildirim hub'ları üzerinde CRUD</span><span class="sxs-lookup"><span data-stu-id="ab4a4-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="ab4a4-110">CRUD kayıtlar hakkında</span><span class="sxs-lookup"><span data-stu-id="ab4a4-110">CRUD on Registrations</span></span>
* <span data-ttu-id="ab4a4-111">Yükleme Yönetimi</span><span class="sxs-lookup"><span data-stu-id="ab4a4-111">Installation Management</span></span>
* <span data-ttu-id="ab4a4-112">Kayıtlar içeri/dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ab4a4-112">Import/Export Registrations</span></span>
* <span data-ttu-id="ab4a4-113">Normal gönderir</span><span class="sxs-lookup"><span data-stu-id="ab4a4-113">Regular Sends</span></span>
* <span data-ttu-id="ab4a4-114">Zamanlanmış gönderir</span><span class="sxs-lookup"><span data-stu-id="ab4a4-114">Scheduled Sends</span></span>
* <span data-ttu-id="ab4a4-115">Java NIO üzerinden zaman uyumsuz işlemler</span><span class="sxs-lookup"><span data-stu-id="ab4a4-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="ab4a4-116">Desteklenen platformlar: APNS (iOS), GCM (Android), WNS (Windows mağazası uygulamaları), MPNS (Windows Phone), ADM (Amazon Kindle yangın), Baidu (Android Google Hizmetleri olmadan)</span><span class="sxs-lookup"><span data-stu-id="ab4a4-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="ab4a4-117">SDK kullanımı</span><span class="sxs-lookup"><span data-stu-id="ab4a4-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="ab4a4-118">Derleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab4a4-118">Compile and build</span></span>
<span data-ttu-id="ab4a4-119">Kullanım [Maven]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-119">Use [Maven]</span></span>

<span data-ttu-id="ab4a4-120">Oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-120">To build:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="ab4a4-121">Kod</span><span class="sxs-lookup"><span data-stu-id="ab4a4-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="ab4a4-122">Bildirim hub'ı CRUDs</span><span class="sxs-lookup"><span data-stu-id="ab4a4-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="ab4a4-123">**Bir NamespaceManager oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="ab4a4-124">**Bildirim hub'ı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="ab4a4-125">OR</span><span class="sxs-lookup"><span data-stu-id="ab4a4-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="ab4a4-126">**Bildirim hub'ı alın:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="ab4a4-127">**Bildirim hub'ı güncelleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="ab4a4-128">**Bildirim hub'ı silin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="ab4a4-129">Kayıt CRUDs</span><span class="sxs-lookup"><span data-stu-id="ab4a4-129">Registration CRUDs</span></span>
<span data-ttu-id="ab4a4-130">**Bir bildirim hub'ı istemci oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="ab4a4-131">**Windows kaydı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="ab4a4-132">**İOS kaydı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="ab4a4-133">Benzer şekilde, Android (GCM), Windows Phone (MPNS) ve Kindle yangın (ADM) kayıtlar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="ab4a4-134">**Şablon kayıtları oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="ab4a4-135">**Kayıtlar oluşturmak kullanarak oluşturduğunuz RegistrationId + upsert düzeni**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="ab4a4-136">Kayıp yanıtları nedeniyle yinelenen kaydı kimlikleri aygıtta depolanıyorsa kaldırır:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-136">Removes duplicates due to any lost responses if storing registration ids on the device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="ab4a4-137">**Kayıtlar güncelleştirin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="ab4a4-138">**Kayıtları silin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="ab4a4-139">**Sorgu kayıtları:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-139">**Query registrations:**</span></span>

* <span data-ttu-id="ab4a4-140">**Tek kayıt alın:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="ab4a4-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="ab4a4-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="ab4a4-142">**Tüm kayıtlar hub alın:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="ab4a4-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="ab4a4-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="ab4a4-144">**Kayıtlar etiketiyle alın:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="ab4a4-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="ab4a4-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="ab4a4-146">**Kayıtlar kanal tarafından alın:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="ab4a4-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="ab4a4-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="ab4a4-148">Tüm koleksiyon sorgular, $top ve devamlılık belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="ab4a4-149">Yükleme API kullanımı</span><span class="sxs-lookup"><span data-stu-id="ab4a4-149">Installation API usage</span></span>
<span data-ttu-id="ab4a4-150">API kayıt yönetimi için alternatif bir mekanizma yüklemesidir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="ab4a4-151">Önemsiz olmayan ve kolayca yanlış veya inefficiently yapılabilir birden çok kayıtlar koruma yerine artık tek bir yükleme nesnesini kullanmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible to use a SINGLE Installation object.</span></span> <span data-ttu-id="ab4a4-152">Yükleme ihtiyaç duyduğunuz her şeyi içerir: itme kanal (cihaz belirteci), etiketler, şablonlar, ikincil döşeme (WNS ve APNS için).</span><span class="sxs-lookup"><span data-stu-id="ab4a4-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="ab4a4-153">Kimliği artık get - yalnızca GUID veya başka bir tanımlayıcı oluşturmak, cihazda tutmak ve anında iletme kanal (cihaz belirteci) ile birlikte arka göndermek için hizmetini çağırmak gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-153">You don't need to call the service to get Id anymore - just generate GUID or any other identifier, keep it on device and send to your backend together with push channel (device token).</span></span> <span data-ttu-id="ab4a4-154">Arka uçta yalnızca tek bir çağrı yapmanız gerekir: CreateOrUpdateInstallation, onu tam olarak ıdempotent, böylece gerektiğinde yeniden deneme çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-154">On the backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free to retry if needed.</span></span>

<span data-ttu-id="ab4a4-155">Örneğin, Amazon Kindle yangın olarak şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="ab4a4-156">Güncelleştirmek istiyorsanız:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-156">If you want to update it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="ab4a4-157">Gelişmiş senaryolar için yükleme nesnesi yalnızca belirli özelliklerini değiştirmek için sağlayan kısmi güncelleştirme yeteneği sahip.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-157">For advanced scenarios we have partial update capability which allows to modify only particular properties of the installation object.</span></span> <span data-ttu-id="ab4a4-158">Temel kısmi güncelleştirme yükleme nesnesi karşı çalıştırabilirsiniz JSON düzeltme işlemleri alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="ab4a4-159">Yükleme Sil:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="ab4a4-160">CreateOrUpdate, düzeltme eki ve Delete sonunda Get ile tutarlı değil.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="ab4a4-161">İstenen işlem yalnızca çağrı sırasında sistem kuyruğa gider ve arka planda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-161">Your requested operation just goes to the system queue during the call and will be executed in background.</span></span> <span data-ttu-id="ab4a4-162">Get ana çalışma zamanı senaryosu için ancak yalnızca hata ayıklama ve sorun giderme amacıyla için tasarlanmamıştır, sıkı bir şekilde hizmet tarafından kısıtlanan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by the service.</span></span>

<span data-ttu-id="ab4a4-163">Yüklemeleri için gönderme akışı kayıtlar ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-163">Send flow for Installations is the same as for Registrations.</span></span> <span data-ttu-id="ab4a4-164">Biz yalnızca belirli yüklemeyi bildirim hedef - yalnızca etiket kullanmak için bir seçenek ekledik "InstallationID: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="ab4a4-164">We've just introduced an option to target notification to the particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="ab4a4-165">Servis talebi için yukarıdaki onu şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="ab4a4-166">Biri çeşitli şablonlar için:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="ab4a4-167">Bildirimleri (standart katmanı için kullanılabilir) zamanlama</span><span class="sxs-lookup"><span data-stu-id="ab4a4-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="ab4a4-168">Aynı normal gönderme ancak bir ek parametre - bildirim teslim zaman gerektirdiğinizde scheduledTime.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-168">The same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="ab4a4-169">Hizmet şimdi + 5 dakika arasında geçen süreyi herhangi bir noktasını kabul eder ve şimdi + 7 gün.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="ab4a4-170">**Windows yerel bildirim zamanla:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="ab4a4-171">İçeri/dışarı aktarma (standart katmanı için kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="ab4a4-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="ab4a4-172">Bazen kayıtlar karşı toplu işlemi gerçekleştirmek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-172">Sometimes it is required to perform bulk operation against registrations.</span></span> <span data-ttu-id="ab4a4-173">Genellikle başka bir sistemi ile tümleştirme için veya yalnızca yoğun düzeltme söylemek için etiketler güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-173">Usually it is for integration with another system or just a massive fix to say update the tags.</span></span> <span data-ttu-id="ab4a4-174">Biz kayıtlar binlerce hakkında konuşurken Get/güncelleştirme akış kullanılacak önerilen kesin değildir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-174">It is strongly not recommended to use Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="ab4a4-175">İçeri/dışarı aktarma yeteneği senaryo karşılamak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-175">Import/Export capability is designed to cover the scenario.</span></span> <span data-ttu-id="ab4a4-176">Temel olarak, bir erişim bazı blob kapsayıcısı için depolama hesabınızın altında bir gelen veri kaynağı ve çıkış konumu olarak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-176">Basically you provide an access to some blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="ab4a4-177">**Dışarı aktarma işini gönder:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="ab4a4-178">**İçe aktarma işi gönder:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="ab4a4-179">**İş tamamlanana kadar bekleyin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="ab4a4-180">**Tüm işleri görüntüleyin:**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="ab4a4-181">**SAS imzayla URI:** bazı blob dosya veya blob kapsayıcı URL'si artı izinleri ve süre sonu gibi parametreleri kümesini artı hesabın SAS anahtarı kullanılarak yapılan tüm bu işlemler imzası budur.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-181">**URI with SAS signature:** This is the URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="ab4a4-182">Azure depolama Java SDK'sı, bu tür bir URI oluşturma dahil olmak üzere Zengin özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="ab4a4-183">Basit alternatif olarak algoritmasını imzalamanın çok temel ve compact uygulaması olan ImportExportE2E test sınıfı (github konumdan) göz atın.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-183">As simple alternative you can take a look at ImportExportE2E test class (from the github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="ab4a4-184">Bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="ab4a4-184">Send Notifications</span></span>
<span data-ttu-id="ab4a4-185">Bildirim nesnesi yalnızca üstbilgileri gövde, bazı yardımcı program yöntemleri yerel ve şablon bildirimleri nesneleri oluşturmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-185">The Notification object is simply a body with headers, some utility methods help in building the native and template notifications objects.</span></span>

* <span data-ttu-id="ab4a4-186">**Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="ab4a4-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="ab4a4-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="ab4a4-189">**Windows Phone 8.0 ve 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="ab4a4-190">**Yangın kindle**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="ab4a4-191">**Etiketleri Gönder**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-191">**Send to Tags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="ab4a4-192">**Etiket ifadesi Gönder**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-192">**Send to tag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="ab4a4-193">**Şablon bildirim gönder**</span><span class="sxs-lookup"><span data-stu-id="ab4a4-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="ab4a4-194">Java Kodunuzu çalıştırmaya şimdi, hedef cihazda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="ab4a4-195"><a name="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ab4a4-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="ab4a4-196">Bu konuda size bildirim hub'ları için basit bir Java REST istemcisi nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-196">In this topic we showed how to create a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="ab4a4-197">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-197">From here you can:</span></span>

* <span data-ttu-id="ab4a4-198">Tam karşıdan [Java SDK'sı], tüm SDK kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="ab4a4-198">Download the full [Java SDK], which contains the entire SDK code.</span></span> 
* <span data-ttu-id="ab4a4-199">Örneklerle Yürüt:</span><span class="sxs-lookup"><span data-stu-id="ab4a4-199">Play with the samples:</span></span>
  * <span data-ttu-id="ab4a4-200">[Notification Hubs ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="ab4a4-201">[Son dakika haberleri göndermek]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-201">[Send breaking news]</span></span>
  * <span data-ttu-id="ab4a4-202">[Yerelleştirilmiş son dakika haberleri göndermek]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="ab4a4-203">[Kimliği doğrulanmış kullanıcılara bildirim göndermek]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-203">[Send notifications to authenticated users]</span></span>
  * <span data-ttu-id="ab4a4-204">[Kimliği doğrulanmış kullanıcılara platformlar arası bildirimleri gönderin]</span><span class="sxs-lookup"><span data-stu-id="ab4a4-204">[Send cross-platform notifications to authenticated users]</span></span>

<span data-ttu-id="ab4a4-205">[Java SDK'sı]: https://github.com/Azure/azure-notificationhubs-java-backend</span><span class="sxs-lookup"><span data-stu-id="ab4a4-205">[Java SDK]: https://github.com/Azure/azure-notificationhubs-java-backend</span></span>
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
<span data-ttu-id="ab4a4-206">[Notification Hubs ile çalışmaya başlama]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-206">[Get Started with Notification Hubs]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/</span></span>
<span data-ttu-id="ab4a4-207">[Son dakika haberleri göndermek]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-207">[Send breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/</span></span>
<span data-ttu-id="ab4a4-208">[Yerelleştirilmiş son dakika haberleri göndermek]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-208">[Send localized breaking news]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
<span data-ttu-id="ab4a4-209">[Kimliği doğrulanmış kullanıcılara bildirim göndermek]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-209">[Send notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/</span></span>
<span data-ttu-id="ab4a4-210">[Kimliği doğrulanmış kullanıcılara platformlar arası bildirimleri gönderin]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-210">[Send cross-platform notifications to authenticated users]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/</span></span>
<span data-ttu-id="ab4a4-211">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="ab4a4-211">[Maven]: http://maven.apache.org/</span></span>

