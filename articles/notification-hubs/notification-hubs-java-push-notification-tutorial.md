---
title: aaaHow toouse Notification Hubs Java ile
description: "Bilgi nasıl toouse Azure Notification Hubs bir Java arka uçtan."
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
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="f1094-103">Nasıl toouse Java'dan Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="f1094-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="f1094-104">Bu konuda hello anahtar hello yeni tam olarak desteklenen resmi özelliklerini açıklayan Azure Notification Hub Java SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="f1094-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="f1094-105">Bu açık kaynaklı proje ve hello tüm SDK kodu görüntüleyebilirsiniz [Java SDK'sı].</span><span class="sxs-lookup"><span data-stu-id="f1094-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="f1094-106">Genel olarak, bir Java/PHP/Python/Ruby arka ucunu tüm bildirim hub'ları özelliklere erişebilir hello MSDN konuda açıklandığı gibi hello bildirim hub'ı REST arabirimini kullanarak [bildirim hub'ları REST API'leri](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1094-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="f1094-107">Bu Java SDK'sı, Java bu REST arabirimleri üzerinden ince sarmalayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f1094-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="f1094-108">Merhaba SDK'sı şu anda destekler:</span><span class="sxs-lookup"><span data-stu-id="f1094-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="f1094-109">Bildirim hub'ları üzerinde CRUD</span><span class="sxs-lookup"><span data-stu-id="f1094-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="f1094-110">CRUD kayıtlar hakkında</span><span class="sxs-lookup"><span data-stu-id="f1094-110">CRUD on Registrations</span></span>
* <span data-ttu-id="f1094-111">Yükleme Yönetimi</span><span class="sxs-lookup"><span data-stu-id="f1094-111">Installation Management</span></span>
* <span data-ttu-id="f1094-112">Kayıtlar içeri/dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="f1094-112">Import/Export Registrations</span></span>
* <span data-ttu-id="f1094-113">Normal gönderir</span><span class="sxs-lookup"><span data-stu-id="f1094-113">Regular Sends</span></span>
* <span data-ttu-id="f1094-114">Zamanlanmış gönderir</span><span class="sxs-lookup"><span data-stu-id="f1094-114">Scheduled Sends</span></span>
* <span data-ttu-id="f1094-115">Java NIO üzerinden zaman uyumsuz işlemler</span><span class="sxs-lookup"><span data-stu-id="f1094-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="f1094-116">Desteklenen platformlar: APNS (iOS), GCM (Android), WNS (Windows mağazası uygulamaları), MPNS (Windows Phone), ADM (Amazon Kindle yangın), Baidu (Android Google Hizmetleri olmadan)</span><span class="sxs-lookup"><span data-stu-id="f1094-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="f1094-117">SDK kullanımı</span><span class="sxs-lookup"><span data-stu-id="f1094-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="f1094-118">Derleme ve oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1094-118">Compile and build</span></span>
<span data-ttu-id="f1094-119">Kullanım [Maven]</span><span class="sxs-lookup"><span data-stu-id="f1094-119">Use [Maven]</span></span>

