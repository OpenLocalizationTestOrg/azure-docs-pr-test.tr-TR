---
title: "OMS BT Hizmet Yönetimi Bağlayıcısı ITSM bağlantıları | Microsoft Docs"
description: "BT hizmet yönetimi merkezi olarak izlemek ve ITSM iş öğelerini yönetmek için OMS Connector'daki ITSM ürünler/hizmetler bağlanın."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: e4f2e0a23aa52a0e02e7047916b77fb15107defa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a><span data-ttu-id="e03fb-103">ITSM ürünler/hizmetler ile BT Hizmet Yönetimi Bağlayıcısı (Önizleme) bağlanma</span><span class="sxs-lookup"><span data-stu-id="e03fb-103">Connect ITSM products/services with IT Service Management Connector (Preview)</span></span>
<span data-ttu-id="e03fb-104">Bu makalede, BT Hizmet Yönetimi OMS Connector'daki ITSM Ürün/hizmet bağlanmak ve merkezi olarak, iş öğelerini yönetmek hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e03fb-104">This article provides information about how to connect your ITSM product/service to IT Service Management Connector in OMS and centrally manage your work items.</span></span> <span data-ttu-id="e03fb-105">BT Hizmet Yönetimi Bağlayıcısı hakkında daha fazla bilgi [genel bakış](log-analytics-itsmc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e03fb-105">More information about IT Service Management Connector, see [Overview](log-analytics-itsmc-overview.md).</span></span>

<span data-ttu-id="e03fb-106">Aşağıdaki ürünler/hizmetler desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e03fb-106">The following products/services are supported:</span></span>

