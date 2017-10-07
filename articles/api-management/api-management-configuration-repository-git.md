---
title: aaaConfigure Git - Azure kullanarak, API Management hizmetiniz | Microsoft Docs
description: "Bilgi nasıl toosave ve Git kullanarak API Management hizmeti yapılandırmanızı yapılandırın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a><span data-ttu-id="343f5-103">Nasıl toosave ve Git kullanarak API Management hizmeti yapılandırmanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="343f5-103">How toosave and configure your API Management service configuration using Git</span></span>
> 
> 

<span data-ttu-id="343f5-104">Her API Management hizmeti örneği hello yapılandırması ve hello hizmet örneği için meta veriler hakkında bilgi içeren bir yapılandırma veritabanı tutar.</span><span class="sxs-lookup"><span data-stu-id="343f5-104">Each API Management service instance maintains a configuration database that contains information about hello configuration and metadata for hello service instance.</span></span> <span data-ttu-id="343f5-105">Değişiklikleri toohello hizmet örneği hello yayımcı Portalı'ndaki bir ayarı değiştirmek, bir PowerShell cmdlet'ini kullanarak veya bir REST API çağrısı yapma yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="343f5-105">Changes can be made toohello service instance by changing a setting in hello publisher portal, using a PowerShell cmdlet, or making a REST API call.</span></span> <span data-ttu-id="343f5-106">Ayrıca toothese yöntemleri, Git kullanarak, hizmet yönetim senaryoları gibi etkinleştirme, hizmet örneği yapılandırması da yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="343f5-106">In addition toothese methods, you can also manage your service instance configuration using Git, enabling service management scenarios such as:</span></span>

* <span data-ttu-id="343f5-107">Yapılandırma sürüm oluşturma - karşıdan yüklemek ve hizmetinizi farklı sürümlerini depolamak</span><span class="sxs-lookup"><span data-stu-id="343f5-107">Configuration versioning - download and store different versions of your service configuration</span></span>
* <span data-ttu-id="343f5-108">Yapılandırma değişiklikleri toplu - yerel depoda hizmetinizi toomultiple bölümlerini değişiklik ve hello değişiklikleri geri toohello sunucusunu tek bir işlem ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="343f5-108">Bulk configuration changes - make changes toomultiple parts of your service configuration in your local repository and integrate hello changes back toohello server with a single operation</span></span>
* <span data-ttu-id="343f5-109">Tanıdık Git araç zinciri ve iş akışı - hello Git araçları ve zaten aşina iş akışlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="343f5-109">Familiar Git toolchain and workflow - use hello Git tooling and workflows that you are already familiar with</span></span>

<span data-ttu-id="343f5-110">Diyagram aşağıdaki hello hello farklı şekillerde tooconfigure genel bir bakış API Management hizmet örneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="343f5-110">hello following diagram shows an overview of hello different ways tooconfigure your API Management service instance.</span></span>

![Git yapılandırın][api-management-git-configure]

<span data-ttu-id="343f5-112">Merhaba yayımcı portalı, PowerShell cmdlet'leri veya hello REST API kullanarak tooyour hizmeti bir değişiklik yaptığınızda hello kullanarak hizmet yapılandırma veritabanınızı yönettiğiniz `https://{name}.management.azure-api.net` hello sağ tarafında hello diyagramda gösterildiği gibi endpoint.</span><span class="sxs-lookup"><span data-stu-id="343f5-112">When you make changes tooyour service using hello publisher portal, PowerShell cmdlets, or hello REST API, you are managing your service configuration database using hello `https://{name}.management.azure-api.net` endpoint, as shown on hello right side of hello diagram.</span></span> <span data-ttu-id="343f5-113">Merhaba diyagramı sol tarafındaki Hello gösterilmektedir hizmeti yapılandırmanızı Git kullanarak nasıl yönetebileceğinizi ve hizmetiniz için Git deposu bulunan `https://{name}.scm.azure-api.net`.</span><span class="sxs-lookup"><span data-stu-id="343f5-113">hello left side of hello diagram illustrates how you can manage your service configuration using Git and Git repository for your service located at `https://{name}.scm.azure-api.net`.</span></span>

<span data-ttu-id="343f5-114">Aşağıdaki adımları hello Git kullanarak, API Management hizmet örneğinizin yönetimine genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="343f5-114">hello following steps provide an overview of managing your API Management service instance using Git.</span></span>

1. <span data-ttu-id="343f5-115">Hizmet erişim Git yapılandırması</span><span class="sxs-lookup"><span data-stu-id="343f5-115">Access Git configuration in your service</span></span>
2. <span data-ttu-id="343f5-116">Hizmet yapılandırma veritabanı tooyour Git deponuza Kaydet</span><span class="sxs-lookup"><span data-stu-id="343f5-116">Save your service configuration database tooyour Git repository</span></span>
3. <span data-ttu-id="343f5-117">Merhaba Git deposuna tooyour yerel makineyi kopyalama</span><span class="sxs-lookup"><span data-stu-id="343f5-117">Clone hello Git repo tooyour local machine</span></span>
4. <span data-ttu-id="343f5-118">Merhaba son depodaki tooyour yerel makinede aşağı ve tamamlama ve anında iletme değişiklikleri geri tooyour depodaki isteme</span><span class="sxs-lookup"><span data-stu-id="343f5-118">Pull hello latest repo down tooyour local machine, and commit and push changes back tooyour repo</span></span>
5. <span data-ttu-id="343f5-119">Hizmet yapılandırma veritabanınıza, depodaki Hello değişikliklerden dağıtma</span><span class="sxs-lookup"><span data-stu-id="343f5-119">Deploy hello changes from your repo into your service configuration database</span></span>

