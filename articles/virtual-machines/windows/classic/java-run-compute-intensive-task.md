---
title: "bir VM üzerinde aaaCompute yoğunluklu Java uygulaması | Microsoft Docs"
description: "Toocreate bir işlem yoğunluklu Java uygulaması çalıştıran bir Azure sanal makinesi başka bir Java uygulaması tarafından nasıl izlenebilir öğrenin."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="449fd-103">Nasıl toorun işlem yoğunluklu görev Java sanal bir makinede</span><span class="sxs-lookup"><span data-stu-id="449fd-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="449fd-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="449fd-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="449fd-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="449fd-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="449fd-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="449fd-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="449fd-107">Azure ile bir sanal makine toohandle işlem yoğunluklu görevleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="449fd-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="449fd-108">Örneğin, bir sanal makine görevleri ve sonuçları tooclient makine ya da mobil uygulamalara teslim etmek.</span><span class="sxs-lookup"><span data-stu-id="449fd-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="449fd-109">Bu makaleyi okuduktan sonra toocreate bir işlem yoğunluklu Java uygulaması çalıştıran bir sanal makineyi başka bir Java uygulaması tarafından nasıl izlenebilir, anlaşılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="449fd-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="449fd-110">Bu öğretici nasıl toocreate Java konsol uygulamaları kitaplıkları tooyour Java uygulaması içe aktarabilir ve Java arşiv (JAR) oluşturabilir bildiğiniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="449fd-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="449fd-111">Microsoft Azure olanağıyla varsayılır.</span><span class="sxs-lookup"><span data-stu-id="449fd-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="449fd-112">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="449fd-112">You will learn:</span></span>

* <span data-ttu-id="449fd-113">Nasıl bir sanal makine bir Java Geliştirme Seti (JDK) ile toocreate zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="449fd-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="449fd-114">Nasıl tooremotely tooyour sanal makinede oturum.</span><span class="sxs-lookup"><span data-stu-id="449fd-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="449fd-115">Nasıl toocreate bir hizmet veri yolu ad alanı.</span><span class="sxs-lookup"><span data-stu-id="449fd-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="449fd-116">Nasıl toocreate bir işlem yoğunluklu görevi gerçekleştiren bir Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="449fd-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="449fd-117">Nasıl toocreate izler bir Java uygulaması hello işlem yoğunluklu görev ilerlemesini hello.</span><span class="sxs-lookup"><span data-stu-id="449fd-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="449fd-118">Nasıl toorun Java uygulamalarını hello.</span><span class="sxs-lookup"><span data-stu-id="449fd-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="449fd-119">Nasıl toostop Java uygulamalarını hello.</span><span class="sxs-lookup"><span data-stu-id="449fd-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="449fd-120">Bu öğretici hello gezici satış temsilcisi hello işlem yoğunluklu görev için kullanır.</span><span class="sxs-lookup"><span data-stu-id="449fd-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="449fd-121">Merhaba, hello Java uygulama çalışan hello işlem yoğunluklu görev örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="449fd-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Gezici satış temsilcisi Çözücü][solver_output]

