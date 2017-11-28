---
title: "Intellij için Azure Gezgini'ni kullanarak depolama hesaplarını yönetme | Microsoft Docs"
description: "Azure storage hesaplarınızı Intellij için Azure Gezgini'ni kullanarak yönetmeyi öğrenin."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a1b56cc2751fc43a1ad6917eca77eec460f26694
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-storage-accounts-by-using-the-azure-explorer-for-intellij"></a><span data-ttu-id="ee415-103">Intellij için Azure Gezgini'ni kullanarak depolama hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="ee415-103">Manage storage accounts by using the Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="ee415-104">Intellij için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından Intellij tümleşik geliştirme ortamı (IDE) içindeki depolama hesaplarını yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee415-104">The Azure Explorer, which is part of the Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside the IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-intellij"></a><span data-ttu-id="ee415-105">Intellij içinde depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee415-105">Create a storage account in IntelliJ</span></span>

<span data-ttu-id="ee415-106">Azure Gezgini'ni kullanarak bir depolama hesabı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ee415-106">To create a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ee415-107">Azure hesabınızı kullanarak oturum [oturum açma yönergeleri Eclipse için Azure Araç Seti için].</span><span class="sxs-lookup"><span data-stu-id="ee415-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span> 

2. <span data-ttu-id="ee415-108">İçinde **Azure Gezgini** görüntülemek için Genişlet **Azure** düğümünü sağ tıklatın **depolama hesapları**ve ardından **depolama hesabı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ee415-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Depolama hesabı komut oluşturma][CS01]

3. <span data-ttu-id="ee415-110">İçinde **depolama hesabı oluştur** iletişim kutusunda, aşağıdaki seçenekleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="ee415-110">In the **Create Storage Account** dialog box, specify the following options:</span></span>

   ![Yeni depolama hesabı iletişim kutusu oluşturma][CS02]

   * <span data-ttu-id="ee415-112">**Ad**: yeni depolama hesabı adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-112">**Name**: Specifies the name for the new storage account.</span></span>

   * <span data-ttu-id="ee415-113">**Tür hesap**: (örneğin "Blob Depolama") oluşturmak için depolama hesabı türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-113">**Account kind**: Specifies the type of storage account to create (for example, "Blob storage").</span></span> <span data-ttu-id="ee415-114">Daha fazla bilgi için bkz: [Azure storage hesapları hakkında].</span><span class="sxs-lookup"><span data-stu-id="ee415-114">For more information, see [About Azure storage accounts].</span></span> 

   * <span data-ttu-id="ee415-115">**Performans**: Seçili yayımcıdan (örneğin, "Premium") kullanmak için sunumu hangi depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-115">**Performance**: Specifies which storage account offering to use from the selected publisher (for example, "Premium").</span></span> <span data-ttu-id="ee415-116">Daha fazla bilgi için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri].</span><span class="sxs-lookup"><span data-stu-id="ee415-116">For more information, see [Azure storage scalability and performance targets].</span></span> 

   * <span data-ttu-id="ee415-117">**Çoğaltma**: depolama hesabı (örneğin, "bölgesel olarak yedekli") için çoğaltma belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-117">**Replication**: Specifies the replication for the storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="ee415-118">Daha fazla bilgi için bkz: [Azure storage çoğaltma].</span><span class="sxs-lookup"><span data-stu-id="ee415-118">For more information, see [Azure storage replication].</span></span> 

   * <span data-ttu-id="ee415-119">**Abonelik**: yeni depolama hesabı için kullanmak istediğiniz Azure aboneliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-119">**Subscription**: Specifies the Azure subscription that you want to use for the new storage account.</span></span>

   * <span data-ttu-id="ee415-120">**Konum**: Burada, depolama hesabı oluşturulur (örneğin, "Batı ABD") konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-120">**Location**: Specifies the location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="ee415-121">**Kaynak grubu**: kaynak grubu, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-121">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="ee415-122">Aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="ee415-122">Select one of the following options:</span></span>
      * <span data-ttu-id="ee415-123">**Yeni Oluştur**: yeni bir kaynak grubu oluşturmak istediğiniz belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-123">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="ee415-124">**Var olanı kullan**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.</span><span class="sxs-lookup"><span data-stu-id="ee415-124">**Use existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

