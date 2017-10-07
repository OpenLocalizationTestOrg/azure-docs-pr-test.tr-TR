---
title: "aaaMicrosoft Azure StorSimple ve bulut çözümleri sağlayıcısı Program genel bakış | Microsoft Docs"
description: "StorSimple iş ortakları için bir genel bakış hello StorSimple ve CSP hakkında."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="3af1a-103">StorSimple sanal dizinin bulut çözümü sağlayıcısı programı için dağıtma</span><span class="sxs-lookup"><span data-stu-id="3af1a-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="3af1a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3af1a-104">Overview</span></span>

<span data-ttu-id="3af1a-105">StorSimple sanal dizinin müşterileri için hello bulut çözümü sağlayıcısı (CSP) iş ortakları tarafından dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="3af1a-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="3af1a-106">Bir CSP ortak bir StorSimple cihaz Yöneticisi hizmeti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3af1a-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="3af1a-107">Bu hizmet, ardından kullanılan toodeploy olması ve StorSimple sanal dizinin yönetmek ve paylaşımları, birimler ve yedekleme hello ilişkili.</span><span class="sxs-lookup"><span data-stu-id="3af1a-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="3af1a-108">Bu makalede, nasıl bir CSP ortak bir müşteri veya yeni bir abonelik tooan varolan müşteri ekleyin ve sonra hizmet toodeploy bir StorSimple sanal dizi CSP oluşturun açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3af1a-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3af1a-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3af1a-109">Prerequisites</span></span>

<span data-ttu-id="3af1a-110">Başlamadan önce emin olun:</span><span class="sxs-lookup"><span data-stu-id="3af1a-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="3af1a-111">Merhaba CSP program altında kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="3af1a-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="3af1a-112">Geçerli sahip [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) oturum açma kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3af1a-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="3af1a-113">Merhaba kimlik toosign toohello iş ortağı portalı tooadd yeni müşteriler etkinleştirmek, müşteriler için arama veya tooa müşteri hesabı hello iş ortağı panosundan gidin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="3af1a-114">Merhaba CSP hello Azure portal hello müşteri adına bir StorSimple Yöneticisi olarak işlev görebilir.</span><span class="sxs-lookup"><span data-stu-id="3af1a-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="3af1a-115">Bir müşteri ekleyin</span><span class="sxs-lookup"><span data-stu-id="3af1a-115">Add a customer</span></span>

