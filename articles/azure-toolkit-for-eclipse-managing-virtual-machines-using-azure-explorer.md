---
title: "kullanılarak aaaManage sanal makine hello Eclipse için Azure Explorer | Microsoft Docs"
description: "Nasıl toomanage kullanarak Azure, sanal makineleriniz için Azure Explorer hello öğrenin Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="e9177-103">Eclipse için hello Azure Gezgini kullanarak sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="e9177-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="e9177-104">Hello hello Eclipse için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından sanal makineleri yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar hello Eclipse tümleşik geliştirme ortamı (IDE) içinde.</span><span class="sxs-lookup"><span data-stu-id="e9177-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e9177-105">Eclipse'te bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="e9177-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="e9177-106">toocreate hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e9177-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="e9177-107">Tooyour Azure hesabı hello kullanarak oturum [oturum açma yönergeleri hello Eclipse için Azure Araç Seti için].</span><span class="sxs-lookup"><span data-stu-id="e9177-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="e9177-108">Merhaba, **Azure Gezgini** görüntülemek için hello genişletin **Azure** düğümü, sağ **sanal makineler**ve ardından **VM Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="e9177-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="e9177-109">![Merhaba VM Oluştur komutu][CR01]</span><span class="sxs-lookup"><span data-stu-id="e9177-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="e9177-110">Merhaba **yeni sanal makine oluşturma** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="e9177-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="e9177-111">Merhaba, **bir abonelik seçin** penceresinde, aboneliğinizi seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e9177-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Merhaba Seç bir abonelik penceresi][CR02]