4. <span data-ttu-id="ee415-125">Yukarıdaki seçeneklerin tümü belirledikten sonra tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ee415-125">When you have specified all of the preceding options, click **OK**.</span></span>

## <a name="create-a-storage-container-in-intellij"></a><span data-ttu-id="ee415-126">Intellij içinde bir depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee415-126">Create a storage container in IntelliJ</span></span>

<span data-ttu-id="ee415-127">Azure Gezgini'ni kullanarak bir depolama kapsayıcısı oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ee415-127">To create a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ee415-128">Azure Gezgini görünümünde bir kapsayıcı oluşturmak ve ardından istediğiniz depolama hesabına sağ **oluşturma blob kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="ee415-128">In the Azure Explorer view, right-click the storage account where you want to create a container, and then click **Create blob container**.</span></span>

   ![BLOB kapsayıcı komut oluşturma][CC01]

2. <span data-ttu-id="ee415-130">İçinde **oluşturma blob kapsayıcısı** iletişim kutusunda, kapsayıcı adını belirtin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="ee415-130">In the **Create blob container** dialog box, specify the name for your container, and then click **OK**.</span></span> <span data-ttu-id="ee415-131">Depolama kapsayıcıları adlandırma hakkında daha fazla bilgi için bkz: [adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran].</span><span class="sxs-lookup"><span data-stu-id="ee415-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![Depolama kapsayıcısı iletişim kutusu oluşturma][CC02]

## <a name="delete-a-storage-container-in-intellij"></a><span data-ttu-id="ee415-133">Intellij depolama kapsayıcısında Sil</span><span class="sxs-lookup"><span data-stu-id="ee415-133">Delete a storage container in IntelliJ</span></span>

<span data-ttu-id="ee415-134">Azure Gezgini'ni kullanarak bir depolama kapsayıcısı silmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ee415-134">To delete a storage container by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ee415-135">Azure Gezgini görünümünde depolama kapsayıcıya sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ee415-135">In the Azure Explorer view, right-click the storage container, and then click **Delete**.</span></span>

   ![Depolama kapsayıcısı komutu silme][DC01]

2. <span data-ttu-id="ee415-137">Onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ee415-137">In the confirmation window, click **Yes**.</span></span>

   ![Depolama kapsayıcısı onay penceresi Sil][DC02]

## <a name="delete-a-storage-account-in-intellij"></a><span data-ttu-id="ee415-139">Intellij bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="ee415-139">Delete a storage account in IntelliJ</span></span>

<span data-ttu-id="ee415-140">Azure Gezgini'ni kullanarak bir depolama hesabını silmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ee415-140">To delete a storage account by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ee415-141">İçinde **Azure Gezgini** görüntülemek, depolama hesabına sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ee415-141">In the **Azure Explorer** view, right-click the storage account, and then select **Delete**.</span></span>

   ![Depolama hesabı menü silme][DS01]

2. <span data-ttu-id="ee415-143">Onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ee415-143">In the confirmation window, click **Yes**.</span></span>

   ![Depolama hesabı onay penceresi Sil][DS02]

## <a name="next-steps"></a><span data-ttu-id="ee415-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee415-145">Next steps</span></span>
<span data-ttu-id="ee415-146">Azure depolama hesapları hakkında daha fazla bilgi için boyutlar ve fiyatlandırma, aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="ee415-146">For more information about Azure storage accounts, sizes, and pricing, see the following resources:</span></span>

