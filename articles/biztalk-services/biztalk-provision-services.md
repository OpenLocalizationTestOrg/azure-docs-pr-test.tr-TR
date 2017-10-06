---
title: hello Azure portal, Azure BizTalk Services aaaCreate | Microsoft Docs
description: "Bilgi nasıl tooprovision veya hello Azure portalı; Azure BizTalk Services oluşturma MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="d43de-103">Hello Azure portalını kullanarak BizTalk Services oluşturma</span><span class="sxs-lookup"><span data-stu-id="d43de-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="d43de-104">toosign toohello Azure portal'ın bir Azure hesabı ve Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="d43de-105">Hesabınız yoksa birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d43de-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="d43de-106">Bkz. [Azure Ücretsiz Deneme](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="d43de-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="d43de-107"><a name="CreateService"></a>BizTalk Hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="d43de-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="d43de-108">Seçtiğiniz sürüm Hello bağlı olarak, tüm BizTalk hizmeti ayarlarını bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="d43de-109">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d43de-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d43de-110">Merhaba alt Gezinti bölmesinde seçin **yeni**:</span><span class="sxs-lookup"><span data-stu-id="d43de-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="d43de-111">![Merhaba yeni düğmesini seçme][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="d43de-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="d43de-112">**UYGULAMA HİZMETLERİ** > **BIZTALK HİZMETİ** > **ÖZEL OLUŞTUR**’u seçin:</span><span class="sxs-lookup"><span data-stu-id="d43de-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="d43de-113">![BizTalk Hizmeti’ni seçin ve Özel Oluştur’u seçin][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="d43de-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="d43de-114">Merhaba BizTalk hizmeti ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="d43de-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="d43de-115"><strong>BizTalk hizmeti adı</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="d43de-116">Herhangi bir ad girin, ancak özel olsun.</span><span class="sxs-lookup"><span data-stu-id="d43de-116">You can enter any name but be specific.</span></span> <span data-ttu-id="d43de-117">Bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="d43de-117">Some examples include:</span></span><br/><br/><span data-ttu-id="d43de-118">
    <em>şirketim</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d43de-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d43de-119">
    <em>şirketimuygulamam</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d43de-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="d43de-120">
    <em>uygulamam</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="d43de-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="d43de-121">". biztalk.windows.net" girdiğiniz otomatik olarak eklenen toohello adıdır.</span><span class="sxs-lookup"><span data-stu-id="d43de-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="d43de-122">Bu gibi BizTalk hizmeti kullanılan tooaccess bir URL oluşturur <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="d43de-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-123"><strong>Sürüm</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="d43de-124">Merhaba test/geliştirme aşamasındaysanız seçin <strong>Geliştirici</strong>.</span><span class="sxs-lookup"><span data-stu-id="d43de-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="d43de-125">Merhaba üretim aşamasında, hello kullanırsanız <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: sürümler grafiği</a> toodetermine varsa <strong>Premium</strong>, <strong>standart</strong>, veya <strong>Basic</strong>, iş senaryonuz için hello doğru seçimdir.</span><span class="sxs-lookup"><span data-stu-id="d43de-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-126"><strong>Bölge</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d43de-127">Merhaba coğrafi bölge toohost BizTalk hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-128"><strong>Etki alanı URL'si</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="d43de-129"><strong>İsteğe bağlı</strong>.</span><span class="sxs-lookup"><span data-stu-id="d43de-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="d43de-130">Varsayılan olarak, hello etki alanı URL'dir <em>YourBizTalkServiceName</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d43de-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="d43de-131">Özel bir etki alanı da girilebilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-131">A custom domain can also be entered.</span></span> <span data-ttu-id="d43de-132">Örneğin, etki alanınız <em>contoso</em> olarak belirtilmişse şunları girebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d43de-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="d43de-133">
    <em>Şirketim</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d43de-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="d43de-134">
    <em>ŞirketimUygulamam</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d43de-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d43de-135">
    <em>Uygulamam</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d43de-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="d43de-136">
    <em>BizTalkHizmetAdınız</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="d43de-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="d43de-137">Merhaba İleri okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="d43de-138">5.</span><span class="sxs-lookup"><span data-stu-id="d43de-138">5.</span></span> <span data-ttu-id="d43de-139">Merhaba depolama ve veritabanı ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="d43de-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d43de-140"><strong>Depolama hesabını izleme/arşivleme</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="d43de-141">Mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d43de-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="d43de-142">Yeni bir depolama hesabı oluşturursanız, hello girin <strong>depolama hesabı adı</strong>.</span><span class="sxs-lookup"><span data-stu-id="d43de-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-143"><strong>Veritabanı izleme</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="d43de-144">Mevcut bir Azure SQL veritabanı kullanıyorsanız, başka bir BizTalk hizmeti tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="d43de-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="d43de-145">Merhaba oturum açma adı ve parola, Azure SQL veritabanı sunucusu oluşturulduğunda girilen gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="d43de-146"><strong>İpucu</strong> hello izleme veritabanı oluşturma ve izleme/arşivleme depolama hesabında BizTalk hizmeti hello gibi aynı bölgede hello.</span><span class="sxs-lookup"><span data-stu-id="d43de-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="d43de-147">Merhaba İleri okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="d43de-148">6.</span><span class="sxs-lookup"><span data-stu-id="d43de-148">6.</span></span> <span data-ttu-id="d43de-149">Merhaba veritabanı ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="d43de-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="d43de-150"><strong>Ad</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="d43de-151">Kullanılabilir olduğunda <strong>yeni bir SQL veritabanı oluştur</strong> hello önceki ekrana seçilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d43de-152">BizTalk hizmeti tarafından kullanılan bir SQL veritabanı adı toobe girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-153"><strong>Sunucu</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="d43de-154">Kullanılabilir olduğunda <strong>yeni bir SQL veritabanı oluştur</strong> hello önceki ekrana seçilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="d43de-155">Mevcut bir SQL Database Sunucusu seçin veya yeni bir SQL Database sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d43de-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-156"><strong>Sunucu oturum açma adı</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="d43de-157">Merhaba oturum açma kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-158"><strong>Sunucu oturum açma parolası</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="d43de-159">Merhaba oturum açma parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="d43de-160"><strong>Bölge</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="d43de-161"><strong>Yeni bir SQL veritabanı oluştur</strong> seçili olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="d43de-162">Merhaba coğrafi bölge toohost SQL veritabanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="d43de-163">Merhaba onay işareti toocomplete hello Sihirbazı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="d43de-164">Merhaba ilerleme simgesi görünür:</span><span class="sxs-lookup"><span data-stu-id="d43de-164">hello progress icon appears:</span></span>  