<span data-ttu-id="449fd-123">Merhaba, hello Java uygulama izleme hello işlem yoğunluklu görevi örneği verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="449fd-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Gezici satış temsilcisi istemci][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="449fd-125">toocreate bir sanal makine</span><span class="sxs-lookup"><span data-stu-id="449fd-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="449fd-126">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="449fd-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="449fd-127">Tıklatın **yeni**, tıklatın **işlem**, tıklatın **sanal makine**ve ardından **Galeri'den**.</span><span class="sxs-lookup"><span data-stu-id="449fd-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="449fd-128">Merhaba, **sanal makine görüntüsü seçin** iletişim kutusunda **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="449fd-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="449fd-129">Unutmayın **JDK 6 Windows Server 2012** henüz hazır toorun JDK 7 bulunmayan eski uygulamaları olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="449fd-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="449fd-130">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-130">Click **Next**.</span></span>
5. <span data-ttu-id="449fd-131">Merhaba, **sanal makine yapılandırması** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="449fd-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="449fd-132">Merhaba sanal makine için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="449fd-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="449fd-133">Merhaba sanal makine için başlangıç boyutu toouse belirtin.</span><span class="sxs-lookup"><span data-stu-id="449fd-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="449fd-134">Hello Merhaba yönetici adı **kullanıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="449fd-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="449fd-135">Sonraki girer bu adı ve hello parolayı unutmayın, uzaktan toohello sanal makinede oturum zaman kullanır.</span><span class="sxs-lookup"><span data-stu-id="449fd-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="449fd-136">Hello bir parola girmenizi **yeni parola** alan ve yeniden hello girin **Onayla** alan.</span><span class="sxs-lookup"><span data-stu-id="449fd-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="449fd-137">Hello Yöneticisi hesabının parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="449fd-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="449fd-138">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-138">Click **Next**.</span></span>
6. <span data-ttu-id="449fd-139">Merhaba, sonraki **sanal makine yapılandırması** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="449fd-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="449fd-140">İçin **bulut hizmeti**, hello varsayılan kullanmak **yeni bir bulut hizmeti oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="449fd-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="449fd-141">Merhaba değeri **bulut hizmeti DNS adı** cloudapp.net arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="449fd-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="449fd-142">Bu Azure benzersiz olduğunu gösterir şekilde gerekirse, bu değeri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="449fd-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="449fd-143">Bir bölgeyi, benzeşim grubunu veya sanal ağ belirtin.</span><span class="sxs-lookup"><span data-stu-id="449fd-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="449fd-144">Bu öğreticinin amaçları doğrultusunda, bir bölge gibi belirtin **Batı ABD**.</span><span class="sxs-lookup"><span data-stu-id="449fd-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="449fd-145">İçin **depolama hesabı**seçin **otomatik olarak oluşturulan depolama hesabı kullan**.</span><span class="sxs-lookup"><span data-stu-id="449fd-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="449fd-146">İçin **kullanılabilirlik kümesi**seçin **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="449fd-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="449fd-147">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-147">Click **Next**.</span></span>
7. <span data-ttu-id="449fd-148">Merhaba son içinde **sanal makine yapılandırması** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="449fd-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="449fd-149">Merhaba varsayılan uç noktası girişleri kabul eder.</span><span class="sxs-lookup"><span data-stu-id="449fd-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="449fd-150">**Tamamla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="449fd-151">tooyour sanal makine tooremotely günlüğünde</span><span class="sxs-lookup"><span data-stu-id="449fd-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="449fd-152">Toohello üzerinde oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="449fd-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="449fd-153">Tıklatın **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="449fd-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="449fd-154">Merhaba, toolog istediğiniz içinde hello sanal makine adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="449fd-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="449fd-155">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-155">Click **Connect**.</span></span>
5. <span data-ttu-id="449fd-156">Yanıt toohello gerekli tooconnect toohello sanal makine olarak ister.</span><span class="sxs-lookup"><span data-stu-id="449fd-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="449fd-157">Hello Yöneticisi adı ve parola istendiğinde, hello sanal makineyi oluşturduğunuzda belirttiğiniz hello değerlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="449fd-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="449fd-158">Bu hello Azure hizmet veri yolu işlevselliğini gerektirir JRE'ın bir parçası olarak yüklenen hello Baltimore CyberTrust kök sertifika toobe Not **cacerts** depolar.</span><span class="sxs-lookup"><span data-stu-id="449fd-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="449fd-159">Bu sertifika otomatik olarak hello Java Çalışma zamanı ortamı (JRE) bu Öğreticisi tarafından kullanılan dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="449fd-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="449fd-160">Bu sertifika, JRE sahip değilseniz **cacerts** depolamak için bkz: [sertifika toohello Java CA sertifika deposuna ekleme] [ add_ca_cert] onu ekleme hakkında bilgi için (yanı Merhaba sertifikalarını cacerts deponuzda görüntüleme hakkında bilgi).</span><span class="sxs-lookup"><span data-stu-id="449fd-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="449fd-161">Nasıl toocreate bir service bus ad alanı</span><span class="sxs-lookup"><span data-stu-id="449fd-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="449fd-162">Azure'da Service Bus kullanarak toobegin kuyruklar, öncelikle bir hizmet ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="449fd-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="449fd-163">Hizmet ad alanı, uygulamanızın Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="449fd-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="449fd-164">toocreate hizmet ad alanı:</span><span class="sxs-lookup"><span data-stu-id="449fd-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="449fd-165">Toohello üzerinde oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="449fd-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="449fd-166">Merhaba sol gezinti bölmesinde hello Klasik Azure portalı, tıklatın **Service Bus, erişim denetimi ve önbelleğe alma**.</span><span class="sxs-lookup"><span data-stu-id="449fd-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="449fd-167">Hello sol üst hello Klasik Azure portalı, hello bölmesinde **Service Bus** düğümü ve ardından hello **yeni** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="449fd-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="449fd-168">![Hizmet veri yolu düğümü ekran görüntüsü][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="449fd-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="449fd-169">Merhaba, **yeni bir hizmet Namespace oluşturma** iletişim kutusuna bir **Namespace**, ve ardından toomake benzersiz olduğundan emin **Kullanılabilirliği Denetle** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="449fd-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="449fd-170">![Yeni Namespace ekran oluşturma][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="449fd-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="449fd-171">Emin olduktan sonra hello ad alanı adı kullanılabilir olduğu, ülke veya bölge, ad alanınızın barındırılması ve hello ardından seçin **oluşturma Namespace** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="449fd-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="449fd-172">oluşturduğunuz hello ad hello Klasik Azure portalı daha sonra görünür ve şu anda tooactivate alır.</span><span class="sxs-lookup"><span data-stu-id="449fd-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="449fd-173">Merhaba durum olana kadar bekleyin **etkin** hello sonraki adıma geçmeden önce.</span><span class="sxs-lookup"><span data-stu-id="449fd-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="449fd-174">Merhaba varsayılan yönetim kimlik hello ad alanı için elde</span><span class="sxs-lookup"><span data-stu-id="449fd-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="449fd-175">Sipariş tooperform yönetim işlemlerinin'hello yeni ad, bir kuyruk oluşturma gibi ad alanı için tooobtain hello yönetim kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="449fd-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="449fd-176">Merhaba Sol Gezinti Bölmesi'nde hello tıklatın **Service Bus** hello kullanılabilir ad alanlarının listesini görüntülemek için düğümü.</span><span class="sxs-lookup"><span data-stu-id="449fd-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="449fd-177">![Kullanılabilir ad alanlarının ekran görüntüsü][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="449fd-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="449fd-178">Gösterilen hello listeden yeni oluşturduğunuz hello ad alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="449fd-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="449fd-179">![Namespace listesi ekran görüntüsü][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="449fd-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="449fd-180">sağ taraftaki Hello **özellikleri** bölmesi, yeni ad alanı için hello özellikleri listeler.</span><span class="sxs-lookup"><span data-stu-id="449fd-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="449fd-181">![Özellikler bölmesinde ekran görüntüsü][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="449fd-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="449fd-182">Merhaba **varsayılan anahtar** gizlenir.</span><span class="sxs-lookup"><span data-stu-id="449fd-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="449fd-183">Merhaba tıklatın **Görünüm** düğmesini toodisplay hello güvenlik kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="449fd-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="449fd-184">![Varsayılan anahtar ekran görüntüsü][default_key]</span><span class="sxs-lookup"><span data-stu-id="449fd-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="449fd-185">Merhaba Not **varsayılan veren** ve hello **varsayılan anahtar** bu bilgileri tooperform işlemleri altına ad alanıyla kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="449fd-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="449fd-186">Nasıl toocreate bir işlem yoğunluklu görevi gerçekleştiren bir Java uygulaması</span><span class="sxs-lookup"><span data-stu-id="449fd-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="449fd-187">(Olmayan oluşturduğunuz toobe hello sanal makine) geliştirme makinenizdeki, indirme hello [Java için Azure SDK](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="449fd-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="449fd-188">Merhaba bu bölümün sonunda Hello örnek kod kullanarak bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="449fd-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="449fd-189">Bu öğreticide, kullanacağız **TSPSolver.java** hello Java dosya adı olarak.</span><span class="sxs-lookup"><span data-stu-id="449fd-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="449fd-190">Merhaba değiştirme **,\_hizmet\_veri yolu\_ad alanı**, **,\_hizmet\_veri yolu\_sahibi**ve **,\_hizmet\_veri yolu\_anahtar** yer tutucuları toouse, hizmet veri yolu **ad alanı**, **varsayılan veren** ve  **Varsayılan anahtar** değerler, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="449fd-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="449fd-191">Kodlama sonra verme hello uygulama tooa runnable Java arşiv (JAR) ve paket hello hello kitaplıklara JAR oluşturulan gereklidir.</span><span class="sxs-lookup"><span data-stu-id="449fd-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="449fd-192">Bu öğreticide, kullanacağız **TSPSolver.jar** oluşturulan hello JAR adı.</span><span class="sxs-lookup"><span data-stu-id="449fd-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="449fd-193">Nasıl toocreate izler bir Java uygulaması hello hello işlem yoğunluklu görev ilerleme durumu</span><span class="sxs-lookup"><span data-stu-id="449fd-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="449fd-194">Geliştirme makinenizde hello bu bölümün sonunda hello örnek kod kullanarak bir Java konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="449fd-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="449fd-195">Bu öğreticide, kullanacağız **TSPClient.java** hello Java dosya adı olarak.</span><span class="sxs-lookup"><span data-stu-id="449fd-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="449fd-196">Daha önce gösterildiği gibi hello değiştirme **,\_hizmet\_veri yolu\_ad alanı**, **,\_hizmet\_veri yolu\_sahibi**, ve **,\_hizmet\_veri yolu\_anahtar** yer tutucuları toouse, hizmet veri yolu **ad alanı**, **varsayılan veren**ve **varsayılan anahtar** değerler, sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="449fd-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="449fd-197">Merhaba uygulama tooa verme runnable JAR ve paket hello gerekli hello kitaplıklara JAR oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="449fd-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="449fd-198">Bu öğreticide, kullanacağız **TSPClient.jar** oluşturulan hello JAR adı.</span><span class="sxs-lookup"><span data-stu-id="449fd-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="449fd-199">Nasıl toorun hello Java uygulamaları</span><span class="sxs-lookup"><span data-stu-id="449fd-199">How toorun hello Java applications</span></span>
<span data-ttu-id="449fd-200">Merhaba işlem yoğunluklu uygulamayı çalıştırın, ilk toocreate hello sırayı sonra toosolve seyahat Saleseman hello geçerli en iyi yolu toohello hizmet veri yolu kuyruğu ekleyeceksiniz sorunun, hello.</span><span class="sxs-lookup"><span data-stu-id="449fd-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="449fd-201">Merhaba sırasında işlem yoğunluklu çalışmıyor (veya daha sonra), çalışma hello istemci toodisplay sonuçları hello service bus kuyruğundan uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="449fd-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="449fd-202">toorun Merhaba işlem yoğunluklu uygulaması</span><span class="sxs-lookup"><span data-stu-id="449fd-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="449fd-203">Tooyour sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="449fd-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="449fd-204">Uygulamanızın çalıştırdığı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="449fd-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="449fd-205">Örneğin, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="449fd-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="449fd-206">Kopya **TSPSolver.jar** çok**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="449fd-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="449fd-207">Adlı bir dosya oluşturun **c:\TSP\cities.txt** içeriği aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="449fd-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="449fd-208">Bir komut isteminde dizinleri tooc:\TSP değiştirin.</span><span class="sxs-lookup"><span data-stu-id="449fd-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="449fd-209">Merhaba JRE'ın bin klasörü hello PATH ortam değişkeni olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="449fd-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="449fd-210">Merhaba TSP Çözücü permütasyon çalıştırmadan önce toocreate hello hizmet veri yolu kuyruğu gerekir.</span><span class="sxs-lookup"><span data-stu-id="449fd-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="449fd-211">Çalışma hello aşağıdaki toocreate hello hizmet veri yolu kuyruğu komutu.</span><span class="sxs-lookup"><span data-stu-id="449fd-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="449fd-212">Merhaba sırası oluşturulduğunda, hello TSP Çözücü permütasyon çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="449fd-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="449fd-213">Örneğin, komut toorun hello Çözücü 8 şehir için aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="449fd-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="449fd-214">Bir sayı belirtmezseniz, bu için 10 Şehir çalışır.</span><span class="sxs-lookup"><span data-stu-id="449fd-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="449fd-215">Merhaba Çözücü geçerli kısa yollar buldukça, bunları toohello sıra ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="449fd-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="449fd-216">Merhaba büyük Merhaba, belirttiğiniz, hello uzun hello Çözücü çalışacak sayı.</span><span class="sxs-lookup"><span data-stu-id="449fd-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="449fd-217">Örneğin, 14 Şehir birkaç dakika sürebilir ve çalıştırmak için 15 Şehir birkaç saat sürebilir çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="449fd-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="449fd-218">Too16 veya daha fazla şehir artırma çalışma zamanı (sonunda hafta, ay ve yıl) gün içinde neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="449fd-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="449fd-219">Merhaba Şehir artar hello sayıda hello Çözücü tarafından değerlendirilen permütasyon sayısını toohello hızla artması son budur.</span><span class="sxs-lookup"><span data-stu-id="449fd-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="449fd-220">Nasıl toorun hello izleme istemci uygulaması</span><span class="sxs-lookup"><span data-stu-id="449fd-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="449fd-221">Merhaba istemci uygulaması çalıştırdığı tooyour makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="449fd-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="449fd-222">Bu ihtiyaç duymadığı toobe hello hello çalıştıran aynı makine **TSPSolver** olabilir ancak uygulama.</span><span class="sxs-lookup"><span data-stu-id="449fd-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="449fd-223">Uygulamanızın çalıştırdığı bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="449fd-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="449fd-224">Örneğin, **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="449fd-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="449fd-225">Kopya **TSPClient.jar** çok**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="449fd-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="449fd-226">Merhaba JRE'ın bin klasörü hello PATH ortam değişkeni olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="449fd-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="449fd-227">Bir komut isteminde dizinleri tooc:\TSP değiştirin.</span><span class="sxs-lookup"><span data-stu-id="449fd-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="449fd-228">Merhaba aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="449fd-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="449fd-229">İsteğe bağlı olarak, bir komut satırı bağımsız değişkeni geçirerek hello sıra denetimi Between dakika toosleep hello sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="449fd-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="449fd-230">Merhaba hello sıra denetleme varsayılan uyku süresi 3 dakika hiçbir komut satırı bağımsız değişkeni çok aktarılırsa, kullanılır**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="449fd-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="449fd-231">Örneğin, hello uyku aralığı için toouse farklı bir değer istiyorsanız, bir dakika hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="449fd-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="449fd-232">"Tam" bir kuyruk iletisi görür kadar hello istemci çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="449fd-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="449fd-233">Merhaba istemci çalıştırmadan hello Çözücü birden çok tekrarı çalıştırırsanız toorun hello istemci birden çok kez toocompletely boş hello sıra gerekebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="449fd-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="449fd-234">Alternatif olarak, hello sıra silin ve yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="449fd-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="449fd-235">Merhaba aşağıdaki komutu çalıştırarak toodelete hello sıra **TSPSolver** (değil **TSPClient**) komutu.</span><span class="sxs-lookup"><span data-stu-id="449fd-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="449fd-236">tüm yollar inceleniyor sonlanana kadar hello Çözücü çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="449fd-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="449fd-237">Nasıl toostop hello Java uygulamaları</span><span class="sxs-lookup"><span data-stu-id="449fd-237">How toostop hello Java applications</span></span>
<span data-ttu-id="449fd-238">Merhaba Çözücü ve istemci uygulamaları için basabilirsiniz **Ctrl + C** tooend önceki toonormal tamamlama istiyorsanız tooexit.</span><span class="sxs-lookup"><span data-stu-id="449fd-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