<span data-ttu-id="f1094-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="f1094-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="f1094-121">Kod</span><span class="sxs-lookup"><span data-stu-id="f1094-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="f1094-122">Bildirim hub'ı CRUDs</span><span class="sxs-lookup"><span data-stu-id="f1094-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="f1094-123">**Bir NamespaceManager oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="f1094-124">**Bildirim hub'ı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="f1094-125">OR</span><span class="sxs-lookup"><span data-stu-id="f1094-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="f1094-126">**Bildirim hub'ı alın:**</span><span class="sxs-lookup"><span data-stu-id="f1094-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="f1094-127">**Bildirim hub'ı güncelleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="f1094-128">**Bildirim hub'ı silin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="f1094-129">Kayıt CRUDs</span><span class="sxs-lookup"><span data-stu-id="f1094-129">Registration CRUDs</span></span>
<span data-ttu-id="f1094-130">**Bir bildirim hub'ı istemci oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="f1094-131">**Windows kaydı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="f1094-132">**İOS kaydı oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="f1094-133">Benzer şekilde, Android (GCM), Windows Phone (MPNS) ve Kindle yangın (ADM) kayıtlar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f1094-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="f1094-134">**Şablon kayıtları oluşturun:**</span><span class="sxs-lookup"><span data-stu-id="f1094-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="f1094-135">**Kayıtlar oluşturmak kullanarak oluşturduğunuz RegistrationId + upsert düzeni**</span><span class="sxs-lookup"><span data-stu-id="f1094-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="f1094-136">Kayıp tooany yanıtları son çoğaltmaları kaydı kimlikleri hello aygıtta depolanıyorsa kaldırır:</span><span class="sxs-lookup"><span data-stu-id="f1094-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="f1094-137">**Kayıtlar güncelleştirin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="f1094-138">**Kayıtları silin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="f1094-139">**Sorgu kayıtları:**</span><span class="sxs-lookup"><span data-stu-id="f1094-139">**Query registrations:**</span></span>

