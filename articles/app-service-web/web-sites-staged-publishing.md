---
title: "Hazırlık ortamları için Azure App Service'te web uygulamalarını yukarı aaaSet | Microsoft Docs"
description: "Toouse yayımlama Azure App Service'deki web uygulamaları için nasıl hazırlanır öğrenin."
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 338424100a20bf823323313fb6699e439f367421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="88611-103">Hazırlık Azure App Service ortamları ayarlama</span><span class="sxs-lookup"><span data-stu-id="88611-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="88611-104">Dağıttığınızda, web uygulaması, Linux, mobil arka uç ve API uygulaması web uygulaması çok[uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), tooa ayrı bir dağıtım yuvası hello varsayılan üretim yuvasına yerine hello çalıştırırken dağıtabilirsiniz **standart**veya **Premium** uygulama hizmeti planı modu.</span><span class="sxs-lookup"><span data-stu-id="88611-104">When you deploy your web app, web app on Linux, mobile back end, and API app too[App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy tooa separate deployment slot instead of hello default production slot when running in hello **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="88611-105">Dağıtım yuvaları, kendi ana bilgisayar adları ile gerçekten Canlı uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="88611-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="88611-106">Uygulama içeriği ve yapılandırmaları öğeleri hello üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="88611-106">App content and configurations elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="88611-107">Uygulama tooa dağıtım yuvası dağıtma hello aşağıdaki faydaları vardır:</span><span class="sxs-lookup"><span data-stu-id="88611-107">Deploying your application tooa deployment slot has hello following benefits:</span></span>

* <span data-ttu-id="88611-108">Hello üretim yuvasıyla değiştirmeden önce hazırlık dağıtım yuvasındaki uygulama değişikliklerini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-108">You can validate app changes in a staging deployment slot before swapping it with hello production slot.</span></span>
* <span data-ttu-id="88611-109">Bir uygulama tooa yuvaya ilk dağıtma ve üretim ile değiştirmeden hello yuvası tüm örneklerini üretime takas önce warmed olduğunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="88611-109">Deploying an app tooa slot first and swapping it into production ensures that all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="88611-110">Uygulamanızı dağıttığınızda bu kapalı kalma süresini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="88611-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="88611-111">Merhaba trafik yeniden yönlendirmesi sorunsuzdur ve değiştirme işlemleri sonucunda hiçbir istek bırakılır.</span><span class="sxs-lookup"><span data-stu-id="88611-111">hello traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="88611-112">Yapılandırarak bu iş akışının tamamı otomatikleştirilebilir [otomatik takas](#Auto-Swap) zaman öncesi takas doğrulama gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="88611-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="88611-113">Değiştirme işleminden sonra önceden hazırlanmış uygulama hello yuvasıyla hello önceki üretim uygulama artık sahiptir.</span><span class="sxs-lookup"><span data-stu-id="88611-113">After a swap, hello slot with previously staged app now has hello previous production app.</span></span> <span data-ttu-id="88611-114">Beklendiği gibi hello üretim yuvasına hello değişiklikleri varsa, tooget "son bilinen iyi sitenizi" geri hemen aynı takas hello gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-114">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good site" back.</span></span>

