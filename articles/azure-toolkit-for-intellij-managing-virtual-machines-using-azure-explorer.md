---
title: "kullanılarak aaaManage sanal makine için Intellij Azure Gezgini hello | Microsoft Docs"
description: "Nasıl toomanage kullanarak Azure, sanal makineleriniz için Azure Explorer hello öğrenin Intellij."
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
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="cbd24-103">Intellij için hello Azure Gezgini kullanarak sanal makineleri yönetme</span><span class="sxs-lookup"><span data-stu-id="cbd24-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="cbd24-104">Hello hello Intellij için Azure araç seti bir parçası olan Azure Gezgini, kullanıcıların Azure hesabından sanal makineleri yönetmek için kullanımı kolay çözümünü Java geliştiricilere sağlar hello Intellij tümleşik geliştirme ortamı (IDE) içinde.</span><span class="sxs-lookup"><span data-stu-id="cbd24-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="cbd24-105">Intellij içinde bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="cbd24-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="cbd24-106">toocreate hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbd24-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="cbd24-107">Hello hello adımları kullanarak tooyour Azure hesabı oturum [oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij] makalesi.</span><span class="sxs-lookup"><span data-stu-id="cbd24-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="cbd24-108">Merhaba, **Azure Gezgini** görüntülemek için hello genişletin **Azure** düğümü, sağ **sanal makineler**ve ardından **VM Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="cbd24-109">![Merhaba VM Oluştur komutu][CR01]</span><span class="sxs-lookup"><span data-stu-id="cbd24-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="cbd24-110">Merhaba **yeni sanal makine oluşturma** Sihirbazı açılır.</span><span class="sxs-lookup"><span data-stu-id="cbd24-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="cbd24-111">Merhaba, **bir abonelik seçin** penceresinde, aboneliğinizi seçin ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Merhaba Seç bir abonelik penceresi][CR02]

