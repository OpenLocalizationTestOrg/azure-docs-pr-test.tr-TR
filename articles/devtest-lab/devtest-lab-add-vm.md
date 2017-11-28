---
title: Azure DevTest Labs laboratuvarda VM ekleme | Microsoft Docs
description: "Azure DevTest Labs laboratuvarda için bir sanal makineye eklemeyi öğrenin"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 449bffb040dafc8edd0b8b0afd80dbea35cd28ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="73c7b-103">Azure DevTest Labs laboratuvarda VM ekleme</span><span class="sxs-lookup"><span data-stu-id="73c7b-103">Add a VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="73c7b-104">Zaten varsa [ilk VM oluşturulan](devtest-lab-create-first-vm.md), büyük olasılıkla bunu bir önceden yüklenmiş yaptığınız [Market görüntüsü](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="73c7b-104">If you have already [created your first VM](devtest-lab-create-first-vm.md), you likely did so from a pre-loaded [marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="73c7b-105">Şimdi, laboratuvarınız için sonraki VM'ler eklemek isterseniz, ayrıca seçebileceğiniz bir *temel* ya da başka bir deyişle bir [özel görüntü](devtest-lab-create-template.md) veya [formülü](devtest-lab-manage-formulas.md).</span><span class="sxs-lookup"><span data-stu-id="73c7b-105">Now, if you want to add subsequent VMs to your lab, you can also choose a *base* that is either a [custom image](devtest-lab-create-template.md) or a [formula](devtest-lab-manage-formulas.md).</span></span> <span data-ttu-id="73c7b-106">Bu öğreticide, bir VM DevTest Labs laboratuvarda eklemek için Azure portalını kullanarak aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73c7b-106">This tutorial walks you through using the Azure portal to add a VM to a lab in DevTest Labs.</span></span>

<span data-ttu-id="73c7b-107">Bu makalede ayrıca laboratuvarınızda bir VM için yapıları yönetme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="73c7b-107">This article also shows you how to manage the artifacts for a VM in your lab.</span></span>

## <a name="steps-to-add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="73c7b-108">Azure DevTest Labs laboratuvarda VM eklemek için adımları</span><span class="sxs-lookup"><span data-stu-id="73c7b-108">Steps to add a VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="73c7b-109">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="73c7b-110">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="73c7b-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="73c7b-111">VM oluşturmak istediğiniz Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-111">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="73c7b-112">Laboratuvar 's üzerinde **genel bakış** dikey penceresinde, select **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-112">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![VM düğme ekleme](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="73c7b-114">Üzerinde **bir temel seçin** dikey penceresinde, VM için temel bir seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-114">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="73c7b-115">Üzerinde **sanal makine** dikey penceresinde, yeni sanal makine için bir ad girin **sanal makine adı** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="73c7b-115">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Laboratuvar VM dikey penceresi](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="73c7b-117">Girin bir **kullanıcı adı** sanal makinede yönetici ayrıcalıkları verilmiş.</span><span class="sxs-lookup"><span data-stu-id="73c7b-117">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="73c7b-118">Depolanmış bir parola kullanmak istiyorsanız, [gizli deposu](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)seçin **kaydedilmiş gizliliği kullanın**ve parolanızı (parola) karşılık gelen bir anahtar değeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-118">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="73c7b-119">Aksi halde, bir parola etiketli metin alanına girin **bir değer yazın**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-119">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="73c7b-120">**Sanal makine disk türü** hangi depolama disk türü laboratuvara sanal makineler için izin verilen belirler.</span><span class="sxs-lookup"><span data-stu-id="73c7b-120">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="73c7b-121">Seçin **sanal makine boyutu** ve işlemci çekirdeği, RAM boyutu ve sabit sürücü boyutu oluşturmak için VM belirtin önceden tanımlanmış öğelerden birini seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-121">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="73c7b-122">Seçin **yapıları** - yapıları - listesinden seçin ve temel görüntü eklemek istediğiniz yapıları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-122">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="73c7b-123">**Not:** DevTest Labs yeni veya yapıları yapılandırma başvurmak [bir VM'ye var artifact ekleyin](#add-an-existing-artifact-to-a-vm) bölümünde ve ardından bitirdikten sonra buraya dönün.</span><span class="sxs-lookup"><span data-stu-id="73c7b-123">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="73c7b-124">Seçin **Gelişmiş ayarları** VM ağ seçeneklerini ve sona erme seçeneklerini yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="73c7b-124">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> 

   <span data-ttu-id="73c7b-125">Bir süre sonu seçeneğini ayarlamak için üzerinde otomatik olarak VM silinir bir tarih belirtmek için takvim simgesini seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-125">To set an expiration option, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="73c7b-126">Varsayılan olarak, VM asla sona erecek.</span><span class="sxs-lookup"><span data-stu-id="73c7b-126">By default, the VM will never expire.</span></span> 
1. <span data-ttu-id="73c7b-127">Görüntülemek veya Azure Resource Manager şablonu kopyalamak istediğiniz oluştuysa, [Kaydet Azure Resource Manager şablonu](#save-azure-resource-manager-template) bölümünde ve bittiğinde buraya dönün.</span><span class="sxs-lookup"><span data-stu-id="73c7b-127">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="73c7b-128">Seçin **oluşturma** Laboratuvar için belirtilen VM eklemek için.</span><span class="sxs-lookup"><span data-stu-id="73c7b-128">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="73c7b-129">Laboratuvar dikey durumunu VM oluşturma: ilk olarak görüntüler **oluşturma**, ardından olarak **çalıştıran** VM başlatıldıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="73c7b-129">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="73c7b-130">[Claimable VM eklemek](devtest-lab-add-claimable-vm.md) , böylece laboratuvara herhangi bir kullanıcı tarafından kullanılabilir VM claimable nasıl yapılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="73c7b-130">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how to make the VM claimable so that it is available for use by any user in the lab.</span></span>
>
>

## <a name="add-an-existing-artifact-to-a-vm"></a><span data-ttu-id="73c7b-131">Bir VM'ye var artifact ekleyin</span><span class="sxs-lookup"><span data-stu-id="73c7b-131">Add an existing artifact to a VM</span></span>
<span data-ttu-id="73c7b-132">Bir VM oluştururken, varolan yapıları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73c7b-132">While creating a VM, you can add existing artifacts.</span></span> <span data-ttu-id="73c7b-133">Her Laboratuvar ortak DevTest Labs Yapıt deposu yanı sıra oluşturulan ve kendi Yapıt deposu eklenen yapıları yapılardan içerir.</span><span class="sxs-lookup"><span data-stu-id="73c7b-133">Each lab includes artifacts from the Public DevTest Labs Artifact Repository as well as artifacts that you've created and added to your own Artifact Repository.</span></span>

* <span data-ttu-id="73c7b-134">Azure DevTest Labs *yapıları* belirlemenize olanak *Eylemler* VM Windows PowerShell komut dosyası çalıştırarak, Bash komutlarını çalıştırarak ve yazılım yükleme gibi sağlandığında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="73c7b-134">Azure DevTest Labs *artifacts* let you specify *actions* that are performed when the VM is provisioned, such as running Windows PowerShell scripts, running Bash commands, and installing software.</span></span>
* <span data-ttu-id="73c7b-135">Yapı *parametreleri* belirli senaryonuz için yapıyı özelleştirmenize olanak tanır</span><span class="sxs-lookup"><span data-stu-id="73c7b-135">Artifact *parameters* let you customize the artifact for your particular scenario</span></span>

<span data-ttu-id="73c7b-136">Yapıları oluşturma, makaleye bakın bulmak için [DevTest Labs ile kullanılmak üzere kendi yapıları Yazar öğrenin](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="73c7b-136">To discover how to create artifacts, see the article, [Learn how to author your own artifacts for use with DevTest Labs](devtest-lab-artifact-author.md).</span></span>

1. <span data-ttu-id="73c7b-137">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-137">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="73c7b-138">Seçin **daha Hizmetleri**ve ardından **DevTest Labs** listeden.</span><span class="sxs-lookup"><span data-stu-id="73c7b-138">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="73c7b-139">Çalışmak istediğiniz VM içeren Laboratuvar labs listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-139">From the list of labs, select the lab containing the VM with which you want to work.</span></span>  
1. <span data-ttu-id="73c7b-140">Seçin **My sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-140">Select **My virtual machines**.</span></span>
1. <span data-ttu-id="73c7b-141">İstenen VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-141">Select the desired VM.</span></span>
1. <span data-ttu-id="73c7b-142">Seçin **yapıları**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-142">Select **Artifacts**.</span></span> 
1. <span data-ttu-id="73c7b-143">Seçin **yapıları uygulamak**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-143">Select **Apply artifacts**.</span></span>
1. <span data-ttu-id="73c7b-144">Üzerinde **yapıları uygulamak** dikey penceresinde VM eklemek istediğiniz yapıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-144">On the **Apply artifacts** blade, select the artifact you wish to add to the VM.</span></span>
1. <span data-ttu-id="73c7b-145">Üzerinde **ekleyin yapıt** dikey penceresinde gerekli parametre değerlerini ve gereken isteğe bağlı parametreleri girin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-145">On the **Add artifact** blade, enter the required parameter values and any optional parameters that you need.</span></span>  
1. <span data-ttu-id="73c7b-146">Seçin **Ekle** yapıyı ekleyin ve dönmek için **yapıları uygulamak** dikey.</span><span class="sxs-lookup"><span data-stu-id="73c7b-146">Select **Add** to add the artifact and return to the **Apply artifacts** blade.</span></span>
1. <span data-ttu-id="73c7b-147">Yapılar, VM için gerektiği şekilde ekleme devam edin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-147">Continue adding artifacts as needed for your VM.</span></span>
1. <span data-ttu-id="73c7b-148">Yapıtları ekledikten sonra [yapıları çalıştırılacağı sırasını değiştirmek](#change-the-order-in-which-artifacts-are-run).</span><span class="sxs-lookup"><span data-stu-id="73c7b-148">Once you've added your artifacts, you can [change the order in which the artifacts are run](#change-the-order-in-which-artifacts-are-run).</span></span> <span data-ttu-id="73c7b-149">Ayrıca geri gidebilirsiniz [görüntülemek veya bir yapı değiştirmek](#view-or-modify-an-artifact).</span><span class="sxs-lookup"><span data-stu-id="73c7b-149">You can also go back to [view or modify an artifact](#view-or-modify-an-artifact).</span></span>
1. <span data-ttu-id="73c7b-150">Ekleme yapıları bittiğinde, seçin **Uygula**</span><span class="sxs-lookup"><span data-stu-id="73c7b-150">When you're done adding artifacts, select **Apply**</span></span>

## <a name="change-the-order-in-which-artifacts-are-run"></a><span data-ttu-id="73c7b-151">Yapıları çalıştırdığınız sırasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="73c7b-151">Change the order in which artifacts are run</span></span>
<span data-ttu-id="73c7b-152">Varsayılan olarak, Eylemler yapılarının VM'ye eklenmiş sırada yürütülür.</span><span class="sxs-lookup"><span data-stu-id="73c7b-152">By default, the actions of the artifacts are executed in the order in which they are added to the VM.</span></span> <span data-ttu-id="73c7b-153">Aşağıdaki adımları yapıları çalıştığı sırayı değiştirmek nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="73c7b-153">The following steps illustrate how to change the order in which the artifacts are run.</span></span>

1. <span data-ttu-id="73c7b-154">Üstündeki **yapıları uygulamak** dikey penceresinde, VM için eklenene yapıları sayısını gösteren bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-154">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![VM eklenen yapıları sayısı](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="73c7b-156">Üzerinde **seçili yapıları** dikey penceresinde, sürükleyip yapıları istenen sıralamaya.</span><span class="sxs-lookup"><span data-stu-id="73c7b-156">On the **Selected artifacts** blade, drag and drop the artifacts into the desired order.</span></span> <span data-ttu-id="73c7b-157">**Not:** yapıyı sürükleyerek sorun yaşıyorsanız, yapıyı sol taraftan sürükleyerek emin olun.</span><span class="sxs-lookup"><span data-stu-id="73c7b-157">**Note:** If you have trouble dragging the artifact, make sure that you are dragging from the left side of the artifact.</span></span> 
1. <span data-ttu-id="73c7b-158">Tamamladığınızda **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-158">Select **OK** when done.</span></span>  

## <a name="view-or-modify-an-artifact"></a><span data-ttu-id="73c7b-159">Görüntüleme veya bir yapı değiştirme</span><span class="sxs-lookup"><span data-stu-id="73c7b-159">View or modify an artifact</span></span>
<span data-ttu-id="73c7b-160">Aşağıdaki adımları görüntülemek veya bir yapı parametreleri değiştirmek nasıl gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="73c7b-160">The following steps illustrate how to view or modify the parameters of an artifact:</span></span>

1. <span data-ttu-id="73c7b-161">Üstündeki **yapıları uygulamak** dikey penceresinde, VM için eklenene yapıları sayısını gösteren bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-161">At the top of the **Apply artifacts** blade, select the link indicating the number of artifacts that have been added to the VM.</span></span>
   
    ![VM eklenen yapıları sayısı](./media/devtest-lab-add-vm-with-artifacts/devtestlab-add-artifacts-blade-selected-artifacts.png)
1. <span data-ttu-id="73c7b-163">Üzerinde **seçili yapıları** dikey penceresinde görüntülemek veya düzenlemek istediğiniz yapıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-163">On the **Selected artifacts** blade, select the artifact that you want to view or edit.</span></span>  
1. <span data-ttu-id="73c7b-164">Üzerinde **ekleyin yapıt** dikey penceresinde, tüm değişikliklerin gerekli ve seçin yapma **Tamam** kapatmak için **ekleyin yapıt** dikey.</span><span class="sxs-lookup"><span data-stu-id="73c7b-164">On the **Add artifact** blade, make any needed changes, and select **OK** to close the **Add artifact** blade.</span></span>
1. <span data-ttu-id="73c7b-165">Seçin **Tamam** kapatmak için **seçili yapıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="73c7b-165">Select **OK** to close the **Selected artifacts** blade.</span></span>

## <a name="save-azure-resource-manager-template"></a><span data-ttu-id="73c7b-166">Azure Resource Manager şablonunu Kaydet</span><span class="sxs-lookup"><span data-stu-id="73c7b-166">Save Azure Resource Manager template</span></span>
<span data-ttu-id="73c7b-167">Bir Azure Resource Manager şablonu tekrarlanabilir bir dağıtımı tanımlamanın bildirim temelli bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="73c7b-167">An Azure Resource Manager template provides a declarative way to define a repeatable deployment.</span></span> <span data-ttu-id="73c7b-168">Aşağıdaki adımlar, oluşturulan VM için Azure Resource Manager şablonu kaydetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="73c7b-168">The following steps explain how to save the Azure Resource Manager template for the VM being created.</span></span>
<span data-ttu-id="73c7b-169">Kaydedildikten sonra Azure Resource Manager şablonu kullanabilirsiniz [Azure PowerShell ile yeni VM'ler dağıtmak](../azure-resource-manager/resource-group-overview.md#template-deployment).</span><span class="sxs-lookup"><span data-stu-id="73c7b-169">Once saved, you can use the Azure Resource Manager template to [deploy new VMs with Azure PowerShell](../azure-resource-manager/resource-group-overview.md#template-deployment).</span></span>

1. <span data-ttu-id="73c7b-170">Üzerinde **sanal makine** dikey penceresinde, select **ARM şablonu görüntüleme**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-170">On the **Virtual machine** blade, select **View ARM Template**.</span></span>
2. <span data-ttu-id="73c7b-171">Üzerinde **görünüm Azure Resource Manager şablonu** dikey penceresinde şablon metni seçin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-171">On the **View Azure Resource Manager template** blade, select the template text.</span></span>
3. <span data-ttu-id="73c7b-172">Seçili metni panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-172">Copy the selected text to the clipboard.</span></span>
4. <span data-ttu-id="73c7b-173">Seçin **Tamam** kapatmak için **görünüm Azure Resource Manager şablonu dikey**.</span><span class="sxs-lookup"><span data-stu-id="73c7b-173">Select **OK** to close the **View Azure Resource Manager Template blade**.</span></span>
5. <span data-ttu-id="73c7b-174">Bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-174">Open a text editor.</span></span>
6. <span data-ttu-id="73c7b-175">Panodaki şablonu metni yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="73c7b-175">Paste in the template text from the clipboard.</span></span>
7. <span data-ttu-id="73c7b-176">Daha sonra kullanmak için dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="73c7b-176">Save the file for later use.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

### <a name="next-steps"></a><span data-ttu-id="73c7b-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73c7b-177">Next steps</span></span>
* <span data-ttu-id="73c7b-178">VM oluşturulduktan sonra seçerek VM'ye bağlanabilir **Bağlan** VM dikey.</span><span class="sxs-lookup"><span data-stu-id="73c7b-178">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="73c7b-179">Bilgi edinmek için nasıl [DevTest Labs VM için özel yapılar oluşturma](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="73c7b-179">Learn how to [create custom artifacts for your DevTest Labs VM](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="73c7b-180">Araştır [DevTest Labs Azure Resource Manager hızlı başlangıç Şablon Galerisi](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="73c7b-180">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
