---
title: "StorSimple aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir (ACRs) toodetermine toouse erişim denetimi kayıtları nasıl açıklar."
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="2ea51-103">Merhaba StorSimple Yöneticisi hizmet toomanage erişim denetimi kayıtları kullanın</span><span class="sxs-lookup"><span data-stu-id="2ea51-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="2ea51-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="2ea51-104">Overview</span></span>
<span data-ttu-id="2ea51-105">Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir toospecify izin verin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="2ea51-106">ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler).</span><span class="sxs-lookup"><span data-stu-id="2ea51-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="2ea51-107">Bir konak tooconnect tooa birim çalıştığında hello aygıt hello IQN adı ve bir eşleşmesi durumunda hello bağlantı kurulur bu birimde ACR ilişkili hello denetler.</span><span class="sxs-lookup"><span data-stu-id="2ea51-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="2ea51-108">Merhaba erişim denetimi kayıtları hello bölüm **yapılandırma** sayfası ile Merhaba hello ana IQN'ler karşılık gelen tüm hello erişim denetimi kayıtları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2ea51-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="2ea51-109">Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="2ea51-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="2ea51-110">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="2ea51-110">Add an access control record</span></span> 
* <span data-ttu-id="2ea51-111">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="2ea51-111">Edit an access control record</span></span> 
* <span data-ttu-id="2ea51-112">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="2ea51-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="2ea51-113">ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="2ea51-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="2ea51-114">Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.</span><span class="sxs-lookup"><span data-stu-id="2ea51-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="2ea51-115">Bir erişim denetimi kaydı ekleme</span><span class="sxs-lookup"><span data-stu-id="2ea51-115">Add an access control record</span></span>
<span data-ttu-id="2ea51-116">Merhaba StorSimple Yöneticisi hizmetini kullanma **yapılandırma** tooadd ACRs sayfa.</span><span class="sxs-lookup"><span data-stu-id="2ea51-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="2ea51-117">Genellikle, bir birimle bir ACR ilişkilendireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="2ea51-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="2ea51-118">Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="2ea51-119">tooadd bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="2ea51-119">tooadd an access control record</span></span>
1. <span data-ttu-id="2ea51-120">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2ea51-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2ea51-121">Merhaba altında listeleme tablo içinde **erişim denetimi kayıtları**, sağlar bir **adı** verin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="2ea51-122">Merhaba IQN altında Windows ana bilgisayar adını sağlayın **iSCSI başlatıcısı adı**.</span><span class="sxs-lookup"><span data-stu-id="2ea51-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="2ea51-123">tooget Merhaba, Windows Server konağının IQN'ini hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="2ea51-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="2ea51-124">Merhaba Microsoft iSCSI başlatıcısını Windows konağında başlatın.</span><span class="sxs-lookup"><span data-stu-id="2ea51-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="2ea51-125">Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **yapılandırma** sekmesinde seçin ve hello hello dize kopyalama **Başlatıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="2ea51-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="2ea51-126">Bu dize hello Yapıştır **iSCSI başlatıcısı adı** ' hello Azure Klasik portalı de hello ACRs tabloda alan.</span><span class="sxs-lookup"><span data-stu-id="2ea51-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="2ea51-127">Tıklatın **kaydetmek** toosave hello ACR yeni oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="2ea51-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="2ea51-128">Merhaba tablo olacak listeleme güncelleştirilmiş tooreflect bu toplama olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ea51-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="2ea51-129">Bir erişim denetimi kaydı Düzenle</span><span class="sxs-lookup"><span data-stu-id="2ea51-129">Edit an access control record</span></span>
<span data-ttu-id="2ea51-130">Merhaba kullandığınız **yapılandırma** hello Azure Klasik portalı tooedit ACRs sayfasında.</span><span class="sxs-lookup"><span data-stu-id="2ea51-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ea51-131">Şu anda kullanımda olmayan ACRs değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ea51-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2ea51-132">şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ea51-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="2ea51-133">Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="2ea51-134">tooedit bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="2ea51-134">tooedit an access control record</span></span>
1. <span data-ttu-id="2ea51-135">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2ea51-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2ea51-136">Merhaba Tablo listesindeki hello erişim denetimi kayıtları, toomodify istediğiniz ACR hello gelin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="2ea51-137">Yeni bir ad ve/veya IQN Merhaba ACR sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2ea51-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="2ea51-138">Tıklatın **kaydetmek** toosave hello ACR değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="2ea51-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="2ea51-139">Merhaba tablo olacak listeleme güncelleştirilmiş tooreflect bu değişikliği olabilir.</span><span class="sxs-lookup"><span data-stu-id="2ea51-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="2ea51-140">Bir erişim denetimi kaydını sil</span><span class="sxs-lookup"><span data-stu-id="2ea51-140">Delete an access control record</span></span>
<span data-ttu-id="2ea51-141">Merhaba kullandığınız **yapılandırma** hello Azure Klasik portalı toodelete ACRs sayfasında.</span><span class="sxs-lookup"><span data-stu-id="2ea51-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ea51-142">Şu anda kullanımda olmayan ACRs silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ea51-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2ea51-143">şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma getirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="2ea51-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="2ea51-144">Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="2ea51-145">toodelete bir erişim denetimi kaydı</span><span class="sxs-lookup"><span data-stu-id="2ea51-145">toodelete an access control record</span></span>
1. <span data-ttu-id="2ea51-146">Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2ea51-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="2ea51-147">Merhaba Tablo listesindeki hello erişim denetim kayıtlarının (ACRs), toodelete istediğiniz ACR hello gelin.</span><span class="sxs-lookup"><span data-stu-id="2ea51-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="2ea51-148">Sil simgesini (**x**) hello aşırı sağ sütundaki hello Seçtiğiniz ACR için görünür.</span><span class="sxs-lookup"><span data-stu-id="2ea51-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="2ea51-149">Merhaba tıklatın **x** simgesi toodelete hello ACR.</span><span class="sxs-lookup"><span data-stu-id="2ea51-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="2ea51-150">Onayınız istendiğinde tıklatın **Evet** toocontinue hello silme işlemi ile.</span><span class="sxs-lookup"><span data-stu-id="2ea51-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="2ea51-151">Merhaba sekmeli liste güncelleştirilmiş tooreflect hello silme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="2ea51-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea51-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ea51-152">Next steps</span></span>
* <span data-ttu-id="2ea51-153">Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="2ea51-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="2ea51-154">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2ea51-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