<span data-ttu-id="88611-115">Her bir uygulama hizmeti planı modu dağıtım yuvaları farklı sayıda destekler.</span><span class="sxs-lookup"><span data-stu-id="88611-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="88611-116">yuva sayısı hello çıkışı toofind uygulamanızın modunu destekliyorsa, bkz: [App Service fiyatlandırması](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="88611-116">toofind out hello number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="88611-117">Uygulamanız birden çok yuvası olduğunda, hello modunu değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-117">When your app has multiple slots, you cannot change hello mode.</span></span>
* <span data-ttu-id="88611-118">Ölçeklendirme için üretim dışı yuvası kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="88611-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="88611-119">Bağlantılı kaynak yönetimi için üretim dışı yuvası desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="88611-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="88611-120">Merhaba, [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) geçici olarak hello üretim dışı yuvası tooa farklı uygulama hizmeti planı modu taşıyarak bu olası etkisini üretim yuvasına yalnızca önleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-120">In hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving hello non-production slot tooa different App Service plan mode.</span></span> <span data-ttu-id="88611-121">Bu hello üretim dışı yuvası hello yine paylaşması Not hello iki yuvaları takas önce hello üretim yuvası ile aynı mod.</span><span class="sxs-lookup"><span data-stu-id="88611-121">Note that hello non-production slot must once again share hello same mode with hello production slot before you can swap hello two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="88611-122">Bir dağıtım yuvası Ekle</span><span class="sxs-lookup"><span data-stu-id="88611-122">Add a deployment slot</span></span>
<span data-ttu-id="88611-123">hello Hello uygulamayı çalıştıran **standart** veya **Premium** modunda sipariş, tooenable için birden çok dağıtım yuvası.</span><span class="sxs-lookup"><span data-stu-id="88611-123">hello app must be running in hello **Standard** or **Premium** mode in order for you tooenable multiple deployment slots.</span></span>

