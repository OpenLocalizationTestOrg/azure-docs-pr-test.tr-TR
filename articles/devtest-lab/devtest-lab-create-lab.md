---
title: Azure DevTest Labs laboratuvarda aaaCreate | Microsoft Docs
description: "Sanal makineler için Azure DevTest Labs'de bir laboratuvar oluşturma"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="00868-103">Azure DevTest Labs'de laboratuvar oluşturma</span><span class="sxs-lookup"><span data-stu-id="00868-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="00868-104">Sınırları ve kotalar belirterek daha iyi olanak sağlayan sanal makineler (VM'ler), bu kaynakları yönetmek gibi Azure DevTest Labs laboratuvarda kaynakları, bir grup kapsayan hello altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="00868-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="00868-105">Bu makalede hello Azure portal kullanarak bir laboratuvar oluşturma hello işleminde size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="00868-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00868-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="00868-106">Prerequisites</span></span>
<span data-ttu-id="00868-107">toocreate bir laboratuvar, şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="00868-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="00868-108">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="00868-108">An Azure subscription.</span></span> <span data-ttu-id="00868-109">Azure satın alma seçenekleri hakkında toolearn bkz [nasıl toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) veya [ücretsiz bir aylık deneme](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00868-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="00868-110">Merhaba abonelik toocreate hello Laboratuvar hello sahibi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="00868-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="00868-111">Adımları toocreate Azure DevTest Labs laboratuvarda</span><span class="sxs-lookup"><span data-stu-id="00868-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="00868-112">Aşağıdaki adımları hello nasıl toouse hello Azure portal toocreate Azure DevTest Labs laboratuvarda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="00868-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="00868-113">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="00868-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="00868-114">Merhaba ana menüden hello sol tarafında seçin **daha Hizmetleri** (sonundaki hello hello listesi).</span><span class="sxs-lookup"><span data-stu-id="00868-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Diğer hizmetler menü seçeneği](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="00868-116">Kullanılabilir hizmetler hello listesinden **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="00868-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="00868-117">Merhaba üzerinde **DevTest Labs** dikey penceresinde, select **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="00868-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Laboratuvar ekleme](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="00868-119">Merhaba üzerinde **DevTest Lab Oluştur** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="00868-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="00868-120">Girin bir **Laboratuvar adı** hello yeni Laboratuvar için.</span><span class="sxs-lookup"><span data-stu-id="00868-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="00868-121">Select hello **abonelik** tooassociate hello Laboratuvar ile.</span><span class="sxs-lookup"><span data-stu-id="00868-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="00868-122">Seçin bir **konumu** hangi toostore hello laboratuarda.</span><span class="sxs-lookup"><span data-stu-id="00868-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="00868-123">Seçin **otomatik kapatma** toospecify tooenable - isterseniz ve hello parametrelerini - tanımlayın hello otomatik tüm hello Laboratuvar'ın Vm'leri kapatılıyor.</span><span class="sxs-lookup"><span data-stu-id="00868-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="00868-124">Merhaba otomatik kapatma özelliği yapabildiği belirtebilirsiniz VM hello istediğinizde çoğunlukla bir maliyet tasarrufu özelliğidir tooautomatically kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="00868-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="00868-125">Merhaba makalede açıklanan başlangıç adımları izleyerek hello Laboratuvar oluşturduktan sonra otomatik kapatma ayarları değiştirebilirsiniz [Azure DevTest Labs laboratuvarda yönelik tüm ilkeleri yönetmek](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="00868-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="00868-126">Seçin **PIN tooDashboard** hello Laboratuvar tooappear hello portal panosunda, bir kısayol istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="00868-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="00868-127">Seçin **Otomasyon seçenekleri** tooget Azure Resource Manager şablonları yapılandırma Otomasyon için.</span><span class="sxs-lookup"><span data-stu-id="00868-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="00868-128">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="00868-128">Select **Create**.</span></span> <span data-ttu-id="00868-129">Seçtikten sonra **oluşturma**, hello **DevTest Labs** dikey penceresinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="00868-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="00868-130">Merhaba izleyerek hello Laboratuvar oluşturma işlemi hello durumunu izleyebilirsiniz **bildirimleri** alanı.</span><span class="sxs-lookup"><span data-stu-id="00868-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="00868-131">Tamamlandığında, yenileme hello sayfa toosee hello Laboratuvar hello labs listesinde yeni oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="00868-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Laboratuvar dikey penceresi oluşturma](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="00868-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00868-133">Next steps</span></span>
<span data-ttu-id="00868-134">Laboratuvarınızı oluşturduktan sonra bazı sonraki adımları tooconsider şunlardır:</span><span class="sxs-lookup"><span data-stu-id="00868-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="00868-135">[Güvenli erişim tooa Laboratuvar](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="00868-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="00868-136">[Laboratuvar ilkeleri belirleme](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="00868-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="00868-137">[Laboratuvar şablonu oluşturma](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="00868-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="00868-138">[VM'leriniz için özel yapılar oluşturma](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="00868-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="00868-139">[Yapıları tooa Laboratuvar'yle bir VM'yi eklemek](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="00868-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

