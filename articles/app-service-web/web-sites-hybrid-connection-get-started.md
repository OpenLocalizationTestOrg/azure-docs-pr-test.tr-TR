---
title: "Azure App Service içinde karma bağlantılar kullanarak aaaAccess şirket içi kaynakları"
description: "Azure App Service'in web uygulamasında ve statik bir TCP bağlantı noktası kullanan şirket içi kaynağı arasında bağlantı oluşturma"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="2d99f-103">Azure Uygulama Hizmeti’nde karma bağlantıları kullanarak şirket içi kaynaklara erişme</span><span class="sxs-lookup"><span data-stu-id="2d99f-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="2d99f-104">SQL Server, MySQL, HTTP Web API'leri ve birçok özel Web hizmeti gibi statik TCP bağlantı kullanan bir Azure uygulama hizmeti uygulaması tooany şirket içi kaynaklara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="2d99f-105">Bu makale size nasıl gösterir toocreate uygulama hizmeti ile bir şirket içi SQL Server veritabanı arasında karma bir bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2d99f-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="2d99f-106">Hello Web Apps bölümü hello karma bağlantılar özelliği yalnızca hello kullanılabilir [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2d99f-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="2d99f-107">toocreate BizTalk Services bağlantısında bkz [karma bağlantılar](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="2d99f-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="2d99f-108">Bu içerik, Azure uygulama hizmetinde tooMobile uygulamalar da geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2d99f-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2d99f-109">Prerequisites</span></span>
* <span data-ttu-id="2d99f-110">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="2d99f-110">An Azure subscription.</span></span> <span data-ttu-id="2d99f-111">Ücretsiz bir abonelik için bkz: [Azure ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d99f-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="2d99f-112">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d99f-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2d99f-113">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2d99f-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="2d99f-114">toouse bir şirket içi SQL Server veya SQL Server Express veritabanı ile karma bağlantı, TCP/IP'yi statik bağlantı noktası üzerinde etkin toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="2d99f-115">Statik bağlantı noktası 1433 kullandığından, varsayılan bir örnek SQL Server üzerinde kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="2d99f-116">Yükleme ve karma bağlantılar ile kullanmak için SQL Server Express yapılandırma hakkında daha fazla bilgi için bkz: [Bağlan tooan şirket içi SQL Server bir Azure web karma bağlantılar kullanarak sitesinden](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2d99f-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="2d99f-117">Merhaba bilgisayar üzerinde bu makalenin sonraki bölümlerinde açıklanan hello şirket içi karma Bağlantı Yöneticisi aracısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="2d99f-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="2d99f-118">Mümkün tooconnect tooAzure 5671 bağlantı noktası üzerinden olmalıdır</span><span class="sxs-lookup"><span data-stu-id="2d99f-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="2d99f-119">Mümkün tooreach hello olmalıdır *ana bilgisayar adı*:*BağlantıNoktasıNumarası* , şirket içi kaynak.</span><span class="sxs-lookup"><span data-stu-id="2d99f-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="2d99f-120">Bu makaledeki adımları Hello hello tarayıcı hello şirket içi karma bağlantı aracısını barındıracak bir hello bilgisayardan kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="2d99f-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="2d99f-121">Hello Azure portalı bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d99f-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="2d99f-122">Merhaba toouse Bu öğretici için istediğiniz Azure Portal, web uygulaması veya mobil uygulama arka ucu önceden oluşturduğunuz, şimdi çok atlayabilirsiniz[karma bağlantı ve bir BizTalk hizmeti oluşturma](#CreateHC) ve buradan başlayın.</span><span class="sxs-lookup"><span data-stu-id="2d99f-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="2d99f-123">Merhaba sol üst köşedeki Merhaba, [Azure Portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil** > **Web uygulaması**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Yeni web uygulaması][NewWebsite]
2. <span data-ttu-id="2d99f-125">Merhaba üzerinde **Web uygulaması** dikey penceresinde, bir URL sağlayın ve tıklatın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Web sitesi adı][WebsiteCreationBlade]
3. <span data-ttu-id="2d99f-127">Birkaç dakika sonra hello web uygulaması oluşturuldu ve kendi web uygulaması dikey penceresi görünür.</span><span class="sxs-lookup"><span data-stu-id="2d99f-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="2d99f-128">Merhaba dikey sitenizi yönetmenize olanak sağlayan bir dikey olarak kaydırılabilir Pano ' dir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Çalışan Web sitesi][WebSiteRunningBlade]
4. <span data-ttu-id="2d99f-130">tooverify hello site canlı, hello tıklayabilirsiniz **Gözat** simgesi toodisplay hello varsayılan sayfası.</span><span class="sxs-lookup"><span data-stu-id="2d99f-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Web uygulamanızı Gözat toosee'ı tıklatın][Browse]
   
    ![Varsayılan web uygulama sayfası][DefaultWebSitePage]

