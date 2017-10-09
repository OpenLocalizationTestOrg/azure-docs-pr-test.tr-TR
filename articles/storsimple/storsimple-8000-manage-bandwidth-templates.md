---
title: "StorSimple 8000 serisi için aaaManage bant genişliği şablonları | Microsoft Docs"
description: "Açıklar nasıl toocontrol bant genişliği kullanılmasına izin ver toomanage StorSimple bant genişliği şablonları."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a><span data-ttu-id="0769f-103">Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple bant genişliği şablonları kullanın.</span><span class="sxs-lookup"><span data-stu-id="0769f-103">Use hello StorSimple Device Manager service toomanage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="0769f-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0769f-104">Overview</span></span>

<span data-ttu-id="0769f-105">Bant genişliği şablonları birden çok gün saat zamanlamaları tootier hello verilerden hello StorSimple cihaz toohello bulut üzerinden tooconfigure ağ bant genişliği kullanımı sağlar.</span><span class="sxs-lookup"><span data-stu-id="0769f-105">Bandwidth templates allow you tooconfigure network bandwidth usage across multiple time-of-day schedules tootier hello data from hello StorSimple device toohello cloud.</span></span>

<span data-ttu-id="0769f-106">Bant genişliği zamanlamaları azaltma ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0769f-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="0769f-107">Özelleştirilmiş bant genişliği zamanlamaları hello iş yükü ağ kullanımları bağlı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="0769f-107">Specify customized bandwidth schedules depending on hello workload network usages.</span></span>
* <span data-ttu-id="0769f-108">Yönetim merkezileştirmek ve hello zamanlamaları birçok cihaz arasında kolay ve sorunsuz bir şekilde yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-108">Centralize management and reuse hello schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="0769f-109">Bu özellik yalnızca StorSimple fiziksel cihazlar (modeller 8100 ve 8600) için ve StorSimple bulut cihazları (modeller 8010 hem de 8020) için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0769f-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="hello-bandwidth-templates-blade"></a><span data-ttu-id="0769f-110">Merhaba bant genişliği şablonları dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="0769f-110">hello Bandwidth templates blade</span></span>

<span data-ttu-id="0769f-111">Merhaba **bant genişliği şablonları** dikey tablo biçiminde tüm hello bant genişliği şablonları hizmetiniz için sahip ve aşağıdaki bilgilerle hello içeren:</span><span class="sxs-lookup"><span data-stu-id="0769f-111">hello **Bandwidth templates** blade has all hello bandwidth templates for your service in a tabular format, and contains hello following information:</span></span>

* <span data-ttu-id="0769f-112">**Ad** – oluşturulduğunda atanan benzersiz bir ad toohello bant genişliği şablonu.</span><span class="sxs-lookup"><span data-stu-id="0769f-112">**Name** – A unique name assigned toohello bandwidth template when it was created.</span></span>
* <span data-ttu-id="0769f-113">**Zamanlama** – hello verilen bant genişliği şablonundaki zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="0769f-113">**Schedule** – hello number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="0769f-114">**Tarafından kullanılan** – hello hello bant genişliği şablonları kullanarak birimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="0769f-114">**Used by** – hello number of volumes using hello bandwidth templates.</span></span>

<span data-ttu-id="0769f-115">Ek bilgi toohelp bant genişliği şablonları yapılandırmak da bulabilirsiniz içinde:</span><span class="sxs-lookup"><span data-stu-id="0769f-115">You can also find additional information toohelp configure bandwidth templates in:</span></span>

