---
title: bir Azure bulut hizmeti projesini Visual Studio ile aaaConfigure | Microsoft Docs
description: "Nasıl tooconfigure bir Azure bulut hizmeti projesini Visual Studio'da o projesi, gereksinimlerinize bağlı olarak öğrenin."
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
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="ddfa3-103">Bir Azure bulut hizmeti projesi ile Visual Studio'yu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ddfa3-103">Configure an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="ddfa3-104">Bu proje için gereksinimlerinize bağlı olarak, bir Azure bulut hizmeti projesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-104">You can configure an Azure cloud service project, depending on your requirements for that project.</span></span> <span data-ttu-id="ddfa3-105">Kategoriler aşağıdaki hello hello proje özelliklerini ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ddfa3-105">You can set properties for hello project for hello following categories:</span></span>

- <span data-ttu-id="ddfa3-106">**Bir bulut hizmeti tooAzure yayımlama** -var olan bir bulut dağıtılan hizmet tooAzure yanlışlıkla silinmez emin bir özellik toomake ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-106">**Publish a cloud service tooAzure** - You can set a property toomake sure that an existing cloud service deployed tooAzure is not accidentally deleted.</span></span>
- <span data-ttu-id="ddfa3-107">**Çalıştırmak veya hello yerel bilgisayardaki bir bulut hizmetinde hata ayıklama** -hizmet yapılandırma toouse seçin ve toostart hello Azure storage öykünücüsü isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-107">**Run or debug a cloud service on hello local computer** - You can select a service configuration toouse and indicate whether you want toostart hello Azure storage emulator.</span></span>
- <span data-ttu-id="ddfa3-108">**Bir bulut hizmet paketi oluşturulduğunda doğrulama** -tüm uyarıları hata olarak o hello bulut hizmet paketi sağlayabilirsiniz böylece herhangi bir sorun oluşmadan dağıtır tootreat karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-108">**Validate a cloud service package when it is created** - You can decide tootreat any warnings as errors so that you can ensure that hello cloud service package deploys without any issues.</span></span> 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a><span data-ttu-id="ddfa3-109">Adımları tooconfigure bir Azure bulut hizmeti projesi</span><span class="sxs-lookup"><span data-stu-id="ddfa3-109">Steps tooconfigure an Azure cloud service project</span></span>
1. <span data-ttu-id="ddfa3-110">Visual Studio'da bir bulut hizmeti projesi oluşturun veya açın</span><span class="sxs-lookup"><span data-stu-id="ddfa3-110">Open or create a cloud service project in Visual Studio</span></span>

1. <span data-ttu-id="ddfa3-111">İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-111">In **Solution Explorer**, right-click hello project, and, from hello context menu, select **Properties**.</span></span>
   
1. <span data-ttu-id="ddfa3-112">Merhaba Hello projenin Özellikler sayfasında, seçin **geliştirme** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-112">In hello project's properties page, select hello **Development** tab.</span></span>

    ![Proje Özellikleri menüsü](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. <span data-ttu-id="ddfa3-114">Ayarlama **var olan bir dağıtıma silmeden önce sor** çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-114">Set **Prompt before deleting an existing deployment** too**True**.</span></span> <span data-ttu-id="ddfa3-115">Bu ayar Azure var olan bir dağıtıma yanlışlıkla silmeyin tooensure yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-115">This setting helps tooensure you don't accidentally delete an existing deployment in Azure</span></span>

1. <span data-ttu-id="ddfa3-116">İstenen select hello **hizmet yapılandırmasını** tooindicate hangi hizmet yapılandırmasını toouse çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama istiyor.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-116">Select hello desired **Service configuration** tooindicate which service configuration you want toouse when you run or debug your cloud service locally.</span></span> <span data-ttu-id="ddfa3-117">Hakkında daha fazla bilgi için bir rol için bir hizmet yapılandırması toomodify bkz [nasıl tooconfigure hello rolleri bir Azure için bulut hizmeti Visual Studio ile](./vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="ddfa3-117">For more information on how toomodify a service configuration for a role, see [How tooconfigure hello roles for an Azure cloud service with Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

1. <span data-ttu-id="ddfa3-118">Ayarlama **Başlat Azure storage öykünücüsü** çok**True** çalıştırdığınızda veya Bulut hizmeti yerel olarak hata ayıklama toostart hello Azure storage öykünücüsü.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-118">Set **Start Azure storage emulator** too**True** toostart hello Azure storage emulator when you run or debug your cloud service locally.</span></span>

1. <span data-ttu-id="ddfa3-119">Ayarlama **uyarıları hata ele** çok**True** toomake paketi doğrulama hatası varsa yayımlayamıyor emin.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-119">Set **Treat warnings as errors** too**True** toomake sure you cannot publish if there are package validation errors.</span></span>

1. <span data-ttu-id="ddfa3-120">Ayarlama **web projesi bağlantı noktalarını kullanacak** çok**True** toomake web rolünüz aynı bağlantı noktası her hello kullandığından emin zaman onu yerel IIS Express olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-120">Set **Use web project ports** too**True** toomake sure that your web role uses hello same port each time it starts locally in IIS Express.</span></span>

1. <span data-ttu-id="ddfa3-121">Merhaba Visual Studio araç çubuğundan seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="ddfa3-121">From hello Visual Studio toolbar, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddfa3-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ddfa3-122">Next steps</span></span>
- [<span data-ttu-id="ddfa3-123">Birden çok hizmet yapılandırmalarını kullanarak bir Azure projesi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ddfa3-123">Configure an Azure project using multiple service configurations</span></span>](vs-azure-tools-multiple-services-project-configurations.md)