<span data-ttu-id="2d99f-133">Ardından, karma bir bağlantı ve BizTalk hizmeti hello web uygulaması için oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2d99f-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="2d99f-134">Karma bağlantı ve bir BizTalk hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d99f-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="2d99f-135">Web uygulaması dikey penceresinde tıklayın **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Karma bağlantılar][CreateHCHCIcon]
2. <span data-ttu-id="2d99f-137">Merhaba karma bağlantıları dikey penceresinde **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="2d99f-138">Merhaba **karma bağlantı ekleyin** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="2d99f-139">İlk karma bağlantınız olduğundan hello **yeni karma bağlantı** seçeneği önceden seçilmiştir ve hello **karma bağlantı oluşturmak** sizin için dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Karma bağlantı oluşturma][TwinCreateHCBlades]
   
    <span data-ttu-id="2d99f-141">Merhaba üzerinde **oluşturma karma bağlantı dikey**:</span><span class="sxs-lookup"><span data-stu-id="2d99f-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="2d99f-142">İçin **adı**, hello bağlantı için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="2d99f-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="2d99f-143">İçin **ana bilgisayar adı**, hello kaynağınız barındıran hello şirket içi bilgisayarın adını girin.</span><span class="sxs-lookup"><span data-stu-id="2d99f-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="2d99f-144">İçin **bağlantı noktası**, şirket içi kaynağa (1433 SQL Server varsayılan bir örnek için) kullandığı hello bağlantı noktası numarası girin.</span><span class="sxs-lookup"><span data-stu-id="2d99f-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="2d99f-145">Tıklatın **Biz konuşması hizmeti**</span><span class="sxs-lookup"><span data-stu-id="2d99f-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="2d99f-146">Merhaba **BizTalk hizmeti oluşturma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="2d99f-147">Merhaba BizTalk hizmeti için bir ad girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![BizTalk hizmeti oluşturma][CreateHCCreateBTS]
   
    <span data-ttu-id="2d99f-149">Merhaba **BizTalk hizmeti oluşturma** dikey penceresi kapanır ve toohello döndürülen **karma bağlantı oluşturmak** dikey.</span><span class="sxs-lookup"><span data-stu-id="2d99f-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="2d99f-150">Merhaba oluşturma karma bağlantı dikey penceresinde **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Tamam'ı tıklatın][CreateBTScomplete]
6. <span data-ttu-id="2d99f-152">Merhaba işlemi tamamlandıktan sonra hello Portal bildirimleri alanında hello hello bağlantı başarıyla oluşturuldu bildirir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="2d99f-153">Merhaba web uygulamanızın dikey penceresinde hello **karma bağlantılar** simgesi artık gösterir 1 karma bağlantı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="2d99f-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Oluşturulan bir karma bağlantı][CreateHCOneConnectionCreated]

