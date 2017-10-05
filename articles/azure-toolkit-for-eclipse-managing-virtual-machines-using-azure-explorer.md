---
title: "Eclipse için Azure Gezgini'ni kullanarak sanal makineleri yönetme | Microsoft Docs"
description: "Eclipse için Azure Gezgini'ni kullanarak Azure sanal makinelerinizi yönetmeyi öğrenin."
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
ms.openlocfilehash: 9784e8af9c530078afee06f08a23403a44b0762f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-by-using-the-azure-explorer-for-eclipse"></a><span data-ttu-id="ca57e-103">Eclipse için Azure Gezgini'ni kullanarak sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="ca57e-103">Manage virtual machines by using the Azure Explorer for Eclipse</span></span>

<span data-ttu-id="ca57e-104">Eclipse için Azure araç seti bir parçası olan Azure Gezgini, bunların Azure hesabında Eclipse tümleşik geliştirme ortamı (IDE) içindeki sanal makineleri yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca57e-104">The Azure Explorer, which is part of the Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside the Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="ca57e-105">Eclipse'te bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="ca57e-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="ca57e-106">Azure Gezgini'ni kullanarak bir sanal makine oluşturmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-106">To create a virtual machine by using the Azure Explorer, do the following:</span></span>

1. <span data-ttu-id="ca57e-107">Azure hesabınızı kullanarak oturum [oturum açma yönergeleri Eclipse için Azure Araç Seti için].</span><span class="sxs-lookup"><span data-stu-id="ca57e-107">Sign in to your Azure account by using the [Sign-in instructions for the Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="ca57e-108">İçinde **Azure Gezgini** görüntülemek için Genişlet **Azure** düğümünü sağ tıklatın **sanal makineler**ve ardından **VM Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-108">In the **Azure Explorer** view, expand the **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="ca57e-109">![VM Oluştur komutu][CR01]</span><span class="sxs-lookup"><span data-stu-id="ca57e-109">![The Create VM command][CR01]</span></span>  
   <span data-ttu-id="ca57e-110">**Yeni sanal makine oluşturma** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="ca57e-110">The **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="ca57e-111">İçinde **bir abonelik seçin** penceresinde, aboneliğinizi seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-111">In the **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Bir abonelik penceresi seçin][CR02]

4. <span data-ttu-id="ca57e-113">İçinde **bir sanal makine görüntüsü seçin** penceresinde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca57e-113">In the **Select a Virtual Machine Image** window, enter the following information:</span></span>

   * <span data-ttu-id="ca57e-114">**Konum**: sanal makineniz oluşturulacağı belirtir (örneğin, *Batı ABD*).</span><span class="sxs-lookup"><span data-stu-id="ca57e-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="ca57e-115">**Yayımcı**: kullanmak, sanal makine oluşturmak için görüntüyü oluşturan yayımcı belirtir (örneğin, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="ca57e-115">**Publisher**: Specifies the publisher that created the image you'll use to create your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="ca57e-116">**Teklif**: Seçili yayımcıdan kullanmak için sunumu sanal makine belirtir (örneğin, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="ca57e-116">**Offer**: Specifies the virtual machine offering to use from the selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="ca57e-117">**SKU**: stok tutma birimini (SKU) gelen Seçili teklifi kullanılacak belirtir (örneğin, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="ca57e-117">**Sku**: Specifies the stockkeeping unit (SKU) to use from the selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="ca57e-118">**Sürüm #**: hangi sürümünün kullanılacağını seçilen SKU belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-118">**Version #**: Specifies which version of the selected SKU to use.</span></span>

    ![Bir sanal makine görüntüsü penceresi seçin][CR03]

5. <span data-ttu-id="ca57e-120">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca57e-120">Click **Next**.</span></span>

6. <span data-ttu-id="ca57e-121">İçinde **sanal makine temel ayarları** penceresinde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca57e-121">In the **Virtual Machine Basic Settings** window, enter the following information:</span></span>

   * <span data-ttu-id="ca57e-122">**Sanal makine adı**: yeni sanal bir harfle başlamalı ve yalnızca harf, rakam ve tire içeren makinenizi adını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-122">**Virtual Machine Name**: Specifies the name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="ca57e-123">**Boyutu**: çekirdek ve sanal makine için ayrılacak bellek sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-123">**Size**: Specifies the number of cores and memory to allocate for your virtual machine.</span></span>

   * <span data-ttu-id="ca57e-124">**Kullanıcı adı**: sanal makineniz yönetmek için oluşturmak için yönetici hesaplarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-124">**User name**: Specifies the administrator account to create for managing your virtual machine.</span></span>

   * <span data-ttu-id="ca57e-125">**Parola** ve **Onayla**: yönetici hesabının parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-125">**Password** and **Confirm**: Specifies the password for your administrator account.</span></span>

    ![Sanal makine temel Ayarları penceresi][CR04]

7. <span data-ttu-id="ca57e-127">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca57e-127">Click **Next**.</span></span>

8. <span data-ttu-id="ca57e-128">İçinde **yeni depolama hesabı oluştur** penceresinde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca57e-128">In the **Create New Storage Account** window, enter the following information:</span></span>

   * <span data-ttu-id="ca57e-129">**Kaynak grubu**: kaynak grubu, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-129">**Resource Group**: Specifies the resource group for your virtual machine.</span></span> <span data-ttu-id="ca57e-130">Aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="ca57e-130">Select one of the following options:</span></span>
      * <span data-ttu-id="ca57e-131">**Yeni Oluştur**: yeni bir kaynak grubu oluşturmak istediğiniz belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-131">**Create new**: Specifies that you want to create a new resource group.</span></span>
      * <span data-ttu-id="ca57e-132">**Var olanı kullan**: Azure hesabınızla ilişkili olan bir kaynak grubunu seçmek istediğiniz belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-132">**Use existing**: Specifies that you want to select a resource group that is already associated with your Azure account.</span></span>

      ![Yeni depolama hesabı oluştur iletişim kutusu][CR05]

   * <span data-ttu-id="ca57e-134">**Depolama hesabı**: sanal makineniz depolamak için kullanılacak depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-134">**Storage account**: Specifies the storage account to use for storing your virtual machine.</span></span> <span data-ttu-id="ca57e-135">Mevcut bir depolama hesabını kullanabilir veya yeni bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca57e-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="ca57e-136">**Sanal ağ** ve **alt**: sanal ağ ve sanal makinenin bağlanacağı alt belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-136">**Virtual Network** and **Subnet**: Specifies the virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="ca57e-137">Bir mevcut ağ ve alt ağ kullanabilir veya yeni bir ağ ve alt ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca57e-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="ca57e-138">Seçerseniz **Yeni Oluştur**, aşağıdaki iletişim kutusu görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="ca57e-138">If you select **Create new**, the following dialog box is displayed:</span></span>

      ![Yeni sanal ağ oluştur iletişim kutusu][CR06]

9. <span data-ttu-id="ca57e-140">İçinde **ilişkili kaynakları** penceresinde, aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca57e-140">In the **Associated Resources** window, enter the following information:</span></span>

   * <span data-ttu-id="ca57e-141">**Genel IP adresi**: sanal makineniz için dışa dönük IP adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="ca57e-142">Yeni bir IP adresi oluşturmak seçebilir veya sanal makinenize genel bir IP adresi değil olacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-142">You can choose to create a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="ca57e-143">**Ağ güvenlik grubu**: isteğe bağlı ağ güvenlik duvarı, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="ca57e-144">Var olan bir Güvenlik Duvarı'nı seçin veya sanal makinenize bir ağ Güvenlik Duvarı'nı kullanmayacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="ca57e-145">**Kullanılabilirlik kümesi**: isteğe bağlı bir kullanılabilirlik kümesi, sanal makinenize ait olabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="ca57e-146">Mevcut bir kullanılabilirlik kümesi seçin veya yeni bir kullanılabilirlik kümesi oluşturmak veya sanal makinenize bir kullanılabilirlik kümesine ait değil, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong to an availability set, you can select **(None)**.</span></span>

   ![İlişkilendirilmiş kaynakları penceresi][CR07]

9. <span data-ttu-id="ca57e-148">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca57e-148">Click **Finish**.</span></span>  
  <span data-ttu-id="ca57e-149">Yeni sanal makinenizi Azure Gezgini aracı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ca57e-149">Your new virtual machine is displayed in the Azure Explorer tool window.</span></span>

   ![Yeni sanal makine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="ca57e-151">Eclipse'te bir sanal makineyi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="ca57e-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="ca57e-152">Eclipse'te Azure Gezgini'ni kullanarak bir sanal makineyi yeniden başlatmak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-152">To restart a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="ca57e-153">İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-153">In the **Azure Explorer** view, right-click the virtual machine, and then select **Restart**.</span></span>

   ![Sanal makine yeniden başlatma komutu][RE01]

2. <span data-ttu-id="ca57e-155">Onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-155">In the confirmation window, click **Yes**.</span></span>

   ![Yeniden başlatma onay penceresi][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="ca57e-157">Eclipse'te bir sanal makineyi kapatın</span><span class="sxs-lookup"><span data-stu-id="ca57e-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="ca57e-158">Eclipse'te Azure Gezgini'ni kullanarak çalışan bir sanal makineyi kapatıp için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-158">To shut down a running virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="ca57e-159">İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-159">In the **Azure Explorer** view, right-click the virtual machine, and then select **Shutdown**.</span></span>

   ![Sanal makine kapatma komutu][SH01]

2. <span data-ttu-id="ca57e-161">Onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-161">In the confirmation window, click **Yes**.</span></span>

   ![Sanal makinenin kapatılması onay penceresi][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="ca57e-163">Eclipse'te sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="ca57e-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="ca57e-164">Eclipse'te Azure Gezgini'ni kullanarak bir sanal makineyi silmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-164">To delete a virtual machine by using the Azure Explorer in Eclipse, do the following:</span></span>

1. <span data-ttu-id="ca57e-165">İçinde **Azure Gezgini** görüntülemek, sanal makineye sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-165">In the **Azure Explorer** view, right-click the virtual machine, and then select **Delete**.</span></span>

   ![Sanal makine Delete komutu][DE01]

2. <span data-ttu-id="ca57e-167">Onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="ca57e-167">In the confirmation window, click **Yes**.</span></span>

   ![Sanal makine silme işlemi onay penceresi][DE02]

## <a name="next-steps"></a><span data-ttu-id="ca57e-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca57e-169">Next steps</span></span>
<span data-ttu-id="ca57e-170">Azure sanal makine boyutları ve fiyatlandırma hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-170">For more information about Azure virtual-machine sizes and pricing, see the following resources:</span></span>

* <span data-ttu-id="ca57e-171">Azure sanal makine boyutları</span><span class="sxs-lookup"><span data-stu-id="ca57e-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="ca57e-172">[Azure'da Windows sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="ca57e-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="ca57e-173">[Azure'daki Linux sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="ca57e-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="ca57e-174">Azure sanal makinesi fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="ca57e-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="ca57e-175">[Windows sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="ca57e-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="ca57e-176">[Linux sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="ca57e-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="ca57e-177">Java IDE Azure araç takımları hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="ca57e-177">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="ca57e-178">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="ca57e-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ca57e-179">[Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="ca57e-179">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ca57e-180">[Eclipse için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="ca57e-180">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ca57e-181">[oturum açma yönergeleri Eclipse için Azure Araç Seti için]</span><span class="sxs-lookup"><span data-stu-id="ca57e-181">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ca57e-182">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="ca57e-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="ca57e-183">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="ca57e-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ca57e-184">[Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="ca57e-184">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ca57e-185">[IntelliJ için Azure Araç Setini Yükleme]</span><span class="sxs-lookup"><span data-stu-id="ca57e-185">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ca57e-186">[Oturum açma Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="ca57e-186">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ca57e-187">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="ca57e-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="ca57e-188">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="ca57e-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="ca57e-189">[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-189">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="ca57e-190">[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-190">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="ca57e-191">[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-191">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ca57e-192">[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-192">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="ca57e-193">[Eclipse için Azure Araç Setini Yükleme]: ./azure-toolkit-for-eclipse-installation.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-193">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="ca57e-194">[IntelliJ için Azure Araç Setini Yükleme]: ./azure-toolkit-for-intellij-installation.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-194">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="ca57e-195">[oturum açma yönergeleri Eclipse için Azure Araç Seti için]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-195">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="ca57e-196">[Oturum açma Azure Araç Seti için Intellij için yönergeler]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-196">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="ca57e-197">[Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-197">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="ca57e-198">[Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="ca57e-198">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="ca57e-199">[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="ca57e-199">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="ca57e-200">[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="ca57e-200">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="ca57e-201">[Azure'da Windows sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes</span><span class="sxs-lookup"><span data-stu-id="ca57e-201">[Sizes for Windows virtual machines in Azure]: /azure/virtual-machines/virtual-machines-windows-sizes</span></span>
<span data-ttu-id="ca57e-202">[Azure'daki Linux sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-linux-sizes</span><span class="sxs-lookup"><span data-stu-id="ca57e-202">[Sizes for Linux virtual machines in Azure]: /azure/virtual-machines/virtual-machines-linux-sizes</span></span>
<span data-ttu-id="ca57e-203">[Windows sanal makine fiyatlandırma]: /pricing/details/virtual-machines/windows/</span><span class="sxs-lookup"><span data-stu-id="ca57e-203">[Windows virtual-machine pricing]: /pricing/details/virtual-machines/windows/</span></span>
<span data-ttu-id="ca57e-204">[Linux sanal makine fiyatlandırma]: /pricing/details/virtual-machines/linux/</span><span class="sxs-lookup"><span data-stu-id="ca57e-204">[Linux virtual-machine pricing]: /pricing/details/virtual-machines/linux/</span></span>

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
