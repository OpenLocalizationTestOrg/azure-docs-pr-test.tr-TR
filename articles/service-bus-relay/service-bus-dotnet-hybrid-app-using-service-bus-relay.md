---
title: "Azure WCF Geçişi karma şirket içi uygulama/bulut uygulaması (.NET) | Microsoft Belgeleri"
description: "Azure WCF Geçişini kullanarak karma .NET şirket içi uygulama/bulut uygulaması oluşturmayı öğrenin."
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
ms.openlocfilehash: 366922a083b9d18ef50e04eb8b459d2725315e1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="9db65-103">Azure WCF Geçişini kullanan karma .NET şirket içi uygulama/bulut uygulaması</span><span class="sxs-lookup"><span data-stu-id="9db65-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="9db65-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="9db65-104">Introduction</span></span>

<span data-ttu-id="9db65-105">Bu makale, Microsoft Azure ve Visual Studio ile nasıl karma bulut uygulaması derleyeceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="9db65-105">This article shows how to build a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="9db65-106">Öğretici Azure kullanımına ilişkin deneyim sahibi olmadığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="9db65-106">The tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="9db65-107">30 dakikadan kısa sürede, birden çok Azure kaynağını kullanan ve bulutta çalışan bir uygulamaya sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in the cloud.</span></span>

<span data-ttu-id="9db65-108">Şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9db65-108">You will learn:</span></span>

* <span data-ttu-id="9db65-109">Bir web çözümünde kullanılması amacıyla web hizmeti oluşturma veya var olan bir web hizmetini uyarlama.</span><span class="sxs-lookup"><span data-stu-id="9db65-109">How to create or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="9db65-110">Azure uygulaması ve başka bir yerde barındırılan web hizmeti arasında veri paylaşımı için Azure WCF Geçişi hizmetini kullanma.</span><span class="sxs-lookup"><span data-stu-id="9db65-110">How to use the Azure WCF Relay service to share data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="9db65-111">Azure Relay geçişinin karma çözümlere yönelik yardımları</span><span class="sxs-lookup"><span data-stu-id="9db65-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="9db65-112">İşletme çözümleri, genel olarak yeni ve benzersiz işletme gereksinimlerini karşılamak için yazılan özel bir kodun ve kullanılan çözüm ve sistemler tarafından sağlanan var olan işlevselliğin bir birleşiminden oluşur.</span><span class="sxs-lookup"><span data-stu-id="9db65-112">Business solutions are typically composed of a combination of custom code written to tackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="9db65-113">Çözüm mimarları, ölçek gereksinimlerini daha kolay bir şekilde karşılamak ve işlem maliyetlerini düşürmek için bulutu kullanmaya başlıyor.</span><span class="sxs-lookup"><span data-stu-id="9db65-113">Solution architects are starting to use the cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="9db65-114">Bunu yaparken de çözümleri için yapı taşı olarak kullanmak istedikleri var olan hizmet varlıklarının kurumsal güvenlik duvarının içinde ve bulut çözümüyle kolayca erişilemeyecek konumda olduklarını fark ettiler.</span><span class="sxs-lookup"><span data-stu-id="9db65-114">In doing so, they find that existing service assets they'd like to leverage as building blocks for their solutions are inside the corporate firewall and out of easy reach for access by the cloud solution.</span></span> <span data-ttu-id="9db65-115">Birçok dahili hizmet, kurumsal ağ ucunda kolayca kullanıma sunulabilecek şekilde derlenmez veya barındırılmaz.</span><span class="sxs-lookup"><span data-stu-id="9db65-115">Many internal services are not built or hosted in a way that they can be easily exposed at the corporate network edge.</span></span>