<span data-ttu-id="2d99f-155">Bu noktada, hello bulut karma bağlantı altyapı önemli bir kısmını tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="2d99f-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="2d99f-156">Ardından, karşılık gelen bir şirket içi parça oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2d99f-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="2d99f-157">Merhaba şirket içi karma Bağlantı Yöneticisi toocomplete hello Bağlantısı'nı yükleme</span><span class="sxs-lookup"><span data-stu-id="2d99f-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="2d99f-158">Merhaba web uygulamanızın dikey penceresinde **tüm ayarları** > **ağ** > **karma bağlantı uç noktalarınızı yapılandırın**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Karma bağlantıları simgesi][HCIcon]
2. <span data-ttu-id="2d99f-160">Merhaba üzerinde **karma bağlantılar** dikey penceresinde, hello **durum** sütun hello için en son eklenen uç nokta gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="2d99f-161">Merhaba bağlantı tooconfigure'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="2d99f-161">Click hello connection tooconfigure it.</span></span>
   
    ![Bağlı değil][NotConnected]
   
    <span data-ttu-id="2d99f-163">Merhaba karma bağlantı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="2d99f-165">Merhaba dikey penceresinde **dinleyicisi Kur**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Dinleyici Kur'a tıklayın][ClickListenerSetup]
4. <span data-ttu-id="2d99f-167">Merhaba **karma bağlantı özelliklerini** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="2d99f-168">Altında **şirket içi karma Bağlantı Yöneticisi**, seçin **tooinstall burayı**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Tooinstall burayı tıklatın][ClickToInstallHCM]
5. <span data-ttu-id="2d99f-170">Merhaba uygulamayı çalıştırmak Güvenlik Uyarısı iletişim kutusunda seçin **çalıştırmak** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="2d99f-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Çalışma toocontinue seçin][ApplicationRunWarning]
6. <span data-ttu-id="2d99f-172">Merhaba, **kullanıcı hesabı denetimi** iletişim kutusunda, seçin **Evet**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Evet'i seçin][UAC]
7. <span data-ttu-id="2d99f-174">Merhaba karma Bağlantı Yöneticisi'ni indirilen ve yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="2d99f-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Yükleme][HCMInstalling]
8. <span data-ttu-id="2d99f-176">Merhaba yükleme tamamlandığında tıklayın **Kapat**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-176">When hello install completes, click **Close**.</span></span>
   
    ![Kapat'ı tıklatın][HCMInstallComplete]
   
    <span data-ttu-id="2d99f-178">Merhaba üzerinde **karma bağlantılar** dikey penceresinde, hello **durum** sütun şimdi gösterir **bağlı**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Bağlı durumu][HCStatusConnected]

