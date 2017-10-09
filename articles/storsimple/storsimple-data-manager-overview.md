---
title: "aaaMicrosoft Azure StorSimple Data Manager genel bakış | Microsoft Docs"
description: "Merhaba StorSimple veri Yöneticisi hizmetini (özel olarak incelenmektedir) genel bir bakış sağlar"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a><span data-ttu-id="3a8c3-103">StorSimple Data Manager genel bakış (özel olarak incelenmektedir)</span><span class="sxs-lookup"><span data-stu-id="3a8c3-103">StorSimple Data Manager overview (Private Preview)</span></span>

## <a name="overview"></a><span data-ttu-id="3a8c3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3a8c3-104">Overview</span></span>

<span data-ttu-id="3a8c3-105">Microsoft Azure StorSimple adresleri genellikle dosya paylaşımları ile ilgili yapılandırılmamış veriler karmaşıklığını hello bir karma bulut depolama çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-105">Microsoft Azure StorSimple is a hybrid cloud storage solution that addresses hello complexities of unstructured data commonly associated with file shares.</span></span> <span data-ttu-id="3a8c3-106">Merhaba uzantısı şirket içi çözüm ve otomatik olarak hello şirket içi depolama ve bulut depolama arasında veri katmanlarını gibi StorSimple bulut depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-106">StorSimple uses cloud storage as an extension of hello on-premises solution and automatically tiers data across hello on-premises storage and cloud storage.</span></span> <span data-ttu-id="3a8c3-107">Veri koruma, yerel ile tümleşik ve bulut anlık görüntüleri, sprawling bir depolama altyapısını hello gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-107">Integrated data protection, with local and cloud snapshots, eliminates hello need for a sprawling storage infrastructure.</span></span> <span data-ttu-id="3a8c3-108">Arşiv ve olağanüstü durum kurtarma ayrıca bir site dışı konumu olarak işlev gören hello bulut ile sorunsuz olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-108">Archival and disaster recovery is also seamless with hello cloud acting as an offsite location.</span></span>

<span data-ttu-id="3a8c3-109">Bu belgede, sunuyoruz hello veri dönüştürme hizmeti, tooseamlessly erişim hello hello bulutta StorSimple veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-109">hello data transformation service that we are introducing in this document, allows you tooseamlessly access hello StorSimple data in hello cloud.</span></span> <span data-ttu-id="3a8c3-110">Bu hizmet, StorSimple API'leri tooextract verileri sağlar ve tooother Azure sunmak taşımalarına tüketilebilir biçimlerde Hizmetleri.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-110">This service provides APIs tooextract data from StorSimple and present it tooother Azure services in formats that can be readily consumed.</span></span> <span data-ttu-id="3a8c3-111">Bu Önizleme'de desteklenen hello biçimler şunlardır: Azure BLOB'ları ve Azure Media Services varlıklar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-111">hello formats supported in this preview are Azure blobs and Azure Media Services assets.</span></span> <span data-ttu-id="3a8c3-112">Bu dönüştürme, tooeasily kablo gibi Azure Media Services, Azure Hdınsight, Azure Machine Learning ve Azure Search toooperate veri StorSimple 8000 serisi şirket içi cihazda hizmetlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-112">This transformation enables you tooeasily wire up services such as Azure Media Services, Azure HDInsight, Azure Machine Learning, and Azure Search toooperate data on StorSimple 8000 series on-premises device.</span></span>

<span data-ttu-id="3a8c3-113">Bu gösteren üst düzey blok diyagramını aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-113">A high-level block diagram illustrating this is shown below.</span></span>

