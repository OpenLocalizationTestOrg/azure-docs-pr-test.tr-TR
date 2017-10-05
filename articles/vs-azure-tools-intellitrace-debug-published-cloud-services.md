---
title: "Bir Azure bulut hizmeti Visual Studio ve IntelliTrace ile bir yayımlanan hata ayıklama | Microsoft Docs"
description: "Bir bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama öğrenin"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5e6662fc-b917-43ea-bf2b-4f2fc3d213dc
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 7905dfb97cbd7578a8422567fe674839d00c21ef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="cc1fb-103">Yayımlanan Azure bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="cc1fb-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="cc1fb-104">IntelliTrace ile Azure içinde çalıştığında bir rol örneği için kapsamlı hata ayıklama bilgileri oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="cc1fb-105">Bir sorunun nedenini bulmak gerekiyorsa, Azure'da çalışıyormuş gibi kodunuzu Visual Studio'dan adım için IntelliTrace günlüklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-105">If you need to find the cause of a problem, you can use the IntelliTrace logs to step through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="cc1fb-106">Etkin, Azure uygulamanız Azure'daki bir bulut hizmeti olarak çalışan ve Visual Studio kaydedilen verileri yeniden yürütme olanak tanır, IntelliTrace kayıtları kodu yürütme ve ortam verilerini anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay the recorded data from Visual Studio.</span></span> 

<span data-ttu-id="cc1fb-107">Visual Studio Enterprise varsa IntelliTrace ve Azure uygulamanızı hedeflerinizi .NET Framework 4 veya sonraki bir sürümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="cc1fb-108">IntelliTrace Azure rollerinizi için bilgi toplar.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="cc1fb-109">Sanal makineler için her zaman 64-bit işletim sistemlerini çalıştıran bu rolleri.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-109">The virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="cc1fb-110">Alternatif olarak, kullandığınız [uzaktan hata ayıklama](http://go.microsoft.com/fwlink/p/?LinkId=623041) doğrudan Azure'da çalışan bir bulut hizmetine eklemek için.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) to attach directly to a cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc1fb-111">IntelliTrace yalnızca hata ayıklama senaryoları için tasarlanmıştır ve Üretim dağıtımı için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="cc1fb-112">IntelliTrace için bir Azure uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cc1fb-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="cc1fb-113">IntelliTrace için Azure uygulama etkinleştirmek için oluşturma ve Visual Studio Azure project uygulamayı yayımlama.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-113">To enable IntelliTrace for an Azure application, you must create and publish the application from a Visual Studio Azure project.</span></span> <span data-ttu-id="cc1fb-114">Azure'da yayımlamadan önce Azure uygulamanız için IntelliTrace yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-114">You must configure IntelliTrace for your Azure application before you publish it to Azure.</span></span> <span data-ttu-id="cc1fb-115">IntelliTrace yapılandırmadan uygulamanızı yayımlarsanız, projeyi yeniden yayımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-115">If you publish your application without configuring IntelliTrace, you need to republish the project.</span></span> <span data-ttu-id="cc1fb-116">Daha fazla bilgi için bkz: [yayımlama bir Azure bulut hizmeti Visual Studio kullanarak projeleri](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="cc1fb-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="cc1fb-117">Proje derleme hedeflerinizi ayarlanır Azure uygulamanızı dağıtmak hazır olduğunuzda doğrulayın **hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-117">When you are ready to deploy your Azure application, verify that your project build targets are set to **Debug**.</span></span>

1. <span data-ttu-id="cc1fb-118">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve bağlam menüsünden seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-118">In **Solution Explorer**, right-click project, and, from the context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="cc1fb-119">İçinde **Azure uygulamasını Yayımla** iletişim kutusu, Azure aboneliği seçin ve Seç **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-119">In the **Publish Azure Application** dialog, select the Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="cc1fb-120">İçinde **ayarları** sayfasında, **Gelişmiş ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-120">In the **Settings** page, select the **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="cc1fb-121">Aç **IntelliTrace'i etkinleştirin** bulutta yayımlandığında, uygulamanız için IntelliTrace günlükleri toplamak için seçeneği.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-121">Turn on the **Enable IntelliTrace** option to collect IntelliTrace logs for your application when it is published in the cloud.</span></span>
   
