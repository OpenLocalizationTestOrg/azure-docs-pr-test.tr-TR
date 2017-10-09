---
title: aaaAzure IOT paketi ile ilgili SSS | Microsoft Docs
description: "IoT Paketi için sık sorulan sorular"
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="75fde-103">IoT Paketi için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="75fde-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="75fde-104">Ayrıca bkz.: hello bağlı Fabrika özel [SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="75fde-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="75fde-105">Merhaba önceden yapılandırılmış çözümleri hello kaynak kodu nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="75fde-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="75fde-106">Merhaba kaynak kodu, GitHub depolarının aşağıdaki hello depolanır:</span><span class="sxs-lookup"><span data-stu-id="75fde-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="75fde-107">[Önceden yapılandırılmış Uzaktan izleme çözümü][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="75fde-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="75fde-108">[Önceden yapılandırılmış Tahmine dayalı bakım çözümü][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="75fde-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="75fde-109">Bağlı Fabrika önceden yapılandırılmış çözümü</span><span class="sxs-lookup"><span data-stu-id="75fde-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="75fde-110">Toohello en son sürümünü kullanan IOT Hub cihaz yönetimi özellikleri hello hello Uzaktan izleme önceden yapılandırılmış çözümün nasıl güncelleştiririm?</span><span class="sxs-lookup"><span data-stu-id="75fde-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="75fde-111">Önceden yapılandırılmış bir çözüm hello https://www.azureiotsuite.com/ sitesinden dağıtırsanız, her zaman hello hello çözümü en son sürümü yeni bir örneğini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="75fde-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="75fde-112">Önceden yapılandırılmış bir çözüm hello komut satırını kullanarak dağıtırsanız, yeni kodu ile var olan bir dağıtıma güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75fde-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="75fde-113">Bkz: [bulut dağıtımı] [ lnk-cloud-deployment] hello GitHub içinde [deposu][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="75fde-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="75fde-114">Bir yeni cihaz yöntemi toohello Uzaktan izleme çözümü desteği nasıl ekleyebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75fde-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="75fde-115">Merhaba bölümüne bakın [yeni bir yöntem toohello simulator desteği eklemek] [ lnk-add-method] hello içinde [önceden yapılandırılmış çözümü özelleştirme] [ lnk-customize] makalesi.</span><span class="sxs-lookup"><span data-stu-id="75fde-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="75fde-116">Merhaba sanal cihaz my istenen özellik değişiklikleri neden yoksayılıyor?</span><span class="sxs-lookup"><span data-stu-id="75fde-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="75fde-117">Hello çözüm önceden yapılandırılmış Uzaktan izleme, benzetimli hello aygıt kodu yalnızca hello kullanır **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** özellikleri istenen tooupdate hello özellikleri bildirdi.</span><span class="sxs-lookup"><span data-stu-id="75fde-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="75fde-118">Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="75fde-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="75fde-119">Cihazımı hello çözüm panosunda, cihazların Merhaba listesi görünmez neden?</span><span class="sxs-lookup"><span data-stu-id="75fde-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="75fde-120">cihazların Merhaba çözüm panosunda Hello listesi sorgu tooreturn hello aygıtların listesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="75fde-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="75fde-121">Şu anda bir sorgu en fazla 10 K aygıtları döndüremez.</span><span class="sxs-lookup"><span data-stu-id="75fde-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="75fde-122">Sorgunuzu Hello arama ölçütlerini daha kısıtlayıcı yapmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="75fde-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="75fde-123">Azure portal ve tıklatmak silme azureiotsuite.com önceden yapılandırılmış bir çözüm üzerinde hello kaynak grubunda silinmesi arasındaki hello fark nedir?</span><span class="sxs-lookup"><span data-stu-id="75fde-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="75fde-124">Merhaba önceden yapılandırılmış çözümü silerseniz [azureiotsuite.com][lnk-azureiotsuite], hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm hello kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="75fde-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="75fde-125">Ek kaynaklar toohello kaynak grubu eklediyseniz, bu kaynakları da silinir.</span><span class="sxs-lookup"><span data-stu-id="75fde-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="75fde-126">Merhaba hello kaynak grubunu silerseniz [Azure portal][lnk-azure-portal], yalnızca bu kaynak grubundaki hello kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="75fde-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="75fde-127">Hello hello önceden yapılandırılmış çözümde ilişkili toodelete hello Azure Active Directory Uygulama etmeniz [Klasik Azure portalı][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="75fde-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="75fde-128">Bir abonelikte kaç IoT Hub örneği sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="75fde-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="75fde-129">Varsayılan olarak, sağlayabilirsiniz [10 IOT hub'ları abonelik başına][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="75fde-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="75fde-130">Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] tooraise bu sınırı.</span><span class="sxs-lookup"><span data-stu-id="75fde-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="75fde-131">Sağlama too10 yukarı önceden yapılandırılmış çözümleri herhangi bir abonelikte yalnızca bir sonucu olarak, her önceden yapılandırılmış çözüm sağlarken bu yana yeni bir IOT Hub'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75fde-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="75fde-132">Bir abonelikte kaç Azure Cosmos DB örneği sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="75fde-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="75fde-133">Elli.</span><span class="sxs-lookup"><span data-stu-id="75fde-133">Fifty.</span></span> <span data-ttu-id="75fde-134">Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] tooraise bu sınırlama, ancak varsayılan olarak, abonelik başına 50 Cosmos DB örnekleri yalnızca sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75fde-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="75fde-135">Bir abonelikte kaç tane Ücretsiz Bing Haritaları API'si sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="75fde-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="75fde-136">İki.</span><span class="sxs-lookup"><span data-stu-id="75fde-136">Two.</span></span> <span data-ttu-id="75fde-137">Bir Azure aboneliğinde Enterprise planları için yalnızca iki adet İç İşlemler Düzey 1 Bing Haritası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75fde-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="75fde-138">Merhaba Uzaktan izleme çözümü, varsayılan hello iç işlemleri düzey 1 planıyla tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="75fde-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="75fde-139">Sonuç olarak, herhangi bir değişiklik yapılmadıysa bir abonelikte çözümlerini izleme uzak tootwo yukarı yalnızca sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="75fde-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="75fde-140">Statik haritaya sahip bir uzaktan izleme çözümü dağıtımım var; etkileşimli bir Bing haritasını nasıl eklerim?</span><span class="sxs-lookup"><span data-stu-id="75fde-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="75fde-141">Kurumsal QueryKey için Bing haritaları API'nizi almak [Azure portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="75fde-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="75fde-142">Toohello Kurumsal için Bing haritaları API'nizi hello olduğu kaynak grubu gidin [Azure portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="75fde-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="75fde-143">Tıklatın **tüm ayarları**, ardından **anahtar yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="75fde-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="75fde-144">İki anahtar görebilirsiniz: **MasterKey** ve **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="75fde-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="75fde-145">Merhaba değerini kopyalayın **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="75fde-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="75fde-146">Kurumsal için Bing Haritaları API'si hesabınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="75fde-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="75fde-147">Merhaba oluşturun [Azure portal] [ lnk-azure-portal] tıklatarak + yeni, Enterprise ve izleme için Bing haritaları API'si arama toocreate ister.</span><span class="sxs-lookup"><span data-stu-id="75fde-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="75fde-148">Merhaba son hello koddan aşağı çekmek [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="75fde-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="75fde-149">Hello deposu hello /docs/ klasöründe hello komut satırı dağıtım rehberini izleyerek dağıtım Bulut veya yerel çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="75fde-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="75fde-150">Yerel çalıştırdıktan veya dağıtım, arama, kök klasörünüzde hello için bulut sonra *. user.config file dosyanızı dağıtımı sırasında oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="75fde-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="75fde-151">Bu dosyayı bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="75fde-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="75fde-152">Değişiklik hello aşağıdaki satır kopyaladığınız tooinclude hello değeri, **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="75fde-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="75fde-153">DreamSpark için Microsoft Azure'a sahipsem önceden yapılandırılmış bir çözüm oluşturabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75fde-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="75fde-154">Şu anda önceden yapılandırılmış bir çözüm oluşturamazsınız bir [DreamSpark için Microsoft Azure] [ lnk-dreamspark] hesabı.</span><span class="sxs-lookup"><span data-stu-id="75fde-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="75fde-155">Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75fde-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="75fde-156">Önceden yapılandırılmış bir çözüm, bulut çözümü sağlayıcısı (CSP) aboneliğiniz varsa oluşturabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="75fde-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="75fde-157">Şu anda bir bulut çözümü sağlayıcısı (CSP) aboneliğiyle önceden yapılandırılmış bir çözüm oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="75fde-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="75fde-158">Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75fde-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="75fde-159">Bir AAD kiracısını nasıl silerim?</span><span class="sxs-lookup"><span data-stu-id="75fde-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="75fde-160">Bkz. Eric Golpe'un blog gönderisi [bir Azure AD Kiracısını silme Kılavuzu][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="75fde-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="75fde-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75fde-161">Next steps</span></span>

<span data-ttu-id="75fde-162">Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="75fde-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="75fde-163">[Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="75fde-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="75fde-164">Önceden yapılandırılmış bağlı Fabrika çözümüne genel bakış</span><span class="sxs-lookup"><span data-stu-id="75fde-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="75fde-165">[Merhaba IOT güvenlikten plan][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="75fde-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance
