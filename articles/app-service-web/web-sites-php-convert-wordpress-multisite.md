---
title: "Birden çok tesis Azure App Service'te WordPress Dönüştür"
description: "Azure galerisinde aracılığıyla oluşturulan mevcut bir WordPress web uygulaması ele öğrenin ve WordPress çoklu site için Dönüştür"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 4a15fb5e97d2ca57e5883c07651c372c54021c92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="convert-wordpress-to-multisite-in-azure-app-service"></a><span data-ttu-id="674ed-103">Birden çok tesis Azure App Service'te WordPress Dönüştür</span><span class="sxs-lookup"><span data-stu-id="674ed-103">Convert WordPress to Multisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="674ed-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="674ed-104">Overview</span></span>
<span data-ttu-id="674ed-105">*Tarafından [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies, Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="674ed-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="674ed-106">Bu öğreticide, Azure galerisinde aracılığıyla oluşturulan mevcut bir WordPress web uygulaması almak ve bir WordPress çoklu site yükleme dönüştürmek öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="674ed-106">In this tutorial, you will learn how to take an existing WordPress web app created through the gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="674ed-107">Ayrıca, her yüklemenizi içinde siteler için özel bir etki alanı atama hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="674ed-107">Additionally, you will learn how to assign a custom domain to each of the subsites within your install.</span></span>

<span data-ttu-id="674ed-108">WordPress olan bir yüklemesini sahip varsayılır.</span><span class="sxs-lookup"><span data-stu-id="674ed-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="674ed-109">Bunu yapmazsanız, Lütfen sağlanan yönergeleri izleyin [Azure galerisinden bir WordPress web sitesi oluşturmak][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="674ed-109">If you do not, please follow the guidance provided in [Create a WordPress web site from the gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="674ed-110">Varolan bir WordPress dönüştürme tek bir site yüklemek için birden çok tesis genellikle oldukça basittir ve ilk adımlar burada çoğunu düz nereden geldiği [A ağ oluştur] [ wordpress-codex-create-a-network] sayfasında [ WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="674ed-110">Converting an existing WordPress single site install to Multisite is generally fairly simple, and many of the initial steps here come straight from the [Create A Network][wordpress-codex-create-a-network] page on the [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="674ed-111">Haydi başlayalım.</span><span class="sxs-lookup"><span data-stu-id="674ed-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="674ed-112">Birden çok tesis izin ver</span><span class="sxs-lookup"><span data-stu-id="674ed-112">Allow Multisite</span></span>
<span data-ttu-id="674ed-113">İlk aracılığıyla çoklu site etkinleştirmeniz gerekiyor `wp-config.php` ile dosya **WP\_izin\_birden çok TESİS** sabit.</span><span class="sxs-lookup"><span data-stu-id="674ed-113">You first need to enable Multisite through the `wp-config.php` file with the **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="674ed-114">Web uygulama dosyalarınızı düzenlemek için iki yöntem vardır: FTP ve Git aracılığıyla ikinci ilk aracılığıyladır.</span><span class="sxs-lookup"><span data-stu-id="674ed-114">There are two methods to edit your web app files: the first is through FTP, and the second through Git.</span></span> <span data-ttu-id="674ed-115">Lütfen, bu yöntemlerden birini Kurulum konusunda bilginiz yoksa, aşağıdaki öğreticiler başvurun:</span><span class="sxs-lookup"><span data-stu-id="674ed-115">If you are unfamiliar with how to setup either of these methods, please refer to the following tutorials:</span></span>

* <span data-ttu-id="674ed-116">[PHP web sitesiyle MySQL ve FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="674ed-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="674ed-117">[PHP web sitesiyle MySQL ve Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="674ed-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="674ed-118">Açık `wp-config.php` dosya düzenleyicisiyle ve yukarıdaki aşağıdakileri ekleyin `/* That's all, stop editing! Happy blogging. */` satır.</span><span class="sxs-lookup"><span data-stu-id="674ed-118">Open the `wp-config.php` file with the editor of your choosing and add the following above the `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="674ed-119">Dosyayı kaydedin ve sunucuya geri yüklemek emin olun!</span><span class="sxs-lookup"><span data-stu-id="674ed-119">Be sure to save the file and upload it back to the server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="674ed-120">Ağ Kurulumu</span><span class="sxs-lookup"><span data-stu-id="674ed-120">Network Setup</span></span>
<span data-ttu-id="674ed-121">Oturum *wp-yönetici* web uygulamanız ve alanının altında yeni bir öğe görmelisiniz **Araçları** adlı menüsü **ağ kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="674ed-121">Log in to the *wp-admin* area of your web app and you should see a new item under the **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="674ed-122">Tıklatın **ağ kurulumu** ve ağınızın ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="674ed-122">Click **Network Setup** and fill in the details of your network.</span></span>

![Ağ Kurulum Ekranı][wordpress-network-setup]

<span data-ttu-id="674ed-124">Bu öğretici kullanır *alt dizinleri* çünkü her zaman çalışması gerekir ve size özel etki alanları her alt site için daha sonra öğreticide ayarlarını yapacak şema site.</span><span class="sxs-lookup"><span data-stu-id="674ed-124">This tutorial uses the *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in the tutorial.</span></span> <span data-ttu-id="674ed-125">Ancak, bir alt etki alanı yüklemek üzerinden bir etki alanına eşlerseniz Kurulum mümkün olmalıdır [Azure Portal](https://portal.azure.com) ve joker DNS düzgün şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="674ed-125">However, it should be possible to setup a subdomain install if you map a domain through the [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="674ed-126">Alt dizin kurulumları alt etki alanı vs hakkında daha fazla bilgi için bkz: [çok siteli ağ türlerini] [ wordpress-codex-types-of-networks] makale üzerinde WordPress Codex.</span><span class="sxs-lookup"><span data-stu-id="674ed-126">For more information on sub-domain vs sub-directory setups see the [Types of multisite network][wordpress-codex-types-of-networks] article on the WordPress Codex.</span></span>

## <a name="enable-the-network"></a><span data-ttu-id="674ed-127">Ağ etkinleştir</span><span class="sxs-lookup"><span data-stu-id="674ed-127">Enable the Network</span></span>
<span data-ttu-id="674ed-128">Ağ veritabanında yapılandırılmıştır, ancak ağ işlevselliğini etkinleştirmek için bir geri kalan adımı yok.</span><span class="sxs-lookup"><span data-stu-id="674ed-128">The network is now configured in the database, but there is one remaining step to enable the network functionality.</span></span> <span data-ttu-id="674ed-129">Sonlandırma `wp-config.php` ayarları ve olun `web.config` her site düzgün bir şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="674ed-129">Finalize the `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="674ed-130">' I tıklattıktan sonra **yükleme** düğmesini *ağ kurulumu* sayfasında, WordPress güncelleştirmek deneyecek `wp-config.php` ve `web.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="674ed-130">After clicking the **Install** button on the *Network Setup* page, WordPress will attempt to update the `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="674ed-131">Ancak, güncelleştirmelerinin başarılı sağlamak üzere dosyaları her zaman kontrol etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="674ed-131">However, you should always check the files to ensure the updates were successful.</span></span> <span data-ttu-id="674ed-132">Aksi durumda, bu ekranı ile gerekli güncelleştirmeleri sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="674ed-132">If not, this screen will present you with the necessary updates.</span></span> <span data-ttu-id="674ed-133">Düzenle ve dosyaları kaydedebilir.</span><span class="sxs-lookup"><span data-stu-id="674ed-133">Edit and save the files.</span></span>

<span data-ttu-id="674ed-134">Yaptıktan sonra oturumu kapatın ve oturum gerekir bu güncelleştirmeler wp-yönetici panoya yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="674ed-134">After making these updates you will need to log out and log back into the wp-admin dashboard.</span></span>

<span data-ttu-id="674ed-135">Şimdi olmamalıdır ek bir menü etiketli yönetici çubuğunda **Sitelerim**.</span><span class="sxs-lookup"><span data-stu-id="674ed-135">There should now be an additional menu on the admin bar labeled **My Sites**.</span></span> <span data-ttu-id="674ed-136">Bu menü, yeni ağınız üzerinden denetlemenize olanak tanır **ağ yönetim** Pano.</span><span class="sxs-lookup"><span data-stu-id="674ed-136">This menu allows you to control your new network through the **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="674ed-137">Özel etki alanlarını ekleme</span><span class="sxs-lookup"><span data-stu-id="674ed-137">Adding custom domains</span></span>
<span data-ttu-id="674ed-138">[WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] eklentisi özel etki alanlarını, ağınızdaki herhangi bir siteye eklemek için bir kolay sağlar.</span><span class="sxs-lookup"><span data-stu-id="674ed-138">The [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze to add custom domains to any site in your network.</span></span> <span data-ttu-id="674ed-139">Eklenti düzgün çalışması Portal ve etki alanı kayıt şirketinizdeki bazı ek ayar yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="674ed-139">In order for the plugin to operate properly, you need to do some additional setup on the Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-to-the-web-app"></a><span data-ttu-id="674ed-140">Web uygulamasının etki alanı eşleştirmeye izin ver</span><span class="sxs-lookup"><span data-stu-id="674ed-140">Enable domain mapping to the web app</span></span>
<span data-ttu-id="674ed-141">**Serbest** [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) planı modu Web uygulamaları için özel etki alanlarını ekleme desteklemez.</span><span class="sxs-lookup"><span data-stu-id="674ed-141">The **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains to Web Apps.</span></span> <span data-ttu-id="674ed-142">Geçiş gerekecek **paylaşılan** veya **standart** modu.</span><span class="sxs-lookup"><span data-stu-id="674ed-142">You will need to switch to **Shared** or **Standard** mode.</span></span> <span data-ttu-id="674ed-143">Bunu yapmak için:</span><span class="sxs-lookup"><span data-stu-id="674ed-143">To do this:</span></span>

* <span data-ttu-id="674ed-144">Azure portalında oturum açın ve web uygulamanızı bulun.</span><span class="sxs-lookup"><span data-stu-id="674ed-144">Log in to the Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="674ed-145">Tıklayın **ölçeği** sekmesinde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="674ed-145">Click on the **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="674ed-146">Altında **genel**, şunlardan birini seçin *paylaşılan* veya *standart*</span><span class="sxs-lookup"><span data-stu-id="674ed-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="674ed-147">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="674ed-147">Click **Save**</span></span>

<span data-ttu-id="674ed-148">Kullanım ve ayarladığınız yapılandırmanın bağlı olarak değişiklik doğrulayın ve web uygulamanız şimdi bir maliyet maruz kalabilirsiniz kabul isteyen bir ileti alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="674ed-148">You may receive a message asking you to verify the change and acknowledge your web app may now incur a cost, depending upon usage and the other configuration you set.</span></span>

<span data-ttu-id="674ed-149">Yeni ayarları işlemek için birkaç saniye sürer artık etki alanınızı ayarlama başlatmak için uygun bir zamandır.</span><span class="sxs-lookup"><span data-stu-id="674ed-149">It takes a few seconds to process the new settings, so now is a good time to start setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="674ed-150">Etki alanınızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="674ed-150">Verify your domain</span></span>
<span data-ttu-id="674ed-151">Azure Web Apps siteye etki alanını eşlemek sağlayacak önce ilk etki alanını eşlemek için yetkiye sahip doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="674ed-151">Before Azure Web Apps will allow you to map a domain to the site, you first need to verify that you have the authorization to map the domain.</span></span> <span data-ttu-id="674ed-152">Bunu yapmak için yeni bir CNAME kaydı, DNS girdisini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="674ed-152">To do so, you must add a new CNAME record to your DNS entry.</span></span>

* <span data-ttu-id="674ed-153">Etki alanınızın DNS Yöneticisi için oturum açın</span><span class="sxs-lookup"><span data-stu-id="674ed-153">Log in to your domain's DNS manager</span></span>
* <span data-ttu-id="674ed-154">Yeni bir CNAME oluşturmanız *awverify*</span><span class="sxs-lookup"><span data-stu-id="674ed-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="674ed-155">Noktası *awverify* için *awverify. YOUR_DOMAIN.azurewebsites.NET*</span><span class="sxs-lookup"><span data-stu-id="674ed-155">Point *awverify* to *awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="674ed-156">DNS değişikliklerin tam yürürlüğe gidin, aşağıdaki adımları hemen çalışmazsa kahve, kupaya olun sonra geri dönün ve yeniden deneyin şekilde gitmek biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="674ed-156">It may take some time for the DNS changes to go into full effect, so if the following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-the-domain-to-the-web-app"></a><span data-ttu-id="674ed-157">Web uygulaması için etki alanı ekleme</span><span class="sxs-lookup"><span data-stu-id="674ed-157">Add the domain to the web app</span></span>
<span data-ttu-id="674ed-158">Web uygulamanız Azure Portalı aracılığıyla dönün, tıklatın **ayarları**ve ardından **özel etki alanları ve SSL**.</span><span class="sxs-lookup"><span data-stu-id="674ed-158">Return to your web app through the Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="674ed-159">Zaman *SSL ayarları* olan görüntülenir, burada girdiğiniz web uygulamanıza atamak istediğiniz tüm etki alanları görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="674ed-159">When the *SSL settings* are displayed, you will see the fields where you will input all the domains which you wish to assign to your web app.</span></span> <span data-ttu-id="674ed-160">Bir etki alanı burada listelenmiyorsa, DNS etki alanı kurulumu nasıl olduğunu bağımsız olarak eşleme WordPress içinde kullanılabilir olmaz.</span><span class="sxs-lookup"><span data-stu-id="674ed-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how the domain DNS is setup.</span></span>

![Özel etki alanlarını iletişim yönetme][wordpress-manage-domains]

<span data-ttu-id="674ed-162">Azure etki alanınızın metin kutusuna yazdıktan sonra daha önce oluşturduğunuz CNAME kaydı doğrular.</span><span class="sxs-lookup"><span data-stu-id="674ed-162">After typing your domain into the text box, Azure will verify the CNAME record you created previously.</span></span> <span data-ttu-id="674ed-163">DNS tam olarak yayılmadan değil varsa, kırmızı bir gösterge gösterir.</span><span class="sxs-lookup"><span data-stu-id="674ed-163">If the DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="674ed-164">Başarılı olduysa, yeşil bir onay işareti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="674ed-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="674ed-165">İletişim kutusunun en altında listelenen IP adresini not alın.</span><span class="sxs-lookup"><span data-stu-id="674ed-165">Take note of the IP Address listed at the bottom of the dialog.</span></span> <span data-ttu-id="674ed-166">Bu kurulum, etki alanınız için A kaydı gerekir.</span><span class="sxs-lookup"><span data-stu-id="674ed-166">You will need this to setup the A record for your domain.</span></span>

## <a name="setup-the-domain-a-record"></a><span data-ttu-id="674ed-167">Etki alanı kayıt Kurulumu</span><span class="sxs-lookup"><span data-stu-id="674ed-167">Setup the domain A record</span></span>
<span data-ttu-id="674ed-168">Diğer adımlar başarılı olursa, Azure web uygulamanıza bir DNS A kaydı aracılığıyla etki alanı artık atayabilir.</span><span class="sxs-lookup"><span data-stu-id="674ed-168">If the other steps were successful, you may now assign the domain to your Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="674ed-169">Burada Azure web uygulamaları CNAME ve A kayıtları ancak kabul olduğunu dikkate almak önemlidir, *gerekir* uygun etki alanı eşleme etkinleştirmek için bir A kaydı kullanın.</span><span class="sxs-lookup"><span data-stu-id="674ed-169">It is important to note here that Azure web apps accept both CNAME and A records, however you *must* use an A record to enable proper domain mapping.</span></span> <span data-ttu-id="674ed-170">Nelerin sizin için YOUR_DOMAIN.azurewebsites.net ile oluşturulan Azure olduğu başka bir CNAME için bir CNAME iletilemez.</span><span class="sxs-lookup"><span data-stu-id="674ed-170">A CNAME cannot be forwarded to another CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="674ed-171">Önceki adımdaki IP adresini kullanarak, DNS Yöneticisi'ne dönmek ve kurulum için bu IP işaret edecek şekilde A kaydı.</span><span class="sxs-lookup"><span data-stu-id="674ed-171">Using the IP address from the previous step, return to your DNS manager and setup the A record to point to that IP.</span></span>

## <a name="install-and-setup-the-plugin"></a><span data-ttu-id="674ed-172">Yükleme ve Kurulum eklentisi</span><span class="sxs-lookup"><span data-stu-id="674ed-172">Install and setup the plugin</span></span>
<span data-ttu-id="674ed-173">WordPress çoklu site şu anda özel etki alanlarını eşlemek için yerleşik bir yöntem sahip değil.</span><span class="sxs-lookup"><span data-stu-id="674ed-173">WordPress Multisite currently does not have a built-in method to map custom domains.</span></span> <span data-ttu-id="674ed-174">Ancak, adlı bir eklenti yoktur [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] , sizin için işlevsellik ekler.</span><span class="sxs-lookup"><span data-stu-id="674ed-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds the functionality for you.</span></span> <span data-ttu-id="674ed-175">Sitenizin ağ yönetim bölümünü oturum açın ve yükleme **WordPress MU etki alanı eşleme** eklentisi.</span><span class="sxs-lookup"><span data-stu-id="674ed-175">Log in to the Network Admin portion of your site and install the **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="674ed-176">Yükleme ve eklenti etkinleştirdikten sonra ziyaret edin **ayarları** > **etki alanı eşleme** eklentiyi yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="674ed-176">After installing and activating the plugin, visit **Settings** > **Domain Mapping** to configure the plugin.</span></span> <span data-ttu-id="674ed-177">İlk metin kutusuna *sunucusu IP adresi*, etki alanı için bir kayıt kurulumu için kullanılan IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="674ed-177">In the first textbox, *Server IP Address*, input the IP Address you used to setup the A record for the domain.</span></span> <span data-ttu-id="674ed-178">Herhangi ayarlayın *etki alanı seçenekleri* size (varsayılan değerler genellikle ince) istekleri ve tıklayın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="674ed-178">Set any *Domain Options* you desire (the defaults are often fine) and click **Save**.</span></span>

## <a name="map-the-domain"></a><span data-ttu-id="674ed-179">Etki alanına Eşle</span><span class="sxs-lookup"><span data-stu-id="674ed-179">Map the domain</span></span>
<span data-ttu-id="674ed-180">Ziyaret **Pano** etki alanına Eşle istediğiniz site için.</span><span class="sxs-lookup"><span data-stu-id="674ed-180">Visit the **Dashboard** for the site you wish to map the domain to.</span></span> <span data-ttu-id="674ed-181">Tıklayın **Araçları** > **etki alanı eşleme** ve yeni etki alanı tıklatın ve metin kutusu yazın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="674ed-181">Click on **Tools** > **Domain Mapping** and type the new domain into the textbox and click **Add**.</span></span>

<span data-ttu-id="674ed-182">Varsayılan olarak, yeni etki alanı otomatik olarak oluşturulur site, etki alanı için yazılacaktır.</span><span class="sxs-lookup"><span data-stu-id="674ed-182">By default, the new domain will be rewritten to the autogenerated site domain.</span></span> <span data-ttu-id="674ed-183">Yeni etki alanına onay gönderilen tüm trafiğin sahip olmak istiyorsanız *bu blog için birincil etki alanı* kutusunu kaydetmeden önce.</span><span class="sxs-lookup"><span data-stu-id="674ed-183">If you want to have all traffic sent to the new domain, check the *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="674ed-184">Etki alanları sınırsız sayıda bir siteye ekleyebilirsiniz, ancak yalnızca bir birincil olabilir.</span><span class="sxs-lookup"><span data-stu-id="674ed-184">You can add an unlimited number of domains to a site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="674ed-185">Yeniden yapın</span><span class="sxs-lookup"><span data-stu-id="674ed-185">Do it again</span></span>
<span data-ttu-id="674ed-186">Azure Web uygulamaları bir web uygulaması için etki alanları sınırsız sayıda eklemenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="674ed-186">Azure Web Apps allow you to add an unlimited number of domains to a web app.</span></span> <span data-ttu-id="674ed-187">Yürütülecek gerekir başka bir etki alanına eklemek için **etki alanınızı doğrulayın** ve **etki alanı kayıt Kurulum** bölümler her etki alanı için.</span><span class="sxs-lookup"><span data-stu-id="674ed-187">To add another domain you will need to execute the **Verify your domain** and **Setup the domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="674ed-188">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="674ed-188">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="674ed-189">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="674ed-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="674ed-190">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="674ed-190">What's changed</span></span>
* <span data-ttu-id="674ed-191">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="674ed-191">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


