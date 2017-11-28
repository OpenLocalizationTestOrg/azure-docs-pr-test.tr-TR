---
title: "aaaAzure WCF geçiş karma şirket içi/bulut uygulama (.NET) | Microsoft Docs"
description: "Bilgi nasıl Azure WCF geçiş kullanarak toocreate bir .NET şirket içi/bulut karma uygulama."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="9ae1e-103">Azure WCF Geçişini kullanan karma .NET şirket içi uygulama/bulut uygulaması</span><span class="sxs-lookup"><span data-stu-id="9ae1e-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="9ae1e-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="9ae1e-104">Introduction</span></span>

<span data-ttu-id="9ae1e-105">Bu makalede, Microsoft Azure ve Visual Studio ile uygulama toobuild karma bir bulut nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="9ae1e-106">Başlangıç Öğreticisi Azure kullanma konusunda deneyim sahibi varsayar.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="9ae1e-107">Az 30 dakika içerisinde birden çok Azure kaynağını kullanan bir uygulama ve hello bulutta çalışan sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="9ae1e-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-108">You will learn:</span></span>

* <span data-ttu-id="9ae1e-109">Nasıl toocreate veya bir web çözümünde var olan bir web hizmetini uyarlama.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="9ae1e-110">Nasıl bir Azure uygulaması ve web hizmeti arasında toouse hello Azure WCF geçiş hizmeti tooshare verileri başka bir yerde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="9ae1e-111">Azure Relay geçişinin karma çözümlere yönelik yardımları</span><span class="sxs-lookup"><span data-stu-id="9ae1e-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="9ae1e-112">İşletme Çözümleri tootackle yeni yazılmış özel kod ve benzersiz iş gereksinimlerine ve mevcut işlevselliğini çözümleri ve zaten kullanımdadır sistemler tarafından sağlanan birlikte genellikle oluşur.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="9ae1e-113">Çözüm mimarları ölçek gereksinimlerine ve işletim maliyetlerini daha kolay işlenmesi için toouse hello bulut başlıyor.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="9ae1e-114">Bunu yaparken, bunların çözümleri için yapı taşları hello Kurumsal güvenlik duvarı içinde ve dışında kolay olduğundan tooleverage istediğiniz var olan hizmet varlıklarının hello bulut çözümü tarafından erişim için ulaşmak bulun.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="9ae1e-115">Birçok dahili Hizmet derlenmez veya bunlar kolayca hello kurumsal ağ ucunda kullanıma sunulabilecek şekilde şekilde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="9ae1e-116">[Azure geçiş](https://azure.microsoft.com/services/service-bus/) için tasarlanmış var olan Windows Communication Foundation (WCF) web hizmetlerini almaya kullanım örneği hello ve Hizmetleri gerek kalmadan hello Kurumsal çevre dışında bulunan güvenli bir şekilde erişilebilir toosolutions olanlar yapma toohello kurumsal ağ altyapısına müdahale eden değişiklikler.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="9ae1e-117">Bu tür geçiş hizmetleri hala kendi mevcut ortamın içinde barındırılan, ancak gelen oturumları ve istekleri toohello geçiş bulutta barındırılan hizmeti için dinleme temsilci.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="9ae1e-118">Ayrıca, Azure Geçişi [Paylaşılan Erişim İmzası (SAS)](../service-bus-messaging/service-bus-sas.md) kimlik doğrulaması kullanarak bu hizmetleri yetkilendirilmemiş erişime karşı korur.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="9ae1e-119">Çözüm senaryosu</span><span class="sxs-lookup"><span data-stu-id="9ae1e-119">Solution scenario</span></span>
<span data-ttu-id="9ae1e-120">Bu öğreticide, hello ürün stoğu sayfasındaki ürünlerin listesini toosee sağlayan bir ASP.NET Web sitesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="9ae1e-121">Başlangıç Öğreticisi, varolan bir şirket içi sistemde ürün bilgilerine sahip ve bu sisteme Azure geçiş tooreach kullanır varsayar.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="9ae1e-122">Bu çözüm, basit bir konsol uygulamasında çalışan web hizmeti ile benzetilir ve bir bellek içi ürün kümesi ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="9ae1e-123">Siz mümkün toorun bu konsol uygulamasını kendi bilgisayarınızda yüklü olması ve hello web rolünü Azure'a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="9ae1e-124">Bilgisayarınızı, bilgisayarınız en az bir güvenlik duvarı ve ağ adresi çevirisi (NAT) katmanı arkasında yer alacağı olsa bile bunu yaparak, nasıl hello Azure veri merkezinde çalışan hello web rolü gerçekten bilgisayarınıza çağrı gönderebildiğini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="9ae1e-125">Merhaba geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ae1e-125">Set up hello development environment</span></span>