1. <span data-ttu-id="88611-124">Merhaba, [Azure Portal](https://portal.azure.com/), uygulamanızın açmak [kaynak dikey](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="88611-124">In hello [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="88611-125">Merhaba seçin **dağıtım yuvası** seçeneğini ve ardından **yuva Ekle**.</span><span class="sxs-lookup"><span data-stu-id="88611-125">Choose hello **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Yeni bir dağıtım yuvası Ekle][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="88611-127">Merhaba uygulama hello değilse **standart** veya **Premium** modu hazırlanmış yayımlamayı etkinleştirmek için desteklenen hello modları belirten bir ileti alırsınız.</span><span class="sxs-lookup"><span data-stu-id="88611-127">If hello app is not already in hello **Standard** or **Premium** mode, you will receive a message indicating hello supported modes for enabling staged publishing.</span></span> <span data-ttu-id="88611-128">Bu noktada, hello seçeneği tooselect sahip **yükseltme** toohello giderek **ölçek** devam etmeden önce uygulamanızın sekmesi.</span><span class="sxs-lookup"><span data-stu-id="88611-128">At this point, you have hello option tooselect **Upgrade** and navigate toohello **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="88611-129">Merhaba, **bir yuva eklemek** dikey penceresinde hello yuvası bir ad verin ve seçin olup olmadığını başka bir var olan dağıtım yuvadan tooclone uygulama yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="88611-129">In hello **Add a slot** blade, give hello slot a name, and select whether tooclone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="88611-130">Merhaba onay işareti toocontinue'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="88611-130">Click hello check mark toocontinue.</span></span>
   
    ![Yapılandırma kaynağı][ConfigurationSource1]
   
    <span data-ttu-id="88611-132">Merhaba bir yuva eklediğiniz ilk kez, yalnızca iki seçenek gerekir: kopya yuvadan yapılandırma hello varsayılan üretim ya da hiç.</span><span class="sxs-lookup"><span data-stu-id="88611-132">hello first time you add a slot, you will only have two choices: clone configuration from hello default slot in production or not at all.</span></span>
    <span data-ttu-id="88611-133">Birkaç yuvaları oluşturduktan sonra üretim hello dışında bir yuvadan mümkün tooclone yapılandırma olacaktır:</span><span class="sxs-lookup"><span data-stu-id="88611-133">After you have created several slots, you will be able tooclone configuration from a slot other than hello one in production:</span></span>
   
    ![Yapılandırma kaynakları][MultipleConfigurationSources]
4. <span data-ttu-id="88611-135">Uygulamanızın kaynak dikey penceresinde tıklayın **dağıtım yuvası**, ölçümleri ve diğer herhangi bir uygulama gibi yapılandırma kümesi ile Bu yuvanın kaynak dikey bir dağıtım yuvası tooopen'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88611-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot tooopen that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="88611-136">Merhaba hello yuva adını gösterilen hello dikey tooremind hello üstünde görüntülemekte olduğunuz, dağıtım yuvası hello.</span><span class="sxs-lookup"><span data-stu-id="88611-136">hello name of hello slot is shown at hello top of hello blade tooremind you that you are viewing hello deployment slot.</span></span>
   
    ![Dağıtım yuvası başlığı][StagingTitle]
5. <span data-ttu-id="88611-138">Merhaba yuvanın dikey penceresinde Hello uygulama URL'Sİ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="88611-138">Click hello app URL in hello slot's blade.</span></span> <span data-ttu-id="88611-139">Merhaba dağıtım yuvası kendi ana bilgisayar adı olan hem de dinamik uygulama dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="88611-139">Notice hello deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="88611-140">toolimit genel erişim toohello dağıtım yuvası bkz [App Service Web uygulaması – blok web erişim toonon üretim dağıtım yuvaları](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="88611-140">toolimit public access toohello deployment slot, see [App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="88611-141">Dağıtım yuvası oluşturulduktan sonra içerik yok.</span><span class="sxs-lookup"><span data-stu-id="88611-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="88611-142">Farklı depo dalından veya tamamen farklı bir depo toohello yuvadan dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-142">You can deploy toohello slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="88611-143">Merhaba yuvanın yapılandırmasını da değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-143">You can also change hello slot's configuration.</span></span> <span data-ttu-id="88611-144">Kullanım hello içerik güncelleştirmeleri hello dağıtım yuvası ile ilişkili profil veya dağıtım kimlik bilgilerini yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="88611-144">Use hello publish profile or deployment credentials associated with hello deployment slot for content updates.</span></span>  <span data-ttu-id="88611-145">Örneğin, [toothis yuvası git ile yayımlama](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="88611-145">For example, you can [publish toothis slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="88611-146">Dağıtım yuvası için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="88611-146">Configuration for deployment slots</span></span>
<span data-ttu-id="88611-147">Başka bir dağıtım yuvası yapılandırmasından kopyaladığınızda hello kopyalanan düzenlenebilir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="88611-147">When you clone configuration from another deployment slot, hello cloned configuration is editable.</span></span> <span data-ttu-id="88611-148">Ayrıca, diğer yapılandırma öğeleri aynı değiştirme işleminden sonra (Yuva belirli) yuva hello kalır ancak bazı yapılandırma öğeleri takas (değil yuva belirli) hello içeriği izler.</span><span class="sxs-lookup"><span data-stu-id="88611-148">Furthermore, some configuration elements will follow hello content across a swap (not slot specific) while other configuration elements will stay in hello same slot after a swap (slot specific).</span></span> <span data-ttu-id="88611-149">Merhaba aşağıdaki listeleri yuvaları takas yükleyen değiştirecek hello yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="88611-149">hello following lists show hello configuration that will change when you swap slots.</span></span>

<span data-ttu-id="88611-150">**Değiştirilen ayarları**:</span><span class="sxs-lookup"><span data-stu-id="88611-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="88611-151">-Framework sürümü, 32/64-bit, Web yuvaları gibi genel ayarları</span><span class="sxs-lookup"><span data-stu-id="88611-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="88611-152">Uygulama ayarları (yapılandırılmış toostick tooa yuvası olabilir)</span><span class="sxs-lookup"><span data-stu-id="88611-152">App settings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="88611-153">Bağlantı dizeleri (yapılandırılmış toostick tooa yuvası olabilir)</span><span class="sxs-lookup"><span data-stu-id="88611-153">Connection strings (can be configured toostick tooa slot)</span></span>
* <span data-ttu-id="88611-154">İşleyici eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="88611-154">Handler mappings</span></span>
* <span data-ttu-id="88611-155">İzleme ve tanılama ayarları</span><span class="sxs-lookup"><span data-stu-id="88611-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="88611-156">Web işleri içeriği</span><span class="sxs-lookup"><span data-stu-id="88611-156">WebJobs content</span></span>

<span data-ttu-id="88611-157">**Değil takas ayarları**:</span><span class="sxs-lookup"><span data-stu-id="88611-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="88611-158">Yayımlama uç noktaları</span><span class="sxs-lookup"><span data-stu-id="88611-158">Publishing endpoints</span></span>
* <span data-ttu-id="88611-159">Özel etki alanı adları</span><span class="sxs-lookup"><span data-stu-id="88611-159">Custom Domain Names</span></span>
* <span data-ttu-id="88611-160">SSL sertifikaları ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="88611-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="88611-161">Ölçek ayarları</span><span class="sxs-lookup"><span data-stu-id="88611-161">Scale settings</span></span>
* <span data-ttu-id="88611-162">Web işleri zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="88611-162">WebJobs schedulers</span></span>

<span data-ttu-id="88611-163">tooconfigure (takas değil), bir uygulama ayarı veya bağlantı dizesi toostick tooa yuvaya erişim hello **uygulama ayarları** belirli yuvası sonra select hello için dikey **yuva ayarı** hello kutusu Merhaba yuvası takılıyor yapılandırma öğeleri.</span><span class="sxs-lookup"><span data-stu-id="88611-163">tooconfigure an app setting or connection string toostick tooa slot (not swapped), access hello **Application Settings** blade for a specific slot, then select hello **Slot Setting** box for hello configuration elements that should stick hello slot.</span></span> <span data-ttu-id="88611-164">Yuva belirli o öğeye hello uygulamayla ilişkili tüm hello dağıtım yuvaları arasında swappable oluşturma hello etkisi gibi bir yapılandırma öğesi işaretleme unutmayın.</span><span class="sxs-lookup"><span data-stu-id="88611-164">Note that marking a configuration element as slot specific has hello effect of establishing that element as not swappable across all hello deployment slots associated with hello app.</span></span>

![Yuva ayarları][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="88611-166">Dağıtım yuvalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="88611-166">Swap deployment slots</span></span> 
<span data-ttu-id="88611-167">Merhaba dağıtım yuvaları takas **genel bakış** veya **dağıtım yuvası** uygulamanızın kaynak dikey penceresinin görünümü.</span><span class="sxs-lookup"><span data-stu-id="88611-167">You can swap deployment slots in hello **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88611-168">Üretime bir uygulamadan bir dağıtım yuvası takas önce tüm yuva olmayan belirli ayarları tıpkı toohave istediğiniz şekilde yapılandırılmış olduğundan emin olun hello değiştirme hedefi içinde.</span><span class="sxs-lookup"><span data-stu-id="88611-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want toohave it in hello swap target.</span></span>
> 
> 

1. <span data-ttu-id="88611-169">tooswap dağıtım yuvaları, tıklatın hello **takas** düğmesi hello uygulamasının hello komut çubuğunda veya dağıtım yuvasının komut çubuğunda hello.</span><span class="sxs-lookup"><span data-stu-id="88611-169">tooswap deployment slots, click hello **Swap** button in hello command bar of hello app or in hello command bar of a deployment slot.</span></span>
   
    ![Değiştirme düğmesi][SwapButtonBar]

2. <span data-ttu-id="88611-171">Merhaba takas kaynak ve takas hedefleyen düzgün şekilde ayarlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="88611-171">Make sure that hello swap source and swap target are set properly.</span></span> <span data-ttu-id="88611-172">Genellikle, hello takas hello üretim yuvasına hedefidir.</span><span class="sxs-lookup"><span data-stu-id="88611-172">Usually, hello swap target is hello production slot.</span></span> <span data-ttu-id="88611-173">Tıklatın **Tamam** toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="88611-173">Click **OK** toocomplete hello operation.</span></span> <span data-ttu-id="88611-174">Merhaba işlemi bittikten sonra hello dağıtım yuvaları takas.</span><span class="sxs-lookup"><span data-stu-id="88611-174">When hello operation finishes, hello deployment slots have been swapped.</span></span>

    ![Değiştirmeyi Tamamla](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="88611-176">Hello için **Önizleme ile değiştirme** değiştirme türü için bkz: [(çok aşaması takas) önizleme ile değiştirme](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="88611-176">For hello **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="88611-177">(Çok aşaması takas) önizleme ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="88611-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="88611-178">Önizleme ile değiştirme ya da çok aşaması takas yuvası özel yapılandırma öğeleri, bağlantı dizeleri gibi doğrulama basitleştirin.</span><span class="sxs-lookup"><span data-stu-id="88611-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="88611-179">Kritik iş yükleri için uygulama hello toovalidate hello üretim yuvanın yapılandırmasını uygulandığında beklendiği gibi davranır istediğiniz ve böyle doğrulama gerçekleştirmelisiniz *önce* hello uygulama üretime takas.</span><span class="sxs-lookup"><span data-stu-id="88611-179">For mission-critical workloads, you want toovalidate that hello app behaves as expected when hello production slot's configuration is applied, and you must perform such validation *before* hello app is swapped into production.</span></span> <span data-ttu-id="88611-180">Önizleme ile değiştirme ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="88611-180">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="88611-181">Linux üzerinde web uygulamalarında Önizleme ile değiştirme desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="88611-181">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="88611-182">Merhaba kullandığınızda **Önizleme ile değiştirme** seçeneği (bkz [dağıtım yuvaları takas](#Swap)), uygulama hizmeti hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="88611-182">When you use hello **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does hello following:</span></span>

- <span data-ttu-id="88611-183">Tutar hello hedef yuvası değişmemiş şekilde mevcut iş yüküne o yuva (örneğin, üretim) etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="88611-183">Keeps hello destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="88611-184">Merhaba yuvası özgü bağlantı dizeleri ve uygulama ayarları dahil hello hedef yuva toohello kaynak yuvaya, Hello yapılandırma öğeleri için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="88611-184">Applies hello configuration elements of hello destination slot toohello source slot, including hello slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="88611-185">Bu daha önce bahsedilen yapılandırma öğeleri kullanarak hello kaynak yuvaya Hello çalışan işlemleri yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="88611-185">Restarts hello worker processes on hello source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="88611-186">Merhaba takas tamamlandığında: hello hedef yuvaya taşır hello öncesi warmed yukarı kaynak yuvaya.</span><span class="sxs-lookup"><span data-stu-id="88611-186">When you complete hello swap: Moves hello pre-warmed-up source slot into hello destination slot.</span></span> <span data-ttu-id="88611-187">Merhaba hedef yuvaya el ile değiştirme gibi hello kaynak yuvasına taşınır.</span><span class="sxs-lookup"><span data-stu-id="88611-187">hello destination slot is moved into hello source slot as in a manual swap.</span></span>
- <span data-ttu-id="88611-188">İptal zaman hello takas: hello kaynak yuva toohello kaynak yuvaya hello yapılandırma öğeleri yeniden uygular.</span><span class="sxs-lookup"><span data-stu-id="88611-188">When you cancel hello swap: Reapplies hello configuration elements of hello source slot toohello source slot.</span></span>

<span data-ttu-id="88611-189">Merhaba uygulama hello hedef yuvanın yapılandırma ile tam olarak nasıl davranacak önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-189">You can preview exactly how hello app will behave with hello destination slot's configuration.</span></span> <span data-ttu-id="88611-190">Doğrulama tamamlandığında, ayrı bir adım hello değiştirmeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="88611-190">Once you complete validation, you complete hello swap in a separate step.</span></span> <span data-ttu-id="88611-191">Bu adım hello kaynak yuvaya zaten hello istenen yapılandırma ile warmed ve istemcilerin kapalı kalma süresi karşılaşmazsınız fayda hello sahiptir.</span><span class="sxs-lookup"><span data-stu-id="88611-191">This step has hello added advantage that hello source slot is already warmed up with hello desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="88611-192">Hello Azure PowerShell cmdlet'leri çok aşaması takas için kullanılabilir için örnek hello dağıtım yuvası bölümü için Azure PowerShell cmdlet'leri dahil edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="88611-192">Samples for hello Azure PowerShell cmdlets available for multi-phase swap are included in hello Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="88611-193">Otomatik Takas yapılandırın</span><span class="sxs-lookup"><span data-stu-id="88611-193">Configure Auto Swap</span></span>
<span data-ttu-id="88611-194">Otomatik Takas ölçeklendirerek toocontinuously istediğiniz DevOps senaryoları hello uygulama son müşteriler için sıfır cold start ve sıfır kapalı kalma süresi ile uygulamanızı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="88611-194">Auto Swap streamlines DevOps scenarios where you want toocontinuously deploy your app with zero cold start and zero downtime for end customers of hello app.</span></span> <span data-ttu-id="88611-195">Kod güncelleştirme toothat yuvası itme her zaman bir dağıtım yuvası üretim ortamına otomatik takas için yapılandırıldığında, onu zaten hello yuvasına warmed sonra uygulama hizmeti otomatik olarak hello uygulama üretime değiştireceksiniz.</span><span class="sxs-lookup"><span data-stu-id="88611-195">When a deployment slot is configured for Auto Swap into production, every time you push your code update toothat slot, App Service will automatically swap hello app into production after it has already warmed up in hello slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88611-196">Otomatik Takas yuvası için etkinleştirdiğinizde, tam olarak hello hedef yuva (genellikle hello üretim yuvasına) için hedeflenen hello yapılandırma hello yuvası yapılandırması olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88611-196">When you enable Auto Swap for a slot, make sure hello slot configuration is exactly hello configuration intended for hello target slot (usually hello production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="88611-197">Otomatik Takas web uygulamaları Linux üzerinde desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="88611-197">Auto swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="88611-198">Otomatik Takas yuvası için yapılandırma kolaydır.</span><span class="sxs-lookup"><span data-stu-id="88611-198">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="88611-199">Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="88611-199">Follow hello steps below:</span></span>

1. <span data-ttu-id="88611-200">İçinde **dağıtım yuvası**, bir üretim dışı yuva seçin ve **uygulama ayarları** Bu yuvanın kaynak dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="88611-200">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="88611-201">Seçin **üzerinde** için **otomatik takas**seçin hello istenen hedef yuvada **otomatik takas yuvası**, tıklatıp **kaydetmek** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="88611-201">Select **On** for **Auto Swap**, select hello desired target slot in **Auto Swap Slot**, and click **Save** in hello command bar.</span></span> <span data-ttu-id="88611-202">Tam olarak hello hedef yuva için hedeflenen hello yapılandırma hello yuvası için yapılandırma olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="88611-202">Make sure configuration for hello slot is exactly hello configuration intended for hello target slot.</span></span>
   
    <span data-ttu-id="88611-203">Merhaba **bildirimleri** flash yeşil sekmesi **başarı** hello işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="88611-203">hello **Notifications** tab will flash a green **SUCCESS** once hello operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="88611-204">tootest otomatik takas uygulamanız için bir üretim dışı hedef yuvada ilk seçebilirsiniz **otomatik takas yuvası** toobecome hello özelliğiyle tanıdık.</span><span class="sxs-lookup"><span data-stu-id="88611-204">tootest Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** toobecome familiar with hello feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="88611-205">Bir kod itme toothat dağıtım yuvası yürütün.</span><span class="sxs-lookup"><span data-stu-id="88611-205">Execute a code push toothat deployment slot.</span></span> <span data-ttu-id="88611-206">Otomatik Takas kısa bir süre sonra gerçekleşir ve hello güncelleştirme hedef yuvanın URL'de yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="88611-206">Auto Swap will happen after a short time and hello update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="toorollback-a-production-app-after-swap"></a><span data-ttu-id="88611-207">toorollback takas sonra bir üretim uygulaması</span><span class="sxs-lookup"><span data-stu-id="88611-207">toorollback a production app after swap</span></span>
<span data-ttu-id="88611-208">Bir yuva değişikliğinden sonra üretimde herhangi bir hata belirlenirse, hello yuvaları hello aynı iki hemen yuvayı değiştirerek geri tootheir öncesi takas durumları alma.</span><span class="sxs-lookup"><span data-stu-id="88611-208">If any errors are identified in production after a slot swap, roll hello slots back tootheir pre-swap states by swapping hello same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="88611-209">Takas önce özel Isınma</span><span class="sxs-lookup"><span data-stu-id="88611-209">Custom warm-up before swap</span></span>
<span data-ttu-id="88611-210">Bazı uygulamalar özel Isınma Eylemler gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="88611-210">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="88611-211">Merhaba `applicationInitialization` web.config dosyasındaki yapılandırma öğesi sağlar, toospecify özel başlatma eylemleri toobe gerçekleştirilen bir isteği almadan önce.</span><span class="sxs-lookup"><span data-stu-id="88611-211">hello `applicationInitialization` configuration element in web.config allows you toospecify custom initialization actions toobe performed before a request is received.</span></span> <span data-ttu-id="88611-212">Merhaba değiştirme işlemi için bu özel Isınma toocomplete bekler.</span><span class="sxs-lookup"><span data-stu-id="88611-212">hello swap operation will wait for this custom warm-up toocomplete.</span></span> <span data-ttu-id="88611-213">Bir örnek web.config parçası değil.</span><span class="sxs-lookup"><span data-stu-id="88611-213">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="toodelete-a-deployment-slot"></a><span data-ttu-id="88611-214">toodelete bir dağıtım yuvası</span><span class="sxs-lookup"><span data-stu-id="88611-214">toodelete a deployment slot</span></span>
<span data-ttu-id="88611-215">Açık hello dağıtım yuvanın dikey penceresinde, bir dağıtım yuvası için hello dikey penceresine tıklayın **genel bakış** (Merhaba varsayılan sayfa) tıklatıp **silmek** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="88611-215">In hello blade for a deployment slot, open hello deployment slot's blade, click **Overview** (hello default page), and click **Delete** in hello command bar.</span></span>  

![Bir dağıtım yuvası Sil][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="88611-217">Dağıtım yuvaları için Azure PowerShell cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="88611-217">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="88611-218">Azure PowerShell cmdlet'leri toomanage Azure uygulama hizmeti dağıtım yuvalarında yönetmek için destek dahil olmak üzere Windows PowerShell üzerinden Azure sağlayan bir modüldür.</span><span class="sxs-lookup"><span data-stu-id="88611-218">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="88611-219">Yükleme ve yapılandırma Azure PowerShell ve Azure PowerShell'i Azure aboneliğiniz ile kimlik doğrulaması hakkında bilgi için bkz: [nasıl tooinstall ve Microsoft Azure PowerShell yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="88611-219">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How tooinstall and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="88611-220">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="88611-220">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="88611-221">Bir dağıtım yuvası oluşturma</span><span class="sxs-lookup"><span data-stu-id="88611-221">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-toosource-slot"></a><span data-ttu-id="88611-222">Gözden geçirme (çok aşaması takas) ile değiştirme başlatmak ve hedef yuvası yapılandırması toosource yuvaya Uygula</span><span class="sxs-lookup"><span data-stu-id="88611-222">Initiate a swap with review (multi-phase swap) and apply destination slot configuration toosource slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="88611-223">Bekleyen bir değiştirme (gözden geçirme ile değiştirme) iptal kaynak yuvası yapılandırması ve geri yükleme</span><span class="sxs-lookup"><span data-stu-id="88611-223">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="88611-224">Dağıtım yuvalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="88611-224">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="88611-225">Dağıtım yuvası Sil</span><span class="sxs-lookup"><span data-stu-id="88611-225">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="88611-226">Dağıtım yuvaları için Azure komut satırı arabirimi (Azure CLI) komutları</span><span class="sxs-lookup"><span data-stu-id="88611-226">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="88611-227">Hello Azure CLI, uygulama hizmeti dağıtım yuvaları yönetmek için destek dahil olmak üzere, Azure ile çalışmak için platformlar arası komutları sağlar.</span><span class="sxs-lookup"><span data-stu-id="88611-227">hello Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="88611-228">Azure CLI yükleme ve yapılandırma hakkında yönergeler hello için hakkında bilgi de dahil olmak üzere tooconnect Azure CLI tooyour Azure aboneliği bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="88611-228">For instructions on installing and configuring hello Azure CLI, including information on how tooconnect Azure CLI tooyour Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="88611-229">hello Azure CLI, Azure App Service için kullanılabilir toolist hello komutlarını çağıran `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="88611-229">toolist hello commands available for Azure App Service in hello Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="88611-230">İçin [Azure CLI 2.0](https://github.com/Azure/azure-cli) bkz: dağıtım yuvaları için komutları [az appservice web dağıtım yuvası](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="88611-230">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="88611-231">Azure site listesi</span><span class="sxs-lookup"><span data-stu-id="88611-231">azure site list</span></span>
<span data-ttu-id="88611-232">Merhaba geçerli abonelikte hello uygulamalar hakkında daha fazla bilgi için arama **azure site listesi**, aşağıdaki örneğine hello gibi.</span><span class="sxs-lookup"><span data-stu-id="88611-232">For information about hello apps in hello current subscription, call **azure site list**, as in hello following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="88611-233">Azure sitesi oluştur</span><span class="sxs-lookup"><span data-stu-id="88611-233">azure site create</span></span>
<span data-ttu-id="88611-234">bir dağıtım yuvası toocreate çağrısı **azure sitesi oluşturmak** ve var olan bir uygulamanın hello adı ve örnek aşağıdaki hello olduğu gibi hello yuvası toocreate hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="88611-234">toocreate a deployment slot, call **azure site create** and specify hello name of an existing app and hello name of hello slot toocreate, as in hello following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="88611-235">Merhaba yeni yuva, kullanım hello tooenable kaynak denetimi **--git** aşağıdaki örneğine hello olduğu gibi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="88611-235">tooenable source control for hello new slot, use hello **--git** option, as in hello following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="88611-236">Azure site değiştirme</span><span class="sxs-lookup"><span data-stu-id="88611-236">azure site swap</span></span>
<span data-ttu-id="88611-237">toomake güncelleştirilen dağıtım yuvası hello üretim uygulama Merhaba, hello kullan **azure site takas** komutu tooperform aşağıdaki örneğine hello gibi bir değiştirme işlemi.</span><span class="sxs-lookup"><span data-stu-id="88611-237">toomake hello updated deployment slot hello production app, use hello **azure site swap** command tooperform a swap operation, as in hello following example.</span></span> <span data-ttu-id="88611-238">Merhaba üretim uygulamasına herhangi kesinti karşılaşmazsınız veya cold start yapılacaktır.</span><span class="sxs-lookup"><span data-stu-id="88611-238">hello production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="88611-239">Azure site Sil</span><span class="sxs-lookup"><span data-stu-id="88611-239">azure site delete</span></span>
<span data-ttu-id="88611-240">toodelete artık bir dağıtım yuvası hello kullanmak gerekli **azure sitesi silme** aşağıdaki örneğine hello olduğu gibi komutu.</span><span class="sxs-lookup"><span data-stu-id="88611-240">toodelete a deployment slot that is no longer needed, use hello **azure site delete** command, as in hello following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="88611-241">Bir web uygulamasını çalışırken görün.</span><span class="sxs-lookup"><span data-stu-id="88611-241">See a web app in action.</span></span> <span data-ttu-id="88611-242">[App Service'i deneyin](https://azure.microsoft.com/try/app-service/) hemen bir kısa süreli başlangıç uygulaması oluşturun — gerekli herhangi bir kredi kartı veya bir taahhüt.</span><span class="sxs-lookup"><span data-stu-id="88611-242">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="88611-243">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="88611-243">Next Steps</span></span>
<span data-ttu-id="88611-244">[Azure App Service Web uygulaması – web erişim toonon üretim dağıtım yuvalarını engelleme](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[giriş tooApp Linux hizmette](./app-service-linux-intro.md)
[Microsoft Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="88611-244">[Azure App Service Web App – block web access toonon-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
[Introduction tooApp Service on Linux](./app-service-linux-intro.md)
[Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

