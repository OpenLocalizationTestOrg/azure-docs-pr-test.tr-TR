---
title: "Visual Studio'da bağlı hizmetler kullanarak Azure Storage ekleme | Microsoft Docs"
description: "Visual Studio bağlı Hizmetleri Ekle iletişim kutusunu kullanarak uygulamanıza Azure depolama ekleme"
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
ms.openlocfilehash: 35638083cd75e1b751d00a9c8163a3bc7480f0cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a><span data-ttu-id="5830d-103">Visual Studio bağlantılı hizmetler kullanarak Azure depolama ekleme</span><span class="sxs-lookup"><span data-stu-id="5830d-103">Adding Azure storage by using Visual Studio Connected Services</span></span>
<span data-ttu-id="5830d-104">Visual Studio ile aşağıdakilerden herhangi birini Azure depolama birimine kullanarak bağlayabilirsiniz **bağlı Hizmetleri Ekle** iletişim:</span><span class="sxs-lookup"><span data-stu-id="5830d-104">With Visual Studio, you can connect any of the following to Azure Storage by using the **Add Connected Services** dialog:</span></span>

- <span data-ttu-id="5830d-105">C# bulut hizmeti</span><span class="sxs-lookup"><span data-stu-id="5830d-105">C# cloud service</span></span>
- <span data-ttu-id="5830d-106">.NET arka uç mobil hizmeti</span><span class="sxs-lookup"><span data-stu-id="5830d-106">.NET backend mobile service</span></span>
- <span data-ttu-id="5830d-107">ASP.NET Web sitesi veya hizmeti</span><span class="sxs-lookup"><span data-stu-id="5830d-107">ASP.NET website or service</span></span>
- <span data-ttu-id="5830d-108">ASP.NET Core hizmeti</span><span class="sxs-lookup"><span data-stu-id="5830d-108">ASP.NET Core service</span></span>
- <span data-ttu-id="5830d-109">Azure Web işi hizmeti</span><span class="sxs-lookup"><span data-stu-id="5830d-109">Azure WebJob service</span></span> 

<span data-ttu-id="5830d-110">Bağlantılı hizmeti işlevselliği tüm gerekli referanslar ve bağlantı kodu projenize ekler ve yapılandırma dosyalarına uygun şekilde değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5830d-110">The connected service functionality adds all the needed references and connection code to your project, and modifies your configuration files appropriately.</span></span> 

<span data-ttu-id="5830d-111">Tamamlandıktan sonra **bağlı Hizmetleri Ekle** sıraları, blob storage ile çalışmaya başlamak için gerekli olan adımları ayrıntılı belgeler görüntüler ve tabloları otomatik olarak iletişim.</span><span class="sxs-lookup"><span data-stu-id="5830d-111">After completion, the **Add Connected Services** dialog automatically displays documentation detailing the steps required to start working with blob storage, queues, and tables.</span></span>

## <a name="connect-to-azure-storage-using-the-connected-services-dialog"></a><span data-ttu-id="5830d-112">Azure depolama bağlantılı Hizmetler iletişim kutusunu kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="5830d-112">Connect to Azure Storage using the Connected Services dialog</span></span>
1. <span data-ttu-id="5830d-113">Projenizi Visual Studio'da açın</span><span class="sxs-lookup"><span data-stu-id="5830d-113">Open your project in Visual Studio</span></span>