![Tamamlandığında ilerleme simgesi görüntülenir][ProgressComplete]

<span data-ttu-id="d43de-166">Tamamlandığında, Azure BizTalk hizmeti hello oluşturulan ve uygulamalarınız için hazır olur.</span><span class="sxs-lookup"><span data-stu-id="d43de-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="d43de-167">Merhaba varsayılan ayarlar yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d43de-167">hello default settings are sufficient.</span></span> <span data-ttu-id="d43de-168">Toochange hello varsayılan ayarları istiyorsanız seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="d43de-169">Ek ayarlar hello görüntülenir [Pano, İzleyici ve ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md) hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="d43de-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="d43de-170">Merhaba BizTalk hizmeti Hello durumuna bağlı olarak, tamamlanamıyor bazı işlemler vardır.</span><span class="sxs-lookup"><span data-stu-id="d43de-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="d43de-171">Bu işlemlerin bir listesi için çok Git[BizTalk Services durumu grafiği](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="d43de-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="d43de-172">Hazırlama sonrası adımlar</span><span class="sxs-lookup"><span data-stu-id="d43de-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="d43de-173">Yerel bir bilgisayara Hello sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="d43de-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="d43de-174">Üretime hazır sertifikayı ekleme</span><span class="sxs-lookup"><span data-stu-id="d43de-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="d43de-175">Merhaba erişim denetimi ad alanını alma</span><span class="sxs-lookup"><span data-stu-id="d43de-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="d43de-176"><a name="InstallCert"></a>Yerel bir bilgisayara Hello sertifika yükleme</span><span class="sxs-lookup"><span data-stu-id="d43de-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="d43de-177">BizTalk Hizmeti hazırlamanın bir parçası olarak, otomatik olarak imzalanan ve BizTalk hizmeti aboneliğinizle ilişkili bir sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d43de-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="d43de-178">Bu sertifikayı indirip burada BizTalk hizmeti uygulamalarını dağıtacağınız ya da iletileri tooa BizTalk Hizmeti uç noktası Gönder bilgisayarların yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="d43de-179">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d43de-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d43de-180">Seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmeti aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="d43de-181">Select hello **Pano** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d43de-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="d43de-182">**SSL Sertifikası İndir**’i seçin:</span><span class="sxs-lookup"><span data-stu-id="d43de-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="d43de-183">![SSL Sertifikasını Değiştirme][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="d43de-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="d43de-184">Merhaba sertifikayı çift tıklatın ve hello Sihirbazı tooinstall hello sertifika üzerinden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d43de-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="d43de-185">Merhaba altına hello sertifikayı yüklediğinizden emin olun **güvenilen kök sertifika yetkilileri** depolar.</span><span class="sxs-lookup"><span data-stu-id="d43de-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="d43de-186"><a name="AddCert"></a>Üretime hazır sertifikayı ekleme</span><span class="sxs-lookup"><span data-stu-id="d43de-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="d43de-187">BizTalk Services oluşturma yalnızca geliştirme ortamlarında kullanılmak üzere tasarlanmıştır otomatik olarak oluşturulan hello otomatik olarak imzalanan sertifika.</span><span class="sxs-lookup"><span data-stu-id="d43de-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="d43de-188">Üretim senaryoları için üretime hazır sertifikayla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d43de-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="d43de-189">Merhaba üzerinde **Pano** sekmesine **SSL sertifikasını Güncelleştir**.</span><span class="sxs-lookup"><span data-stu-id="d43de-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="d43de-190">Tooyour özel SSL sertifikasına göz atın (*CertificateName*.pfx), BizTalk hizmeti adını içeren, hello parolayı girin ve ardından hello onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d43de-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="d43de-191"><a name="ACS"></a>Merhaba erişim denetimi ad alanını alma</span><span class="sxs-lookup"><span data-stu-id="d43de-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="d43de-192">İçinde toohello oturum [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="d43de-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="d43de-193">Seçin **BIZTALK SERVICES** sol gezinti bölmesinde hello ve BizTalk hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="d43de-194">Merhaba görev çubuğunda seçin **bağlantı bilgilerini**:</span><span class="sxs-lookup"><span data-stu-id="d43de-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="d43de-195">![Bağlantı Bilgilerini seçme][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="d43de-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="d43de-196">Merhaba erişim denetimi değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d43de-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="d43de-197">Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d43de-198">Merhaba erişim denetimi ad alanı BizTalk hizmetiniz için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d43de-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="d43de-199">Merhaba erişim denetimi değerleri herhangi bir uygulama ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="d43de-200">Azure BizTalk Services oluşturulduğunda, bu erişim denetimi ad alanı BizTalk hizmeti dağıtımınız ile Merhaba kimlik doğrulaması denetler.</span><span class="sxs-lookup"><span data-stu-id="d43de-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="d43de-201">Toochange hello abonelik veya hello ad alanını yönetmek istiyorsanız seçin **ACTIVE DIRECTORY** sol gezinti bölmesinde hello ve sonra da ad alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="d43de-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="d43de-202">Merhaba görev çubuğu seçeneklerinizi listeler.</span><span class="sxs-lookup"><span data-stu-id="d43de-202">hello task bar lists your options.</span></span>

<span data-ttu-id="d43de-203">Tıklatarak **Yönet** açılır hello erişim denetimi Yönetim Portalı.</span><span class="sxs-lookup"><span data-stu-id="d43de-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="d43de-204">Hello erişim denetimi Yönetim Portalı'da, BizTalk hizmeti kullanan hello **hizmet kimliklerini**:</span><span class="sxs-lookup"><span data-stu-id="d43de-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="d43de-205">![Merhaba erişim denetimi Yönetim Portalı'nda ACS hizmet kimlikleri][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="d43de-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="d43de-206">Merhaba erişim denetimi hizmeti kimliği, uygulamaların veya istemcilerin tooauthenticate erişim denetimi ile doğrudan izin vermek ve bir belirteç almalarına kimlik bilgileri kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d43de-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d43de-207">Merhaba BizTalk hizmeti kullanan **sahibi** hello varsayılan hizmet kimliği ve hello **parola** değeri.</span><span class="sxs-lookup"><span data-stu-id="d43de-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="d43de-208">Parola değeri hello yerine hello simetrik anahtar değeri kullanırsanız hello aşağıdaki hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="d43de-209">*Belirtilen hello ile toohello erişim denetimi yönetim hizmeti hesabına bağlanılamadı kimlik bilgileri*</span><span class="sxs-lookup"><span data-stu-id="d43de-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="d43de-210">[ACS Ad Alanınızı Yönetme](https://msdn.microsoft.com/library/azure/hh674478.aspx) bazı kılavuzları ve önerileri listeler.</span><span class="sxs-lookup"><span data-stu-id="d43de-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="d43de-211">Açıklanan gereksinimler</span><span class="sxs-lookup"><span data-stu-id="d43de-211">Requirements explained</span></span>
<span data-ttu-id="d43de-212">Bu gereksinimleri toohello uygulamayın ücretsiz sürüm.</span><span class="sxs-lookup"><span data-stu-id="d43de-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="d43de-213"><strong>Ne gerekiyor?</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="d43de-214"><strong>Neden gerekiyor?</strong></span><span class="sxs-lookup"><span data-stu-id="d43de-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d43de-215">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="d43de-215">Azure subscription</span></span></td>
<td><span data-ttu-id="d43de-216">Merhaba abonelik toohello Azure portalında oturum açarak belirler.</span><span class="sxs-lookup"><span data-stu-id="d43de-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="d43de-217">Merhaba hesap sahibi oluşturur hello aboneliğinizi <a HREF="https://account.windowsazure.com/Subscriptions"> Azure abonelikleri</a>.</span><span class="sxs-lookup"><span data-stu-id="d43de-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="d43de-218">Hello Azure hesabı birden fazla abonelik olabilir ve izin herkes tarafından yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="d43de-219">Örneğin, Azure hesap sahibi adlı bir abonelik oluşturulur <em>BizTalkServiceSubscription</em> ve sağlar, şirket BizTalk yöneticileri hello (örneğin, ContosoBTSAdmins@live.com) erişim toothis abonelik.</span><span class="sxs-lookup"><span data-stu-id="d43de-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="d43de-220">Bu senaryoda, hello BizTalk Yöneticiler toohello Azure portalında oturum açın ve Azure BizTalk Services de dahil olmak üzere hello abonelikte tam yönetici hakları tooall hello barındırılan hizmetleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d43de-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="d43de-221">Merhaba BizTalk yöneticileri hello Azure hesap sahipleri değildir ve bu nedenle erişim tooany faturalama bilgileri yok.</span><span class="sxs-lookup"><span data-stu-id="d43de-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="d43de-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Hello Azure portalında abonelikleri ve depolama hesaplarını yönetecek</a> daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="d43de-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="d43de-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d43de-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="d43de-224">Merhaba tabloları, görünümleri ve saklı yordamlar hello hello izleme verileri de dahil olmak üzere, BizTalk hizmeti tarafından kullanılan depolar.</span><span class="sxs-lookup"><span data-stu-id="d43de-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="d43de-225">BizTalk Hizmeti oluşturduğunuzda, mevcut Azure SQL Sunucusu, Azure SQL Database kullanırsınız ya da otomatik olarak yeni bir Sunucu veya SQL Database oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="d43de-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="d43de-226">Merhaba SQL Database ölçeği otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="d43de-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="d43de-227">Genellikle, hello varsayılan ölçek BizTalk hizmeti için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d43de-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="d43de-228">Değişen hello ölçek fiyatı etkiler.</span><span class="sxs-lookup"><span data-stu-id="d43de-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="d43de-229">Bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Azure SQL Veritabanı'nda Hesaplar ve Faturalar</a>
</span><span class="sxs-lookup"><span data-stu-id="d43de-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="d43de-230">
<strong>Notlar</strong>
</span><span class="sxs-lookup"><span data-stu-id="d43de-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="d43de-231">Yeni bir Azure SQL sunucusu ve SQL Database oluşturduğunuzda, Azure Hizmetleri otomatik olarak etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="d43de-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="d43de-232">Merhaba BizTalk hizmeti gerektirir Azure Hizmetleri etkin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d43de-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="d43de-233">Mevcut bir Azure SQL sunucusunda yeni bir Azure SQL veritabanı oluşturursanız, güvenlik duvarı kuralları sunucu değişmez hello hello.</span><span class="sxs-lookup"><span data-stu-id="d43de-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="d43de-234">Sonuç olarak, diğer Azure hizmetlerine erişim toohello sunucunun veritabanlarına izin verilmiyor mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d43de-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="d43de-235">Azure Erişim Denetimi ad alanı</span><span class="sxs-lookup"><span data-stu-id="d43de-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="d43de-236">Azure BizTalk Services ile kimlik doğrular.</span><span class="sxs-lookup"><span data-stu-id="d43de-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="d43de-237">Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="d43de-238">BizTalk hizmeti oluşturduğunuzda, hello erişim denetimi ad alanı otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d43de-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="d43de-239">Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="d43de-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="d43de-240">Tootables, BLOB'ları ve kuyrukları, BizTalk hizmeti toosave hello aşağıdaki tarafından kullanılan erişim izni verir:</span><span class="sxs-lookup"><span data-stu-id="d43de-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="d43de-241">Bu İzleyici hello BizTalk hizmeti günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="d43de-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="d43de-242">Çıktı izleme hello hello de görüntülenir **izleme** hello Azure portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="d43de-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="d43de-243">Bir X12 veya AS2 sözleşmesi iş ortakları arasında oluştururken hello arşivleme özelliğini toostore ileti özelliklerini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d43de-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="d43de-244">Bu veriler hello depolama hesabı kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d43de-245">BizTalk hizmeti oluşturduğunuzda, mevcut bir Storage hesabını kullanabilir ya da otomatik olarak yeni bir Storage hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d43de-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="d43de-246">Merhaba varsayılan Storage ayarları BizTalk hizmeti için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="d43de-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="d43de-247">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="d43de-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="d43de-248">Bu anahtarları depolama hesabı erişim tooyour denetler.</span><span class="sxs-lookup"><span data-stu-id="d43de-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="d43de-249">Merhaba BizTalk hizmeti otomatik olarak hello birincil anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="d43de-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="d43de-250">Daha fazla bilgi için bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Storage</a>.</span><span class="sxs-lookup"><span data-stu-id="d43de-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="d43de-251">SSL özel sertifikası</span><span class="sxs-lookup"><span data-stu-id="d43de-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="d43de-252">Azure BizTalk Hizmeti oluşturulduğunda, BizTalk hizmeti adını içeren bir HTTPS URL'si de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d43de-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="d43de-253">Otomatik olarak yapılandırılan toouse otomatik olarak imzalanan salt geliştirme sertifikasını URL'dir.</span><span class="sxs-lookup"><span data-stu-id="d43de-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="d43de-254">Üretim için özel bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="d43de-255">
<strong>Önemli SSL Sertifikası Bilgileri</strong>

</span><span class="sxs-lookup"><span data-stu-id="d43de-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="d43de-256">Merhaba sertifika sona erme tarihi 5 yıldan az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d43de-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="d43de-257">Tüm özel sertifikaları için parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-257">All private certificates require a password.</span></span> <span data-ttu-id="d43de-258">Bu parolayı öğrenin ve en iyisi bu parolayı yöneticilerinizle paylaşın.</span><span class="sxs-lookup"><span data-stu-id="d43de-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="d43de-259">Otomatik olarak imzalanan sertifikalar test/geliştirme ortamında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d43de-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="d43de-260">Otomatik olarak imzalanan sertifikalar kullanıldığında hello sertifika tooyour kişisel sertifika deposuna aktarın ve güvenilen kök sertifika yetkilileri sertifika deposuna hello.</span><span class="sxs-lookup"><span data-stu-id="d43de-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="d43de-261">Merhaba üretim sertifika isteği tooyour sertifika yetkilisi gönderirken, aşağıdaki sertifika özelliklere hello verin:</span><span class="sxs-lookup"><span data-stu-id="d43de-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="d43de-262"><strong>Gelişmiş Anahtar Kullanımı</strong>: Azure BizTalk Services için en azından Sunucu Kimlik Doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d43de-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="d43de-263"><strong>Ortak ad</strong>: hello tam etki alanı adını (FQDN), Azure BizTalk hizmeti URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="d43de-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="d43de-264">Bu makaledeki <a HREF="#CreateService">BizTalk Hizmeti oluşturma</a> bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="d43de-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="d43de-265">Merhaba BizTalk hizmeti oluşturulduktan sonra yeni veya farklı bir sertifika eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d43de-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="d43de-266">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="d43de-266">Hybrid Connections</span></span>
<span data-ttu-id="d43de-267">Azure BizTalk hizmeti oluşturduğunuzda, hello **karma bağlantılar** sekmesi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="d43de-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Karma Bağlantılar Sekmesi][HybridConnectionTab]

<span data-ttu-id="d43de-269">Karma bağlantılar olan kullanılan tooconnect bir Azure Web sitesine veya Azure mobil hizmeti tooany şirket içi SQL Server, MySQL, HTTP Web API'leri, Mobile Services ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan kaynaklara.</span><span class="sxs-lookup"><span data-stu-id="d43de-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="d43de-270">Karma bağlantılar ve hello BizTalk bağdaştırıcı hizmeti farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d43de-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="d43de-271">Merhaba BizTalk bağdaştırıcı hizmeti kullanılan tooconnect Azure BizTalk Services tooan şirket içi iş kolu (LOB) sistemidir.</span><span class="sxs-lookup"><span data-stu-id="d43de-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="d43de-272">Bkz: [karma bağlantılar](integration-hybrid-connection-overview.md) oluşturma ve yönetme karma bağlantılar dahil olmak üzere daha fazla toolearn.</span><span class="sxs-lookup"><span data-stu-id="d43de-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43de-273">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d43de-273">Next steps</span></span>
<span data-ttu-id="d43de-274">Bir BizTalk hizmeti oluşturuldu, hello ile farklı öğrenmeniz [BizTalk Services: pano, İzleyici ve ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="d43de-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="d43de-275">BizTalk Hizmeti uygulamalarınız için hazır.</span><span class="sxs-lookup"><span data-stu-id="d43de-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="d43de-276">uygulamaları, Git çok oluşturma toostart[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="d43de-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="d43de-277">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d43de-277">See also</span></span>
* [<span data-ttu-id="d43de-278">BizTalk Services: Sürümler Grafiği</span><span class="sxs-lookup"><span data-stu-id="d43de-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="d43de-279">BizTalk Services: Durum Grafiği</span><span class="sxs-lookup"><span data-stu-id="d43de-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="d43de-280">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="d43de-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="d43de-281">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="d43de-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="d43de-282">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="d43de-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="d43de-283">I Başlat'ı kullanarak Azure BizTalk Services SDK'sı nasıl hello</span><span class="sxs-lookup"><span data-stu-id="d43de-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="d43de-284">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="d43de-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