![Üst düzey diyagramı](./media//storsimple-data-manager-overview/high-level-diagram.png)

<span data-ttu-id="3a8c3-115">Bu belgede, bu hizmet için bir özel Önizleme ne kaydolabilirsiniz açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-115">This document explains how you can sign up for a private preview of this service.</span></span> <span data-ttu-id="3a8c3-116">Ayrıca, StorSimple veri ve diğer Azure hizmetleriyle hello bulutta kullanma Bu hizmet toowrite uygulamaların nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-116">It also explains how you can use this service toowrite applications that use StorSimple data and other Azure services in hello cloud.</span></span>

## <a name="sign-up-for-data-manager-preview"></a><span data-ttu-id="3a8c3-117">Veri Yöneticisi Önizleme için kaydolma</span><span class="sxs-lookup"><span data-stu-id="3a8c3-117">Sign up for Data Manager preview</span></span>
<span data-ttu-id="3a8c3-118">Merhaba veri Yöneticisi hizmeti için kaydolmadan önce hello aşağıdaki önkoşulları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-118">Before you sign up for hello Data Manager service, review hello following prerequisites.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3a8c3-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3a8c3-119">Prerequisites</span></span>

<span data-ttu-id="3a8c3-120">Bu alıştırmada, sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-120">This exercise assumes that you have</span></span>
* <span data-ttu-id="3a8c3-121">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-121">an active Azure subscription.</span></span>
* <span data-ttu-id="3a8c3-122">StorSimple 8000 serisi aygıt erişim tooa kayıtlı</span><span class="sxs-lookup"><span data-stu-id="3a8c3-122">access tooa registered StorSimple 8000 series device</span></span>
* <span data-ttu-id="3a8c3-123">Tüm hello StorSimple 8000 serisi aygıtla ilişkili tuşlarını hello.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-123">all hello keys associated with hello StorSimple 8000 series device.</span></span>

### <a name="sign-up"></a><span data-ttu-id="3a8c3-124">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="3a8c3-124">Sign up</span></span>

<span data-ttu-id="3a8c3-125">Merhaba StorSimple veri Yöneticisi özel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-125">hello StorSimple Data Manager is in private preview.</span></span> <span data-ttu-id="3a8c3-126">Bu hizmet özel önizlemesi için adımları toosign aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3a8c3-126">Perform hello following steps toosign up for a private preview of this service:</span></span>

1.  <span data-ttu-id="3a8c3-127">Oturum hello Azure portal hello StorSimple Data Manager uzantısına sahip: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span><span class="sxs-lookup"><span data-stu-id="3a8c3-127">Log into hello Azure portal with hello StorSimple Data Manager extension at: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager).</span></span> <span data-ttu-id="3a8c3-128">Azure kimlik toolog kullanın.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-128">Use your Azure credentials toolog in.</span></span>

2.  <span data-ttu-id="3a8c3-129">Merhaba tıklatın  **+**  simgesi toocreate bir hizmet.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-129">Click hello **+** icon toocreate a service.</span></span> <span data-ttu-id="3a8c3-130">Tıklatın **depolama** ve ardından **bkz tüm** açılan hello dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-130">Click **Storage** and then click **See All** in hello blade that opens up.</span></span>

    ![Arama StorSimple veri Yöneticisi simgesi](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. <span data-ttu-id="3a8c3-132">Merhaba StorSimple Data Manager simgesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-132">You see hello StorSimple Data Manager icon.</span></span>

    ![StorSimple veri Yöneticisi simgesini seçin](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. <span data-ttu-id="3a8c3-134">StorSimple veri Yöneticisi simgesine tıklayın ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-134">Click StorSimple Data Manager icon and then click **Create**.</span></span> <span data-ttu-id="3a8c3-135">Merhaba özel önizlemesine tooenable istediğiniz ve ardından hello abonelik çekme **bana kaydolun!**</span><span class="sxs-lookup"><span data-stu-id="3a8c3-135">Pick hello subscription that you want tooenable for hello private preview and then click **Sign me up!**</span></span>

    ![Bana kaydolun](./media/storsimple-data-manager-overview/sign-me-up.png)

5. <span data-ttu-id="3a8c3-137">Bu istek tooonboard gönderir.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-137">This sends a request tooonboard you.</span></span> <span data-ttu-id="3a8c3-138">Biz yerleşik mümkün olan en kısa sürede çalışacaksınız.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-138">We will onboard you as soon as possible.</span></span> <span data-ttu-id="3a8c3-139">Aboneliğinizi etkinleştirildikten sonra StorSimple veri Yöneticisi hizmeti oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-139">After your subscription is enabled, you can create a StorSimple Data Manager service.</span></span>

6. <span data-ttu-id="3a8c3-140">tooeasily hello StorSimple veri Yöneticisi hizmetine erişim, hello yıldız simgesine toopin'ı tıklatın, tooyour Sık Kullanılanlar.</span><span class="sxs-lookup"><span data-stu-id="3a8c3-140">tooeasily access hello StorSimple Data Manager service, click hello star icon toopin it tooyour favorites.</span></span>

    ![Erişim StorSimple veri yöneticileri](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a><span data-ttu-id="3a8c3-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a8c3-142">Next steps</span></span>

<span data-ttu-id="3a8c3-143">[StorSimple veri Yöneticisi kullanıcı Arabirimi tootransform verilerinizi kullanma](storsimple-data-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="3a8c3-143">[Use StorSimple Data Manager UI tootransform your data](storsimple-data-manager-ui.md).</span></span>