4. <span data-ttu-id="cbd24-113">Merhaba, **bir sanal makine görüntüsü seçin** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="cbd24-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="cbd24-114">**Konum**: sanal makineniz oluşturulacağı belirtir (örneğin, *Batı ABD*).</span><span class="sxs-lookup"><span data-stu-id="cbd24-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="cbd24-115">**Görüntü önerilen**: kısaltılmış bir sık kullanılan görüntüleri listesinden görüntü seçeceğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="cbd24-116">**Özel görüntü**: özel bir görüntü bilgisinden hello sağlayarak seçecektir belirtir:</span><span class="sxs-lookup"><span data-stu-id="cbd24-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="cbd24-117">**Yayımcı**: sanal makine için kullanacağınız hello görüntüyü oluşturan hello yayımcı belirtir (örneğin, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="cbd24-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="cbd24-118">**Teklif**: hello sanal makine toouse hello seçili yayımcıdan sunumu belirtir (örneğin, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="cbd24-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="cbd24-119">**SKU**: hello stok tutma birimini (SKU) toouse hello Seçili teklifi gelen belirtir (örneğin, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="cbd24-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="cbd24-120">**Sürüm #**: Seçili hello hangi sürümünü belirtir SKU toouse.</span><span class="sxs-lookup"><span data-stu-id="cbd24-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Merhaba, bir sanal makine görüntüsü penceresi seçin][CR03]

5. <span data-ttu-id="cbd24-122">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cbd24-122">Click **Next**.</span></span> 

6. <span data-ttu-id="cbd24-123">Merhaba, **sanal makine temel ayarları** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="cbd24-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="cbd24-124">**Sanal makine adı**: Merhaba, yeni sanal makine için ad, bir harf ile başlamalı ve yalnızca harf, rakam ve tire içerebilir, belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="cbd24-125">**Boyutu**: çekirdek ve bellek tooallocate sanal makineniz için hello sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="cbd24-126">**Kullanıcı adı**: sanal makineniz yönetmek için hello yönetici hesabı toocreate belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="cbd24-127">**Parola** ve **Onayla**: Merhaba, yönetici hesabının parolasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![Merhaba sanal makine temel Ayarları penceresi][CR04]

7. <span data-ttu-id="cbd24-129">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cbd24-129">Click **Next**.</span></span> 

8. <span data-ttu-id="cbd24-130">Merhaba, **ilişkili kaynakları** penceresinde, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="cbd24-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="cbd24-131">**Kaynak grubu**: hello kaynak grubu, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="cbd24-132">Seçenekler aşağıdaki hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="cbd24-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="cbd24-133">**Yeni Oluştur**: toocreate yeni bir kaynak grubu istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="cbd24-134">**Var olanı kullan**: Azure hesabınızla ilişkili kaynak grupları listesinden tooselect istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![Merhaba ilişkili kaynakları penceresi][CR07]

   * <span data-ttu-id="cbd24-136">**Depolama hesabı**: sanal makineniz depolamak için depolama hesabı toouse hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="cbd24-137">Mevcut bir depolama hesabını seçin veya yeni bir hesap oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cbd24-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="cbd24-138">Seçerseniz **Yeni Oluştur**, iletişim kutusu aşağıdaki hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="cbd24-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![Merhaba depolama hesabı oluştur iletişim kutusu][CR05]

   * <span data-ttu-id="cbd24-140">**Sanal ağ** ve **alt**: hello sanal ağ ve sanal makinenin bağlanacağı alt belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="cbd24-141">Bir mevcut ağ ve alt ağ kullanabilir veya yeni bir ağ ve alt ağ oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbd24-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="cbd24-142">Seçerseniz **Yeni Oluştur**, iletişim kutusu aşağıdaki hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="cbd24-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![Merhaba sanal ağ oluştur iletişim kutusu][CR06]

   * <span data-ttu-id="cbd24-144">**Genel IP adresi**: sanal makineniz için dışa dönük IP adresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="cbd24-145">Yeni bir IP adresi toocreate seçebilir veya sanal makinenize genel bir IP adresi değil olacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="cbd24-146">**Ağ güvenlik grubu**: isteğe bağlı ağ güvenlik duvarı, sanal makine için belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="cbd24-147">Var olan bir Güvenlik Duvarı'nı seçin veya sanal makinenize bir ağ Güvenlik Duvarı'nı kullanmayacaksa, seçebileceğiniz **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="cbd24-148">**Kullanılabilirlik kümesi**: isteğe bağlı bir kullanılabilirlik kümesi, sanal makinenize ait olabilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="cbd24-149">Mevcut bir kullanılabilirlik kümesi seçin, yeni bir kullanılabilirlik kümesi oluşturabilir veya, sanal makinenize tooan kullanılabilirlik kümesine ait değil, seçin **(hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="cbd24-150">**Son**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cbd24-150">Click **Finish**.</span></span>  
    <span data-ttu-id="cbd24-151">Yeni bir sanal makine hello Azure Gezgini aracı penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="cbd24-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Yeni sanal makine hello Azure Gezgin Görünümü][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="cbd24-153">Intellij içinde bir sanal makineyi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="cbd24-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="cbd24-154">toorestart Intellij içinde hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbd24-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="cbd24-155">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![Merhaba sanal makine yeniden başlatma komutu][RE01]

2. <span data-ttu-id="cbd24-157">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Merhaba yeniden sanal makine onay penceresi][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="cbd24-159">Intellij içinde bir sanal makineyi kapatın</span><span class="sxs-lookup"><span data-stu-id="cbd24-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="cbd24-160">Intellij içinde hello Azure Gezgini kullanarak çalışan bir sanal makineyi aşağı tooshut hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbd24-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="cbd24-161">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![Merhaba sanal makine kapatma komutu][SH01]

2. <span data-ttu-id="cbd24-163">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-163">In hello confirmation window, click **Yes**.</span></span> 

   ![sanal makine onay penceresi Hello Kapat][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="cbd24-165">Bir sanal makinede Intellij Sil</span><span class="sxs-lookup"><span data-stu-id="cbd24-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="cbd24-166">toodelete Intellij içinde hello Azure Gezgini kullanarak bir sanal makine hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="cbd24-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="cbd24-167">Merhaba, **Azure Gezgini** görüntülemek, hello sanal makineye sağ tıklayın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![Merhaba sanal makinesi Delete komutu][DE01]

2. <span data-ttu-id="cbd24-169">Merhaba onay penceresinde **Evet**.</span><span class="sxs-lookup"><span data-stu-id="cbd24-169">In hello confirmation window, click **Yes**.</span></span> 

   ![sanal makine onay penceresi Hello Sil][DE02]

## <a name="next-steps"></a><span data-ttu-id="cbd24-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cbd24-171">Next steps</span></span>
<span data-ttu-id="cbd24-172">Azure sanal makine boyutları ve fiyatlandırma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cbd24-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="cbd24-173">Azure sanal makine boyutları</span><span class="sxs-lookup"><span data-stu-id="cbd24-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="cbd24-174">[Azure'da Windows sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="cbd24-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="cbd24-175">[Azure'daki Linux sanal makineler için Boyutlar]</span><span class="sxs-lookup"><span data-stu-id="cbd24-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="cbd24-176">Azure sanal makinesi fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="cbd24-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="cbd24-177">[Windows sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="cbd24-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="cbd24-178">[Linux sanal makine fiyatlandırma]</span><span class="sxs-lookup"><span data-stu-id="cbd24-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="cbd24-179">Java IDE hello Azure araç takımları hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cbd24-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="cbd24-180">[Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="cbd24-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbd24-181">[Merhaba Eclipse için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="cbd24-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbd24-182">[Yükleme hello Eclipse için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="cbd24-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbd24-183">[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]</span><span class="sxs-lookup"><span data-stu-id="cbd24-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="cbd24-184">[Eclipse'te Azure Hello World web uygulaması oluşturma]</span><span class="sxs-lookup"><span data-stu-id="cbd24-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="cbd24-185">[IntelliJ için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="cbd24-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbd24-186">[Merhaba Intellij için Azure Araç Seti yenilikleri]</span><span class="sxs-lookup"><span data-stu-id="cbd24-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbd24-187">[Yükleme hello Intellij için Azure Araç Seti]</span><span class="sxs-lookup"><span data-stu-id="cbd24-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbd24-188">[oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij]</span><span class="sxs-lookup"><span data-stu-id="cbd24-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="cbd24-189">[Intellij Azure'da Hello World web uygulaması oluşturun]</span><span class="sxs-lookup"><span data-stu-id="cbd24-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="cbd24-190">Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi] ve [Visual Studio Team Services için Java Araçları].</span><span class="sxs-lookup"><span data-stu-id="cbd24-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse.md
[IntelliJ için Azure Araç Seti]: ./azure-toolkit-for-intellij.md
[Eclipse'te Azure Hello World web uygulaması oluşturma]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Intellij Azure'da Hello World web uygulaması oluşturun]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Yükleme hello Eclipse için Azure Araç Seti]: ./azure-toolkit-for-eclipse-installation.md
[Yükleme hello Intellij için Azure Araç Seti]: ./azure-toolkit-for-intellij-installation.md
[Oturum açma hello Eclipse için Azure Araç Seti için yönergeler]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[oturum açma ilişkin yönergeler için hello Azure Araç Seti Intellij]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Merhaba Eclipse için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-eclipse-whats-new.md
[Merhaba Intellij için Azure Araç Seti yenilikleri]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Geliştirici Merkezi]: https://azure.microsoft.com/develop/java/
[Visual Studio Team Services için Java Araçları]: https://java.visualstudio.com/

[Azure'da Windows sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-windows-sizes
[Azure'daki Linux sanal makineler için Boyutlar]: /azure/virtual-machines/virtual-machines-linux-sizes
[Windows sanal makine fiyatlandırma]: /pricing/details/virtual-machines/windows/
[Linux sanal makine fiyatlandırma]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
