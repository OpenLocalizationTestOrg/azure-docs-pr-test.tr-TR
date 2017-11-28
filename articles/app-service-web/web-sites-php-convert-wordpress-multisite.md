---
title: Azure App Service'te WordPress tooMultisite aaaConvert
description: "Nasıl tootake var olan bir WordPress web uygulaması Azure hello Galerisi'nde aracılığıyla oluşturulan ve tooWordPress birden çok tesis Dönüştür öğrenin"
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
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a><span data-ttu-id="8223b-103">Azure App Service'te WordPress tooMultisite Dönüştür</span><span class="sxs-lookup"><span data-stu-id="8223b-103">Convert WordPress tooMultisite in Azure App Service</span></span>
## <a name="overview"></a><span data-ttu-id="8223b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="8223b-104">Overview</span></span>
<span data-ttu-id="8223b-105">*Tarafından [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies, Inc.][ms-open-tech]*</span><span class="sxs-lookup"><span data-stu-id="8223b-105">*By [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*</span></span>

<span data-ttu-id="8223b-106">Bu öğreticide, var olan bir WordPress web uygulaması tootake hello Galerisi'nde Azure ve WordPress birden çok tesis içine yüklemek dönüştürme aracılığıyla nasıl oluşturulacağını öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8223b-106">In this tutorial, you will learn how tootake an existing WordPress web app created through hello gallery in Azure and convert it into a WordPress Multisite install.</span></span> <span data-ttu-id="8223b-107">Ayrıca, nasıl tooassign Merhaba, özel etki alanı tooeach yüklemenizi içinde alt site öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8223b-107">Additionally, you will learn how tooassign a custom domain tooeach of hello subsites within your install.</span></span>

<span data-ttu-id="8223b-108">WordPress olan bir yüklemesini sahip varsayılır.</span><span class="sxs-lookup"><span data-stu-id="8223b-108">It is assumed that you have an existing installation of WordPress.</span></span> <span data-ttu-id="8223b-109">Bunu yapmazsanız, Lütfen sağlanan hello yönergeleri izleyin [azure'da hello Galeriden bir WordPress web sitesi oluşturmak][website-from-gallery].</span><span class="sxs-lookup"><span data-stu-id="8223b-109">If you do not, please follow hello guidance provided in [Create a WordPress web site from hello gallery in Azure][website-from-gallery].</span></span>

<span data-ttu-id="8223b-110">Varolan bir WordPress dönüştürme tek bir site yükleme tooMultisite genellikle oldukça basittir ve burada başlangıç adımları hello çoğunu düz hello gelen [A ağ oluştur] [ wordpress-codex-create-a-network] hello sayfasında[WordPress Codex](http://codex.wordpress.org).</span><span class="sxs-lookup"><span data-stu-id="8223b-110">Converting an existing WordPress single site install tooMultisite is generally fairly simple, and many of hello initial steps here come straight from hello [Create A Network][wordpress-codex-create-a-network] page on hello [WordPress Codex](http://codex.wordpress.org).</span></span>

<span data-ttu-id="8223b-111">Haydi başlayalım.</span><span class="sxs-lookup"><span data-stu-id="8223b-111">Let's get started.</span></span>

## <a name="allow-multisite"></a><span data-ttu-id="8223b-112">Birden çok tesis izin ver</span><span class="sxs-lookup"><span data-stu-id="8223b-112">Allow Multisite</span></span>
<span data-ttu-id="8223b-113">İlk tooenable birden çok tesis hello aracılığıyla ihtiyacınız `wp-config.php` hello dosyasıyla **WP\_izin\_birden çok TESİS** sabit.</span><span class="sxs-lookup"><span data-stu-id="8223b-113">You first need tooenable Multisite through hello `wp-config.php` file with hello **WP\_ALLOW\_MULTISITE** constant.</span></span> <span data-ttu-id="8223b-114">Web uygulama dosyalarınızı iki yöntem tooedit vardır: hello ilk olduğu FTP ve Git aracılığıyla ikinci hello aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="8223b-114">There are two methods tooedit your web app files: hello first is through FTP, and hello second through Git.</span></span> <span data-ttu-id="8223b-115">Konusunda bilginiz yoksa toosetup bu yöntemlerden birini başvurun öğreticileri aşağıdaki toohello:</span><span class="sxs-lookup"><span data-stu-id="8223b-115">If you are unfamiliar with how toosetup either of these methods, please refer toohello following tutorials:</span></span>

* <span data-ttu-id="8223b-116">[PHP web sitesiyle MySQL ve FTP][website-w-mysql-and-ftp-ftp-setup]</span><span class="sxs-lookup"><span data-stu-id="8223b-116">[PHP web site with MySQL and FTP][website-w-mysql-and-ftp-ftp-setup]</span></span>
* <span data-ttu-id="8223b-117">[PHP web sitesiyle MySQL ve Git][website-w-mysql-and-git-git-setup]</span><span class="sxs-lookup"><span data-stu-id="8223b-117">[PHP web site with MySQL and Git][website-w-mysql-and-git-git-setup]</span></span>

<span data-ttu-id="8223b-118">Açık hello `wp-config.php` dosya seçtiğiniz hello düzenleyicisiyle ve hello yukarıda hello aşağıdakileri ekleyin `/* That's all, stop editing! Happy blogging. */` satır.</span><span class="sxs-lookup"><span data-stu-id="8223b-118">Open hello `wp-config.php` file with hello editor of your choosing and add hello following above hello `/* That's all, stop editing! Happy blogging. */` line.</span></span>

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

<span data-ttu-id="8223b-119">Emin toosave hello dosyası olması ve geri toohello sunucu karşıya!</span><span class="sxs-lookup"><span data-stu-id="8223b-119">Be sure toosave hello file and upload it back toohello server!</span></span>

## <a name="network-setup"></a><span data-ttu-id="8223b-120">Ağ Kurulumu</span><span class="sxs-lookup"><span data-stu-id="8223b-120">Network Setup</span></span>
<span data-ttu-id="8223b-121">İçinde toohello oturum *wp-yönetici* web uygulamanız ve alan hello altında yeni bir öğe görmeniz gerekir **Araçları** adlı menüsü **ağ kurulumu**.</span><span class="sxs-lookup"><span data-stu-id="8223b-121">Log in toohello *wp-admin* area of your web app and you should see a new item under hello **Tools** menu called **Network Setup**.</span></span> <span data-ttu-id="8223b-122">Tıklatın **ağ kurulumu** ve ağınızın hello ayrıntıları doldurun.</span><span class="sxs-lookup"><span data-stu-id="8223b-122">Click **Network Setup** and fill in hello details of your network.</span></span>

![Ağ Kurulum Ekranı][wordpress-network-setup]

<span data-ttu-id="8223b-124">Bu öğretici hello kullanır *alt dizinleri* çünkü her zaman çalışması gerekir ve size özel etki alanları her alt site için daha sonra hello öğreticide ayarlarını yapacak şema site.</span><span class="sxs-lookup"><span data-stu-id="8223b-124">This tutorial uses hello *Sub-directories* site schema because it should always work, and we will be setting up custom domains for each subsite later in hello tutorial.</span></span> <span data-ttu-id="8223b-125">Ancak, bir alt etki alanı yüklemek hello üzerinden bir etki alanına eşlerseniz olası toosetup olmalıdır [Azure Portal](https://portal.azure.com) ve joker DNS düzgün şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8223b-125">However, it should be possible toosetup a subdomain install if you map a domain through hello [Azure Portal](https://portal.azure.com) and setup wildcard DNS properly.</span></span>

<span data-ttu-id="8223b-126">Alt etki alanı vs hakkında daha fazla bilgi için alt dizin kurulumları hello bkz [çok siteli ağ türlerini] [ wordpress-codex-types-of-networks] makale hello WordPress Codex üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8223b-126">For more information on sub-domain vs sub-directory setups see hello [Types of multisite network][wordpress-codex-types-of-networks] article on hello WordPress Codex.</span></span>

## <a name="enable-hello-network"></a><span data-ttu-id="8223b-127">Merhaba ağ etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8223b-127">Enable hello Network</span></span>
<span data-ttu-id="8223b-128">Merhaba ağ hello veritabanında yapılandırılmıştır, ancak bir kalan adım tooenable hello ağ işlevi yoktur.</span><span class="sxs-lookup"><span data-stu-id="8223b-128">hello network is now configured in hello database, but there is one remaining step tooenable hello network functionality.</span></span> <span data-ttu-id="8223b-129">Merhaba Sonlandır `wp-config.php` ayarları ve olun `web.config` her site düzgün bir şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="8223b-129">Finalize hello `wp-config.php` settings and ensure `web.config` properly routes each site.</span></span>

<span data-ttu-id="8223b-130">Merhaba tıkladıktan sonra **yükleme** hello düğmesinde *ağ kurulumu* sayfasında, WordPress tooupdate hello deneyecek `wp-config.php` ve `web.config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="8223b-130">After clicking hello **Install** button on hello *Network Setup* page, WordPress will attempt tooupdate hello `wp-config.php` and `web.config` files.</span></span> <span data-ttu-id="8223b-131">Ancak, hello dosyaları tooensure hello güncelleştirmeleri başarılı her zaman kontrol etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8223b-131">However, you should always check hello files tooensure hello updates were successful.</span></span> <span data-ttu-id="8223b-132">Aksi durumda, bu ekranı hello gerekli güncelleştirmeleri sunacaktır.</span><span class="sxs-lookup"><span data-stu-id="8223b-132">If not, this screen will present you with hello necessary updates.</span></span> <span data-ttu-id="8223b-133">Düzenle ve hello dosyalarını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8223b-133">Edit and save hello files.</span></span>

<span data-ttu-id="8223b-134">Yaptıktan sonra bu güncelleştirmeleri toolog çıkışı ve günlük gerekir hello wp-yönetici panoya yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="8223b-134">After making these updates you will need toolog out and log back into hello wp-admin dashboard.</span></span>

<span data-ttu-id="8223b-135">Şimdi olmamalıdır ek bir menü etiketli hello yönetici çubuğunda **Sitelerim**.</span><span class="sxs-lookup"><span data-stu-id="8223b-135">There should now be an additional menu on hello admin bar labeled **My Sites**.</span></span> <span data-ttu-id="8223b-136">Bu menü toocontrol sağlayan yeni ağınızdan hello **ağ yönetim** Pano.</span><span class="sxs-lookup"><span data-stu-id="8223b-136">This menu allows you toocontrol your new network through hello **Network Admin** dashboard.</span></span>

## <a name="adding-custom-domains"></a><span data-ttu-id="8223b-137">Özel etki alanlarını ekleme</span><span class="sxs-lookup"><span data-stu-id="8223b-137">Adding custom domains</span></span>
<span data-ttu-id="8223b-138">Merhaba [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] eklentisi yapar kolay tooadd özel etki alanlarını tooany site ağınızda.</span><span class="sxs-lookup"><span data-stu-id="8223b-138">hello [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] plugin makes it a breeze tooadd custom domains tooany site in your network.</span></span> <span data-ttu-id="8223b-139">Merhaba eklentisi toooperate sırada düzgün toodo hello Portal ve ayrıca etki alanı kayıt şirketinizdeki bazı ek kurulum gerekir.</span><span class="sxs-lookup"><span data-stu-id="8223b-139">In order for hello plugin toooperate properly, you need toodo some additional setup on hello Portal, and also at your domain registrar.</span></span>

## <a name="enable-domain-mapping-toohello-web-app"></a><span data-ttu-id="8223b-140">Etki alanı eşleme toohello web uygulaması etkinleştir</span><span class="sxs-lookup"><span data-stu-id="8223b-140">Enable domain mapping toohello web app</span></span>
<span data-ttu-id="8223b-141">Merhaba **serbest** [uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714) plan modunda özel etki alanlarını tooWeb uygulamalar ekleme desteklemez.</span><span class="sxs-lookup"><span data-stu-id="8223b-141">hello **Free** [App Service](http://go.microsoft.com/fwlink/?LinkId=529714) plan mode does not support adding custom domains tooWeb Apps.</span></span> <span data-ttu-id="8223b-142">Tooswitch çok gerekir**paylaşılan** veya **standart** modu.</span><span class="sxs-lookup"><span data-stu-id="8223b-142">You will need tooswitch too**Shared** or **Standard** mode.</span></span> <span data-ttu-id="8223b-143">toodo bu:</span><span class="sxs-lookup"><span data-stu-id="8223b-143">toodo this:</span></span>

* <span data-ttu-id="8223b-144">Toohello Azure portalında oturum açın ve web uygulamanızı bulun.</span><span class="sxs-lookup"><span data-stu-id="8223b-144">Log in toohello Azure Portal and locate your web app.</span></span> 
* <span data-ttu-id="8223b-145">Tıklatın hello üzerinde **ölçeği** sekmesinde **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="8223b-145">Click on hello **Scale up** tab in **Settings**.</span></span>
* <span data-ttu-id="8223b-146">Altında **genel**, şunlardan birini seçin *paylaşılan* veya *standart*</span><span class="sxs-lookup"><span data-stu-id="8223b-146">Under **General**, select either *SHARED* or *STANDARD*</span></span>
* <span data-ttu-id="8223b-147">Tıklatın **Kaydet**</span><span class="sxs-lookup"><span data-stu-id="8223b-147">Click **Save**</span></span>

<span data-ttu-id="8223b-148">Tooverify hello değişiklik soran bir ileti alırsınız ve web uygulamanız şimdi kullanım bağlı olarak bir maliyet doğurur ve belirlediğiniz başka bir yapılandırma hello kabul.</span><span class="sxs-lookup"><span data-stu-id="8223b-148">You may receive a message asking you tooverify hello change and acknowledge your web app may now incur a cost, depending upon usage and hello other configuration you set.</span></span>

<span data-ttu-id="8223b-149">Tooprocess hello yeni ayarları, birkaç saniye sürer etki alanınızın iyi zaman toostart ayarlama böylece sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8223b-149">It takes a few seconds tooprocess hello new settings, so now is a good time toostart setting up your domain.</span></span>

## <a name="verify-your-domain"></a><span data-ttu-id="8223b-150">Etki alanınızı doğrulayın</span><span class="sxs-lookup"><span data-stu-id="8223b-150">Verify your domain</span></span>
<span data-ttu-id="8223b-151">Azure Web Apps toomap bir etki alanı toohello site sağlayacak. önce ilk hello yetkilendirme toomap hello etki alanınız olduğunu tooverify gerekir.</span><span class="sxs-lookup"><span data-stu-id="8223b-151">Before Azure Web Apps will allow you toomap a domain toohello site, you first need tooverify that you have hello authorization toomap hello domain.</span></span> <span data-ttu-id="8223b-152">toodo bu nedenle, yeni bir CNAME kaydı tooyour DNS girişi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8223b-152">toodo so, you must add a new CNAME record tooyour DNS entry.</span></span>

* <span data-ttu-id="8223b-153">Tooyour etki alanının DNS Yöneticisi'nde oturum</span><span class="sxs-lookup"><span data-stu-id="8223b-153">Log in tooyour domain's DNS manager</span></span>
* <span data-ttu-id="8223b-154">Yeni bir CNAME oluşturmanız *awverify*</span><span class="sxs-lookup"><span data-stu-id="8223b-154">Create a new CNAME *awverify*</span></span>
* <span data-ttu-id="8223b-155">Noktası *awverify* çok*awverify. YOUR_DOMAIN.azurewebsites.NET*</span><span class="sxs-lookup"><span data-stu-id="8223b-155">Point *awverify* too*awverify.YOUR_DOMAIN.azurewebsites.net*</span></span>

<span data-ttu-id="8223b-156">Bunu süre hello DNS değişiklikleri toogo için tam etkili, aşağıdaki adımları hello hemen çalışmazsa kahve, kupaya olun sonra geri dönün ve yeniden deneyin böylece gidin.</span><span class="sxs-lookup"><span data-stu-id="8223b-156">It may take some time for hello DNS changes toogo into full effect, so if hello following steps do not work immediately, go make a cup of coffee, then come back and try again.</span></span>

## <a name="add-hello-domain-toohello-web-app"></a><span data-ttu-id="8223b-157">Merhaba etki alanı toohello web uygulaması Ekle</span><span class="sxs-lookup"><span data-stu-id="8223b-157">Add hello domain toohello web app</span></span>
<span data-ttu-id="8223b-158">Dönüş tooyour web uygulaması'hello Azure Portal aracılığıyla tıklatın **ayarları**ve ardından **özel etki alanları ve SSL**.</span><span class="sxs-lookup"><span data-stu-id="8223b-158">Return tooyour web app through hello Azure Portal, click **Settings**, and then click **Custom domains and SSL**.</span></span>

<span data-ttu-id="8223b-159">Ne zaman hello *SSL ayarları* olan görüntülenir, burada girdiğiniz tooassign tooyour web uygulaması istediğiniz tüm hello etki alanlarının hello alanların görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8223b-159">When hello *SSL settings* are displayed, you will see hello fields where you will input all hello domains which you wish tooassign tooyour web app.</span></span> <span data-ttu-id="8223b-160">Bir etki alanı burada listelenmiyorsa, WordPress içinde nasıl hello etki alanı DNS kurulması bağımsız olarak eşleme için kullanılabilir olmaz.</span><span class="sxs-lookup"><span data-stu-id="8223b-160">If a domain is not listed here, it will not be available for mapping inside WordPress, regardless of how hello domain DNS is setup.</span></span>

![Özel etki alanlarını iletişim yönetme][wordpress-manage-domains]

<span data-ttu-id="8223b-162">Etki alanınızı hello metin kutusuna yazdıktan sonra Azure hello CNAME kaydı daha önce oluşturduğunuz doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8223b-162">After typing your domain into hello text box, Azure will verify hello CNAME record you created previously.</span></span> <span data-ttu-id="8223b-163">Merhaba DNS tam olarak yayılmadan değil varsa, kırmızı bir gösterge gösterir.</span><span class="sxs-lookup"><span data-stu-id="8223b-163">If hello DNS has not fully propagated, a red indicator will show.</span></span> <span data-ttu-id="8223b-164">Başarılı olduysa, yeşil bir onay işareti görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="8223b-164">If it was successful, you will see a green checkmark.</span></span> 

<span data-ttu-id="8223b-165">IP adresi hello iletişim hello alt kısmında listelenen hello not edin.</span><span class="sxs-lookup"><span data-stu-id="8223b-165">Take note of hello IP Address listed at hello bottom of hello dialog.</span></span> <span data-ttu-id="8223b-166">Bu toosetup hello kayıt etki alanınız için gerekir.</span><span class="sxs-lookup"><span data-stu-id="8223b-166">You will need this toosetup hello A record for your domain.</span></span>

## <a name="setup-hello-domain-a-record"></a><span data-ttu-id="8223b-167">Kurulum Hello etki alanı A kaydı</span><span class="sxs-lookup"><span data-stu-id="8223b-167">Setup hello domain A record</span></span>
<span data-ttu-id="8223b-168">Merhaba diğer adımlar başarılı olursa, DNS A kaydına hello etki alanı tooyour Azure web uygulaması şimdi atayabilir.</span><span class="sxs-lookup"><span data-stu-id="8223b-168">If hello other steps were successful, you may now assign hello domain tooyour Azure web app through a DNS A record.</span></span> 

<span data-ttu-id="8223b-169">Azure web uygulamaları CNAME ve A kayıtları ancak kabul etmiş önemli toonote burada olduğundan, *gerekir* bir A kaydı tooenable uygun etki alanı eşlemesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8223b-169">It is important toonote here that Azure web apps accept both CNAME and A records, however you *must* use an A record tooenable proper domain mapping.</span></span> <span data-ttu-id="8223b-170">CNAME tooanother CNAME, Azure sizin yerinize YOUR_DOMAIN.azurewebsites.net ile oluşturulan olduğu iletilemez.</span><span class="sxs-lookup"><span data-stu-id="8223b-170">A CNAME cannot be forwarded tooanother CNAME, which is what Azure created for you with YOUR_DOMAIN.azurewebsites.net.</span></span>

<span data-ttu-id="8223b-171">Başlangıç IP adresi hello önceki adımdaki kullanarak, tooyour DNS Yöneticisi'ni ve Kurulum hello kayıt toopoint toothat IP döndürür.</span><span class="sxs-lookup"><span data-stu-id="8223b-171">Using hello IP address from hello previous step, return tooyour DNS manager and setup hello A record toopoint toothat IP.</span></span>

## <a name="install-and-setup-hello-plugin"></a><span data-ttu-id="8223b-172">Yükleme ve Kurulum hello eklentisi</span><span class="sxs-lookup"><span data-stu-id="8223b-172">Install and setup hello plugin</span></span>
<span data-ttu-id="8223b-173">WordPress çoklu site şu anda bir yerleşik bir yöntem toomap özel etki alanlarına sahip değil.</span><span class="sxs-lookup"><span data-stu-id="8223b-173">WordPress Multisite currently does not have a built-in method toomap custom domains.</span></span> <span data-ttu-id="8223b-174">Ancak adlı bir eklenti yoktur [WordPress MU etki alanı eşleme] [ wordpress-plugin-wordpress-mu-domain-mapping] hello işlevsellik sizin için ekler.</span><span class="sxs-lookup"><span data-stu-id="8223b-174">However, there is a plugin called [WordPress MU Domain Mapping][wordpress-plugin-wordpress-mu-domain-mapping] that adds hello functionality for you.</span></span> <span data-ttu-id="8223b-175">Toohello Ağ Yönetim bölümünde, sitenizin günlüğüne bakın ve hello **WordPress MU etki alanı eşleme** eklentisi.</span><span class="sxs-lookup"><span data-stu-id="8223b-175">Log in toohello Network Admin portion of your site and install hello **WordPress MU Domain Mapping** plugin.</span></span>

<span data-ttu-id="8223b-176">Yükleme ve hello eklentisi etkinleştirme ziyaret sonra **ayarları** > **etki alanı eşleme** tooconfigure hello eklentisi.</span><span class="sxs-lookup"><span data-stu-id="8223b-176">After installing and activating hello plugin, visit **Settings** > **Domain Mapping** tooconfigure hello plugin.</span></span> <span data-ttu-id="8223b-177">Merhaba ilk metin kutusuna, *sunucusu IP adresi*, giriş hello toosetup kullanılan IP adresi hello hello etki alanı için bir kaydı.</span><span class="sxs-lookup"><span data-stu-id="8223b-177">In hello first textbox, *Server IP Address*, input hello IP Address you used toosetup hello A record for hello domain.</span></span> <span data-ttu-id="8223b-178">Herhangi ayarlayın *etki alanı seçenekleri* istediğiniz (Merhaba varsayılan değerler genellikle ince) tıklatıp **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8223b-178">Set any *Domain Options* you desire (hello defaults are often fine) and click **Save**.</span></span>

## <a name="map-hello-domain"></a><span data-ttu-id="8223b-179">Harita hello etki alanı</span><span class="sxs-lookup"><span data-stu-id="8223b-179">Map hello domain</span></span>
<span data-ttu-id="8223b-180">Merhaba ziyaret **Pano** hello site için toomap hello etki alanına istiyor.</span><span class="sxs-lookup"><span data-stu-id="8223b-180">Visit hello **Dashboard** for hello site you wish toomap hello domain to.</span></span> <span data-ttu-id="8223b-181">Tıklayın **Araçları** > **etki alanı eşleme** ve türü hello yeni etki alanına tıklayın ve hello textbox **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8223b-181">Click on **Tools** > **Domain Mapping** and type hello new domain into hello textbox and click **Add**.</span></span>

<span data-ttu-id="8223b-182">Varsayılan olarak, yeni bir etki alanı hello yeniden toohello otomatik olarak oluşturulur site, etki alanı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8223b-182">By default, hello new domain will be rewritten toohello autogenerated site domain.</span></span> <span data-ttu-id="8223b-183">Tüm gönderilen trafiğin toohello yeni etki alanı toohave istiyorsanız hello denetleyin *bu blog için birincil etki alanı* kutusunu kaydetmeden önce.</span><span class="sxs-lookup"><span data-stu-id="8223b-183">If you want toohave all traffic sent toohello new domain, check hello *Primary domain for this blog* box before saving.</span></span> <span data-ttu-id="8223b-184">Etki alanları tooa site sınırsız sayıda ekleyebilirsiniz, ancak yalnızca bir birincil olabilir.</span><span class="sxs-lookup"><span data-stu-id="8223b-184">You can add an unlimited number of domains tooa site, but  only one can be primary.</span></span>

## <a name="do-it-again"></a><span data-ttu-id="8223b-185">Yeniden yapın</span><span class="sxs-lookup"><span data-stu-id="8223b-185">Do it again</span></span>
<span data-ttu-id="8223b-186">Azure Web uygulamaları tooadd etki alanları tooa web uygulaması sınırsız sayıda olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8223b-186">Azure Web Apps allow you tooadd an unlimited number of domains tooa web app.</span></span> <span data-ttu-id="8223b-187">tooadd tooexecute hello gerekir başka bir etki alanı **etki alanınızı doğrulayın** ve **Kurulum hello etki alanı A kaydı** bölümler her etki alanı için.</span><span class="sxs-lookup"><span data-stu-id="8223b-187">tooadd another domain you will need tooexecute hello **Verify your domain** and **Setup hello domain A record** sections for each domain.</span></span>    

> [!NOTE]
> <span data-ttu-id="8223b-188">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8223b-188">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8223b-189">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="8223b-189">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="8223b-190">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="8223b-190">What's changed</span></span>
* <span data-ttu-id="8223b-191">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8223b-191">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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