<span data-ttu-id="343f5-120">Bu makalede nasıl tooenable ve Git toomanage hizmetinizi kullanabilir ve hello dosya ve klasörleri hello Git deposu için bir başvuru sağlar.</span><span class="sxs-lookup"><span data-stu-id="343f5-120">This article describes how tooenable and use Git toomanage your service configuration and provides a reference for hello files and folders in hello Git repository.</span></span>

## <a name="access-git-configuration-in-your-service"></a><span data-ttu-id="343f5-121">Hizmet erişim Git yapılandırması</span><span class="sxs-lookup"><span data-stu-id="343f5-121">Access Git configuration in your service</span></span>
<span data-ttu-id="343f5-122">Merhaba sağ üst köşesinde hello yayımcı portalına hello Git simge görüntüleyerek hızla Git yapılandırmanızı hello durumunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="343f5-122">You can quickly view hello status of your Git configuration by viewing hello Git icon in hello upper-right corner of hello publisher portal.</span></span> <span data-ttu-id="343f5-123">Bu örnekte, kaydedilmemiş değişiklikler toohello depo olduğunu hello durum iletisi gösterir.</span><span class="sxs-lookup"><span data-stu-id="343f5-123">In this example, hello status message indicates that there are unsaved changes toohello repository.</span></span> <span data-ttu-id="343f5-124">Merhaba API Management hizmeti yapılandırma veritabanına toohello deposu henüz kaydedilmedi olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="343f5-124">This is because hello API Management service configuration database has not yet been saved toohello repository.</span></span>

![Git durumu][api-management-git-icon-enable]

<span data-ttu-id="343f5-126">tooview ve Git yapılandırma ayarlarını yapılandırma, hello Git simgesine tıklayın veya hello tıklatın **güvenlik** menü toohello giderek **yapılandırma deposu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="343f5-126">tooview and configure your Git configuration settings, you can either click hello Git icon, or click hello **Security** menu and navigate toohello **Configuration repository** tab.</span></span>

![GIT etkinleştir][api-management-enable-git]

> [!IMPORTANT]
> <span data-ttu-id="343f5-128">Özellikleri hello deposunda saklanır ve onun geçmişinde dek kalacak şekilde, tanımlı değil tüm gizli devre dışı bırakın ve Git erişim yeniden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="343f5-128">Any secrets that are not defined as properties will be stored in hello repository and will remain in its history until you disable and re-enable Git access.</span></span> <span data-ttu-id="343f5-129">Özellikler sağlayan güvenli bir yerde toomanage toostore aktarıp gizli tüm API yapılandırması ve ilkeleri de dahil olmak üzere sabit dize değerleri, doğrudan ilke deyimleri bunları.</span><span class="sxs-lookup"><span data-stu-id="343f5-129">Properties provide a secure place toomanage constant string values, including secrets, across all API configuration and policies, so you don't have toostore them directly in your policy statements.</span></span> <span data-ttu-id="343f5-130">Daha fazla bilgi için bkz: [nasıl Azure API yönetimi ilkelerini toouse özelliklerinde](api-management-howto-properties.md).</span><span class="sxs-lookup"><span data-stu-id="343f5-130">For more information, see [How toouse properties in Azure API Management policies](api-management-howto-properties.md).</span></span>
> 
> 