1. <span data-ttu-id="5830d-114">İçinde **Çözüm Gezgini**, sağ tıklatın **bağlantılı Hizmetler** düğümünü ve bağlam menüsünden ve select **bağlı hizmet Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5830d-114">In **Solution Explorer**, right-click the **Connected Services** node, and, from the context menu, and select **Add Connected Service**.</span></span>
   
    ![Azure eklemek bağlı hizmet](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. <span data-ttu-id="5830d-116">İçinde **bağlantılı Hizmetler** sayfasında, **Azure Storage ile bulut depolama**.</span><span class="sxs-lookup"><span data-stu-id="5830d-116">In the **Connected Services** page, select **Cloud Storage with Azure Storage**.</span></span>
   
    ![Azure depolama ekleme](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. <span data-ttu-id="5830d-118">İçinde **Azure Storage** iletişim kutusu, varolan bir depolama hesabı seçin ve Seç **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5830d-118">In the **Azure Storage** dialog, select an existing storage account, and select **Add**.</span></span>
   
    <span data-ttu-id="5830d-119">Bir depolama hesabı oluşturmanız gerekiyorsa, sonraki adıma gidin.</span><span class="sxs-lookup"><span data-stu-id="5830d-119">If you need to create a storage account, go to the next step.</span></span> <span data-ttu-id="5830d-120">Aksi takdirde, 6. adıma atlayın.</span><span class="sxs-lookup"><span data-stu-id="5830d-120">Otherwise, skip to step 6.</span></span>
    
    ![Varolan bir depolama hesabı projeye ekleyin](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. <span data-ttu-id="5830d-122">Bir depolama hesabı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="5830d-122">To create a storage account:</span></span> 
   
   1. <span data-ttu-id="5830d-123">Seçin **yeni depolama hesabı oluşturma** iletişim kutusunun altındaki.</span><span class="sxs-lookup"><span data-stu-id="5830d-123">Select **Create a New Storage Account** at the bottom of the dialog.</span></span>

   1. <span data-ttu-id="5830d-124">Doldurmak **depolama hesabı oluştur** iletişim ve select **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="5830d-124">Fill out the **Create Storage Account** dialog, and select **Create**.</span></span>
      
       ![Yeni Azure depolama hesabı](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. <span data-ttu-id="5830d-126">Zaman **Azure Storage** iletişim kutusu görüntülendiğinde, yeni depolama hesabı listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5830d-126">When the **Azure Storage** dialog is displayed, the new storage account appears in the list.</span></span> <span data-ttu-id="5830d-127">Listede yeni depolama hesabı seçin ve Seç **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5830d-127">Select the new storage account in the list, and select **Add**.</span></span>

1. <span data-ttu-id="5830d-128">Bağlantılı hizmeti görünür altında depolama **hizmeti başvuruları** projenizin düğümü.</span><span class="sxs-lookup"><span data-stu-id="5830d-128">The storage connected service appears under the **Service References** node of your project.</span></span>
   
## <a name="how-your-project-is-modified"></a><span data-ttu-id="5830d-129">Projenizi nasıl değiştirilir</span><span class="sxs-lookup"><span data-stu-id="5830d-129">How your project is modified</span></span>
<span data-ttu-id="5830d-130">İletişim kutusu bitirdikten sonra Visual Studio başvuruları ekler ve belirli yapılandırma dosyalarını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="5830d-130">When you finish the dialog, Visual Studio adds references and modifies certain configuration files.</span></span> <span data-ttu-id="5830d-131">Özel değişiklikleri proje türüne bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="5830d-131">The specific changes depend on the project type:</span></span> 

- <span data-ttu-id="5830d-132">ASP.NET proje - [ne – ASP.NET projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span><span class="sxs-lookup"><span data-stu-id="5830d-132">ASP.NET project - [What happened – ASP.NET Projects](http://go.microsoft.com/fwlink/p/?LinkId=513126)</span></span>
- <span data-ttu-id="5830d-133">ASP.NET Core proje - [ne – ASP.NET 5 projeleri](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span><span class="sxs-lookup"><span data-stu-id="5830d-133">ASP.NET Core project - [What happened – ASP.NET 5 Projects](http://go.microsoft.com/fwlink/p/?LinkId=513124)</span></span> 
- <span data-ttu-id="5830d-134">Bulut hizmeti projesi (web rolleri ve çalışan rolleri) - [ne – bulut hizmeti projeleri](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span><span class="sxs-lookup"><span data-stu-id="5830d-134">Cloud service project (web roles and worker roles) - [What happened – Cloud Service projects](http://go.microsoft.com/fwlink/p/?LinkId=516965)</span></span>
- <span data-ttu-id="5830d-135">Web işi projesinin - [ne oldu - WebJob projeleri](visual-studio/vs-storage-webjobs-what-happened.md)</span><span class="sxs-lookup"><span data-stu-id="5830d-135">WebJob project - [What happened - WebJob projects](visual-studio/vs-storage-webjobs-what-happened.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5830d-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5830d-136">Next steps</span></span>
- [<span data-ttu-id="5830d-137">MSDN forumu: Azure depolama</span><span class="sxs-lookup"><span data-stu-id="5830d-137">MSDN Forum: Azure Storage</span></span>](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [<span data-ttu-id="5830d-138">Microsoft Azure depolama ekibi blogu</span><span class="sxs-lookup"><span data-stu-id="5830d-138">Microsoft Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
- [<span data-ttu-id="5830d-139">Azure Storage belgeleri</span><span class="sxs-lookup"><span data-stu-id="5830d-139">Azure Storage documentation</span></span>](https://docs.microsoft.com/azure/storage/)