- [<span data-ttu-id="e03fb-107">System Center Service Manager</span><span class="sxs-lookup"><span data-stu-id="e03fb-107">System Center Service Manager</span></span>](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="e03fb-108">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="e03fb-108">ServiceNow</span></span>](#connect-servicenow-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="e03fb-109">Provance</span><span class="sxs-lookup"><span data-stu-id="e03fb-109">Provance</span></span>](#connect-provance-to-it-service-management-connector-in-oms)
- [<span data-ttu-id="e03fb-110">Cherwell</span><span class="sxs-lookup"><span data-stu-id="e03fb-110">Cherwell</span></span>](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-to-it-service-management-connector-in-oms"></a><span data-ttu-id="e03fb-111">System Center Service Manager BT hizmetine bağlanmak OMS Yönetimi Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e03fb-111">Connect System Center Service Manager to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="e03fb-112">Aşağıdaki bölümlerde BT Hizmet Yönetimi Bağlayıcısı OMS, System Center Service Manager ürününüzü bağlanma hakkında ayrıntılar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-112">The following sections provide details about how to connect your System Center Service Manager product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e03fb-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e03fb-113">Prerequisites</span></span>

<span data-ttu-id="e03fb-114">Aşağıdaki önkoşulları yerine olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e03fb-114">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="e03fb-115">BT Hizmet Yönetimi Bağlayıcısı yüklü.</span><span class="sxs-lookup"><span data-stu-id="e03fb-115">IT Service Management Connector installed.</span></span>
<span data-ttu-id="e03fb-116">Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="e03fb-116">More information:  [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="e03fb-117">Service Manager Web uygulaması (Web uygulaması) dağıtılır ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-117">The Service Manager Web application (Web app) is deployed and configured.</span></span> <span data-ttu-id="e03fb-118">Web uygulaması hakkında bilgi [burada](#create-and-deploy-service-manager-web-app-service).</span><span class="sxs-lookup"><span data-stu-id="e03fb-118">Information on Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
- <span data-ttu-id="e03fb-119">Karma bağlantı oluşturulur ve yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-119">Hybrid connection created and configured.</span></span> <span data-ttu-id="e03fb-120">Daha fazla bilgi: [karma bağlantı yapılandırma](#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="e03fb-120">More information: [Configure the hybrid Connection](#configure-the-hybrid-connection).</span></span>
- <span data-ttu-id="e03fb-121">Service Manager sürümleri desteklenir: 2012 R2 veya 2016.</span><span class="sxs-lookup"><span data-stu-id="e03fb-121">Supported versions of Service Manager:  2012 R2 or 2016.</span></span>
- <span data-ttu-id="e03fb-122">Kullanıcı rolü: [gelişmiş işleç](https://technet.microsoft.com/library/ff461054.aspx).</span><span class="sxs-lookup"><span data-stu-id="e03fb-122">User role:  [Advanced operator](https://technet.microsoft.com/library/ff461054.aspx).</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="e03fb-123">Bağlantı yordamı</span><span class="sxs-lookup"><span data-stu-id="e03fb-123">Connection procedure</span></span>

<span data-ttu-id="e03fb-124">System Center Service Manager Örneğiniz için BT Hizmet Yönetimi Bağlayıcısı bağlanmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-124">Use the following procedure to connect your System Center Service Manager instance to the IT Service Management Connector:</span></span>

1. <span data-ttu-id="e03fb-125">Git **OMS** >**ayarları** > **bağlı kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-125">Go to **OMS** >**Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="e03fb-126">Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-126">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![<span data-ttu-id="e03fb-127">Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="e03fb-127">Service manager</span></span> ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. <span data-ttu-id="e03fb-128">Aşağıdaki tabloda açıklandığı gibi bilgileri sağlayın ve tıklayın **kaydetmek** bağlantı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="e03fb-128">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="e03fb-129">Bu parametre zorunludur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-129">All these parameters are mandatory.</span></span>

| <span data-ttu-id="e03fb-130">**Alan**</span><span class="sxs-lookup"><span data-stu-id="e03fb-130">**Field**</span></span> | <span data-ttu-id="e03fb-131">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e03fb-131">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e03fb-132">**Ad**</span><span class="sxs-lookup"><span data-stu-id="e03fb-132">**Name**</span></span>   | <span data-ttu-id="e03fb-133">BT Hizmet Yönetimi Bağlayıcısı ile bağlanmak istediğiniz System Center Service Manager örneği için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-133">Type a name for the System Center Service Manager instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-134">Bu örnekte iş öğelerini yapılandırma / ayrıntılı günlük analizi görünümü olduğunda, bu adı daha sonra kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="e03fb-134">You use this name later when you configure work items in this instance/ view detailed log analytics.</span></span> |
| <span data-ttu-id="e03fb-135">**Bağlantı türü seçin**</span><span class="sxs-lookup"><span data-stu-id="e03fb-135">**Select Connection type**</span></span>   | <span data-ttu-id="e03fb-136">Seçin **System Center Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-136">Select **System Center Service Manager**.</span></span> |
| <span data-ttu-id="e03fb-137">**Sunucu URL'si**</span><span class="sxs-lookup"><span data-stu-id="e03fb-137">**Server URL**</span></span>   | <span data-ttu-id="e03fb-138">Service Manager Web uygulamasının URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-138">Type the URL of the Service Manager Web app.</span></span> <span data-ttu-id="e03fb-139">Service Manager Web uygulaması hakkında daha fazla bilgiyi [burada](#create-and-deploy-service-manager-web-app-service).</span><span class="sxs-lookup"><span data-stu-id="e03fb-139">More information about Service Manager Web app is [here](#create-and-deploy-service-manager-web-app-service).</span></span>
| <span data-ttu-id="e03fb-140">**İstemci kimliği**</span><span class="sxs-lookup"><span data-stu-id="e03fb-140">**Client ID**</span></span>   | <span data-ttu-id="e03fb-141">Web uygulaması kimlik doğrulamasını (otomatik komut dosyası kullanarak) oluşturulan istemci kimliği yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-141">Type the client ID that you generated (using the automatic script) for authenticating the Web app.</span></span> <span data-ttu-id="e03fb-142">Otomatik komut dosyası hakkında daha fazla bilgiyi [burada.](log-analytics-itsmc-service-manager-script.md)</span><span class="sxs-lookup"><span data-stu-id="e03fb-142">More information about the automated script is [here.](log-analytics-itsmc-service-manager-script.md)</span></span>|
| <span data-ttu-id="e03fb-143">**İstemci parolası**</span><span class="sxs-lookup"><span data-stu-id="e03fb-143">**Client Secret**</span></span>   | <span data-ttu-id="e03fb-144">İstemci parolası yazın bu kimliği için oluşturulan</span><span class="sxs-lookup"><span data-stu-id="e03fb-144">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="e03fb-145">**Veri Eşitleme kapsamı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-145">**Data Sync Scope**</span></span>   | <span data-ttu-id="e03fb-146">BT Hizmet Yönetimi Bağlayıcısı üzerinden eşitlemek istediğiniz Service Manager iş öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-146">Select the Service Manager work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-147">Bu iş öğeleri günlük analizi aktarılır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-147">These work items are imported into Log Analytics.</span></span> <span data-ttu-id="e03fb-148">**Seçenekler:** olaylar, değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-148">**Options:**  Incidents, Change Requests.</span></span>|
| <span data-ttu-id="e03fb-149">**Eşitleme veri**</span><span class="sxs-lookup"><span data-stu-id="e03fb-149">**Sync Data**</span></span> | <span data-ttu-id="e03fb-150">Verileri istediğiniz beri geçen gün sayısını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-150">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="e03fb-151">**Üst sınır**: 120 gün.</span><span class="sxs-lookup"><span data-stu-id="e03fb-151">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="e03fb-152">**ITSM çözümde yeni yapılandırma öğesi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="e03fb-152">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="e03fb-153">Yapılandırma öğeleri ITSM ürün oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-153">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="e03fb-154">Seçili olduğunda, OMS etkilenen CI desteklenen ITSM sistem içinde yapılandırma öğeleri (Cı'ler var olmayan) durumunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-154">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="e03fb-155">**Varsayılan**: devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e03fb-155">**Default**: disabled.</span></span> |

<span data-ttu-id="e03fb-156">Başarıyla bağlanıldı ve eşitlenen kullanıldığında:</span><span class="sxs-lookup"><span data-stu-id="e03fb-156">When successfully connected, and synced:</span></span>

- <span data-ttu-id="e03fb-157">Seçili iş öğelerini Hizmet Yöneticisi'nden OMS aktarılır **günlük analizi.**</span><span class="sxs-lookup"><span data-stu-id="e03fb-157">Selected work items from Service Manager are imported into OMS **Log Analytics.**</span></span> <span data-ttu-id="e03fb-158">Bu bir özetini görüntüleyebilirsiniz BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-158">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>

- <span data-ttu-id="e03fb-159">OMS olaylar OMS uyarıları veya günlük arama, bu Service Manager örneğini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-159">From OMS, you can create incidents from OMS alerts or from log search, in this Service Manager instance.</span></span>

<span data-ttu-id="e03fb-160">Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span><span class="sxs-lookup"><span data-stu-id="e03fb-160">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-and-deploy-service-manager-web-app-service"></a><span data-ttu-id="e03fb-161">Oluşturma ve Service Manager web uygulama hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="e03fb-161">Create and deploy Service Manager web app service</span></span>

<span data-ttu-id="e03fb-162">OMS BT Hizmet Yönetimi bağlayıcı ile şirket içi Hizmet Yöneticisi'ni bağlanmak için Microsoft Github'da Service Manager Web uygulaması oluşturmuştur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-162">To connect the on-premises Service Manager with the IT Service Management Connector on OMS, Microsoft has created a Service Manager Web app on the GitHub.</span></span>

<span data-ttu-id="e03fb-163">Service Manager için ITSM Web uygulamasını kurup ayarlamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-163">To set up the ITSM Web app for your Service Manager, do the following:</span></span>

- <span data-ttu-id="e03fb-164">**Web uygulaması dağıtma** – Web uygulaması dağıtma, özelliklerini ayarlamak ve Azure AD ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="e03fb-164">**Deploy the Web app** – Deploy the Web app, set the properties, and authenticate with Azure AD.</span></span> <span data-ttu-id="e03fb-165">Web uygulaması kullanarak dağıtabilirsiniz [betik otomatik](log-analytics-itsmc-service-manager-script.md) Microsoft, sağlamıştır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-165">You can deploy the web app by using the [automated script](log-analytics-itsmc-service-manager-script.md) that Microsoft has provided you.</span></span>
- <span data-ttu-id="e03fb-166">**Karma bağlantı yapılandırma** - [bu bağlantıyı yapılandırmak](#configure-the-hybrid-connection), el ile.</span><span class="sxs-lookup"><span data-stu-id="e03fb-166">**Configure the hybrid connection** - [Configure this connection](#configure-the-hybrid-connection), manually.</span></span>

#### <a name="deploy-the-web-app"></a><span data-ttu-id="e03fb-167">Web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="e03fb-167">Deploy the web app</span></span>
<span data-ttu-id="e03fb-168">Otomatik kullanmak [betik](log-analytics-itsmc-service-manager-script.md) Web uygulamasını dağıtmak için özelliklerini ayarlamak ve Azure AD ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="e03fb-168">Use the automated [script](log-analytics-itsmc-service-manager-script.md) to deploy the Web app, set the properties, and authenticate with Azure AD.</span></span>

<span data-ttu-id="e03fb-169">Aşağıdaki gerekli ayrıntıları sağlayarak komut dosyasını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-169">Run the script by providing the following required details:</span></span>

- <span data-ttu-id="e03fb-170">Azure Abonelik Ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="e03fb-170">Azure subscription details</span></span>
- <span data-ttu-id="e03fb-171">Kaynak grubu adı</span><span class="sxs-lookup"><span data-stu-id="e03fb-171">Resource group name</span></span>
- <span data-ttu-id="e03fb-172">Konum</span><span class="sxs-lookup"><span data-stu-id="e03fb-172">Location</span></span>
- <span data-ttu-id="e03fb-173">Service Manager sunucu ayrıntıları (sunucu adı, etki alanı, kullanıcı adı ve parola)</span><span class="sxs-lookup"><span data-stu-id="e03fb-173">Service Manager server details (server name, domain, user name, and password)</span></span>
- <span data-ttu-id="e03fb-174">Web uygulamanız için site adı öneki</span><span class="sxs-lookup"><span data-stu-id="e03fb-174">Site name prefix for your Web app</span></span>
- <span data-ttu-id="e03fb-175">ServiceBus Namespace.</span><span class="sxs-lookup"><span data-stu-id="e03fb-175">ServiceBus Namespace.</span></span>

<span data-ttu-id="e03fb-176">Komut dosyası (benzersiz hale getirmek amacıyla birkaç ek dizeleri birlikte) belirtilen adı kullanarak Web uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-176">The script creates the Web app using the name that you specified (along with few additional strings to make it unique).</span></span> <span data-ttu-id="e03fb-177">Bunu oluşturan **Web uygulaması URL'si**, **istemci kimliği** ve **gizli**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-177">It generates the **Web app URL**, **client ID** and **client secret**.</span></span>

<span data-ttu-id="e03fb-178">Bir bağlantı ile BT Hizmet Yönetimi Bağlayıcısı oluşturduğunuzda değerleri kaydetmek, bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-178">Save the values, you use them when you create a connection with IT Service Management Connector.</span></span>

<span data-ttu-id="e03fb-179">**Web uygulaması yükleme denetimi**</span><span class="sxs-lookup"><span data-stu-id="e03fb-179">**Check the Web app installation**</span></span>

1. <span data-ttu-id="e03fb-180">Git **Azure portal** > **kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-180">Go to **Azure portal** > **Resources**.</span></span>
2. <span data-ttu-id="e03fb-181">Web uygulaması seçin, **ayarları** > **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-181">Select the Web app, click **Settings** > **Application Settings**.</span></span>
3. <span data-ttu-id="e03fb-182">Komut dosyası aracılığıyla uygulama dağıtımı sırasındaki sağlanan Service Manager örneğiyle ilgili bilgiler onaylayın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-182">Confirm the information about the Service Manager instance that you provided at the time of deploying the app through the script.</span></span>

### <a name="configure-the-hybrid-connection"></a><span data-ttu-id="e03fb-183">Karma bağlantıyı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e03fb-183">Configure the hybrid connection</span></span>

<span data-ttu-id="e03fb-184">OMS BT Hizmet Yönetimi bağlayıcısıyla Service Manager örneğine bağlar karma bağlantıyı yapılandırmak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-184">Use the following procedure to configure the hybrid connection that connects the Service Manager instance with the IT Service Management Connector in OMS.</span></span>

1. <span data-ttu-id="e03fb-185">Service Manager Web uygulamasının altında Bul **Azure kaynaklarını**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-185">Find the Service Manager Web app, under **Azure Resources**.</span></span>
2. <span data-ttu-id="e03fb-186">Tıklatın **ayarları** > **ağ**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-186">Click **Settings** > **Networking**.</span></span>
3. <span data-ttu-id="e03fb-187">Altında **karma bağlantılar**, tıklatın **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-187">Under **Hybrid Connections**, click **Configure your hybrid connection endpoints**.</span></span>

    ![Karma bağlantının ağ](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. <span data-ttu-id="e03fb-189">İçinde **karma bağlantılar** dikey penceresinde tıklatın **karma Bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-189">In the **Hybrid Connections** blade, click **Add hybrid connection**.</span></span>

    ![Karma Bağlantısı Ekle](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. <span data-ttu-id="e03fb-191">İçinde **eklemek karma bağlantılar** dikey penceresinde tıklatın **oluştur yeni karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-191">In the **Add Hybrid Connections** blade, click **Create new hybrid Connection**.</span></span>

    ![Yeni Karma bağlantı](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. <span data-ttu-id="e03fb-193">Aşağıdaki değerleri yazın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-193">Type the following values:</span></span>

    - <span data-ttu-id="e03fb-194">**Uç nokta adı**: yeni bir karma bağlantı için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-194">**EndPoint Name**: Specify a name for the new Hybrid connection.</span></span>
    -  <span data-ttu-id="e03fb-195">**Uç noktası ana bilgisayar**: Service Manager yönetim sunucusunun FQDN'si.</span><span class="sxs-lookup"><span data-stu-id="e03fb-195">**EndPoint Host**: FQDN of the Service Manager management server.</span></span>
    - <span data-ttu-id="e03fb-196">**Uç nokta bağlantı noktası**: 5724 yazın</span><span class="sxs-lookup"><span data-stu-id="e03fb-196">**EndPoint Port**: Type 5724</span></span>
    - <span data-ttu-id="e03fb-197">**Servicebus ad alanı**: varolan bir servicebus ad kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e03fb-197">**Servicebus namespace**: Use an existing servicebus namespace or create a new one.</span></span>
    - <span data-ttu-id="e03fb-198">**Konum**: konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-198">**Location**: select the location.</span></span>
    -  <span data-ttu-id="e03fb-199">**Ad**:, oluşturuyorsanız servicebus için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-199">**Name**: Specify a name to the servicebus if you are creating it.</span></span>

    ![Karma bağlantı değerleri](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. <span data-ttu-id="e03fb-201">Tıklatın **Tamam** kapatmak için **karma bağlantı oluşturmak** dikey penceresinde ve karma bağlantı oluşturma Başlat.</span><span class="sxs-lookup"><span data-stu-id="e03fb-201">Click **OK** to close the **Create hybrid connection** blade and start creating the hybrid connection.</span></span>

    <span data-ttu-id="e03fb-202">Karma bağlantısı oluşturulduktan sonra dikey altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e03fb-202">Once the Hybrid connection is created, it is displayed under the blade.</span></span>

7. <span data-ttu-id="e03fb-203">Karma bağlantısı oluşturulduktan sonra bağlantıyı seçin ve'ı tıklatın **Ekle seçili karma bağlantı**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-203">After the hybrid connection is created, select the connection and click **Add selected hybrid connection**.</span></span>

    ![Yeni Karma bağlantı](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-the-listener-setup"></a><span data-ttu-id="e03fb-205">Dinleyici Kurulumu Yapılandır</span><span class="sxs-lookup"><span data-stu-id="e03fb-205">Configure the listener setup</span></span>

<span data-ttu-id="e03fb-206">Karma bağlantının dinleyicisi Kur yapılandırmak için aşağıdaki yordamı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-206">Use the following procedure to configure the listener setup for the hybrid connection.</span></span>

1. <span data-ttu-id="e03fb-207">İçinde **karma bağlantılar** dikey penceresinde tıklatın **Bağlantı Yöneticisi'ni indirin** ve System Center Service Manager örneğinin çalıştığı makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-207">In the **Hybrid Connections** blade, click **Download the Connection Manager** and install it on the machine where System Center Service Manager instance is running.</span></span>

    <span data-ttu-id="e03fb-208">Yükleme tamamlandıktan sonra **karma Bağlantı Yöneticisi kullanıcı Arabirimi** seçeneği altında kullanılabilir **Başlat** menüsü.</span><span class="sxs-lookup"><span data-stu-id="e03fb-208">Once the installation is complete, **Hybrid Connection Manager UI** option is available under **Start** menu.</span></span>

2. <span data-ttu-id="e03fb-209">Tıklatın **karma Bağlantı Yöneticisi kullanıcı Arabirimi** , Azure kimlik bilgileriniz istenir.</span><span class="sxs-lookup"><span data-stu-id="e03fb-209">Click **Hybrid Connection Manager UI** , you will be prompted for your Azure credentials.</span></span>

3. <span data-ttu-id="e03fb-210">Azure kimlik bilgilerinizle oturum açma ve karma bağlantı oluşturulduğu aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-210">Login with your Azure credentials and select your subscription where the Hybrid connection was created.</span></span>

4. <span data-ttu-id="e03fb-211">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-211">Click **Save**.</span></span>

<span data-ttu-id="e03fb-212">Karma bağlantı başarıyla bağlandı.</span><span class="sxs-lookup"><span data-stu-id="e03fb-212">Your hybrid connection is successfully connected.</span></span>

![başarılı karma bağlantı](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> <span data-ttu-id="e03fb-214">Sonra karma bağlantısı oluşturulduğunda, doğrulayın ve dağıtılan Service Manager Web uygulaması ziyaret ederek bağlantıyı sınayın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-214">After the hybrid connection is created, verify and test the connection by visiting the deployed Service Manager Web app.</span></span> <span data-ttu-id="e03fb-215">OMS BT Hizmet Yönetimi bağlayıcıda bağlanmaya çalışmadan önce bağlantı başarılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e03fb-215">Ensure the connection is successful before you try to connect to the IT Service Management Connector in OMS.</span></span>

<span data-ttu-id="e03fb-216">Aşağıdaki resimde, başarılı bir bağlantı ayrıntılarını gösterir:</span><span class="sxs-lookup"><span data-stu-id="e03fb-216">The following image shows the details of a successful connection:</span></span>

![Karma bağlantı testi](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-to-it-service-management-connector-in-oms"></a><span data-ttu-id="e03fb-218">ServiceNow BT hizmetine bağlanmak OMS Yönetimi Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e03fb-218">Connect ServiceNow to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="e03fb-219">Aşağıdaki bölümlerde OMS BT Hizmet Yönetimi Connector ServiceNow ürününüzü bağlanma hakkında ayrıntılar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-219">The following sections provide details about how to connect your ServiceNow product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e03fb-220">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e03fb-220">Prerequisites</span></span>

<span data-ttu-id="e03fb-221">Aşağıdaki önkoşulları yerine olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e03fb-221">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="e03fb-222">BT Hizmet Yönetimi Bağlayıcısı yüklü.</span><span class="sxs-lookup"><span data-stu-id="e03fb-222">IT Service Management Connector installed.</span></span> <span data-ttu-id="e03fb-223">Daha fazla bilgi: [yapılandırma.](log-analytics-itsmc-overview.md#configuration)</span><span class="sxs-lookup"><span data-stu-id="e03fb-223">More information: [Configuration.](log-analytics-itsmc-overview.md#configuration)</span></span>
- <span data-ttu-id="e03fb-224">ServiceNow sürümler – Fuji, Geneva, Helsinki desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e03fb-224">ServiceNow supported versions – Fuji, Geneva, Helsinki.</span></span>

<span data-ttu-id="e03fb-225">ServiceNow yöneticileri, kendi ServiceNow örneği aşağıdakileri yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e03fb-225">ServiceNow Admins must do the following in their ServiceNow instance:</span></span>
- <span data-ttu-id="e03fb-226">İstemci kimliği ve ServiceNow ürün için istemci parolası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-226">Generate client ID and client secret for the ServiceNow product.</span></span> <span data-ttu-id="e03fb-227">İstemci kimliği ve parolası oluşturma hakkında daha fazla bilgi için bkz: [OAuth Kurulumu](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span><span class="sxs-lookup"><span data-stu-id="e03fb-227">For information on how to generate client ID and secret, see [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span>
- <span data-ttu-id="e03fb-228">Microsoft OMS tümleştirme (ServiceNow uygulama) için kullanıcı uygulamasını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-228">Install the User App for Microsoft OMS integration (ServiceNow app).</span></span> <span data-ttu-id="e03fb-229">[Daha fazla bilgi edinin](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span><span class="sxs-lookup"><span data-stu-id="e03fb-229">[Learn more](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).</span></span>
- <span data-ttu-id="e03fb-230">Yüklenen kullanıcı uygulaması için tümleştirme kullanıcı rolü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e03fb-230">Create integration user role for the user app installed.</span></span> <span data-ttu-id="e03fb-231">Tümleştirme kullanıcı rolü oluşturma konusunda bilgiler [burada](#create-integration-user-role-in-servicenow-app).</span><span class="sxs-lookup"><span data-stu-id="e03fb-231">Information on how to create the integration user role is [here](#create-integration-user-role-in-servicenow-app).</span></span>


### <a name="connection-procedure"></a><span data-ttu-id="e03fb-232">**Bağlantı yordamı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-232">**Connection procedure**</span></span>

<span data-ttu-id="e03fb-233">ServiceNow bağlantı oluşturmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-233">Use the following procedure to create a ServiceNow connection:</span></span>

1. <span data-ttu-id="e03fb-234">Git **OMS** > **ayarları** > **bağlı kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-234">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="e03fb-235">Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-235">Select **ITSM Connector,** click **Add New Connection**.</span></span>

    ![ServiceNow bağlantı](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. <span data-ttu-id="e03fb-237">Aşağıdaki tabloda açıklandığı gibi bilgileri sağlayın ve tıklayın **kaydetmek** bağlantı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="e03fb-237">Provide the information as described in the following table, and click **Save** to create the connection:</span></span>

> [!NOTE]
> <span data-ttu-id="e03fb-238">Bu parametre zorunludur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-238">All these parameters are mandatory.</span></span>

| <span data-ttu-id="e03fb-239">**Alan**</span><span class="sxs-lookup"><span data-stu-id="e03fb-239">**Field**</span></span> | <span data-ttu-id="e03fb-240">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e03fb-240">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e03fb-241">**Ad**</span><span class="sxs-lookup"><span data-stu-id="e03fb-241">**Name**</span></span>   | <span data-ttu-id="e03fb-242">BT Hizmet Yönetimi Bağlayıcısı ile bağlanmak istediğiniz ServiceNow örneği için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-242">Type a name for the ServiceNow instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-243">İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-243">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="e03fb-244">**Bağlantı türü seçin**</span><span class="sxs-lookup"><span data-stu-id="e03fb-244">**Select Connection type**</span></span>   | <span data-ttu-id="e03fb-245">Seçin **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-245">Select **ServiceNow**.</span></span> |
| <span data-ttu-id="e03fb-246">**Kullanıcı Adı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-246">**Username**</span></span>   | <span data-ttu-id="e03fb-247">BT Hizmet Yönetimi Bağlayıcısı bağlantıyı desteklemek üzere ServiceNow uygulamasında oluşturulan tümleştirme kullanıcı adı yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-247">Type the integration user name that you created in the ServiceNow app to support the connection to the IT Service Management Connector.</span></span> <span data-ttu-id="e03fb-248">Daha fazla bilgi: [oluşturma ServiceNow uygulama kullanıcı rolü](#create-integration-user-role-in-servicenow-app).</span><span class="sxs-lookup"><span data-stu-id="e03fb-248">More information: [Create ServiceNow app user role](#create-integration-user-role-in-servicenow-app).</span></span>|
| <span data-ttu-id="e03fb-249">**Parola**</span><span class="sxs-lookup"><span data-stu-id="e03fb-249">**Password**</span></span>   | <span data-ttu-id="e03fb-250">Bu kullanıcı adıyla ilişkili parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-250">Type the password associated with this user name.</span></span> <span data-ttu-id="e03fb-251">**Not**: kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere OMS hizmet içinde depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-251">**Note**: User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>  |
| <span data-ttu-id="e03fb-252">**Sunucu URL'si**</span><span class="sxs-lookup"><span data-stu-id="e03fb-252">**Server URL**</span></span>   | <span data-ttu-id="e03fb-253">BT Hizmet Yönetimi Bağlayıcısı için bağlanmak istediğiniz ServiceNow örneğinin URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-253">Type the URL of the ServiceNow instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="e03fb-254">**İstemci kimliği**</span><span class="sxs-lookup"><span data-stu-id="e03fb-254">**Client ID**</span></span>   | <span data-ttu-id="e03fb-255">Daha önce oluşturulan OAuth2 kimlik doğrulamasında kullanmak istediğiniz istemci kimliği yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-255">Type the client ID that you want to use for OAuth2 Authentication, which you generated earlier.</span></span>  <span data-ttu-id="e03fb-256">İstemci kimliği ve parolası oluşturma hakkında daha fazla bilgi: [OAuth Kurulumu](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span><span class="sxs-lookup"><span data-stu-id="e03fb-256">More information on generating client ID and secret:   [OAuth Setup](http://wiki.servicenow.com/index.php?title=OAuth_Setup).</span></span> |
| <span data-ttu-id="e03fb-257">**İstemci parolası**</span><span class="sxs-lookup"><span data-stu-id="e03fb-257">**Client Secret**</span></span>   | <span data-ttu-id="e03fb-258">İstemci parolası yazın bu kimliği için oluşturulan</span><span class="sxs-lookup"><span data-stu-id="e03fb-258">Type the client secret, generated for this ID.</span></span>   |
| <span data-ttu-id="e03fb-259">**Veri Eşitleme kapsamı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-259">**Data Sync Scope**</span></span>   | <span data-ttu-id="e03fb-260">BT Hizmet Yönetimi bağlayıcısı aracılığıyla OMS eşitlemek istediğiniz ServiceNow iş öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-260">Select the ServiceNow work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-261">Seçilen değerleri günlük analizi alınır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-261">The selected values are imported into log analytics.</span></span>   <span data-ttu-id="e03fb-262">**Seçenekler:** olaylar ve değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-262">**Options:**  Incidents and Change Requests.</span></span>|
| <span data-ttu-id="e03fb-263">**Eşitleme veri**</span><span class="sxs-lookup"><span data-stu-id="e03fb-263">**Sync Data**</span></span> | <span data-ttu-id="e03fb-264">Verileri istediğiniz beri geçen gün sayısını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-264">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="e03fb-265">**Üst sınır**: 120 gün.</span><span class="sxs-lookup"><span data-stu-id="e03fb-265">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="e03fb-266">**ITSM çözümde yeni yapılandırma öğesi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="e03fb-266">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="e03fb-267">Yapılandırma öğeleri ITSM ürün oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-267">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="e03fb-268">Seçili olduğunda, OMS etkilenen CI desteklenen ITSM sistem içinde yapılandırma öğeleri (Cı'ler var olmayan) durumunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-268">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="e03fb-269">**Varsayılan**: devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e03fb-269">**Default**: disabled.</span></span> |


<span data-ttu-id="e03fb-270">Başarıyla bağlanıldı ve eşitlenen kullanıldığında:</span><span class="sxs-lookup"><span data-stu-id="e03fb-270">When successfully connected, and synced:</span></span>

- <span data-ttu-id="e03fb-271">Seçili iş öğelerini ServiceNow bağlantısından OMS günlük analizi alınır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-271">Selected work items from ServiceNow connection are imported into OMS Log Analytics.</span></span>  <span data-ttu-id="e03fb-272">Bu bir özetini görüntüleyebilirsiniz BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-272">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="e03fb-273">Bu ServiceNow örneğinin OMS uyarıları veya günlük aramadan olaylar, uyarılar ve olaylar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-273">You can create incidents, alerts, and events from OMS Alerts or log search in this ServiceNow instance.</span></span>  


<span data-ttu-id="e03fb-274">Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span><span class="sxs-lookup"><span data-stu-id="e03fb-274">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="create-integration-user-role-in-servicenow-app"></a><span data-ttu-id="e03fb-275">ServiceNow uygulamada tümleştirme kullanıcı rolü oluşturun</span><span class="sxs-lookup"><span data-stu-id="e03fb-275">Create integration user role in ServiceNow app</span></span>

<span data-ttu-id="e03fb-276">Aşağıdaki yordam kullanıcı:</span><span class="sxs-lookup"><span data-stu-id="e03fb-276">User the following procedure:</span></span>

1.  <span data-ttu-id="e03fb-277">Ziyaret [ServiceNow deposunu](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) yükleyip **ServiceNow ve Microsoft OMS tümleştirme için kullanıcı uygulaması** ServiceNow örneğinin içine.</span><span class="sxs-lookup"><span data-stu-id="e03fb-277">Visit the [ServiceNow store](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) and install the **User App for ServiceNow and Microsoft OMS Integration** into your ServiceNow Instance.</span></span>
2.  <span data-ttu-id="e03fb-278">Yükleme tamamlandıktan sonra sol gezinti çubuğunda ServiceNow örneğinin, arama ve select Microsoft OMS Tümleştirici ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-278">After installation, visit the left navigation bar of the ServiceNow instance, search, and select Microsoft OMS integrator.</span></span>  
3.  <span data-ttu-id="e03fb-279">Tıklatın **yükleme Yapılacaklar listesi**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-279">Click **Installation Checklist**.</span></span>

    <span data-ttu-id="e03fb-280">Durum görüntülenir **tamamlanmadı** oluşturulacak kullanıcı rolü henüz ise.</span><span class="sxs-lookup"><span data-stu-id="e03fb-280">The status is displayed as  **Not complete** if the user role is yet to be created.</span></span>

4.  <span data-ttu-id="e03fb-281">Metin kutularındaki yanına **tümleştirme kullanıcı oluşturma**, BT Hizmet Yönetimi Bağlayıcısı OMS içinde bağlanıp kullanıcının kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-281">In the text boxes, next to **Create integration user**, enter the user name for the user that can connect to the IT Service Management Connector in OMS.</span></span>
5.  <span data-ttu-id="e03fb-282">Bu kullanıcı için parola girin ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-282">Enter the password for this user, and click **OK**.</span></span>  

>[!NOTE]

> <span data-ttu-id="e03fb-283">OMS içinde ServiceNow bağlantı kurmak için bu kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-283">You use these credentials to make the ServiceNow connection in OMS.</span></span>

<span data-ttu-id="e03fb-284">Yeni oluşturulan kullanıcı atanmış varsayılan rolleriyle görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e03fb-284">The newly created user is displayed with the default roles assigned.</span></span>

<span data-ttu-id="e03fb-285">Varsayılan roller:</span><span class="sxs-lookup"><span data-stu-id="e03fb-285">Default roles:</span></span>
- <span data-ttu-id="e03fb-286">personalize_choices</span><span class="sxs-lookup"><span data-stu-id="e03fb-286">personalize_choices</span></span>
- <span data-ttu-id="e03fb-287">import_transformer</span><span class="sxs-lookup"><span data-stu-id="e03fb-287">import_transformer</span></span>
-   <span data-ttu-id="e03fb-288">x_mioms_microsoft.user</span><span class="sxs-lookup"><span data-stu-id="e03fb-288">x_mioms_microsoft.user</span></span>
-   <span data-ttu-id="e03fb-289">ITIL</span><span class="sxs-lookup"><span data-stu-id="e03fb-289">itil</span></span>
-   <span data-ttu-id="e03fb-290">template_editor</span><span class="sxs-lookup"><span data-stu-id="e03fb-290">template_editor</span></span>
-   <span data-ttu-id="e03fb-291">view_changer</span><span class="sxs-lookup"><span data-stu-id="e03fb-291">view_changer</span></span>

<span data-ttu-id="e03fb-292">Kullanıcı başarıyla oluşturduktan sonra durumu **denetleyin yükleme Yapılacaklar listesi** oluşturulan uygulama için kullanıcı rolü ayrıntılarını listeleme tamamlandı olarak taşır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-292">Once the user is successfully created, the status of **Check Installation Checklist** moves to Completed, listing the details of the user role created for the app.</span></span>

> [!NOTE]

> <span data-ttu-id="e03fb-293">Bir kullanıcı oluşturmak izin vermek için **uyarıları** ve **olayları** OMS ServiceNow içinde:</span><span class="sxs-lookup"><span data-stu-id="e03fb-293">To allow a user to create **alerts** and **events** in ServiceNow from OMS:</span></span>

> - <span data-ttu-id="e03fb-294">Olay Yönetimi Modülü yüklü ServiceNow örneğinde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e03fb-294">Ensure you have the Event Management module Installed on your ServiceNow instance.</span></span>

> - <span data-ttu-id="e03fb-295">Aşağıdaki roller için tümleştirme kullanıcı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e03fb-295">Add the following roles to the integration user:</span></span>
>      - <span data-ttu-id="e03fb-296">evt_mgmt_integration</span><span class="sxs-lookup"><span data-stu-id="e03fb-296">evt_mgmt_integration</span></span>
>      - <span data-ttu-id="e03fb-297">evt_mgmt_operator</span><span class="sxs-lookup"><span data-stu-id="e03fb-297">evt_mgmt_operator</span></span>  


## <a name="connect-provance-to-it-service-management-connector-in-oms"></a><span data-ttu-id="e03fb-298">Provance BT hizmetine bağlanmak OMS Yönetimi Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e03fb-298">Connect Provance to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="e03fb-299">Aşağıdaki bölümlerde OMS BT Hizmet Yönetimi Connector Provance ürününüzü bağlanma hakkında ayrıntılar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-299">The following sections provide details about how to connect your Provance product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e03fb-300">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e03fb-300">Prerequisites</span></span>

<span data-ttu-id="e03fb-301">Aşağıdaki önkoşulları yerine olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e03fb-301">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="e03fb-302">BT Hizmet Yönetimi Bağlayıcısı yüklü.</span><span class="sxs-lookup"><span data-stu-id="e03fb-302">IT Service Management Connector installed.</span></span> <span data-ttu-id="e03fb-303">Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="e03fb-303">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="e03fb-304">Azure AD ile - provance uygulama kaydedileceğini ve istemci kimliği kullanımına sunulur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-304">Provance App should be registered with Azure AD - and client ID is made available.</span></span> <span data-ttu-id="e03fb-305">Ayrıntılı bilgi için bkz: [active directory kimlik doğrulamasını yapılandırmak nasıl](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e03fb-305">For detailed information, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>
- <span data-ttu-id="e03fb-306">Kullanıcı rolü: yönetici.</span><span class="sxs-lookup"><span data-stu-id="e03fb-306">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="e03fb-307">Bağlantı yordamı</span><span class="sxs-lookup"><span data-stu-id="e03fb-307">Connection Procedure</span></span>

<span data-ttu-id="e03fb-308">Provance bağlantı oluşturmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-308">Use the following procedure to create a Provance connection:</span></span>

1. <span data-ttu-id="e03fb-309">Git **OMS** > **ayarları** > **bağlı kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-309">Go to **OMS** > **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="e03fb-310">Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-310">Select **ITSM Connector,** click **Add New Connection**.</span></span>  

    ![Provance bağlantı](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. <span data-ttu-id="e03fb-312">Aşağıdaki tabloda açıklandığı gibi bilgileri sağlayın ve tıklayın **kaydetmek** bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e03fb-312">Provide the information as described in the following table, and click **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="e03fb-313">Bu parametre zorunludur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-313">All these parameters are mandatory.</span></span>

| <span data-ttu-id="e03fb-314">**Alan**</span><span class="sxs-lookup"><span data-stu-id="e03fb-314">**Field**</span></span> | <span data-ttu-id="e03fb-315">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e03fb-315">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e03fb-316">**Ad**</span><span class="sxs-lookup"><span data-stu-id="e03fb-316">**Name**</span></span>   | <span data-ttu-id="e03fb-317">BT Hizmet Yönetimi Bağlayıcısı ile bağlanmak istediğiniz Provance örneği için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-317">Type a name for the Provance instance that you want to connect with the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-318">İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-318">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="e03fb-319">**Bağlantı türü seçin**</span><span class="sxs-lookup"><span data-stu-id="e03fb-319">**Select Connection type**</span></span>   | <span data-ttu-id="e03fb-320">Seçin **Provance**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-320">Select **Provance**.</span></span> |
| <span data-ttu-id="e03fb-321">**Kullanıcı Adı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-321">**Username**</span></span>   | <span data-ttu-id="e03fb-322">BT Hizmet Yönetimi Bağlayıcısı bağlanabilmesi için kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-322">Type the user name that can connect to the IT Service Management Connector.</span></span>    |
| <span data-ttu-id="e03fb-323">**Parola**</span><span class="sxs-lookup"><span data-stu-id="e03fb-323">**Password**</span></span>   | <span data-ttu-id="e03fb-324">Bu kullanıcı adıyla ilişkili parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-324">Type the password associated with this user name.</span></span> <span data-ttu-id="e03fb-325">**Not:** kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere OMS hizmet içinde depolanmaz. _</span><span class="sxs-lookup"><span data-stu-id="e03fb-325">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service._</span></span>|
| <span data-ttu-id="e03fb-326">**Sunucu URL'si**</span><span class="sxs-lookup"><span data-stu-id="e03fb-326">**Server URL**</span></span>   | <span data-ttu-id="e03fb-327">BT Hizmet Yönetimi Bağlayıcısı için bağlanmak istediğiniz Provance örneğinizi URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-327">Type the URL of your Provance instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="e03fb-328">**İstemci kimliği**</span><span class="sxs-lookup"><span data-stu-id="e03fb-328">**Client ID**</span></span>   | <span data-ttu-id="e03fb-329">Provance örneğinde oluşturulan bu bağlantısının kimlik doğrulaması için istemci kimliği yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-329">Type the client ID for authenticating this connection, which you generated in your Provance instance.</span></span>  <span data-ttu-id="e03fb-330">İstemci kimliği hakkında daha fazla bilgi [active directory kimlik doğrulamasını yapılandırmak nasıl](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e03fb-330">More information on client ID, see [how to configure active directory authentication](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span> |
| <span data-ttu-id="e03fb-331">**Veri Eşitleme kapsamı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-331">**Data Sync Scope**</span></span>   | <span data-ttu-id="e03fb-332">BT Hizmet Yönetimi bağlayıcısı aracılığıyla OMS eşitlemek istediğiniz Provance iş öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-332">Select the Provance work items that you want to sync to OMS, through the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-333">Bu iş öğeleri günlük analizi aktarılır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-333">These work items are imported into log analytics.</span></span>   <span data-ttu-id="e03fb-334">**Seçenekler:** olaylar, değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-334">**Options:**   Incidents, Change Requests.</span></span>|
| <span data-ttu-id="e03fb-335">**Eşitleme veri**</span><span class="sxs-lookup"><span data-stu-id="e03fb-335">**Sync Data**</span></span> | <span data-ttu-id="e03fb-336">Verileri istediğiniz beri geçen gün sayısını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-336">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="e03fb-337">**Üst sınır**: 120 gün.</span><span class="sxs-lookup"><span data-stu-id="e03fb-337">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="e03fb-338">**ITSM çözümde yeni yapılandırma öğesi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="e03fb-338">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="e03fb-339">Yapılandırma öğeleri ITSM ürün oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-339">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="e03fb-340">Seçili olduğunda, OMS etkilenen CI desteklenen ITSM sistem içinde yapılandırma öğeleri (Cı'ler var olmayan) durumunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-340">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="e03fb-341">**Varsayılan**: devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e03fb-341">**Default**: disabled.</span></span>|

<span data-ttu-id="e03fb-342">Başarıyla bağlanıldı ve eşitlenen kullanıldığında:</span><span class="sxs-lookup"><span data-stu-id="e03fb-342">When successfully connected, and synced:</span></span>

- <span data-ttu-id="e03fb-343">Seçili iş öğelerini Provance bağlantısından OMS aktarılır **günlük analizi.**</span><span class="sxs-lookup"><span data-stu-id="e03fb-343">Selected work items from Provance connection are imported into OMS **Log Analytics.**</span></span>  <span data-ttu-id="e03fb-344">Bu bir özetini görüntüleyebilirsiniz BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-344">You can view the summary of these work items on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="e03fb-345">Olayları ve olayları OMS uyarıları veya günlük arama bu Provance örneğinde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-345">You can create incidents and events from OMS Alerts or Log Search in this Provance instance.</span></span>

<span data-ttu-id="e03fb-346">Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span><span class="sxs-lookup"><span data-stu-id="e03fb-346">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

## <a name="connect-cherwell-to-it-service-management-connector-in-oms"></a><span data-ttu-id="e03fb-347">Cherwell BT hizmetine bağlanmak OMS Yönetimi Bağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="e03fb-347">Connect Cherwell to IT Service Management Connector in OMS</span></span>

<span data-ttu-id="e03fb-348">Aşağıdaki bölümlerde OMS BT Hizmet Yönetimi Connector Cherwell ürününüzü bağlanma hakkında ayrıntılar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-348">The following sections provide details about how to connect your Cherwell product to the IT Service Management Connector in OMS.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e03fb-349">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e03fb-349">Prerequisites</span></span>

<span data-ttu-id="e03fb-350">Aşağıdaki önkoşulları yerine olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="e03fb-350">Ensure you have the following prerequisites met:</span></span>

- <span data-ttu-id="e03fb-351">BT Hizmet Yönetimi Bağlayıcısı yüklü.</span><span class="sxs-lookup"><span data-stu-id="e03fb-351">IT Service Management Connector installed.</span></span> <span data-ttu-id="e03fb-352">Daha fazla bilgi: [yapılandırma](log-analytics-itsmc-overview.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="e03fb-352">More information: [Configuration](log-analytics-itsmc-overview.md#configuration).</span></span>
- <span data-ttu-id="e03fb-353">Oluşturulan istemci kimliği.</span><span class="sxs-lookup"><span data-stu-id="e03fb-353">Client ID generated.</span></span> <span data-ttu-id="e03fb-354">Daha fazla bilgi: [Cherwell için istemci kodu oluştur](#generate-client-id-for-cherwell).</span><span class="sxs-lookup"><span data-stu-id="e03fb-354">More information: [Generate client ID for Cherwell](#generate-client-id-for-cherwell).</span></span>
- <span data-ttu-id="e03fb-355">Kullanıcı rolü: yönetici.</span><span class="sxs-lookup"><span data-stu-id="e03fb-355">User role:  Administrator.</span></span>

### <a name="connection-procedure"></a><span data-ttu-id="e03fb-356">Bağlantı yordamı</span><span class="sxs-lookup"><span data-stu-id="e03fb-356">Connection Procedure</span></span>

<span data-ttu-id="e03fb-357">Cherwell bağlantı oluşturmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-357">Use the following procedure to create a Cherwell connection:</span></span>

1. <span data-ttu-id="e03fb-358">Git **OMS** >  **ayarları** > **bağlı kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-358">Go to **OMS** >  **Settings** > **Connected Sources**.</span></span>
2. <span data-ttu-id="e03fb-359">Seçin **ITSM bağlayıcı** tıklatın **yeni bağlantı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-359">Select **ITSM Connector** click **Add New Connection**.</span></span>  

    ![Cherwell kullanıcı kimliği](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. <span data-ttu-id="e03fb-361">Aşağıdaki tabloda açıklandığı gibi bilgileri sağlayın ve tıklayın **kaydetmek** bağlantı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="e03fb-361">Provide the information as described in the following table, and click  **Save** to create the connection.</span></span>

> [!NOTE]
> <span data-ttu-id="e03fb-362">Bu parametre zorunludur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-362">All these parameters are mandatory.</span></span>

| <span data-ttu-id="e03fb-363">**Alan**</span><span class="sxs-lookup"><span data-stu-id="e03fb-363">**Field**</span></span> | <span data-ttu-id="e03fb-364">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="e03fb-364">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e03fb-365">**Ad**</span><span class="sxs-lookup"><span data-stu-id="e03fb-365">**Name**</span></span>   | <span data-ttu-id="e03fb-366">BT Hizmet Yönetimi Bağlayıcısı bağlanmak istediğiniz Cherwell örneği için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-366">Type a name for the Cherwell instance that you want to connect to the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-367">İş öğeleri bu ITSM yapılandırma / ayrıntılı günlük analizi görünümü, OMS içinde daha sonra bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-367">You use this name later in OMS when you configure work items in this ITSM/ view detailed log analytics.</span></span> |
| <span data-ttu-id="e03fb-368">**Bağlantı türü seçin**</span><span class="sxs-lookup"><span data-stu-id="e03fb-368">**Select Connection type**</span></span>   | <span data-ttu-id="e03fb-369">Seçin **Cherwell.**</span><span class="sxs-lookup"><span data-stu-id="e03fb-369">Select **Cherwell.**</span></span> |
| <span data-ttu-id="e03fb-370">**Kullanıcı Adı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-370">**Username**</span></span>   | <span data-ttu-id="e03fb-371">BT Hizmet Yönetimi bağlayıcı bağlanabilir Cherwell kullanıcı adını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-371">Type the Cherwell user name that can connect to the IT Service Management Connector.</span></span> |
| <span data-ttu-id="e03fb-372">**Parola**</span><span class="sxs-lookup"><span data-stu-id="e03fb-372">**Password**</span></span>   | <span data-ttu-id="e03fb-373">Bu kullanıcı adıyla ilişkili parolayı yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-373">Type the password associated with this user name.</span></span> <span data-ttu-id="e03fb-374">**Not:** kullanıcı adı ve parola yalnızca kimlik doğrulama belirteçleri oluşturmak için kullanılır ve herhangi bir yere OMS hizmet içinde depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-374">**Note:** User name and password are used for generating authentication tokens only, and are not stored anywhere within the OMS service.</span></span>|
| <span data-ttu-id="e03fb-375">**Sunucu URL'si**</span><span class="sxs-lookup"><span data-stu-id="e03fb-375">**Server URL**</span></span>   | <span data-ttu-id="e03fb-376">BT Hizmet Yönetimi Bağlayıcısı için bağlanmak istediğiniz Cherwell örneğinizi URL'sini yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-376">Type the URL of your Cherwell instance that you want to connect to IT Service Management Connector.</span></span> |
| <span data-ttu-id="e03fb-377">**İstemci kimliği**</span><span class="sxs-lookup"><span data-stu-id="e03fb-377">**Client ID**</span></span>   | <span data-ttu-id="e03fb-378">Cherwell örneğinde oluşturulan bu bağlantısının kimlik doğrulaması için istemci kimliği yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-378">Type the client ID for authenticating this connection, which you generated in your Cherwell instance.</span></span>   |
| <span data-ttu-id="e03fb-379">**Veri Eşitleme kapsamı**</span><span class="sxs-lookup"><span data-stu-id="e03fb-379">**Data Sync Scope**</span></span>   | <span data-ttu-id="e03fb-380">BT Hizmet Yönetimi Bağlayıcısı üzerinden eşitlemek istediğiniz Cherwell iş öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-380">Select the Cherwell work items that you want to sync through the IT Service Management Connector.</span></span>  <span data-ttu-id="e03fb-381">Bu iş öğeleri günlük analizi aktarılır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-381">These work items are imported into log analytics.</span></span>   <span data-ttu-id="e03fb-382">**Seçenekler:** olaylar, değişiklik istekleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-382">**Options:**  Incidents, Change Requests.</span></span> |
| <span data-ttu-id="e03fb-383">**Eşitleme veri**</span><span class="sxs-lookup"><span data-stu-id="e03fb-383">**Sync Data**</span></span> | <span data-ttu-id="e03fb-384">Verileri istediğiniz beri geçen gün sayısını yazın.</span><span class="sxs-lookup"><span data-stu-id="e03fb-384">Type the number of past days that you want the data from.</span></span> <span data-ttu-id="e03fb-385">**Üst sınır**: 120 gün.</span><span class="sxs-lookup"><span data-stu-id="e03fb-385">**Maximum limit**: 120 days.</span></span> |
| <span data-ttu-id="e03fb-386">**ITSM çözümde yeni yapılandırma öğesi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="e03fb-386">**Create new configuration item in ITSM solution**</span></span> | <span data-ttu-id="e03fb-387">Yapılandırma öğeleri ITSM ürün oluşturmak istiyorsanız bu seçeneği belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e03fb-387">Select this option if you want to create the configuration items in the ITSM product.</span></span> <span data-ttu-id="e03fb-388">Seçili olduğunda, OMS etkilenen CI desteklenen ITSM sistem içinde yapılandırma öğeleri (Cı'ler var olmayan) durumunda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e03fb-388">When selected, OMS creates the affected CIs as configuration items (in case of non-existing CIs) in the supported ITSM system.</span></span> <span data-ttu-id="e03fb-389">**Varsayılan**: devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e03fb-389">**Default**: disabled.</span></span> |

<span data-ttu-id="e03fb-390">Başarıyla bağlanıldı ve eşitlenen kullanıldığında:</span><span class="sxs-lookup"><span data-stu-id="e03fb-390">When successfully connected, and synced:</span></span>

- <span data-ttu-id="e03fb-391">Seçili iş öğeleri bu Cherwell bağlantısından OMS günlük analizi alınır.</span><span class="sxs-lookup"><span data-stu-id="e03fb-391">Selected work items from this Cherwell connection are imported into OMS Log Analytics.</span></span> <span data-ttu-id="e03fb-392">Bu bir özetini görüntüleyebilirsiniz BT Hizmet Yönetimi Bağlayıcısı kutucuğu iş öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e03fb-392">You can view the summary of these work items  on the IT Service Management Connector tile.</span></span>
- <span data-ttu-id="e03fb-393">Olayları ve olayları bu OMS Cherwell örneğinden oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e03fb-393">You can create incidents and events in this Cherwell instance from OMS.</span></span> <span data-ttu-id="e03fb-394">Daha fazla bilgi: Oluştur ITSM iş öğeleri OMS uyarılar ve ITSM oluşturmak için iş öğelerini OMS günlüklerinden.</span><span class="sxs-lookup"><span data-stu-id="e03fb-394">More information: Create ITSM work items for OMS alerts and Create ITSM work items from OMS logs.</span></span>

<span data-ttu-id="e03fb-395">Daha fazla bilgi: [OMS uyarılar için iş öğeleri oluşturma ITSM](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) ve [OMS günlükleri oluşturmak ITSM iş öğelerinden](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span><span class="sxs-lookup"><span data-stu-id="e03fb-395">More information: [Create ITSM work items for OMS alerts](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) and [Create ITSM work items from OMS logs](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).</span></span>

### <a name="generate-client-id-for-cherwell"></a><span data-ttu-id="e03fb-396">İstemci kimliği için Cherwell oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e03fb-396">Generate client ID for Cherwell</span></span>

<span data-ttu-id="e03fb-397">Cherwell için istemci kimliği/anahtar oluşturmak için aşağıdaki yordamı kullanın:</span><span class="sxs-lookup"><span data-stu-id="e03fb-397">To generate the client ID/key for Cherwell, use the following procedure:</span></span>

1. <span data-ttu-id="e03fb-398">Cherwell Örneğiniz için yönetici olarak oturum açın</span><span class="sxs-lookup"><span data-stu-id="e03fb-398">Log in to your Cherwell instance as admin.</span></span>
2. <span data-ttu-id="e03fb-399">Tıklatın **güvenlik** > **Düzenle REST API İstemci Ayarları**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-399">Click **Security** > **Edit REST API client settings**.</span></span>
3. <span data-ttu-id="e03fb-400">Seçin **oluştur yeni istemci** > **gizli**.</span><span class="sxs-lookup"><span data-stu-id="e03fb-400">Select **Create new client** > **client secret**.</span></span>

    ![Cherwell kullanıcı kimliği](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a><span data-ttu-id="e03fb-402">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e03fb-402">Next steps</span></span>
 - [<span data-ttu-id="e03fb-403">OMS uyarılar için ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e03fb-403">Create ITSM work items for OMS alerts</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [<span data-ttu-id="e03fb-404">OMS günlüklerinden ITSM iş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e03fb-404">Create ITSM work items from OMS logs</span></span>](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [<span data-ttu-id="e03fb-405">Bağlantınız için Görünüm günlük analizi</span><span class="sxs-lookup"><span data-stu-id="e03fb-405">View log analytics for your connection</span></span>](log-analytics-itsmc-overview.md#using-the-solution)