<span data-ttu-id="343f5-131">Etkinleştirme veya hello REST API kullanarak Git erişimini devre dışı bırakma hakkında daha fazla bilgi için bkz: [etkinleştirmek veya devre dışı hello REST API kullanarak Git erişim](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span><span class="sxs-lookup"><span data-stu-id="343f5-131">For information on enabling or disabling Git access using hello REST API, see [Enable or disable Git access using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).</span></span>

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a><span data-ttu-id="343f5-132">toosave hello hizmet yapılandırma toohello Git deposu</span><span class="sxs-lookup"><span data-stu-id="343f5-132">toosave hello service configuration toohello Git repository</span></span>
<span data-ttu-id="343f5-133">Merhaba depo kopyalama önce hello ilk toosave hello geçerli durumunu hello hizmeti yapılandırma toohello havuzu adımdır.</span><span class="sxs-lookup"><span data-stu-id="343f5-133">hello first step before cloning hello repository is toosave hello current state of hello service configuration toohello repository.</span></span> <span data-ttu-id="343f5-134">Tıklatın **yapılandırma toorepository kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="343f5-134">Click **Save configuration toorepository**.</span></span>

![Yapılandırmayı kaydedin][api-management-save-configuration]

<span data-ttu-id="343f5-136">Merhaba onay ekranda istediğiniz değişiklikleri yapın ve tıklatın **Tamam** toosave.</span><span class="sxs-lookup"><span data-stu-id="343f5-136">Make any desired changes on hello confirmation screen and click **Ok** toosave.</span></span>

![Yapılandırmayı kaydedin][api-management-save-configuration-confirm]

<span data-ttu-id="343f5-138">Birkaç dakika sonra hello yapılandırma kaydedilir ve başlangıç tarihi ve saati hello son yapılandırma değişikliği ve hello hizmet yapılandırmasını ve hello arasındaki hello son eşitleme dahil olmak üzere hello yapılandırma durumu hello havuzun görüntülenir Depo.</span><span class="sxs-lookup"><span data-stu-id="343f5-138">After a few moments hello configuration is saved, and hello configuration status of hello repository is displayed, including hello date and time of hello last configuration change and hello last synchronization between hello service configuration and hello repository.</span></span>

![Yapılandırma durumu][api-management-configuration-status]

<span data-ttu-id="343f5-140">Merhaba yapılandırma toohello depo kaydedildikten sonra kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="343f5-140">Once hello configuration is saved toohello repository, it can be cloned.</span></span>

<span data-ttu-id="343f5-141">Merhaba REST API'sini kullanarak bu işlemi gerçekleştirme hakkında daha fazla bilgi için bkz: [hello REST API kullanarak anlık görüntü yürütme yapılandırma](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span><span class="sxs-lookup"><span data-stu-id="343f5-141">For information on performing this operation using hello REST API, see [Commit configuration snapshot using hello REST API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).</span></span>

## <a name="tooclone-hello-repository-tooyour-local-machine"></a><span data-ttu-id="343f5-142">tooclone hello depo tooyour yerel makine</span><span class="sxs-lookup"><span data-stu-id="343f5-142">tooclone hello repository tooyour local machine</span></span>
<span data-ttu-id="343f5-143">bir depo tooclone hello URL tooyour deposu, bir kullanıcı adı ve parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="343f5-143">tooclone a repository, you need hello URL tooyour repository, a user name, and a password.</span></span> <span data-ttu-id="343f5-144">Merhaba kullanıcı adı ve URL hello hello yukarıya yakın görüntülenir **yapılandırma deposu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="343f5-144">hello user name and URL are displayed near hello top of hello **Configuration repository** tab.</span></span>

![Git kopyalama][api-management-configuration-git-clone]

<span data-ttu-id="343f5-146">Merhaba hello altındaki oluşturulan Hello parola **yapılandırma deposu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="343f5-146">hello password is generated at hello bottom of hello **Configuration repository** tab.</span></span>

![Parola oluştur][api-management-generate-password]

<span data-ttu-id="343f5-148">toogenerate bir parola önce o hello emin **süre sonu** sona erme tarihi ve saati istenen toohello ayarlayın ve ardından **belirteç Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="343f5-148">toogenerate a password, first ensure that hello **Expiry** is set toohello desired expiration date and time, and then click **Generate Token**.</span></span>

![Parola][api-management-password]

> [!IMPORTANT]
> <span data-ttu-id="343f5-150">Bu parolayı not edin.</span><span class="sxs-lookup"><span data-stu-id="343f5-150">Make a note of this password.</span></span> <span data-ttu-id="343f5-151">Çıktıktan sonra bu sayfayı hello parolayı yeniden görüntülenmeyecek.</span><span class="sxs-lookup"><span data-stu-id="343f5-151">Once you leave this page hello password will not be displayed again.</span></span>
> 
> 

<span data-ttu-id="343f5-152">Örnek Kullanım hello Git Bash hello aracı [Windows için Git](http://www.git-scm.com/downloads) ancak bilginiz herhangi bir Git aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="343f5-152">hello following examples use hello Git Bash tool from [Git for Windows](http://www.git-scm.com/downloads) but you can use any Git tool that you are familiar with.</span></span>

<span data-ttu-id="343f5-153">Git aracınızı hello istenen klasöründe açın ve aşağıdaki komutu tooclone hello git deposu tooyour yerel makine, hello yayımcı portalı tarafından sağlanan hello komutunu kullanarak hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="343f5-153">Open your Git tool in hello desired folder and run hello following command tooclone hello git repository tooyour local machine, using hello command provided by hello publisher portal.</span></span>

```
git clone https://bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="343f5-154">Merhaba kullanıcı adı ve istendiğinde parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="343f5-154">Provide hello user name and password when prompted.</span></span>

<span data-ttu-id="343f5-155">Herhangi bir hata alırsanız, değiştirmeyi deneyin, `git clone` komut tooinclude hello kullanıcı adı ve parola, hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="343f5-155">If you receive any errors, try modifying your `git clone` command tooinclude hello user name and password, as shown in hello following example.</span></span>

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="343f5-156">Bu bir hata sağlıyorsa, URL hello komutu hello parola bölümü kodlama deneyin.</span><span class="sxs-lookup"><span data-stu-id="343f5-156">If this provides an error, try URL encoding hello password portion of hello command.</span></span> <span data-ttu-id="343f5-157">Bir hızlı yol toodo bu tooopen Visual Studio ve sorunu hello şu komutu hello **komut penceresi**.</span><span class="sxs-lookup"><span data-stu-id="343f5-157">One quick way toodo this is tooopen Visual Studio, and issue hello following command in hello **Immediate Window**.</span></span> <span data-ttu-id="343f5-158">tooopen hello **komut penceresi**, herhangi bir çözüm veya proje Visual Studio'da açın (veya yeni bir boş konsol uygulaması oluşturun) ve seçin **Windows**, **hemen** gelen Merhaba **hata ayıklama** menüsü.</span><span class="sxs-lookup"><span data-stu-id="343f5-158">tooopen hello **Immediate Window**, open any solution or project in Visual Studio (or create a new empty console application), and choose **Windows**, **Immediate** from hello **Debug** menu.</span></span>

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

<span data-ttu-id="343f5-159">Kodlanmış hello parola, kullanıcı adını ve depo konumu tooconstruct hello git komutu ile birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="343f5-159">Use hello encoded password along with your user name and repository location tooconstruct hello git command.</span></span>

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

<span data-ttu-id="343f5-160">Merhaba deposu kopyalanması sonra görüntülemek ve, yerel dosya sistemi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="343f5-160">Once hello repository is cloned you can view and work with it in your local file system.</span></span> <span data-ttu-id="343f5-161">Daha fazla bilgi için bkz: [dosya ve klasör yapısı yerel Git deposu başvuru](#file-and-folder-structure-reference-of-local-git-repository).</span><span class="sxs-lookup"><span data-stu-id="343f5-161">For more information, see [File and folder structure reference of local Git repository](#file-and-folder-structure-reference-of-local-git-repository).</span></span>

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a><span data-ttu-id="343f5-162">tooupdate yerel deponuza yapılandırmasıyla hello en güncel hizmet örneği</span><span class="sxs-lookup"><span data-stu-id="343f5-162">tooupdate your local repository with hello most current service instance configuration</span></span>
<span data-ttu-id="343f5-163">Merhaba yayımcı portalı veya hello REST API kullanarak değişiklikleri tooyour API Management hizmet örneği yaparsanız, yerel deponuza hello en son değişikliklerle güncelleştirmek için önce bu değişiklikleri toohello depo kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="343f5-163">If you make changes tooyour API Management service instance in hello publisher portal or using hello REST API, you must save these changes toohello repository before you can update your local repository with hello latest changes.</span></span> <span data-ttu-id="343f5-164">toodo bunu, **yapılandırma toorepository kaydetmek** hello üzerinde **yapılandırma deposu** sekmesinde hello yayımcı Portalı'nda ve yerel deponuza komutunda aşağıdaki hello sorun.</span><span class="sxs-lookup"><span data-stu-id="343f5-164">toodo this, click **Save configuration toorepository** on hello **Configuration repository** tab in hello publisher portal, and then issue hello following command in your local repository.</span></span>

```
git pull
```

<span data-ttu-id="343f5-165">Çalıştırmadan önce `git pull` için yerel deponuza hello klasörde olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="343f5-165">Before running `git pull` ensure that you are in hello folder for your local repository.</span></span> <span data-ttu-id="343f5-166">Merhaba yalnızca tamamladıysanız `git clone` hello aşağıdaki gibi bir komutu çalıştırarak hello dizin tooyour depodaki değiştirmeli sonra komutu.</span><span class="sxs-lookup"><span data-stu-id="343f5-166">If you have just completed hello `git clone` command, then you must change hello directory tooyour repo by running a command like hello following.</span></span>

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a><span data-ttu-id="343f5-167">Yerel Depodaki toohello sunucu depodaki toopush değişiklikler</span><span class="sxs-lookup"><span data-stu-id="343f5-167">toopush changes from your local repo toohello server repo</span></span>
<span data-ttu-id="343f5-168">Yerel deposu toohello sunucu depodan toopush değiştirir, yaptığınız değişiklikleri kaydetmek ve bunları toohello sunucu deposu gönderme gerekir.</span><span class="sxs-lookup"><span data-stu-id="343f5-168">toopush changes from your local repository toohello server repository, you must commit your changes and then push them toohello server repository.</span></span> <span data-ttu-id="343f5-169">toocommit yaptığınız değişiklikler, Git komut aracı, anahtar toohello dizinin yerel deposu ve aşağıdaki komutları sorunu hello açın.</span><span class="sxs-lookup"><span data-stu-id="343f5-169">toocommit your changes, open your Git command tool, switch toohello directory of your local repository, and issue hello following commands.</span></span>

```
git add --all
git commit -m "Description of your changes"
```

<span data-ttu-id="343f5-170">Tüm hello tamamlar çalıştırmak toohello sunucu toopush hello komutu.</span><span class="sxs-lookup"><span data-stu-id="343f5-170">toopush all of hello commits toohello server, run hello following command.</span></span>

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a><span data-ttu-id="343f5-171">toodeploy tüm hizmet yapılandırma değişiklikleri toohello API Management hizmeti örneği</span><span class="sxs-lookup"><span data-stu-id="343f5-171">toodeploy any service configuration changes toohello API Management service instance</span></span>
<span data-ttu-id="343f5-172">Kabul edilen ve basılmış toohello sunucu deposu yerel değişikliklerinizi olduktan sonra bunları tooyour API Management hizmet örneği dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="343f5-172">Once your local changes are committed and pushed toohello server repository, you can deploy them tooyour API Management service instance.</span></span>

![Dağıtma][api-management-configuration-deploy]

<span data-ttu-id="343f5-174">Merhaba REST API'sini kullanarak bu işlemi gerçekleştirme hakkında daha fazla bilgi için bkz: [dağıtmak Git değişiklikleri hello REST API kullanarak tooconfiguration veritabanı](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span><span class="sxs-lookup"><span data-stu-id="343f5-174">For information on performing this operation using hello REST API, see [Deploy Git changes tooconfiguration database using hello REST API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).</span></span>

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a><span data-ttu-id="343f5-175">Yerel Git deposu dosya ve klasör yapısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="343f5-175">File and folder structure reference of local Git repository</span></span>
<span data-ttu-id="343f5-176">Merhaba hello yerel git deposu bulunan dosya ve klasörleri hello hizmet örneği hakkında hello yapılandırma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-176">hello files and folders in hello local git repository contain hello configuration information about hello service instance.</span></span>

| <span data-ttu-id="343f5-177">Öğe</span><span class="sxs-lookup"><span data-stu-id="343f5-177">Item</span></span> | <span data-ttu-id="343f5-178">Açıklama</span><span class="sxs-lookup"><span data-stu-id="343f5-178">Description</span></span> |
| --- | --- |
| <span data-ttu-id="343f5-179">Kök API management klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-179">root api-management folder</span></span> |<span data-ttu-id="343f5-180">Merhaba hizmet örneği için en üst düzey yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-180">Contains top-level configuration for hello service instance</span></span> |
| <span data-ttu-id="343f5-181">API klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-181">apis folder</span></span> |<span data-ttu-id="343f5-182">Merhaba hizmet örneği içinde hello API'leri için Hello yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-182">Contains hello configuration for hello apis in hello service instance</span></span> |
| <span data-ttu-id="343f5-183">grupları klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-183">groups folder</span></span> |<span data-ttu-id="343f5-184">Merhaba hizmet örneği içinde hello grupları için Hello yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-184">Contains hello configuration for hello groups in hello service instance</span></span> |
| <span data-ttu-id="343f5-185">ilkeleri klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-185">policies folder</span></span> |<span data-ttu-id="343f5-186">Merhaba hizmet örneği içinde Hello ilkelerini içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-186">Contains hello policies in hello service instance</span></span> |
| <span data-ttu-id="343f5-187">portalStyles klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-187">portalStyles folder</span></span> |<span data-ttu-id="343f5-188">Merhaba hizmet örneği içinde hello Geliştirici Portalı özelleştirmeleri için Hello yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-188">Contains hello configuration for hello developer portal customizations in hello service instance</span></span> |
| <span data-ttu-id="343f5-189">Ürünler klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-189">products folder</span></span> |<span data-ttu-id="343f5-190">Merhaba hizmet örneği içinde hello ürünleri için Hello yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-190">Contains hello configuration for hello products in hello service instance</span></span> |
| <span data-ttu-id="343f5-191">Şablonlar klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-191">templates folder</span></span> |<span data-ttu-id="343f5-192">Merhaba hizmet örneği içinde hello e-posta şablonları için Hello yapılandırmayı içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-192">Contains hello configuration for hello email templates in hello service instance</span></span> |

<span data-ttu-id="343f5-193">Her klasör bir veya daha fazla içerebilir ve bazı durumlarda bir veya daha fazla klasör, örneğin her API, ürün veya grup için bir klasör durumda.</span><span class="sxs-lookup"><span data-stu-id="343f5-193">Each folder can contain one or more files, and in some cases one or more folders, for example a folder for each API, product, or group.</span></span> <span data-ttu-id="343f5-194">Her klasördeki Hello dosyalar hello klasör adı tarafından açıklanan hello varlık türü için özeldir.</span><span class="sxs-lookup"><span data-stu-id="343f5-194">hello files within each folder are specific for hello entity type described by hello folder name.</span></span>

| <span data-ttu-id="343f5-195">Dosya türü</span><span class="sxs-lookup"><span data-stu-id="343f5-195">File type</span></span> | <span data-ttu-id="343f5-196">Amaç</span><span class="sxs-lookup"><span data-stu-id="343f5-196">Purpose</span></span> |
| --- | --- |
| <span data-ttu-id="343f5-197">JSON</span><span class="sxs-lookup"><span data-stu-id="343f5-197">json</span></span> |<span data-ttu-id="343f5-198">Yapılandırma bilgilerini hello ilgili varlık hakkında</span><span class="sxs-lookup"><span data-stu-id="343f5-198">Configuration information about hello respective entity</span></span> |
| <span data-ttu-id="343f5-199">HTML</span><span class="sxs-lookup"><span data-stu-id="343f5-199">html</span></span> |<span data-ttu-id="343f5-200">Açıklamaları genellikle hello Geliştirici Portalı'nda görüntülenen hello varlık hakkında</span><span class="sxs-lookup"><span data-stu-id="343f5-200">Descriptions about hello entity, often displayed in hello developer portal</span></span> |
| <span data-ttu-id="343f5-201">xml</span><span class="sxs-lookup"><span data-stu-id="343f5-201">xml</span></span> |<span data-ttu-id="343f5-202">İlke deyimleri</span><span class="sxs-lookup"><span data-stu-id="343f5-202">Policy statements</span></span> |
| <span data-ttu-id="343f5-203">CSS</span><span class="sxs-lookup"><span data-stu-id="343f5-203">css</span></span> |<span data-ttu-id="343f5-204">Geliştirici Portalı özelleştirme için stil sayfaları</span><span class="sxs-lookup"><span data-stu-id="343f5-204">Style sheets for developer portal customization</span></span> |

<span data-ttu-id="343f5-205">Bu dosyalar oluşturulabilir, silinen, düzenlenemez ve yerel dosya sisteminde yönetilen ve hello değişiklikleri geri toohello API Management hizmet örneğinizin dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="343f5-205">These files can be created, deleted, edited, and managed on your local file system, and hello changes deployed back toohello your API Management service instance.</span></span>

> [!NOTE]
> <span data-ttu-id="343f5-206">Merhaba aşağıdaki varlıklar hello Git deposunda yer almayan ve Git kullanılarak yapılandırılamaz.</span><span class="sxs-lookup"><span data-stu-id="343f5-206">hello following entities are not contained in hello Git repository and cannot be configured using Git.</span></span>
> 
> * <span data-ttu-id="343f5-207">Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="343f5-207">Users</span></span>
> * <span data-ttu-id="343f5-208">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="343f5-208">Subscriptions</span></span>
> * <span data-ttu-id="343f5-209">Özellikler</span><span class="sxs-lookup"><span data-stu-id="343f5-209">Properties</span></span>
> * <span data-ttu-id="343f5-210">Geliştirici Portalı varlıkları stilleri dışında</span><span class="sxs-lookup"><span data-stu-id="343f5-210">Developer portal entities other than styles</span></span>
> 
> 

### <a name="root-api-management-folder"></a><span data-ttu-id="343f5-211">Kök API management klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-211">Root api-management folder</span></span>
<span data-ttu-id="343f5-212">Merhaba kök `api-management` klasörünü içeren bir `configuration.json` biçimini izleyen hello hello hizmet örneği hakkında üst düzey bilgileri içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="343f5-212">hello root `api-management` folder contains a `configuration.json` file that contains top-level information about hello service instance in hello following format.</span></span>

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

<span data-ttu-id="343f5-213">ilk dört ayarları hello (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, ve `UserRegistrationTermsConsentRequired`) üzerinde hello ayarları aşağıdaki toohello eşleme **kimlikleri** hello sekmesinde **güvenlik** bölümü.</span><span class="sxs-lookup"><span data-stu-id="343f5-213">hello first four settings (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, and `UserRegistrationTermsConsentRequired`) map toohello following settings on hello **Identities** tab in hello **Security** section.</span></span>

| <span data-ttu-id="343f5-214">Kimlik ayarı</span><span class="sxs-lookup"><span data-stu-id="343f5-214">Identity setting</span></span> | <span data-ttu-id="343f5-215">Çok eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="343f5-215">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="343f5-216">RegistrationEnabled</span><span class="sxs-lookup"><span data-stu-id="343f5-216">RegistrationEnabled</span></span> |<span data-ttu-id="343f5-217">**Anonim kullanıcılar toosign açma sayfasına yeniden yönlendir** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-217">**Redirect anonymous users toosign-in page** checkbox</span></span> |
| <span data-ttu-id="343f5-218">UserRegistrationTerms</span><span class="sxs-lookup"><span data-stu-id="343f5-218">UserRegistrationTerms</span></span> |<span data-ttu-id="343f5-219">**Kullanıcı Kaydolma kullanım koşullarını** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-219">**Terms of use on user signup** textbox</span></span> |
| <span data-ttu-id="343f5-220">UserRegistrationTermsEnabled</span><span class="sxs-lookup"><span data-stu-id="343f5-220">UserRegistrationTermsEnabled</span></span> |<span data-ttu-id="343f5-221">**Kullanım koşulları kaydolma sayfasında göster** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-221">**Show terms of use on signup page** checkbox</span></span> |
| <span data-ttu-id="343f5-222">UserRegistrationTermsConsentRequired</span><span class="sxs-lookup"><span data-stu-id="343f5-222">UserRegistrationTermsConsentRequired</span></span> |<span data-ttu-id="343f5-223">**Onay gerektiren** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-223">**Require consent** checkbox</span></span> |

![Kimlik ayarları][api-management-identity-settings]

<span data-ttu-id="343f5-225">Sonraki dört ayarları hello (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, ve `DelegationValidationKey`) üzerinde hello ayarları aşağıdaki toohello eşleme **temsilci** hello sekmesinde **güvenlik** bölümü.</span><span class="sxs-lookup"><span data-stu-id="343f5-225">hello next four settings (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, and `DelegationValidationKey`) map toohello following settings on hello **Delegation** tab in hello **Security** section.</span></span>

| <span data-ttu-id="343f5-226">Temsilci ayarı</span><span class="sxs-lookup"><span data-stu-id="343f5-226">Delegation setting</span></span> | <span data-ttu-id="343f5-227">Çok eşlemeleri</span><span class="sxs-lookup"><span data-stu-id="343f5-227">Maps too</span></span>|
| --- | --- |
| <span data-ttu-id="343f5-228">DelegationEnabled</span><span class="sxs-lookup"><span data-stu-id="343f5-228">DelegationEnabled</span></span> |<span data-ttu-id="343f5-229">**Oturum açma ve kaydolma temsilci** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-229">**Delegate sign-in & sign-up** checkbox</span></span> |
| <span data-ttu-id="343f5-230">DelegationUrl</span><span class="sxs-lookup"><span data-stu-id="343f5-230">DelegationUrl</span></span> |<span data-ttu-id="343f5-231">**Temsilci uç nokta URL'si** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-231">**Delegation endpoint URL** textbox</span></span> |
| <span data-ttu-id="343f5-232">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="343f5-232">DelegatedSubscriptionEnabled</span></span> |<span data-ttu-id="343f5-233">**Temsilci ürün aboneliği** onay kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-233">**Delegate product subscription** checkbox</span></span> |
| <span data-ttu-id="343f5-234">DelegationValidationKey</span><span class="sxs-lookup"><span data-stu-id="343f5-234">DelegationValidationKey</span></span> |<span data-ttu-id="343f5-235">**Doğrulama anahtarı temsilci** metin kutusu</span><span class="sxs-lookup"><span data-stu-id="343f5-235">**Delegate Validation Key** textbox</span></span> |

![Temsilci ayarları][api-management-delegation-settings]

<span data-ttu-id="343f5-237">Merhaba son ayar `$ref-policy`, toohello genel ilke deyimleri dosya hello hizmet örneği için eşler.</span><span class="sxs-lookup"><span data-stu-id="343f5-237">hello final setting, `$ref-policy`, maps toohello global policy statements file for hello service instance.</span></span>

### <a name="apis-folder"></a><span data-ttu-id="343f5-238">API klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-238">apis folder</span></span>
<span data-ttu-id="343f5-239">Merhaba `apis` klasörü aşağıdaki öğelerindeki hello içeren hello hizmet örneği içinde her API için bir klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-239">hello `apis` folder contains a folder for each API in hello service instance which contains hello following items.</span></span>

* <span data-ttu-id="343f5-240">`apis\<api name>\configuration.json`-Bu hello API için başlangıç yapılandırmasını ve hello arka uç hizmeti URL'si ve hello işlemleri hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-240">`apis\<api name>\configuration.json` - this is hello configuration for hello API and contains information about hello backend service URL and hello operations.</span></span> <span data-ttu-id="343f5-241">Merhaba budur toocall olsaydı döndürülür aynı bilgileri [belirli bir API alma](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) ile `export=true` içinde `application/json` biçimi.</span><span class="sxs-lookup"><span data-stu-id="343f5-241">This is hello same information that would be returned if you were toocall [Get a specific API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) with `export=true` in `application/json` format.</span></span>
* <span data-ttu-id="343f5-242">`apis\<api name>\api.description.html`-Bu hello API hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [API varlık](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="343f5-242">`apis\<api name>\api.description.html` - this is hello description of hello API and corresponds toohello `description` property of hello [API entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).</span></span>
* <span data-ttu-id="343f5-243">`apis\<api name>\operations\`-Bu klasörde `<operation name>.description.html` hello API toohello işlemlerinde eşleme dosyaları.</span><span class="sxs-lookup"><span data-stu-id="343f5-243">`apis\<api name>\operations\` - this folder contains `<operation name>.description.html` files that map toohello operations in hello API.</span></span> <span data-ttu-id="343f5-244">Her dosya hello toohello eşleştiren API tek bir işlemde hello açıklamasını içerir `description` hello özelliğinin [işlemi varlık](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) hello REST API de.</span><span class="sxs-lookup"><span data-stu-id="343f5-244">Each file contains hello description of a single operation in hello API which maps toohello `description` property of hello [operation entity](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in hello REST API.</span></span>

### <a name="groups-folder"></a><span data-ttu-id="343f5-245">grupları klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-245">groups folder</span></span>
<span data-ttu-id="343f5-246">Merhaba `groups` klasörü hello hizmet örneği içinde tanımlanan her grup için bir klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-246">hello `groups` folder contains a folder for each group defined in hello service instance.</span></span>

* <span data-ttu-id="343f5-247">`groups\<group name>\configuration.json`-Bu hello hello grubu için bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="343f5-247">`groups\<group name>\configuration.json` - this is hello configuration for hello group.</span></span> <span data-ttu-id="343f5-248">Merhaba budur toocall hello olsaydı döndürülür aynı bilgileri [belirli bir grup alma](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) işlemi.</span><span class="sxs-lookup"><span data-stu-id="343f5-248">This is hello same information that would be returned if you were toocall hello [Get a specific group](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) operation.</span></span>
* <span data-ttu-id="343f5-249">`groups\<group name>\description.html`-Bu hello grubunun hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [Grup varlık](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span><span class="sxs-lookup"><span data-stu-id="343f5-249">`groups\<group name>\description.html` - this is hello description of hello group and corresponds toohello `description` property of hello [group entity](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).</span></span>

### <a name="policies-folder"></a><span data-ttu-id="343f5-250">ilkeleri klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-250">policies folder</span></span>
<span data-ttu-id="343f5-251">Merhaba `policies` klasörü hizmet örneğiniz hello İlkesi ifadeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-251">hello `policies` folder contains hello policy statements for your service instance.</span></span>

* <span data-ttu-id="343f5-252">`policies\global.xml`-Hizmet Örneğiniz için genel kapsamda tanımlanan ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-252">`policies\global.xml` - contains policies defined at global scope for your service instance.</span></span>
* <span data-ttu-id="343f5-253">`policies\apis\<api name>\`-API kapsamda tanımlanan tüm ilkeler varsa, bu klasörde yer alır.</span><span class="sxs-lookup"><span data-stu-id="343f5-253">`policies\apis\<api name>\` - if you have any policies defined at API scope, they are contained in this folder.</span></span>
* <span data-ttu-id="343f5-254">`policies\apis\<api name>\<operation name>\`Klasör - işlemi kapsamında tanımlı tüm ilkeler varsa, bu klasörde yer alır `<operation name>.xml` toohello ilke deyimleri her işlem için eşleme dosyaları.</span><span class="sxs-lookup"><span data-stu-id="343f5-254">`policies\apis\<api name>\<operation name>\` folder - if you have any policies defined at operation scope, they are contained in this folder in `<operation name>.xml` files that map toohello policy statements for each operation.</span></span>
* <span data-ttu-id="343f5-255">`policies\products\`-Ürün kapsamda tanımlanan tüm ilkeler varsa, bunlar içeren bu klasörde yer alan `<product name>.xml` toohello ilke deyimleri her ürün için eşleme dosyaları.</span><span class="sxs-lookup"><span data-stu-id="343f5-255">`policies\products\` - if you have any policies defined at product scope, they are contained in this folder, which contains `<product name>.xml` files that map toohello policy statements for each product.</span></span>

### <a name="portalstyles-folder"></a><span data-ttu-id="343f5-256">portalStyles klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-256">portalStyles folder</span></span>
<span data-ttu-id="343f5-257">Merhaba `portalStyles` klasörü, Geliştirici Portalı özelleştirmeler hello hizmet örneği için yapılandırma ve stil sayfalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-257">hello `portalStyles` folder contains configuration and style sheets for developer portal customizations for hello service instance.</span></span>

* <span data-ttu-id="343f5-258">`portalStyles\configuration.json`-hello Geliştirici Portalı tarafından kullanılan hello stil sayfaları hello adlarını içerir</span><span class="sxs-lookup"><span data-stu-id="343f5-258">`portalStyles\configuration.json` - contains hello names of hello style sheets used by hello developer portal</span></span>
* <span data-ttu-id="343f5-259">`portalStyles\<style name>.css`-Her `<style name>.css` dosyasını içeren hello Geliştirici Portalı için stiller (`Preview.css` ve `Production.css` varsayılan olarak).</span><span class="sxs-lookup"><span data-stu-id="343f5-259">`portalStyles\<style name>.css` - each `<style name>.css` file contains styles for hello developer portal (`Preview.css` and `Production.css` by default).</span></span>

### <a name="products-folder"></a><span data-ttu-id="343f5-260">Ürünler klasörü</span><span class="sxs-lookup"><span data-stu-id="343f5-260">products folder</span></span>
<span data-ttu-id="343f5-261">Merhaba `products` klasörü hello hizmet örneği içinde tanımlanan her ürün için bir klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="343f5-261">hello `products` folder contains a folder for each product defined in hello service instance.</span></span>

* <span data-ttu-id="343f5-262">`products\<product name>\configuration.json`-Bu hello hello ürünü için bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="343f5-262">`products\<product name>\configuration.json` - this is hello configuration for hello product.</span></span> <span data-ttu-id="343f5-263">Merhaba budur toocall hello olsaydı döndürülür aynı bilgileri [belirli bir ürün almak](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) işlemi.</span><span class="sxs-lookup"><span data-stu-id="343f5-263">This is hello same information that would be returned if you were toocall hello [Get a specific product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) operation.</span></span>
* <span data-ttu-id="343f5-264">`products\<product name>\product.description.html`-Bu hello ürününün hello açıklaması ve toohello karşılık gelen `description` hello özelliğinin [ürün varlığı](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) hello REST API de.</span><span class="sxs-lookup"><span data-stu-id="343f5-264">`products\<product name>\product.description.html` - this is hello description of hello product and corresponds toohello `description` property of hello [product entity](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in hello REST API.</span></span>

### <a name="templates"></a><span data-ttu-id="343f5-265">şablonları</span><span class="sxs-lookup"><span data-stu-id="343f5-265">templates</span></span>
<span data-ttu-id="343f5-266">Merhaba `templates` hello yapılandırmasını içeren klasör [şablonları e-posta](api-management-howto-configure-notifications.md) hello hizmet örneği.</span><span class="sxs-lookup"><span data-stu-id="343f5-266">hello `templates` folder contains configuration for hello [email templates](api-management-howto-configure-notifications.md) of hello service instance.</span></span>

* <span data-ttu-id="343f5-267">`<template name>\configuration.json`-Bu hello hello e-posta şablonu için bir yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="343f5-267">`<template name>\configuration.json` - this is hello configuration for hello email template.</span></span>
* <span data-ttu-id="343f5-268">`<template name>\body.html`-hello hello e-posta şablonunun gövdesini budur.</span><span class="sxs-lookup"><span data-stu-id="343f5-268">`<template name>\body.html` - this is hello body of hello email template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="343f5-269">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="343f5-269">Next steps</span></span>
<span data-ttu-id="343f5-270">Diğer yolları toomanage hakkında bilgi için hizmet örneği bakın:</span><span class="sxs-lookup"><span data-stu-id="343f5-270">For information on other ways toomanage your service instance, see:</span></span>

* <span data-ttu-id="343f5-271">Hizmet örneğinizi PowerShell cmdlet'lerini aşağıdaki hello kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="343f5-271">Manage your service instance using hello following PowerShell cmdlets</span></span>
  * [<span data-ttu-id="343f5-272">Hizmet dağıtımı PowerShell cmdlet başvurusu</span><span class="sxs-lookup"><span data-stu-id="343f5-272">Service deployment PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [<span data-ttu-id="343f5-273">Hizmet Yönetimi PowerShell cmdlet başvurusu</span><span class="sxs-lookup"><span data-stu-id="343f5-273">Service management PowerShell cmdlet reference</span></span>](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* <span data-ttu-id="343f5-274">Hizmet örneğinizi hello yayımcı portalında Yönet</span><span class="sxs-lookup"><span data-stu-id="343f5-274">Manage your service instance in hello publisher portal</span></span>
  * [<span data-ttu-id="343f5-275">İlk API'nizi yönetme</span><span class="sxs-lookup"><span data-stu-id="343f5-275">Manage your first API</span></span>](api-management-get-started.md)
* <span data-ttu-id="343f5-276">Hizmet örneğinizi Hello REST API kullanarak yönetme</span><span class="sxs-lookup"><span data-stu-id="343f5-276">Manage your service instance using hello REST API</span></span>
  * [<span data-ttu-id="343f5-277">API Management REST API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="343f5-277">API Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="343f5-278">Video genel izleyin</span><span class="sxs-lookup"><span data-stu-id="343f5-278">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png




