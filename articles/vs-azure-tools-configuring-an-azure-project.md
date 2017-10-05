---
title: "Bir Azure bulut hizmeti projesi ile Visual Studio'yu yapılandırma | Microsoft Docs"
description: "Bu proje için gereksinimlerinize bağlı olarak Visual Studio'da bir Azure bulut hizmeti projesi yapılandırmayı öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 799715093bd1a8c8e77e6cdb7168670dc263dfa5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="e0093-103">Bir Azure bulut hizmeti projesi ile Visual Studio'yu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e0093-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="e0093-104">Bu proje için gereksinimlerinize bağlı olarak, bir Azure bulut hizmeti projesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0093-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="e0093-105">Aşağıdaki kategorilerde ve proje özelliklerini ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e0093-105">You can set properties for the project for the following categories:</span></span>

- <span data-ttu-id="e0093-106">**Bir bulut hizmeti için Azure yayımlama** -Azure'a dağıtılan var olan bir bulut hizmetini yanlışlıkla silinmez emin olmak için bir özellik ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0093-106">**Publish a cloud service to Azure** - You can set a property to make sure that an existing cloud service deployed to Azure is not accidentally deleted.</span></span>
- <span data-ttu-id="e0093-107">**Çalıştırabilir veya yerel bilgisayarda bir bulut hizmetinde hata ayıklama** -kullanın ve Azure storage öykünücüsü başlatmak isteyip istemediğinizi belirtmek için bir hizmet yapılandırması seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0093-107">**Run or debug a cloud service on the local computer** - You can select a service configuration to use and indicate whether you want to start the Azure storage emulator.</span></span>
- <span data-ttu-id="e0093-108">**Bir bulut hizmet paketi oluşturulduğunda doğrulama** -bulut hizmet paketi sorunları dağıtır emin olmak için tüm uyarıları hata olarak değerlendirmek karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e0093-108">**Validate a cloud service package when it is created** - You can decide to treat any warnings as errors so that you can ensure that the cloud service package deploys without any issues.</span></span> 

## <a name="steps-to-configure-an-azure-cloud-service-project"></a><span data-ttu-id="e0093-109">Bir Azure bulut hizmeti projesi yapılandırma adımları</span><span class="sxs-lookup"><span data-stu-id="e0093-109">Steps to configure an Azure cloud service project</span></span>
1. <span data-ttu-id="e0093-110">Visual Studio'da bir bulut hizmeti projesi oluşturun veya açın</span><span class="sxs-lookup"><span data-stu-id="e0093-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="e0093-111">İçinde **Çözüm Gezgini**, projeye sağ tıklayın ve bağlam menüsünden seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="e0093-111">In **Solution Explorer**, right-click the project, and, from the context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="e0093-112">Proje özellikleri sayfasını seçin **geliştirme** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e0093-112">In the project's properties page, select the **Development** tab.</span></span>

    ![Proje Özellikleri menüsü](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="e0093-114">Ayarlama **var olan bir dağıtıma silmeden önce sor** için **doğru**.</span><span class="sxs-lookup"><span data-stu-id="e0093-114">Set **Prompt before deleting an existing deployment** to **True**.</span></span> <span data-ttu-id="e0093-115">Bu ayar Azure var olan bir dağıtıma yanlışlıkla silmeyin sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e0093-115">This setting helps to ensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="e0093-116">İstenen seçin **hizmet yapılandırmasını** çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama kullanmak istediğiniz hangi hizmet yapılandırmasını belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="e0093-116">Select the desired **Service configuration** to indicate which service configuration you want to use when you run or debug your cloud service locally.</span></span> <span data-ttu-id="e0093-117">Bir rol için bir hizmet yapılandırmasının nasıl değiştirileceği hakkında daha fazla bilgi için bkz: [Visual Studio ile bir Azure bulut hizmeti için rolleri yapılandırmak nasıl](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="e0093-117">For more information on how to modify a service configuration for a role, see [How to configure the roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="e0093-118">Ayarlama **Başlat Azure storage öykünücüsü** için **True** çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama Azure storage öykünücüsü başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="e0093-118">Set **Start Azure storage emulator** to **True** to start the Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="e0093-119">Ayarlama **uyarıları hata ele** için **True** paketi doğrulama hatası varsa yayımlayamıyor emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="e0093-119">Set **Treat warnings as errors** to **True** to make sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="e0093-120">Ayarlama **web projesi bağlantı noktalarını kullanacak** için **True** web rolünüz aynı bağlantı noktasını kullandığından emin olmak için her zaman, yerel IIS Express olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="e0093-120">Set **Use web project ports** to **True** to make sure that your web role uses the same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="e0093-121">Visual Studio araç çubuğundan seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="e0093-121">From the Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0093-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0093-122">Next steps</span></span>
- [<span data-ttu-id="e0093-123">Birden çok hizmet yapılandırmalarını kullanarak bir Azure projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e0093-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

