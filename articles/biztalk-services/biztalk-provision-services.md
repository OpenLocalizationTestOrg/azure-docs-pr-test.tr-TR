---
title: "Azure portalında Azure BizTalk Services oluşturma | Microsoft Belgeleri"
description: "Azure portalında Azure BizTalk Services hazırlamayı veya oluşturmayı öğrenin; MABS, WABS"
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
ms.openlocfilehash: eca77b4a82eb67e1755717bb4429f8d450a64dc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="5dff4-103">Azure portalını kullanarak BizTalk Services oluşturma</span><span class="sxs-lookup"><span data-stu-id="5dff4-103">Create BizTalk Services using the Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="5dff4-104">Azure portalında oturum açmak için bir Azure hesabınız ve Azure aboneliğiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="5dff4-105">Hesabınız yoksa birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="5dff4-106">Bkz. [Azure Ücretsiz Deneme](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="5dff4-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="5dff4-107"><a name="CreateService"></a>BizTalk Hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="5dff4-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="5dff4-108">Seçtiğiniz Sürüm’e bağlı olarak, BizTalk Hizmeti ayarlarının tümü kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="5dff4-109">[Azure portalında](http://go.microsoft.com/fwlink/p/?LinkID=213885) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5dff4-110">Alt gezinti bölmesinde **YENİ**’yi seçin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="5dff4-111">![Yeni düğmesini seçin][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="5dff4-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="5dff4-112">**UYGULAMA HİZMETLERİ** > **BIZTALK HİZMETİ** > **ÖZEL OLUŞTUR**’u seçin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="5dff4-113">![BizTalk Hizmeti’ni seçin ve Özel Oluştur’u seçin][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="5dff4-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="5dff4-114">BizTalk Hizmeti ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="5dff4-115"><strong>BizTalk hizmeti adı</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="5dff4-116">Herhangi bir ad girin, ancak özel olsun.</span><span class="sxs-lookup"><span data-stu-id="5dff4-116">You can enter any name but be specific.</span></span> <span data-ttu-id="5dff4-117">Bazı örnekler:</span><span class="sxs-lookup"><span data-stu-id="5dff4-117">Some examples include:</span></span><br/><br/><span data-ttu-id="5dff4-118">
    <em>şirketim</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="5dff4-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="5dff4-119">
    <em>şirketimuygulamam</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="5dff4-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="5dff4-120">
    <em>uygulamam</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="5dff4-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="5dff4-121">". biztalk.windows.net" otomatik olarak girdiğiniz ada eklenir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="5dff4-122">Bu, BizTalk hizmetinize erişmek için kullanılan bir URL oluşturur; örneğin, <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="5dff4-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-123"><strong>Sürüm</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="5dff4-124">Test etme/geliştirme aşamasındaysanız, <strong>Geliştirici</strong>’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="5dff4-125">Üretim aşamasındaysanız, kullanırsanız <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Sürümler Grafiği</a>’ni, iş senaryonuz için <strong>Premium</strong> mu, <strong>Standart</strong> mı, yoksa <strong>Temel</strong> sürümünün mü daha doğru olduğun saptamak amacıyla kullanın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-126"><strong>Bölge</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="5dff4-127">BizTalk Hizmetinizi barındıracak coğrafi bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-128"><strong>Etki alanı URL'si</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="5dff4-129"><strong>İsteğe bağlı</strong>.</span><span class="sxs-lookup"><span data-stu-id="5dff4-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="5dff4-130">Varsayılan olarak, etki alanı URL'si <em>YourBizTalkServiceName</em>. biztalk.windows.net biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="5dff4-131">Özel bir etki alanı da girilebilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-131">A custom domain can also be entered.</span></span> <span data-ttu-id="5dff4-132">Örneğin, etki alanınız <em>contoso</em> olarak belirtilmişse şunları girebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5dff4-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="5dff4-133">
    <em>Şirketim</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5dff4-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="5dff4-134">
    <em>ŞirketimUygulamam</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5dff4-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="5dff4-135">
    <em>Uygulamam</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5dff4-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="5dff4-136">
    <em>BizTalkHizmetAdınız</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="5dff4-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="5dff4-137">İLERİ okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="5dff4-138">5.</span><span class="sxs-lookup"><span data-stu-id="5dff4-138">5.</span></span> <span data-ttu-id="5dff4-139">Storage ve Veritabanı Ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="5dff4-140"><strong>Depolama hesabını izleme/arşivleme</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="5dff4-141">Mevcut bir depolama hesabını seçin veya yeni bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5dff4-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="5dff4-142">Yeni bir Storage hesabı oluşturuyorsanız, <strong>Storage Hesabı Adı</strong> girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-143"><strong>Veritabanı izleme</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="5dff4-144">Mevcut bir Azure SQL veritabanı kullanıyorsanız, başka bir BizTalk hizmeti tarafından kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="5dff4-145">Azure SQL Veritabanı Sunucusu oluşturulduğunda oturum açma adı ve parola girilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="5dff4-146"><strong>İPUCU</strong> BizTalk hizmetiyle aynı bölgede Veritabanı izleme ve depolama hesabı izleme/arşivleme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5dff4-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="5dff4-147">İLERİ okunu seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="5dff4-148">6.</span><span class="sxs-lookup"><span data-stu-id="5dff4-148">6.</span></span> <span data-ttu-id="5dff4-149">Veritabanı ayarlarını girin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="5dff4-150"><strong>Ad</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="5dff4-151">Önceki ekranda <strong>Yeni bir SQL veritabanı oluştur</strong> seçili olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="5dff4-152">BizTalk Hizmeti tarafından kullanılacak bir SQL Database adı girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-153"><strong>Sunucu</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="5dff4-154">Önceki ekranda <strong>Yeni bir SQL veritabanı oluştur</strong> seçili olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="5dff4-155">Mevcut bir SQL Database Sunucusu seçin veya yeni bir SQL Database sunucusu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5dff4-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-156"><strong>Sunucu oturum açma adı</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="5dff4-157">Oturum açma kullanıcı adını girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-158"><strong>Sunucu oturum açma parolası</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="5dff4-159">Oturum açma parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="5dff4-160"><strong>Bölge</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="5dff4-161"><strong>Yeni bir SQL veritabanı oluştur</strong> seçili olduğunda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="5dff4-162">SQL Database’inizi barındıracak coğrafi bölgeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="5dff4-163">Sihirbazı tamamlamak için onay işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="5dff4-164">İlerleme simgesi görünür:</span><span class="sxs-lookup"><span data-stu-id="5dff4-164">The progress icon appears:</span></span>  
![Tamamlandığında ilerleme simgesi görüntülenir][ProgressComplete]

<span data-ttu-id="5dff4-166">Tamamlandığında, Azure BizTalk Hizmeti oluşturulmuştur ve uygulamalarınız için hazırdır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="5dff4-167">Varsayılan ayarlar yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-167">The default settings are sufficient.</span></span> <span data-ttu-id="5dff4-168">Varsayılan ayarları değiştirmek istiyorsanız, sol gezinti bölmesinde **BIZTALK HİZMETLERİ**’ni, sonra da BizTalk Hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="5dff4-169">En üstteki [Pano, İzleyici ve Ölçek sekmelerinde](biztalk-dashboard-monitor-scale-tabs.md) ek ayarlar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="5dff4-170">BizTalk Hizmeti durumunu bağlı olarak, bazı tamamlanamayan işlemler vardır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="5dff4-171">Bu işlemlerin bir listesi için [BizTalk Services Durumu Grafiği](biztalk-service-state-chart.md)’ne gidin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="5dff4-172">Hazırlama sonrası adımlar</span><span class="sxs-lookup"><span data-stu-id="5dff4-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="5dff4-173">Sertifikayı yerel bir bilgisayara yükleme</span><span class="sxs-lookup"><span data-stu-id="5dff4-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="5dff4-174">Üretime hazır sertifikayı ekleme</span><span class="sxs-lookup"><span data-stu-id="5dff4-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="5dff4-175">Access Control ad alanını alma</span><span class="sxs-lookup"><span data-stu-id="5dff4-175">Get the Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="5dff4-176"><a name="InstallCert"></a>Sertifikayı yerel bir bilgisayara yükleme</span><span class="sxs-lookup"><span data-stu-id="5dff4-176"><a name="InstallCert"></a>Install the certificate on a local computer</span></span>
<span data-ttu-id="5dff4-177">BizTalk Hizmeti hazırlamanın bir parçası olarak, otomatik olarak imzalanan ve BizTalk hizmeti aboneliğinizle ilişkili bir sertifika oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="5dff4-178">Bu sertifikayı indirip BizTalk Hizmeti uç noktasına iletileri göndereceğiniz veya BizTalk Hizmeti uygulamalarını dağıtacağınız bilgisayarlara bunu yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="5dff4-179">[Azure portalında](http://go.microsoft.com/fwlink/p/?LinkID=213885) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5dff4-180">Sol gezinti bölmesinde **BIZTALK HİZMETLERİ**’ni, sonra da BizTalk Hizmeti aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="5dff4-181">**Pano** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="5dff4-182">**SSL Sertifikası İndir**’i seçin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="5dff4-183">![SSL Sertifikasını Değiştirme][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="5dff4-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="5dff4-184">Sertifikaya çift tıklayın ve sertifikayı yüklemek için sihirbazda ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="5dff4-185">**Güvenilen Kök Sertifika Yetkilileri** deposu altına sertifikayı yüklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5dff4-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="5dff4-186"><a name="AddCert"></a>Üretime hazır sertifikayı ekleme</span><span class="sxs-lookup"><span data-stu-id="5dff4-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="5dff4-187">BizTalk Services oluşturulduğunda otomatik olarak oluşturulan otomatik imzalı sertifika yalnızca geliştirme ortamlarında kullanılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="5dff4-188">Üretim senaryoları için üretime hazır sertifikayla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="5dff4-189">**Pano** sekmesinde **SSL Sertifikasını Güncelleştir**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="5dff4-190">BizTalk Hizmet adınızı ekleyen özel SSL sertifikanıza (*CertificateName*.pfx) göz atın, parolayı girin ve ardından onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <span data-ttu-id="5dff4-191"><a name="ACS"></a>Access Control ad alanını alma</span><span class="sxs-lookup"><span data-stu-id="5dff4-191"><a name="ACS"></a>Get the Access Control namespace</span></span>
1. <span data-ttu-id="5dff4-192">[Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=213885) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="5dff4-193">Sol gezinti bölmesinde **BIZTALK HİZMETLERİ**’ni, sonra da BizTalk Hizmetini seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="5dff4-194">Görev çubuğunda **Bağlantı Bilgileri**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="5dff4-195">![Bağlantı Bilgilerini seçme][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="5dff4-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="5dff4-196">Erişim Denetimi değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-196">Copy the Access Control values.</span></span>

<span data-ttu-id="5dff4-197">Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="5dff4-198">Erişim Denetimi ad alanı BizTalk Hizmetiniz için otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="5dff4-199">Erişim Denetimi değerleri herhangi bir uygulamayla birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="5dff4-200">Azure BizTalk Services oluşturulduğunda, bu Erişim Denetimi ad alanı kimlik doğrulamasını BizTalk hizmeti dağıtımınızla denetler.</span><span class="sxs-lookup"><span data-stu-id="5dff4-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="5dff4-201">Aboneliğinizi değiştirmek veya ad alanını yönetmek isterseniz, sol bölmedeki **ACTIVE DIRECTORY**’yi, sonra da ad alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="5dff4-202">Görev çubuğu seçeneklerinizi listeler.</span><span class="sxs-lookup"><span data-stu-id="5dff4-202">The task bar lists your options.</span></span>

<span data-ttu-id="5dff4-203">**Yönet**’e tıklanması Erişim Denetimi Yönetim Portalı’nı açar.</span><span class="sxs-lookup"><span data-stu-id="5dff4-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="5dff4-204">Erişim Denetimi Yönetim Portalı'nda, BizTalk hizmeti **hizmet kimliklerini** kullanır:</span><span class="sxs-lookup"><span data-stu-id="5dff4-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="5dff4-205">![Access Control Yönetim Portalı’nda ACS Hizmet Kimlikleri][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="5dff4-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="5dff4-206">Erişim Denetimi hizmeti kimliği, uygulamaların veya istemcilerin Erişim Denetimi’yle doğrudan kimlik doğrulaması yapmasını ve belirteç almasını sağlayan bir dizi kimlik bilgisidir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dff4-207">BizTalk Hizmeti varsayılan hizmet kimliği ve **Parola** değeri için **Sahip**’i kullanır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="5dff4-208">Parola değeri yerine Simetrik Anahtar değeri kullanırsanız aşağıdaki hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="5dff4-209">*Belirtilen kimlik bilgileriyle Access Control Yönetim Hizmeti hesabına bağlanılamadı*</span><span class="sxs-lookup"><span data-stu-id="5dff4-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="5dff4-210">[ACS Ad Alanınızı Yönetme](https://msdn.microsoft.com/library/azure/hh674478.aspx) bazı kılavuzları ve önerileri listeler.</span><span class="sxs-lookup"><span data-stu-id="5dff4-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="5dff4-211">Açıklanan gereksinimler</span><span class="sxs-lookup"><span data-stu-id="5dff4-211">Requirements explained</span></span>
<span data-ttu-id="5dff4-212">Bu gereksinimler Ücretsiz Sürüm için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="5dff4-213"><strong>Ne gerekiyor?</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="5dff4-214"><strong>Neden gerekiyor?</strong></span><span class="sxs-lookup"><span data-stu-id="5dff4-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5dff4-215">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="5dff4-215">Azure subscription</span></span></td>
<td><span data-ttu-id="5dff4-216">Abonelik, Azure portalında kimin oturum açabileceğini saptar.</span><span class="sxs-lookup"><span data-stu-id="5dff4-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="5dff4-217">Hesap sahibi aboneliği <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Abonelikleri</a>’nde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-218">Azure hesabında birden fazla abonelik olabilir ve izni olan herkes tarafından yönetilebilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="5dff4-219">Örneğin, Azure hesap sahibiniz <em>BizTalkServiceSubscription</em> adlı bir abonelik oluşturur ve şirketinizdeki BizTalk Yöneticilerine (örneğin, ContosoBTSAdmins@live.com) bu abonelik için erişim hakkı verir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="5dff4-220">Bu senaryoda, BizTalk Yöneticileri Azure portalında oturum açar ve Azure BizTalk Services de dahil olmak üzere abonelikte barındırılan tüm hizmetler için tam yönetici haklarına sahip olurlar.</span><span class="sxs-lookup"><span data-stu-id="5dff4-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="5dff4-221">BizTalk Yöneticileri Azure hesap sahipleri değildir; bu nedenle de herhangi fatura bilgilerine erişimleri yoktur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="5dff4-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Azure portalında Abonelikleri ve Depolama Hesaplarını Yönetme</a> konusu daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5dff4-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="5dff4-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5dff4-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="5dff4-224">Veri izleme de dahil, BizTalk Hizmeti tarafından kullanılan tablolar, görünümler ve depolanan yordamlar.</span><span class="sxs-lookup"><span data-stu-id="5dff4-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-225">BizTalk Hizmeti oluşturduğunuzda, mevcut Azure SQL Sunucusu, Azure SQL Database kullanırsınız ya da otomatik olarak yeni bir Sunucu veya SQL Database oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-226">SQL Database ölçeği otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="5dff4-227">Genellikle, varsayılan ölçek BizTalk hizmeti için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="5dff4-228">Ölçeğin değiştirilmesi fiyatı etkiler.</span><span class="sxs-lookup"><span data-stu-id="5dff4-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="5dff4-229">Bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Azure SQL Veritabanı'nda Hesaplar ve Faturalar</a>
</span><span class="sxs-lookup"><span data-stu-id="5dff4-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="5dff4-230">
<strong>Notlar</strong>
</span><span class="sxs-lookup"><span data-stu-id="5dff4-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="5dff4-231">Yeni bir Azure SQL sunucusu ve SQL Database oluşturduğunuzda, Azure Hizmetleri otomatik olarak etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="5dff4-232">BizTalk Hizmeti için Azure Hizmetlerinin etkin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="5dff4-233">Mevcut Azure SQL Sunucusunda yeni bir Azure SQL Database oluşturursanız, Sunucunun güvenlik duvarı kuralları değişmez.</span><span class="sxs-lookup"><span data-stu-id="5dff4-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="5dff4-234">Sonuç olarak, başka Azure Hizmetlerinin Sunucunun veritabanlarına erişim izni yoktur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="5dff4-235">Azure Erişim Denetimi ad alanı</span><span class="sxs-lookup"><span data-stu-id="5dff4-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="5dff4-236">Azure BizTalk Services ile kimlik doğrular.</span><span class="sxs-lookup"><span data-stu-id="5dff4-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="5dff4-237">Visual Studio’dan BizTalk Hizmeti projesini dağıttığınızda, Erişim Denetimi ad alanına bunu girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="5dff4-238">BizTalk Hizmeti oluşturduğunuzda, Erişim Denetimi ad alanı otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="5dff4-239">Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="5dff4-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="5dff4-240">BizTalk hizmetinizin kullandığı tablolara, blob'lara ve kuyruklara erişim vererek aşağıdakileri kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5dff4-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="5dff4-241">BizTalk Hizmetini izleyen günlük dosyaları.</span><span class="sxs-lookup"><span data-stu-id="5dff4-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="5dff4-242">İzleme çıktısı Azure portalındaki **İzleme** sekmesinde de görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="5dff4-243">İş ortakları arasında X12 veya AS2 sözleşmesi oluşturulduğunda, ileti özelliklerini depolamak için Arşivleme özelliğini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="5dff4-244">Bu veriler Storage hesabına kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="5dff4-245">BizTalk hizmeti oluşturduğunuzda, mevcut bir Storage hesabını kullanabilir ya da otomatik olarak yeni bir Storage hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-246">Varsayılan Storage ayarları BizTalk hizmeti için yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-247">Storage hesabı oluşturduğunuzda, Birincil ve İkincil Anahtar da otomatik olarak oluşur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="5dff4-248">Bu Anahtarlar Storage hesabınıza erişimi denetler.</span><span class="sxs-lookup"><span data-stu-id="5dff4-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="5dff4-249">BizTalk Hizmeti otomatik olarak Birincil Anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="5dff4-250">Daha fazla bilgi için bkz. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Storage</a>.</span><span class="sxs-lookup"><span data-stu-id="5dff4-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="5dff4-251">SSL özel sertifikası</span><span class="sxs-lookup"><span data-stu-id="5dff4-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="5dff4-252">Azure BizTalk Hizmeti oluşturulduğunda, BizTalk hizmeti adını içeren bir HTTPS URL'si de oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5dff4-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="5dff4-253">Bu URL, otomatik olarak imzalanan salt geliştirme sertifikasını kullanmak için otomatik olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="5dff4-254">Üretim için özel bir SSL sertifikası gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="5dff4-255">
<strong>Önemli SSL Sertifikası Bilgileri</strong>

</span><span class="sxs-lookup"><span data-stu-id="5dff4-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="5dff4-256">Sertifikanın son kullanım tarihi 5 yıldan az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="5dff4-257">Tüm özel sertifikaları için parola gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-257">All private certificates require a password.</span></span> <span data-ttu-id="5dff4-258">Bu parolayı öğrenin ve en iyisi bu parolayı yöneticilerinizle paylaşın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="5dff4-259">Otomatik olarak imzalanan sertifikalar test/geliştirme ortamında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="5dff4-260">Otomatik olarak imzalanan sertifikalar kullanıldığında, sertifikayı Kişisel sertifika deponuza ve Güvenilen Kök Sertifika Yetkilileri sertifika deposuna içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="5dff4-261">Sertifika yetkilinize üretim sertifikası isteği gönderildiğinde, şu sertifika özelliklerini verin:</span><span class="sxs-lookup"><span data-stu-id="5dff4-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="5dff4-262"><strong>Gelişmiş Anahtar Kullanımı</strong>: Azure BizTalk Services için en azından Sunucu Kimlik Doğrulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="5dff4-263"><strong>Ortak Ad</strong>: Azure BizTalk Hizmeti URL'nizin tam etki alanı adını (FQDN) girin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="5dff4-264">Bu makaledeki <a HREF="#CreateService">BizTalk Hizmeti oluşturma</a> bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="5dff4-265">BizTalk Hizmeti oluşturulduktan sonra yeni veya farklı bir sertifika eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5dff4-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="5dff4-266">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="5dff4-266">Hybrid Connections</span></span>
<span data-ttu-id="5dff4-267">Azure BizTalk hizmeti oluşturduğunuzda **Karma Bağlantılar** sekmesi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="5dff4-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![Karma Bağlantılar Sekmesi][HybridConnectionTab]

<span data-ttu-id="5dff4-269">Karma Bağlantılar Azure web sitesine veya Azure mobil hizmetinden SQL Sunucusu, MySQL, HTTP Web API'leri, Mobile Services ve birçok özel Web Hizmeti gibi statik TCP bağlantı noktası kullanan şirket içi kaynaklara bağlanmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="5dff4-270">Karma Bağlantılar ve BizTalk Bağdaştırıcı Hizmeti farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="5dff4-271">BizTalk Bağdaştırıcı Hizmeti, Azure BizTalk Services’ı şirket içi iş kolu (LOB) sistemine bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="5dff4-272">Karma Bağlantıları oluşturma ve yönetme de dahil, daha fazla bilgi için bkz. [Karma Bağlantılar](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5dff4-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5dff4-273">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5dff4-273">Next steps</span></span>
<span data-ttu-id="5dff4-274">Artık bir BizTalk Hizmeti oluşturuldu, şimdi de kendinizi farklı [BizTalk Services: Pano, İzleyici ve Ölçek sekmeleri](biztalk-dashboard-monitor-scale-tabs.md) ile tanışmaya hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="5dff4-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="5dff4-275">BizTalk Hizmeti uygulamalarınız için hazır.</span><span class="sxs-lookup"><span data-stu-id="5dff4-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="5dff4-276">Uygulamalar oluşturmaya başlamak için [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197)’a gidin.</span><span class="sxs-lookup"><span data-stu-id="5dff4-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="5dff4-277">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="5dff4-277">See also</span></span>
* [<span data-ttu-id="5dff4-278">BizTalk Services: Sürümler Grafiği</span><span class="sxs-lookup"><span data-stu-id="5dff4-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="5dff4-279">BizTalk Services: Durum Grafiği</span><span class="sxs-lookup"><span data-stu-id="5dff4-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="5dff4-280">BizTalk Services: Yedekleme ve Geri Yükleme</span><span class="sxs-lookup"><span data-stu-id="5dff4-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="5dff4-281">BizTalk Services: Azaltma</span><span class="sxs-lookup"><span data-stu-id="5dff4-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="5dff4-282">BizTalk Services: Verenin Adı ve Verenin Anahtarı</span><span class="sxs-lookup"><span data-stu-id="5dff4-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="5dff4-283">Azure BizTalk Services SDK'sını Kullanmaya Nasıl Başlarım</span><span class="sxs-lookup"><span data-stu-id="5dff4-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="5dff4-284">Karma Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="5dff4-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