1. <span data-ttu-id="cc1fb-122">Temel IntelliTrace yapılandırmasını özelleştirmek için seçin **ayarları** yanına **IntelliTrace'i etkinleştirin**.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-122">To customize the basic IntelliTrace configuration, select **Settings** next to **Enable IntelliTrace**.</span></span>

    ![IntelliTrace ayarları bağlantısı](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="cc1fb-124">İçinde **IntelliTrace ayarları** iletişim kutusunda, günlük, mi çağrı bilgileri toplamak, hangi modülleri ve toplamak için işlemler günlüklerde ve kayıt ayırmak için ne kadar alan hangi olayların belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-124">In the **IntelliTrace Settings** dialog, you can specify which events to log, whether to collect call information, which modules and processes to collect logs for, and how much space to allocate to the recording.</span></span> <span data-ttu-id="cc1fb-125">IntelliTrace hakkında daha fazla bilgi için bkz: [IntelliTrace ile hata ayıklama](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="cc1fb-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace ayarları](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="cc1fb-127">IntelliTrace günlüğünü (varsayılan boyutu 250 MB'dır) IntelliTrace ayarlarında belirtilen en büyük boyutunu döngüsel günlük dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-127">The IntelliTrace log is a circular log file of the maximum size specified in the IntelliTrace settings (the default size is 250 MB).</span></span> <span data-ttu-id="cc1fb-128">IntelliTrace günlüklerini sanal makine dosya sistemindeki bir dosyaya toplanır.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-128">IntelliTrace logs are collected to a file in the file system of the virtual machine.</span></span> <span data-ttu-id="cc1fb-129">Günlükleri istediğinizde, bir anlık görüntü zamandaki o noktada alınır ve yerel bilgisayara indirilir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-129">When you request the logs, a snapshot is taken at that point in time and downloaded to your local computer.</span></span>

<span data-ttu-id="cc1fb-130">Azure bulut hizmeti için Azure yayımlandıktan sonra IntelliTrace Azure düğümünden etkinleştirilmiş olup olmadığını belirleyebilirsiniz **Sunucu Gezgini**aşağıdaki görüntüde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="cc1fb-130">After the Azure cloud service has been published to Azure, you can determine if IntelliTrace has been enabled from the Azure node in **Server Explorer**, as shown in the following image:</span></span>

![Sunucu Gezgini - IntelliTrace etkin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="cc1fb-132">Rol örneği için IntelliTrace günlüklerini indirin</span><span class="sxs-lookup"><span data-stu-id="cc1fb-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="cc1fb-133">Visual Studio kullanarak, aşağıdaki adımları izleyerek bir rol örneği için IntelliTrace günlüklerini yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc1fb-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="cc1fb-134">İçinde **Sunucu Gezgini**, genişletin **bulut Hizmetleri** düğümünü ve günlükleri indirmek istediğiniz rol örneği bulun.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-134">In **Server Explorer**, expand the **Cloud Services** node, and locate role instance whose logs you wish to download.</span></span> 

1. <span data-ttu-id="cc1fb-135">Rol örneği sağ tıklatın ve s bağlam menüsünden seçin **IntelliTrace günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-135">Right-click the role instance, and from the s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![IntelliTrace günlüklerini menü seçeneği görüntüleyin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="cc1fb-137">IntelliTrace günlüklerini, yerel bilgisayarınızda bir dizindeki bir dosya indirilir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-137">The IntelliTrace logs are downloaded to a file in a directory on your local computer.</span></span> <span data-ttu-id="cc1fb-138">IntelliTrace isteği her zaman günlükleri, yeni bir anlık görüntüsü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-138">Each time that you request the IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="cc1fb-139">Günlükleri karşıdan yüklenirken Visual Studio işlemin ilerlemesini görüntüler **Azure etkinlik günlüğü** penceresi.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-139">While the logs are being downloaded, Visual Studio displays the progress of the operation in the **Azure Activity Log** window.</span></span> <span data-ttu-id="cc1fb-140">Aşağıdaki çizimde gösterildiği gibi daha fazla ayrıntı işlem için satır öğeyi genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-140">As shown in the following figure, you can expand the line item for the operation to see more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="cc1fb-142">Visual Studio IntelliTrace günlüklerini karşıdan yüklenirken çalışmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-142">You can continue to work in Visual Studio while the IntelliTrace logs are downloading.</span></span> <span data-ttu-id="cc1fb-143">Günlük yükleme tamamlandığında, Visual Studio açılır.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-143">When the log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="cc1fb-144">IntelliTrace günlüklerini framework oluşturur ve daha sonra işleyen özel durumları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-144">The IntelliTrace logs might contain exceptions that the framework generates and handles afterwards.</span></span> <span data-ttu-id="cc1fb-145">İç framework kod bunları güvenle yoksayabilirsiniz bir rolü, başlatma için normal bir parçası olarak bu özel durumları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="cc1fb-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cc1fb-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cc1fb-146">Next steps</span></span>
- [<span data-ttu-id="cc1fb-147">Azure bulut hizmetlerinde hata ayıklama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="cc1fb-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="cc1fb-148">Visual Studio kullanarak bir Azure bulut hizmetinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="cc1fb-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)