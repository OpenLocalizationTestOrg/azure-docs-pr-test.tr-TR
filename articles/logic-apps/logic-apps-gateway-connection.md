---
title: "Azure mantıksal uygulamaları için şirket içi veri kaynaklarına erişim | Microsoft Docs"
description: "Mantığı uygulamalardan şirket içi veri kaynaklarına erişebilmesi için şirket içi veri ağ geçidi kurun ayarlayın"
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="937c5-104">Şirket içi şirket içi veri ağ geçidi ile mantığı uygulamalardan veri kaynaklarına erişim</span><span class="sxs-lookup"><span data-stu-id="937c5-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="937c5-105">Mantıksal uygulamalarınızı şirket içi veri kaynaklarına erişmek için ile desteklenen bağlayıcılar mantıksal uygulamaları kullanan şirket içi veri ağ geçidi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="937c5-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="937c5-106">Ağ geçidi hızlı veri aktarımı ve logic apps ile şirket içi veri kaynakları arasındaki şifreleme sağlayan köprü gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="937c5-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="937c5-107">Ağ geçidi şifrelenmiş kanalda Azure Service Bus aracılığıyla şirket içi kaynaklardan veri aktarır.</span><span class="sxs-lookup"><span data-stu-id="937c5-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="937c5-108">Ağ geçidi aracısından güvenli giden trafik olarak tüm trafiğin kaynaklandığı.</span><span class="sxs-lookup"><span data-stu-id="937c5-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="937c5-109">Daha fazla bilgi edinmek [veri ağ geçidinin nasıl çalıştığını](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="937c5-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="937c5-110">Ağ geçidi, şirket içinde bu veri kaynaklarının bağlantılarını destekler:</span><span class="sxs-lookup"><span data-stu-id="937c5-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="937c5-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="937c5-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="937c5-112">DB2</span><span class="sxs-lookup"><span data-stu-id="937c5-112">DB2</span></span>  
*   <span data-ttu-id="937c5-113">Dosya Sistemi</span><span class="sxs-lookup"><span data-stu-id="937c5-113">File System</span></span>
*   <span data-ttu-id="937c5-114">Informix</span><span class="sxs-lookup"><span data-stu-id="937c5-114">Informix</span></span>
*   <span data-ttu-id="937c5-115">MQ</span><span class="sxs-lookup"><span data-stu-id="937c5-115">MQ</span></span>
*   <span data-ttu-id="937c5-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="937c5-116">MySQL</span></span>
*   <span data-ttu-id="937c5-117">Oracle Veritabanı</span><span class="sxs-lookup"><span data-stu-id="937c5-117">Oracle Database</span></span>
*   <span data-ttu-id="937c5-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="937c5-118">PostgreSQL</span></span>
*   <span data-ttu-id="937c5-119">SAP uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="937c5-119">SAP Application Server</span></span> 
*   <span data-ttu-id="937c5-120">SAP ileti sunucusu</span><span class="sxs-lookup"><span data-stu-id="937c5-120">SAP Message Server</span></span>
*   <span data-ttu-id="937c5-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="937c5-121">SharePoint</span></span>
*   <span data-ttu-id="937c5-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="937c5-122">SQL Server</span></span>
*   <span data-ttu-id="937c5-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="937c5-123">Teradata</span></span>

<span data-ttu-id="937c5-124">Bu adımları, şirket içi veri ağ geçidi kurun logic apps ile çalışacak biçimde ayarlamak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="937c5-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="937c5-125">Desteklenen bağlayıcılar hakkında daha fazla bilgi için bkz: [Azure Logic Apps bağlayıcılarının](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="937c5-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="937c5-126">Ağ geçidi diğer hizmetlerle birlikte kullanma hakkında daha fazla bilgi için bu makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="937c5-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="937c5-127">Microsoft Power BI şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="937c5-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="937c5-128">Azure Analysis Services veri ağ geçidi şirket içi</span><span class="sxs-lookup"><span data-stu-id="937c5-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="937c5-129">Microsoft Flow şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="937c5-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="937c5-130">Microsoft PowerApps şirket içi veri ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="937c5-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="937c5-131">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="937c5-131">Requirements</span></span>

