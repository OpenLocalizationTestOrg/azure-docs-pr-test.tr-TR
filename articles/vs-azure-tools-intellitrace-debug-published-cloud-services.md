---
title: "aaaDebugging yayımlanan bir Azure bulut hizmeti Visual Studio ve IntelliTrace ile | Microsoft Docs"
description: "Nasıl toodebug bir bulut hizmeti Visual Studio ve IntelliTrace ile bilgi edinin"
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
ms.openlocfilehash: 60734a71d5499de72e1ca81a3ab0ab9f34bc303a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-a-published-azure-cloud-service-with-visual-studio-and-intellitrace"></a><span data-ttu-id="109cc-103">Yayımlanan Azure bulut hizmeti Visual Studio ve IntelliTrace ile hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="109cc-103">Debugging a published Azure cloud service with Visual Studio and IntelliTrace</span></span>
<span data-ttu-id="109cc-104">IntelliTrace ile Azure içinde çalıştığında bir rol örneği için kapsamlı hata ayıklama bilgileri oturum açabilir.</span><span class="sxs-lookup"><span data-stu-id="109cc-104">With IntelliTrace, you can log extensive debugging information for a role instance when it runs in Azure.</span></span> <span data-ttu-id="109cc-105">Toofind hello bir sorunun nedenini gerekiyorsa, Azure'da çalışıyormuş gibi hello IntelliTrace günlüklerini toostep Visual Studio kodunuzdan aracılığıyla kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="109cc-105">If you need toofind hello cause of a problem, you can use hello IntelliTrace logs toostep through your code from Visual Studio as if it were running in Azure.</span></span> <span data-ttu-id="109cc-106">Gerçekte, Azure uygulamanız Azure'daki bir bulut hizmeti olarak çalışan ve olanak tanır, IntelliTrace anahtar kodu yürütme ve ortam verilerini kaydeder hello kaydedilen veri Visual Studio'dan yeniden yürütün.</span><span class="sxs-lookup"><span data-stu-id="109cc-106">In effect, IntelliTrace records key code execution and environment data when your Azure application is running as a cloud service in Azure, and lets you replay hello recorded data from Visual Studio.</span></span> 

<span data-ttu-id="109cc-107">Visual Studio Enterprise varsa IntelliTrace ve Azure uygulamanızı hedeflerinizi .NET Framework 4 veya sonraki bir sürümünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="109cc-107">You can use IntelliTrace if you have Visual Studio Enterprise installed and your Azure application targets .NET Framework 4 or a later version.</span></span> <span data-ttu-id="109cc-108">IntelliTrace Azure rollerinizi için bilgi toplar.</span><span class="sxs-lookup"><span data-stu-id="109cc-108">IntelliTrace collects information for your Azure roles.</span></span> <span data-ttu-id="109cc-109">Merhaba sanal makineler için her zaman 64-bit işletim sistemlerini çalıştıran bu rolleri.</span><span class="sxs-lookup"><span data-stu-id="109cc-109">hello virtual machines for these roles always run 64-bit operating systems.</span></span>