<span data-ttu-id="9ae1e-126">Azure uygulamalarını geliştirmeye başlamadan önce hello Araçları'nı indirmek ve geliştirme ortamınızı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="9ae1e-127">.NET için SDK hello Hello Azure SDK'sını yüklemek [indirmeler sayfası](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9ae1e-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9ae1e-128">Merhaba, **.NET** sütun hello sürümünü [Visual Studio](http://www.visualstudio.com) kullanmakta olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="9ae1e-129">Bu öğretici kullanımda Visual Studio 2015 Hello adımlar, ancak bunlar da Visual Studio 2017 ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="9ae1e-130">Toorun istenir veya hello yükleyici kaydettiğinizde tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="9ae1e-131">Merhaba, **Web Platformu yükleyicisi**,'ı tıklatın **yüklemek** ve hello yükleme işlemine devam edin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="9ae1e-132">Merhaba yüklemesi tamamlandıktan sonra her şeyi olacaktır gerekli toostart toodevelop hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="9ae1e-133">Merhaba SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="9ae1e-134">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-134">Create a namespace</span></span>

<span data-ttu-id="9ae1e-135">Merhaba Azure geçiş özelliklerinde toobegin kullanarak, öncelikle bir hizmet ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="9ae1e-136">Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="9ae1e-137">Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="9ae1e-138">Şirket içi sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-138">Create an on-premises server</span></span>

<span data-ttu-id="9ae1e-139">Öncelikle, bir (sahte) şirket içi ürün kataloğu sistemi derleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="9ae1e-140">Bu, oldukça basit olacaktır; Bu bir toointegrate çalıştığınız tüm hizmet yüzeyini içeren gerçek şirket içi ürün kataloğu sistemini temsil eden olarak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="9ae1e-141">Bu proje bir Visual Studio konsol uygulamasıdır ve kullandığı hello [Azure Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus kitaplıkları ile yapılandırma ayarları.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="9ae1e-142">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-142">Create hello project</span></span>

1. <span data-ttu-id="9ae1e-143">Yönetici ayrıcalıklarını kullanarak Microsoft Visual Studio'yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="9ae1e-144">toodo, bu nedenle, hello Visual Studio program simgesine sağ tıklayın ve ardından **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="9ae1e-145">Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="9ae1e-146">**Yüklü Şablonlar**'daki **Visual C#** bölümünde **Konsol Uygulaması (.NET Framework)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="9ae1e-147">Merhaba, **adı** kutusu, tür hello adı **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="9ae1e-148">Tıklatın **Tamam** toocreate hello **ProductsServer** projesi.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="9ae1e-149">Visual Studio hello NuGet paketi yöneticisini zaten yüklediyseniz, toohello bir sonraki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="9ae1e-150">Yükleme yapmadıysanız [NuGet][NuGet] bölümünü ziyaret edin ve [NuGet'i Yükle](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="9ae1e-151">Merhaba istemleri tooinstall hello NuGet Paket Yöneticisi izleyin ve ardından Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="9ae1e-152">Çözüm Gezgini'nde hello sağ **ProductsServer** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="9ae1e-153">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="9ae1e-154">Select hello **WindowsAzure.ServiceBus** paket.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="9ae1e-155">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="9ae1e-156">Bu hello gerekli istemci derlemelerine başvuru oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="9ae1e-157">Ürün sözleşmeniz için yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-157">Add a new class for your product contract.</span></span> <span data-ttu-id="9ae1e-158">Çözüm Gezgini'nde hello sağ **ProductsServer** proje ve tıklatın **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="9ae1e-159">Merhaba, **adı** kutusu, tür hello adı **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="9ae1e-160">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-160">Then click **Add**.</span></span>
10. <span data-ttu-id="9ae1e-161">İçinde **ProductsContract.cs**, hello hello hizmeti için hello sözleşmesini tanımlayan kodu aşağıdaki ile Merhaba ad alanı tanımını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. <span data-ttu-id="9ae1e-162">Program.cs içinde hello ad alanı tanımını hello hello Profil Hizmeti ile Merhaba konağını ekler kodu aşağıdaki ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="9ae1e-163">Çözüm Gezgini'nde hello çift tıklayarak **App.config** tooopen dosya hello Visual Studio düzenleyicisinde içinde.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="9ae1e-164">Merhaba hello sonundaki `<system.ServiceModel>` öğesi (ancak hala içinde `<system.ServiceModel>`), aşağıdaki XML kodunu hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="9ae1e-165">Emin tooreplace olması *yourServiceNamespace* ad alanınızın hello adla ve *yourKey* , alınan önceki hello portalından hello SAS anahtarıyla:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. <span data-ttu-id="9ae1e-166">Merhaba, App.config yine de `<appSettings>` öğesi, hello Portalı'ndan daha önce edindiğiniz hello bağlantı dizesiyle değiştirin hello bağlantı dizesi değeri.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="9ae1e-167">Tuşuna **Ctrl + Shift + B** veya hello **yapı** menüsünde tıklatın **yapı çözümü** toobuild hello uygulama ve hello çalışmanızın o ana kadarki doğruluğundan.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="9ae1e-168">ASP.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-168">Create an ASP.NET application</span></span>

<span data-ttu-id="9ae1e-169">Bu bölümde, ürün hizmetinizden alınan verileri görüntüleyen basit bir ASP.NET uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="9ae1e-170">Başlangıç projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-170">Create hello project</span></span>

1. <span data-ttu-id="9ae1e-171">Visual Studio'nun yönetici ayrıcalıklarıyla çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="9ae1e-172">Visual Studio'da, hello **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="9ae1e-173">**Yüklü Şablonlar**'daki **Visual C#** bölümünde bulunan **ASP.NET Web Uygulaması (.NET Framework)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="9ae1e-174">Ad hello proje **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="9ae1e-175">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="9ae1e-176">Merhaba gelen **ASP.NET şablonları** hello listesinde **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **MVC**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="9ae1e-177">Merhaba tıklatın **kimlik doğrulamayı Değiştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="9ae1e-178">Merhaba, **kimlik doğrulamayı Değiştir** iletişim kutusunda **doğrulaması yok** seçilir ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="9ae1e-179">Bu öğreticide, kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="9ae1e-180">Merhaba edilene **yeni ASP.NET Web uygulaması** iletişim kutusunda, tıklatın **Tamam** toocreate hello MVC uygulama.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="9ae1e-181">Şimdi yeni bir web uygulaması için Azure kaynaklarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="9ae1e-182">Merhaba Hello adımları [tooAzure bu makalenin yayımlama](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9ae1e-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="9ae1e-183">Ardından, toothis öğretici dönün ve toohello sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="9ae1e-184">Çözüm Gezgini'nde **Modeller**'e sağ tıklayıp **Ekle**’ye ve ardından **Sınıf**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="9ae1e-185">Merhaba, **adı** kutusu, tür hello adı **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="9ae1e-186">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="9ae1e-187">Merhaba web uygulamasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="9ae1e-187">Modify hello web application</span></span>

1. <span data-ttu-id="9ae1e-188">Merhaba Product.cs dosyasında Visual Studio, hello var olan ad alanı tanımını koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. <span data-ttu-id="9ae1e-189">Çözüm Gezgini'nde hello genişletin **denetleyicileri** klasörünü hello çift tıklatın **HomeController.cs** tooopen dosya Visual Studio içinde.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="9ae1e-190">İçinde **HomeController.cs**, hello var olan ad alanı tanımını koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="9ae1e-191">Çözüm Gezgini'nde hello görünümler/paylaşılan klasörünü genişletin ve ardından **_Layout.cshtml** tooopen onu hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="9ae1e-192">Tüm oluşumlarını değiştirme **My ASP.NET Application** çok**LITWARE's Products**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="9ae1e-193">Merhaba kaldırmak **giriş**, **hakkında**, ve **kişi** bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="9ae1e-194">Aşağıdaki örneğine hello hello vurgulanmış kodu silin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="9ae1e-195">Çözüm Gezgini'nde hello görünümler/giriş klasörünü genişletin ve ardından **Index.cshtml** tooopen onu hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="9ae1e-196">Merhaba dosyanın tüm içeriğini Hello koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-196">Replace hello entire contents of hello file with hello following code.</span></span>

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. <span data-ttu-id="9ae1e-197">tooverify hello doğruluğu çalışmanızın o ana kadarki basabilirsiniz **Ctrl + Shift + B** toobuild hello projesi.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="9ae1e-198">Merhaba uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-198">Run hello app locally</span></span>

<span data-ttu-id="9ae1e-199">Çalıştığını hello uygulama tooverify çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="9ae1e-200">Emin **ProductsPortal** hello etkin projesidir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="9ae1e-201">Merhaba Çözüm Gezgini'nde proje adına sağ tıklayıp **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="9ae1e-202">Visual Studio'da **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="9ae1e-203">Uygulamanız, bir tarayıcıda çalışıyor olarak görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="9ae1e-204">Merhaba parçaları bir araya getirme</span><span class="sxs-lookup"><span data-stu-id="9ae1e-204">Put hello pieces together</span></span>

<span data-ttu-id="9ae1e-205">Merhaba sonraki hello şirket içi ürünlerin sunucusu hello ASP.NET uygulaması ile toohook adımdır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="9ae1e-206">Visual Studio'da yeniden Aç'u hello zaten açık değilse, **ProductsPortal** hello oluşturulan proje [ASP.NET uygulaması oluşturma](#create-an-aspnet-application) bölümü.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="9ae1e-207">Merhaba "Bir şirket içi sunucu oluşturma" bölümünde, benzer toohello adımı hello NuGet paketi toohello proje başvuruları ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="9ae1e-208">Çözüm Gezgini'nde hello sağ **ProductsPortal** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="9ae1e-209">"Hizmet veri yolu" ve select hello arama **WindowsAzure.ServiceBus** öğesi.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="9ae1e-210">Ardından hello yüklemeyi tamamlamak ve bu iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="9ae1e-211">Çözüm Gezgini'nde hello sağ **ProductsPortal** proje ve ardından **Ekle**, ardından **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="9ae1e-212">Toohello gidin **ProductsContract.cs** hello dosyasından **ProductsServer** konsol projesi.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="9ae1e-213">Toohighlight ProductsContract.cs'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="9ae1e-214">Aşağı ok Hello sonraki çok tıklatın**Ekle**, ardından **bağlantı olarak Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="9ae1e-215">Şimdi hello açmak **HomeController.cs** dosya hello Visual Studio düzenleyicisinde ve hello ad alanı tanımını koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="9ae1e-216">Emin tooreplace olması *yourServiceNamespace* hizmet ad alanınızın hello adla ve *yourKey* da SAS anahtarınızla.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="9ae1e-217">Bu hello hello çağrı sonucunu döndürerek hello istemci toocall hello şirket içi hizmet, olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="9ae1e-218">Çözüm Gezgini'nde hello sağ **ProductsPortal** çözüm (yapma emin tooright tıklatma hello çözüm, değil hello Proje).</span><span class="sxs-lookup"><span data-stu-id="9ae1e-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="9ae1e-219">**Ekle**'ye ve ardından **Var Olan Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="9ae1e-220">Toohello gidin **ProductsServer** proje ve ardından hello **ProductsServer.csproj** çözüm dosya tooadd onu.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="9ae1e-221">**ProductsServer** sipariş toodisplay hello verilerde çalıştırmalıdır **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="9ae1e-222">Çözüm Gezgini'nde hello sağ **ProductsPortal** çözümü ve tıklatın **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="9ae1e-223">Merhaba **özellik sayfaları** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="9ae1e-224">Sol tarafında hello üzerinde tıklatın **başlangıç projesi**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="9ae1e-225">Merhaba sağ tarafta tıklatın **birden fazla başlangıç projesi**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="9ae1e-226">Emin **ProductsServer** ve **ProductsPortal** , o sırada göründüğünden **Başlat** ikisi için de hello eylem olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="9ae1e-227">Merhaba yine de **özellikleri** iletişim kutusu, tıklatın **proje bağımlılıkları** yan sol hello üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="9ae1e-228">Merhaba, **projeleri** tıklatın **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="9ae1e-229">**ProductsPortal**'ın seçilmediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="9ae1e-230">Merhaba, **projeleri** tıklatın **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="9ae1e-231">**ProductsServer** projesinin seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="9ae1e-232">Tıklatın **Tamam** hello içinde **özellik sayfaları** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="9ae1e-233">Merhaba projeyi yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-233">Run hello project locally</span></span>

<span data-ttu-id="9ae1e-234">Visual Studio'da yerel olarak tootest Merhaba uygulaması basın **F5**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="9ae1e-235">Merhaba şirket içi sunucu (**ProductsServer**) ilk başlayın, ardından hello **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="9ae1e-236">Bu süre, hello ürün stoğunun hello ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="9ae1e-237">Tuşuna **yenileme** hello üzerinde **ProductsPortal** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="9ae1e-238">Merhaba sayfayı yenileyin, her bir ileti görüntüler hello sunucu uygulama göreceğiniz zaman `GetProducts()` gelen **ProductsServer** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="9ae1e-239">Her iki uygulamayı toohello sonraki adıma devam etmeden önce kapatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="9ae1e-240">Merhaba ProductsPortal proje tooan Azure web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="9ae1e-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="9ae1e-241">Merhaba sonraki adımdır toorepublish hello Azure Web uygulaması **ProductsPortal** ön uç.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="9ae1e-242">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-242">Do hello following:</span></span>

1. <span data-ttu-id="9ae1e-243">Çözüm Gezgini'nde hello sağ **ProductsPortal** proje öğesini tıklatıp **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="9ae1e-244">Ardından **Yayımla** hello üzerinde **Yayımla** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9ae1e-245">Bir hata iletisi hello tarayıcı penceresinde hello zaman görebilirsiniz **ProductsPortal** web projesi hello dağıtım sonrasında otomatik olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="9ae1e-246">Bu beklenen bir durumdur ve oluşur hello **ProductsServer** uygulaması henüz çalışmadığından.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="9ae1e-247">Merhaba URL hello sonraki adımda ihtiyaç duyacağınız kopyalama hello hello URL'sini web uygulaması dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="9ae1e-248">Visual Studio'da hello Azure App Service etkinliği penceresinden de bu URL'yi elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="9ae1e-249">Uygulama çalıştıran hello tarayıcı penceresini toostop hello kapatın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="9ae1e-250">ProductsPortal'ı web uygulaması olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="9ae1e-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="9ae1e-251">Merhaba bulutta çalışan hello uygulama önce emin olmanız gerekir **ProductsPortal** gelen Visual Studio'dan bir web uygulaması olarak başlatılır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="9ae1e-252">Visual Studio'da hello sağ **ProductsPortal** proje ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="9ae1e-253">Merhaba sol sütunda, tıklatın **Web**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="9ae1e-254">Merhaba, **eylemi Başlat** bölümünde, hello tıklatın **Start URL** düğmesine tıklayın ve hello metin kutusuna, daha önce dağıttınız web uygulamanız için; hello URL'sini girin örneğin, `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="9ae1e-255">Merhaba gelen **dosya** Visual Studio'da menüsünü **Tümünü Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="9ae1e-256">Merhaba yapı menüden Visual Studio'da, **çözümü yeniden derle**.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="9ae1e-257">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9ae1e-257">Run hello application</span></span>

1. <span data-ttu-id="9ae1e-258">F5 toobuild tuşuna basın ve hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="9ae1e-259">Merhaba şirket içi sunucu (Merhaba **ProductsServer** konsol uygulaması) ilk başlayın, ardından hello **ProductsPortal** uygulaması, bir tarayıcı penceresinde başlamalıdır, aşağıdaki ekran hello gösterildiği gibi görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="9ae1e-260">Yeniden, hello ürün stoğunun hello ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini ve bu verileri hello web uygulamasında gösterdiğini dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="9ae1e-261">Merhaba URL toomake emin denetleyin, **ProductsPortal** hello bulut Azure web uygulaması olarak çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="9ae1e-262">Merhaba **ProductsServer** çalışıp çalışmadığını ve konsol uygulaması olmalıdır tooserve hello veri toohello **ProductsPortal** uygulama.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="9ae1e-263">Merhaba tarayıcı bir hata görüntülerse birkaç saniye daha bekleyin **ProductsServer** tooload ve aşağıdaki görüntü hello iletisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="9ae1e-264">Tuşuna basarak **yenileme** hello tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="9ae1e-265">Geri hello tarayıcıda basın **yenileme** hello üzerinde **ProductsPortal** sayfası.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="9ae1e-266">Merhaba sayfayı yenileyin, her bir ileti görüntüler hello sunucu uygulama göreceğiniz zaman `GetProducts()` gelen **ProductsServer** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="9ae1e-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="9ae1e-267">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ae1e-267">Next steps</span></span>

<span data-ttu-id="9ae1e-268">Azure geçişi hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9ae1e-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="9ae1e-269">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="9ae1e-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="9ae1e-270">Toouse nasıl geçiş</span><span class="sxs-lookup"><span data-stu-id="9ae1e-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png