* [<span data-ttu-id="0769f-116">Bant genişliği şablonları hakkında sorular ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="0769f-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="0769f-117">Bant genişliği şablonları için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="0769f-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="0769f-118">Bant genişliği şablonu ekleyin</span><span class="sxs-lookup"><span data-stu-id="0769f-118">Add a bandwidth template</span></span>

<span data-ttu-id="0769f-119">Aşağıdaki adımları toocreate yeni bant genişliği şablonu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0769f-119">Perform hello following steps toocreate a new bandwidth template.</span></span>

#### <a name="tooadd-a-bandwidth-template"></a><span data-ttu-id="0769f-120">tooadd bant genişliği şablonu</span><span class="sxs-lookup"><span data-stu-id="0769f-120">tooadd a bandwidth template</span></span>

1. <span data-ttu-id="0769f-121">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, tıklatın **bant genişliği şablonları** ve ardından **+ Ekle bant genişliği şablonu**.</span><span class="sxs-lookup"><span data-stu-id="0769f-121">Go tooyour StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![Bant genişliği şablonu ekleyin + tıklayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="0769f-123">Merhaba, **bant genişliği şablonu Ekle** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="0769f-123">In hello **Add bandwidth template** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="0769f-124">Bant genişliği şablonu için benzersiz bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="0769f-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="0769f-125">Bir bant genişliği zamanlama tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0769f-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="0769f-126">bir zamanlama toocreate:</span><span class="sxs-lookup"><span data-stu-id="0769f-126">toocreate a schedule:</span></span>
   
        1. <span data-ttu-id="0769f-127">Merhaba Hello aşağı açılan listeden seçin **gün** hello hafta Merhaba zamanlama için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="0769f-127">From hello drop-down list, choose hello **Days** of hello week hello schedule is configured for.</span></span> <span data-ttu-id="0769f-128">Birden fazla gün seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="0769f-129">Girin bir **başlangıç saati** içinde _ss: dd_ biçimi.</span><span class="sxs-lookup"><span data-stu-id="0769f-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="0769f-130">Merhaba zamanlama başlar, bu olur.</span><span class="sxs-lookup"><span data-stu-id="0769f-130">This is when hello schedule will begin.</span></span>

        3. <span data-ttu-id="0769f-131">Girin bir **bitiş saati** içinde _ss: dd_ biçimi.</span><span class="sxs-lookup"><span data-stu-id="0769f-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="0769f-132">Merhaba zamanlama durdurur durumdur.</span><span class="sxs-lookup"><span data-stu-id="0769f-132">This is when hello schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="0769f-133">Çakışan zamanlamaları izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="0769f-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="0769f-134">Merhaba başlangıç ve bitiş zamanlarını çakışan bir zamanlamada neden olacak bir hata iletisi toothat efekti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0769f-134">If hello start and end times will result in an overlapping schedule, you will see an error message toothat effect.</span></span>

        4. <span data-ttu-id="0769f-135">Merhaba belirtin **bant genişliği Hızı**.</span><span class="sxs-lookup"><span data-stu-id="0769f-135">Specify hello **Bandwidth Rate**.</span></span> <span data-ttu-id="0769f-136">Merhaba bant genişliği megabit / saniye (Mbps) StorSimple Cihazınızı hello bulut (karşıya ve karşıdan yüklemeleri) ilgili işlemler tarafından kullanılan budur.</span><span class="sxs-lookup"><span data-stu-id="0769f-136">This is hello bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving hello cloud (both uploads and downloads).</span></span> <span data-ttu-id="0769f-137">1 ve bu alan için 1000 arasında bir sayı girin.</span><span class="sxs-lookup"><span data-stu-id="0769f-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![Bant genişliği zamanlamayı tanımlayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="0769f-139">Tümü tamamlanıncaya kadar yukarıdaki adımları toodefine hello birden çok zamanlama şablonunuz için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0769f-139">Repeat hello above steps toodefine multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="0769f-140">Tıklatın **Ekle** toostart bant genişliği şablonu oluşturma.</span><span class="sxs-lookup"><span data-stu-id="0769f-140">Click **Add** toostart creating a bandwidth template.</span></span> <span data-ttu-id="0769f-141">Şablon oluşturulan hello toohello bant genişliği şablonları listesi eklenir.</span><span class="sxs-lookup"><span data-stu-id="0769f-141">hello created template is added toohello list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="0769f-142">Bant genişliği Şablonu Düzenle</span><span class="sxs-lookup"><span data-stu-id="0769f-142">Edit a bandwidth template</span></span>

<span data-ttu-id="0769f-143">Aşağıdaki adımları tooedit bant genişliği şablonu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0769f-143">Perform hello following steps tooedit a bandwidth template.</span></span>

### <a name="tooedit-a-bandwidth-template"></a><span data-ttu-id="0769f-144">tooedit bant genişliği şablonu</span><span class="sxs-lookup"><span data-stu-id="0769f-144">tooedit a bandwidth template</span></span>

1. <span data-ttu-id="0769f-145">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **bant genişliği şablonları**.</span><span class="sxs-lookup"><span data-stu-id="0769f-145">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="0769f-146">Bant genişliği şablonları Hello listesinde toodelete istediğiniz hello şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="0769f-146">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="0769f-147">Sağ tıklayın ve hello bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="0769f-147">Right-click and from hello context menu, select **Delete**.</span></span>
3. <span data-ttu-id="0769f-148">Onayınız istendiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0769f-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="0769f-149">Bu hello bant genişliği şablonu silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-149">This should delete hello bandwidth template.</span></span> 
4. <span data-ttu-id="0769f-150">bant genişliği şablonları listesi Hello tooreflect hello silme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0769f-150">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="0769f-151">Merhaba zamanlama çakışmalar değiştirdiğiniz hello bant genişliği şablonu mevcut bir zamanlamayı ile düzenlerseniz, değişiklikler kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="0769f-151">You cannot save your changes if hello edited schedule overlaps with an existing schedule in hello bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="0769f-152">Bant genişliği Şablonu Sil</span><span class="sxs-lookup"><span data-stu-id="0769f-152">Delete a bandwidth template</span></span>

<span data-ttu-id="0769f-153">Aşağıdaki adımları toodelete bant genişliği şablonu hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0769f-153">Perform hello following steps toodelete a bandwidth template.</span></span>

#### <a name="toodelete-a-bandwidth-template"></a><span data-ttu-id="0769f-154">toodelete bant genişliği şablonu</span><span class="sxs-lookup"><span data-stu-id="0769f-154">toodelete a bandwidth template</span></span>

1. <span data-ttu-id="0769f-155">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **bant genişliği şablonları**.</span><span class="sxs-lookup"><span data-stu-id="0769f-155">Go tooyour StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="0769f-156">Bant genişliği şablonları Hello listesinde toodelete istediğiniz hello şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="0769f-156">In hello list of bandwidth templates, select hello template you wish toodelete.</span></span> <span data-ttu-id="0769f-157">Sağ tıklayın ve Delete hello bağlam menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="0769f-157">Right-click and from hello context menu, select Delete.</span></span>
3. <span data-ttu-id="0769f-158">Onayınız istendiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0769f-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="0769f-159">Bu hello bant genişliği şablonu silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-159">This should delete hello bandwidth template.</span></span>
4. <span data-ttu-id="0769f-160">bant genişliği şablonları listesi Hello tooreflect hello silme güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="0769f-160">hello list of bandwidth templates updates tooreflect hello deletion.</span></span>

<span data-ttu-id="0769f-161">Tüm birimlerin kullanımında Hello şablonu ise, toodelete izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="0769f-161">If hello template is in use by any volume(s), you will not be allowed toodelete it.</span></span> <span data-ttu-id="0769f-162">Merhaba şablon kullanımda belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0769f-162">You will see an error message indicating that hello template is in use.</span></span> <span data-ttu-id="0769f-163">Tüm hello başvuruları toohello şablonu kaldırılması gerektiğini bildiren bir hata iletisi iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="0769f-163">An error message dialog box will appear advising you that all hello references toohello template should be removed.</span></span>

<span data-ttu-id="0769f-164">Merhaba erişerek tüm hello başvuruları toohello şablonunu silebilirsiniz **birim kapsayıcıları** sayfasında ve böylece başka bir şablon kullanın veya bir özel veya sınırsız bant genişliği kullanın, bu şablonu kullanan hello birim kapsayıcıları değiştirme ayar.</span><span class="sxs-lookup"><span data-stu-id="0769f-164">You can delete all hello references toohello template by accessing hello **Volume Containers** page and modifying hello volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="0769f-165">Tüm hello başvuruları kaldırıldıktan sonra hello şablonunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-165">When all hello references have been removed, you can delete hello template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="0769f-166">Varsayılan bant genişliği şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="0769f-166">Use a default bandwidth template</span></span>

<span data-ttu-id="0769f-167">Varsayılan bant genişliği şablonu sağlanır ve birim kapsayıcıları tarafından hello bulut erişirken varsayılan tooenforce bant genişliği denetimleri tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0769f-167">A default bandwidth template is provided and is used by volume containers by default tooenforce bandwidth controls when accessing hello cloud.</span></span> <span data-ttu-id="0769f-168">Hello varsayılan şablonu, ayrıca kullanıcılar kendi şablonlarını oluşturmak için hazır bir başvuru olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="0769f-168">hello default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="0769f-169">Bu varsayılan şablon Hello ayrıntılarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0769f-169">hello details of this default template are:</span></span>

* <span data-ttu-id="0769f-170">**Ad** – sınırsız gece ve hafta sonları</span><span class="sxs-lookup"><span data-stu-id="0769f-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="0769f-171">**Zamanlama** – 8: 00 ve 17: 00 saatleri aygıt saat arasındaki 1 MB/sn bant genişliği oranını geçerlidir Pazartesi tooFriday tek bir zamanlamadan.</span><span class="sxs-lookup"><span data-stu-id="0769f-171">**Schedule** – A single schedule from Monday tooFriday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="0769f-172">Merhaba bant genişliği tooUnlimited hello hafta hello kalanı için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="0769f-172">hello bandwidth is set tooUnlimited for hello remainder of hello week.</span></span>

<span data-ttu-id="0769f-173">Merhaba varsayılan şablonu düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="0769f-173">hello default template can be edited.</span></span> <span data-ttu-id="0769f-174">(düzenlenen sürümleri de dahil olmak üzere) bu şablonu Hello kullanımı izlenir.</span><span class="sxs-lookup"><span data-stu-id="0769f-174">hello usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="0769f-175">Belirli bir zamanda başlatır süren bir bant genişliği şablonu oluştur</span><span class="sxs-lookup"><span data-stu-id="0769f-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="0769f-176">Bu yordam toocreate belirli bir zamanda başlatır ve tüm gün çalışan bir zamanlama izleyin.</span><span class="sxs-lookup"><span data-stu-id="0769f-176">Follow this procedure toocreate a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="0769f-177">Merhaba örnekte hello zamanlama hello sabah içinde 09: 00'dan başlar ve sonraki sabah 09: 00 hello kadar çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="0769f-177">In hello example, hello schedule starts at 9 AM in hello morning and runs until 9 AM hello next morning.</span></span> <span data-ttu-id="0769f-178">Başlangıç hello önemli toonote olduğundan ve bitiş zamanları belirli bir zamanlama için her ikisini de aynı 24 saatlik zamanlama ve birden fazla gün yayılamaz hello üzerinde yer almalıdır.</span><span class="sxs-lookup"><span data-stu-id="0769f-178">It's important toonote that hello start and end times for a given schedule must both be contained on hello same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="0769f-179">Birden çok gün span bant genişliği şablonlarını tooset ihtiyacınız varsa, (Merhaba örnekte gösterildiği gibi) birden çok zamanlama toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-179">If you need tooset up bandwidth templates that span multiple days, you will need toouse multiple schedules (as shown in hello example).</span></span>

#### <a name="toocreate-an-all-day-bandwidth-template"></a><span data-ttu-id="0769f-180">toocreate süren bir bant genişliği şablonu</span><span class="sxs-lookup"><span data-stu-id="0769f-180">toocreate an all-day bandwidth template</span></span>

1. <span data-ttu-id="0769f-181">Merhaba sabah içinde 09: 00'dan başlar ve kadar gece yarısı çalışan bir zamanlama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0769f-181">Create a schedule that starts at 9 AM in hello morning and runs until midnight.</span></span>
2. <span data-ttu-id="0769f-182">Başka bir zamanlama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0769f-182">Add another schedule.</span></span> <span data-ttu-id="0769f-183">09: 00 hello sabah içinde kadar Hello ikinci zamanlama toorun gece yarısına yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0769f-183">Configure hello second schedule toorun from midnight until 9 AM in hello morning.</span></span>
3. <span data-ttu-id="0769f-184">Merhaba bant genişliği şablonu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0769f-184">Save hello bandwidth template.</span></span>

<span data-ttu-id="0769f-185">Merhaba bileşik zamanlama sonra bir zamanda başlatmak ve günlük çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0769f-185">hello composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="0769f-186">Bant genişliği şablonları hakkında sorular ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="0769f-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="0769f-187">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-187">**Q**.</span></span> <span data-ttu-id="0769f-188">Between hello zamanlama toobandwidth denetimleri ne olur?</span><span class="sxs-lookup"><span data-stu-id="0769f-188">What happens toobandwidth controls when you are in between hello schedules?</span></span> <span data-ttu-id="0769f-189">(Bir zamanlama sona erdi ve başka bir henüz başlatılmadı.)</span><span class="sxs-lookup"><span data-stu-id="0769f-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="0769f-190">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-190">**A**.</span></span> <span data-ttu-id="0769f-191">Böyle durumlarda, bant genişliği denetimleri işe.</span><span class="sxs-lookup"><span data-stu-id="0769f-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="0769f-192">Bu, hello aygıt sınırsız bant genişliği veri toohello bulut katmanlandırma olduğunda kullanabileceğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0769f-192">This means that hello device can use unlimited bandwidth when tiering data toohello cloud.</span></span>

<span data-ttu-id="0769f-193">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-193">**Q**.</span></span> <span data-ttu-id="0769f-194">Bant genişliği şablonları çevrimdışı cihazında değişiklik yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="0769f-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="0769f-195">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-195">**A**.</span></span> <span data-ttu-id="0769f-196">Merhaba karşılık gelen cihaz çevrimdışı ise mümkün toomodify bant genişliği şablonları birimleri kapsayıcılarında olmaz.</span><span class="sxs-lookup"><span data-stu-id="0769f-196">You will not be able toomodify bandwidth templates on volumes containers if hello corresponding device is offline.</span></span>

<span data-ttu-id="0769f-197">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-197">**Q**.</span></span> <span data-ttu-id="0769f-198">İlişkili hello birimlerinin çevrimdışı olduğunda bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-198">Can you edit a bandwidth template associated with a volume container when hello associated volumes are offline?</span></span>

<span data-ttu-id="0769f-199">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-199">**A**.</span></span> <span data-ttu-id="0769f-200">Birimleri çevrimdışı bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="0769f-201">Hiçbir veri birimlerinin çevrimdışı olduğunda hello aygıt toohello buluttan katmanlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0769f-201">Note that when volumes are offline, no data will be tiered from hello device toohello cloud.</span></span>

<span data-ttu-id="0769f-202">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-202">**Q**.</span></span> <span data-ttu-id="0769f-203">Varsayılan bir şablon silebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="0769f-203">Can you delete a default template?</span></span>

<span data-ttu-id="0769f-204">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-204">**A**.</span></span> <span data-ttu-id="0769f-205">Varsayılan bir şablon silebilirsiniz rağmen iyi bir fikir toodo şekilde değil.</span><span class="sxs-lookup"><span data-stu-id="0769f-205">Although you can delete a default template, it is not a good idea toodo so.</span></span> <span data-ttu-id="0769f-206">düzenlenen sürümleri de dahil olmak üzere varsayılan bir şablon Hello kullanımı izlenir.</span><span class="sxs-lookup"><span data-stu-id="0769f-206">hello usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="0769f-207">izleme verilerini hello analiz edilir ve zaman hello süresince kullanılan tooimprove hello varsayılan şablonudur.</span><span class="sxs-lookup"><span data-stu-id="0769f-207">hello tracking data is analyzed and over hello course of time, is used tooimprove hello default template.</span></span>

<span data-ttu-id="0769f-208">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-208">**Q**.</span></span> <span data-ttu-id="0769f-209">Bant genişliği şablonlarınızı değiştiren toobe gerektiğini nasıl belirlediğiniz?</span><span class="sxs-lookup"><span data-stu-id="0769f-209">How do you determine that your bandwidth templates need toobe modified?</span></span>

<span data-ttu-id="0769f-210">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-210">**A**.</span></span> <span data-ttu-id="0769f-211">Merhaba başlattığınızda işaretlerini toomodify hello bant genişliği şablonlar ihtiyacınız olan biri hello ağ görmesini yavaşlaması veya bir gün içinde birden çok kez boğma.</span><span class="sxs-lookup"><span data-stu-id="0769f-211">One of hello signs that you need toomodify hello bandwidth templates is when you start seeing hello network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="0769f-212">Bu durumda, hello depolama ve kullanım ağ hello g/ç performans ve ağ üretilen grafikleri bakarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="0769f-212">If this happens, monitor hello storage and usage network by looking at hello I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="0769f-213">Merhaba ağ verimliliği verilerden başlangıç saati belirleyin ve hangi hello ağ sorununu oluşur birim kapsayıcıları hello.</span><span class="sxs-lookup"><span data-stu-id="0769f-213">From hello network throughput data, identify hello time of day and hello volume containers in which hello network bottleneck occurs.</span></span> <span data-ttu-id="0769f-214">Veri Katmanlı toohello bulut yüklenirken bu ortaya çıkarsa (aygıt toocloud için g/ç performans tüm birim kapsayıcıları için bu bilgileri almak,), birim kapsayıcıları ile ilişkili toomodify hello bant genişliği şablonları gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-214">If this happens when data is being tiered toohello cloud (get this information from I/O performance for all volume containers for device toocloud), then you will need toomodify hello bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="0769f-215">Merhaba değiştiren sonra şablonları kullanılıyor, toomonitor hello ağ için önemli gecikmeleri yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-215">After hello modified templates are in use, you will need toomonitor hello network again for significant latencies.</span></span> <span data-ttu-id="0769f-216">Ardından bu hala yoksa, bant genişliği şablonlarınızı toorevisit gerekir.</span><span class="sxs-lookup"><span data-stu-id="0769f-216">If these still exist, then you will need toorevisit your bandwidth templates.</span></span>

<span data-ttu-id="0769f-217">**Q**.</span><span class="sxs-lookup"><span data-stu-id="0769f-217">**Q**.</span></span> <span data-ttu-id="0769f-218">Bu çakışma zamanlar cihazımı üzerinde birden çok birim kapsayıcıları varsa ne olur ancak tooeach farklı sınırlar uygulanır?</span><span class="sxs-lookup"><span data-stu-id="0769f-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply tooeach?</span></span>

<span data-ttu-id="0769f-219">**A**.</span><span class="sxs-lookup"><span data-stu-id="0769f-219">**A**.</span></span> <span data-ttu-id="0769f-220">3 birim kapsayıcıları aygıtla olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0769f-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="0769f-221">Merhaba tamamen Bu kapsayıcılar ile ilişkilendirilmiş zamanlamaları çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="0769f-221">hello schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="0769f-222">Her bu kapsayıcıların kullanılan hello bant genişliği 5, 10 ve 15 Mbps sırasıyla kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="0769f-222">For each of these containers, hello bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="0769f-223">Ne zaman g/ç oluşan tüm bu kapsayıcıların aynı zamanda, hello minimum hello 3 bant genişliği sınırlarının uygulanabilir hello adresindeki: Bu durumda, bu g/ç istekleri paylaşımına giden olarak 5 MB/sn aynı sıra hello.</span><span class="sxs-lookup"><span data-stu-id="0769f-223">When I/O are occurring on all of these containers at hello same time, hello minimum of hello 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share hello same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="0769f-224">Bant genişliği şablonları için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="0769f-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="0769f-225">StorSimple cihazınız için bu en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="0769f-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="0769f-226">Bant genişliği şablonları, aygıt tooenable değişken hello ağ verimliliği hello aygıt tarafından hello günün farklı zamanlarda azaltma üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0769f-226">Configure bandwidth templates on your device tooenable variable throttling of hello network throughput by hello device at different times of hello day.</span></span> <span data-ttu-id="0769f-227">Yedekleme zamanlamaları ile kullanıldığında bu bant genişliği şablonları, yoğun olmayan saatlerde ek ağ bant genişliği bulut işlemleri için etkili bir şekilde yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0769f-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="0769f-228">Hello boyutuna hello dağıtım ve hello gerekli kurtarma süresi hedefi (RTO) göre belirli bir dağıtım için gereken gerçek bant hello hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="0769f-228">Calculate hello actual bandwidth required for a particular deployment based on hello size of hello deployment and hello required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0769f-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0769f-229">Next steps</span></span>

<span data-ttu-id="0769f-230">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0769f-230">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

