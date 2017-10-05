---
title: Azure IOT paketi ile ilgili SSS | Microsoft Docs
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="344ce-103">IoT Paketi için sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="344ce-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="344ce-104">Ayrıca bkz.: bağlı Fabrika özel [SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="344ce-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="344ce-105">Önceden yapılandırılmış çözümleri için kaynak kodunu nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="344ce-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="344ce-106">Kaynak kodu aşağıdaki GitHub depolarının depolanır:</span><span class="sxs-lookup"><span data-stu-id="344ce-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="344ce-107">[Önceden yapılandırılmış Uzaktan izleme çözümü][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="344ce-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="344ce-108">[Önceden yapılandırılmış Tahmine dayalı bakım çözümü][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="344ce-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="344ce-109">Bağlı Fabrika önceden yapılandırılmış çözümü</span><span class="sxs-lookup"><span data-stu-id="344ce-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="344ce-110">IOT Hub cihaz yönetimi özellikleri kullanan Uzaktan izleme önceden yapılandırılmış çözümü en son sürümüne nasıl güncelleştiririm?</span><span class="sxs-lookup"><span data-stu-id="344ce-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="344ce-111">Önceden yapılandırılmış bir çözüm https://www.azureiotsuite.com/ sitesinden dağıtırsanız, her zaman çözüm en son sürümünü yeni bir örneğini dağıtır.</span><span class="sxs-lookup"><span data-stu-id="344ce-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="344ce-112">Komut satırını kullanarak önceden yapılandırılmış bir çözüm dağıtırsanız, yeni kodu ile var olan bir dağıtıma güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="344ce-113">Bkz: [bulut dağıtımı] [ lnk-cloud-deployment] github'da [deposu][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="344ce-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="344ce-114">Uzaktan izleme önceden yapılandırılmış çözümü için yeni bir cihaz yöntemi desteğini nasıl ekleyebilirim?</span><span class="sxs-lookup"><span data-stu-id="344ce-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="344ce-115">Bölümüne bakın [simulator için yeni bir yöntem için destek eklemek] [ lnk-add-method] içinde [önceden yapılandırılmış çözümü özelleştirme] [ lnk-customize] makalesi.</span><span class="sxs-lookup"><span data-stu-id="344ce-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="344ce-116">Sanal cihaz my istenen özellik değişiklikleri neden yoksayılıyor?</span><span class="sxs-lookup"><span data-stu-id="344ce-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="344ce-117">Uzaktan izleme önceden yapılandırılmış çözümde sanal cihaz kod yalnızca **Desired.Config.TemperatureMeanValue** ve **Desired.Config.TelemetryInterval** bildirilen özellikleri güncelleştirmek için özellikler istenen.</span><span class="sxs-lookup"><span data-stu-id="344ce-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="344ce-118">Diğer tüm istenen özelliği değişiklik isteklerini göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="344ce-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="344ce-119">Cihazımı çözüm panosunda aygıtların listesi görünmez neden?</span><span class="sxs-lookup"><span data-stu-id="344ce-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="344ce-120">Çözüm panosunda aygıtların listesi, cihaz listesini döndürmek için bir sorgu kullanır.</span><span class="sxs-lookup"><span data-stu-id="344ce-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="344ce-121">Şu anda bir sorgu en fazla 10 K aygıtları döndüremez.</span><span class="sxs-lookup"><span data-stu-id="344ce-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="344ce-122">Arama ölçütlerini sorgunuza daha kısıtlayıcı yapmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="344ce-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="344ce-123">Azure portalında bir kaynak grubunu silmek ile azureiotsuite.com'da önceden yapılandırılmış bir çözüm için silmeye tıklama arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="344ce-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="344ce-124">Önceden yapılandırılmış çözümü silerseniz [azureiotsuite.com][lnk-azureiotsuite], önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="344ce-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="344ce-125">Kaynak grubuna ek kaynaklar eklediyseniz, bu kaynakları da silinir.</span><span class="sxs-lookup"><span data-stu-id="344ce-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="344ce-126">Kaynak grubunu silerseniz [Azure portal][lnk-azure-portal], yalnızca bu kaynak grubundaki kaynakları silersiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="344ce-127">Ayrıca önceden yapılandırılmış Çözümle ilişkili Azure Active Directory Uygulama silmenize gerek [Klasik Azure portalı][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="344ce-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="344ce-128">Bir abonelikte kaç IoT Hub örneği sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="344ce-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="344ce-129">Varsayılan olarak, sağlayabilirsiniz [10 IOT hub'ları abonelik başına][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="344ce-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="344ce-130">Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] bu sınırı artırmak için.</span><span class="sxs-lookup"><span data-stu-id="344ce-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="344ce-131">Sonuç olarak, önceden yapılandırılmış her çözüm yeni bir IOT hub'ı hazırlar olduğundan, yalnızca belirli bir aboneliğe en fazla 10 önceden yapılandırılmış çözümü sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="344ce-132">Bir abonelikte kaç Azure Cosmos DB örneği sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="344ce-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="344ce-133">Elli.</span><span class="sxs-lookup"><span data-stu-id="344ce-133">Fifty.</span></span> <span data-ttu-id="344ce-134">Oluşturabileceğiniz bir [Azure destek bileti] [ link-azuresupportticket] bu sınırı artırmak için ancak varsayılan olarak, abonelik başına 50 Cosmos DB örnekleri yalnızca sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="344ce-135">Bir abonelikte kaç tane Ücretsiz Bing Haritaları API'si sağlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="344ce-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="344ce-136">İki.</span><span class="sxs-lookup"><span data-stu-id="344ce-136">Two.</span></span> <span data-ttu-id="344ce-137">Bir Azure aboneliğinde Enterprise planları için yalnızca iki adet İç İşlemler Düzey 1 Bing Haritası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="344ce-138">Uzaktan izleme çözümü, varsayılan olarak bir İç İşlemler Düzey 1 planı ile hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="344ce-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="344ce-139">Sonuç olarak, herhangi bir değişiklik yapılmadıysa bir abonelikte yalnızca en fazla iki tane uzaktan izleme çözümü sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="344ce-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="344ce-140">Statik haritaya sahip bir uzaktan izleme çözümü dağıtımım var; etkileşimli bir Bing haritasını nasıl eklerim?</span><span class="sxs-lookup"><span data-stu-id="344ce-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="344ce-141">Kurumsal QueryKey için Bing haritaları API'nizi almak [Azure portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="344ce-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="344ce-142">Kurumsal için Bing haritaları API'nizi olduğu kaynak grubuna gidin [Azure portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="344ce-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="344ce-143">Tıklatın **tüm ayarları**, ardından **anahtar yönetimi**.</span><span class="sxs-lookup"><span data-stu-id="344ce-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="344ce-144">İki anahtar görebilirsiniz: **MasterKey** ve **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="344ce-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="344ce-145">Değeri kopyalama **QueryKey**.</span><span class="sxs-lookup"><span data-stu-id="344ce-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="344ce-146">Kurumsal için Bing Haritaları API'si hesabınız yok mu?</span><span class="sxs-lookup"><span data-stu-id="344ce-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="344ce-147">Oluşturun [Azure portal] [ lnk-azure-portal] göre tıklayarak + yeni, Kurumsal için Bing haritaları API'si için arama ve oluşturmak için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="344ce-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="344ce-148">En son koddan aşağı çekmek [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="344ce-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="344ce-149">Depodaki /docs/ klasöründe komut satırı dağıtım rehberini izleyerek dağıtım Bulut veya yerel çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="344ce-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="344ce-150">Yerel bir dağıtım veya bir bulut dağıtımını çalıştırdıktan sonra, kök klasörünüzde dağıtım sırasında oluşturulan *.user.config file dosyanızı arayın.</span><span class="sxs-lookup"><span data-stu-id="344ce-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="344ce-151">Bu dosyayı bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="344ce-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="344ce-152">Kopyaladığınız değeri eklemek için aşağıdaki satırı değiştirin, **QueryKey**:</span><span class="sxs-lookup"><span data-stu-id="344ce-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="344ce-153">DreamSpark için Microsoft Azure'a sahipsem önceden yapılandırılmış bir çözüm oluşturabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="344ce-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="344ce-154">Şu anda önceden yapılandırılmış bir çözüm oluşturamazsınız bir [DreamSpark için Microsoft Azure] [ lnk-dreamspark] hesabı.</span><span class="sxs-lookup"><span data-stu-id="344ce-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="344ce-155">Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="344ce-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="344ce-156">Önceden yapılandırılmış bir çözüm, bulut çözümü sağlayıcısı (CSP) aboneliğiniz varsa oluşturabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="344ce-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="344ce-157">Şu anda bir bulut çözümü sağlayıcısı (CSP) aboneliğiyle önceden yapılandırılmış bir çözüm oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="344ce-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="344ce-158">Ancak, oluşturabileceğiniz bir [ücretsiz deneme hesabı için Azure] [ lnk-30daytrial] sağlayan yalnızca birkaç dakika içinde önceden yapılandırılmış bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="344ce-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="344ce-159">Bir AAD kiracısını nasıl silerim?</span><span class="sxs-lookup"><span data-stu-id="344ce-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="344ce-160">Bkz. Eric Golpe'un blog gönderisi [bir Azure AD Kiracısını silme Kılavuzu][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="344ce-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="344ce-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="344ce-161">Next steps</span></span>

<span data-ttu-id="344ce-162">Önceden yapılandırılmış IoT Suite çözümlerinin diğer özelliklerinden bazılarını da keşfedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="344ce-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="344ce-163">[Önceden yapılandırılmış Tahmine dayalı bakım çözümüne genel bakış][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="344ce-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="344ce-164">Önceden yapılandırılmış bağlı Fabrika çözümüne genel bakış</span><span class="sxs-lookup"><span data-stu-id="344ce-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="344ce-165">[Baştan sona IoT güvenliği][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="344ce-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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