* <span data-ttu-id="ee415-147">[Microsoft Azure Depolama'ya Giriş]</span><span class="sxs-lookup"><span data-stu-id="ee415-147">[Introduction to Microsoft Azure Storage]</span></span>
* <span data-ttu-id="ee415-148">[Azure storage hesapları hakkında]</span><span class="sxs-lookup"><span data-stu-id="ee415-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="ee415-149">Azure depolama hesabı boyutları</span><span class="sxs-lookup"><span data-stu-id="ee415-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="ee415-150">[Windows Azure depolama hesapları için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="ee415-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="ee415-151">[Linux depolama hesaplarını Azure boyutları]</span><span class="sxs-lookup"><span data-stu-id="ee415-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="ee415-152">Azure depolama hesabı fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="ee415-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="ee415-153">[Windows depolama hesabı fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="ee415-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="ee415-154">[Linux depolama hesabı fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="ee415-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="ee415-155">Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="ee415-155">For more information about Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="ee415-156">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="ee415-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ee415-157">[Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="ee415-157">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ee415-158">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="ee415-158">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ee415-159">[oturum açma yönergeleri Eclipse için Azure Araç Seti için]</span><span class="sxs-lookup"><span data-stu-id="ee415-159">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ee415-160">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="ee415-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="ee415-161">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="ee415-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ee415-162">[Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="ee415-162">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ee415-163">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="ee415-163">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ee415-164">[Oturum açma Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="ee415-164">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ee415-165">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="ee415-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="ee415-166">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="ee415-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="ee415-167">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="ee415-167">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="ee415-168">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="ee415-168">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="ee415-169">[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ee415-169">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ee415-170">[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ee415-170">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ee415-171">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="ee415-171">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="ee415-172">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="ee415-172">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="ee415-173">[oturum açma yönergeleri Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="ee415-173">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="ee415-174">[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="ee415-174">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="ee415-175">[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ee415-175">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="ee415-176">[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ee415-176">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="ee415-177">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="ee415-177">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="ee415-178">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ee415-178">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="ee415-179">[Microsoft Azure Depolama'ya Giriş]: /azure/storage/storage-introduction</span><span class="sxs-lookup"><span data-stu-id="ee415-179">[Introduction to Microsoft Azure Storage]: /azure/storage/storage-introduction</span></span>
<span data-ttu-id="ee415-180">[Azure storage hesapları hakkında]: /azure/storage/storage-create-storage-account</span><span class="sxs-lookup"><span data-stu-id="ee415-180">[About Azure storage accounts]: /azure/storage/storage-create-storage-account</span></span>
<span data-ttu-id="ee415-181">[Azure storage çoğaltma]: /azure/storage/storage-redundancy</span><span class="sxs-lookup"><span data-stu-id="ee415-181">[Azure storage replication]: /azure/storage/storage-redundancy</span></span>
<span data-ttu-id="ee415-182">[Azure storage ölçeklenebilirlik ve performans hedefleri]: /azure/storage/storage-scalability-targets</span><span class="sxs-lookup"><span data-stu-id="ee415-182">[Azure storage scalability and Performance Targets]: /azure/storage/storage-scalability-targets</span></span>
<span data-ttu-id="ee415-183">[adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran]: http://go.microsoft.com/fwlink/?LinkId=255555</span><span class="sxs-lookup"><span data-stu-id="ee415-183">[Naming and referencing containers, blobs, and metadata]: http://go.microsoft.com/fwlink/?LinkId=255555</span></span>

<span data-ttu-id="ee415-184">[Windows Azure depolama hesapları için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="ee415-184">[Sizes for Windows storage accounts in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="ee415-185">[Linux depolama hesaplarını Azure boyutları]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="ee415-185">[Sizes for Linux storage accounts in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="ee415-186">[Windows depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="ee415-186">[Windows storage-account pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="ee415-187">[Linux depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="ee415-187">[Linux storage-account pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-intellij-managing-storage-accounts-using-azure-explorer/DC02.png