<span data-ttu-id="3af1a-116">Bir müşteri eklerseniz, bir abonelik otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="3af1a-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="3af1a-117">bir müşteri tooadd (ve otomatik olarak bir abonelik oluşturun), hello aşağıdaki hello iş ortağı Portalı'ndaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="3af1a-118">Toohello Git [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) ve CSP kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3af1a-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="3af1a-119">Tıklatın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-119">Click **Dashboard**.</span></span>

     ![İş ortağı Merkezi'nde Panosu](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="3af1a-121">Merhaba sol-bölmesinde **müşteriler**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="3af1a-122">Merhaba sağ-bölmesinde **müşteriler eklemek**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="3af1a-123">Merhaba müşteri Hello ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="3af1a-124">Tıklatın **sonraki: abonelikleri** toocreate bir müşteri aboneliğe.</span><span class="sxs-lookup"><span data-stu-id="3af1a-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Müşteri ekleme](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="3af1a-126">Seçin **Microsoft Azure** sunar.</span><span class="sxs-lookup"><span data-stu-id="3af1a-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="3af1a-127">Kaydırma toohello alt hello sayfasını tıklatın ve **gözden**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Abonelik bilgileri gözden geçirin](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="3af1a-129">Merhaba bilgileri gözden geçirin ve tıklayın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-129">Review hello information and click **Submit**.</span></span>

    ![Abonelik gönderme](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="3af1a-131">İleride kullanılmak üzere Hello onay bilgilerini kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-131">Save hello confirmation information for future reference.</span></span>

    ![Kaydetme onayı](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="3af1a-133">Bulma veya yeni eklediğiniz toohello müşteri gidin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="3af1a-134">Merhaba tıklatın **şirket adı** hello ayrıntıları içine aşağı toodrill.</span><span class="sxs-lookup"><span data-stu-id="3af1a-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Merhaba müşteri arayın](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="3af1a-136">Merhaba sol bölmede seçin **Hizmet Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="3af1a-137">Merhaba altında sağ bölmede, içinde **yönetmek Hizmetleri**, tıklatın **Microsoft Azure Yönetim Portalı** içinde toosign müşteri için Azure yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3af1a-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![TooAzure Portalı'nda oturum açın](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="3af1a-139">toocreate StorSimple cihaz Yöneticisi tıklatın **+ yeni** ve arayın veya çok gidin**StorSimple sanal cihaz seri**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="3af1a-140">Daha fazla bilgi için çok Git[StorSimple Aygıt Yöneticisi'ni hizmet dağıtma](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="3af1a-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple cihaz Yöneticisi hizmeti oluşturma](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="3af1a-142">Bir abonelik Ekle</span><span class="sxs-lookup"><span data-stu-id="3af1a-142">Add a subscription</span></span>

<span data-ttu-id="3af1a-143">Bazı durumlarda, varolan bir müşteri olabilir ve tooadd bir abonelik gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="3af1a-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="3af1a-144">tooadd bir abonelik tooan varolan müşteri hello aşağıdaki hello iş ortağı Portalı'ndaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="3af1a-145">Toohello Git [ortağı Merkezi'nde](http://partnercenter.microsoft.com/) ve CSP kimlik bilgilerinizi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3af1a-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="3af1a-146">Tıklatın **Pano**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-146">Click **Dashboard**.</span></span>

     ![İş ortağı Merkezi'nde Panosu](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="3af1a-148">Merhaba sol-bölmesinde **müşteriler**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="3af1a-149">Bulma veya aboneliği tooadd istediğiniz toohello müşteri gidin.</span><span class="sxs-lookup"><span data-stu-id="3af1a-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="3af1a-150">Merhaba tıklatın ![genişletme onay simgesi](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) simgesi tooexpand hello satır hello şirket adı, müşteriniz için.</span><span class="sxs-lookup"><span data-stu-id="3af1a-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="3af1a-151">Merhaba Ayrıntılar tıklatın **abonelik ekleme**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-151">In hello details, click **Add subscriptions**.</span></span>

    ![Müşteriler](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="3af1a-153">Denetleyin **Microsoft Azure** hello için **üst teklifleri** hello abonelik ve tıklatın **gönderme**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="3af1a-154">Bu, yeni bir abonelik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3af1a-154">This creates a new subscription.</span></span>

    ![Yeni Abonelik Ekle](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="3af1a-156">Yeni bir abonelik oluşturulduktan sonra tıklatın **<--müşteriler** hello sol bölmede tooreturn toohello içinde **müşteriler** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3af1a-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="3af1a-157">Kendisi için bir abonelik oluşturduğunuz hello müşteri arayın.</span><span class="sxs-lookup"><span data-stu-id="3af1a-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="3af1a-158">Merhaba tıklatın **şirket adı** hello ayrıntıları içine aşağı toodrill.</span><span class="sxs-lookup"><span data-stu-id="3af1a-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Merhaba müşteri arayın](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="3af1a-160">Merhaba sol bölmede seçin **Hizmet Yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="3af1a-161">Merhaba altında sağ bölmede, içinde **yönetmek Hizmetleri**, tıklatın **Microsoft Azure Yönetim Portalı** içinde toosign müşteri için Azure yönetici olarak.</span><span class="sxs-lookup"><span data-stu-id="3af1a-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![TooAzure Portalı'nda oturum açın](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="3af1a-163">toocreate StorSimple cihaz Yöneticisi tıklatın **+ yeni** ve arayın veya çok gidin**StorSimple sanal cihaz seri**.</span><span class="sxs-lookup"><span data-stu-id="3af1a-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="3af1a-164">Daha fazla bilgi için çok Git[StorSimple Aygıt Yöneticisi'ni hizmet dağıtma](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="3af1a-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![StorSimple cihaz Yöneticisi hizmeti oluşturma](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="3af1a-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3af1a-166">Next steps</span></span>

- <span data-ttu-id="3af1a-167">CSP hello StorSimple daha fazla sorularınız varsa, çok gidin[CSP StorSimple: sık sorulan sorular](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3af1a-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="3af1a-168">Kullanıyorsanız toodeploy, StorSimple Git çok hazır[, StorSimple CSP içinde dağıtmak](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3af1a-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
