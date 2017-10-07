---
title: "aaaInstall şirket içi veri ağ geçidi - Azure Logic Apps | Microsoft Docs"
description: "Şirket içi veri kaynaklarına erişim önce hızlı veri aktarımı ve şirket içi veri kaynakları ve mantıksal uygulamalar arasında şifreleme için hello şirket içi veri ağ geçidi yükleyin"
keywords: "Şirket içi veri aktarımı, şifreleme, veri kaynakları veri erişimi"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="70354-104">Azure mantıksal uygulamaları için Hello şirket içi veri ağ geçidi yükleyin</span><span class="sxs-lookup"><span data-stu-id="70354-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="70354-105">Mantıksal uygulamalarınızı şirket içi veri kaynaklarına erişebilmesi için yükleme ve hello şirket içi veri ağ geçidi kurun.</span><span class="sxs-lookup"><span data-stu-id="70354-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="70354-106">Merhaba ağ geçidi hızlı veri aktarımı ve şirket içi sistemleri ve logic apps arasında şifreleme sağlayan köprü gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="70354-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="70354-107">Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="70354-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="70354-108">Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı.</span><span class="sxs-lookup"><span data-stu-id="70354-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="70354-109">Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="70354-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="70354-110">Merhaba ağ geçidi bağlantıları toothese veri kaynakları şirket içinde destekler:</span><span class="sxs-lookup"><span data-stu-id="70354-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="70354-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="70354-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="70354-112">DB2</span><span class="sxs-lookup"><span data-stu-id="70354-112">DB2</span></span>  
*   <span data-ttu-id="70354-113">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="70354-113">File System</span></span>
*   <span data-ttu-id="70354-114">Informix</span><span class="sxs-lookup"><span data-stu-id="70354-114">Informix</span></span>
*   <span data-ttu-id="70354-115">MQ</span><span class="sxs-lookup"><span data-stu-id="70354-115">MQ</span></span>
*   <span data-ttu-id="70354-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="70354-116">MySQL</span></span>
*   <span data-ttu-id="70354-117">Oracle Veritabanı</span><span class="sxs-lookup"><span data-stu-id="70354-117">Oracle Database</span></span>
*   <span data-ttu-id="70354-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="70354-118">PostgreSQL</span></span>
*   <span data-ttu-id="70354-119">SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="70354-119">SAP Application Server</span></span> 
*   <span data-ttu-id="70354-120">SAP ileti sunucusu</span><span class="sxs-lookup"><span data-stu-id="70354-120">SAP Message Server</span></span>
*   <span data-ttu-id="70354-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="70354-121">SharePoint</span></span>
*   <span data-ttu-id="70354-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="70354-122">SQL Server</span></span>
*   <span data-ttu-id="70354-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="70354-123">Teradata</span></span>

