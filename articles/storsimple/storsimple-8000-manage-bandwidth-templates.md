---
title: "StorSimple 8000 serisi için bant genişliği şablonları yönetme | Microsoft Docs"
description: "Bant genişliği kullanımını denetlemenize izin StorSimple bant genişliği şablonları yönetmek açıklar."
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
ms.openlocfilehash: 50d0a920bef097013feddc828d2c37133b9057b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-manage-storsimple-bandwidth-templates"></a><span data-ttu-id="b7ec7-103">StorSimple bant genişliği şablonları yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="b7ec7-103">Use the StorSimple Device Manager service to manage StorSimple bandwidth templates</span></span>

## <a name="overview"></a><span data-ttu-id="b7ec7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b7ec7-104">Overview</span></span>

<span data-ttu-id="b7ec7-105">Bant genişliği şablonları StorSimple cihaz verileri bulut katmanı için birden çok gün saat zamanlama arasında ağ bant genişliği kullanımını yapılandırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-105">Bandwidth templates allow you to configure network bandwidth usage across multiple time-of-day schedules to tier the data from the StorSimple device to the cloud.</span></span>

<span data-ttu-id="b7ec7-106">Bant genişliği zamanlamaları azaltma ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-106">With bandwidth throttling schedules you can:</span></span>

* <span data-ttu-id="b7ec7-107">İş yükü ağ kullanımları bağlı olarak özelleştirilmiş bant genişliği zamanlamaları belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-107">Specify customized bandwidth schedules depending on the workload network usages.</span></span>
* <span data-ttu-id="b7ec7-108">Yönetim merkezileştirmek ve zamanlamaları birçok cihaz arasında kolay ve sorunsuz bir şekilde yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-108">Centralize management and reuse the schedules across multiple devices in an easy and seamless manner.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ec7-109">Bu özellik yalnızca StorSimple fiziksel cihazlar (modeller 8100 ve 8600) için ve StorSimple bulut cihazları (modeller 8010 hem de 8020) için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-109">This feature is available only for StorSimple physical devices (models 8100 and 8600) and not for StorSimple Cloud Appliances (models 8010 and 8020).</span></span>


## <a name="the-bandwidth-templates-blade"></a><span data-ttu-id="b7ec7-110">Bant genişliği şablonları dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="b7ec7-110">The Bandwidth templates blade</span></span>

<span data-ttu-id="b7ec7-111">**Bant genişliği şablonları** dikey penceresinde tüm bant genişliği şablonları hizmetiniz için bir tablo biçiminde sahip ve aşağıdaki bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-111">The **Bandwidth templates** blade has all the bandwidth templates for your service in a tabular format, and contains the following information:</span></span>

* <span data-ttu-id="b7ec7-112">**Ad** – oluşturulduğunda atanan bant genişliği şablonu için benzersiz bir ad.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-112">**Name** – A unique name assigned to the bandwidth template when it was created.</span></span>
* <span data-ttu-id="b7ec7-113">**Zamanlama** – verilen bant genişliği şablonundaki zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-113">**Schedule** – The number of schedules contained in a given bandwidth template.</span></span>
* <span data-ttu-id="b7ec7-114">**Tarafından kullanılan** – bant genişliği şablonları kullanarak birimlerin sayısı.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-114">**Used by** – The number of volumes using the bandwidth templates.</span></span>

<span data-ttu-id="b7ec7-115">Bant genişliği şablonlarını yapılandırmanıza yardımcı olacak ek bilgiler de bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-115">You can also find additional information to help configure bandwidth templates in:</span></span>