<span data-ttu-id="9db65-116">[Azure Geçişi](https://azure.microsoft.com/services/service-bus/) ise mevcut Windows Communication Foundation (WCF) web hizmetlerinin alınarak kurumsal ağ altyapısını bozan değişikliklere gerek kalmadan kurumsal çevre dışında bulunan çözümlere güvenli bir şekilde erişmesini sağlamaya yönelik kullanım senaryosu için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9db65-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for the use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible to solutions that reside outside the corporate perimeter without requiring intrusive changes to the corporate network infrastructure.</span></span> <span data-ttu-id="9db65-117">Bu tür geçişi hizmetleri, var olan ortamlarında barındırılmaya devam eder ancak bu hizmetler gelen oturumları ve istekleri bulutta barındırılan geçiş hizmetine devreder.</span><span class="sxs-lookup"><span data-stu-id="9db65-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests to the cloud-hosted relay service.</span></span> <span data-ttu-id="9db65-118">Ayrıca, Azure Geçişi [Paylaşılan Erişim İmzası (SAS)](../service-bus-messaging/service-bus-sas.md) kimlik doğrulaması kullanarak bu hizmetleri yetkilendirilmemiş erişime karşı korur.</span><span class="sxs-lookup"><span data-stu-id="9db65-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="9db65-119">Çözüm senaryosu</span><span class="sxs-lookup"><span data-stu-id="9db65-119">Solution scenario</span></span>
<span data-ttu-id="9db65-120">Bu öğreticide, ürün stoğu sayfasındaki ürünlerin listesini görmenize olanak sağlayan bir ASP.NET web sitesi oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-120">In this tutorial, you will create an ASP.NET website that enables you to see a list of products on the product inventory page.</span></span>

![][0]

<span data-ttu-id="9db65-121">Öğretici, var olan şirket içi sistemde ürün bilgilerine sahip olduğunuzu varsayar ve bu sisteme erişmek için Azure Geçişini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9db65-121">The tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay to reach into that system.</span></span> <span data-ttu-id="9db65-122">Bu çözüm, basit bir konsol uygulamasında çalışan web hizmeti ile benzetilir ve bir bellek içi ürün kümesi ile desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9db65-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="9db65-123">Bu konsol uygulamasını kendi bilgisayarınızda çalıştırabilirsiniz ve web rolünü Azure'a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9db65-123">You will be able to run this console application on your own computer and deploy the web role into Azure.</span></span> <span data-ttu-id="9db65-124">Bu özellik sayesinde, bilgisayarınız en az bir güvenlik duvarının arkasında ve bir ağ adresi çevirisi (NAT) katmanında yer alsa bile Azure veri merkezinde çalışan web rolünün gerçekten bilgisayarınıza çağrı gönderebildiğini göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9db65-124">By doing so, you will see how the web role running in the Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="9db65-125">Geliştirme ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="9db65-125">Set up the development environment</span></span>

<span data-ttu-id="9db65-126">Azure uygulamalarını geliştirmeye başlamadan önce, araçları indirip geliştirme ortamınızı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="9db65-126">Before you can begin developing Azure applications, download the tools and set up your development environment:</span></span>

1. <span data-ttu-id="9db65-127">SDK [indirme sayfasından](https://azure.microsoft.com/downloads/) .NET için Azure SDK'sını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-127">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="9db65-128">**.NET** sütununda, kullandığınız [Visual Studio](http://www.visualstudio.com) sürümüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-128">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="9db65-129">Bu öğreticideki adımlar Visual Studio 2015 kullanır, ancak Visual Studio 2017 ile de çalışır.</span><span class="sxs-lookup"><span data-stu-id="9db65-129">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="9db65-130">Yükleyiciyi çalıştırmanız veya kaydetmeniz istendiğinde **Çalıştır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-130">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="9db65-131">**Web Platformu Yükleyicisi**'nde **Yükle**'ye tıklayın ve kuruluma devam edin.</span><span class="sxs-lookup"><span data-stu-id="9db65-131">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="9db65-132">Kurulum tamamlandığında uygulamayı geliştirmeye başlamak için gereken her şeye sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-132">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="9db65-133">SDK, Visual Studio'da Azure uygulamalarını kolayca geliştirmenize olanak sağlayan araçları içerir.</span><span class="sxs-lookup"><span data-stu-id="9db65-133">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="9db65-134">Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9db65-134">Create a namespace</span></span>

<span data-ttu-id="9db65-135">Azure'da geçiş özelliklerini kullanmaya başlamak için öncelikle bir hizmet ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9db65-135">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="9db65-136">Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.</span><span class="sxs-lookup"><span data-stu-id="9db65-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="9db65-137">[Buradaki yönergeleri](relay-create-namespace-portal.md) izleyerek bir Geçiş ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9db65-137">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="9db65-138">Şirket içi sunucu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9db65-138">Create an on-premises server</span></span>

<span data-ttu-id="9db65-139">Öncelikle, bir (sahte) şirket içi ürün kataloğu sistemi derleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="9db65-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="9db65-140">Bu oldukça kolay bir işlemdir. Bu çalışmanın, entegre etmeye çalıştığımız tüm hizmet yüzeyini içeren gerçek bir şirket içi ürün kataloğu sistemini temsil ettiğini düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9db65-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying to integrate.</span></span>

<span data-ttu-id="9db65-141">Bu proje bir Visual Studio konsol uygulamasıdır ve Service Bus kitaplıkları ile yapılandırma ayarlarını dahil etmek için [Azure Service Bus NuGet paketini](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) kullanır.</span><span class="sxs-lookup"><span data-stu-id="9db65-141">This project is a Visual Studio console application, and uses the [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) to include the Service Bus libraries and configuration settings.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="9db65-142">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="9db65-142">Create the project</span></span>

1. <span data-ttu-id="9db65-143">Yönetici ayrıcalıklarını kullanarak Microsoft Visual Studio'yu başlatın.</span><span class="sxs-lookup"><span data-stu-id="9db65-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="9db65-144">Bunu yapmak için Visual Studio program simgesine sağ tıklayıp **Yönetici olarak çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-144">To do so, right-click the Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="9db65-145">Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-145">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="9db65-146">**Yüklü Şablonlar**'daki **Visual C#** bölümünde **Konsol Uygulaması (.NET Framework)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="9db65-147">**Ad** kutusuna **ProductsServer** adını yazın:</span><span class="sxs-lookup"><span data-stu-id="9db65-147">In the **Name** box, type the name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="9db65-148">**ProductsServer** projesini oluşturmak için **Tamam** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-148">Click **OK** to create the **ProductsServer** project.</span></span>
5. <span data-ttu-id="9db65-149">Visual Studio'ya yönelik NuGet paketi yöneticisini zaten yüklediyseniz bir sonraki adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-149">If you have already installed the NuGet package manager for Visual Studio, skip to the next step.</span></span> <span data-ttu-id="9db65-150">Yükleme yapmadıysanız [NuGet][NuGet] bölümünü ziyaret edin ve [NuGet'i Yükle](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c)'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="9db65-151">NuGet paketi yöneticisini yüklemek için gereken istemleri gerçekleştirin ve Visual Studio'yu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9db65-151">Follow the prompts to install the NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="9db65-152">Çözüm Gezgini'nde **ProductsServer** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-152">In Solution Explorer, right-click the **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="9db65-153">**Gözat** sekmesine tıklayıp `Microsoft Azure Service Bus` için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="9db65-153">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="9db65-154">**WindowsAzure.ServiceBus** paketini seçin.</span><span class="sxs-lookup"><span data-stu-id="9db65-154">Select the **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="9db65-155">**Yükle**'ye tıklayın ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="9db65-155">Click **Install**, and accept the terms of use.</span></span>

   ![][13]

   <span data-ttu-id="9db65-156">Artık gerekli istemci derlemelerine başvuru oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-156">Note that the required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="9db65-157">Ürün sözleşmeniz için yeni bir sınıf ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-157">Add a new class for your product contract.</span></span> <span data-ttu-id="9db65-158">Çözüm Gezgini'nde **ProductsServer** projesine sağ tıklayın ve ardından **Ekle** ve **Sınıf** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-158">In Solution Explorer, right-click the **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="9db65-159">**Ad** kutusuna **ProductsContract.cs** adını yazın:</span><span class="sxs-lookup"><span data-stu-id="9db65-159">In the **Name** box, type the name **ProductsContract.cs**.</span></span> <span data-ttu-id="9db65-160">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-160">Then click **Add**.</span></span>
10. <span data-ttu-id="9db65-161">**ProductsContract.cs** sınıfında, ad alanı tanımını hizmet sözleşmesini tanımlayan şu kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9db65-161">In **ProductsContract.cs**, replace the namespace definition with the following code, which defines the contract for the service.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define the data contract for the service
        [DataContract]
        // Declare the serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define the service contract.
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
11. <span data-ttu-id="9db65-162">Program.cs sınıfında içinde, ad alanı tanımını profil hizmetini ve bu hizmete yönelik ana bilgisayarı ekleyen şu kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9db65-162">In Program.cs, replace the namespace definition with the following code, which adds the profile service and the host for it.</span></span>

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement the IProducts interface.
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

            // Display a message in the service console application
            // when the list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define the Main() function in the service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER to close");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. <span data-ttu-id="9db65-163">Çözüm Gezgini'nde, **App.config** dosyasına çift tıklayarak dosyayı Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="9db65-163">In Solution Explorer, double-click the **App.config** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="9db65-164">`<system.ServiceModel>` öğesinin en altına (yine `<system.ServiceModel>` içinde kalacak şekilde) aşağıdaki XML kodunu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-164">At the bottom of the `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add the following XML code.</span></span> <span data-ttu-id="9db65-165">*yourKey* alanını daha önce portaldan aldığınız SAS anahtarıyla ve *yourServiceNamespace* alanını da ad alanı adınızla değiştirdiğinizden emin olun:</span><span class="sxs-lookup"><span data-stu-id="9db65-165">Be sure to replace *yourServiceNamespace* with the name of your namespace, and *yourKey* with the SAS key you retrieved earlier from the portal:</span></span>

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
13. <span data-ttu-id="9db65-166">App.config dosyasından çıkmadan, `<appSettings>` öğesinde bağlantı dizesi değerini portaldan daha önce edindiğiniz bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9db65-166">Still in App.config, in the `<appSettings>` element, replace the connection string value with the connection string you previously obtained from the portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="9db65-167">Uygulamayı derlemek ve o ana kadarki doğruluğunu onaylamak üzere **Derle** menüsünde **Çözümü Derle** seçeneğine tıklayın veya **Ctrl+Shift+B**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-167">Press **Ctrl+Shift+B** or from the **Build** menu, click **Build Solution** to build the application and verify the accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="9db65-168">ASP.NET uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9db65-168">Create an ASP.NET application</span></span>

<span data-ttu-id="9db65-169">Bu bölümde, ürün hizmetinizden alınan verileri görüntüleyen basit bir ASP.NET uygulaması oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="9db65-170">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="9db65-170">Create the project</span></span>

1. <span data-ttu-id="9db65-171">Visual Studio'nun yönetici ayrıcalıklarıyla çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="9db65-172">Visual Studio'da, **Dosya** menüsündeki **Yeni** seçeneğine ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-172">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="9db65-173">**Yüklü Şablonlar**'daki **Visual C#** bölümünde bulunan **ASP.NET Web Uygulaması (.NET Framework)** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="9db65-174">Projeyi **ProductsPortal** olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="9db65-174">Name the project **ProductsPortal**.</span></span> <span data-ttu-id="9db65-175">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="9db65-176">**New ASP.NET Web Uygulaması** iletişim kutusundaki **ASP.NET Şablonları** listesinde **MVC** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-176">From the **ASP.NET Templates** list in the **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="9db65-177">**Kimlik Doğrulamayı Değiştir** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-177">Click the **Change Authentication** button.</span></span> <span data-ttu-id="9db65-178">**Kimlik Doğrulamayı Değiştir** iletişim kutusunda **Kimlik Doğrulama Yok** seçeneğinin belirlendiğinden emin olun ve ardından **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-178">In the **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="9db65-179">Bu öğreticide, kullanıcının oturum açmasını gerektirmeyen bir uygulamayı dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="9db65-180">MVC uygulamasını oluşturmak üzere **New ASP.NET Web Uygulaması** iletişim kutusunda **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-180">Back in the **New ASP.NET Web Application** dialog, click **OK** to create the MVC app.</span></span>
8. <span data-ttu-id="9db65-181">Şimdi yeni bir web uygulaması için Azure kaynaklarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9db65-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="9db65-182">[Bu makalenin Azure'da Yayımlama bölümündeki](../app-service-web/app-service-web-get-started-dotnet.md) adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-182">Follow the steps in the [Publish to Azure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="9db65-183">Daha sonra, bu öğreticiye geri dönün ve sonraki adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="9db65-183">Then, return to this tutorial and proceed to the next step.</span></span>
10. <span data-ttu-id="9db65-184">Çözüm Gezgini'nde **Modeller**'e sağ tıklayıp **Ekle**’ye ve ardından **Sınıf**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="9db65-185">**Ad** kutusuna **Product.cs** yazın.</span><span class="sxs-lookup"><span data-stu-id="9db65-185">In the **Name** box, type the name **Product.cs**.</span></span> <span data-ttu-id="9db65-186">Daha sonra **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-the-web-application"></a><span data-ttu-id="9db65-187">Web uygulamasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="9db65-187">Modify the web application</span></span>

1. <span data-ttu-id="9db65-188">Visual Studio'da Product.cs dosyasındaki var olan ad alanı tanımını şu kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9db65-188">In the Product.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span>

   ```csharp
    // Declare properties for the products inventory.
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
2. <span data-ttu-id="9db65-189">Çözüm Gezgini'nde **Denetleyiciler** klasörünü genişletin ve Visual Studio'da açmak için **HomeController.cs** dosyasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-189">In Solution Explorer, expand the **Controllers** folder, then double-click the **HomeController.cs** file to open it in Visual Studio.</span></span>
3. <span data-ttu-id="9db65-190">**HomeController.cs** dosyasındaki var olan ad alanı tanımını aşağıdaki kod ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9db65-190">In **HomeController.cs**, replace the existing namespace definition with the following code.</span></span>

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of the products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. <span data-ttu-id="9db65-191">Çözüm Gezgini'nde, Görünümler/Paylaşılan klasörünü genişletin ve ardından **_Layout.cshtml** öğesine tıklayarak Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="9db65-191">In Solution Explorer, expand the Views\Shared folder, then double-click **_Layout.cshtml** to open it in the Visual Studio editor.</span></span>
5. <span data-ttu-id="9db65-192">**My ASP.NET Application** uygulamasının tüm örneklerini **LITWARE's Products** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9db65-192">Change all occurrences of **My ASP.NET Application** to **LITWARE's Products**.</span></span>
6. <span data-ttu-id="9db65-193">**Home**, **About** ve **Contact** bağlantılarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="9db65-193">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="9db65-194">Aşağıdaki örnekte vurgulanmış kodu silin.</span><span class="sxs-lookup"><span data-stu-id="9db65-194">In the following example, delete the highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="9db65-195">Çözüm Gezgini'nde, Görünümler/Giriş klasörünü genişletin ve ardından **Index.cshtml** öğesine tıklayarak Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="9db65-195">In Solution Explorer, expand the Views\Home folder, then double-click **Index.cshtml** to open it in the Visual Studio editor.</span></span> <span data-ttu-id="9db65-196">Dosyanın tüm içeriğini aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9db65-196">Replace the entire contents of the file with the following code.</span></span>

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
8. <span data-ttu-id="9db65-197">Çalışmanızın o ana kadarki doğruluğunu onaylamak üzere projeyi derlemek için **Ctrl+Shift+B**'ye basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9db65-197">To verify the accuracy of your work so far, you can press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="run-the-app-locally"></a><span data-ttu-id="9db65-198">Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9db65-198">Run the app locally</span></span>

<span data-ttu-id="9db65-199">Çalışır durumda olduğunu doğrulamak için uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9db65-199">Run the application to verify that it works.</span></span>

1. <span data-ttu-id="9db65-200">**ProductsPortal** projesinin, etkin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-200">Ensure that **ProductsPortal** is the active project.</span></span> <span data-ttu-id="9db65-201">Çözüm Gezgini'nde proje adına sağ tıklayıp **Başlangıç Projesi Olarak Ayarla**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="9db65-201">Right-click the project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="9db65-202">Visual Studio'da **F5** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="9db65-203">Uygulamanız, bir tarayıcıda çalışıyor olarak görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="9db65-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-the-pieces-together"></a><span data-ttu-id="9db65-204">Parçaları bir araya getirme</span><span class="sxs-lookup"><span data-stu-id="9db65-204">Put the pieces together</span></span>

<span data-ttu-id="9db65-205">Sonraki adım, şirket içi ürünlerin sunucusu ile ASP.NET uygulamasını birleştirmektir.</span><span class="sxs-lookup"><span data-stu-id="9db65-205">The next step is to hook up the on-premises products server with the ASP.NET application.</span></span>

1. <span data-ttu-id="9db65-206">Açık değilse [ASP.NET uygulaması oluşturma](#create-an-aspnet-application) bölümünde oluşturduğunuz **ProductsPortal** projesini Visual Studio'da yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="9db65-206">If it is not already open, in Visual Studio re-open the **ProductsPortal** project you created in the [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="9db65-207">"Şirket İçi Sunucu Oluşturma" bölümündeki adıma benzer şekilde proje başvurularına NuGet paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-207">Similar to the step in the "Create an On-Premises Server" section, add the NuGet package to the project references.</span></span> <span data-ttu-id="9db65-208">Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-208">In Solution Explorer, right-click the **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="9db65-209">"Service Bus" için arama yapın ve **WindowsAzure.ServiceBus** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9db65-209">Search for "Service Bus" and select the **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="9db65-210">Yüklemeyi tamamlayıp iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="9db65-210">Then complete the installation and close this dialog box.</span></span>
4. <span data-ttu-id="9db65-211">Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve ardından **Ekle** ve **Var Olan Öğe** seçeneklerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-211">In Solution Explorer, right-click the **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="9db65-212">**ProductsServer** konsol projesinden **ProductsContract.cs** dosyasına gidin.</span><span class="sxs-lookup"><span data-stu-id="9db65-212">Navigate to the **ProductsContract.cs** file from the **ProductsServer** console project.</span></span> <span data-ttu-id="9db65-213">ProductsContract.cs dosyasına tıklayarak dosyayı vurgulayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-213">Click to highlight ProductsContract.cs.</span></span> <span data-ttu-id="9db65-214">**Ekle** seçeneğinin yanındaki aşağı oka ve ardından **Bağlantı Olarak Ekle** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-214">Click the down arrow next to **Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="9db65-215">Şimdi, Visual Studio düzenleyicisinde **HomeController.cs** dosyasını açın ve ad alanı tanımını aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9db65-215">Now open the **HomeController.cs** file in the Visual Studio editor and replace the namespace definition with the following code.</span></span> <span data-ttu-id="9db65-216">*yourServiceNamespace* alanını hizmet ad alanınızla ve *yourKey* alanını da SAS anahtarınızla değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-216">Be sure to replace *yourServiceNamespace* with the name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="9db65-217">Bu işlem, çağrı sonucunu döndürerek istemcinin şirket içi hizmete çağrı yapmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9db65-217">This will enable the client to call the on-premises service, returning the result of the call.</span></span>

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
           // Declare the channel factory.
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
                   // Return a view of the products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. <span data-ttu-id="9db65-218">Çözüm Gezgini’nde **ProductsPortal** çözümüne sağ tıklayın (projeye değil, çözüme sağ tıkladığınızdan emin olun).</span><span class="sxs-lookup"><span data-stu-id="9db65-218">In Solution Explorer, right-click the **ProductsPortal** solution (make sure to right-click the solution, not the project).</span></span> <span data-ttu-id="9db65-219">**Ekle**'ye ve ardından **Var Olan Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="9db65-220">**ProductsServer** projesine gidip **ProductsServer.csproj** çözümüne çift tıklayarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-220">Navigate to the **ProductsServer** project, then double-click the **ProductsServer.csproj** solution file to add it.</span></span>
9. <span data-ttu-id="9db65-221">**ProductsPortal**'da veri görüntülemek için**ProductsServer** projesinin çalışıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9db65-221">**ProductsServer** must be running in order to display the data on **ProductsPortal**.</span></span> <span data-ttu-id="9db65-222">Çözüm Gezgini'nde **ProductsPortal** çözümüne sağ tıklayın ve ardından **Özellikler** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-222">In Solution Explorer, right-click the **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="9db65-223">**Özellik Sayfaları** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9db65-223">The **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="9db65-224">Sol taraftaki **Başlangıç Projesi**'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-224">On the left side, click **Startup Project**.</span></span> <span data-ttu-id="9db65-225">Sağ taraftaki **Birden çok başlangıç projesine** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-225">On the right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="9db65-226">**ProductsServer** ve **ProductsPortal** projelerinin belirtilen sırada göründüğünden ve her ikisi için de eylem olarak **Başlat** seçeneğinin ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as the action for both.</span></span>

      ![][25]

11. <span data-ttu-id="9db65-227">Yine **Özellikler** iletişim kutusunda, sol tarafta bulunan **Proje Bağımlılıkları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-227">Still in the **Properties** dialog box, click **Project Dependencies** on the left side.</span></span>
12. <span data-ttu-id="9db65-228">**Projeler** listesinde **ProductsServer** projesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-228">In the **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="9db65-229">**ProductsPortal**'ın seçilmediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="9db65-230">**Projeler** listesinde **ProductsPortal** projesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-230">In the **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="9db65-231">**ProductsServer** projesinin seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9db65-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="9db65-232">**Özellik Sayfaları** iletişim kutusunda **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-232">Click **OK** in the **Property Pages** dialog box.</span></span>

## <a name="run-the-project-locally"></a><span data-ttu-id="9db65-233">Projeyi yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9db65-233">Run the project locally</span></span>

<span data-ttu-id="9db65-234">Uygulamayı yerel olarak test etmek için Visual Studio'da **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-234">To test the application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="9db65-235">İlk olarak şirket içi sunucunun (**ProductsServer**) başlaması gerekir, ardından **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9db65-235">The on-premises server (**ProductsServer**) should start first, then the **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="9db65-236">Bu kez ürün stoğunun ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9db65-236">This time, you will see that the product inventory lists data retrieved from the product service on-premises system.</span></span>

![][10]

<span data-ttu-id="9db65-237">**ProductsPortal** sayfasında **Yenile** düğmesine basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-237">Press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="9db65-238">Sayfayı her yenilediğinizde, **ProductsServer** uygulamasından `GetProducts()` çağrıldığında sunucu uygulamasının bir ileti gönderdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9db65-238">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="9db65-239">Sonraki adıma geçmeden önce her iki uygulamayı da kapatın.</span><span class="sxs-lookup"><span data-stu-id="9db65-239">Close both applications before proceeding to the next step.</span></span>

## <a name="deploy-the-productsportal-project-to-an-azure-web-app"></a><span data-ttu-id="9db65-240">ProductsPortal projesini bir Azure web uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="9db65-240">Deploy the ProductsPortal project to an Azure web app</span></span>

<span data-ttu-id="9db65-241">Sonraki adımda, Azure Web uygulaması **ProductsPortal** ön ucunu yeniden yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9db65-241">The next step is to republish the Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="9db65-242">Şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="9db65-242">Do the following:</span></span>

1. <span data-ttu-id="9db65-243">Çözüm Gezgini'nde **ProductsPortal** projesine sağ tıklayın ve **Yayımla** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-243">In Solution Explorer, right-click the **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="9db65-244">Ardından **Yayımlama** sayfasında **Yayımla**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-244">Then, click **Publish** on the **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9db65-245">Dağıtımdan sonra **ProductsPortal** web projesinin otomatik olarak başlatılması durumunda tarayıcıda bir hata iletisi görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="9db65-245">You may see an error message in the browser window when the **ProductsPortal** web project is automatically launched after the deployment.</span></span> <span data-ttu-id="9db65-246">**ProductsServer** uygulaması henüz çalışmadığından bu durumun meydana gelmesi olasıdır.</span><span class="sxs-lookup"><span data-stu-id="9db65-246">This is expected, and occurs because the **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="9db65-247">Bir sonraki adımda ihtiyaç duyacağınız için, dağıtılan web uygulamasının URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-247">Copy the URL of the deployed web app, as you will need the URL in the next step.</span></span> <span data-ttu-id="9db65-248">Ayrıca, Visual Studio'daki Azure App Service Etkinliği penceresinden de bu URL'yi elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9db65-248">You can also obtain this URL from the Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="9db65-249">Çalışan uygulamayı durdurmak için tarayıcı penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="9db65-249">Close the browser window to stop the running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="9db65-250">ProductsPortal'ı web uygulaması olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="9db65-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="9db65-251">Uygulamayı bulutta çalıştırmadan önce **ProductsPortal** öğesinin Visual Studio'da bir web uygulaması olarak başlatıldığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9db65-251">Before running the application in the cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="9db65-252">Visual Studio'da **ProductsPortal** projesine sağ tıklayın ve ardından **Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-252">In Visual Studio, right-click the **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="9db65-253">Sol sütunda, **Web**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-253">In the left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="9db65-254">**Eylemi Başlat** bölümünde, **URL'yi Başlat** düğmesine tıklayın ve daha önce dağıttınız web uygulamasının URL'sini metin kutusuna girin (örneğin, `http://productsportal1234567890.azurewebsites.net/`).</span><span class="sxs-lookup"><span data-stu-id="9db65-254">In the **Start Action** section, click the **Start URL** button, and in the text box enter the URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="9db65-255">Visual Studio'daki **Dosya** menüsünde **Tümünü Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-255">From the **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="9db65-256">Visual Studio'da Derle menüsünde **Çözümü Yeniden Derle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9db65-256">From the Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="9db65-257">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9db65-257">Run the application</span></span>

1. <span data-ttu-id="9db65-258">Uygulamayı derleyip çalıştırmak için F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-258">Press F5 to build and run the application.</span></span> <span data-ttu-id="9db65-259">Öncelikle şirket içi sunucu (**ProductsServer** konsol uygulaması) başlamalıdır, ardından aşağıdaki ekran görüntüsünde gösterildiği gibi **ProductsPortal** uygulaması bir tarayıcı penceresinde başlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="9db65-259">The on-premises server (the **ProductsServer** console application) should start first, then the **ProductsPortal** application should start in a browser window, as shown in the following screen shot.</span></span> <span data-ttu-id="9db65-260">Ürün stoğunun ürün hizmeti şirket içi sisteminden aldığı verileri listelediğini ve bu verileri web uygulamasında gösterdiğini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9db65-260">Notice again that the product inventory lists data retrieved from the product service on-premises system, and displays that data in the web app.</span></span> <span data-ttu-id="9db65-261">**ProductsPortal**'ın bir Azure web uygulaması olarak bulutta çalıştığından emin olmak için URL'yi kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="9db65-261">Check the URL to make sure that **ProductsPortal** is running in the cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="9db65-262">**ProductsServer** konsol uygulamasının çalışır ve **ProductsPortal** uygulamasına veri sunma işlemini gerçekleştirebilir durumda olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9db65-262">The **ProductsServer** console application must be running and able to serve the data to the **ProductsPortal** application.</span></span> <span data-ttu-id="9db65-263">Tarayıcı bir hata görüntülerse birkaç saniye daha **ProductsServer** uygulamasının yüklenmesini ve aşağıdaki iletiyi görüntülemesini bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9db65-263">If the browser displays an error, wait a few more seconds for **ProductsServer** to load and display the following message.</span></span> <span data-ttu-id="9db65-264">Daha sonra, tarayıcıda **Yenile** seçeneğine basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-264">Then press **Refresh** in the browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="9db65-265">Tarayıcı yenilendikten sonra **ProductsPortal** sayfasında **Yenile**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="9db65-265">Back in the browser, press **Refresh** on the **ProductsPortal** page.</span></span> <span data-ttu-id="9db65-266">Sayfayı her yenilediğinizde, **ProductsServer** uygulamasından `GetProducts()` çağrıldığında sunucu uygulamasının bir ileti gönderdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9db65-266">Each time you refresh the page, you'll see the server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="9db65-267">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9db65-267">Next steps</span></span>

<span data-ttu-id="9db65-268">Azure Geçiş hakkında daha fazla bilgi edinmek için şu kaynaklara bakın:</span><span class="sxs-lookup"><span data-stu-id="9db65-268">To learn more about Azure Relay, see the following resources:</span></span>  

* [<span data-ttu-id="9db65-269">Azure Geçiş nedir?</span><span class="sxs-lookup"><span data-stu-id="9db65-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="9db65-270">Geçiş nasıl kullanılır?</span><span class="sxs-lookup"><span data-stu-id="9db65-270">How to use Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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