* <span data-ttu-id="937c5-132">Önceden olmalıdır [veri ağ geçidi yerel bir bilgisayarda yüklü](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="937c5-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="937c5-133">Azure portalında oturum açtığınızda, aynı iş veya Okul hesabı için kullanılan kullanmak zorunda [şirket içi veri ağ geçidi yükleme](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="937c5-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="937c5-134">Oturum açma hesabınızın Ayrıca ağ geçidi yükleme için Azure portalında bir ağ geçidi kaynak oluştururken kullanmak için bir Azure aboneliğine sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="937c5-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="937c5-135">Ağ geçidi yüklemenizi zaten bir Azure ağ geçidi kaynağı tarafından istenemiyor.</span><span class="sxs-lookup"><span data-stu-id="937c5-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="937c5-136">Ağ geçidi yüklemenizi yalnızca bir Azure ağ geçidi kaynağına ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937c5-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="937c5-137">Yükleme için diğer kaynaklar kullanılamıyor, ağ geçidi kaynağı oluşturun, böylece talep olur.</span><span class="sxs-lookup"><span data-stu-id="937c5-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="937c5-138">Veri ağ geçidi bağlantısı kurma</span><span class="sxs-lookup"><span data-stu-id="937c5-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="937c5-139">1. Şirket içi veri ağ geçidi yükleme</span><span class="sxs-lookup"><span data-stu-id="937c5-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="937c5-140">Henüz yapmadıysanız, izleyin [şirket içi veri ağ geçidi yüklemek için adımları](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="937c5-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="937c5-141">Diğer adımlarla devam etmeden önce veri ağ geçidi yerel bir bilgisayarda yüklü emin olun.</span><span class="sxs-lookup"><span data-stu-id="937c5-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="937c5-142">2. Şirket içi veri ağ geçidi için bir Azure kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="937c5-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="937c5-143">Yerel bir bilgisayarda ağ geçidi'ni yükledikten sonra bir kaynak olarak Azure data gateway oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="937c5-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="937c5-144">Bu adım, ağ geçidi kaynağı ayrıca Azure aboneliğiniz ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="937c5-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="937c5-145">[Azure portalı](https://portal.azure.com "Azure portalı") oturumunu açın.</span><span class="sxs-lookup"><span data-stu-id="937c5-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="937c5-146">Ağ geçidi yüklemek için kullanılan e-posta adresi okul veya aynı Azure iş emin olun.</span><span class="sxs-lookup"><span data-stu-id="937c5-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="937c5-147">Azure sol menüsünde, **yeni** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi** aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="937c5-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !["Şirket içi veri ağ geçidi" Bul](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="937c5-149">Üzerinde **oluşturma bağlantı ağ geçidi** dikey penceresinde, veri ağ geçidi kaynağı oluşturmak için bu ayrıntıları sağlayın:</span><span class="sxs-lookup"><span data-stu-id="937c5-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="937c5-150">**Ad**: ağ geçidi kaynağı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="937c5-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="937c5-151">**Abonelik**: ağ geçidi kaynağınız ile ilişkilendirmek için Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="937c5-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="937c5-152">Bu abonelik mantıksal uygulamanızı aynı abonelik olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="937c5-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="937c5-153">Varsayılan abonelik oturum açmak için kullandığınız Azure hesabı temel alır.</span><span class="sxs-lookup"><span data-stu-id="937c5-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="937c5-154">**Kaynak grubu**: bir kaynak grubu oluşturun veya varolan bir kaynak grubu, ağ geçidi kaynağı dağıtmak için seçin.</span><span class="sxs-lookup"><span data-stu-id="937c5-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="937c5-155">Kaynak grupları ilgili Azure varlıklar koleksiyonu olarak yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="937c5-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="937c5-156">**Konum**: Azure kısıtlayan sırasında ağ geçidi bulut hizmeti için seçtiğiniz aynı bölgede bu konuma [ağ geçidi yükleme](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="937c5-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="937c5-157">Ağ geçidi kaynak konumu ağ geçidi bulut hizmeti konumu eşleştiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="937c5-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="937c5-158">Aksi halde, sonraki adımda seçebilmeniz için yüklü ağ geçitleri listesinde ağ geçidi yüklemenizi görünmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="937c5-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="937c5-159">Farklı bölgelerde mantıksal uygulamanızı ve ağ geçidi kaynağı için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937c5-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="937c5-160">**Yükleme adı**: ağ geçidi yüklemenizi seçili değilse, daha önce yüklediğiniz ağ geçidi seçin.</span><span class="sxs-lookup"><span data-stu-id="937c5-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="937c5-161">Ağ geçidi kaynağı Azure panonuza eklemek için **panoya Sabitle**.</span><span class="sxs-lookup"><span data-stu-id="937c5-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="937c5-162">İşiniz bittiğinde seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="937c5-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="937c5-163">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="937c5-163">For example:</span></span>

    ![Şirket içi veri ağ geçidi oluşturmak için ayrıntıları belirtin](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="937c5-165">Bulma veya ana menüden Azure sol, herhangi bir zamanda data gateway görüntülemek için Git **daha Hizmetleri** > **Kurumsal tümleştirme** > **şirket içi veri ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="937c5-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    !["Daha fazla Hizmetleri", "Kurumsal tümleştirme", "şirket içi veri ağ geçidi" sayfasına gidin](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="937c5-167">3. Şirket içi veri ağ geçidi mantıksal uygulamanızı Bağlan</span><span class="sxs-lookup"><span data-stu-id="937c5-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="937c5-168">Veri ağ geçidi kaynağı oluşturulur ve Azure aboneliğiniz bu kaynakla ilişkili olduğundan, mantıksal uygulamanızı ve veri ağ geçidi arasında bir bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="937c5-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="937c5-169">Ağ geçidi bağlantı konumunuz mantıksal uygulamanızı ile aynı bölgede olması gerekir, ancak farklı bir bölgede bulunan bir veri ağ geçidi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937c5-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="937c5-170">Azure portalında oluşturun veya mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.</span><span class="sxs-lookup"><span data-stu-id="937c5-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="937c5-171">SQL Server gibi şirket içi bağlantıları destekleyen bir bağlayıcı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="937c5-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="937c5-172">Gösterilen sırada aşağıdaki seçin **Connect şirket içi veri ağ geçidi üzerinden**benzersiz bağlantı adı ve gerekli bilgileri sağlayın ve kullanmak istediğiniz veri ağ geçidi kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="937c5-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="937c5-173">İşiniz bittiğinde seçin **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="937c5-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="937c5-174">Benzersiz bağlantı adı özellikle birden çok bağlantı oluşturduğunuzda bu bağlantıyı daha sonra kolayca belirlemenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="937c5-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="937c5-175">Uygunsa, ayrıca, kullanıcı adı için tam etki alanı içerir.</span><span class="sxs-lookup"><span data-stu-id="937c5-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![Mantıksal uygulama ve veri ağ geçidi arasında bağlantı oluşturma](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="937c5-177">Tebrikler, ağ geçidi bağlantınızı kullanmak mantığı uygulamanız için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="937c5-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="937c5-178">Ağ geçidi bağlantı ayarlarını Düzenle</span><span class="sxs-lookup"><span data-stu-id="937c5-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="937c5-179">Mantıksal uygulamanız için bir ağ geçidi bağlantısı oluşturduktan sonra daha sonra özel bağlantı ayarlarını güncelleştirmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937c5-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="937c5-180">Ağ geçidi bağlantısı bulmak için:</span><span class="sxs-lookup"><span data-stu-id="937c5-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="937c5-181">Mantıksal uygulama dikey altında **geliştirme araçları**seçin **API bağlantıları**.</span><span class="sxs-lookup"><span data-stu-id="937c5-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="937c5-182">**API bağlantıları** bölmesinde Ağ Geçidi bağlantıları dahil olmak üzere mantıksal uygulamanızı ile ilişkili tüm API bağlantıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="937c5-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Mantıksal uygulamanızı gidin, ""API bağlantıları seçin](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="937c5-184">Veya, ana Azure sol menüden, Git **daha Hizmetleri** > **Web ve mobil Hizmetler** > **API bağlantıları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="937c5-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="937c5-185">Veya, ana Azure sol menüde, Git **tüm kaynakları** tüm API bağlantıları için Azure aboneliğinizle ilişkili ağ geçidi bağlantıları dahil olmak üzere.</span><span class="sxs-lookup"><span data-stu-id="937c5-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="937c5-186">Görüntüleyin veya düzenleyin ve seçmek istediğiniz ağ geçidi bağlantısı seçin **Düzenle API bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="937c5-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="937c5-187">Yaptığınız güncelleştirmeler etkili değil olarak işaretlerse, [ağ geçidi Windows hizmeti durdurup](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="937c5-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="937c5-188">Geçiş veya şirket içi veri ağ geçidi kaynağı silme</span><span class="sxs-lookup"><span data-stu-id="937c5-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="937c5-189">Farklı ağ geçidi kaynağı oluşturmak, ağ geçidiniz farklı bir kaynakla ilişkilendirme veya ağ geçidi kaynağı kaldırmak için ağ geçidi kaynağına ağ geçidi yükleme etkilemeden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937c5-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="937c5-190">Ana Azure sol menüden, Git **tüm kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="937c5-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="937c5-191">Bul ve veri ağ geçidi kaynağı seçin.</span><span class="sxs-lookup"><span data-stu-id="937c5-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="937c5-192">Seçin **şirket içi veri ağ geçidi**ve kaynak araç çubuğunda seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="937c5-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="937c5-193">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="937c5-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="937c5-194">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="937c5-194">Next steps</span></span>

* [<span data-ttu-id="937c5-195">Mantıksal uygulamanızı güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="937c5-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="937c5-196">Yayın örnekleri ve senaryoları için logic apps</span><span class="sxs-lookup"><span data-stu-id="937c5-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
