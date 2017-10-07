---
title: "aaaService System Center Operations Manager ile tümleştirme Haritası | Microsoft Docs"
description: "Linux sistemleri ve haritalar Hizmetleri arasındaki iletişimi hello ve hizmet Haritası Windows uygulama bileşenleri otomatik olarak bulur bir Operations Management Suite çözümüdür. Hizmet eşlemesi kullanarak bu makalede ele tooautomatically Operations Manager'da dağıtılmış uygulama diyagramları oluşturun."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="aa298-104">System Center Operations Manager ile hizmet Haritası tümleştirme</span><span class="sxs-lookup"><span data-stu-id="aa298-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="aa298-105">Bu özellik genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="aa298-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="aa298-106">Operations Management Suite hizmet Haritası otomatik olarak sistemlerde, Windows ve Linux uygulama bileşenleri bulur ve Hizmetleri arasındaki hello iletişim eşler.</span><span class="sxs-lookup"><span data-stu-id="aa298-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="aa298-107">Hizmet eşlemesi tooview Kritik hizmetler sunan birbirine bağlı sistemler olarak düşündüğünüz birini sunucuları hello yolunuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="aa298-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="aa298-108">Hizmet eşlemesi herhangi TCP bağlı mimarisi hello yanı sıra bir aracının yüklenmesi gereken herhangi bir yapılandırma boyunca sunucuları, işlemleri ve bağlantı noktaları arasındaki bağlantıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="aa298-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="aa298-109">Daha fazla bilgi için bkz: Merhaba [hizmet Haritası belgelerine](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="aa298-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="aa298-110">İle tümleştirme arasında hizmet Haritası ve System Center Operations Manager, Operations Manager'da, hizmet eşlemesinde hello dinamik bağımlılık eşlemeleri temel alan dağıtılmış uygulama diyagramları otomatik olarak oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa298-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa298-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aa298-111">Prerequisites</span></span>
* <span data-ttu-id="aa298-112">Sunucular kümesi yönetme bir Operations Manager yönetim grubu.</span><span class="sxs-lookup"><span data-stu-id="aa298-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="aa298-113">Bir Operations Management Suite çalışma alanı hello etkin hizmet Haritası çözüm ile.</span><span class="sxs-lookup"><span data-stu-id="aa298-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="aa298-114">Operations Manager ve gönderen veri tooService eşleme tarafından yönetilen sunucular kümesi (en az bir tane).</span><span class="sxs-lookup"><span data-stu-id="aa298-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="aa298-115">Windows ve Linux sunucuları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aa298-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="aa298-116">Bir hizmet sorumlusu erişim toohello hello Operations Management Suite çalışma alanıyla ilişkili Azure aboneliği ile.</span><span class="sxs-lookup"><span data-stu-id="aa298-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="aa298-117">Daha fazla bilgi için çok Git[bir hizmet sorumlusu oluşturma](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="aa298-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="aa298-118">Merhaba hizmet Haritası Yönetimi paketini yükleyin</span><span class="sxs-lookup"><span data-stu-id="aa298-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="aa298-119">Operations Manager ile hizmet Haritası arasında hello tümleştirme hello Microsoft.SystemCenter.ServiceMap Yönetim Paketi grubu (Microsoft.SystemCenter.ServiceMap.mpb) alarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="aa298-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="aa298-120">Merhaba paket yönetim paketleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="aa298-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="aa298-121">Microsoft hizmet eşlemesi uygulama görünümleri</span><span class="sxs-lookup"><span data-stu-id="aa298-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="aa298-122">Microsoft System Center hizmet Haritası iç</span><span class="sxs-lookup"><span data-stu-id="aa298-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="aa298-123">Microsoft System Center hizmeti harita geçersiz kılmaları</span><span class="sxs-lookup"><span data-stu-id="aa298-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="aa298-124">Microsoft System Center hizmet eşlemesi</span><span class="sxs-lookup"><span data-stu-id="aa298-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="aa298-125">Merhaba hizmet Haritası tümleştirmesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="aa298-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="aa298-126">Merhaba hizmet Haritası Yönetim Paketi, yeni bir düğüm yükledikten sonra **hizmet Haritası**, altında görüntülenen **Operations Management Suite** hello içinde **Yönetim** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="aa298-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="aa298-127">tooconfigure hizmet Haritası tümleştirme hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="aa298-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="aa298-128">tooopen hello Yapılandırma Sihirbazı ' nda hello **hizmet eşlemesi genel bakış** bölmesinde tıklatın **çalışma Ekle**.</span><span class="sxs-lookup"><span data-stu-id="aa298-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Hizmet eşlemesi genel bakış bölmesinde](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="aa298-130">Merhaba, **bağlantı yapılandırması** penceresinde hello Kiracı adı veya kimliği, uygulama kimliği (Merhaba kullanıcı adı veya istemci kimliği olarak da bilinir) ve hello hizmet sorumlusu parolasını girin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="aa298-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="aa298-131">Daha fazla bilgi için çok Git[bir hizmet sorumlusu oluşturma](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="aa298-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![Merhaba Bağlantı Yapılandırması penceresi](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="aa298-133">Merhaba, **abonelik seçimi** penceresinde hello Azure abonelik, Azure kaynak grubu (Merhaba hello Operations Management Suite çalışma içeren bir) ve Operations Management Suite çalışma alanı seçin ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="aa298-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Merhaba Operations Manager yapılandırma çalışma alanı](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="aa298-135">Merhaba, **makine Grup Seçimi** penceresinde, hangi hizmet eşlemesi makine grupları seçin toosync tooOperations Yöneticisi istiyor.</span><span class="sxs-lookup"><span data-stu-id="aa298-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="aa298-136">Tıklatın **Ekle/Kaldır makine grupları**, grupları hello listesinden seçim **kullanılabilir makine grupları**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="aa298-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="aa298-137">Grupları seçmek bittiğinde tıklatın **Tamam** toofinish.</span><span class="sxs-lookup"><span data-stu-id="aa298-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Merhaba Operations Manager yapılandırma makine grupları](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="aa298-139">Merhaba, **sunucu seçimi** penceresinde, yapılandırdığınız hello hizmet eşlemesi sunucuları grubu toosync Operations Manager ve hizmet eşlemesi arasında istediğiniz hello sunucularıyla.</span><span class="sxs-lookup"><span data-stu-id="aa298-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="aa298-140">Tıklatın **sunucuları Ekle/Kaldır**.</span><span class="sxs-lookup"><span data-stu-id="aa298-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="aa298-141">Merhaba tümleştirme toobuild için bir sunucu için bir dağıtılmış uygulama diyagram hello sunucu olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="aa298-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="aa298-142">Operations Manager tarafından yönetilen</span><span class="sxs-lookup"><span data-stu-id="aa298-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="aa298-143">Hizmet eşlemesi tarafından yönetilen</span><span class="sxs-lookup"><span data-stu-id="aa298-143">Managed by Service Map</span></span>
    * <span data-ttu-id="aa298-144">Merhaba hizmet eşlemesi sunucuları grubu listelenen</span><span class="sxs-lookup"><span data-stu-id="aa298-144">Listed in hello Service Map Servers Group</span></span>

    ![Merhaba Operations Manager Yapılandırma grubu](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="aa298-146">İsteğe bağlı: Hello yönetim sunucusu kaynak havuzu toocommunicate Operations Management Suite ile seçin ve ardından **çalışma alanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="aa298-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Merhaba Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="aa298-148">Dakika tooconfigure ele ve hello Operations Management Suite çalışma kaydetmek.</span><span class="sxs-lookup"><span data-stu-id="aa298-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="aa298-149">Bunu yapılandırıldıktan sonra Operations Manager Operations Management Suite hello ilk hizmet Haritası eşitleme başlatır.</span><span class="sxs-lookup"><span data-stu-id="aa298-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![Merhaba Operations Manager yapılandırma kaynak havuzu](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="aa298-151">İzleyici hizmet eşlemesi</span><span class="sxs-lookup"><span data-stu-id="aa298-151">Monitor Service Map</span></span>
<span data-ttu-id="aa298-152">Merhaba Operations Management Suite çalışma bağlandıktan sonra yeni bir klasör, hizmet Haritası hello görüntülenir **izleme** hello Operations Manager konsolunun bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="aa298-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![Hello bölmesini Operations Manager izleme](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="aa298-154">dört düğüm Hello hizmet Haritası klasör içerir:</span><span class="sxs-lookup"><span data-stu-id="aa298-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="aa298-155">**Etkin uyarılar**: tüm hello etkin uyarıları Operations Manager hizmet Haritası arasında hello iletişimi hakkında listeler.</span><span class="sxs-lookup"><span data-stu-id="aa298-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="aa298-156">Bu uyarılar eşitlenen tooOperations yöneticisi olan Operations Management Suite uyarıları olmadığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="aa298-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="aa298-157">**Sunucuları**: listeleri hello izlenen sunucular toosync hizmet eşlemesinden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="aa298-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![Merhaba Operations Manager izleme sunucuları bölmesi](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="aa298-159">**Makine grubu bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm makine grupları listeler.</span><span class="sxs-lookup"><span data-stu-id="aa298-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="aa298-160">Dağıtılmış uygulama diyagramı hiçbir grup tooview tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa298-160">You can click any group tooview its distributed application diagram.</span></span>

    ![Merhaba Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="aa298-162">**Server bağımlılık görünümleri**: hizmet eşlemesinden eşitlenen tüm sunucuları listeler.</span><span class="sxs-lookup"><span data-stu-id="aa298-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="aa298-163">Dağıtılmış uygulama diyagramı tüm sunucu tooview tıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa298-163">You can click any server tooview its distributed application diagram.</span></span>

    ![Merhaba Operations Manager dağıtılmış uygulama diyagramı](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="aa298-165">Düzenleme veya silme hello çalışma</span><span class="sxs-lookup"><span data-stu-id="aa298-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="aa298-166">Düzenleme veya yapılandırılmış hello çalışma hello aracılığıyla silme **hizmet eşlemesi genel bakış** bölmesinde (**Yönetim** bölmesinde > **Operations Management Suite**  >  **Hizmet eşlemesi**).</span><span class="sxs-lookup"><span data-stu-id="aa298-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="aa298-167">Şu an için yalnızca bir Operations Management Suite çalışma yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa298-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Merhaba Operations Manager çalışma alanını Düzenle bölmesi](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="aa298-169">Kuralları ve geçersiz kılmalar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="aa298-169">Configure rules and overrides</span></span>
<span data-ttu-id="aa298-170">Bir kural _Microsoft.SystemCenter.ServiceMapImport.Rule_, tooperiodically fetch bilgi hizmeti eşlemesinden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="aa298-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="aa298-171">toochange eşitleme zamanlamalarını, geçersiz kılmalar hello kuralının yapılandırabilirsiniz (**yazma** bölmesinde > **kuralları** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="aa298-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![Merhaba Operations Manager geçersiz kılan özellikler penceresi](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="aa298-173">**Etkin**: etkinleştirmek veya Otomatik Güncelleştirmeler devre dışı.</span><span class="sxs-lookup"><span data-stu-id="aa298-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="aa298-174">**IntervalMinutes**: sıfırlama güncelleştirmeler arasındaki hello süre.</span><span class="sxs-lookup"><span data-stu-id="aa298-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="aa298-175">Merhaba varsayılan zaman aralığı bir saattir.</span><span class="sxs-lookup"><span data-stu-id="aa298-175">hello default interval is one hour.</span></span> <span data-ttu-id="aa298-176">Toosync sunucu eşlemeleri daha sık isterseniz hello değeri değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa298-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="aa298-177">**TimeoutSeconds**: hello isteği zaman aşımına uğramadan önce hello süreyi Sıfırla.</span><span class="sxs-lookup"><span data-stu-id="aa298-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="aa298-178">**TimeWindowMinutes**: veri sorgulama için sıfırlama hello zaman penceresi.</span><span class="sxs-lookup"><span data-stu-id="aa298-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="aa298-179">Varsayılan değer 60 dakikalık ' dir.</span><span class="sxs-lookup"><span data-stu-id="aa298-179">Default is a 60-minute window.</span></span> <span data-ttu-id="aa298-180">Hizmet eşlemesi tarafından izin verilen hello en büyük değer 60 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="aa298-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="aa298-181">Bilinen sorunlar ve sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="aa298-181">Known issues and limitations</span></span>

<span data-ttu-id="aa298-182">Merhaba geçerli tasarım sunar hello aşağıdaki sorunlar ve sınırlamalar:</span><span class="sxs-lookup"><span data-stu-id="aa298-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="aa298-183">Yalnızca tooa tek Operations Management Suite çalışma bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="aa298-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="aa298-184">Sunucuları toohello hizmet eşlemesi sunucuları grubu hello el ile eklemesi mümkün olsa da **yazma** bölmesinde, bu sunucular için hello eşlemeleri olmayan eşitlenen hemen.</span><span class="sxs-lookup"><span data-stu-id="aa298-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="aa298-185">Bunlar hizmet eşlemesinden hello sonraki eşitleme döngüsü sırasında senkronize edilir.</span><span class="sxs-lookup"><span data-stu-id="aa298-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="aa298-186">Toohello dağıtılmış uygulama hello Yönetim Paketi tarafından oluşturulan diyagramları herhangi bir değişiklik yaparsanız, bu değişiklikleri olasılıkla hello sonraki eşitleme ile hizmet eşlemesi üzerinde üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="aa298-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="aa298-187">Hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa298-187">Create a service principal</span></span>
<span data-ttu-id="aa298-188">Bir hizmet sorumlusu oluşturma hakkında daha fazla resmi Azure belgeler için bkz:</span><span class="sxs-lookup"><span data-stu-id="aa298-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="aa298-189">PowerShell kullanarak bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa298-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="aa298-190">Azure CLI kullanarak bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa298-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="aa298-191">Hello Azure portal kullanarak bir hizmet sorumlusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa298-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="aa298-192">Geri Bildirim</span><span class="sxs-lookup"><span data-stu-id="aa298-192">Feedback</span></span>
<span data-ttu-id="aa298-193">Tüm geri bildirim bize hizmet haritası veya bu belge hakkında var?</span><span class="sxs-lookup"><span data-stu-id="aa298-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="aa298-194">Ziyaret bizim [kullanıcı sesi sayfa](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), buradan özellikleri önermek veya varolan önerilere oy verin.</span><span class="sxs-lookup"><span data-stu-id="aa298-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
