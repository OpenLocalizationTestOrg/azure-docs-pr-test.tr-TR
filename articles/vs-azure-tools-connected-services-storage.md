---
title: "Visual Studio'da bağlı hizmetler kullanarak Azure Storage aaaAdd | Microsoft Docs"
description: "Merhaba Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak Azure Storage tooyour uygulama Ekle"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="6f56d-103">Visual Studio bağlantılı hizmetler kullanarak Azure depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="6f56d-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="6f56d-104">Visual Studio ile tooAzure depolama hello kullanarak aşağıdaki hello hiçbirini bağlayabilirsiniz **bağlı Hizmetleri Ekle** iletişim:</span><span class="sxs-lookup"><span data-stu-id="6f56d-104">With Visual Studio, you can connect any of hello following tooAzure Storage by using hello **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="6f56d-105">C# bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f56d-105">C# cloud service</span></span>
- <span data-ttu-id="6f56d-106">.NET arka uç mobil hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f56d-106">.NET backend mobile service</span></span>
- <span data-ttu-id="6f56d-107">ASP.NET Web sitesi veya hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f56d-107">ASP.NET website or service</span></span>
- <span data-ttu-id="6f56d-108">ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f56d-108">ASP.NET Core service</span></span>
- <span data-ttu-id="6f56d-109">Azure Web işi hizmeti</span><span class="sxs-lookup"><span data-stu-id="6f56d-109">Azure WebJob service</span></span> 

<span data-ttu-id="6f56d-110">Merhaba bağlı hizmeti işlevselliği tüm gerekli hello başvuruları ve bağlantı kod tooyour projesi ekler ve yapılandırma dosyalarına uygun şekilde değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6f56d-110">hello connected service functionality adds all hello needed references and connection code tooyour project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="6f56d-111">Tamamlandıktan sonra hello **bağlı Hizmetleri Ekle** iletişim hello adımları gerekli toostart blob storage'ı, kuyruklar ve tablolar çalışma ayrıntılı belgeler otomatik olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="6f56d-111">After completion, hello **Add Connected Services** dialog automatically displays documentation detailing hello steps required toostart working with blob storage, queues, and tables.</span></span>

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a><span data-ttu-id="6f56d-112">TooAzure hello bağlantılı hizmetler kullanarak depolama Bağlan iletişim kutusu</span><span class="sxs-lookup"><span data-stu-id="6f56d-112">Connect tooAzure Storage using hello Connected Services dialog</span></span>
1. <span data-ttu-id="6f56d-113">Projenizi Visual Studio'da açın</span><span class="sxs-lookup"><span data-stu-id="6f56d-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="6f56d-114">İçinde **Çözüm Gezgini**, sağ hello **bağlantılı Hizmetler** düğümü ve hello bağlam menüsünden ve select **bağlı hizmet Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6f56d-114">In **Solution Explorer**, right-click hello **Connected Services** node, and, from hello context menu, and select **Add Connected Service**.</span></span>
   
    ![Azure eklemek bağlı hizmet](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="6f56d-116">Merhaba, **bağlantılı Hizmetler** sayfasında, **Azure Storage ile bulut depolama**.</span><span class="sxs-lookup"><span data-stu-id="6f56d-116">In hello **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure depolama ekleme](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="6f56d-118">Merhaba, **Azure Storage** iletişim kutusu, varolan bir depolama hesabı seçin ve Seç **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6f56d-118">In hello **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="6f56d-119">Bir depolama hesabı toocreate gerekiyorsa, toohello sonraki adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="6f56d-119">If you need toocreate a storage account, go toohello next step.</span></span> <span data-ttu-id="6f56d-120">Aksi halde toostep 6 geçin.</span><span class="sxs-lookup"><span data-stu-id="6f56d-120">Otherwise, skip toostep 6.</span></span>
    
    ![Var olan depolama hesabı tooproject Ekle](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="6f56d-122">toocreate bir depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="6f56d-122">toocreate a storage account:</span></span> 
   
   1. <span data-ttu-id="6f56d-123">Seçin **yeni depolama hesabı oluşturma** hello iletişim hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="6f56d-123">Select **Create a New Storage Account** at hello bottom of hello dialog.</span></span>

   1. <span data-ttu-id="6f56d-124">Merhaba doldurun **depolama hesabı oluştur** iletişim ve select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6f56d-124">Fill out hello **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Yeni Azure depolama hesabı](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="6f56d-126">Ne zaman hello **Azure Storage** iletişim kutusu gösterilir, hello yeni depolama hesabı hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="6f56d-126">When hello **Azure Storage** dialog is displayed, hello new storage account appears in hello list.</span></span> <span data-ttu-id="6f56d-127">Merhaba listede Hello yeni depolama hesabı seçin ve Seç **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6f56d-127">Select hello new storage account in hello list, and select **Add**.</span></span>

1. <span data-ttu-id="6f56d-128">Merhaba depolama bağlı hizmeti hello altında görünür **hizmeti başvuruları** projenizin düğümü.</span><span class="sxs-lookup"><span data-stu-id="6f56d-128">hello storage connected service appears under hello **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="6f56d-129">Projenizi nasıl değiştirilir</span><span class="sxs-lookup"><span data-stu-id="6f56d-129">How your project is modified</span></span>
<span data-ttu-id="6f56d-130">Merhaba iletişim bitirdikten sonra Visual Studio başvuruları ekler ve belirli yapılandırma dosyalarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="6f56d-130">When you finish hello dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="6f56d-131">Merhaba belirli değişiklikleri hello proje türüne bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="6f56d-131">hello specific changes depend on hello project type:</span></span> 

- <span data-ttu-id="6f56d-132">ASP.NET proje - [ne – ASP.NET projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="6f56d-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="6f56d-133">ASP.NET Core proje - [ne – ASP.NET 5 projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="6f56d-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="6f56d-134">Bulut hizmeti projesi (web rolleri ve çalışan rolleri) - [ne – bulut hizmeti projeleri](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="6f56d-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="6f56d-135">Web işi projesinin - [ne oldu - WebJob projeleri](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="6f56d-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f56d-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6f56d-136">Next steps</span></span>
- [<span data-ttu-id="6f56d-137">MSDN forumu: Azure depolama</span><span class="sxs-lookup"><span data-stu-id="6f56d-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="6f56d-138">Microsoft Azure depolama ekibi blogu</span><span class="sxs-lookup"><span data-stu-id="6f56d-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="6f56d-139">Azure Storage belgeleri</span><span class="sxs-lookup"><span data-stu-id="6f56d-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
