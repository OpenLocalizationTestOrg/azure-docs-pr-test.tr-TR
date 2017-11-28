---
title: "Eclipse için Azure Explorer kullanarak aaaManage depolama hesapları hello | Microsoft Docs"
description: "Nasıl toomanage Eclipse için hello Azure Explorer kullanarak, Azure depolama hesapları hakkında bilgi edinin."
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
ms.openlocfilehash: b7ec53e77e3c96d87754b9a658d31e6182121b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="9e67c-103">Eclipse için hello Azure Gezgini kullanarak depolama hesaplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9e67c-103">Manage storage accounts by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="9e67c-104">Merhaba hello Eclipse için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından depolama hesaplarını yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar hello Eclipse tümleşik geliştirme ortamı (IDE) içinde.</span><span class="sxs-lookup"><span data-stu-id="9e67c-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing storage accounts in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-storage-account-in-eclipse"></a><span data-ttu-id="9e67c-105">Eclipse'te depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e67c-105">Create a storage account in Eclipse</span></span>

<span data-ttu-id="9e67c-106">toocreate hello Azure Gezgini kullanarak bir depolama hesabı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9e67c-106">toocreate a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="9e67c-107">Tooyour Azure hesabı hello kullanarak oturum [oturum açma yönergeleri hello Eclipse için Azure Araç Seti için].</span><span class="sxs-lookup"><span data-stu-id="9e67c-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="9e67c-108">Hello içinde **Azure Gezgini** görüntülemek için hello genişletin **Azure** düğümünü sağ tıklatın **depolama hesapları**ve ardından **depolama hesabı oluştur**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Storage Accounts**, and then click **Create Storage Account**.</span></span>

   ![Depolama hesabı komut oluşturma][CS01]

3. <span data-ttu-id="9e67c-110">Merhaba, **depolama hesabı oluştur** iletişim kutusunda, aşağıdaki seçenekleri şu hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="9e67c-110">In hello **Create Storage Account** dialog box, specify hello following options:</span></span>

   ![Yeni depolama hesabı iletişim kutusu oluşturma][CS02]

   * <span data-ttu-id="9e67c-112">**Ad**: hello yeni depolama hesabı hello adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-112">**Name**: Specifies hello name for hello new storage account.</span></span>

   * <span data-ttu-id="9e67c-113">**Abonelik**: Merhaba toouse hello yeni depolama hesabı için istediğiniz Azure aboneliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-113">**Subscription**: Specifies hello Azure subscription that you want toouse for hello new storage account.</span></span>

   * <span data-ttu-id="9e67c-114">**Kaynak grubu**: hello kaynak grubu, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-114">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="9e67c-115">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="9e67c-115">Select one of hello following options:</span></span>
      * <span data-ttu-id="9e67c-116">**Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-116">**Create New**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="9e67c-117">**Varolan kullanmak**: Azure hesabınızla ilişkili kaynak gruplarının bir listeden seçer belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-117">**Use Existing**: Specifies that you will select from a list of resource groups that are associated with your Azure account.</span></span>

   * <span data-ttu-id="9e67c-118">**Bölge**: Burada, depolama hesabı oluşturulur (örneğin, "Batı ABD") hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-118">**Region**: Specifies hello location where your storage account will be created (for example, "West US").</span></span>

   * <span data-ttu-id="9e67c-119">**Tür hesap**: depolama hesabı toocreate (örneğin, "Blob Depolama") hello türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-119">**Account kind**: Specifies hello type of storage account toocreate (for example, "Blob storage").</span></span> <span data-ttu-id="9e67c-120">Daha fazla bilgi için bkz: [Azure storage hesapları hakkında].</span><span class="sxs-lookup"><span data-stu-id="9e67c-120">For more information, see [About Azure storage accounts].</span></span>

   * <span data-ttu-id="9e67c-121">**Performans**: (örneğin, "Premium") hello seçili yayımcıdan toouse sunumu hangi depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-121">**Performance**: Specifies which storage account offering toouse from hello selected publisher (for example, "Premium").</span></span> <span data-ttu-id="9e67c-122">Daha fazla bilgi için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri].</span><span class="sxs-lookup"><span data-stu-id="9e67c-122">For more information, see [Azure storage scalability and performance targets].</span></span>

   * <span data-ttu-id="9e67c-123">**Çoğaltma**: hello çoğaltma hello depolama hesabı (örneğin, "bölgesel olarak yedekli") için belirtir.</span><span class="sxs-lookup"><span data-stu-id="9e67c-123">**Replication**: Specifies hello replication for hello storage account (for example, "Zone-Redundant").</span></span> <span data-ttu-id="9e67c-124">Daha fazla bilgi için bkz: [Azure storage çoğaltma].</span><span class="sxs-lookup"><span data-stu-id="9e67c-124">For more information, see [Azure storage replication].</span></span>