<span data-ttu-id="2d99f-180">Bu hello karma bağlantı altyapı tamamlandı şimdi onu kullanan bir karma uygulama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2d99f-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="2d99f-181">Merhaba aşağıdaki bölümler şunları nasıl yapacağınızı toouse Mobile Apps .NET arka uç projesi ile karma bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2d99f-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="2d99f-182">Merhaba mobil uygulama .NET arka uç projesi tooconnect toohello SQL Server veritabanını Yapılandır</span><span class="sxs-lookup"><span data-stu-id="2d99f-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="2d99f-183">App Service'de Mobile Apps .NET arka uç projesi yalnızca ASP.NET web uygulamasını bir ek Mobile Apps yüklenmiş ve başlatılmış SDK'sı ' dir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="2d99f-184">toouse web uygulamanızı Mobile Apps arka uç olarak gerekir [indirin ve hello Mobile Apps .NET arka ucu SDK başlatma](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="2d99f-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="2d99f-185">Mobil uygulamalar için ayrıca hello şirket içi veritabanı için bir bağlantı dizesi toodefine gerekir ve hello arka uç toouse bu bağlantıyı değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="2d99f-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="2d99f-186">Visual Studio'da Aç hello Web.config dosyasında, mobil uygulama .NET arka ucu için Çözüm Gezgini'nde hello bulun **connectionStrings** bölümünde, yeni bir SqlClient giriş hangi noktaları toohello şirket içi SQL hello aşağıdaki gibi ekleyin: Veritabanı sunucusu:</span><span class="sxs-lookup"><span data-stu-id="2d99f-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="2d99f-187">Tooreplace unutmayın `<**secure_password**>` için oluşturduğunuz hello parola ile bu dizesinde *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="2d99f-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="2d99f-188">Tıklatın **kaydetmek** Visual Studio toosave hello Web.config dosyasında.</span><span class="sxs-lookup"><span data-stu-id="2d99f-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2d99f-189">Bu bağlantı ayarı hello yerel bilgisayarda çalışırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="2d99f-190">Azure üzerinde çalışırken, bu ayarı geçersiz kılınmadı hello Portalı'nda tanımlanan hello bağlantı ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="2d99f-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="2d99f-191">Merhaba genişletin **modelleri** klasörü ve biten açık hello veri modeli dosyası *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="2d99f-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="2d99f-192">Merhaba değiştirme **DbContext** örnek oluşturucusu toopass hello değeri `OnPremisesDBConnection` toohello temel **DbContext** oluşturucusu, aşağıdaki kod parçacığında benzer toohello:</span><span class="sxs-lookup"><span data-stu-id="2d99f-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="2d99f-193">Merhaba hizmeti şimdi hello yeni bağlantı toohello SQL Server veritabanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="2d99f-194">Merhaba mobil uygulama arka uç toouse hello şirket içi bağlantı dizesi güncelleştir</span><span class="sxs-lookup"><span data-stu-id="2d99f-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="2d99f-195">Ardından, böylece Azure'dan kullanılabilir tooadd bir uygulama ayarı için bu yeni bağlantı dizesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="2d99f-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="2d99f-196">Merhaba edilene [Azure portal](https://portal.azure.com) mobil uygulamanızın hello web app arka uç kodu içini tıklatın **tüm ayarları**, ardından **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="2d99f-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="2d99f-197">Merhaba, **Web uygulaması ayarları** dikey penceresinde çok ilerleyin**bağlantı dizeleri** ve yeni bir ekleyin **SQL Server** adlı bağlantı dizesi `OnPremisesDBConnection` gibibirdeğeresahip`Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="2d99f-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="2d99f-198">Değiştir `<**secure_password**>` şirket içi veritabanınız için hello güvenli parola ile.</span><span class="sxs-lookup"><span data-stu-id="2d99f-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Şirket içi veritabanı için bağlantı dizesi](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="2d99f-200">Tuşuna **kaydetmek** toosave hello karma bağlantı ve bağlantı dizesi, yeni oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="2d99f-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="2d99f-201">Bu noktada hello sunucu projesi yeniden yayımlamanız ve mevcut Mobile Apps istemcileriniz ile Merhaba yeni bağlantı sınayın.</span><span class="sxs-lookup"><span data-stu-id="2d99f-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="2d99f-202">Veri okuma ve hello karma bağlantıyı kullanarak toohello şirket içi veritabanına yazılır.</span><span class="sxs-lookup"><span data-stu-id="2d99f-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="2d99f-203">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2d99f-203">Next Steps</span></span>
* <span data-ttu-id="2d99f-204">Karma bağlantı kullanan bir ASP.NET web uygulaması oluşturma hakkında daha fazla bilgi için bkz: [Bağlan tooan şirket içi SQL Server bir Azure web karma bağlantılar kullanarak sitesinden](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2d99f-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="2d99f-205">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="2d99f-205">Additional Resources</span></span>
[<span data-ttu-id="2d99f-206">Karma Bağlantılara genel bakış</span><span class="sxs-lookup"><span data-stu-id="2d99f-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="2d99f-207">Karma bağlantılar (Channel 9 video) Josh geçiş sunar</span><span class="sxs-lookup"><span data-stu-id="2d99f-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="2d99f-208">Karma bağlantılar web sitesi</span><span class="sxs-lookup"><span data-stu-id="2d99f-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="2d99f-209">BizTalk Services: Pano, İzleyici, Ölçek, yapılandırma ve karma bağlantı sekmeleri</span><span class="sxs-lookup"><span data-stu-id="2d99f-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="2d99f-210">Gerçek dünya karma bir buluta sorunsuz uygulama taşıma (Channel 9 video) ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="2d99f-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="2d99f-211">Connect tooan şirket içi karma bağlantılar (Channel 9 video) kullanarak Azure Mobile Services SQL Server'dan</span><span class="sxs-lookup"><span data-stu-id="2d99f-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="2d99f-212">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="2d99f-212">What's changed</span></span>
* <span data-ttu-id="2d99f-213">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2d99f-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
