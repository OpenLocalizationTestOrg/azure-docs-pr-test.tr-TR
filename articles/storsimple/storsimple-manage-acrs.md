---
title: "StorSimple erişim denetimi kayıtları yönetme | Microsoft Docs"
description: "Erişim denetimi kayıtları (ACRs) barındıran bir birime bağlanabilir belirlemek için StorSimple cihazında nasıl kullanılacağını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="90f7c-103">Erişim denetimi kayıtları yönetmek için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="90f7c-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="90f7c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="90f7c-104">Overview</span></span>
<span data-ttu-id="90f7c-105">Erişim denetimi kayıtları (ACRs), StorSimple cihaz üzerindeki bir birimi hangi ana bilgisayarların bağlanabileceği belirtmenize olanak verir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="90f7c-106">ACRs belirli bir birimi ayarlayın ve ana bilgisayarların iSCSI nitelikli adlar (IQN'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="90f7c-107">Bir ana bilgisayara bir birime bağlanmaya çalıştığında, cihaz IQN adının bu birimde ACR ilişkili ve bir eşleşme varsa, ardından bağlantı kurulur denetler.</span><span class="sxs-lookup"><span data-stu-id="90f7c-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="90f7c-108">Erişim denetimi kayıtları bölüm üzerinde **yapılandırma** sayfası konak karşılık gelen IQN'ler ile tüm erişim denetimi kayıtları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="90f7c-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="90f7c-109">Bu öğretici ACR ile ilgili aşağıdaki ortak görevler açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="90f7c-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="90f7c-110">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="90f7c-110">Add an access control record</span></span> 
* <span data-ttu-id="90f7c-111">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="90f7c-111">Edit an access control record</span></span> 
* <span data-ttu-id="90f7c-112">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="90f7c-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="90f7c-113">Bir ACR bir birime atarken, bu birim bozuk olabilir çünkü birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="90f7c-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="90f7c-114">Bir ACR bir birimden silerken, silme, okuma-yazma kesilme neden olabilir çünkü karşılık gelen ana birim eriştiğini değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="90f7c-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="90f7c-115">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="90f7c-115">Add an access control record</span></span>
<span data-ttu-id="90f7c-116">StorSimple Yöneticisi hizmetini kullanma **yapılandırma** ACRs eklemek için sayfa.</span><span class="sxs-lookup"><span data-stu-id="90f7c-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="90f7c-117">Genellikle, bir birimle bir ACR ilişkilendireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="90f7c-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="90f7c-118">Bir ACR eklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="90f7c-119">Bir erişim denetimi kaydı eklemek için</span><span class="sxs-lookup"><span data-stu-id="90f7c-119">To add an access control record</span></span>
1. <span data-ttu-id="90f7c-120">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="90f7c-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="90f7c-121">Altında Tablo listesindeki **erişim denetimi kayıtları**, sağlar bir **adı** verin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="90f7c-122">Windows ana bilgisayarınız IQN adını sağlayın **iSCSI başlatıcısı adı**.</span><span class="sxs-lookup"><span data-stu-id="90f7c-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="90f7c-123">Windows Server konağının IQN'sini almak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="90f7c-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="90f7c-124">Microsoft iSCSI başlatıcısını Windows konağında başlatın.</span><span class="sxs-lookup"><span data-stu-id="90f7c-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="90f7c-125">**iSCSI Başlatıcısı Özellikleri** penceresinin **Yapılandırma** sekmesinde, **Başlatıcı Adı** alanından dizeyi seçip kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="90f7c-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="90f7c-126">Bu dizesini yapıştırabilir **iSCSI başlatıcısı adı** Klasik Azure portalı ACRs tablosunda alan.</span><span class="sxs-lookup"><span data-stu-id="90f7c-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="90f7c-127">Tıklatın **kaydetmek** yeni oluşturulan ACR kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="90f7c-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="90f7c-128">Sekmeli liste, bu toplama yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="90f7c-129">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="90f7c-129">Edit an access control record</span></span>
<span data-ttu-id="90f7c-130">Kullandığınız **yapılandırma** ACRs düzenlemek için Klasik Azure portalındaki sayfası.</span><span class="sxs-lookup"><span data-stu-id="90f7c-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="90f7c-131">Şu anda kullanımda olmayan ACRs değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90f7c-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="90f7c-132">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR düzenlemek için önce birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="90f7c-133">Bir ACR düzenlemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="90f7c-134">Bir erişim denetimi kaydını düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="90f7c-134">To edit an access control record</span></span>
1. <span data-ttu-id="90f7c-135">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="90f7c-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="90f7c-136">Erişim denetimi kayıtları Tablo listesinde değiştirmek istediğiniz ACR gelin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="90f7c-137">Yeni bir ad ve/veya IQN için ACR sağlayın.</span><span class="sxs-lookup"><span data-stu-id="90f7c-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="90f7c-138">Tıklatın **kaydetmek** değiştirilmiş ACR kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="90f7c-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="90f7c-139">Sekmeli liste, bu değişikliği yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="90f7c-140">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="90f7c-140">Delete an access control record</span></span>
<span data-ttu-id="90f7c-141">Kullandığınız **yapılandırma** ACRs silmek için Azure Klasik portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="90f7c-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="90f7c-142">Şu anda kullanımda olmayan ACRs silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90f7c-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="90f7c-143">Şu anda kullanılmakta olan bir birimi ile ilişkili bir ACR silmek için önce birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="90f7c-144">Bir erişim denetimi kaydını silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="90f7c-145">Bir erişim denetimi kaydını silmek için</span><span class="sxs-lookup"><span data-stu-id="90f7c-145">To delete an access control record</span></span>
1. <span data-ttu-id="90f7c-146">Hizmet giriş sayfasında hizmetinizi seçin, hizmet adına çift tıklayın ve ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="90f7c-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="90f7c-147">Erişim denetimi kayıtları (ACRs) Tablo listesinde silmek istediğiniz ACR gelin.</span><span class="sxs-lookup"><span data-stu-id="90f7c-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="90f7c-148">Sil simgesini (**x**) için seçtiğiniz ACR aşırı sağ sütunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="90f7c-149">Tıklatın **x** ACR silmek için simge.</span><span class="sxs-lookup"><span data-stu-id="90f7c-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="90f7c-150">Onayınız istendiğinde tıklatın **Evet** silme işlemine devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="90f7c-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="90f7c-151">Sekmeli liste silme yansıtacak şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="90f7c-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90f7c-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90f7c-152">Next steps</span></span>
* <span data-ttu-id="90f7c-153">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="90f7c-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="90f7c-154">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="90f7c-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