* <span data-ttu-id="f1094-140">**Tek kayıt alın:**</span><span class="sxs-lookup"><span data-stu-id="f1094-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="f1094-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="f1094-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="f1094-142">**Tüm kayıtlar hub alın:**</span><span class="sxs-lookup"><span data-stu-id="f1094-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="f1094-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="f1094-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="f1094-144">**Kayıtlar etiketiyle alın:**</span><span class="sxs-lookup"><span data-stu-id="f1094-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="f1094-145">hub.getRegistrationsByTag("myTag");</span><span class="sxs-lookup"><span data-stu-id="f1094-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="f1094-146">**Kayıtlar kanal tarafından alın:**</span><span class="sxs-lookup"><span data-stu-id="f1094-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="f1094-147">hub.getRegistrationsByChannel("devicetoken");</span><span class="sxs-lookup"><span data-stu-id="f1094-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="f1094-148">Tüm koleksiyon sorgular, $top ve devamlılık belirteçleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f1094-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="f1094-149">Yükleme API kullanımı</span><span class="sxs-lookup"><span data-stu-id="f1094-149">Installation API usage</span></span>
<span data-ttu-id="f1094-150">API kayıt yönetimi için alternatif bir mekanizma yüklemesidir.</span><span class="sxs-lookup"><span data-stu-id="f1094-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="f1094-151">Önemsiz olmayan ve kolayca yanlış veya inefficiently yapılabilir birden çok kayıtlar koruma yerine onu olası toouse tek yükleme nesnesi sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="f1094-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="f1094-152">Yükleme ihtiyaç duyduğunuz her şeyi içerir: itme kanal (cihaz belirteci), etiketler, şablonlar, ikincil döşeme (WNS ve APNS için).</span><span class="sxs-lookup"><span data-stu-id="f1094-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="f1094-153">Toocall hello hizmet tooget kimliği artık gerekmeyen - yalnızca GUID veya başka bir tanımlayıcı oluşturmak, cihazda tutmak ve anında iletme kanal (cihaz belirteci) ile birlikte tooyour arka uç gönderin.</span><span class="sxs-lookup"><span data-stu-id="f1094-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="f1094-154">Merhaba arka uçta yalnızca tek bir çağrı yapmanız gerekir: CreateOrUpdateInstallation, onu tam olarak ıdempotent, bu nedenle sağladığı ücretsiz tooretry gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="f1094-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="f1094-155">Örneğin, Amazon Kindle yangın olarak şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="f1094-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="f1094-156">Tooupdate istiyorsanız bunu:</span><span class="sxs-lookup"><span data-stu-id="f1094-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="f1094-157">Gelişmiş senaryolar için biz yalnızca belirli özellikleri hello yükleme nesnesi toomodify veren kısmi güncelleştirme özelliğine sahip.</span><span class="sxs-lookup"><span data-stu-id="f1094-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="f1094-158">Temel kısmi güncelleştirme yükleme nesnesi karşı çalıştırabilirsiniz JSON düzeltme işlemleri alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="f1094-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="f1094-159">Yükleme Sil:</span><span class="sxs-lookup"><span data-stu-id="f1094-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="f1094-160">CreateOrUpdate, düzeltme eki ve Delete sonunda Get ile tutarlı değil.</span><span class="sxs-lookup"><span data-stu-id="f1094-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="f1094-161">İstenen işlem yalnızca toohello sistem sırası hello araması sırasında gider ve arka planda yürütülür.</span><span class="sxs-lookup"><span data-stu-id="f1094-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="f1094-162">Get ana çalışma zamanı senaryosu için ancak yalnızca hata ayıklama ve sorun giderme amacıyla için tasarlanmamıştır, sıkı bir şekilde hello hizmeti tarafından kısıtlanan dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f1094-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="f1094-163">Yüklemeleri için gönderme akışı olan hello aynı kayıtlar için.</span><span class="sxs-lookup"><span data-stu-id="f1094-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="f1094-164">Biz yalnızca bir seçenek tootarget bildirim toohello ekledik belirli yükleme - yalnızca kullanım etiketi "InstallationID: {desired-id}".</span><span class="sxs-lookup"><span data-stu-id="f1094-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="f1094-165">Servis talebi için yukarıdaki onu şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="f1094-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="f1094-166">Biri çeşitli şablonlar için:</span><span class="sxs-lookup"><span data-stu-id="f1094-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="f1094-167">Bildirimleri (standart katmanı için kullanılabilir) zamanlama</span><span class="sxs-lookup"><span data-stu-id="f1094-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="f1094-168">aynı normal gönderme ancak bir ek parametre - bildirim teslim zaman gerektirdiğinizde scheduledTime hello.</span><span class="sxs-lookup"><span data-stu-id="f1094-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="f1094-169">Hizmet şimdi + 5 dakika arasında geçen süreyi herhangi bir noktasını kabul eder ve şimdi + 7 gün.</span><span class="sxs-lookup"><span data-stu-id="f1094-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="f1094-170">**Windows yerel bildirim zamanla:**</span><span class="sxs-lookup"><span data-stu-id="f1094-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="f1094-171">İçeri/dışarı aktarma (standart katmanı için kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="f1094-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="f1094-172">Bazen gerekli tooperform toplu işlem kayıtlar karşı ediyor.</span><span class="sxs-lookup"><span data-stu-id="f1094-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="f1094-173">Genellikle başka bir sistem veya yalnızca yoğun düzeltme toosay güncelleştirme hello etiketleri tümleştirme içindir.</span><span class="sxs-lookup"><span data-stu-id="f1094-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="f1094-174">Biz kayıtlar binlerce hakkında konuşurken varsa toouse Get/güncelleştirme akış önerilir güçlü değil.</span><span class="sxs-lookup"><span data-stu-id="f1094-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="f1094-175">İçeri/dışarı aktarma yeteneği tasarlanmış toocover hello senaryodur.</span><span class="sxs-lookup"><span data-stu-id="f1094-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="f1094-176">Temel olarak, bir erişim toosome blob kapsayıcısı depolama hesabınızın altında bir gelen veri kaynağı ve çıkış konumu olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f1094-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="f1094-177">**Dışarı aktarma işini gönder:**</span><span class="sxs-lookup"><span data-stu-id="f1094-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="f1094-178">**İçe aktarma işi gönder:**</span><span class="sxs-lookup"><span data-stu-id="f1094-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="f1094-179">**İş tamamlanana kadar bekleyin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="f1094-180">**Tüm işleri görüntüleyin:**</span><span class="sxs-lookup"><span data-stu-id="f1094-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="f1094-181">**SAS imzayla URI:** bazı blob dosya veya blob kapsayıcısı hello URL'si artı izinleri ve süre sonu gibi parametreleri kümesini artı hesabın SAS anahtarı kullanılarak yapılan tüm bu işlemler imzası budur.</span><span class="sxs-lookup"><span data-stu-id="f1094-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="f1094-182">Azure depolama Java SDK'sı, bu tür bir URI oluşturma dahil olmak üzere Zengin özellikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="f1094-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="f1094-183">Basit alternatif olarak algoritmasını imzalamanın çok temel ve compact uygulaması olan ImportExportE2E test sınıfından (Merhaba github konum) göz atın.</span><span class="sxs-lookup"><span data-stu-id="f1094-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="f1094-184">Bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="f1094-184">Send Notifications</span></span>
<span data-ttu-id="f1094-185">Hello bildirim nesnesi yalnızca üstbilgileri gövde, bazı yardımcı program yöntemleri hello yerel ve şablon bildirimleri nesneleri oluşturmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f1094-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="f1094-186">**Windows mağazası ve Windows Phone 8.1 (Silverlight olmayan)**</span><span class="sxs-lookup"><span data-stu-id="f1094-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="f1094-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="f1094-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="f1094-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="f1094-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="f1094-189">**Windows Phone 8.0 ve 8.1 Silverlight**</span><span class="sxs-lookup"><span data-stu-id="f1094-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="f1094-190">**Yangın kindle**</span><span class="sxs-lookup"><span data-stu-id="f1094-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="f1094-191">**TooTags Gönder**</span><span class="sxs-lookup"><span data-stu-id="f1094-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="f1094-192">**Tootag ifade Gönder**</span><span class="sxs-lookup"><span data-stu-id="f1094-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="f1094-193">**Şablon bildirim gönder**</span><span class="sxs-lookup"><span data-stu-id="f1094-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="f1094-194">Java Kodunuzu çalıştırmaya şimdi, hedef cihazda görünen bir bildirim üretir.</span><span class="sxs-lookup"><span data-stu-id="f1094-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="f1094-195"><a name="next-steps"></a>Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f1094-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="f1094-196">Bu konuda size nasıl basit bir Java toocreate REST gösterdi istemci bildirim hub'ları için.</span><span class="sxs-lookup"><span data-stu-id="f1094-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="f1094-197">Buradan şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f1094-197">From here you can:</span></span>

* <span data-ttu-id="f1094-198">Merhaba tam karşıdan [Java SDK'sı], hello tüm SDK kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f1094-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="f1094-199">Merhaba örnekleriyle Yürüt:</span><span class="sxs-lookup"><span data-stu-id="f1094-199">Play with hello samples:</span></span>
  * <span data-ttu-id="f1094-200">[Notification Hubs ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="f1094-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="f1094-201">[Son dakika haberleri göndermek]</span><span class="sxs-lookup"><span data-stu-id="f1094-201">[Send breaking news]</span></span>
  * <span data-ttu-id="f1094-202">[Yerelleştirilmiş son dakika haberleri göndermek]</span><span class="sxs-lookup"><span data-stu-id="f1094-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="f1094-203">[Tooauthenticated kullanıcılar bildirimleri gönderme]</span><span class="sxs-lookup"><span data-stu-id="f1094-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="f1094-204">[Platformlar arası bildirimleri tooauthenticated kullanıcılar Gönder]</span><span class="sxs-lookup"><span data-stu-id="f1094-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[Java SDK'sı]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Notification Hubs ile çalışmaya başlama]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Son dakika haberleri göndermek]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Yerelleştirilmiş son dakika haberleri göndermek]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Tooauthenticated kullanıcılar bildirimleri gönderme]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Platformlar arası bildirimleri tooauthenticated kullanıcılar Gönder]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

