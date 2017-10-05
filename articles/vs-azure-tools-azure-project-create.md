---
title: "Visual Studio ile bir Azure bulut hizmeti projesi oluşturma | Microsoft Docs"
description: "Şimdi Visual Studio ile bir Azure bulut hizmeti projesi oluşturmayı öğrenin"
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
ms.openlocfilehash: 1f6ded87b551f660853ea4eb0548f3d942e28fa8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a><span data-ttu-id="7af8a-103">Visual Studio ile bir Azure bulut hizmeti projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7af8a-103">Creating an Azure cloud service project with Visual Studio</span></span>
<span data-ttu-id="7af8a-104">Visual Studio için Azure Araçları, bir Azure bulut hizmeti oluşturmanıza olanak sağlayan bir proje şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="7af8a-104">The Azure Tools for Visual Studio provides a project template that lets you create an Azure cloud service.</span></span> <span data-ttu-id="7af8a-105">Proje oluşturulduktan sonra yapılandırmak, hata ayıklama ve bulut hizmeti Azure'a dağıtmak Visual Studio sağlar.</span><span class="sxs-lookup"><span data-stu-id="7af8a-105">Once the project has been created, Visual Studio enables you to configure, debug, and deploy the cloud service to Azure.</span></span>

## <a name="steps-to-create-an-azure-cloud-service-project-in-visual-studio"></a><span data-ttu-id="7af8a-106">Visual Studio'da bir Azure bulut hizmeti projesi oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="7af8a-106">Steps to create an Azure cloud service project in Visual Studio</span></span>
<span data-ttu-id="7af8a-107">Bu bölümde bir veya daha fazla web rolleri ile Visual Studio'da bir Azure bulut hizmeti projesi oluşturmada size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="7af8a-107">This section walks you through creating an Azure cloud service project in Visual Studio with one or more web roles.</span></span>  

1. <span data-ttu-id="7af8a-108">Visual Studio'yu yönetici olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="7af8a-108">Start Visual Studio as an administrator.</span></span>

1. <span data-ttu-id="7af8a-109">Ana menüde seçin **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="7af8a-109">On the main menu, select **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="7af8a-110">Seçin **bulut** Visual C# veya Visual Basic proje şablonu düğümleri ve seçin **Azure bulut hizmeti** şablonları listesinden.</span><span class="sxs-lookup"><span data-stu-id="7af8a-110">Select **Cloud** from the Visual C# or Visual Basic project template nodes, and select **Azure Cloud Service** from the list of templates.</span></span>

    ![Yeni Azure bulut hizmeti](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. <span data-ttu-id="7af8a-112">Projenizi geliştirmek için kullanmak istediğiniz .NET Framework sürümünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="7af8a-112">Specify which version of the .NET Framework you want to use to develop your project.</span></span>

1. <span data-ttu-id="7af8a-113">Bir ad ve projenizin konumunu ve çözüm için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="7af8a-113">Enter a name and location for your project and a name for the solution.</span></span> 

1. <span data-ttu-id="7af8a-114">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7af8a-114">Select **OK**.</span></span>

1. <span data-ttu-id="7af8a-115">İçinde **yeni Microsoft Azure bulut hizmeti** iletişim kutusunda, eklemek istediğiniz rolü seçin ve sağ ok düğmesine çözümünüze ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7af8a-115">In the **New Microsoft Azure Cloud Service** dialog, select the roles that you want to add, and choose the right arrow button to add them to your solution.</span></span>

    ![Yeni Azure bulut hizmeti rollerinizi seçin](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. <span data-ttu-id="7af8a-117">Eklediğiniz bir rolü yeniden adlandırmak için vurgulu rolünde üzerinde **yeni Microsoft Azure bulut hizmeti** iletişim kutusunda ve bağlam menüsünden seçin **yeniden adlandırma**.</span><span class="sxs-lookup"><span data-stu-id="7af8a-117">To rename a role that you've added, hover on the role in the **New Microsoft Azure Cloud Service** dialog, and, from the context menu, select **Rename**.</span></span> <span data-ttu-id="7af8a-118">Bir rol, çözümünüz içinde adlandırabilirsiniz (içinde **Çözüm Gezgini**) eklendikten sonra.</span><span class="sxs-lookup"><span data-stu-id="7af8a-118">You can also rename a role within your solution (in the **Solution Explorer**) after it has been added.</span></span>

    ![Azure bulut hizmeti rolü yeniden adlandır](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

<span data-ttu-id="7af8a-120">Visual Studio Azure project çözümdeki rol projelerine ilişkileri içerir.</span><span class="sxs-lookup"><span data-stu-id="7af8a-120">The Visual Studio Azure project has associations to the role projects in the solution.</span></span> <span data-ttu-id="7af8a-121">Proje ayrıca içeriyor *hizmet tanımı dosyası* ve *hizmet yapılandırma dosyası*:</span><span class="sxs-lookup"><span data-stu-id="7af8a-121">The project also includes the *service definition file* and *service configuration file*:</span></span>

- <span data-ttu-id="7af8a-122">**Hizmet tanımı dosyası** -uygulama, hangi rollerin gerekli dahil olmak üzere, uç noktaları ve sanal makine boyutu için çalışma zamanı ayarları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7af8a-122">**Service definition file** - Defines the runtime settings for your application, including what roles are required, endpoints, and virtual machine size.</span></span> 
- <span data-ttu-id="7af8a-123">**Hizmet yapılandırma dosyası** -kaç rol çalıştırın ve bir rol için tanımlanan ayarlarının değerleri örnekleridir yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7af8a-123">**Service configuration file** - Configures how many instances of a role are run and the values of the settings defined for a role.</span></span> 

<span data-ttu-id="7af8a-124">Bu dosyalar hakkında daha fazla bilgi için bkz: [rolleri bir Azure bulut hizmeti için Visual Studio ile yapılandırma](vs-azure-tools-configure-roles-for-cloud-service.md).</span><span class="sxs-lookup"><span data-stu-id="7af8a-124">For more information about these files, see [Configure the Roles for an Azure cloud service with Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7af8a-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7af8a-125">Next steps</span></span>
- [<span data-ttu-id="7af8a-126">Visual Studio ile Azure bulut hizmeti projelerinde rollerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7af8a-126">Managing roles in Azure cloud service projects with Visual Studio</span></span>](./vs-azure-tools-cloud-service-project-managing-roles.md)