<span data-ttu-id="70354-124">Bu adımları nasıl toofirst yükleme hello veri ağ geçidi, önce şirket içi Göster [hello ağ geçidi ve logic apps arasında bir bağlantı ayarlayın](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="70354-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="70354-125">Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="70354-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="70354-126">Nasıl toouse hello diğer hizmetler ile ağ geçidi hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="70354-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="70354-127">Microsoft Power BI şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="70354-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="70354-128">Azure Analysis Services veri ağ geçidi şirket içi</span><span class="sxs-lookup"><span data-stu-id="70354-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="70354-129">Microsoft Flow şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="70354-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="70354-130">Microsoft PowerApps şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="70354-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="70354-131">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="70354-131">Requirements</span></span>

<span data-ttu-id="70354-132">**Minimum**:</span><span class="sxs-lookup"><span data-stu-id="70354-132">**Minimum**:</span></span>

* <span data-ttu-id="70354-133">.NET 4.5 framework</span><span class="sxs-lookup"><span data-stu-id="70354-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="70354-134">Windows 7 veya Windows Server 2008 R2 64-bit sürümünü (veya üstü)</span><span class="sxs-lookup"><span data-stu-id="70354-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="70354-135">**Önerilen**:</span><span class="sxs-lookup"><span data-stu-id="70354-135">**Recommended**:</span></span>

* <span data-ttu-id="70354-136">8 çekirdekli CPU</span><span class="sxs-lookup"><span data-stu-id="70354-136">8 Core CPU</span></span>
* <span data-ttu-id="70354-137">8 GB bellek</span><span class="sxs-lookup"><span data-stu-id="70354-137">8 GB Memory</span></span>
* <span data-ttu-id="70354-138">64 bit sürümü Windows 2012 R2'in (veya üstü)</span><span class="sxs-lookup"><span data-stu-id="70354-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="70354-139">**İle ilgili önemli noktalar**:</span><span class="sxs-lookup"><span data-stu-id="70354-139">**Important considerations**:</span></span>

* <span data-ttu-id="70354-140">Merhaba şirket içi veri ağ geçidi yalnızca yerel bir bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="70354-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="70354-141">Merhaba ağ geçidi etki alanı denetleyicisine yükleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="70354-142">Merhaba üzerinde tooinstall hello ağ geçidi yok veri kaynağınız ile aynı bilgisayara.</span><span class="sxs-lookup"><span data-stu-id="70354-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="70354-143">toominimize gecikme, olası tooyour veri kaynağı olarak ya da hello aynı kapatmak gibi hello ağ geçidi yükleyebilirsiniz izinleri olduğunu varsayarak bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="70354-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="70354-144">Merhaba ağ geçidi kapanmadan toosleep geçip geçmeyeceğini veya hello ağ geçidi bu koşullarda çalıştığından toohello Internet bağlanmıyor bir bilgisayarda yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="70354-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="70354-145">Ayrıca, kablosuz ağ üzerinden ağ geçidi performansı düşebilir.</span><span class="sxs-lookup"><span data-stu-id="70354-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="70354-146">Yükleme sırasında bilgileriyle oturum açmalıdır bir [iş veya Okul hesabı](https://docs.microsoft.com/azure/active-directory/sign-up-organization) Azure Active Directory tarafından (Azure AD), bir Microsoft hesabı yönetilir.</span><span class="sxs-lookup"><span data-stu-id="70354-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="70354-147">Merhaba aynı iş veya Okul hesabı daha sonra da hello Azure toouse sahip oluşturduğunuzda ve bir ağ geçidi kaynağı ile ağ geçidi yüklemenizi ilişkilendirmek portal.</span><span class="sxs-lookup"><span data-stu-id="70354-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="70354-148">Logic app ve hello şirket içi veri kaynağınız arasında hello bağlantı oluşturduğunuzda, ardından bu ağ geçidi kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="70354-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="70354-149">Neden gerekir t bir Azure AD iş veya Okul hesabı?</span><span class="sxs-lookup"><span data-stu-id="70354-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="70354-150">Bir Office 365 teklif için kaydolan ve gerçek iş e-sağlamadı, oturum açma adresinizi nasıl görünebileceği jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="70354-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="70354-151">14.16.6317.4 sürümden daha eski bir yükleyici ile ayarladığınız mevcut bir ağ geçidi varsa, ağ geçidinizin konum çalışan hello son yükleyici tarafından değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="70354-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="70354-152">Ancak, bunun yerine istediğiniz başlangıç konumu ile Merhaba son yükleyici tooset yeni bir ağ geçidi yukarı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="70354-153">14.16.6317.4 sürümden daha eski bir ağ geçidi yükleyicisi varsa, ancak ağ geçidiniz yüklemediniz henüz indirebilir ve hello son yükleyiciyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="70354-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="70354-154">Merhaba data gateway yükleyin</span><span class="sxs-lookup"><span data-stu-id="70354-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="70354-155">[Karşıdan yükle ve yerel bilgisayarda hello ağ geçidi yükleyicisi çalıştırın](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="70354-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="70354-156">Gözden geçirin ve kullanım ve gizlilik bildirimini hello koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="70354-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="70354-157">Merhaba yolu, yerel bilgisayarınızda tooinstall hello ağ geçidi istediğiniz yeri belirtin.</span><span class="sxs-lookup"><span data-stu-id="70354-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="70354-158">İstendiğinde, Azure iş veya Okul hesabı, bir Microsoft hesabı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="70354-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Oturum oturum Azure iş veya Okul hesabı](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="70354-160">Yüklü ağ geçidiniz ile Merhaba kaydettirmek [ağ geçidi bulut Hizmeti'ne](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="70354-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="70354-161">Seçin **bu bilgisayarda yeni bir ağ geçidini kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="70354-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="70354-162">Merhaba ağ geçidi bulut Hizmeti'ne şifreler ve veri kaynağı kimlik bilgilerini ve ağ geçidi ayrıntıları depolar.</span><span class="sxs-lookup"><span data-stu-id="70354-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="70354-163">Merhaba hizmeti, şirket içinde sorguları ve sonuçları mantıksal uygulamanızı, hello şirket içi veri ağ geçidi ve veri kaynağınız arasında da yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="70354-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="70354-164">Ağ geçidi yüklemeniz için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="70354-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="70354-165">Bir kurtarma anahtarı oluşturun, sonra kurtarma anahtarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="70354-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="70354-166">Kurtarma anahtarı en az sekiz karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="70354-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="70354-167">Kaydet ve başlangıç anahtarı güvenli bir yerde sakladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="70354-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="70354-168">Toomigrate, istediğinizde de bu anahtarı ihtiyacınız geri yüklemek veya mevcut bir ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="70354-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="70354-169">Merhaba ağ geçidi bulut Hizmeti'ne ve ağ geçidi yüklemenizi tarafından kullanılan Azure Service Bus toochange hello varsayılan bölgesini seçin **değişikliğin bölgesini**.</span><span class="sxs-lookup"><span data-stu-id="70354-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Değişiklik bölgesi](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="70354-171">Merhaba varsayılan bölge, Azure AD Kiracı ile ilişkilendirilen hello bölgedir.</span><span class="sxs-lookup"><span data-stu-id="70354-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="70354-172">Merhaba Hello sonraki bölmesinde açmak **seçin bölge** çok farklı bir bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="70354-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Başka bir bölge seçin](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="70354-174">Örneğin, select mantıksal uygulamanızı aynı bölgede hello ya da select hello bölgeye en yakın tooyour şirket içi veri kaynağı gecikme süresini azaltmak için.</span><span class="sxs-lookup"><span data-stu-id="70354-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="70354-175">Ağ geçidi kaynak ve mantıksal uygulamanızı farklı konumlarda olabilir.</span><span class="sxs-lookup"><span data-stu-id="70354-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="70354-176">Yükleme sonrasında bu bölgeyi değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-176">You can't change this region after installation.</span></span> <span data-ttu-id="70354-177">Bu bölge ayrıca belirler ve hello Azure kaynak ağ geçidiniz için oluşturabileceğiniz hello konumu kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="70354-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="70354-178">Bu nedenle, ağ geçidi kaynağı Azure'da oluşturduğunuzda, hello kaynak konumu ağ geçidi yüklemesi sırasında seçilen hello bölge eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="70354-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="70354-179">Ağ geçidiniz için daha sonra farklı bir bölgeye toouse istiyorsanız, yeni bir ağ geçidi kurun ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="70354-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="70354-180">Hazır olduğunuzda, seçin **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="70354-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="70354-181">Şimdi, böylece hello Azure Portalı'nda aşağıdaki adımları izleyin [ağ geçidiniz için bir Azure kaynağı oluşturma](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="70354-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="70354-182">Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="70354-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="70354-183">Geçirme, geri yüklemek veya mevcut bir ağ geçidi alın</span><span class="sxs-lookup"><span data-stu-id="70354-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="70354-184">Bu görevler tooperform hello ağ geçidi yüklendiğinde, belirttiğiniz hello kurtarma anahtarı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70354-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="70354-185">Bilgisayarınızın Başlat menüsünden seçin **şirket içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="70354-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="70354-186">Merhaba yükleyici açılır oturumu ile sonra hello aynı Azure iş veya tooinstall hello ağ geçidi önceden Okul hesabı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70354-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="70354-187">Seçin **geçirme, geri yükleme veya mevcut bir ağ geçidi üzerinden Al**.</span><span class="sxs-lookup"><span data-stu-id="70354-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="70354-188">Üzerinden toomigrate, restore veya Al istediğiniz hello ağ geçidi için Hello adı ve kurtarma anahtarı sağlayın.</span><span class="sxs-lookup"><span data-stu-id="70354-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="70354-189">Merhaba ağ geçidini yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="70354-189">Restart hello gateway</span></span>

<span data-ttu-id="70354-190">Merhaba ağ geçidi, bir Windows hizmet olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="70354-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="70354-191">Diğer Windows hizmeti gibi başlatın ve birden çok yolla hello hizmetini durdurun.</span><span class="sxs-lookup"><span data-stu-id="70354-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="70354-192">Örneğin, hello ağ geçidi çalıştığı hello bilgisayarda yükseltilmiş izinleri olan bir komut istemi açın ve ya da şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70354-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="70354-193">toostop hello hizmeti, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70354-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="70354-194">toostart hello hizmeti, şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70354-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="70354-195">Windows hizmet hesabı</span><span class="sxs-lookup"><span data-stu-id="70354-195">Windows service account</span></span>

<span data-ttu-id="70354-196">Merhaba şirket içi veri ağ geçidi toouse ayarlanmış `NT SERVICE\PBIEgwService` hello Windows hizmeti oturum açma kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="70354-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="70354-197">Varsayılan olarak, hello ağ geçidi yüklediğiniz hello ağ geçidi hello "hizmet olarak oturum aç" hakkına hello makine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="70354-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="70354-198">Okul hesabı toosign toocloud Hizmetleri'nde kullanılan veya Hello Windows hizmet hesabını tooon içi veri kaynaklarına bağlanmak için kullanılan hello hesabından ve hello Azure çalışma alanından farklı.</span><span class="sxs-lookup"><span data-stu-id="70354-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="70354-199">Bir güvenlik duvarı veya proxy yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70354-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="70354-200">Merhaba ağ geçidi oluşturur giden bir bağlantıyı çok [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="70354-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="70354-201">tooprovide proxy bilgi, ağ geçidi için [proxy ayarlarını yapılandırma](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="70354-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="70354-202">toocheck güvenlik duvarı veya proxy bağlantıları, engelleyebilecek olup olmadığını doğrulayın makinenizin toohello gerçekten bağlanıp bağlanamayacağını Internet ve hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="70354-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="70354-203">Bir PowerShell isteminden şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="70354-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="70354-204">Bu komut, yalnızca bir ağ bağlantısı ve bağlantı toohello Azure Service Bus'test eder.</span><span class="sxs-lookup"><span data-stu-id="70354-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="70354-205">Merhaba komutu herhangi bir şey yok şekilde hello ağ geçidi veya şifreler ve kimlik bilgilerinizi ve ağ geçidi ayrıntıları depolayan hello ağ geçidi bulut hizmeti ile toodo.</span><span class="sxs-lookup"><span data-stu-id="70354-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="70354-206">Ayrıca, bu komut yalnızca Windows Server 2012 R2 veya daha sonra kullanılabilir ve Windows 8.1 veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="70354-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="70354-207">Önceki işletim sistemi sürümlerinde, Telnet kullanabileceğiniz çok bağlantısını test edin.</span><span class="sxs-lookup"><span data-stu-id="70354-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="70354-208">Daha fazla bilgi edinmek [Azure Service Bus ve karma çözümleri](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="70354-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="70354-209">Sonuçlarınızı benzer toothis örnek gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="70354-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="70354-210">Varsa **TcpTestSucceeded** çok ayarlanmadı**doğru**, güvenlik duvarı tarafından engellenmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="70354-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="70354-211">Toobe kapsamlı istiyorsanız hello yerine **ComputerName** ve **bağlantı noktası** altında listelenen değerleri hello değerlerle [bağlantı noktalarını yapılandırma](#configure-ports) bu konuda.</span><span class="sxs-lookup"><span data-stu-id="70354-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="70354-212">Merhaba Güvenlik Duvarı'nı Azure Service Bus toohello Azure veri merkezleri yapar, hello bağlantıları engelliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="70354-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="70354-213">Bu senaryo durumda Onayla (engelini kaldırma) tüm IP adresleri için bu veri merkezleri, bölgenizdeki hello.</span><span class="sxs-lookup"><span data-stu-id="70354-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="70354-214">Bu IP adresleri için [get hello Azure IP adreslerinin listesi burada](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="70354-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="70354-215">Bağlantı noktalarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="70354-215">Configure ports</span></span>

<span data-ttu-id="70354-216">Merhaba ağ geçidi oluşturur giden bir bağlantıyı çok[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) ve giden bağlantı noktaları iletişim kurar: TCP 443 (varsayılan), 5671, 5672, 9354 aracılığıyla 9350.</span><span class="sxs-lookup"><span data-stu-id="70354-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="70354-217">Merhaba ağ geçidi gelen bağlantı noktalarının gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="70354-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="70354-218">Daha fazla bilgi edinmek [Azure Service Bus ve karma çözümleri](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="70354-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="70354-219">ETKİ ALANI ADLARI</span><span class="sxs-lookup"><span data-stu-id="70354-219">DOMAIN NAMES</span></span> | <span data-ttu-id="70354-220">GİDEN BAĞLANTI NOKTALARI</span><span class="sxs-lookup"><span data-stu-id="70354-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="70354-221">AÇIKLAMA</span><span class="sxs-lookup"><span data-stu-id="70354-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70354-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="70354-222">*.analysis.windows.net</span></span> | <span data-ttu-id="70354-223">443</span><span class="sxs-lookup"><span data-stu-id="70354-223">443</span></span> | <span data-ttu-id="70354-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70354-224">HTTPS</span></span> | 
| <span data-ttu-id="70354-225">*. login.windows.net</span><span class="sxs-lookup"><span data-stu-id="70354-225">*.login.windows.net</span></span> | <span data-ttu-id="70354-226">443</span><span class="sxs-lookup"><span data-stu-id="70354-226">443</span></span> | <span data-ttu-id="70354-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70354-227">HTTPS</span></span> | 
| <span data-ttu-id="70354-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="70354-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="70354-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="70354-229">5671-5672</span></span> | <span data-ttu-id="70354-230">Gelişmiş Message Queuing Protokolü (AMQP)</span><span class="sxs-lookup"><span data-stu-id="70354-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="70354-231">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="70354-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="70354-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="70354-232">443, 9350-9354</span></span> | <span data-ttu-id="70354-233">Hizmet veri yolu geçişi (erişim denetimi belirteci alımı için 443'ü gerektirir) TCP üzerinden üzerindeki dinleyicileri</span><span class="sxs-lookup"><span data-stu-id="70354-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="70354-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="70354-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="70354-235">443</span><span class="sxs-lookup"><span data-stu-id="70354-235">443</span></span> | <span data-ttu-id="70354-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70354-236">HTTPS</span></span> | 
| <span data-ttu-id="70354-237">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="70354-237">*.core.windows.net</span></span> | <span data-ttu-id="70354-238">443</span><span class="sxs-lookup"><span data-stu-id="70354-238">443</span></span> | <span data-ttu-id="70354-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70354-239">HTTPS</span></span> | 
| <span data-ttu-id="70354-240">Login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="70354-240">login.microsoftonline.com</span></span> | <span data-ttu-id="70354-241">443</span><span class="sxs-lookup"><span data-stu-id="70354-241">443</span></span> | <span data-ttu-id="70354-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="70354-242">HTTPS</span></span> | 
| <span data-ttu-id="70354-243">*. msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="70354-243">*.msftncsi.com</span></span> | <span data-ttu-id="70354-244">443</span><span class="sxs-lookup"><span data-stu-id="70354-244">443</span></span> | <span data-ttu-id="70354-245">Merhaba ağ geçidi hello Power BI hizmeti tarafından erişilemiyor tootest internet bağlantısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70354-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="70354-246">Merhaba etki alanları yerine tooapprove IP adresine sahip değilse, indirin ve hello kullan [Microsoft Azure veri merkezi IP aralıkları listesi](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="70354-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="70354-247">Bazı durumlarda, tam etki alanı adı yerine IP adresi ile hello Azure hizmet veri yolu bağlantıları hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="70354-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="70354-248">Merhaba veri ağ geçidi nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="70354-248">How does hello data gateway work?</span></span>

<span data-ttu-id="70354-249">Merhaba veri ağ geçidi mantıksal uygulamanızı, hello ağ geçidi bulut Hizmeti'ne ve şirket içi veri kaynağınız arasında hızlı ve güvenli iletişimi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="70354-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![Diagram-for-on-Premises-Data-Gateway-Flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="70354-251">Bu nedenle zaman hello kullanıcı hello bulutta tooyour bağlı olduğu bir öğesiyle etkileşim veri kaynağı şirket içi:</span><span class="sxs-lookup"><span data-stu-id="70354-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="70354-252">Merhaba ağ geçidi bulut Hizmeti'ne hello şifrelenmiş kimlik bilgileri hello veri kaynağı için birlikte bir sorgu oluşturur ve hello sorgu toohello sıra hello ağ geçidi tooprocess için gönderir.</span><span class="sxs-lookup"><span data-stu-id="70354-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="70354-253">Merhaba ağ geçidi bulut Hizmeti'ne hello sorgu analiz eder ve hello isteği toohello Azure Service Bus iter.</span><span class="sxs-lookup"><span data-stu-id="70354-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="70354-254">Merhaba şirket içi veri ağ geçidi hello Azure hizmet veri yolu için bekleyen istekler yoklar.</span><span class="sxs-lookup"><span data-stu-id="70354-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="70354-255">Merhaba ağ geçidi hello sorgu alır, hello kimlik şifresini çözer ve söz konusu kimlik bilgileriyle toohello veri kaynağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="70354-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="70354-256">Merhaba ağ geçidi hello sorgu toohello veri kaynağı için yürütme gönderir.</span><span class="sxs-lookup"><span data-stu-id="70354-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="70354-257">Merhaba sonuçları hello veri kaynağı, geri toohello ağ geçidi ve toohello ağ geçidi bulut Hizmeti'ne sonra gönderilir.</span><span class="sxs-lookup"><span data-stu-id="70354-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="70354-258">Merhaba ağ geçidi bulut Hizmeti'ne sonra hello sonuçları kullanır.</span><span class="sxs-lookup"><span data-stu-id="70354-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="70354-259">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="70354-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="70354-260">Genel</span><span class="sxs-lookup"><span data-stu-id="70354-260">General</span></span>

<span data-ttu-id="70354-261">**Q**: bir ağ geçidi için SQL Azure gibi hello bulut veri kaynaklarında ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="70354-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="70354-262">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="70354-262">
**A**: No.</span></span> <span data-ttu-id="70354-263">Bir ağ geçidi tooon içi veri kaynakları yalnızca bağlanır.</span><span class="sxs-lookup"><span data-stu-id="70354-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="70354-264">**Q**: hello ağ geçidi aynı makine hello veri kaynağı olarak hello yüklü toobe sahip mi?</span><span class="sxs-lookup"><span data-stu-id="70354-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="70354-265">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="70354-265">
**A**: No.</span></span> <span data-ttu-id="70354-266">Merhaba ağ geçidi sağlanan hello bağlantı bilgilerini kullanarak toohello veri kaynağına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="70354-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="70354-267">Bu bağlamda bir istemci uygulaması olarak Hello ağ geçidi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="70354-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="70354-268">Merhaba ağ geçidi yalnızca sağlanan hello yetenek tooconnect toohello sunucu adı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="70354-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="70354-269">**Q**: neden gerekir t bir Azure okul veya iş hesabı toosign?</span><span class="sxs-lookup"><span data-stu-id="70354-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="70354-270">
**A**: yalnızca Azure bir iş veya Okul hesabınız hello şirket içi veri ağ geçidi yüklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="70354-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="70354-271">Oturum açma hesabınızın Azure Active Directory (Azure AD) tarafından yönetilen bir kiracı depolanır.</span><span class="sxs-lookup"><span data-stu-id="70354-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="70354-272">Genellikle, Azure AD hesabınızın kullanıcı asıl adı (UPN) hello e-posta adresi ile eşleşir.</span><span class="sxs-lookup"><span data-stu-id="70354-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="70354-273">**Q**: kimlik bilgilerimi depolandığı?</span><span class="sxs-lookup"><span data-stu-id="70354-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="70354-274">
**A**: bir veri kaynağı için girdiğiniz hello kimlik bilgileri şifrelenir ve hello ağ geçidi bulut hizmetinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="70354-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="70354-275">Merhaba kimlik hello şirket içi veri ağ geçidi şifresi çözülür.</span><span class="sxs-lookup"><span data-stu-id="70354-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="70354-276">**Q**: ağ bant genişliği için tüm gereksinimleri vardır?</span><span class="sxs-lookup"><span data-stu-id="70354-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="70354-277">
**A**: ağ bağlantısı iyi üretilen işi olan öneririz.</span><span class="sxs-lookup"><span data-stu-id="70354-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="70354-278">Her ortam farklıdır ve gönderilen verilerin miktarını hello hello sonuçları etkiler.</span><span class="sxs-lookup"><span data-stu-id="70354-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="70354-279">ExpressRoute kullanarak şirket içi ve hello Azure veri merkezleri arasında işleme düzeyini tooguarantee yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="70354-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="70354-280">Merhaba üçüncü taraf aracı Azure hızı Test uygulama toohelp ölçer, üretilen iş kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="70354-281">**Q**: hello gecikmesi çalışan sorguları tooa veri kaynağından hello ağ geçidi nedir?</span><span class="sxs-lookup"><span data-stu-id="70354-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="70354-282">Merhaba en iyi mimarisi nedir?</span><span class="sxs-lookup"><span data-stu-id="70354-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="70354-283">
**A**: tooreduce ağ gecikmesi, mümkün olduğunca yakın toohello veri kaynağı olarak yükleme hello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="70354-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="70354-284">Merhaba gerçek veri kaynağında hello ağ geçidi yükleyebilirsiniz, bu yakınlık sunulan hello gecikme süresi en aza indirir.</span><span class="sxs-lookup"><span data-stu-id="70354-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="70354-285">Merhaba veri merkezleri çok göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="70354-285">Consider hello datacenters too.</span></span> <span data-ttu-id="70354-286">Örneğin, hizmetiniz hello Batı ABD datacenter kullanır ve SQL Server'ın bir Azure VM ile barındırılan olması durumunda, Azure VM hello Batı ABD çok olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70354-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="70354-287">Bu yakınlık gecikme süresi en aza indirir ve çıkış ücretlerini hello Azure VM üzerinde önler.</span><span class="sxs-lookup"><span data-stu-id="70354-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="70354-288">**Q**: gönderilen sonuçları geri toohello bulut şeklini?</span><span class="sxs-lookup"><span data-stu-id="70354-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="70354-289">
**A**: sonuçları hello Azure Service Bus gönderilir.</span><span class="sxs-lookup"><span data-stu-id="70354-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="70354-290">**Q**: tüm gelen bağlantıları toohello ağ geçidi'nden hello bulut vardır?</span><span class="sxs-lookup"><span data-stu-id="70354-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="70354-291">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="70354-291">
**A**: No.</span></span> <span data-ttu-id="70354-292">Merhaba ağ geçidi giden bağlantılar tooAzure hizmet veri yolu kullanır.</span><span class="sxs-lookup"><span data-stu-id="70354-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="70354-293">**Q**: ne ı giden bağlantıları engelle?</span><span class="sxs-lookup"><span data-stu-id="70354-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="70354-294">Ne tooopen gerekir?</span><span class="sxs-lookup"><span data-stu-id="70354-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="70354-295">
**A**: hello bağlantı noktaları ve ağ geçidi kullanan hello konakları bakın.</span><span class="sxs-lookup"><span data-stu-id="70354-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="70354-296">**Q**: ne hello gerçek Windows hizmeti adı verilir?</span><span class="sxs-lookup"><span data-stu-id="70354-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="70354-297">
**A**: Services'de hello ağ geçidi Power BI kurumsal ağ geçidi hizmeti olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="70354-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="70354-298">**Q**: ağ geçidi Windows hizmeti bir Azure Active Directory hesap ile çalıştırmak hello?</span><span class="sxs-lookup"><span data-stu-id="70354-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="70354-299">
**A**: Hayır</span><span class="sxs-lookup"><span data-stu-id="70354-299">
**A**: No.</span></span> <span data-ttu-id="70354-300">Merhaba Windows hizmeti geçerli bir Windows hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70354-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="70354-301">Varsayılan olarak, hello ile hizmet SID, NT SERVICE\PBIEgwService hello hizmeti çalışır.</span><span class="sxs-lookup"><span data-stu-id="70354-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="70354-302">Yüksek kullanılabilirlik ve olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="70354-302">High availability and disaster recovery</span></span>

<span data-ttu-id="70354-303">**Q**: olağanüstü durum kurtarma için kullanılabilir seçenekleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="70354-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="70354-304">
**A**: hello kurtarma anahtarı toorestore kullanın veya bir ağ geçidi taşıyın.</span><span class="sxs-lookup"><span data-stu-id="70354-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="70354-305">Merhaba ağ geçidi yüklediğinizde hello kurtarma anahtarını belirtin.</span><span class="sxs-lookup"><span data-stu-id="70354-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="70354-306">**Q**: hello kurtarma anahtarı hello avantajı nedir?</span><span class="sxs-lookup"><span data-stu-id="70354-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="70354-307">
**A**: hello kurtarma anahtarı bir şekilde toomigrate sağlar veya ağ geçidi ayarlarınızı sonra bir olağanüstü durum kurtarma.</span><span class="sxs-lookup"><span data-stu-id="70354-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="70354-308">**Q**: hello ağ geçidi ile yüksek kullanılabilirlik senaryolarını etkinleştirmek için herhangi bir plan vardır?</span><span class="sxs-lookup"><span data-stu-id="70354-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="70354-309">
**A**: hello yol haritası üzerinde bu senaryolar verilmiştir ancak henüz bir zaman çizelgesi bulunmuyor.</span><span class="sxs-lookup"><span data-stu-id="70354-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="70354-310">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="70354-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="70354-311">**Q**: nasıl sorguları toohello şirket içi veri kaynağına gönderilen görebilir?</span><span class="sxs-lookup"><span data-stu-id="70354-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="70354-312">
**A**: gönderilen hello sorgular sorgu izlemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="70354-313">Sorun giderme tamamlanınca toohello özgün değeri geri izleme toochange sorgu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="70354-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="70354-314">Sorgu izlemesi açık bırakarak daha büyük günlükleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="70354-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="70354-315">Ayrıca, izleme sorguları için veri kaynağınız olan araçlar da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="70354-316">Örneğin, SQL Server ve Analysis Services için genişletilmiş olaylar veya SQL Profiler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="70354-317">**Q**: hello gateway günlükleri nerede?</span><span class="sxs-lookup"><span data-stu-id="70354-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="70354-318">
**A**: Bu konunun ilerleyen bölümlerinde bkz araçları.</span><span class="sxs-lookup"><span data-stu-id="70354-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="70354-319">Güncelleştirme toohello en son sürümü</span><span class="sxs-lookup"><span data-stu-id="70354-319">Update toohello latest version</span></span>

<span data-ttu-id="70354-320">Merhaba ağ geçidi sürümü güncel olmayan hale geldiğinde birçok sorunları ortaya.</span><span class="sxs-lookup"><span data-stu-id="70354-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="70354-321">Genel iyi uygulama olarak, hello en son sürümünü kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="70354-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="70354-322">Merhaba ağ geçidi için ayda bir veya daha uzun güncelleştirmediyseniz hello hello ağ geçidinin en son sürümünü yüklemeyi göz önünde bulundurun ve hello sorunu yeniden bakın.</span><span class="sxs-lookup"><span data-stu-id="70354-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="70354-323">Hata: tooadd kullanıcı toogroup başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="70354-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="70354-324">(-2147463168 PBIEgwService performans günlük kullanıcılar)</span><span class="sxs-lookup"><span data-stu-id="70354-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="70354-325">Desteklenmeyen bir etki alanı denetleyicisinde tooinstall hello ağ geçidi çalışırsanız, bu hatayı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="70354-326">Bir etki alanı denetleyicisi olmayan bir makineyi hello geçidinde dağıttığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="70354-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="70354-327">Araçlar</span><span class="sxs-lookup"><span data-stu-id="70354-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="70354-328">Merhaba ağ geçidi configurer günlüklerini toplayın</span><span class="sxs-lookup"><span data-stu-id="70354-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="70354-329">Merhaba ağ geçidi için birkaç günlüklerini toplayabilir.</span><span class="sxs-lookup"><span data-stu-id="70354-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="70354-330">Her zaman hello günlükleri ile başlayın!</span><span class="sxs-lookup"><span data-stu-id="70354-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="70354-331">Yükleyici günlükleri</span><span class="sxs-lookup"><span data-stu-id="70354-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="70354-332">Yapılandırma günlükleri</span><span class="sxs-lookup"><span data-stu-id="70354-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="70354-333">Kurumsal ağ geçidi hizmeti günlükleri</span><span class="sxs-lookup"><span data-stu-id="70354-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="70354-334">Olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="70354-334">Event logs</span></span>

<span data-ttu-id="70354-335">Veri Yönetimi ağ geçidi ve PowerBIGateway günlüklerini altında hello bulabilirsiniz **uygulama ve hizmet günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="70354-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="70354-336">Fiddler'ı izleme</span><span class="sxs-lookup"><span data-stu-id="70354-336">Fiddler Trace</span></span>

<span data-ttu-id="70354-337">[Fiddler](http://www.telerik.com/fiddler) HTTP trafiği izler telerik'ten ücretsiz bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="70354-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="70354-338">Merhaba hello istemci makineden Power BI hizmeti ile bu trafiği görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70354-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="70354-339">Bu hizmet, hataları ve diğer ilgili bilgileri gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="70354-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70354-340">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="70354-340">Next steps</span></span>
    
* [<span data-ttu-id="70354-341">Mantığı uygulamalardan tooon içi verilere bağlanma</span><span class="sxs-lookup"><span data-stu-id="70354-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="70354-342">Kurumsal tümleştirme özellikleri</span><span class="sxs-lookup"><span data-stu-id="70354-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="70354-343">Azure mantıksal uygulamaları için bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="70354-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
