---
title: "aaaHow tooSet bilgisayarı .NET ile Media Services geliştirmeye yönelik kurma"
description: ".NET için hello Media Services SDK'sını kullanarak Media Services hello önkoşulları hakkında bilgi edinin. Da bilgi nasıl toocreate bir Visual Studio uygulaması."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="94428-104">.NET ile Media Services Geliştirme</span><span class="sxs-lookup"><span data-stu-id="94428-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="94428-105">Bu konuda toostart geliştirme medya hizmetleri nasıl ele alınmıştır .NET kullanan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="94428-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="94428-106">Merhaba **Azure Media Services .NET SDK'sı** kitaplığı .NET kullanarak Media Services karşı tooprogram sağlar.</span><span class="sxs-lookup"><span data-stu-id="94428-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="94428-107">Bu bile .NET ile daha kolay toodevelop hello toomake **Azure Media Services .NET SDK uzantıları** kitaplığı sağlanır.</span><span class="sxs-lookup"><span data-stu-id="94428-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="94428-108">Bu kitaplığı bir dizi genişletme yöntemleri ve .NET kodunuzu basitleştirmeye yardımcı işlevlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="94428-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="94428-109">Her iki kitaplıkları aracılığıyla kullanılabilir **NuGet** ve **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="94428-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94428-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="94428-110">Prerequisites</span></span>
* <span data-ttu-id="94428-111">Yeni veya mevcut bir Azure aboneliğinde bir Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="94428-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="94428-112">Merhaba konusuna [nasıl tooCreate Media Services hesabı](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="94428-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="94428-113">İşletim sistemleri: Windows 10, Windows 7, Windows 2008 R2 veya Windows 8.</span><span class="sxs-lookup"><span data-stu-id="94428-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="94428-114">.NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="94428-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="94428-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94428-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="94428-116">Visual Studio projesi oluşturup yapılandırma</span><span class="sxs-lookup"><span data-stu-id="94428-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="94428-117">Bu bölümde, nasıl gösterilir toocreate Visual Studio Proje ve Media Services geliştirmeye kaydınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="94428-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="94428-118">Bu durumda, bir C# Windows konsol uygulaması hello projedir, ancak hello burada gösterilen aynı kurulum adımlarını geçerli tooother tür projeler için Media Services uygulamalar (örneğin, bir Windows Forms uygulaması veya bir ASP.NET Web uygulaması) oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94428-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="94428-119">Bu bölümde gösterilmiştir nasıl toouse **NuGet** tooadd Media Services .NET SDK uzantıları ve diğer bağımlı kitaplıkları.</span><span class="sxs-lookup"><span data-stu-id="94428-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="94428-120">Alternatif olarak, Github'dan hello son Media Services .NET SDK'sı BITS alabilirsiniz ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) veya [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)) hello çözümü oluşturmak ve hello başvuruları toohello istemci projesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="94428-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="94428-121">Tüm hello gerekli bağımlılıkları indirilir ve otomatik olarak ayıklanan.</span><span class="sxs-lookup"><span data-stu-id="94428-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="94428-122">Visual Studio’da yeni bir C# Konsol Uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="94428-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="94428-123">Merhaba girin **adı**, **konumu**, ve **çözüm adı**ve ardından Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="94428-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="94428-124">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="94428-124">Build hello solution.</span></span>
3. <span data-ttu-id="94428-125">Kullanım **NuGet** tooinstall ve ekleme **Azure Media Services .NET SDK uzantıları** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="94428-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="94428-126">Bu paketin yüklenmesiyle **Media Services .NET SDK** da yüklenir ve diğer tüm gerekli bağımlılıklar eklenir.</span><span class="sxs-lookup"><span data-stu-id="94428-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="94428-127">Hello en yeni sürümünü NuGet yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="94428-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="94428-128">Daha fazla bilgi ve yükleme yönergeleri için bkz: [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="94428-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="94428-129">Çözüm Gezgini'nde, hello hello proje adına sağ tıklayın ve Manage NuGet paketleri seçin.</span><span class="sxs-lookup"><span data-stu-id="94428-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="94428-130">Merhaba NuGet paketlerini Yönet iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="94428-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="94428-131">Hello Çevrimiçi Galerisi, Azure MediaServices uzantıları için arama Azure Media Services .NET SDK uzantıları seçin ve ardından hello yükle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="94428-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="94428-132">Merhaba proje değiştirilir ve toohello Media Services .NET SDK uzantıları, Media Services .NET SDK başvuruyor ve diğer bağımlı derlemelerden eklenir.</span><span class="sxs-lookup"><span data-stu-id="94428-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="94428-133">toopromote temizleyici bir geliştirme ortamı NuGet paketi geri yüklemeyi etkinleştirme göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="94428-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="94428-134">Daha fazla bilgi için bkz: [NuGet paket geri yükleme "](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="94428-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="94428-135">Bir başvuru çok ekleyin**System.Configuration** derleme.</span><span class="sxs-lookup"><span data-stu-id="94428-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="94428-136">Bu derleme hello System.Configuration içerir. **ConfigurationManager** sınıf kullanılan tooaccess yapılandırma dosyaları (örneğin, App.config).</span><span class="sxs-lookup"><span data-stu-id="94428-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="94428-137">Merhaba başvuruları Yönet iletişim kutusunu kullanarak tooadd başvuruları hello Çözüm Gezgini'nde hello proje adına sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="94428-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="94428-138">Ardından, Ekle ve başvurular seçin.</span><span class="sxs-lookup"><span data-stu-id="94428-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="94428-139">Merhaba başvuruları Yönet iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="94428-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="94428-140">.NET framework derlemeleri altındaki bulmak ve hello System.Configuration derleme seçin ve Tamam'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="94428-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="94428-141">Merhaba App.config dosyasını açın ve eklemek bir *appSettings* bölüm toohello dosyası.</span><span class="sxs-lookup"><span data-stu-id="94428-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="94428-142">Gerekli tooconnect toohello Media Services API olan hello değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="94428-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="94428-143">Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="94428-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="94428-144">Kullanıyorsanız [kullanıcı kimlik doğrulaması](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) yapılandırma dosyanızı büyük olasılıkla, Azure AD Kiracı etki alanı değerlere sahip ve AMS REST API uç noktası hello.</span><span class="sxs-lookup"><span data-stu-id="94428-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="94428-145">Hello Azure Media Services belgelerine çoğu kod örnekleri kümesi, kimlik doğrulama tooconnect toohello AMS API kullanıcı (etkileşimli) türünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="94428-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="94428-146">Bu kimlik doğrulama yöntemini de yönetim veya yerel uygulamalar izleme için çalışır: mobil uygulamaları, Windows uygulamaları ve konsol uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="94428-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="94428-147">Bu kimlik doğrulama yöntemi, sunucu, web Hizmetleri, uygulamaları API'leri türü için uygun değil.</span><span class="sxs-lookup"><span data-stu-id="94428-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="94428-148">Daha fazla bilgi için bkz: [Azure AD kimlik doğrulaması ile erişim hello AMS API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="94428-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="94428-149">Merhaba var olanın üzerine yaz **kullanarak** koddan hello hello Program.cs dosyasının hello başında deyimleri.</span><span class="sxs-lookup"><span data-stu-id="94428-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="94428-150">Bu noktada, Media Services uygulama geliştirme hazır toostart var.</span><span class="sxs-lookup"><span data-stu-id="94428-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="94428-151">Örnek</span><span class="sxs-lookup"><span data-stu-id="94428-151">Example</span></span>

<span data-ttu-id="94428-152">Burada, toohello AMS API bağlanır ve tüm kullanılabilir medya işlemcileri listeler küçük bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="94428-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="94428-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="94428-153">Next steps</span></span>

<span data-ttu-id="94428-154">Şimdi [toohello AMS API bağlanabilir](media-services-use-aad-auth-to-access-ams-api.md) ve başlangıç [geliştirme](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="94428-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="94428-155">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="94428-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="94428-156">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="94428-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

