---
title: "Veri Fabrikası için yönetim ağ geçidi aaaData | Microsoft Docs"
description: "Şirket içi ve hello arasında veri ağ geçidi toomove veri ayarlama bulut. Veri Yönetimi ağ geçidi, verilerinizi Azure Data Factory toomove kullanın."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="2361d-104">Veri Yönetimi Ağ Geçidi</span><span class="sxs-lookup"><span data-stu-id="2361d-104">Data Management Gateway</span></span>
<span data-ttu-id="2361d-105">Merhaba veri yönetimi ağ geçidi şirket içi ortamına toocopy verilerinizde Bulut ve şirket içi veri depoları arasında yüklemeniz gereken bir istemci aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="2361d-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="2361d-106">Merhaba şirket içi veri depoları Data Factory ile desteklenen hello listelenen [desteklenen veri kaynakları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) bölümü.</span><span class="sxs-lookup"><span data-stu-id="2361d-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="2361d-107">Bu makalede hello hello kılavuzda tamamlar [şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2361d-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2361d-108">Merhaba kılavuzda, bir şirket içi SQL Server veritabanı tooan Azure blob hello ağ geçidi toomove verileri kullanan bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2361d-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="2361d-109">Bu makalede hello veri yönetimi ağ geçidi hakkında ayrıntılı bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="2361d-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="2361d-110">Veri Yönetimi ağ geçidi hello ağ geçidi ile birden çok şirket içi makineler ilişkilendirerek ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2361d-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="2361d-111">Ölçeklendirmek yukarı bir düğümde aynı anda çalıştırabilirsiniz veri taşıma işlerinin sayısını artırarak.</span><span class="sxs-lookup"><span data-stu-id="2361d-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="2361d-112">Bu özellik, tek bir düğüme sahip mantıksal bir ağ geçidi için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="2361d-113">Bkz: [ölçeklendirme veri yönetimi ağ geçidi Azure veri fabrikası'nda](data-factory-data-management-gateway-high-availability-scalability.md) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="2361d-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="2361d-114">Şu anda, ağ geçidi yalnızca hello kopyalama etkinliği ve saklı yordam etkinliği veri fabrikasında destekler.</span><span class="sxs-lookup"><span data-stu-id="2361d-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="2361d-115">Bir özel etkinlik tooaccess şirket içi veri kaynaklarından olası toouse hello ağ geçidi olmadığı.</span><span class="sxs-lookup"><span data-stu-id="2361d-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="2361d-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2361d-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="2361d-117">Veri Yönetimi ağ geçidi özelliklerini</span><span class="sxs-lookup"><span data-stu-id="2361d-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="2361d-118">Veri Yönetimi ağ geçidi hello aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="2361d-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="2361d-119">Model veri kaynakları şirket içi ve bulut veri kaynaklarında içinde aynı veri fabrikası hello ve veri taşıma.</span><span class="sxs-lookup"><span data-stu-id="2361d-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="2361d-120">Acil Durum İzleme ve ağ geçidi durumu hello Data Factory sayfasından görünürlük ile yönetim için tek bir bölme vardır.</span><span class="sxs-lookup"><span data-stu-id="2361d-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="2361d-121">Erişim tooon içi veri kaynaklarına güvenli bir şekilde yönetin.</span><span class="sxs-lookup"><span data-stu-id="2361d-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="2361d-122">Hiçbir değişiklik toocorporate güvenlik duvarı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2361d-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="2361d-123">Ağ geçidi yalnızca giden HTTP tabanlı bağlantılar tooopen yapar Internet.</span><span class="sxs-lookup"><span data-stu-id="2361d-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="2361d-124">Sertifikanız ile şirket içi veri depoları için kimlik bilgilerini şifreler.</span><span class="sxs-lookup"><span data-stu-id="2361d-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="2361d-125">Veri verimli bir şekilde hareket – veri paralel, esnek toointermittent ağ sorunları otomatik yeniden deneme mantığı ile aktarılır.</span><span class="sxs-lookup"><span data-stu-id="2361d-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="2361d-126">Komut akışının ve veri akışı</span><span class="sxs-lookup"><span data-stu-id="2361d-126">Command flow and data flow</span></span>
<span data-ttu-id="2361d-127">Şirket içi ve bulut arasında kopyalama etkinliği toocopy veri kullandığınızda hello etkinlik bir ağ geçidi tootransfer verileri şirket içi veri kaynağı toocloud ve bunun tersi de kullanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="2361d-128">Hello üst düzey veri akışı için ve adımları için veri ağ geçidi kopyayla özeti aşağıdadır: ![ağ geçidini kullanarak veri akışı](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="2361d-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="2361d-129">Veri Geliştirici oluşturur bir ağ geçidi ya da hello kullanarak bir Azure Data Factory'deki [Azure portal](https://portal.azure.com) veya [PowerShell cmdlet'ini](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="2361d-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="2361d-130">Veri Geliştirici hello ağ geçidi belirterek bir şirket içi veri deposu için bağlı hizmet oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2361d-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="2361d-131">Bağlantılı hizmetinin hello kurulumunun bir parçası olarak veri Geliştirici hello kimlik bilgilerini ayarlama uygulama toospecify kimlik doğrulama türleri ve kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="2361d-132">Merhaba uygulama iletişim hello veri ile iletişim kurar kimlik bilgilerini ayarlama tootest bağlantı ve hello ağ geçidi toosave kimlik bilgileri depolar.</span><span class="sxs-lookup"><span data-stu-id="2361d-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="2361d-133">Ağ geçidi hello bulutta hello kimlik bilgilerini kaydetmeden önce (veri geliştirici tarafından sağlanan), hello ağ geçidi ile ilişkili hello sertifikasıyla hello kimlik bilgilerini şifreler.</span><span class="sxs-lookup"><span data-stu-id="2361d-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="2361d-134">Data Factory Hizmeti'ne zamanlama & işlerin bir paylaşılan Azure service bus kuyruğu kullanan bir denetim kanalı üzerinden Yönetim için hello ağ geçidi ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="2361d-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="2361d-135">Bir kopyalama etkinliği iş başlayacağı zamana toobe gerektiğinde, veri fabrikası kimlik bilgileri ile birlikte hello isteğini sıraya koyar.</span><span class="sxs-lookup"><span data-stu-id="2361d-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="2361d-136">Ağ geçidi hello sıra yoklama sonra hello işi başlatır.</span><span class="sxs-lookup"><span data-stu-id="2361d-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="2361d-137">Merhaba ağ geçidi hello kimlik bilgileriyle aynı sertifika ve ardından uygun kimlik doğrulama türü ve kimlik bilgileri ile toohello şirket içi veri deposu bağlanır hello şifresini çözer.</span><span class="sxs-lookup"><span data-stu-id="2361d-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="2361d-138">Merhaba ağ geçidi, bir şirket içi depolama tooa bulut depolama biriminden veya tersi hello kopyalama etkinliği hello veri ardışık düzeninde nasıl yapılandırıldığına bağlı olarak veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="2361d-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="2361d-139">Bu adım için hello ağ geçidi doğrudan Azure Blob Depolama gibi bulut tabanlı depolama hizmetleri güvenli (HTTPS) kanal üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="2361d-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="2361d-140">Ağ geçidini kullanma konuları</span><span class="sxs-lookup"><span data-stu-id="2361d-140">Considerations for using gateway</span></span>
* <span data-ttu-id="2361d-141">Veri Yönetimi ağ geçidi tek bir örneği birden çok şirket içi veri kaynakları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="2361d-142">Ancak, **bağlı tooonly bir Azure veri fabrikası bir tek ağ geçidi örneği olan** ve başka bir data factory ile paylaşılamaz.</span><span class="sxs-lookup"><span data-stu-id="2361d-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="2361d-143">Sağlayabilirsiniz **veri yönetimi ağ geçidi yalnızca bir örneği** tek bir makinede yüklü.</span><span class="sxs-lookup"><span data-stu-id="2361d-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="2361d-144">Tooaccess şirket içi veri kaynakları gereken iki veri fabrikaları olduğunu varsayalım iki şirket içi bilgisayarlarda tooinstall ağ geçitleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="2361d-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="2361d-145">Diğer bir deyişle, bir ağ geçidi bağlı tooa belirli veri fabrikası olur</span><span class="sxs-lookup"><span data-stu-id="2361d-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="2361d-146">Merhaba **ağ geçidi hello hello veri kaynağı olarak aynı makine üzerinde toobe gerek yoktur**.</span><span class="sxs-lookup"><span data-stu-id="2361d-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="2361d-147">Ancak, ağ geçidi daha yakından toohello veri kaynağına sahip hello ağ geçidi tooconnect toohello veri kaynağı hello süresini azaltır.</span><span class="sxs-lookup"><span data-stu-id="2361d-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="2361d-148">Bir ana bilgisayar şirket içi veri kaynağına hello farklı bir makinede hello ağ geçidi yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="2361d-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="2361d-149">Merhaba ağ geçidi ve veri kaynağı farklı makinelerde olduğunda hello ağ geçidi veri kaynağı ile kaynaklar için rekabet edemez.</span><span class="sxs-lookup"><span data-stu-id="2361d-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="2361d-150">Sağlayabilirsiniz **birden çok ağ geçidi toohello bağlanma farklı makinelerde aynı şirket içi veri kaynağına**.</span><span class="sxs-lookup"><span data-stu-id="2361d-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="2361d-151">Örneğin, iki veri fabrikaları ancak her iki hello veri fabrikaları ile aynı şirket içi veri kaynağına kayıtlı hello hizmet veren iki ağ geçidi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="2361d-152">Bilgisayar hizmet yüklü bir ağ geçidi zaten varsa bir **Power BI** senaryosu, yükleme bir **Azure Data Factory için ayrı bir ağ geçidi** başka bir makinede.</span><span class="sxs-lookup"><span data-stu-id="2361d-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="2361d-153">Ağ geçidi kullandığınızda da kullanılmalıdır **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="2361d-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="2361d-154">Veri kaynağı (bir güvenlik duvarının arkasında olan) bir şirket içi veri kaynağı olarak davran kullandığınızda bile **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="2361d-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="2361d-155">Merhaba hizmet hello veri kaynağı arasında Hello ağ geçidi tooestablish bağlantısı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2361d-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="2361d-156">Yapmanız gerekenler **hello ağ geçidini kullanan** hello veri deposu hello bulutta üzerinde olsa bile bir **Azure Iaas sanal**.</span><span class="sxs-lookup"><span data-stu-id="2361d-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="2361d-157">Yükleme</span><span class="sxs-lookup"><span data-stu-id="2361d-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="2361d-158">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2361d-158">Prerequisites</span></span>
* <span data-ttu-id="2361d-159">desteklenen hello **işletim sistemi** sürümleri Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="2361d-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="2361d-160">Bir etki alanı denetleyicisinde hello veri yönetimi ağ geçidi yüklemesi şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="2361d-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="2361d-161">.NET framework 4.5.1 veya üzeri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2361d-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="2361d-162">Windows 7 makinede ağ geçidi yüklüyorsanız, .NET Framework 4.5 veya üstünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2361d-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="2361d-163">Bkz: [.NET Framework sistem gereksinimleri](https://msdn.microsoft.com/library/8z6watww.aspx) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="2361d-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="2361d-164">Önerilen hello **yapılandırma** hello ağ geçidi makinesi en az 2 GHz, 4 çekirdek, 8 GB RAM ve 80 GB disk için.</span><span class="sxs-lookup"><span data-stu-id="2361d-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="2361d-165">Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata istekleri yanıt vermez.</span><span class="sxs-lookup"><span data-stu-id="2361d-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="2361d-166">Bu nedenle, uygun bir yapılandırma **güç planı** hello ağ geçidi'ı yüklemeden önce hello bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="2361d-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="2361d-167">Merhaba makine yapılandırılmış toohibernate ise, hello ağ geçidi yükleme isteyen bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2361d-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="2361d-168">Merhaba makine tooinstall yönetici olmanız ve hello veri yönetimi ağ geçidi başarılı bir şekilde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2361d-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="2361d-169">Ek kullanıcılar toohello ekleyebilirsiniz **veri yönetimi ağ geçidi kullanıcıları** yerel Windows grubu.</span><span class="sxs-lookup"><span data-stu-id="2361d-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="2361d-170">Merhaba, bu grubun üyesi mümkün toouse hello **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** aracı tooconfigure hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="2361d-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="2361d-171">Etkinlik çalışması üzerinde belirli bir sıklık durum kopyalama gibi hello hello makinede kaynak kullanımı (CPU, bellek) de aynı yoğun ve boşta saatlerle desen hello izler.</span><span class="sxs-lookup"><span data-stu-id="2361d-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="2361d-172">Kaynak Kullanımı Yoğun olarak da hello taşınan veri miktarına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2361d-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="2361d-173">Birden çok kopyası işleri devam ederken, kaynak kullanımı yoğun zamanlarda gidebilir bakın.</span><span class="sxs-lookup"><span data-stu-id="2361d-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="2361d-174">Yükleme Seçenekleri</span><span class="sxs-lookup"><span data-stu-id="2361d-174">Installation options</span></span>
<span data-ttu-id="2361d-175">Veri Yönetimi ağ geçidi yolları aşağıdaki hello yüklenebilir:</span><span class="sxs-lookup"><span data-stu-id="2361d-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="2361d-176">Merhaba bir MSI kurulum paketi yükleyerek [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="2361d-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="2361d-177">Merhaba MSI kullanılan tooupgrade mevcut veri yönetimi ağ geçidi toohello en son sürümü, korunan tüm ayarlar ile de olabilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="2361d-178">Tıklayarak **veri ağ geçidi yükleyip** bağlantıyı el ile Kurulumu altında veya **doğrudan bu bilgisayar Yükle** EXPRESS Kurulumu altında.</span><span class="sxs-lookup"><span data-stu-id="2361d-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="2361d-179">Bkz: [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makalede hızlı kurulum kullanma hakkında adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="2361d-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="2361d-180">Merhaba el ile adım toohello İndirme Merkezi alır.</span><span class="sxs-lookup"><span data-stu-id="2361d-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="2361d-181">karşıdan yükleme ve İndirme Merkezi'nden hello ağ geçidi için hello hello sonraki bölümde yönergelerdir.</span><span class="sxs-lookup"><span data-stu-id="2361d-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="2361d-182">Yükleme için en iyi yöntemler:</span><span class="sxs-lookup"><span data-stu-id="2361d-182">Installation best practices:</span></span>
1. <span data-ttu-id="2361d-183">Böylece Hello makine değil hazırda bekleme güç planı hello konak hello ağ geçidi için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2361d-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="2361d-184">Merhaba ana makine hazırda bekleme durumunda hello ağ geçidi toodata istekleri yanıt vermez.</span><span class="sxs-lookup"><span data-stu-id="2361d-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="2361d-185">Merhaba ağ geçidiyle ilişkili hello sertifikayı yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="2361d-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="2361d-186">İndirme Merkezi'nden Hello ağ geçidi yükleyin</span><span class="sxs-lookup"><span data-stu-id="2361d-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="2361d-187">Çok gidin[Microsoft Veri Yönetimi ağ geçidi yükleme sayfası](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="2361d-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="2361d-188">' I tıklatın **karşıdan**, select hello uygun sürümünü (**32-bit** vs. **64-bit**), tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2361d-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="2361d-189">Merhaba çalıştırmak **MSI** doğrudan veya tooyour sabit diske kaydetmek ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2361d-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="2361d-190">Merhaba üzerinde **Hoş Geldiniz** sayfasında, bir **dil** tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2361d-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="2361d-191">**Kabul** tıklayın ve son kullanıcı lisans sözleşmesi hello **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2361d-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="2361d-192">Seçin **klasörü** tooinstall hello ağ geçidi ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2361d-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="2361d-193">Merhaba üzerinde **hazır tooinstall** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="2361d-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="2361d-194">Tıklatın **son** toocomplete yükleme.</span><span class="sxs-lookup"><span data-stu-id="2361d-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="2361d-195">Başlangıç anahtarı hello Azure portal ' alın.</span><span class="sxs-lookup"><span data-stu-id="2361d-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="2361d-196">Adım adım yönergeler için Hello sonraki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="2361d-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="2361d-197">Merhaba üzerinde **kayıt ağ geçidi** sayfasında **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** , makinede çalışan adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="2361d-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="2361d-198">Başlangıç anahtarı hello metni yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="2361d-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="2361d-199">İsteğe bağlı olarak, tıklayın **Göster ağ geçidi anahtarı** toosee hello anahtar metin.</span><span class="sxs-lookup"><span data-stu-id="2361d-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="2361d-200">Tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2361d-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="2361d-201">Anahtarı kullanarak ağ geçidini kaydedin</span><span class="sxs-lookup"><span data-stu-id="2361d-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="2361d-202">Merhaba Portalı'nda mantıksal bir ağ geçidi oluşturmadıysanız</span><span class="sxs-lookup"><span data-stu-id="2361d-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="2361d-203">bir ağ geçidi hello portal ve get hello anahtarında hello toocreate **yapılandırma** sayfası, hello izlenecek adımları izleyin [şirket içi ve bulut arasında veri taşıma](data-factory-move-data-between-onprem-and-cloud.md) makale.</span><span class="sxs-lookup"><span data-stu-id="2361d-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="2361d-204">Merhaba Portalı'nda hello mantıksal ağ geçidi oluşturduysanız</span><span class="sxs-lookup"><span data-stu-id="2361d-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="2361d-205">Azure portalında toohello gidin **Data Factory** sayfasında ve tıklayın **bağlı hizmetler** döşeme.</span><span class="sxs-lookup"><span data-stu-id="2361d-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Veri Fabrikası sayfası](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="2361d-207">Merhaba, **bağlı hizmetler** sayfası, select hello mantıksal **ağ geçidi** hello portalında oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="2361d-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![mantıksal ağ geçidi](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="2361d-209">Merhaba, **veri ağ geçidi** sayfasında, **veri ağ geçidi yükleyip**.</span><span class="sxs-lookup"><span data-stu-id="2361d-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Merhaba Portalı'nda bağlantı indirin](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="2361d-211">Merhaba, **yapılandırma** sayfasında, **yeniden oluşturun anahtar**.</span><span class="sxs-lookup"><span data-stu-id="2361d-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="2361d-212">Evet hello uyarı iletisi dikkatle okuduktan sonra'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Yeniden anahtar](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="2361d-214">Kopyala düğmesine bir sonraki toohello anahtar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="2361d-215">Merhaba, kopyalanan toohello Pano anahtardır.</span><span class="sxs-lookup"><span data-stu-id="2361d-215">hello key is copied toohello clipboard.</span></span>

    ![Anahtarı kopyalayın](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="2361d-217">Sistem Tepsisi Simgeleri / bildirimleri</span><span class="sxs-lookup"><span data-stu-id="2361d-217">System tray icons/ notifications</span></span>
<span data-ttu-id="2361d-218">Merhaba aşağıdaki görüntüde bazılarını hello gördüğünüz Tepsisi simgeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="2361d-218">hello following image shows some of hello tray icons that you see.</span></span>

![Sistem Tepsisi Simgeleri](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="2361d-220">İmleç hello sistem tepsisi simgesi/bildirim iletisi taşırsanız, açılan penceresinde hello ağ geçidi/güncelleştirme işlemini hello durumu hakkında ayrıntılar bakın.</span><span class="sxs-lookup"><span data-stu-id="2361d-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="2361d-221">Bağlantı noktaları ve güvenlik duvarı</span><span class="sxs-lookup"><span data-stu-id="2361d-221">Ports and firewall</span></span>
<span data-ttu-id="2361d-222">İki güvenlik duvarı tooconsider ihtiyacınız vardır: **Kurumsal Güvenlik Duvarı** hello merkezi yönlendirici hello kuruluşunuzun üzerinde çalışan ve **Windows Güvenlik Duvarı** hello yerel makine üzerinde bir arka plan programı olarak hello burada yapılandırılan Ağ Geçidi yüklü.</span><span class="sxs-lookup"><span data-stu-id="2361d-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![Güvenlik duvarları](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="2361d-224">Kurumsal güvenlik duvarı düzeyinde hello aşağıdaki yapılandırmayı etki alanları ve giden bağlantı noktaları:</span><span class="sxs-lookup"><span data-stu-id="2361d-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="2361d-225">Etki alanı adları</span><span class="sxs-lookup"><span data-stu-id="2361d-225">Domain names</span></span> | <span data-ttu-id="2361d-226">Bağlantı Noktaları</span><span class="sxs-lookup"><span data-stu-id="2361d-226">Ports</span></span> | <span data-ttu-id="2361d-227">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2361d-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2361d-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2361d-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="2361d-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="2361d-229">443, 80</span></span> |<span data-ttu-id="2361d-230">Veri Taşıma hizmeti arka uç ile iletişim için kullanılan</span><span class="sxs-lookup"><span data-stu-id="2361d-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="2361d-231">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2361d-231">*.core.windows.net</span></span> |<span data-ttu-id="2361d-232">443</span><span class="sxs-lookup"><span data-stu-id="2361d-232">443</span></span> |<span data-ttu-id="2361d-233">Azure Blob (yapılandırılmışsa) kullanarak hazırlanmış kopyalama için kullanılan</span><span class="sxs-lookup"><span data-stu-id="2361d-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="2361d-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="2361d-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="2361d-235">443</span><span class="sxs-lookup"><span data-stu-id="2361d-235">443</span></span> |<span data-ttu-id="2361d-236">Veri Taşıma hizmeti arka uç ile iletişim için kullanılan</span><span class="sxs-lookup"><span data-stu-id="2361d-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="2361d-237">Windows Güvenlik Duvarı düzeyde, bu giden bağlantı noktaları normal şekilde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="2361d-238">Merhaba etki alanları ve bağlantı noktalarını uygun şekilde yapılandırabilirsiniz, varsa ağ geçidi makinesi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="2361d-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="2361d-239">Kaynağını temel alan / havuzlarını toowhitelist ek etki alanları ve giden bağlantı noktaları olabilir, Kurumsal/Windows Güvenlik Duvarı.</span><span class="sxs-lookup"><span data-stu-id="2361d-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="2361d-240">Bazı bulut veritabanları için (örneğin: [Azure SQL veritabanı](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), vb.), ağ geçidi makinede güvenlik duvarı yapılandırmalarını toowhitelist IP adresini gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="2361d-241">Bir kaynak veri deposu tooa havuz veri deposundan veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="2361d-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="2361d-242">Merhaba güvenlik duvarı kurallarının düzgün şekilde hello Kurumsal güvenlik duvarı, Windows Güvenlik Duvarı hello gateway makinesinde, üzerinde etkindir ve kendisini hello verileri depolamak emin olun.</span><span class="sxs-lookup"><span data-stu-id="2361d-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="2361d-243">Bu kurallar etkinleştirme hello ağ geçidi tooconnect tooboth kaynak ve havuz başarıyla sağlar.</span><span class="sxs-lookup"><span data-stu-id="2361d-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="2361d-244">Merhaba kopyalama işleminde dahil her veri deposu için kuralları etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="2361d-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="2361d-245">Örneğin, gelen toocopy **bir şirket içi veri deposu tooan Azure SQL veritabanı havuzunu veya bir Azure SQL Data Warehouse havuz**, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="2361d-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="2361d-246">Gidene izin ver **TCP** iletişim bağlantı noktası **1433** Windows Güvenlik Duvarı ve kurumsal güvenlik duvarı için.</span><span class="sxs-lookup"><span data-stu-id="2361d-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="2361d-247">Azure SQL server tooadd hello IP adresinin hello ağ geçidi makinesi toohello izin verilen IP adreslerinin listesi Hello güvenlik duvarı ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2361d-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="2361d-248">Güvenlik duvarını giden bağlantı noktası 1433 izin vermez, ağ geçidi doğrudan Azure SQL erişemiyor.</span><span class="sxs-lookup"><span data-stu-id="2361d-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="2361d-249">Bu durumda, kullanabilir [hazırlanan kopyalama](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure veritabanı / SQL Azure DW.</span><span class="sxs-lookup"><span data-stu-id="2361d-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="2361d-250">Bu senaryoda, yalnızca HTTPS (443 numaralı) hello veri taşıma için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="2361d-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="2361d-251">Proxy sunucusu hususları</span><span class="sxs-lookup"><span data-stu-id="2361d-251">Proxy server considerations</span></span>
<span data-ttu-id="2361d-252">Kurumsal ağ ortamınızın bir proxy kullanıyorsa, sunucu tooaccess Internet Merhaba, veri yönetimi ağ geçidi toouse uygun proxy ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2361d-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="2361d-253">Merhaba ilk kayıt aşamasında hello proxy ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2361d-253">You can set hello proxy during hello initial registration phase.</span></span>

![Kayıt sırasında kümesi proxy](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="2361d-255">Ağ geçidi hello proxy sunucusu tooconnect toohello bulut hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="2361d-256">Tıklatın **değişiklik** ilk kurulum sırasında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2361d-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="2361d-257">Merhaba gördüğünüz **proxy ayarını** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2361d-257">You see hello **proxy setting** dialog.</span></span>

![Yapılandırma Yöneticisi'ni kullanarak küme proxy](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="2361d-259">Üç yapılandırma seçeneği vardır:</span><span class="sxs-lookup"><span data-stu-id="2361d-259">There are three configuration options:</span></span>

* <span data-ttu-id="2361d-260">**Proxy kullanmayın**: ağ geçidi proxy tooconnect toocloud hizmetlerin açıkça kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="2361d-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="2361d-261">**Sistem proxy kullanacak**: ağ geçidi olarak yapılandırılmış diahost.exe.config ve diawp.exe.config ayarının hello proxy kullanır.  Proxy diahost.exe.config ve diawp.exe.config yapılandırılmışsa, ağ geçidi toocloud hizmeti proxy üzerinden geçmeden doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="2361d-262">**Özel ara sunucu kullanmak**: hello HTTP proxy ayarı toouse diahost.exe.config ve diawp.exe.config yapılandırmalarında kullanmak yerine ağ geçidi için yapılandırın.  Adresi ve bağlantı noktası gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2361d-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="2361d-263">Kullanıcı adı ve parola, proxy'nin kimlik doğrulama ayarını bağlı olarak isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="2361d-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="2361d-264">Tüm ayarlar hello kimlik bilgileri sertifikası hello ağ geçidi ile şifrelenir ve hello ağ geçidi ana makinede yerel olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="2361d-265">Merhaba güncelleştirilen proxy ayarlarını kaydettikten sonra hello veri yönetimi ağ geçidi ana bilgisayar hizmeti otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="2361d-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="2361d-266">Tooview veya proxy ayarlarını güncelleştirmek istiyorsanız ağ geçidi başarıyla, kaydedildikten sonra veri yönetimi ağ geçidi Yapılandırma Yöneticisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="2361d-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="2361d-267">Başlatma **veri yönetimi ağ geçidi Yapılandırma Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="2361d-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="2361d-268">Geçiş toohello **ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2361d-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="2361d-269">Tıklatın **değişiklik** bağlamak **HTTP Proxy** bölüm toolaunch hello **Set HTTP Proxy** iletişim.</span><span class="sxs-lookup"><span data-stu-id="2361d-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="2361d-270">Merhaba tıklattıktan sonra **sonraki** düğmesi, ağ geçidi ana bilgisayar hizmeti izni toosave hello proxy ayarını ve yeniden başlatma hello için soran bir uyarı iletişim kutusu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="2361d-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="2361d-271">Görüntüleyin ve Configuration Manager aracını kullanarak HTTP proxy güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2361d-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Yapılandırma Yöneticisi'ni kullanarak küme proxy](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="2361d-273">Bir proxy sunucusu NTLM kimlik doğrulaması ile ayarladıysanız, ağ geçidi ana bilgisayar hizmeti hello etki alanı hesabı altında çalışır.</span><span class="sxs-lookup"><span data-stu-id="2361d-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="2361d-274">Daha sonra hello etki alanı hesabı hello parolayı değiştirirseniz, hello hizmeti için yapılandırma ayarlarını tooupdate unutmayın ve uygun şekilde yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="2361d-275">Toothis gereksinim tooupdate hello parola sık gerektirmeyen özel etki alanı hesabı tooaccess hello proxy sunucusu kullan öneririz.</span><span class="sxs-lookup"><span data-stu-id="2361d-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="2361d-276">Proxy sunucusu ayarlarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2361d-276">Configure proxy server settings</span></span>
<span data-ttu-id="2361d-277">Seçerseniz **sistem proxy kullanacak** hello HTTP Proxy'si için ayarı, ağ geçidi hello proxy diahost.exe.config ve diawp.exe.config ayarını kullanır.  Proxy diahost.exe.config ve diawp.exe.config belirtilirse, ağ geçidi toocloud hizmeti proxy üzerinden geçmeden doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="2361d-278">Merhaba aşağıdaki yordamı hello diahost.exe.config dosyasını güncelleştirmek için yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2361d-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="2361d-279">Dosya Gezgini'nde, C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared\diahost.exe.config tooback güvenli bir kopyasını hello özgün dosyasının yedeğini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2361d-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="2361d-280">Yönetici olarak çalıştırarak Notepad.exe başlatın ve metin dosyasını "C:\Program Files\Microsoft veri yönetimi Gateway\2.0\Shared\diahost.exe.config. açın Hello kod aşağıdaki gösterildiği gibi hello varsayılan etiket için system.net bulun:</span><span class="sxs-lookup"><span data-stu-id="2361d-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="2361d-281">Proxy sunucu ayrıntıları hello aşağıdaki örnekte gösterildiği gibi daha sonra ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2361d-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="2361d-282">Ek özellikler scriptLocation gibi hello proxy etiketi toospecify gerekli hello ayarları içinde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="2361d-283">Çok başvuran[proxy öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) sözdizimi hakkında.</span><span class="sxs-lookup"><span data-stu-id="2361d-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="2361d-284">Merhaba özgün konumuna Hello yapılandırma dosyasını kaydetmek sonra hello hello değişiklikleri toplar veri yönetimi ağ geçidi ana bilgisayar hizmeti yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="2361d-285">toorestart hello hizmet: hello Denetim Masası'ndan veya hello hizmetler uygulamasını kullanın **veri yönetimi ağ geçidi Yapılandırma Yöneticisi** > merhaba tıklatın **Hizmeti Durdur** düğmesine ve ardından hello **Hizmetini başlatmak**.</span><span class="sxs-lookup"><span data-stu-id="2361d-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="2361d-286">Merhaba Hizmet başlatılmazsa, hatalı bir XML etiket söz dizimini, düzenlendiği hello uygulama yapılandırma dosyasına eklendi olasıdır.</span><span class="sxs-lookup"><span data-stu-id="2361d-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2361d-287">Tooupdate unutmadığınızdan **her ikisi de** diahost.exe.config ve diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="2361d-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="2361d-288">Ayrıca toothese noktaları ayrıca toomake Microsoft Azure, şirketinizin beyaz olmasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="2361d-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="2361d-289">Geçerli Microsoft Azure IP adreslerinin listesi Hello hello indirilebilir [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2361d-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="2361d-290">Güvenlik Duvarı ve proxy sunucusu ile ilgili sorunlar için olası Belirtiler</span><span class="sxs-lookup"><span data-stu-id="2361d-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="2361d-291">Hataları benzer toohello olanları aşağıdaki sorunlarla karşılaşırsanız, tooimproper hangi bağlantı tooData Fabrika tooauthenticate kendisini ağ geçidinden engeller hello güvenlik duvarı veya proxy sunucusunun yapılandırmasını, son olasıdır.</span><span class="sxs-lookup"><span data-stu-id="2361d-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="2361d-292">Güvenlik Duvarı ve proxy sunucunuz düzgün yapılandırılmış tooprevious bölüm tooensure bakın.</span><span class="sxs-lookup"><span data-stu-id="2361d-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="2361d-293">Tooregister hello ağ geçidi çalıştığınızda, aşağıdaki hata hello alırsınız: "başarısız tooregister hello ağ geçidi anahtarı.</span><span class="sxs-lookup"><span data-stu-id="2361d-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="2361d-294">Tooregister hello ağ geçidi anahtarı yeniden denemeden önce veri yönetimi ağ geçidi bağlı bir durumda hello ve hello veri yönetimi ağ geçidi ana bilgisayar hizmeti başlatıldığında onaylayın."</span><span class="sxs-lookup"><span data-stu-id="2361d-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="2361d-295">Yapılandırma Yöneticisi'ni açın, durum "Bağlantı kesildi" veya "Bağlanıyor." görürsünüz</span><span class="sxs-lookup"><span data-stu-id="2361d-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="2361d-296">Windows olay günlükleri, "Olay Görüntüleyici" görüntülerken > "Uygulama ve hizmet günlükleri" > "Veri yönetimi ağ geçidi", aşağıdaki hata hello gibi hata iletilerine bakın:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="2361d-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="2361d-297">Kimlik bilgisi şifreleme için 8050 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="2361d-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="2361d-298">Merhaba **kimlik bilgilerini ayarlama** uygulamanız tarafından kullanılan bağlantı noktasına gelen hello **8050** bir şirket içi yedekleme ayarladığınızda toorelay kimlik bilgileri toohello ağ geçidi hello Azure portal hizmetinde bağlı.</span><span class="sxs-lookup"><span data-stu-id="2361d-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="2361d-299">Ağ geçidi Kurulum sırasında varsayılan olarak, hello ağ geçidi yükleme hello ağ geçidi makinede açar.</span><span class="sxs-lookup"><span data-stu-id="2361d-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="2361d-300">Bir üçüncü taraf güvenlik duvarı kullanıyorsanız, başlangıç bağlantı noktası 8050 el ile açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2361d-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="2361d-301">Ağ geçidi Kurulum sırasında güvenlik duvarı sorunu yaşayıp çalıştırırsanız, komut tooinstall hello ağ geçidi hello güvenlik duvarını yapılandırma olmadan aşağıdaki hello kullanmayı deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2361d-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="2361d-302">Merhaba gateway makinesinde hello bağlantı noktası 8050 değil tooopen seçerseniz, hello kullanma dışındaki mekanizmalarını kullanmak **kimlik bilgilerini ayarlama** uygulama tooconfigure verilerini depolamak kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2361d-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="2361d-303">Örneğin, kullanabilirsiniz [yeni AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="2361d-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="2361d-304">Bkz: [kimlik bilgilerini ayarlama ve güvenlik](#set-credentials-and-securityy) nasıl veri kimlik bilgilerini depolamak üzerinde bölüm ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="2361d-305">Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2361d-305">Update</span></span>
<span data-ttu-id="2361d-306">Varsayılan olarak, veri yönetimi ağ geçidi hello ağ geçidi daha yeni bir sürümü kullanılabilir olduğunda otomatik olarak güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2361d-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="2361d-307">Tüm hello zamanlanmış görevler tümü tamamlanıncaya kadar hello ağ geçidi güncelleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="2361d-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="2361d-308">Merhaba güncelleştirme işlemi tamamlanana kadar başka görev hello ağ geçidi tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="2361d-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="2361d-309">Merhaba güncelleştirmesi başarısız olursa, ağ geçidi toohello eski sürümünü geri alınır.</span><span class="sxs-lookup"><span data-stu-id="2361d-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="2361d-310">Zamanlanmış hello güncelleştirme yerler aşağıdaki hello zamanında bakın:</span><span class="sxs-lookup"><span data-stu-id="2361d-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="2361d-311">hello Azure Portalı'ndaki Hello ağ geçidi özellikleri sayfasında.</span><span class="sxs-lookup"><span data-stu-id="2361d-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="2361d-312">Merhaba veri yönetimi ağ geçidi Yapılandırma Yöneticisi giriş sayfası</span><span class="sxs-lookup"><span data-stu-id="2361d-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="2361d-313">Sistem tepsisi bildirimi iletisi.</span><span class="sxs-lookup"><span data-stu-id="2361d-313">System tray notification message.</span></span>

<span data-ttu-id="2361d-314">hello veri yönetimi ağ geçidi Yapılandırma Yöneticisi Hello Giriş sekmesinde hello güncelleştirme zamanlaması görüntüler ve hello son zaman hello ağ geçidi yüklü/güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="2361d-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Güncelleştirmeleri zamanlama](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="2361d-316">Merhaba güncelleştirmeyi hemen yükleyin veya hello ağ geçidi toobe Zamanlanmış Başlangıç zamanında otomatik olarak güncelleştirilmesini bekleyin.</span><span class="sxs-lookup"><span data-stu-id="2361d-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="2361d-317">Örneğin, hello ağ geçidi Yapılandırma Yöneticisi tooinstall tıklayabilirsiniz hello Güncelleştir düğmesini yanı sıra, hemen gösterilen bildirim iletisi hello görüntü gösterir aşağıdaki hello.</span><span class="sxs-lookup"><span data-stu-id="2361d-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Güncelleştirme DMG Yapılandırma Yöneticisi'nde](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="2361d-319">Merhaba bildirim iletisi hello sistem tepsisindeki hello görüntü aşağıdaki gösterildiği gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="2361d-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Sistem tepsisi iletisi](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="2361d-321">Güncelleştirme işlemi (el ile veya otomatik) hello sistem tepsisindeki hello durumunu bakın.</span><span class="sxs-lookup"><span data-stu-id="2361d-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="2361d-322">Ağ geçidi Yapılandırma Yöneticisi'ni başlattığınızda başlattığında, o hello ağ geçidi çubuğu hello bildirim iletide güncelleştirilmiştir birlikte bağlantı çok bkz[yeni konu nedir](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="2361d-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="2361d-323">toodisable/etkinleştirme otomatik güncelleştirme özelliği</span><span class="sxs-lookup"><span data-stu-id="2361d-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="2361d-324">Devre dışı bırak/hello otomatik güncelleştirme özelliği aşağıdaki adımları hello yaparak etkinleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="2361d-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="2361d-325">[Tek düğüm için ağ geçidi]</span><span class="sxs-lookup"><span data-stu-id="2361d-325">[For single node gateway]</span></span>
1. <span data-ttu-id="2361d-326">Merhaba gateway makinesindeki Windows PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="2361d-327">Toohello C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript klasörüne geçin.</span><span class="sxs-lookup"><span data-stu-id="2361d-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="2361d-328">Komut tooturn hello otomatik güncelleştirme aşağıdaki çalışma hello özelliği (devre dışı bırakın).</span><span class="sxs-lookup"><span data-stu-id="2361d-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="2361d-329">tekrar açma tooturn:</span><span class="sxs-lookup"><span data-stu-id="2361d-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="2361d-330">[[Çok düğümlü yüksek oranda kullanılabilir ve Ölçeklenebilir Ağ Geçidi (Önizleme)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="2361d-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="2361d-331">Merhaba gateway makinesindeki Windows PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="2361d-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="2361d-332">Toohello C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript klasörüne geçin.</span><span class="sxs-lookup"><span data-stu-id="2361d-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="2361d-333">Komut tooturn hello otomatik güncelleştirme aşağıdaki çalışma hello özelliği (devre dışı bırakın).</span><span class="sxs-lookup"><span data-stu-id="2361d-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="2361d-334">Yüksek kullanılabilirlik özelliği (Önizleme) ile ağ geçidi için fazladan bir AuthKey param gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2361d-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="2361d-335">tekrar açma tooturn:</span><span class="sxs-lookup"><span data-stu-id="2361d-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="2361d-336">Merhaba ağ geçidi makineden farklı bir makineden hello portal erişirseniz Merhaba kimlik bilgileri Yöneticisi uygulaması toohello ağ geçidi makinesi bağlanabilir emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2361d-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="2361d-337">Merhaba uygulaması hello ağ geçidi makinesi bağlanamazsa, bunu, hello veri kaynağı ve tootest bağlantı toohello veri kaynağı için kimlik bilgilerini tooset izin vermiyor.</span><span class="sxs-lookup"><span data-stu-id="2361d-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="2361d-338">Merhaba kullandığınızda **kimlik bilgilerini ayarlama** uygulama hello portal şifreler hello kimlik hello belirtilen hello sertifikayla **sertifika** hello sekmesinde **ağ geçidi Configuration Manager** hello gateway makinesinde.</span><span class="sxs-lookup"><span data-stu-id="2361d-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="2361d-339">Merhaba kimlik bilgilerini şifrelemek için API tabanlı bir yaklaşım arıyorsanız hello kullanabilirsiniz [yeni AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2361d-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="2361d-340">Merhaba cmdlet hello sertifikasını bu ağ geçidi yapılandırılmış toouse tooencrypt hello kimlik bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="2361d-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="2361d-341">Şifrelenmiş kimlik bilgileri toohello ekleme **EncryptedCredential** hello öğesinin **connectionString** hello JSON içinde.</span><span class="sxs-lookup"><span data-stu-id="2361d-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="2361d-342">Merhaba JSON hello ile kullandığınız [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet'ini veya hello Data Factory Düzenleyici.</span><span class="sxs-lookup"><span data-stu-id="2361d-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="2361d-343">Data Factory düzenleyici kullanarak kimlik bilgilerini ayarlama daha fazla bir yaklaşım vardır.</span><span class="sxs-lookup"><span data-stu-id="2361d-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="2361d-344">Bir SQL Server bağlantılı oluşturursanız ve hello Düzenleyicisi'ni kullanarak hizmet kimlik bilgilerini düz metin olarak girin, hello kimlik bilgileri hello Data Factory hizmetine sahip bir sertifika kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="2361d-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="2361d-345">Merhaba sertifikasını bu ağ geçidi yapılandırılmış toouse kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="2361d-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="2361d-346">Bu yaklaşım bazı durumlarda biraz daha hızlı olabilir ancak daha az güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="2361d-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="2361d-347">Bu nedenle, yalnızca geliştirme ve Test amaçları için bu yaklaşım izlemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="2361d-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="2361d-348">PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="2361d-348">PowerShell cmdlets</span></span>
<span data-ttu-id="2361d-349">Bu bölümde açıklanmıştır nasıl toocreate ve Azure PowerShell cmdlet'lerini kullanarak ağ geçidini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="2361d-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="2361d-350">Başlatma **Azure PowerShell** Yönetici modunda.</span><span class="sxs-lookup"><span data-stu-id="2361d-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="2361d-351">Çalıştırarak tooyour Azure hesabı oturum komutu aşağıdaki ve Azure kimlik bilgilerinizi girerken hello.</span><span class="sxs-lookup"><span data-stu-id="2361d-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="2361d-352">Kullanım hello **yeni AzureRmDataFactoryGateway** cmdlet toocreate şekilde mantıksal bir ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="2361d-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="2361d-353">**Örnek komut ve çıktı**:</span><span class="sxs-lookup"><span data-stu-id="2361d-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="2361d-354">Azure PowerShell'de toohello klasörüne geçin: **C:\Program Files\Microsoft veri yönetimi Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="2361d-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="2361d-355">Çalıştırma **RegisterGateway.ps1** hello yerel değişkeni ile ilişkilendirilmiş **$Key** hello komutu aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="2361d-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="2361d-356">Bu komut dosyasını daha önce oluşturduğunuz hello mantıksal ağ geçidi ile makinenizde yüklü hello istemci Aracısı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="2361d-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="2361d-357">Uzak makinedeki hello ağ geçidi hello IsRegisterOnRemoteMachine parametresini kullanarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2361d-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="2361d-358">Örnek:</span><span class="sxs-lookup"><span data-stu-id="2361d-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="2361d-359">Merhaba kullanabilirsiniz **Get-AzureRmDataFactoryGateway** cmdlet tooget hello ağ geçidi, veri fabrikası'nda listesi.</span><span class="sxs-lookup"><span data-stu-id="2361d-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="2361d-360">Ne zaman hello **durum** gösterir **çevrimiçi**, ağ geçidiniz hazır toouse olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2361d-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="2361d-361">Hello kullanarak bir ağ geçidi kaldırabilirsiniz **Kaldır AzureRmDataFactoryGateway** hello kullanarak bir ağ geçidi için cmdlet ve güncelleştirme açıklama **kümesi AzureRmDataFactoryGateway** cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="2361d-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="2361d-362">Data Factory Cmdlet başvurusu sözdizimi ve bu cmdlet'ler hakkında diğer ayrıntılar için bkz.</span><span class="sxs-lookup"><span data-stu-id="2361d-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="2361d-363">PowerShell kullanarak listesi ağ geçitleri</span><span class="sxs-lookup"><span data-stu-id="2361d-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="2361d-364">PowerShell kullanarak ağ geçidi kaldırma</span><span class="sxs-lookup"><span data-stu-id="2361d-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="2361d-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2361d-365">Next steps</span></span>
* <span data-ttu-id="2361d-366">Bkz: [şirket içi ve bulut arasında veri taşıma veri depolarına](data-factory-move-data-between-onprem-and-cloud.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="2361d-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="2361d-367">Merhaba kılavuzda, bir şirket içi SQL Server veritabanı tooan Azure blob hello ağ geçidi toomove verileri kullanan bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2361d-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