<span data-ttu-id="109cc-110">Alternatif olarak, kullandığınız [uzaktan hata ayıklama](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach doğrudan Azure'da çalışan tooa bulut hizmeti.</span><span class="sxs-lookup"><span data-stu-id="109cc-110">As an alternative, you can use [remote debugging](http://go.microsoft.com/fwlink/p/?LinkId=623041) tooattach directly tooa cloud service that's running in Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="109cc-111">IntelliTrace yalnızca hata ayıklama senaryoları için tasarlanmıştır ve Üretim dağıtımı için kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="109cc-111">IntelliTrace is intended for debug scenarios only, and should not be used for a production deployment.</span></span>
> 

## <a name="configure-an-azure-application-for-intellitrace"></a><span data-ttu-id="109cc-112">IntelliTrace için bir Azure uygulaması yapılandırma</span><span class="sxs-lookup"><span data-stu-id="109cc-112">Configure an Azure application for IntelliTrace</span></span>
<span data-ttu-id="109cc-113">tooenable IntelliTrace Azure uygulamaya ait oluşturmalı ve Visual Studio Azure project hello uygulamadan yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="109cc-113">tooenable IntelliTrace for an Azure application, you must create and publish hello application from a Visual Studio Azure project.</span></span> <span data-ttu-id="109cc-114">TooAzure yayımlamadan önce Azure uygulamanız için IntelliTrace yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="109cc-114">You must configure IntelliTrace for your Azure application before you publish it tooAzure.</span></span> <span data-ttu-id="109cc-115">IntelliTrace yapılandırmadan uygulamanızı yayımlamak, toorepublish hello proje gerekir.</span><span class="sxs-lookup"><span data-stu-id="109cc-115">If you publish your application without configuring IntelliTrace, you need toorepublish hello project.</span></span> <span data-ttu-id="109cc-116">Daha fazla bilgi için bkz: [yayımlama bir Azure bulut hizmeti Visual Studio kullanarak projeleri](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span><span class="sxs-lookup"><span data-stu-id="109cc-116">For more information, see [Publishing an Azure cloud services projects using Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623012).</span></span>

1. <span data-ttu-id="109cc-117">Olduğunuzda toodeploy Azure uygulamanız hazır, projenizin yapı hedeflediği çok ayarlandığını doğrulayın**hata ayıklama**.</span><span class="sxs-lookup"><span data-stu-id="109cc-117">When you are ready toodeploy your Azure application, verify that your project build targets are set too**Debug**.</span></span>

1. <span data-ttu-id="109cc-118">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve, hello bağlam menüsünden seçin **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="109cc-118">In **Solution Explorer**, right-click project, and, from hello context menu, select **Publish**.</span></span>
   
1. <span data-ttu-id="109cc-119">Merhaba, **Azure uygulamasını Yayımla** iletişim kutusu, select hello Azure aboneliği ve select **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="109cc-119">In hello **Publish Azure Application** dialog, select hello Azure subscription, and select **Next**.</span></span>

1. <span data-ttu-id="109cc-120">Merhaba, **ayarları** sayfası, select hello **Gelişmiş ayarları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="109cc-120">In hello **Settings** page, select hello **Advanced Settings** tab.</span></span>

1. <span data-ttu-id="109cc-121">Merhaba üzerinde kapatma **IntelliTrace'i etkinleştirin** hello bulutta yayımlandığında, uygulamanız için toocollect IntelliTrace günlüklerini seçeneği.</span><span class="sxs-lookup"><span data-stu-id="109cc-121">Turn on hello **Enable IntelliTrace** option toocollect IntelliTrace logs for your application when it is published in hello cloud.</span></span>
   
1. <span data-ttu-id="109cc-122">toocustomize hello temel IntelliTrace yapılandırma, select **ayarları** sonraki çok**IntelliTrace'i etkinleştirin**.</span><span class="sxs-lookup"><span data-stu-id="109cc-122">toocustomize hello basic IntelliTrace configuration, select **Settings** next too**Enable IntelliTrace**.</span></span>

    ![IntelliTrace ayarları bağlantısı](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/intellitrace-settings-link.png)
   
1. <span data-ttu-id="109cc-124">Merhaba, **IntelliTrace ayarları** iletişim kutusunda, hangi olayların toolog, toocollect arama bilgileri, hangi modüller ve işlemler toocollect günlüklerinde ve ne kadar alan tooallocate toohello kaydı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="109cc-124">In hello **IntelliTrace Settings** dialog, you can specify which events toolog, whether toocollect call information, which modules and processes toocollect logs for, and how much space tooallocate toohello recording.</span></span> <span data-ttu-id="109cc-125">IntelliTrace hakkında daha fazla bilgi için bkz: [IntelliTrace ile hata ayıklama](http://go.microsoft.com/fwlink/?LinkId=214468).</span><span class="sxs-lookup"><span data-stu-id="109cc-125">For more information about IntelliTrace, see [Debugging with IntelliTrace](http://go.microsoft.com/fwlink/?LinkId=214468).</span></span>
   
    ![IntelliTrace ayarları](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC519063.png)

<span data-ttu-id="109cc-127">Merhaba IntelliTrace günlük hello en büyük boyutunu (Merhaba varsayılan boyutu 250 MB'tır) hello IntelliTrace ayarlarında belirtilen döngüsel günlük dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="109cc-127">hello IntelliTrace log is a circular log file of hello maximum size specified in hello IntelliTrace settings (hello default size is 250 MB).</span></span> <span data-ttu-id="109cc-128">IntelliTrace günlüklerini toplanan tooa dosyasında hello dosya sistemi hello sanal makinenin yer alır.</span><span class="sxs-lookup"><span data-stu-id="109cc-128">IntelliTrace logs are collected tooa file in hello file system of hello virtual machine.</span></span> <span data-ttu-id="109cc-129">Merhaba günlükleri istediğinde, bir anlık görüntü zamandaki o noktada alınır ve tooyour yerel bilgisayara indirilir.</span><span class="sxs-lookup"><span data-stu-id="109cc-129">When you request hello logs, a snapshot is taken at that point in time and downloaded tooyour local computer.</span></span>

<span data-ttu-id="109cc-130">Hello Azure bulut hizmeti yayımlanan tooAzure sağlandıktan sonra IntelliTrace hello Azure ' etkin olmadığını belirleyebilirsiniz düğümünde **Sunucu Gezgini**hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="109cc-130">After hello Azure cloud service has been published tooAzure, you can determine if IntelliTrace has been enabled from hello Azure node in **Server Explorer**, as shown in hello following image:</span></span>

![Sunucu Gezgini - IntelliTrace etkin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC744134.png)

## <a name="download-intellitrace-logs-for-a-role-instance"></a><span data-ttu-id="109cc-132">Rol örneği için IntelliTrace günlüklerini indirin</span><span class="sxs-lookup"><span data-stu-id="109cc-132">Download IntelliTrace logs for a role instance</span></span>
<span data-ttu-id="109cc-133">Visual Studio kullanarak, aşağıdaki adımları izleyerek bir rol örneği için IntelliTrace günlüklerini yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="109cc-133">Using Visual Studio, you can download IntelliTrace logs for a role instance by following these steps:</span></span>

1. <span data-ttu-id="109cc-134">İçinde **Sunucu Gezgini**, hello genişletin **bulut Hizmetleri** düğümünü ve günlükleri toodownload istediğiniz rol örneği bulun.</span><span class="sxs-lookup"><span data-stu-id="109cc-134">In **Server Explorer**, expand hello **Cloud Services** node, and locate role instance whose logs you wish toodownload.</span></span> 

1. <span data-ttu-id="109cc-135">Merhaba rol örneği sağ tıklatın ve hello s bağlam menüsünden seçin **IntelliTrace günlüklerini görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="109cc-135">Right-click hello role instance, and from hello s context menu, select **View IntelliTrace Logs**.</span></span> 

    ![IntelliTrace günlüklerini menü seçeneği görüntüleyin](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/view-intellitrace-logs.png)

1. <span data-ttu-id="109cc-137">Merhaba IntelliTrace günlüklerini, yerel bilgisayarınızda indirilen tooa dosyasında bir dizin yer alır.</span><span class="sxs-lookup"><span data-stu-id="109cc-137">hello IntelliTrace logs are downloaded tooa file in a directory on your local computer.</span></span> <span data-ttu-id="109cc-138">Merhaba IntelliTrace günlüklerini, istek her zaman yeni bir anlık görüntüsü oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="109cc-138">Each time that you request hello IntelliTrace logs, a new snapshot is created.</span></span> <span data-ttu-id="109cc-139">Hello günlükleri karşıdan yüklenirken Visual Studio hello hello hello işlemin ilerlemesini görüntüler **Azure etkinlik günlüğü** penceresi.</span><span class="sxs-lookup"><span data-stu-id="109cc-139">While hello logs are being downloaded, Visual Studio displays hello progress of hello operation in hello **Azure Activity Log** window.</span></span> <span data-ttu-id="109cc-140">Hello aşağıdaki şekilde gösterildiği gibi daha fazla ayrıntı hello işlemi toosee hello kalem genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="109cc-140">As shown in hello following figure, you can expand hello line item for hello operation toosee more detail.</span></span>

![VST_IntelliTraceDownloadProgress](./media/vs-azure-tools-intellitrace-debug-published-cloud-services/IC745551.png)

<span data-ttu-id="109cc-142">Merhaba IntelliTrace günlüklerini karşıdan yüklenirken Visual Studio'da toowork devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="109cc-142">You can continue toowork in Visual Studio while hello IntelliTrace logs are downloading.</span></span> <span data-ttu-id="109cc-143">Merhaba günlük yükleme tamamlandığında, Visual Studio açılır.</span><span class="sxs-lookup"><span data-stu-id="109cc-143">When hello log has finished downloading, it opens in Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="109cc-144">Merhaba IntelliTrace günlüklerini özel durumları içerebilir, hello framework oluşturur ve daha sonra işler.</span><span class="sxs-lookup"><span data-stu-id="109cc-144">hello IntelliTrace logs might contain exceptions that hello framework generates and handles afterwards.</span></span> <span data-ttu-id="109cc-145">İç framework kod bunları güvenle yoksayabilirsiniz bir rolü, başlatma için normal bir parçası olarak bu özel durumları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="109cc-145">Internal framework code generates these exceptions as a normal part of starting up a role, so you may safely ignore them.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="109cc-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="109cc-146">Next steps</span></span>
- [<span data-ttu-id="109cc-147">Azure bulut hizmetlerinde hata ayıklama seçenekleri</span><span class="sxs-lookup"><span data-stu-id="109cc-147">Options for debugging Azure cloud services</span></span>](vs-azure-tools-debugging-cloud-services-overview.md)
- [<span data-ttu-id="109cc-148">Visual Studio kullanarak bir Azure bulut hizmetinde yayımlama</span><span class="sxs-lookup"><span data-stu-id="109cc-148">Publishing an Azure cloud service using Visual Studio</span></span>](vs-azure-tools-publishing-a-cloud-service.md)