---
title: "Pano, İzleyici, Ölçek, yapılandırmak ve karma bağlantılar BizTalk Services | Microsoft Docs"
description: "Denetimleri hakkında bilgi edinin ve izleme Klasik portal sekmelerindeki performans için BizTalk Services: pano, İzleyici, Ölçek, yapılandırma ve karma bağlantılar. MABS, WABS"
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
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="eb6f1-104">Pano, İzleme, Ölçeklendirme, Yapılandırma ve Karma Bağlantı sekmelerini inceleyin</span><span class="sxs-lookup"><span data-stu-id="eb6f1-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="eb6f1-105">BizTalk hizmeti oluşturma ve uygulamanızı dağıttıktan sonra bazı BizTalk hizmeti ayarlarını değiştirin ve uygulama performansı izleme.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="eb6f1-106">Klasik Azure portalını açtığınızda, otomatik olarak yerleştirilmiş **tüm öğeleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="eb6f1-107">BizTalk hizmeti görüntülemek için BizTalk hizmetinizi seçin **tüm öğeleri** sekmesinde veya seçin **BIZTALK SERVICES** sekmesinde; ve ardından, BizTalk hizmeti adını seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="eb6f1-108">Aşağıdaki sekmeleri içeren yeni bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="eb6f1-109">Bu konuda aşağıdaki sekmelerden açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="eb6f1-110">Hızlı Başlangıç)</span><span class="sxs-lookup"><span data-stu-id="eb6f1-110">Quickstart (</span></span>![Hızlı Başlangıç][Quickstart]<span data-ttu-id="eb6f1-112">)</span><span class="sxs-lookup"><span data-stu-id="eb6f1-112">)</span></span>
<span data-ttu-id="eb6f1-113">BizTalk Services sürümüne göre listelenen tüm seçenekleri kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="eb6f1-114"><strong>Araçları edinin</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="eb6f1-115">Şirket içi geliştirme bilgisayarınızda Visual Studio Proje şablonları yüklemek için BizTalk Services SDK'sını indirin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="eb6f1-116">Bu şablonlar oluşturma <strong>BizTalk Services</strong> (köprü) ve <strong>BizTalk hizmeti yapıları</strong> BizTalk hizmetinize dağıtılan (dönüştürme) Visual Studio projeleri.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="eb6f1-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Ne başlamalıyım Azure BizTalk Services SDK'sını kullanarak </a> ve <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Azure BizTalk Services SDK'sını yükleme</a> başlamak için adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="eb6f1-118"><strong>İş ortağı anlaşmaları oluşturma</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="eb6f1-119">Azure BizTalk Services burada ortakları ekleme ve X12, AS2, oluşturma Azure üzerinde barındırılan portalı açar ve EDIFACT EDI sözleşmeleri.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="eb6f1-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> başlamak için adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="eb6f1-121"><strong>BizTalk hizmetleri hakkında daha fazla bilgi edinin</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="eb6f1-122">Git <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">center öğrenme</a> Azure BizTalk Services hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="eb6f1-123">Altındaki görev çubuğunda şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="eb6f1-124"><strong>Yönetme</strong> , uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="eb6f1-125">Azure BizTalk Services Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="eb6f1-126">BizTalk Services ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere EDI yapılandırma girişinin portalıdır ve EDIFACT sözleşmelerini.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-127">Bu aynı sonucu verir <strong>ortak sözleşmeleri oluşturmak</strong> üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="eb6f1-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> BizTalk Services portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="eb6f1-129"><strong>Bağlantı bilgilerini</strong> , erişim denetimi Namespace</span><span class="sxs-lookup"><span data-stu-id="eb6f1-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="eb6f1-130">Bağlantı bilgilerini seçtiğinizde, erişim denetimi Namespace, varsayılan veren ve varsayılan anahtar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="eb6f1-131">Bu değerleri kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-132">Erişim denetimi portalı da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="eb6f1-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Erişim denetimi Namespace oluşturmak</a> erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="eb6f1-134"><strong>Eşitleme anahtarları</strong> depolama hesabındaki</span><span class="sxs-lookup"><span data-stu-id="eb6f1-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="eb6f1-135">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="eb6f1-136">Bu şifreleme anahtarları, depolama hesabınıza erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="eb6f1-137">BizTalk hizmeti otomatik olarak birincil anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="eb6f1-138"><strong>Eşitleme anahtarları</strong> BizTalk hizmeti kesintiye uğratmadan birincil anahtar ve ikincil anahtar arasında geçiş yapma olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-139">Örneğin, depolama hesabı için yeni bir birincil anahtar kullanmak için BizTalk hizmeti istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="eb6f1-140">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="eb6f1-141">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="eb6f1-142">İkincil anahtar seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-142">Select the Secondary Key.</span></span> <span data-ttu-id="eb6f1-143">Bunu yaptığınızda, ikincil anahtarı kullanarak BizTalk hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="eb6f1-144">Azure Klasik portalında, depolama hesabınızı seçin ve birincil anahtar yeniden.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="eb6f1-145">BizTalk hizmetinizi ikincil anahtarı kullanarak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="eb6f1-146">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="eb6f1-147">Şimdi, birincil anahtar seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-147">Now, select the Primary Key.</span></span> <span data-ttu-id="eb6f1-148">Bu yeni birincil, yeniden anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="eb6f1-149">Azure Klasik portalında, depolama hesabınızı seçin ve ikincil anahtar yeniden.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="eb6f1-150">Bu işlem, "rollover anahtarları" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-150">This process is called "rollover keys".</span></span> <span data-ttu-id="eb6f1-151">Amacı, BizTalk hizmeti kesintiye uğratmadan birincil anahtar ve ikincil anahtar arasında geçiş yapmak kullanıcıların sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="eb6f1-152"><strong>Silme</strong> uygulamanız</span><span class="sxs-lookup"><span data-stu-id="eb6f1-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="eb6f1-153">Seçtiğinizde silin, BizTalk hizmeti ve dağıtılmış tüm öğeler kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="eb6f1-154">Pano</span><span class="sxs-lookup"><span data-stu-id="eb6f1-154">Dashboard</span></span>
<span data-ttu-id="eb6f1-155">BizTalk Services sürümüne göre listelenen tüm seçenekleri kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="eb6f1-156">BizTalk hizmet adınızı seçin, Pano sekmesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="eb6f1-157">Panosunda, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="eb6f1-158">Kullanıma genel bakış: kullanılan karma bağlantı sayısını gösterir</span><span class="sxs-lookup"><span data-stu-id="eb6f1-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="eb6f1-159">Ayrıca veri kullanımı GB cinsinden görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="eb6f1-160">Ölçüm grafiği: performans ölçümleri sabit bir listesini gösterir</span><span class="sxs-lookup"><span data-stu-id="eb6f1-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="eb6f1-161">Bu ölçümler BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="eb6f1-162">Ayrıca seçebilirsiniz **göreli** veya **mutlak** değerleri ve zaman aralığını **aralığı** grafikte görüntülenen ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="eb6f1-163">Bu performans ölçümlerini bir açıklaması için Git [kullanılabilir ölçümler](#Metrics) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="eb6f1-164">Hızlı Bakış: BizTalk hizmeti özelliklerinizi listeler</span><span class="sxs-lookup"><span data-stu-id="eb6f1-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="eb6f1-165"><strong>İzleme veritabanı kimlik bilgileri güncelleştir</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="eb6f1-166">Kullanıcı adı ve izleme veritabanına oturum açmak için kullandığınız parolayı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-167"><strong>SSL sertifikasını güncelleştir</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="eb6f1-168">BizTalk hizmetini farklı bir SSL sertifikası kullanacak şekilde güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="eb6f1-169">Otomatik olarak imzalanan bir SSL sertifikası otomatik olarak oluşturulur, <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">BizTalk hizmeti oluşturma</a>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-170"><strong>Sertifikayı indirin</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="eb6f1-171">Yerel makineye BizTalk hizmeti tarafından kullanılan SSL sertifikası yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-172"><strong>Durumu</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="eb6f1-173">BizTalk hizmeti geçerli durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-174">Bkz: <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Hizmet durumu grafiği</a>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-175"><strong>Hizmet URL'si</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="eb6f1-176">BizTalk hizmeti için URL.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-177">Bu aynı sonucu verir <strong>etki alanı URL'si</strong> BizTalk hizmeti oluşturulduğunda girildi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-178"><strong>Genel sanal IP (VIP) adresi</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="eb6f1-179">BizTalk Hizmetinize atanmış IP adresi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-180">Tüm giriş uç noktaları için kullanılır ve kaynak adres giden trafik için.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="eb6f1-181">Oluşturulan sürece bu IP adresi, BizTalk hizmetinize aittir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="eb6f1-182">BizTalk hizmeti silerseniz, IP adresi için başka bir BizTalk hizmeti atanır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-183"><strong>ACS Namespace</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="eb6f1-184">BizTalk hizmeti ile kimlik doğrulamasını yapar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-185"><strong>Sürüm</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="eb6f1-186">BizTalk hizmeti oluşturulduğunda listeleri Edition girdi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-187"><strong>Konum</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="eb6f1-188">BizTalk hizmetinizi barındıran coğrafi bölgeyi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-189"><strong>Oluşturulan</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="eb6f1-190">BizTalk hizmeti oluşturulduğu saat ve tarihi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-191"><strong>Veritabanı izleme</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="eb6f1-192">BizTalk hizmeti tarafından kullanılan izleme tablosu depolar Azure SQL veritabanı adı.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="eb6f1-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> izleme veritabanında ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-194"><strong>Depolama izleme/arşivleme</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="eb6f1-195">BizTalk hizmeti izleme çıktısını depolar Azure depolama hesabı adı.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="eb6f1-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Gereksinimleri Explained</a> depolama hesabında ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-197"><strong>Abonelik adı</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="eb6f1-198">BizTalk hizmetinizi barındıran abonelik listeler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-199">Abonelik Klasik Azure portalına erişimi yönetir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-200"><strong>Abonelik kimliği</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="eb6f1-201">Bir abonelik kimliği, bir abonelik oluşturduğunuzda, otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="eb6f1-202">REST API kullanırken, abonelik kimliği girmeniz gerekebilir</span><span class="sxs-lookup"><span data-stu-id="eb6f1-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="eb6f1-203">[BizTalk Services: Klasik portalı kullanarak Azure sağlama](http://go.microsoft.com/fwlink/p/?LinkID=302280) BizTalk hizmeti oluşturma adımlarını listeler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="eb6f1-204">, Bağlantı bilgilerini, eşitleme anahtarları, yönetin ve görev çubuğunda silin:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="eb6f1-205"><strong>Yönetme</strong> , uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="eb6f1-206">Azure BizTalk Services Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="eb6f1-207">BizTalk Services ortakları ekleme ve X12, AS2, oluşturma dahil olmak üzere EDI yapılandırma girişinin portalıdır ve EDIFACT sözleşmelerini.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-208">Bu aynı sonucu verir <strong>ortak sözleşmeleri oluşturmak</strong> üzerinde <strong>Hızlı Başlangıç</strong> sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="eb6f1-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">EDI ileti BizTalk Services Portal bileşenlerini yapılandırma</a> BizTalk Services portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-210"><strong>Bağlantı bilgilerini</strong> , erişim denetimi Namespace</span><span class="sxs-lookup"><span data-stu-id="eb6f1-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="eb6f1-211">Erişim denetimi Namespace, varsayılan veren ve varsayılan anahtar değerleri görüntüler; hangi kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-212">Erişim denetimi portalı da açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="eb6f1-213">Bu erişim denetimi portalı sol gezinti bölmesinde Active Directory seçeneğini kullanarak aynıdır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="eb6f1-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Bilgisayarınızı ACS Namespace yönetme</a> erişim denetimi portalı üzerinde daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-215"><strong>Eşitleme anahtarları</strong> depolama hesabındaki</span><span class="sxs-lookup"><span data-stu-id="eb6f1-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="eb6f1-216">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="eb6f1-217">Bu şifreleme anahtarları, depolama hesabınıza erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="eb6f1-218">BizTalk hizmeti otomatik olarak birincil anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="eb6f1-219"><strong>Eşitleme anahtarları</strong> BizTalk hizmeti kesintiye uğratmadan birincil anahtar ve ikincil anahtar arasında geçiş yapma olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-220">Örneğin, depolama hesabı için yeni bir birincil anahtar kullanmak için BizTalk hizmeti istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="eb6f1-221">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="eb6f1-222">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="eb6f1-223">İkincil anahtar seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-223">Select the Secondary Key.</span></span> <span data-ttu-id="eb6f1-224">Bunu yaptığınızda, ikincil anahtarı kullanarak BizTalk hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="eb6f1-225">Azure Klasik portalında, depolama hesabınızı seçin ve birincil anahtar yeniden.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="eb6f1-226">BizTalk hizmetinizi ikincil anahtarı kullanarak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="eb6f1-227">BizTalk hizmetinizi seçip <strong>anahtarları Eşitle</strong>.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="eb6f1-228">Şimdi, birincil anahtar seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-228">Now, select the Primary Key.</span></span> <span data-ttu-id="eb6f1-229">Bu yeni birincil, yeniden anahtarıdır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="eb6f1-230">Azure Klasik portalında, depolama hesabınızı seçin ve ikincil anahtar yeniden.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="eb6f1-231">Bu işlem, "rollover anahtarları" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-231">This process is called "rollover keys".</span></span> <span data-ttu-id="eb6f1-232">Amacı, BizTalk hizmeti kesintiye uğratmadan birincil anahtar ve ikincil anahtar arasında geçiş yapmak kullanıcıların sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="eb6f1-233"><strong>Silme</strong> uygulamanız</span><span class="sxs-lookup"><span data-stu-id="eb6f1-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="eb6f1-234">BizTalk hizmeti ve dağıtılmış tüm öğeler kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="eb6f1-235">İzleme</span><span class="sxs-lookup"><span data-stu-id="eb6f1-235">Monitor</span></span>
<span data-ttu-id="eb6f1-236">Ücretsiz sürüm için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="eb6f1-237">BizTalk hizmet adınızı seçtiğinizde, İzleyici sekmesi kullanılabilir ve şunları görüntüler:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="eb6f1-238">Ölçüm grafiği: Seçili performans ölçümleri görüntüler</span><span class="sxs-lookup"><span data-stu-id="eb6f1-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="eb6f1-239">Bu ölçümler BizTalk hizmeti ile ilgili gerçek zamanlı değerleri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="eb6f1-240">Hangi performans ölçümleri görüntülenen seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="eb6f1-241">En fazla altı performans ölçümleri eşzamanlı olarak görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="eb6f1-242">Ayrıca seçebilirsiniz **göreli** veya **mutlak** değerleri ve zaman aralığını **aralığı** görüntülenen ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="eb6f1-243">Grafikte ölçümleri görüntülemek veya kaldırmak için:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="eb6f1-244">Seçin **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="eb6f1-245">Seçin **ölçüm Ekle** görev çubuğunda:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="eb6f1-246">![Select ölçüm Ekle][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="eb6f1-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="eb6f1-247">Görüntülemek istediğiniz performans ölçümleri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="eb6f1-248">Geri dönmek için onay işaretini seçin **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="eb6f1-249">Bu ölçüm ait değer grafikte görüntülenecek ölçüm yanındaki daire seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="eb6f1-250">Örneğin, **CPU kullanımı** çıkışı ölçüm gri; çıktısını grafikte gösterilmez:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="eb6f1-251">![CPU kullanım ölçüm gri][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="eb6f1-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="eb6f1-252">Gri etkinleştirmek için büyüyen daire seçin **CPU kullanımı** ölçüm grafikte çıktısını görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="eb6f1-253">![CPU kullanım ölçüm etkin][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="eb6f1-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="eb6f1-254">Görüntü grafik hem de listesinden bir ölçüm kaldırmak için seçin **silmek ölçüm** görev çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="eb6f1-255">Ölçüm geri listesine eklemek için seçin **ölçüm Ekle** görev çubuğunda ölçüm denetleyin ve geri dönmek için onay işaretini seçin **İzleyici** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="eb6f1-256">Gri ölçüm etkinleştirmek için büyüyen daire seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="eb6f1-257"><a name="Metrics"></a>Kullanılabilir ölçümler</span><span class="sxs-lookup"><span data-stu-id="eb6f1-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="eb6f1-258">Aşağıdaki performans sayaçları/ölçümleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="eb6f1-259"><strong>RountdTrip gecikme süresi</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="eb6f1-260">Milisaniye (ms) iletiyi tamamen BizTalk hizmeti tarafından işlenen kadar ileti alındığında bir ileti zamandan işlenmesi için geçen ortalama süre tüm köprüleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="eb6f1-261">Başarıyla işlenen iletiler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="eb6f1-262">Aşağıdaki olaylar gerçekleştiğinde, zaman damgası oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="eb6f1-263">Ağ geçidi ileti girer</span><span class="sxs-lookup"><span data-stu-id="eb6f1-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="eb6f1-264">İleti hedef yönlendirilir</span><span class="sxs-lookup"><span data-stu-id="eb6f1-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="eb6f1-265">Hedef yanıtı aldı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-265">Destination response is received</span></span></li>
<li><span data-ttu-id="eb6f1-266">Ağ geçidine gönderilen hedef onay yanıtı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="eb6f1-267">Bu ölçüm, aşağıdaki hesaplamanın sonucu gösterir:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="eb6f1-268">[Hedef onay yanıtı ağ geçidine gönderilen] - [ileti girer ağ geçidi]</span><span class="sxs-lookup"><span data-stu-id="eb6f1-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-269"><strong>Kaynaktaki hataları</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="eb6f1-270">Başarısız iletilerin toplam sayısını görüntüler BizTalk kaynak uç noktaları iletilerden çekme zaman hizmeti tarafından.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-271"><strong>CPU kullanımı</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="eb6f1-272">Tüm rol örneklerinin ortalama % işlemci zamanı listeler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-273"><strong>İşleme gecikmesi</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="eb6f1-274">Varış yeri için harcanan zaman hariç tüm köprüleri arasında milisaniye (ms) BizTalk hizmeti tarafından bir iletiyi işlemek için geçen ortalama süre görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="eb6f1-275">Başarıyla işlenen iletiler kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="eb6f1-276">Her aşağıdaki olaylardan biri gerçekleştiğinde bir zaman damgası oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="eb6f1-277">Ağ geçidi ileti girer</span><span class="sxs-lookup"><span data-stu-id="eb6f1-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="eb6f1-278">İleti hedef yönlendirilir</span><span class="sxs-lookup"><span data-stu-id="eb6f1-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="eb6f1-279">Hedef yanıtı aldı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-279">Destination response is received</span></span></li>
<li><span data-ttu-id="eb6f1-280">Ağ geçidine gönderilen hedef onay yanıtı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="eb6f1-281">Bu ölçüm, aşağıdaki hesaplamanın sonucu gösterir:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="eb6f1-282">[Hedef onay yanıtı ağ geçidine gönderilen] - [ileti girer ağ geçidi] - [hedef yanıt alındığında] + [hedefe ileti yönlendirilmiş]</span><span class="sxs-lookup"><span data-stu-id="eb6f1-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-283"><strong>İşlemdeki hataları</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="eb6f1-284">Tüm köprüleri BizTalk hizmeti tarafından işlenmesi sırasında bir zaman aralığı içinde başarısız oldu iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-285"><strong>Gönderilen iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="eb6f1-286">BizTalk hizmeti tarafından bir zaman aralığı içinde tüm köprüleri gönderilen iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="eb6f1-287">Bu ölçüm, ardışık düzen tarafından gönderilen bir ileti rota hedef ulaştığında artırılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="eb6f1-288">Bu ölçüm, bir ileti başarıyla işlendi göstermez.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="eb6f1-289">Rota hedef ardışık düzene alınmasını alındısı gönderdiğinde bir istek-yanıt senaryosunda, ölçüm artırılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-290"><strong>Alınan iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="eb6f1-291">Bir zaman aralığı içinde tüm köprüleri BizTalk hizmeti tarafından alınan iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="eb6f1-292">Bu ölçüm ardışık düzen tarafından yeni bir ileti alındığında artırılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-293"><strong>İşlemindeki iletiler</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="eb6f1-294">BizTalk hizmeti tarafından bir zaman aralığı içinde işlenmekte olan iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="eb6f1-295"><strong>İşlenen iletileri</strong></span><span class="sxs-lookup"><span data-stu-id="eb6f1-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="eb6f1-296">BizTalk hizmeti tarafından tüm köprüleri arasında bir zaman aralığı içinde başarıyla işlenen iletilerin toplam sayısını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="eb6f1-297">Bu ölçüm, bir ileti ardışık düzen tarafından başarıyla alındı ve başarıyla hedefe yönlendirilen olduğunda artırılır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="eb6f1-298">Ölçek</span><span class="sxs-lookup"><span data-stu-id="eb6f1-298">Scale</span></span>
<span data-ttu-id="eb6f1-299">Ölçek sekmesini ekleyin ya da BizTalk hizmeti tarafından kullanılan birim sayısını çıkarın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-300">Varsayılan olarak, yoktur birim yapılandırılmış bir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="eb6f1-301">Ek birimler, BizTalk hizmeti ölçeklendirmek için eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="eb6f1-302">Ölçek artırdığınızda, üretilen iş artmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="eb6f1-303">Kaynaklar ayrıca, işlemci gücü ve dağıtılan köprüleri, anlaşmalar, LOB bağlantıları dahil olmak üzere artar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="eb6f1-304">Örneğin, 1 birim ölçekte 2 birimlerine artırın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="eb6f1-305">Bu durumda, çift köprü sayısı dağıtmak, anlaşmaları çift, LOB bağlantıları çift ve işlemci gücü çift.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="eb6f1-306">Bazı BizTalk sürümleri Ölçek seçeneği sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="eb6f1-307">Bu durumda, tek bir birim izin verilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="eb6f1-308">Sürümünüz genişletilmiş birim sayısını belirlemek için başvurmak [BizTalk Services: sürümler grafiği](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f1-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="eb6f1-309">Birim sayısını artırmayı fiyatlandırmayı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="eb6f1-310">Birimleri artırırsanız, seçme **kaydetmek** faturalama etkilenen olmadığını bildiren bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="eb6f1-311">Ardından devam etmek seçin.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-311">You then choose to continue.</span></span> <span data-ttu-id="eb6f1-312">Zaman birimleri, güncelleştirme Etkin'den BizTalk hizmeti durumu değişiklikleri sayısını artırın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="eb6f1-313">Güncelleştirme durumu, BizTalk hizmeti çalışmaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="eb6f1-314">[BizTalk Services: Sürümler grafiği](biztalk-editions-feature-chart.md) "Birim" tanımlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="eb6f1-315">Yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eb6f1-315">Configure</span></span>
<span data-ttu-id="eb6f1-316">Karma bağlantılar için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="eb6f1-317">Yedekleme durumu Yok'a ayarlar veya otomatik.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="eb6f1-318">None olarak ayarlandığında, yedekleme otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="eb6f1-319">Otomatik olarak ayarlandığında, yedek dosyaları saklamak için sıklığı, yedekleme ve ne kadar süre yedeklemeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="eb6f1-320">[BizTalk Services: Yedekleme ve geri yükleme](biztalk-backup-restore.md) ait ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="eb6f1-321"><a name="HybridConnections"></a>Karma bağlantılar</span><span class="sxs-lookup"><span data-stu-id="eb6f1-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="eb6f1-322">Karma bağlantılar Azure uygulaması, Web uygulamaları veya Azure App Service'de Mobile Apps gibi statik TCP bağlantı noktası, SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi kullanan bir şirket içi kaynağa bağlayın.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="eb6f1-323">Karma bağlantılar, Azure Klasik Portalı'nda BizTalk Services'da yönetilir.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="eb6f1-324">Azure App Service içinde karma bağlantılar oluşturmak için bkz: [erişim şirket içi Azure App Service içinde karma bağlantılar kullanarak kaynakları](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f1-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="eb6f1-325">Oluşturmak veya karma bağlantılar Azure BizTalk Services yönetmek için bkz: [karma bağlantılar](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eb6f1-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="eb6f1-326">Sonraki</span><span class="sxs-lookup"><span data-stu-id="eb6f1-326">Next</span></span>
<span data-ttu-id="eb6f1-327">Farklı sekmelerle tanıdık, Azure BizTalk Services özellikleri hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb6f1-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="eb6f1-328">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="eb6f1-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="eb6f1-329">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="eb6f1-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="eb6f1-330">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="eb6f1-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="eb6f1-331">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="eb6f1-331">See Also</span></span>
* [<span data-ttu-id="eb6f1-332">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="eb6f1-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="eb6f1-333">BizTalk Services: Geliştirici, temel, standart ve Premium sürümler grafiği</span><span class="sxs-lookup"><span data-stu-id="eb6f1-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="eb6f1-334">BizTalk Services: Klasik portalı kullanarak Azure hazırlama</span><span class="sxs-lookup"><span data-stu-id="eb6f1-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="eb6f1-335">BizTalk Services: BizTalk hizmeti durumu grafiği</span><span class="sxs-lookup"><span data-stu-id="eb6f1-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="eb6f1-336">Azure BizTalk Services SDK'sını Kullanmaya Nasıl Başlarım</span><span class="sxs-lookup"><span data-stu-id="eb6f1-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

