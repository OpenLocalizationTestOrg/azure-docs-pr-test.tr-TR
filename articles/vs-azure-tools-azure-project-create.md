---
title: bir Azure bulut hizmeti projesini Visual Studio ile aaaCreating | Microsoft Docs
description: "Şimdi toocreate bir Azure bulut hizmeti projesini Visual Studio ile bilgi edinin"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="3746f-103">Visual Studio ile bir Azure bulut hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="3746f-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="3746f-104">Hello Azure Araçları Visual Studio için Azure bulut hizmeti oluşturmanıza olanak sağlayan bir proje şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="3746f-104">hello Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="3746f-105">Visual Studio Hello Proje oluşturulduktan sonra tooconfigure sağlar, hata ayıklama ve hello bulut hizmeti tooAzure dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3746f-105">Once hello project has been created, Visual Studio enables you tooconfigure, debug, and deploy hello cloud service tooAzure.</span></span>

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="3746f-106">Adımları toocreate Visual Studio'da bir Azure bulut hizmeti projesi</span><span class="sxs-lookup"><span data-stu-id="3746f-106">Steps toocreate an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="3746f-107">Bu bölümde bir veya daha fazla web rolleri ile Visual Studio'da bir Azure bulut hizmeti projesi oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="3746f-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="3746f-108">Visual Studio'yu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="3746f-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="3746f-109">Merhaba ana menüde seçin **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="3746f-109">On hello main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="3746f-110">Seçin **bulut** hello Visual C# veya Visual Basic proje şablonu düğümleri ve seçin **Azure bulut hizmeti** şablonları hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="3746f-110">Select **Cloud** from hello Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from hello list of templates.</span></span>

    ![Yeni Azure bulut hizmeti](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="3746f-112">Merhaba projenizin toouse toodevelop istediğiniz .NET Framework sürümünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="3746f-112">Specify which version of hello .NET Framework you want toouse toodevelop your project.</span></span>

1. <span data-ttu-id="3746f-113">Bir ad ve projenizin konumunu ve hello çözüm için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="3746f-113">Enter a name and location for your project and a name for hello solution.</span></span> 

1. <span data-ttu-id="3746f-114">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3746f-114">Select **OK**.</span></span>

1. <span data-ttu-id="3746f-115">Merhaba, **yeni Microsoft Azure bulut hizmeti** iletişim, tooadd istediğiniz ve hello sağ ok düğmesine tooadd seçin select hello rolleri bunları tooyour çözümü.</span><span class="sxs-lookup"><span data-stu-id="3746f-115">In hello **New Microsoft Azure Cloud Service** dialog, select hello roles that you want tooadd, and choose hello right arrow button tooadd them tooyour solution.</span></span>

    ![Yeni Azure bulut hizmeti rollerinizi seçin](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="3746f-117">toorename eklediğiniz, bir rol hello hello rolünde gidildiğinde **yeni Microsoft Azure bulut hizmeti** iletişim kutusunda ve hello bağlam menüsünden seçin **yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="3746f-117">toorename a role that you've added, hover on hello role in hello **New Microsoft Azure Cloud Service** dialog, and, from hello context menu, select **Rename**.</span></span> <span data-ttu-id="3746f-118">Bir rol, çözümünüz içinde adlandırabilirsiniz (Merhaba içinde **Çözüm Gezgini**) eklendikten sonra.</span><span class="sxs-lookup"><span data-stu-id="3746f-118">You can also rename a role within your solution (in hello **Solution Explorer**) after it has been added.</span></span>

    ![Azure bulut hizmeti rolü yeniden adlandır](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="3746f-120">Merhaba Visual Studio Azure project hello çözümde ilişkilendirmeleri toohello rol proje yok.</span><span class="sxs-lookup"><span data-stu-id="3746f-120">hello Visual Studio Azure project has associations toohello role projects in hello solution.</span></span> <span data-ttu-id="3746f-121">Merhaba proje de hello içeriyor *hizmet tanımı dosyası* ve *hizmet yapılandırma dosyası*:</span><span class="sxs-lookup"><span data-stu-id="3746f-121">hello project also includes hello *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="3746f-122">**Hizmet tanımı dosyası** -uygulama, hangi rollerin gerekli dahil olmak üzere, uç noktaları ve sanal makine boyutu hello çalışma zamanı ayarlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3746f-122">**Service definition file** - Defines hello runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="3746f-123">**Hizmet yapılandırma dosyası** -kaç bir rolün örnekleri çalıştırılır ve hello bir rol için tanımlanan hello ayarlarının değerleri yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="3746f-123">**Service configuration file** - Configures how many instances of a role are run and hello values of hello settings defined for a role.</span></span> 

<span data-ttu-id="3746f-124">Bu dosyalar hakkında daha fazla bilgi için bkz: [hello rolleri bir Azure bulut hizmeti için Visual Studio ile yapılandırma](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="3746f-124">For more information about these files, see [Configure hello Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3746f-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3746f-125">Next steps</span></span>
- [<span data-ttu-id="3746f-126">Visual Studio ile Azure bulut hizmeti projelerinde rollerini yönetme</span><span class="sxs-lookup"><span data-stu-id="3746f-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