4. <span data-ttu-id="e9177-113">Merhaba, **bir sanal makine görüntüsü seçin** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="e9177-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="e9177-114">**Konum**: sanal makineniz oluşturulacağı belirtir (örneğin, *Batı ABD*).</span><span class="sxs-lookup"><span data-stu-id="e9177-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="e9177-115">**Yayımcı**: sanal makineniz toocreate kullanmanız hello görüntüyü oluşturan hello yayımcı belirtir (örneğin, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="e9177-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="e9177-116">**Teklif**: hello sanal makine toouse hello seçili yayımcıdan sunumu belirtir (örneğin, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="e9177-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="e9177-117">**SKU**: hello stok tutma birimini (SKU) toouse hello Seçili teklifi gelen belirtir (örneğin, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="e9177-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="e9177-118">**Sürüm #**: Seçili hello hangi sürümünü belirtir SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="e9177-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Merhaba, bir sanal makine görüntüsü penceresi seçin][CR03]

5. <span data-ttu-id="e9177-120">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9177-120">Click **Next**.</span></span>

6. <span data-ttu-id="e9177-121">Merhaba, **sanal makine temel ayarları** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="e9177-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="e9177-122">**Sanal makine adı**: Merhaba, yeni sanal makine için ad, bir harf ile başlamalı ve yalnızca harf, rakam ve tire içerebilir, belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="e9177-123">**Boyutu**: çekirdek ve bellek tooallocate sanal makineniz için hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="e9177-124">**Kullanıcı adı**: sanal makineniz yönetmek için hello yönetici hesabı toocreate belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="e9177-125">**Parola** ve **Onayla**: Merhaba, yönetici hesabının parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![Merhaba sanal makine temel Ayarları penceresi][CR04]

7. <span data-ttu-id="e9177-127">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9177-127">Click **Next**.</span></span>

8. <span data-ttu-id="e9177-128">Merhaba, **yeni depolama hesabı oluştur** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="e9177-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="e9177-129">**Kaynak grubu**: hello kaynak grubu, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="e9177-130">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="e9177-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="e9177-131">**Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="e9177-132">**Var olanı kullan**: tooselect Azure hesabınızla ilişkili olan bir kaynak grubunu istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![Merhaba yeni depolama hesabı oluştur iletişim kutusu][CR05]

   * <span data-ttu-id="e9177-134">**Depolama hesabı**: sanal makineniz depolamak için depolama hesabı toouse hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="e9177-135">Mevcut bir depolama hesabını kullanabilir veya yeni bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9177-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="e9177-136">**Sanal ağ** ve **alt**: hello sanal ağ ve sanal makinenin bağlanacağı alt belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="e9177-137">Bir mevcut ağ ve alt ağ kullanabilir veya yeni bir ağ ve alt ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9177-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="e9177-138">Seçerseniz **Yeni Oluştur**, iletişim kutusu aşağıdaki hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="e9177-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![Merhaba yeni sanal ağ oluştur iletişim kutusu][CR06]

9. <span data-ttu-id="e9177-140">Merhaba, **ilişkili kaynakları** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="e9177-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="e9177-141">**Genel IP adresi**: sanal makineniz için dışa dönük IP adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="e9177-142">Yeni bir IP adresi toocreate seçebilir veya sanal makinenize genel bir IP adresi değil olacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="e9177-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="e9177-143">**Ağ güvenlik grubu**: isteğe bağlı ağ güvenlik duvarı, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="e9177-144">Var olan bir Güvenlik Duvarı'nı seçin veya sanal makinenize bir ağ Güvenlik Duvarı'nı kullanmayacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="e9177-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="e9177-145">**Kullanılabilirlik kümesi**: isteğe bağlı bir kullanılabilirlik kümesi, sanal makinenize ait olabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="e9177-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="e9177-146">Mevcut bir kullanılabilirlik kümesi seçin veya yeni bir kullanılabilirlik kümesi oluşturun veya sanal makineniz tooan kullanılabilirlik kümesine ait değil, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="e9177-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![Merhaba ilişkili kaynakları penceresi][CR07]

9. <span data-ttu-id="e9177-148">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e9177-148">Click **Finish**.</span></span>  
  <span data-ttu-id="e9177-149">Yeni bir sanal makine hello Azure Gezgini aracı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e9177-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Yeni sanal makine][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e9177-151">Eclipse'te bir sanal makineyi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="e9177-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="e9177-152">Eclipse'te, hello Azure Gezgini kullanarak bir sanal makine toorestart hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e9177-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="e9177-153">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="e9177-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Merhaba sanal makine yeniden başlatma komutu][RE01]

2. <span data-ttu-id="e9177-155">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e9177-155">In hello confirmation window, click **Yes**.</span></span>

   ![Merhaba yeniden onay penceresi][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e9177-157">Eclipse'te bir sanal makineyi kapatın</span><span class="sxs-lookup"><span data-stu-id="e9177-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="e9177-158">Eclipse'te, hello Azure Gezgini kullanarak çalışan bir sanal makineyi aşağı tooshut hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e9177-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="e9177-159">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="e9177-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Merhaba sanal makine kapatma komutu][SH01]

2. <span data-ttu-id="e9177-161">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e9177-161">In hello confirmation window, click **Yes**.</span></span>

   ![Merhaba sanal makinenin kapatılması onay penceresi][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="e9177-163">Eclipse'te sanal makineyi silme</span><span class="sxs-lookup"><span data-stu-id="e9177-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="e9177-164">Eclipse'te, hello Azure Gezgini kullanarak bir sanal makine toodelete hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="e9177-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="e9177-165">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e9177-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![Merhaba sanal makinesi Delete komutu][DE01]

2. <span data-ttu-id="e9177-167">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="e9177-167">In hello confirmation window, click **Yes**.</span></span>

   ![Merhaba sanal makine silme işlemi onay penceresi][DE02]

## <a name="next-steps"></a><span data-ttu-id="e9177-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e9177-169">Next steps</span></span>
<span data-ttu-id="e9177-170">Azure sanal makine boyutları ve fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e9177-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="e9177-171">Azure sanal makine boyutları</span><span class="sxs-lookup"><span data-stu-id="e9177-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="e9177-172">[Azure'da Windows sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="e9177-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="e9177-173">[Azure'daki Linux sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="e9177-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="e9177-174">Azure sanal makinesi fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="e9177-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="e9177-175">[Windows sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="e9177-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="e9177-176">[Linux sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="e9177-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="e9177-177">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="e9177-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="e9177-178">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="e9177-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9177-179">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="e9177-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9177-180">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="e9177-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9177-181">[oturum açma yönergeleri hello Eclipse için Azure Araç Seti için]</span><span class="sxs-lookup"><span data-stu-id="e9177-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9177-182">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="e9177-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="e9177-183">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="e9177-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9177-184">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="e9177-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9177-185">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="e9177-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9177-186">[Oturum açma hello Azure Araç Seti için Intellij için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="e9177-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9177-187">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="e9177-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="e9177-188">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="e9177-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

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

[Azure'da Windows sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure'daki Linux sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows sanal makine fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux sanal makine fiyatlandırma]: /pricing/details/virtual-machines/linux/

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
