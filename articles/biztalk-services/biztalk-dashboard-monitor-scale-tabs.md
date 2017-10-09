---
title: "aaaDashboard, monitör, Ölçek, yapılandırma ve karma bağlantılar BizTalk Services | Microsoft Docs"
description: "Merhaba denetimleri hakkında bilgi edinin ve izleme hello Klasik portal sekmelerde performans için BizTalk Services: pano, İzleyici, Ölçek, yapılandırma ve karma bağlantılar. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="adcde-104">Merhaba Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="adcde-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="adcde-105">BizTalk hizmeti oluşturma ve uygulamanızı dağıttıktan sonra bazı hello BizTalk hizmeti ayarlarını değiştirin ve hello uygulama performansı izleme.</span><span class="sxs-lookup"><span data-stu-id="adcde-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="adcde-106">Merhaba Klasik Azure portalını açtığınızda, başlangıç sırasında otomatik olarak yerleştirilir **tüm öğeleri** sekmesini tooview BizTalk hizmetinizi seçin, BizTalk hizmetinize hello **tüm öğeleri** sekme veya select hello **BIZTALK SERVICES** sekmesinde; ve ardından, BizTalk hizmeti adını seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="adcde-107">Bu sekme aşağıdaki hello ile yeni bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="adcde-108">Bu konuda aşağıdaki sekmelerden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="adcde-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="adcde-109">Hızlı Başlangıç)</span><span class="sxs-lookup"><span data-stu-id="adcde-109">Quickstart (</span></span>![Hızlı Başlangıç][Quickstart]<span data-ttu-id="adcde-111">)</span><span class="sxs-lookup"><span data-stu-id="adcde-111">)</span></span>
<span data-ttu-id="adcde-112">Merhaba BizTalk Services sürümüne bağlı olarak listelenen tüm seçenekleri kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="adcde-113"><strong>Merhaba araçları edinin</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="adcde-114">Şirket içi geliştirme bilgisayarınızda Hello BizTalk Services SDK'sı tooinstall hello Visual Studio Proje şablonları indirin.</span><span class="sxs-lookup"><span data-stu-id="adcde-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="adcde-115">Bu şablonlar hello oluşturma <strong>BizTalk Services</strong> (köprü) ve hello <strong>BizTalk hizmeti yapıları</strong> dağıtılan tooyour BizTalk hizmeti olan (dönüştürme) Visual Studio projeleri.</span><span class="sxs-lookup"><span data-stu-id="adcde-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="adcde-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Ne ı Başlat kullanarak hello Azure BizTalk Services SDK'sı </a> ve <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">yükleme hello Azure BizTalk Services SDK'sı</a> listeleri hello adımları tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="adcde-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="adcde-117"><strong>İş ortağı anlaşmaları oluşturma</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="adcde-118">Açılır hello Azure BizTalk Services burada ortakları ekleme ve X12, AS2, oluşturma Azure üzerinde barındırılan portalı ve EDIFACT EDI sözleşmeleri.</span><span class="sxs-lookup"><span data-stu-id="adcde-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="adcde-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> listeleri hello adımları tooget başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="adcde-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="adcde-120"><strong>BizTalk hizmetleri hakkında daha fazla bilgi edinin</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="adcde-121">Toohello Git <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">center öğrenme</a> toolearn Azure BizTalk Services hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="adcde-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="adcde-122">Merhaba görev çubuğunda hello altta, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adcde-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="adcde-123"><strong>Yönetme</strong> , uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="adcde-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="adcde-124">Hello Azure BizTalk Services portalı açar.</span><span class="sxs-lookup"><span data-stu-id="adcde-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="adcde-125">Merhaba BizTalk Services portalı olan iş ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere, hello giriş tooEDI yapılandırma ve EDIFACT sözleşmelerini.</span><span class="sxs-lookup"><span data-stu-id="adcde-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="adcde-126">Bu olduğu hello aynı <strong>ortak sözleşmeleri oluşturmak</strong> hello üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.</span><span class="sxs-lookup"><span data-stu-id="adcde-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="adcde-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> hello BizTalk Services Portal hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="adcde-128"><strong>Bağlantı bilgilerini</strong> hello erişim denetimi Namespace,</span><span class="sxs-lookup"><span data-stu-id="adcde-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="adcde-129">Bağlantı bilgilerini seçtiğinizde, erişim denetimi Namespace, varsayılan, veren hello ve varsayılan anahtar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adcde-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="adcde-130">Bu değerleri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="adcde-131">Merhaba erişim denetimi portalı da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="adcde-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Erişim denetimi Namespace oluşturmak</a> hello erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="adcde-133"><strong>Eşitleme anahtarları</strong> hello depolama hesabı,</span><span class="sxs-lookup"><span data-stu-id="adcde-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="adcde-134">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="adcde-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="adcde-135">Bu şifreleme anahtarları erişim tooyour depolama hesabı denetler.</span><span class="sxs-lookup"><span data-stu-id="adcde-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="adcde-136">BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="adcde-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="adcde-137"><strong>Eşitleme anahtarları</strong> hello BizTalk hizmeti kesintiye uğratmadan hello birincil anahtar hello ikincil anahtar arasındaki kullanıcılar tooswitch etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="adcde-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="adcde-138">Örneğin, BizTalk hizmeti toouse hello depolama hesabı için yeni bir birincil anahtar hello istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="adcde-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="adcde-139">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="adcde-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="adcde-140">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="adcde-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="adcde-141">Merhaba ikincil anahtarı seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-141">Select hello Secondary Key.</span></span> <span data-ttu-id="adcde-142">Bunu yaptığınızda hello BizTalk hizmeti hello ikincil anahtarı kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="adcde-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="adcde-143">Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello birincil anahtarı yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="adcde-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="adcde-144">BizTalk hizmetinizi hello ikincil anahtarı kullanarak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="adcde-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="adcde-145">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="adcde-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="adcde-146">Şimdi, hello birincil anahtarı seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="adcde-147">Bu olduğu hello yeni birincil anahtar, yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="adcde-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="adcde-148">Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello ikincil anahtarını yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="adcde-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="adcde-149">Bu işlem, "rollover anahtarları" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-149">This process is called "rollover keys".</span></span> <span data-ttu-id="adcde-150">Merhaba tooenable kullanıcılar tooswitch hello birincil anahtar ve ikincil anahtar hello arasında hello BizTalk hizmeti kesintiye uğratmadan amaçtır.</span><span class="sxs-lookup"><span data-stu-id="adcde-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="adcde-151"><strong>Silme</strong> uygulamanız</span><span class="sxs-lookup"><span data-stu-id="adcde-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="adcde-152">Seçtiğinizde silin, BizTalk hizmeti ve tüm öğeleri dağıtılan tooit kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="adcde-153">Pano</span><span class="sxs-lookup"><span data-stu-id="adcde-153">Dashboard</span></span>
<span data-ttu-id="adcde-154">Merhaba BizTalk Services sürümüne bağlı olarak listelenen tüm seçenekleri kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="adcde-155">BizTalk hizmet adınızı seçin, hello Pano sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adcde-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="adcde-156">Panosunda, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adcde-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="adcde-157">Kullanıma genel bakış: kullanılan karma bağlantılar hello sayısını gösterir</span><span class="sxs-lookup"><span data-stu-id="adcde-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="adcde-158">Ayrıca hello veri kullanımı GB cinsinden görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="adcde-159">Ölçüm grafiği: performans ölçümleri sabit bir listesini gösterir</span><span class="sxs-lookup"><span data-stu-id="adcde-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="adcde-160">Bu ölçümler hello durumunu hello BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="adcde-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="adcde-161">Merhaba de seçebilirsiniz **göreli** veya **mutlak** değerleri ve hello zaman aralığı **aralığı** hello grafiğinde görüntülenen hello ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="adcde-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="adcde-162">Bu performans ölçümleri açıklaması için çok Git[kullanılabilir ölçümler](#Metrics) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="adcde-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="adcde-163">Hızlı Bakış: BizTalk hizmeti özelliklerinizi listeler</span><span class="sxs-lookup"><span data-stu-id="adcde-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="adcde-164"><strong>İzleme veritabanı kimlik bilgileri güncelleştir</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="adcde-165">Kullanıcı adı değişiklikleri hello ve izleme veritabanı hello toolog kullanılan parolayı.</span><span class="sxs-lookup"><span data-stu-id="adcde-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-166"><strong>SSL sertifikasını güncelleştir</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="adcde-167">Merhaba BizTalk hizmeti toouse farklı bir SSL sertifikası güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="adcde-168">Otomatik olarak imzalanan bir SSL sertifikası otomatik olarak oluşturulur, <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">hello BizTalk hizmeti oluşturma</a>.</span><span class="sxs-lookup"><span data-stu-id="adcde-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-169"><strong>Sertifikayı indirin</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="adcde-170">BizTalk hizmeti tooa yerel makinenize tarafından kullanılan hello SSL sertifikası yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-171"><strong>Durumu</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="adcde-172">Merhaba, BizTalk hizmetinin geçerli durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="adcde-173">Bkz: <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Hizmet durumu grafiği</a>.</span><span class="sxs-lookup"><span data-stu-id="adcde-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="adcde-174"><strong>Hizmet URL'si</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="adcde-175">BizTalk hizmeti başlangıç URL'si.</span><span class="sxs-lookup"><span data-stu-id="adcde-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="adcde-176">Bu olduğu hello aynı hello <strong>etki alanı URL'si</strong> BizTalk hizmeti oluşturulduğunda girildi.</span><span class="sxs-lookup"><span data-stu-id="adcde-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-177"><strong>Genel sanal IP (VIP) adresi</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="adcde-178">Başlangıç IP adresi tooyour BizTalk hizmeti atanır.</span><span class="sxs-lookup"><span data-stu-id="adcde-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="adcde-179">Tüm giriş uç noktaları için kullanılır ve giden trafiği hello kaynak adresidir.</span><span class="sxs-lookup"><span data-stu-id="adcde-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="adcde-180">Oluşturulan sürece bu IP adresi tooyour BizTalk hizmeti aittir.</span><span class="sxs-lookup"><span data-stu-id="adcde-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="adcde-181">Hello BizTalk hizmeti silerseniz, başlangıç IP adresi tooanother BizTalk hizmeti atanır.</span><span class="sxs-lookup"><span data-stu-id="adcde-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-182"><strong>ACS Namespace</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="adcde-183">BizTalk hizmeti Hello ile kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="adcde-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-184"><strong>Sürüm</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="adcde-185">Merhaba BizTalk hizmeti oluşturulduğunda Edition girilen hello listeler.</span><span class="sxs-lookup"><span data-stu-id="adcde-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-186"><strong>Konum</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="adcde-187">Görüntüler, BizTalk hizmeti barındıran coğrafi bölge hello.</span><span class="sxs-lookup"><span data-stu-id="adcde-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-188"><strong>Oluşturulan</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="adcde-189">Tarih ve saati görüntüler hello hello BizTalk hizmeti oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="adcde-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-190"><strong>Veritabanı izleme</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="adcde-191">BizTalk hizmeti tarafından kullanılan tablolar izleme hello depolar hello Azure SQL veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="adcde-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="adcde-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> hello veritabanı izleme hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-193"><strong>Depolama izleme/arşivleme</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="adcde-194">BizTalk hizmetinizi çıktısını izleme hello depolayan hello Azure depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="adcde-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="adcde-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> hello depolama hesabı hakkında ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-196"><strong>Abonelik adı</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="adcde-197">BizTalk hizmetinizi barındıran hello abonelik listeler.</span><span class="sxs-lookup"><span data-stu-id="adcde-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="adcde-198">Merhaba abonelik erişim toohello Klasik Azure portalı yönetir.</span><span class="sxs-lookup"><span data-stu-id="adcde-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-199"><strong>Abonelik kimliği</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="adcde-200">Bir abonelik kimliği, bir abonelik oluşturduğunuzda, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adcde-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="adcde-201">REST API kullanırken, tooenter hello abonelik kimliği gerekebilir</span><span class="sxs-lookup"><span data-stu-id="adcde-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="adcde-202">[BizTalk Services: Klasik portalı kullanarak Azure sağlama](http://go.microsoft.com/fwlink/p/?LinkID=302280) listeleri hello adımları toocreate BizTalk hizmeti.</span><span class="sxs-lookup"><span data-stu-id="adcde-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="adcde-203">, Bağlantı bilgilerini, eşitleme anahtarları, yönetin ve hello görev çubuğunda silin:</span><span class="sxs-lookup"><span data-stu-id="adcde-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="adcde-204"><strong>Yönetme</strong> , uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="adcde-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="adcde-205">Hello Azure BizTalk Services portalı açar.</span><span class="sxs-lookup"><span data-stu-id="adcde-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="adcde-206">Merhaba BizTalk Services portalı olan iş ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere, hello giriş tooEDI yapılandırma ve EDIFACT sözleşmelerini.</span><span class="sxs-lookup"><span data-stu-id="adcde-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="adcde-207">Bu olduğu hello aynı <strong>ortak sözleşmeleri oluşturmak</strong> hello üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.</span><span class="sxs-lookup"><span data-stu-id="adcde-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="adcde-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> hello BizTalk Services Portal hakkında daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-209"><strong>Bağlantı bilgilerini</strong> hello erişim denetimi Namespace,</span><span class="sxs-lookup"><span data-stu-id="adcde-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="adcde-210">Erişim denetimi Namespace, varsayılan veren ve varsayılan anahtar değerleri görüntüler hello; hangi kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="adcde-211">Merhaba erişim denetimi portalı da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="adcde-212">Bu erişim denetimi portalı olan hello hello Sol Gezinti Bölmesi'nde hello Active Directory seçeneğini kullanarak aynı.</span><span class="sxs-lookup"><span data-stu-id="adcde-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="adcde-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Bilgisayarınızı ACS Namespace yönetme</a> hello erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-214"><strong>Eşitleme anahtarları</strong> hello depolama hesabı,</span><span class="sxs-lookup"><span data-stu-id="adcde-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="adcde-215">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="adcde-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="adcde-216">Bu şifreleme anahtarları erişim tooyour depolama hesabı denetler.</span><span class="sxs-lookup"><span data-stu-id="adcde-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="adcde-217">BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="adcde-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="adcde-218"><strong>Eşitleme anahtarları</strong> hello BizTalk hizmeti kesintiye uğratmadan hello birincil anahtar hello ikincil anahtar arasındaki kullanıcılar tooswitch etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="adcde-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="adcde-219">Örneğin, BizTalk hizmeti toouse hello depolama hesabı için yeni bir birincil anahtar hello istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="adcde-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="adcde-220">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="adcde-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="adcde-221">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="adcde-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="adcde-222">Merhaba ikincil anahtarı seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-222">Select hello Secondary Key.</span></span> <span data-ttu-id="adcde-223">Bunu yaptığınızda hello BizTalk hizmeti hello ikincil anahtarı kullanarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="adcde-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="adcde-224">Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello birincil anahtarı yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="adcde-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="adcde-225">BizTalk hizmetinizi hello ikincil anahtarı kullanarak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="adcde-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="adcde-226">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="adcde-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="adcde-227">Şimdi, hello birincil anahtarı seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="adcde-228">Bu olduğu hello yeni birincil anahtar, yeniden oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="adcde-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="adcde-229">Hello Klasik Azure portalı, depolama hesabınızı seçin ve hello ikincil anahtarını yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="adcde-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="adcde-230">Bu işlem, "rollover anahtarları" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-230">This process is called "rollover keys".</span></span> <span data-ttu-id="adcde-231">Merhaba tooenable kullanıcılar tooswitch hello birincil anahtar ve ikincil anahtar hello arasında hello BizTalk hizmeti kesintiye uğratmadan amaçtır.</span><span class="sxs-lookup"><span data-stu-id="adcde-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="adcde-232"><strong>Silme</strong> uygulamanız</span><span class="sxs-lookup"><span data-stu-id="adcde-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="adcde-233">BizTalk hizmeti ve tüm öğeleri dağıtılan tooit kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="adcde-234">İzleme</span><span class="sxs-lookup"><span data-stu-id="adcde-234">Monitor</span></span>
<span data-ttu-id="adcde-235">Toohello uygulanmaz ücretsiz sürüm.</span><span class="sxs-lookup"><span data-stu-id="adcde-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="adcde-236">BizTalk hizmet adınızı seçtiğinizde hello İzleyici sekmesi kullanılabilir ve hello şunları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="adcde-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="adcde-237">Ölçüm grafiği: Performans ölçümleri görüntüler hello seçili</span><span class="sxs-lookup"><span data-stu-id="adcde-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="adcde-238">Bu ölçümler hello durumunu hello BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="adcde-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="adcde-239">Hangi performans ölçümleri görüntülenen seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="adcde-240">En fazla altı performans ölçümleri eşzamanlı olarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="adcde-241">Merhaba de seçebilirsiniz **göreli** veya **mutlak** değerleri ve hello zaman aralığı **aralığı** görüntülenen hello ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="adcde-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="adcde-242">Merhaba grafikte tooremove veya görüntü ölçümleri:</span><span class="sxs-lookup"><span data-stu-id="adcde-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="adcde-243">Select hello **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="adcde-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="adcde-244">Seçin **ölçüm Ekle** hello görev çubuğunda:</span><span class="sxs-lookup"><span data-stu-id="adcde-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="adcde-245">![Select ölçüm Ekle][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="adcde-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="adcde-246">Merhaba performans ölçümleri toodisplay istediğiniz denetleyin.</span><span class="sxs-lookup"><span data-stu-id="adcde-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="adcde-247">Merhaba onay işareti tooreturn toohello seçin **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="adcde-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="adcde-248">Merhaba daire sonraki toohello ölçüm toodisplay hello grafiğinde, ölçüm ait değer seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="adcde-249">Örneğin, hello **CPU kullanımı** çıkışı ölçüm gri; çıktısını hello grafik olarak gösterilmez:</span><span class="sxs-lookup"><span data-stu-id="adcde-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="adcde-250">![CPU kullanım ölçüm gri][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="adcde-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="adcde-251">Select hello gri daire tooenable hello **CPU kullanımı** ölçüm toodisplay çıktısını hello grafikte:</span><span class="sxs-lookup"><span data-stu-id="adcde-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="adcde-252">![CPU kullanım ölçüm etkin][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="adcde-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="adcde-253">tooremove hello görünen grafik ve hello listesinde, bir ölçüm seçin **silmek ölçüm** hello görev çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="adcde-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="adcde-254">tooadd hello ölçüm geri toohello listesinden, **ölçüm Ekle** hello görev çubuğunda hello ölçüm Seç hello onay işareti tooreturn toohello denetleyip **İzleyici** sekmesi. Select hello daire tooenable hello seçilemez ölçüm.</span><span class="sxs-lookup"><span data-stu-id="adcde-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="adcde-255"><a name="Metrics"></a>Kullanılabilir ölçümler</span><span class="sxs-lookup"><span data-stu-id="adcde-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="adcde-256">performans sayaçları/ölçümleri aşağıdaki hello kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="adcde-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="adcde-257"><strong>RountdTrip gecikme süresi</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="adcde-258">Merhaba ortalama süre (ms) tooprocess selamlama iletisine tam olarak tüm köprüleri arasında hello BizTalk hizmeti tarafından işlenen kadar hello zaman hello iletisi bir ileti alındığında milisaniye cinsinden geçen görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="adcde-259">Başarıyla işlenen iletiler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="adcde-260">Bir zaman damgası, olayları aşağıdaki hello oluştuğunda oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="adcde-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="adcde-261">İleti hello ağ geçidi girer.</span><span class="sxs-lookup"><span data-stu-id="adcde-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="adcde-262">Yönlendirilmiş toohello hedef iletisidir</span><span class="sxs-lookup"><span data-stu-id="adcde-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="adcde-263">Hedef yanıtı aldı</span><span class="sxs-lookup"><span data-stu-id="adcde-263">Destination response is received</span></span></li>
<li><span data-ttu-id="adcde-264">Hedef bildirim gönderilen yanıtı toohello ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="adcde-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="adcde-265">Bu ölçüm, hesaplama aşağıdaki hello hello sonucunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="adcde-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="adcde-266">[Hedef bildirim gönderilen yanıtı toohello ağ geçidi] - [ileti girer hello ağ geçidi]</span><span class="sxs-lookup"><span data-stu-id="adcde-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-267"><strong>Kaynaktaki hataları</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="adcde-268">Merhaba başarısız iletilerin toplam sayısını görüntüler hello hello kaynak uç noktaları iletilerden çekme BizTalk hizmet tarafından.</span><span class="sxs-lookup"><span data-stu-id="adcde-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-269"><strong>CPU kullanımı</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="adcde-270">Merhaba ortalama % işlemci zamanı, tüm rol örneği listeler.</span><span class="sxs-lookup"><span data-stu-id="adcde-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-271"><strong>İşleme gecikmesi</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="adcde-272">Bir ileti hello zaman hariç tüm köprüleri arasında hello BizTalk hizmeti tarafından varış yeri için harcanan milisaniye (ms) tooprocess alınan hello ortalama süreyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="adcde-273">Başarıyla işlenen iletiler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="adcde-274">Olayları aşağıdaki hello her oluştuğunda bir zaman damgası oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="adcde-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="adcde-275">İleti hello ağ geçidi girer.</span><span class="sxs-lookup"><span data-stu-id="adcde-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="adcde-276">Yönlendirilmiş toohello hedef iletisidir</span><span class="sxs-lookup"><span data-stu-id="adcde-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="adcde-277">Hedef yanıtı aldı</span><span class="sxs-lookup"><span data-stu-id="adcde-277">Destination response is received</span></span></li>
<li><span data-ttu-id="adcde-278">Hedef bildirim gönderilen yanıtı toohello ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="adcde-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="adcde-279">Bu ölçüm, hesaplama aşağıdaki hello hello sonucunu gösterir:</span><span class="sxs-lookup"><span data-stu-id="adcde-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="adcde-280">[Hedef bildirim gönderilen yanıtı toohello ağ geçidi] - [ileti girer hello ağ geçidi] - [hedef yanıt alındığında] + [ileti yönlendirilmiş toohello hedef]</span><span class="sxs-lookup"><span data-stu-id="adcde-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-281"><strong>İşlemdeki hataları</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="adcde-282">Merhaba işleme sırasında tüm hello köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığında başarısız iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-283"><strong>Gönderilen iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="adcde-284">Tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde gönderilen iletilerin toplam sayısını görüntüler hello.</span><span class="sxs-lookup"><span data-stu-id="adcde-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="adcde-285">Bu ölçüm, ardışık düzen tarafından gönderilen bir ileti hello rota hedef ulaştığında artırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="adcde-286">Bu ölçüm, bir ileti başarıyla işlendi göstermez.</span><span class="sxs-lookup"><span data-stu-id="adcde-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="adcde-287">Merhaba rota hedef giriş bildirim geri toohello ardışık gönderdiğinde istek-yanıt senaryoda hello ölçüm artırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-288"><strong>Alınan iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="adcde-289">Tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde alınan iletilerin toplam sayısını görüntüler hello.</span><span class="sxs-lookup"><span data-stu-id="adcde-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="adcde-290">Bu ölçüm, yeni bir ileti hello ardışık düzen tarafından alındığında artırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-291"><strong>İşlemindeki iletiler</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="adcde-292">Bir zaman aralığı içinde hello BizTalk hizmeti tarafından işlenmekte olan iletilerin toplam sayısını görüntüler hello.</span><span class="sxs-lookup"><span data-stu-id="adcde-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="adcde-293"><strong>İşlenen iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="adcde-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="adcde-294">Görüntüler başarıyla tüm köprüleri arasında hello BizTalk hizmeti tarafından bir zaman aralığı içinde işlenen iletilerin toplam sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="adcde-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="adcde-295">Bu ölçüm, bir ileti başarıyla hello ardışık düzen ve başarıyla yönlendirilmiş toohello hedef tarafından alındığında artırılır.</span><span class="sxs-lookup"><span data-stu-id="adcde-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="adcde-296">Ölçek</span><span class="sxs-lookup"><span data-stu-id="adcde-296">Scale</span></span>
<span data-ttu-id="adcde-297">Hello ölçek sekmesinde, ekleyin veya BizTalk hizmeti tarafından kullanılan birim sayısını hello çıkarın.</span><span class="sxs-lookup"><span data-stu-id="adcde-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="adcde-298">Varsayılan olarak, yoktur birim yapılandırılmış bir.</span><span class="sxs-lookup"><span data-stu-id="adcde-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="adcde-299">Ek birimler tooscale eklenebilir, BizTalk hizmeti.</span><span class="sxs-lookup"><span data-stu-id="adcde-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="adcde-300">Merhaba ölçek artırdığınızda, üretilen iş artmaktadır.</span><span class="sxs-lookup"><span data-stu-id="adcde-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="adcde-301">Hello kaynakları da, dağıtılan köprüleri, anlaşmalar, LOB bağlantıları dahil olmak üzere ve işlemci gücü artar.</span><span class="sxs-lookup"><span data-stu-id="adcde-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="adcde-302">Örneğin, 1 birim too2 birimlerinden hello ölçeği artırın.</span><span class="sxs-lookup"><span data-stu-id="adcde-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="adcde-303">Bu durumda, çift hello sayısı köprüleri, çift hello anlaşmaları, çift hello LOB bağlantıları ve çift hello işleme gücünü dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adcde-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="adcde-304">Bazı BizTalk sürümleri Ölçek seçeneği sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="adcde-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="adcde-305">Bu durumda, tek bir birim izin verilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="adcde-306">toodetermine sürümünüz ölçeklendirilmiş, kaç tane birimleri başvurmak çok[BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="adcde-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="adcde-307">Birimleri Hello sayısını artırmayı fiyatlandırmayı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="adcde-308">Merhaba birimleri artırırsanız, seçme **kaydetmek** faturalama etkilenen olmadığını bildiren bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="adcde-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="adcde-309">Ardından, toocontinue de seçin.</span><span class="sxs-lookup"><span data-stu-id="adcde-309">You then choose toocontinue.</span></span> <span data-ttu-id="adcde-310">Hello birim sayısını artırdığınızda, Active tooUpdating hello BizTalk hizmeti durumunu değiştirir.</span><span class="sxs-lookup"><span data-stu-id="adcde-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="adcde-311">Hello güncelleştirme durumu, BizTalk hizmeti toorun devam eder.</span><span class="sxs-lookup"><span data-stu-id="adcde-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="adcde-312">[BizTalk Services: Sürümler grafiği](biztalk-editions-feature-chart.md) "Birim" tanımlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="adcde-313">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="adcde-313">Configure</span></span>
<span data-ttu-id="adcde-314">TooHybrid bağlantıları için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="adcde-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="adcde-315">Merhaba yedekleme durumu tooNone veya otomatik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="adcde-316">TooNone, ayarlandığında yedekleme otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adcde-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="adcde-317">TooAutomatic, ayarlandığında hello yedekleme konumu, hello yedekleme ve ne kadar süreyle tookeep hello yedekleme dosyalarını hello sıklığını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="adcde-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="adcde-318">[BizTalk Services: Yedekleme ve geri yükleme](biztalk-backup-restore.md) hello ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="adcde-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="adcde-319"><a name="HybridConnections"></a>Karma bağlantılar</span><span class="sxs-lookup"><span data-stu-id="adcde-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="adcde-320">Karma bağlantılar Azure uygulaması, Web uygulamaları veya Mobile Apps Azure App Service'te bir statik TCP bağlantı noktası, SQL Server, MySQL, HTTP Web API'leri ve en özel Web Hizmetleri gibi kullanan tooan şirket içi kaynağa gibi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="adcde-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="adcde-321">Karma bağlantılar BizTalk Services'da hello Klasik Azure portalı yönetilir.</span><span class="sxs-lookup"><span data-stu-id="adcde-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="adcde-322">Karma bağlantılar Azure App Service'te toocreate bkz [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="adcde-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="adcde-323">toocreate veya karma bağlantılar Azure BizTalk Services yönetmek için bkz: [karma bağlantılar](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="adcde-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="adcde-324">Sonraki</span><span class="sxs-lookup"><span data-stu-id="adcde-324">Next</span></span>
<span data-ttu-id="adcde-325">Merhaba farklı sekmelerle tanıdık, hello Azure BizTalk Services özellikleri hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="adcde-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="adcde-326">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="adcde-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="adcde-327">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="adcde-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="adcde-328">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="adcde-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="adcde-329">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="adcde-329">See Also</span></span>
* [<span data-ttu-id="adcde-330">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="adcde-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="adcde-331">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="adcde-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="adcde-332">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="adcde-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="adcde-333">BizTalk Services: BizTalk hizmeti durumu grafiği</span><span class="sxs-lookup"><span data-stu-id="adcde-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="adcde-334">I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello</span><span class="sxs-lookup"><span data-stu-id="adcde-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

