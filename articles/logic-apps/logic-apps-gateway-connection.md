---
title: "Şirket içi Azure Logic Apps için aaaAccess veri kaynakları | Microsoft Docs"
description: "Merhaba şirket içi veri ağ geçidi mantığı uygulamalardan şirket içi veri kaynaklarına erişebilmesi için ayarlama"
keywords: "Şirket içi veri aktarımı, şifreleme, veri kaynakları veri erişimi"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="cdc99-104">Şirket içi hello şirket içi veri ağ geçidi ile mantığı uygulamalardan veri kaynaklarına erişim</span><span class="sxs-lookup"><span data-stu-id="cdc99-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="cdc99-105">Şirket içi mantığı uygulamalarınızdan tooaccess veri kaynakları ile desteklenen bağlayıcılar mantıksal uygulamaları kullanan şirket içi veri ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cdc99-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="cdc99-106">Merhaba ağ geçidi hızlı veri aktarımı ve logic apps ile şirket içi veri kaynakları arasındaki şifreleme sağlayan köprü gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="cdc99-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="cdc99-107">Merhaba ağ geçidi şifrelenmiş kanalda hello Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="cdc99-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="cdc99-108">Güvenli giden trafiği hello ağ geçidi aracısından olarak tüm trafiğin kaynaklandığı.</span><span class="sxs-lookup"><span data-stu-id="cdc99-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="cdc99-109">Daha fazla bilgi edinmek [hello veri ağ geçidi nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="cdc99-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="cdc99-110">Merhaba ağ geçidi bağlantıları toothese veri kaynakları şirket içinde destekler:</span><span class="sxs-lookup"><span data-stu-id="cdc99-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="cdc99-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdc99-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="cdc99-112">DB2</span><span class="sxs-lookup"><span data-stu-id="cdc99-112">DB2</span></span>  
*   <span data-ttu-id="cdc99-113">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="cdc99-113">File System</span></span>
*   <span data-ttu-id="cdc99-114">Informix</span><span class="sxs-lookup"><span data-stu-id="cdc99-114">Informix</span></span>
*   <span data-ttu-id="cdc99-115">MQ</span><span class="sxs-lookup"><span data-stu-id="cdc99-115">MQ</span></span>
*   <span data-ttu-id="cdc99-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="cdc99-116">MySQL</span></span>
*   <span data-ttu-id="cdc99-117">Oracle Veritabanı</span><span class="sxs-lookup"><span data-stu-id="cdc99-117">Oracle Database</span></span>
*   <span data-ttu-id="cdc99-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="cdc99-118">PostgreSQL</span></span>
*   <span data-ttu-id="cdc99-119">SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="cdc99-119">SAP Application Server</span></span> 
*   <span data-ttu-id="cdc99-120">SAP ileti sunucusu</span><span class="sxs-lookup"><span data-stu-id="cdc99-120">SAP Message Server</span></span>
*   <span data-ttu-id="cdc99-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="cdc99-121">SharePoint</span></span>
*   <span data-ttu-id="cdc99-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="cdc99-122">SQL Server</span></span>
*   <span data-ttu-id="cdc99-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="cdc99-123">Teradata</span></span>

<span data-ttu-id="cdc99-124">Bu adımlar nasıl hello yukarı tooset veri ağ geçidi toowork logic apps ile şirket içi gösterir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="cdc99-125">Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="cdc99-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="cdc99-126">Nasıl toouse hello diğer hizmetler ile ağ geçidi hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="cdc99-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="cdc99-127">Microsoft Power BI şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="cdc99-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="cdc99-128">Azure Analysis Services veri ağ geçidi şirket içi</span><span class="sxs-lookup"><span data-stu-id="cdc99-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="cdc99-129">Microsoft Flow şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="cdc99-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="cdc99-130">Microsoft PowerApps şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="cdc99-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="cdc99-131">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="cdc99-131">Requirements</span></span>

* <span data-ttu-id="cdc99-132">Önceden olmalıdır [hello veri ağ geçidi yerel bir bilgisayarda yüklü](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cdc99-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="cdc99-133">Toohello Azure portalında oturum açtığınızda hello aynı iş veya Okul çok kullanılan hesap toouse sahip[hello şirket içi veri ağ geçidi yükleme](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="cdc99-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="cdc99-134">Ağ geçidi yüklemenize hello Azure portalında bir ağ geçidi kaynak oluşturduğunuzda, oturum açma hesabı ayrıca bir Azure aboneliği toouse sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cdc99-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="cdc99-135">Ağ geçidi yüklemenizi zaten bir Azure ağ geçidi kaynağı tarafından istenemiyor.</span><span class="sxs-lookup"><span data-stu-id="cdc99-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="cdc99-136">Ağ geçidi yükleme tooonly bir Azure ağ geçidi kaynağınız ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc99-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="cdc99-137">Böylece Hello yükleme için diğer kaynaklar kullanılamıyor hello ağ geçidi kaynağı oluşturmak talep olur.</span><span class="sxs-lookup"><span data-stu-id="cdc99-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="cdc99-138">Merhaba veri ağ geçidi bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="cdc99-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="cdc99-139">1. Merhaba şirket içi veri ağ geçidi yükleyin</span><span class="sxs-lookup"><span data-stu-id="cdc99-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="cdc99-140">Henüz yapmadıysanız, hello izleyin [adımları tooinstall hello şirket içi veri ağ geçidi](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cdc99-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="cdc99-141">Merhaba ile devam etmeden önce diğer adımlar, yerel bir bilgisayarda hello veri ağ geçidi yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cdc99-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="cdc99-142">2. Merhaba şirket içi veri ağ geçidi için bir Azure kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cdc99-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="cdc99-143">Yerel bir bilgisayarda hello ağ geçidi yükledikten sonra bir kaynak olarak Azure data gateway oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="cdc99-144">Bu adım, ağ geçidi kaynağı ayrıca Azure aboneliğiniz ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="cdc99-145">İçinde toohello oturum [Azure portal](https://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="cdc99-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="cdc99-146">Toouse hello aynı Azure iş veya Okul e-posta adresi tooinstall hello ağ geçidi kullanılan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cdc99-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="cdc99-147">Merhaba sol menüsünde Azure, **yeni** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="cdc99-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !["Şirket içi veri ağ geçidi" Bul](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="cdc99-149">Merhaba üzerinde **oluşturma bağlantı ağ geçidi** dikey penceresinde, bu ayrıntıları toocreate veri ağ geçidi kaynağı sağlar:</span><span class="sxs-lookup"><span data-stu-id="cdc99-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="cdc99-150">**Ad**: ağ geçidi kaynağı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="cdc99-151">**Abonelik**: seçin, ağ geçidi kaynağı ile Azure aboneliği tooassociate hello.</span><span class="sxs-lookup"><span data-stu-id="cdc99-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="cdc99-152">Bu abonelik olmalıdır hello mantıksal uygulamanızı aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="cdc99-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="cdc99-153">Merhaba varsayılan abonelik hello toosign içinde kullanılan Azure hesabı temel alır.</span><span class="sxs-lookup"><span data-stu-id="cdc99-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="cdc99-154">**Kaynak grubu**: bir kaynak grubu oluşturun veya varolan bir kaynak grubu, ağ geçidi kaynağı dağıtmak için seçin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="cdc99-155">Kaynak grupları ilgili Azure varlıklar koleksiyonu olarak yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cdc99-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="cdc99-156">**Konum**: Azure kısıtlayan bu konumu toohello sırasında hello ağ geçidi bulut hizmeti için seçtiğiniz aynı bölgede [ağ geçidi yükleme](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="cdc99-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="cdc99-157">Merhaba ağ geçidi kaynak konumu hello ağ geçidi bulut hizmeti konumu eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="cdc99-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="cdc99-158">Aksi takdirde, ağ geçidi yüklemenizi hello yüklü ağ geçitleri listesinde, tooselect hello sonraki adımda görünmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="cdc99-159">Farklı bölgelerde mantıksal uygulamanızı ve ağ geçidi kaynağı için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc99-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="cdc99-160">**Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, daha önce yüklediğiniz hello ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="cdc99-161">tooadd hello ağ geçidi kaynak tooyour Azure Pano seçin **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="cdc99-162">İşiniz bittiğinde seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="cdc99-163">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="cdc99-163">For example:</span></span>

    ![Şirket içi data gateway ayrıntıları toocreate sağlayın](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="cdc99-165">toofind veya görünümde herhangi bir zamanda data gateway hello ana Azure sol menüsünden Git çok **daha Hizmetleri** > **Kurumsal tümleştirme** > **şirket içi veri Ağ geçitleri**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Çok Git "Daha fazla Hizmetleri", "Kurumsal tümleştirme", "Şirket içi veri ağ geçidi"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="cdc99-167">3. Mantıksal uygulama toohello şirket içi data gateway Bağlan</span><span class="sxs-lookup"><span data-stu-id="cdc99-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="cdc99-168">Veri ağ geçidi kaynağı oluşturulur ve Azure aboneliğiniz bu kaynakla ilişkili göre logic app ve hello data gateway arasında bir bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cdc99-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="cdc99-169">Ağ geçidi bağlantı konumunuz hello aynı bulunmalıdır bölgeye mantıksal uygulamanızı, ancak farklı bir bölgede mevcut bir veri ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc99-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="cdc99-170">Hello Azure portal, oluşturun veya mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.</span><span class="sxs-lookup"><span data-stu-id="cdc99-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="cdc99-171">SQL Server gibi şirket içi bağlantıları destekleyen bir bağlayıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="cdc99-172">Gösterilen hello sırasının seçin **Connect şirket içi veri ağ geçidi üzerinden**benzersiz bağlantı adı belirtin ve hello gerekli bilgileri ve hello veri ağ geçidi kaynağı toouse istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="cdc99-173">İşiniz bittiğinde seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="cdc99-174">Benzersiz bağlantı adı özellikle birden çok bağlantı oluşturduğunuzda bu bağlantıyı daha sonra kolayca belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cdc99-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="cdc99-175">Uygunsa, ayrıca Merhaba, kullanıcı adı için tam etki alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Mantıksal uygulama ve veri ağ geçidi arasında bağlantı oluşturma](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="cdc99-177">Tebrikler, ağ geçidi bağlantınızı, logic app toouse için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="cdc99-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="cdc99-178">Ağ geçidi bağlantı ayarlarını Düzenle</span><span class="sxs-lookup"><span data-stu-id="cdc99-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="cdc99-179">Mantıksal uygulamanız için bir ağ geçidi bağlantısı oluşturduktan sonra özel bağlantı toolater güncelleştirme hello ayarlarını isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc99-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="cdc99-180">toofind hello ağ geçidi bağlantısı:</span><span class="sxs-lookup"><span data-stu-id="cdc99-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="cdc99-181">Merhaba mantığını uygulaması dikey penceresinde, altında **geliştirme araçları**seçin **API bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="cdc99-182">Merhaba **API bağlantıları** bölmesinde Ağ Geçidi bağlantıları dahil olmak üzere mantıksal uygulamanızı ile ilişkili tüm API bağlantıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="cdc99-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Tooyour mantıksal uygulama gidin, ""API bağlantıları seçin](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="cdc99-184">Veya hello ana Azure sol menüden, çok gidin **daha Hizmetleri** > **Web ve mobil Hizmetler** > **API bağlantıları** tüm API bağlantılarında Ağ Geçidi bağlantıları dahil olmak üzere, Azure aboneliğinizle ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="cdc99-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="cdc99-185">Veya hello ana Azure sol menüde, çok gidin**tüm kaynakları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="cdc99-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="cdc99-186">Tooview veya düzenlemek istediğiniz ve seçin hello ağ geçidi bağlantısı seçin **Düzenle API bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="cdc99-187">Yaptığınız güncelleştirmeler etkili değil olarak işaretlerse, [hello ağ geçidi Windows hizmetini durdurup yeniden başlatarak](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="cdc99-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="cdc99-188">Geçiş veya şirket içi veri ağ geçidi kaynağı silme</span><span class="sxs-lookup"><span data-stu-id="cdc99-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="cdc99-189">toocreate farklı ağ geçidi kaynak ağ geçidiniz farklı bir kaynakla ilişkilendirme veya hello ağ geçidi kaynağı kaldırmak, hello ağ geçidi yükleme etkilemeden hello ağ geçidi kaynağı silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdc99-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="cdc99-190">Merhaba ana Azure sol menüden, çok Git**tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="cdc99-191">Bul ve veri ağ geçidi kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="cdc99-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="cdc99-192">Seçin **şirket içi veri ağ geçidi**ve hello kaynak araç çubuğunda seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="cdc99-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="cdc99-193">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="cdc99-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="cdc99-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cdc99-194">Next steps</span></span>

* [<span data-ttu-id="cdc99-195">Mantıksal uygulamanızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="cdc99-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="cdc99-196">Yayın örnekleri ve senaryoları için logic apps</span><span class="sxs-lookup"><span data-stu-id="cdc99-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