4. <span data-ttu-id="9e67c-125">Tüm seçenekleri önceki hello belirledikten sonra tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-125">When you have specified all of hello preceding options, click **Create**.</span></span>

## <a name="create-a-storage-container-in-eclipse"></a><span data-ttu-id="9e67c-126">Eclipse'te bir depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e67c-126">Create a storage container in Eclipse</span></span>

<span data-ttu-id="9e67c-127">toocreate hello Azure Gezgini kullanarak bir depolama kapsayıcısı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9e67c-127">toocreate a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="9e67c-128">Merhaba, **Azure Gezgini** görüntülemek için burada, toocreate bir kapsayıcı istediğiniz ve ardından hello depolama hesabına sağ **oluşturma blob kapsayıcısı**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-128">In hello **Azure Explorer** view, right-click hello storage account where you want toocreate a container, and then click **Create blob container**.</span></span>

   ![BLOB kapsayıcı komut oluşturma][CC01]

2. <span data-ttu-id="9e67c-130">Merhaba, **oluşturma blob kapsayıcısı** iletişim kutusu, Merhaba, kapsayıcı için bir ad belirtin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-130">In hello **Create blob container** dialog box, specify hello name for your container, and then click **OK**.</span></span> <span data-ttu-id="9e67c-131">Depolama kapsayıcıları adlandırma hakkında daha fazla bilgi için bkz: [adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran].</span><span class="sxs-lookup"><span data-stu-id="9e67c-131">For more information about naming storage containers, see [Naming and referencing containers, blobs, and metadata].</span></span>

   ![BLOB kapsayıcısı iletişim kutusu oluşturma][CC02]

## <a name="delete-a-storage-container-in-eclipse"></a><span data-ttu-id="9e67c-133">Depolama kapsayıcısı eclipse'te Sil</span><span class="sxs-lookup"><span data-stu-id="9e67c-133">Delete a storage container in Eclipse</span></span>

<span data-ttu-id="9e67c-134">toodelete hello Azure Gezgini kullanarak bir depolama kapsayıcısı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9e67c-134">toodelete a storage container by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="9e67c-135">Merhaba, **Azure Gezgini** görüntülemek, hello depolama kapsayıcısına sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-135">In hello **Azure Explorer** view, right-click hello storage container, and then click **Delete**.</span></span>

   ![Depolama kapsayıcısı komutu silme][DC01]

2. <span data-ttu-id="9e67c-137">Merhaba onay penceresinde **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-137">In hello confirmation window, click **OK**.</span></span>

   ![Depolama kapsayıcısı onay penceresi Sil][DC02]

## <a name="delete-a-storage-account-in-eclipse"></a><span data-ttu-id="9e67c-139">Eclipse'te bir depolama hesabını silme</span><span class="sxs-lookup"><span data-stu-id="9e67c-139">Delete a storage account in Eclipse</span></span>

