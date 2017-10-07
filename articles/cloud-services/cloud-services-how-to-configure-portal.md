---
title: aaaHow tooconfigure bir bulut hizmeti (portal) | Microsoft Docs
description: "Tooconfigure bulut Azure hizmetleri nasıl öğrenin. Uzaktan erişim toorole örnekleri yapılandırmak ve tooupdate hello bulut hizmeti yapılandırması öğrenin. Bu örnekler hello Azure portalını kullanın."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="2c362-105">TooConfigure Cloud Services nasıl</span><span class="sxs-lookup"><span data-stu-id="2c362-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c362-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="2c362-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="2c362-107">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="2c362-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="2c362-108">Hello Azure portalında bir bulut hizmeti için en yaygın olarak kullanılan hello ayarlarını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="2c362-109">Veya tooupdate isterseniz yapılandırma dosyalarını doğrudan bir hizmet yapılandırma dosyası tooupdate indirin ve güncelleştirilmiş hello dosya ve güncelleştirme hello bulut hizmetiyle hello yapılandırma değişiklikleri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2c362-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="2c362-110">Her iki durumda da hello yapılandırma güncelleştirmeleri tooall rol örnekleri atılır.</span><span class="sxs-lookup"><span data-stu-id="2c362-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="2c362-111">Ayrıca hello örneğine, bulut hizmeti rollerinizi ya da Uzak Masaüstü bunları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="2c362-112">Her rol için en az iki rol örneği varsa, azure yalnızca 99,95 yüzde hizmet kullanılabilirliği hello sırasında yapılandırma güncelleştirmeleri emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="2c362-113">Merhaba diğer güncelleştirilirken, bir sanal makine tooprocess istemci isteklerini etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="2c362-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="2c362-114">Daha fazla bilgi için bkz: [hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="2c362-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="2c362-115">Bir bulut hizmeti değiştirme</span><span class="sxs-lookup"><span data-stu-id="2c362-115">Change a cloud service</span></span>
<span data-ttu-id="2c362-116">Açılış hello sonra [Azure portal](https://portal.azure.com/), tooyour bulut hizmetine gidin.</span><span class="sxs-lookup"><span data-stu-id="2c362-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="2c362-117">Buradan, birçok özelliklerini yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="2c362-117">From here, you manage many aspects of it.</span></span>

![Ayarları sayfası](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="2c362-119">Merhaba **ayarları** veya **tüm ayarları** bağlantılar hello açılır **ayarları** hello değiştirebileceğiniz dikey **özellikleri**, hello değiştirme **Yapılandırma**, hello yönetmek **sertifikaları**, Kurulum **uyarı kuralları**ve hello yönetmek **kullanıcılar** kimlerin erişimi Bulut hizmeti toothis.</span><span class="sxs-lookup"><span data-stu-id="2c362-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Azure bulut hizmeti ayarlar dikey penceresi](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="2c362-121">Konuk işletim sistemi sürümü yönetme</span><span class="sxs-lookup"><span data-stu-id="2c362-121">Manage Guest OS version</span></span>

<span data-ttu-id="2c362-122">Varsayılan olarak, Azure konuk işletim sistemi toohello en son desteklenen görüntünüzü Merhaba, hizmet yapılandırma (.cscfg), belirttiğiniz işletim sistemi ailesi içinde düzenli aralıklarla Windows Server 2016 gibi güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="2c362-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="2c362-123">Belirli bir işletim sistemi sürümü tootarget gerekiyorsa, hello ayarlayabilirsiniz **yapılandırma** dikey.</span><span class="sxs-lookup"><span data-stu-id="2c362-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Küme işletim sistemi sürümü](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="2c362-125">Belirli bir işletim sistemi sürümüne otomatik işletim sistemi devre dışı bırakır seçme güncelleştirir ve sizin sorumluluğunuzdadır düzeltme eki uygulama yapar.</span><span class="sxs-lookup"><span data-stu-id="2c362-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="2c362-126">Rolü örneklerinizi güncelleştirmeleri almakta veya uygulama toosecurity açıkları getirebilir emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="2c362-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="2c362-127">İzleme</span><span class="sxs-lookup"><span data-stu-id="2c362-127">Monitoring</span></span>
<span data-ttu-id="2c362-128">Uyarıları tooyour bulut hizmeti ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="2c362-129">Tıklatın **ayarları** > **uyarı kuralları** > **uyarı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2c362-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="2c362-130">Buradan, bir uyarı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-130">From here, you can setup an alert.</span></span> <span data-ttu-id="2c362-131">Merhaba ile **ölçüm** açılan kutusu, veri türleri aşağıdaki hello için uyarı ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c362-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="2c362-132">Disk okuma</span><span class="sxs-lookup"><span data-stu-id="2c362-132">Disk read</span></span>
* <span data-ttu-id="2c362-133">Disk yazma</span><span class="sxs-lookup"><span data-stu-id="2c362-133">Disk write</span></span>
* <span data-ttu-id="2c362-134">Ağ içine</span><span class="sxs-lookup"><span data-stu-id="2c362-134">Network in</span></span>
* <span data-ttu-id="2c362-135">Ağ dışına</span><span class="sxs-lookup"><span data-stu-id="2c362-135">Network out</span></span>
* <span data-ttu-id="2c362-136">CPU yüzdesi</span><span class="sxs-lookup"><span data-stu-id="2c362-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="2c362-137">Bir ölçüm kutucuğunda İzlemeyi Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2c362-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="2c362-138">Kullanmak yerine **ayarları** > **uyarı kuralları**, ölçüm döşemeleri hello hello birinde tıklayabilirsiniz **izleme** hello bölümünü **bulut Hizmet** dikey.</span><span class="sxs-lookup"><span data-stu-id="2c362-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Bulut hizmeti izleme](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="2c362-140">Buradan hello döşeme ile kullanılan hello grafiği özelleştirme veya bir uyarı kuralı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="2c362-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="2c362-141">Yeniden başlatma, yeniden görüntü oluşturma ya da Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="2c362-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="2c362-142">Şu anda Uzak Masaüstü'nü hello kullanarak yapılandıramazsınız **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="2c362-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="2c362-143">Ancak, bunu hello ayarlayabilirsiniz [Klasik Azure portalı](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), aracılığıyla veya [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2c362-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="2c362-144">İlk olarak, hello bulut hizmeti örneğinde'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2c362-144">First, click on hello cloud service instance.</span></span>

![Bulut hizmeti örneği](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="2c362-146">Açılan dikey Hello Uzak Masaüstü bağlantısı başlatmak, uzaktan hello örneğini veya Uzaktan yeniden görüntü oluşturma (Başlangıç yeni bir görüntü ile) Merhaba örneğini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="2c362-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Bulut hizmeti örneği düğmeleri](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="2c362-148">.cscfg yeniden yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2c362-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="2c362-149">Bulut hizmetinizi hello aracılığıyla tooreconfigure gerekebilir [hizmet yapılandırma (cscfg)](cloud-services-model-and-package.md#cscfg) dosyası.</span><span class="sxs-lookup"><span data-stu-id="2c362-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="2c362-150">Öncelikle, .cscfg toodownload gerekir dosya, değiştirin ve sonra bunu yükleyin.</span><span class="sxs-lookup"><span data-stu-id="2c362-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="2c362-151">Tıklatın hello üzerinde **ayarları** simgesini veya hello **tüm ayarları** tooopen hello yukarı bağlantı **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="2c362-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Ayarları sayfası](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="2c362-153">Tıklatın hello üzerinde **yapılandırma** öğesi.</span><span class="sxs-lookup"><span data-stu-id="2c362-153">Click on hello **Configuration** item.</span></span>

    ![Yapılandırma dikey penceresi](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="2c362-155">Tıklatın hello üzerinde **karşıdan** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="2c362-155">Click on hello **Download** button.</span></span>

    ![İndir](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="2c362-157">Hello hizmet yapılandırma dosyası güncelleştirdikten sonra karşıya yükleme ve hello yapılandırma güncelleştirmeleri uygulayın:</span><span class="sxs-lookup"><span data-stu-id="2c362-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Karşıya Yükle](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="2c362-159">Merhaba .cscfg dosyasını tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2c362-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c362-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c362-160">Next steps</span></span>
* <span data-ttu-id="2c362-161">Nasıl çok öğrenin[bir bulut hizmetinin dağıtılacağı](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c362-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="2c362-162">Yapılandırma bir [özel etki alanı adı](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c362-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="2c362-163">[Bulut hizmetinizi yönetme](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c362-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="2c362-164">Yapılandırma [ssl sertifikalarını](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2c362-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