* [<span data-ttu-id="b7ec7-116">Bant genişliği şablonları hakkında sorular ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="b7ec7-116">Questions and answers about bandwidth templates</span></span>](#questions-and-answers-about-bandwidth-templates)
* [<span data-ttu-id="b7ec7-117">Bant genişliği şablonları için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="b7ec7-117">Best practices for bandwidth templates</span></span>](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a><span data-ttu-id="b7ec7-118">Bant genişliği şablonu ekleyin</span><span class="sxs-lookup"><span data-stu-id="b7ec7-118">Add a bandwidth template</span></span>

<span data-ttu-id="b7ec7-119">Yeni bir bant genişliği şablonu oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-119">Perform the following steps to create a new bandwidth template.</span></span>

#### <a name="to-add-a-bandwidth-template"></a><span data-ttu-id="b7ec7-120">Bant genişliği şablonu eklemek için</span><span class="sxs-lookup"><span data-stu-id="b7ec7-120">To add a bandwidth template</span></span>

1. <span data-ttu-id="b7ec7-121">StorSimple cihaz Yöneticisi hizmetinize gidin, tıklatın **bant genişliği şablonları** ve ardından **+ Ekle bant genişliği şablonu**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-121">Go to your StorSimple Device Manager service, click **Bandwidth templates** and then click **+ Add Bandwidth template**.</span></span>

    ![Bant genişliği şablonu ekleyin + tıklayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. <span data-ttu-id="b7ec7-123">İçinde **bant genişliği şablonu Ekle** dikey penceresinde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-123">In the **Add bandwidth template** blade, do the following steps:</span></span>
   
    1. <span data-ttu-id="b7ec7-124">Bant genişliği şablonu için benzersiz bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-124">Specify a unique name for your bandwidth template.</span></span>
    2. <span data-ttu-id="b7ec7-125">Bir bant genişliği zamanlama tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-125">Define a bandwidth schedule.</span></span> <span data-ttu-id="b7ec7-126">Bir zamanlama oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-126">To create a schedule:</span></span>
   
        1. <span data-ttu-id="b7ec7-127">Aşağı açılan listeden seçin **gün** haftası zamanlama için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-127">From the drop-down list, choose the **Days** of the week the schedule is configured for.</span></span> <span data-ttu-id="b7ec7-128">Birden fazla gün seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-128">You can select multiple days.</span></span>        
        
        2. <span data-ttu-id="b7ec7-129">Girin bir **başlangıç saati** içinde _ss: dd_ biçimi.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-129">Enter a **Start Time** in _hh:mm_ format.</span></span> <span data-ttu-id="b7ec7-130">Bu zamanlamanın başlayacağı durumunda olur.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-130">This is when the schedule will begin.</span></span>

        3. <span data-ttu-id="b7ec7-131">Girin bir **bitiş saati** içinde _ss: dd_ biçimi.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-131">Enter an **End Time** in _hh:mm_ format.</span></span> <span data-ttu-id="b7ec7-132">Bu zamanlamayı durdurur durumunda olur.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-132">This is when the schedule will stop.</span></span>
      
           > [!NOTE]
           > <span data-ttu-id="b7ec7-133">Çakışan zamanlamaları izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-133">Overlapping schedules are not allowed.</span></span> <span data-ttu-id="b7ec7-134">Başlangıç ve bitiş zamanlarını çakışan bir zamanlamada neden olur, bunu belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-134">If the start and end times will result in an overlapping schedule, you will see an error message to that effect.</span></span>

        4. <span data-ttu-id="b7ec7-135">Belirtin **bant genişliği Hızı**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-135">Specify the **Bandwidth Rate**.</span></span> <span data-ttu-id="b7ec7-136">Megabit / saniye (Mbps) StorSimple Cihazınızı (karşıya ve karşıdan yüklemeleri) bulut ilgili işlemler tarafından kullanılan bant genişliği budur.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-136">This is the bandwidth in Megabits per second (Mbps) used by your StorSimple device in operations involving the cloud (both uploads and downloads).</span></span> <span data-ttu-id="b7ec7-137">1 ve bu alan için 1000 arasında bir sayı girin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-137">Supply a number between 1 and 1,000 for this field.</span></span>

            ![Bant genişliği zamanlamayı tanımlayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            <span data-ttu-id="b7ec7-139">Tümü tamamlanıncaya kadar şablonunuz için birden çok zamanlamaları tanımlamak için yukarıdaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-139">Repeat the above steps to define multiple schedules for your template until you are done.</span></span>

        5. <span data-ttu-id="b7ec7-140">Tıklatın **Ekle** bant genişliği şablonu oluşturmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-140">Click **Add** to start creating a bandwidth template.</span></span> <span data-ttu-id="b7ec7-141">Oluşturulan şablon bant genişliği şablonları listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-141">The created template is added to the list of bandwidth templates.</span></span>
      

## <a name="edit-a-bandwidth-template"></a><span data-ttu-id="b7ec7-142">Bant genişliği Şablonu Düzenle</span><span class="sxs-lookup"><span data-stu-id="b7ec7-142">Edit a bandwidth template</span></span>

<span data-ttu-id="b7ec7-143">Bant genişliği şablonu düzenlemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-143">Perform the following steps to edit a bandwidth template.</span></span>

### <a name="to-edit-a-bandwidth-template"></a><span data-ttu-id="b7ec7-144">Bant genişliği şablonu düzenlemek için</span><span class="sxs-lookup"><span data-stu-id="b7ec7-144">To edit a bandwidth template</span></span>

1. <span data-ttu-id="b7ec7-145">' I tıklatın ve StorSimple cihaz yöneticinize hizmeti Git **bant genişliği şablonları**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-145">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="b7ec7-146">Bant genişliği şablonları listesinde silmek istediğiniz şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-146">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="b7ec7-147">Sağ tıklayın ve bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-147">Right-click and from the context menu, select **Delete**.</span></span>
3. <span data-ttu-id="b7ec7-148">Onayınız istendiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-148">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="b7ec7-149">Bu, bant genişliği şablonu silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-149">This should delete the bandwidth template.</span></span> 
4. <span data-ttu-id="b7ec7-150">Silme işlemini yansıtmak için bant genişliği şablonları güncelleştirmeleri listesi.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-150">The list of bandwidth templates updates to reflect the deletion.</span></span>

> [!NOTE]
> <span data-ttu-id="b7ec7-151">Düzenlenen zamanlama değiştirdiğiniz bant genişliği şablonu mevcut bir zamanlamayı ile çakışırsa, değişiklikler kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-151">You cannot save your changes if the edited schedule overlaps with an existing schedule in the bandwidth template that you are modifying.</span></span>

## <a name="delete-a-bandwidth-template"></a><span data-ttu-id="b7ec7-152">Bant genişliği Şablonu Sil</span><span class="sxs-lookup"><span data-stu-id="b7ec7-152">Delete a bandwidth template</span></span>

<span data-ttu-id="b7ec7-153">Bant genişliği şablonu silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-153">Perform the following steps to delete a bandwidth template.</span></span>

#### <a name="to-delete-a-bandwidth-template"></a><span data-ttu-id="b7ec7-154">Bant genişliği şablonu silmek için</span><span class="sxs-lookup"><span data-stu-id="b7ec7-154">To delete a bandwidth template</span></span>

1. <span data-ttu-id="b7ec7-155">' I tıklatın ve StorSimple cihaz yöneticinize hizmeti Git **bant genişliği şablonları**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-155">Go to your StorSimple Device Manager service and click **Bandwidth templates**.</span></span>
2. <span data-ttu-id="b7ec7-156">Bant genişliği şablonları listesinde silmek istediğiniz şablonu seçin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-156">In the list of bandwidth templates, select the template you wish to delete.</span></span> <span data-ttu-id="b7ec7-157">Sağ tıklatın ve bağlam menüsünden Sil'i seçin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-157">Right-click and from the context menu, select Delete.</span></span>
3. <span data-ttu-id="b7ec7-158">Onayınız istendiğinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-158">When prompted for confirmation, click **OK**.</span></span> <span data-ttu-id="b7ec7-159">Bu, bant genişliği şablonu silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-159">This should delete the bandwidth template.</span></span>
4. <span data-ttu-id="b7ec7-160">Silme işlemini yansıtmak için bant genişliği şablonları güncelleştirmeleri listesi.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-160">The list of bandwidth templates updates to reflect the deletion.</span></span>

<span data-ttu-id="b7ec7-161">Şablon tüm birimlerin tarafından kullanılıyorsa, silmeden verilmez.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-161">If the template is in use by any volume(s), you will not be allowed to delete it.</span></span> <span data-ttu-id="b7ec7-162">Şablon kullanımda olduğunu belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-162">You will see an error message indicating that the template is in use.</span></span> <span data-ttu-id="b7ec7-163">Şablona yapılan tüm başvuruları kaldırılması gerektiğini bildiren bir hata iletisi iletişim kutusu görünür.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-163">An error message dialog box will appear advising you that all the references to the template should be removed.</span></span>

<span data-ttu-id="b7ec7-164">Şablona yapılan tüm başvuruları erişerek silebilirsiniz **birim kapsayıcıları** sayfa ve böylece başka bir şablon kullanın veya bir özel veya sınırsız bant genişliği ayarı kullanın, bu şablonu kullanan birim kapsayıcıları değiştirme.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-164">You can delete all the references to the template by accessing the **Volume Containers** page and modifying the volume containers that use this template so that they use another template or use a custom or unlimited bandwidth setting.</span></span> <span data-ttu-id="b7ec7-165">Tüm başvuruları kaldırıldıktan sonra şablonu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-165">When all the references have been removed, you can delete the template.</span></span>

## <a name="use-a-default-bandwidth-template"></a><span data-ttu-id="b7ec7-166">Varsayılan bant genişliği şablonu kullanın</span><span class="sxs-lookup"><span data-stu-id="b7ec7-166">Use a default bandwidth template</span></span>

<span data-ttu-id="b7ec7-167">Varsayılan bant genişliği şablonu sağlanır ve birim kapsayıcıları tarafından bulut erişirken bant genişliği denetimleri zorlamak için varsayılan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-167">A default bandwidth template is provided and is used by volume containers by default to enforce bandwidth controls when accessing the cloud.</span></span> <span data-ttu-id="b7ec7-168">Varsayılan şablonu, aynı zamanda kullanıcılar kendi şablonlarını oluşturmak için hazır bir başvuru olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-168">The default template also serves as a ready reference for users who create their own templates.</span></span> <span data-ttu-id="b7ec7-169">Bu varsayılan şablon ayrıntılarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-169">The details of this default template are:</span></span>

* <span data-ttu-id="b7ec7-170">**Ad** – sınırsız gece ve hafta sonları</span><span class="sxs-lookup"><span data-stu-id="b7ec7-170">**Name** – Unlimited nights and weekends</span></span>
* <span data-ttu-id="b7ec7-171">**Zamanlama** – Pazartesi'den tek bir zamanlama Cuma 8: 00 ve 17: 00 saatleri aygıt saat arasındaki 1 MB/sn bant genişliği oranını uygular.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-171">**Schedule** – A single schedule from Monday to Friday that applies a bandwidth rate of 1 Mbps between 8 AM and 5 PM device time.</span></span> <span data-ttu-id="b7ec7-172">Bant genişliği için sınırsız hafta geri kalanı için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-172">The bandwidth is set to Unlimited for the remainder of the week.</span></span>

<span data-ttu-id="b7ec7-173">Varsayılan şablonu düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-173">The default template can be edited.</span></span> <span data-ttu-id="b7ec7-174">Bu şablon (düzenlenen sürümleri de dahil olmak üzere) kullanımını izlenir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-174">The usage of this template (including edited versions) is tracked.</span></span>

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a><span data-ttu-id="b7ec7-175">Belirli bir zamanda başlatır süren bir bant genişliği şablonu oluştur</span><span class="sxs-lookup"><span data-stu-id="b7ec7-175">Create an all-day bandwidth template that starts at a specified time</span></span>

<span data-ttu-id="b7ec7-176">Belirli bir zamanda başlatır ve tüm gün çalışan bir zamanlama oluşturmak için bu yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-176">Follow this procedure to create a schedule that starts at a specified time and runs all day.</span></span> <span data-ttu-id="b7ec7-177">Örnekte, zamanlama içinde sabah 09: 00'dan başlar ve 09: 00 kadar sonraki sabah çalışır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-177">In the example, the schedule starts at 9 AM in the morning and runs until 9 AM the next morning.</span></span> <span data-ttu-id="b7ec7-178">Belirli bir zamanlama için başlangıç ve bitiş zamanları her ikisi de aynı 24 saatlik zaman çizelgesine göre bulunmalıdır ve birden fazla gün yayılamaz dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-178">It's important to note that the start and end times for a given schedule must both be contained on the same 24 hour schedule and cannot span multiple days.</span></span> <span data-ttu-id="b7ec7-179">Birden çok gün yayılan bant genişliği şablonları ayarlamak gerekiyorsa, birden çok zamanlama (örnekte gösterildiği gibi) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-179">If you need to set up bandwidth templates that span multiple days, you will need to use multiple schedules (as shown in the example).</span></span>

#### <a name="to-create-an-all-day-bandwidth-template"></a><span data-ttu-id="b7ec7-180">Günlük bir bant genişliği şablonu oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="b7ec7-180">To create an all-day bandwidth template</span></span>

1. <span data-ttu-id="b7ec7-181">Sabah, 09: 00'dan başlar ve kadar gece yarısı çalışan bir zamanlama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-181">Create a schedule that starts at 9 AM in the morning and runs until midnight.</span></span>
2. <span data-ttu-id="b7ec7-182">Başka bir zamanlama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-182">Add another schedule.</span></span> <span data-ttu-id="b7ec7-183">09: 00 sabah içinde kadar gece çalıştırmak için ikinci zamanlamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-183">Configure the second schedule to run from midnight until 9 AM in the morning.</span></span>
3. <span data-ttu-id="b7ec7-184">Bant genişliği şablonu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-184">Save the bandwidth template.</span></span>

<span data-ttu-id="b7ec7-185">Bileşik zamanlama sonra bir zamanda başlatmak ve günlük çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-185">The composite schedule will then start at a time of your choosing and run all-day.</span></span>

## <a name="questions-and-answers-about-bandwidth-templates"></a><span data-ttu-id="b7ec7-186">Bant genişliği şablonları hakkında sorular ve yanıtlar</span><span class="sxs-lookup"><span data-stu-id="b7ec7-186">Questions and answers about bandwidth templates</span></span>

<span data-ttu-id="b7ec7-187">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-187">**Q**.</span></span> <span data-ttu-id="b7ec7-188">Between zamanlama bant genişliği denetimleri için ne olur?</span><span class="sxs-lookup"><span data-stu-id="b7ec7-188">What happens to bandwidth controls when you are in between the schedules?</span></span> <span data-ttu-id="b7ec7-189">(Bir zamanlama sona erdi ve başka bir henüz başlatılmadı.)</span><span class="sxs-lookup"><span data-stu-id="b7ec7-189">(A schedule has ended and another one has not started yet.)</span></span>

<span data-ttu-id="b7ec7-190">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-190">**A**.</span></span> <span data-ttu-id="b7ec7-191">Böyle durumlarda, bant genişliği denetimleri işe.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-191">In such cases, no bandwidth controls will be employed.</span></span> <span data-ttu-id="b7ec7-192">Bu cihaz verileri buluta katmanlama zaman sınırsız bant genişliği olarak kullanabileceğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-192">This means that the device can use unlimited bandwidth when tiering data to the cloud.</span></span>

<span data-ttu-id="b7ec7-193">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-193">**Q**.</span></span> <span data-ttu-id="b7ec7-194">Bant genişliği şablonları çevrimdışı cihazında değişiklik yapabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="b7ec7-194">Can you modify bandwidth templates on an offline device?</span></span>

<span data-ttu-id="b7ec7-195">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-195">**A**.</span></span> <span data-ttu-id="b7ec7-196">Karşılık gelen cihaz çevrimdışı ise birimleri kapsayıcılarında bant genişliği şablonları değiştirmek mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-196">You will not be able to modify bandwidth templates on volumes containers if the corresponding device is offline.</span></span>

<span data-ttu-id="b7ec7-197">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-197">**Q**.</span></span> <span data-ttu-id="b7ec7-198">İlişkili birimler çevrimdışı olduğunda bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-198">Can you edit a bandwidth template associated with a volume container when the associated volumes are offline?</span></span>

<span data-ttu-id="b7ec7-199">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-199">**A**.</span></span> <span data-ttu-id="b7ec7-200">Birimleri çevrimdışı bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-200">You can modify a bandwidth template associated with a volume container whose volumes are offline.</span></span> <span data-ttu-id="b7ec7-201">Birimlerinin çevrimdışı olduğunda, hiçbir veri CİHAZDAN buluta katmanlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-201">Note that when volumes are offline, no data will be tiered from the device to the cloud.</span></span>

<span data-ttu-id="b7ec7-202">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-202">**Q**.</span></span> <span data-ttu-id="b7ec7-203">Varsayılan bir şablon silebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="b7ec7-203">Can you delete a default template?</span></span>

<span data-ttu-id="b7ec7-204">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-204">**A**.</span></span> <span data-ttu-id="b7ec7-205">Varsayılan bir şablon silebilirsiniz rağmen Bunu yapmak için iyi bir fikir değil.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-205">Although you can delete a default template, it is not a good idea to do so.</span></span> <span data-ttu-id="b7ec7-206">Düzenlenen sürümleri de dahil olmak üzere varsayılan bir şablon kullanımı izlenir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-206">The usage of a default template, including edited versions, is tracked.</span></span> <span data-ttu-id="b7ec7-207">İzleme verilerini analiz edilir ve süresi boyunca varsayılan şablonu geliştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-207">The tracking data is analyzed and over the course of time, is used to improve the default template.</span></span>

<span data-ttu-id="b7ec7-208">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-208">**Q**.</span></span> <span data-ttu-id="b7ec7-209">Bant genişliği şablonlarınızı değiştirilmesi gereken nasıl belirlediğiniz?</span><span class="sxs-lookup"><span data-stu-id="b7ec7-209">How do you determine that your bandwidth templates need to be modified?</span></span>

<span data-ttu-id="b7ec7-210">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-210">**A**.</span></span> <span data-ttu-id="b7ec7-211">Ağ yavaşlayabilir veya bir gün içinde birden çok kez boğma görmesini başlattığınızda bant genişliği şablonları değiştirmenize gerek işaretlerini biridir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-211">One of the signs that you need to modify the bandwidth templates is when you start seeing the network slow down or choke multiple times in a day.</span></span> <span data-ttu-id="b7ec7-212">Bu durumda, depolama ve kullanım ağ g/ç performans ve ağ üretilen grafikleri bakarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-212">If this happens, monitor the storage and usage network by looking at the I/O Performance and Network Throughput charts.</span></span>

<span data-ttu-id="b7ec7-213">Ağ verimliliği verilerden günün saati ve ağ sorununu oluştuğu birim kapsayıcıları tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-213">From the network throughput data, identify the time of day and the volume containers in which the network bottleneck occurs.</span></span> <span data-ttu-id="b7ec7-214">Verileri buluta katmanlı olduğunda bu ortaya çıkarsa (g/ç performans bulut cihaz için tüm birim kapsayıcıları için bu bilgileri Al), sonra da, birim kapsayıcıları ile ilişkili bant genişliği şablonları değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-214">If this happens when data is being tiered to the cloud (get this information from I/O performance for all volume containers for device to cloud), then you will need to modify the bandwidth templates associated with your volume containers.</span></span>

<span data-ttu-id="b7ec7-215">Değiştirilen şablonlar kullanımda olan sonra önemli gecikme için tekrar izlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-215">After the modified templates are in use, you will need to monitor the network again for significant latencies.</span></span> <span data-ttu-id="b7ec7-216">Bunlar hala yoksa, bant genişliği şablonlarınızı yeniden ziyaret etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-216">If these still exist, then you will need to revisit your bandwidth templates.</span></span>

<span data-ttu-id="b7ec7-217">**Q**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-217">**Q**.</span></span> <span data-ttu-id="b7ec7-218">Bu çakışma zamanlar cihazımı üzerinde birden çok birim kapsayıcıları varsa ne olur, ancak farklı sınırlar her birine uygulanan?</span><span class="sxs-lookup"><span data-stu-id="b7ec7-218">What happens if multiple volume containers on my device have schedules that overlap but different limits apply to each?</span></span>

<span data-ttu-id="b7ec7-219">**A**.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-219">**A**.</span></span> <span data-ttu-id="b7ec7-220">3 birim kapsayıcıları aygıtla olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-220">Let's assume that you have a device with 3 volume containers.</span></span> <span data-ttu-id="b7ec7-221">Bu kapsayıcılar ile tamamen ilişkilendirilmiş zamanlamaları çakışıyor.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-221">The schedules associated with these containers completely overlap.</span></span> <span data-ttu-id="b7ec7-222">Her Bu kapsayıcıları için kullanılan bant genişliği 5, 10 ve 15 Mbps sırasıyla kısıtlamalardır.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-222">For each of these containers, the bandwidth limits used are 5, 10, and 15 Mbps respectively.</span></span> <span data-ttu-id="b7ec7-223">G/ç oluşan, tüm bu kapsayıcıların aynı anda en az 3 bant genişliği sınırlarının uygulanabilir: Bu durumda, bu g/ç istekleri giden olarak 5 MB/sn aynı sıraya paylaşın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-223">When I/O are occurring on all of these containers at the same time, the minimum of the 3 bandwidth limits may be applied: in this case, 5 Mbps as these outgoing I/O requests share the same queue.</span></span>

## <a name="best-practices-for-bandwidth-templates"></a><span data-ttu-id="b7ec7-224">Bant genişliği şablonları için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="b7ec7-224">Best practices for bandwidth templates</span></span>

<span data-ttu-id="b7ec7-225">StorSimple cihazınız için bu en iyi uygulamaları izleyin:</span><span class="sxs-lookup"><span data-stu-id="b7ec7-225">Follow these best practices for your StorSimple device:</span></span>

* <span data-ttu-id="b7ec7-226">Bant genişliği şablonları değişken ağ verimliliği aygıt tarafından günün farklı zamanlarda azaltmayı etkinleştirmek için Cihazınızı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-226">Configure bandwidth templates on your device to enable variable throttling of the network throughput by the device at different times of the day.</span></span> <span data-ttu-id="b7ec7-227">Yedekleme zamanlamaları ile kullanıldığında bu bant genişliği şablonları, yoğun olmayan saatlerde ek ağ bant genişliği bulut işlemleri için etkili bir şekilde yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-227">These bandwidth templates when used with backup schedules can effectively leverage additional network bandwidth for cloud operations during off-peak hours.</span></span>
* <span data-ttu-id="b7ec7-228">Dağıtım ve gerekli kurtarma süresi hedefi (RTO) boyutuna göre belirli bir dağıtım için gereken gerçek bant hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="b7ec7-228">Calculate the actual bandwidth required for a particular deployment based on the size of the deployment and the required recovery time objective (RTO).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7ec7-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7ec7-229">Next steps</span></span>

<span data-ttu-id="b7ec7-230">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b7ec7-230">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