<span data-ttu-id="9e67c-140">toodelete hello Azure Gezgini kullanarak bir depolama hesabı hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="9e67c-140">toodelete a storage account by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="9e67c-141">Merhaba, **Azure Gezgini** görüntülemek, hello depolama hesabına sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-141">In hello **Azure Explorer** view, right-click hello storage account, and then click **Delete**.</span></span>

   ![Depolama hesabı komutu silme][DS01]

2. <span data-ttu-id="9e67c-143">Merhaba onay penceresinde **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-143">In hello confirmation window, click **OK**.</span></span>

   ![Depolama hesabı onay penceresi Sil][DS02]

## <a name="next-steps"></a><span data-ttu-id="9e67c-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e67c-145">Next steps</span></span>
<span data-ttu-id="9e67c-146">Azure depolama hesapları, boyutlar ve fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9e67c-146">For more information about Azure storage accounts, sizes, and pricing, see hello following resources:</span></span>

* <span data-ttu-id="9e67c-147">[Giriş tooMicrosoft Azure depolama]</span><span class="sxs-lookup"><span data-stu-id="9e67c-147">[Introduction tooMicrosoft Azure Storage]</span></span>
* <span data-ttu-id="9e67c-148">[Azure storage hesapları hakkında]</span><span class="sxs-lookup"><span data-stu-id="9e67c-148">[About Azure storage accounts]</span></span>
* <span data-ttu-id="9e67c-149">Azure depolama hesabı boyutları</span><span class="sxs-lookup"><span data-stu-id="9e67c-149">Azure storage-account sizes</span></span>
  * <span data-ttu-id="9e67c-150">[Windows Azure depolama hesapları için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="9e67c-150">[Sizes for Windows storage accounts in Azure]</span></span>
  * <span data-ttu-id="9e67c-151">[Linux depolama hesaplarını Azure boyutları]</span><span class="sxs-lookup"><span data-stu-id="9e67c-151">[Sizes for Linux storage accounts in Azure]</span></span>
* <span data-ttu-id="9e67c-152">Azure depolama hesabı fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="9e67c-152">Azure storage-account pricing</span></span>
  * <span data-ttu-id="9e67c-153">[Windows depolama hesabı fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="9e67c-153">[Windows storage-account pricing]</span></span>
  * <span data-ttu-id="9e67c-154">[Linux depolama hesabı fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="9e67c-154">[Linux storage-account pricing]</span></span>

<span data-ttu-id="9e67c-155">Java IDE için Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9e67c-155">For more information about Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="9e67c-156">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9e67c-156">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9e67c-157">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9e67c-157">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9e67c-158">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9e67c-158">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9e67c-159">[oturum açma yönergeleri hello Eclipse için Azure Araç Seti için]</span><span class="sxs-lookup"><span data-stu-id="9e67c-159">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="9e67c-160">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="9e67c-160">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="9e67c-161">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9e67c-161">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9e67c-162">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="9e67c-162">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9e67c-163">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="9e67c-163">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9e67c-164">[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="9e67c-164">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="9e67c-165">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="9e67c-165">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="9e67c-166">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="9e67c-166">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[oturum açma yönergeleri hello Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Giriş tooMicrosoft Azure depolama]: /azure/storage/storage-introduction
[Azure storage hesapları hakkında]: /azure/storage/storage-create-storage-account
[Azure storage çoğaltma]: /azure/storage/storage-redundancy
[Azure storage ölçeklenebilirlik ve performans hedefleri]: /azure/storage/storage-scalability-targets
[adlandırma ve kapsayıcıları, blobları ve meta verileri başvuran]: http://go.microsoft.com/fwlink/?LinkId=255555

[Windows Azure depolama hesapları için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Linux depolama hesaplarını Azure boyutları]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux depolama hesabı fiyatlandırma]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[CS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS01.png
[CS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CS02.png
[CC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC01.png
[CC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/CC02.png

[DS01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS01.png
[DS02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DS02.png
[DC01]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC01.png
[DC02]: ./media/azure-toolkit-for-eclipse-managing-storage-accounts-using-azure-explorer/DC02.png
