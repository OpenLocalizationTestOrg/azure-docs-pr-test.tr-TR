---
title: "Azure geçişi kullanarak aaaService Bus REST Öğreticisi | Microsoft Docs"
description: "REST tabanlı bir arabirimi kullanıma sunan basit bir Azure Service Bus geçişi ana bilgisayar uygulaması derleyin."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="0b0fb-103">Azure WCF geçişi REST Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="0b0fb-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="0b0fb-104">Bu öğretici toobuild basit bir Azure geçişi REST tabanlı bir arabirimi kullanıma sunan uygulama nasıl ana bilgisayar açıklar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="0b0fb-105">REST, HTTP üzerinden Service Bus API'lerine istekleri tooaccess hello bir web tarayıcısı gibi bir web istemcisi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="0b0fb-106">Merhaba öğretici, Service Bus hello Windows Communication Foundation (WCF) REST programlama modeli tooconstruct bir REST hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="0b0fb-107">Daha fazla bilgi için bkz: [WCF REST programlama modeli](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) ve [Hizmetleri Tasarlama ve uygulama](/dotnet/framework/wcf/designing-and-implementing-services) hello WCF belgelerinde içinde.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="0b0fb-108">1. Adım: Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b0fb-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="0b0fb-109">Merhaba Azure geçiş özelliklerinde toobegin kullanarak, öncelikle bir hizmet ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="0b0fb-110">Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="0b0fb-111">Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="0b0fb-112">2. adım: bir REST tabanlı WCF Hizmeti sözleşmesi toouse Azure geçiş ile tanımlama</span><span class="sxs-lookup"><span data-stu-id="0b0fb-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="0b0fb-113">WCF REST tarzı bir hizmete oluşturduğunuzda, hello sözleşme tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="0b0fb-114">ana bilgisayar destekler ne gibi işlemler hello Hello sözleşme belirtir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="0b0fb-115">Bir hizmet işlemi, web hizmeti yöntemi olarak düşünülebilir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="0b0fb-116">Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="0b0fb-117">Merhaba arabirimdeki her yöntem tooa belirli hizmet işlemi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="0b0fb-118">Merhaba [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliği uygulanan tooeach arabirimi ve gerekir hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliği uygulanan tooeach işlemi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="0b0fb-119">Bir yöntemi varsa hello içeren bir arabirimdeki [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) hello yok [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), yöntem kullanıma sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="0b0fb-120">Bu görevler için kullanılan hello kodu aşağıdaki hello yordamın hello örnekte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="0b0fb-121">Merhaba WCF sözleşmesi ve REST stili sözleşmesi arasındaki birincil fark olan bir özellik toohello hello eklenmesi [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b0fb-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="0b0fb-122">Bu özellik arabirimi tooa yönteminizi hello üzerinde yönteminde toomap diğer tarafını hello arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="0b0fb-123">Bu durumda, kullanacağız [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink yöntemi tooHTTP alın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="0b0fb-124">Bu hizmet tooaccurately almak ve toohello arabirimi gönderilen komutları yorumlama veri yolu sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="0b0fb-125">toocreate bir arabirim ile bir sözleşme</span><span class="sxs-lookup"><span data-stu-id="0b0fb-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="0b0fb-126">Visual Studio'yu yönetici olarak açın: hello sağ hello programında **Başlat** menüsüne ve ardından **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="0b0fb-127">Yeni bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-127">Create a new console application project.</span></span> <span data-ttu-id="0b0fb-128">Hello tıklatın **dosya** menü ve select **yeni**seçeneğini belirleyip **proje**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="0b0fb-129">Merhaba, **yeni proje** iletişim kutusu, tıklatın **Visual C#**seçin hello **konsol uygulaması** şablonu ve adlandırın **Imagelistener**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="0b0fb-130">Merhaba varsayılan kullanmak **konumu**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-130">Use hello default **Location**.</span></span> <span data-ttu-id="0b0fb-131">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="0b0fb-132">Visual Studio, bir C# projesi için `Program.cs` dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="0b0fb-133">Bu sınıf, boş bir içerir `Main()` yöntemi, bir konsol uygulama projesi toobuild için doğru gerekli.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="0b0fb-134">Başvuruları tooService veri yolu ekleyin ve **System.ServiceModel.dll** hello Service Bus NuGet paketini yükleyerek toohello projesi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="0b0fb-135">Bu paket otomatik olarak başvuruları toohello Service Bus kitaplıklarının yanı sıra hello WCF ekler **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="0b0fb-136">Çözüm Gezgini'nde hello sağ **Imagelistener** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="0b0fb-137">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="0b0fb-138">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="0b0fb-139">Bir başvuru çok açıkça eklemeniz gerekir**System.ServiceModel.Web.dll** toohello proje:</span><span class="sxs-lookup"><span data-stu-id="0b0fb-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="0b0fb-140">a.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-140">a.</span></span> <span data-ttu-id="0b0fb-141">Çözüm Gezgini'nde hello sağ **başvuruları** hello proje klasörünü ve ardından altında bir klasör **Başvuru Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="0b0fb-142">b.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-142">b.</span></span> <span data-ttu-id="0b0fb-143">Merhaba, **Başvuru Ekle** iletişim kutusunda, hello **Framework** sekmesinde hello sol taraftaki ve hello **arama** kutusuna **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="0b0fb-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="0b0fb-144">Select hello **System.ServiceModel.Web** onay kutusunu işaretleyin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="0b0fb-145">Merhaba aşağıdakileri ekleyin `using` deyimleri hello Program.cs dosyasının hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="0b0fb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) WCF programlı erişim toobasic özellikleri etkinleştirir hello ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="0b0fb-147">WCF geçiş hello nesnelerin çoğunu ve WCF toodefine Hizmet sözleşmeleri özniteliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="0b0fb-148">Geçiş uygulamalarınızın çoğunda bu ad alanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="0b0fb-149">Benzer şekilde, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) yardımcı Azure geçişi ve hello istemci web tarayıcısı ile iletişim hello nesne hello kanal tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="0b0fb-150">Son olarak, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) toocreate web tabanlı uygulamalar sağlayan hello türler içerir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="0b0fb-151">Merhaba yeniden adlandırma `ImageListener` ad alanı çok**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="0b0fb-152">Doğrudan hello ad alanı bildiriminin büyük ayracını açma hello sonra adlı yeni arabirimi tanımlayın **Iımagecontract** ve hello geçerli **ServiceContractAttribute** özniteliği toohello arabirimi ile bir değeri `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="0b0fb-153">Hello ad alanı değeri kodunuzu hello kapsam boyunca kullandığınız hello ad alanından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="0b0fb-154">Merhaba ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır ve sürüm bilgisini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="0b0fb-155">Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="0b0fb-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="0b0fb-156">Hello ad alanını açıkça belirlemek hello varsayılan ad alanı değeri toohello sözleşme adına eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="0b0fb-157">Merhaba içinde `IImageContract` arabirim, hello tek bir işlem hello için bir yöntem bildirin `IImageContract` sözleşme çıkarır hello içinde arabirim ve hello geçerli `OperationContractAttribute` özniteliği hello genel hizmet veri yolu bir parçası olarak tooexpose istediğiniz toohello yöntemi Sözleşme.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="0b0fb-158">Merhaba, **OperationContract** özniteliği, hello eklemek **WebGet** değeri.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="0b0fb-159">Geçiş hizmeti tooroute HTTP GET istekleri çok etkinleştirir hello bunları yapmak`GetImage`ve dönüş değerleri, tootranslate hello `GetImage` HTTP GETRESPONSE yanıtına içine.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="0b0fb-160">Daha sonra hello öğreticide, bir web tarayıcısı tooaccess bu yöntem ve toodisplay hello görüntü hello tarayıcıda kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="0b0fb-161">Merhaba hemen sonra `IImageContract` tanımı, her iki hello devralan bir kanal bildirin `IImageContract` ve `IClientChannel` arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="0b0fb-162">Bir kanal üzerinden hello hizmet ve istemci bilgileri tooeach diğer kullandıkları hello WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="0b0fb-163">Daha sonra ana bilgisayar uygulamanızda hello kanalı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="0b0fb-164">Azure geçişi, ardından bu kanal toopass hello HTTP GET isteklerine hello tarayıcı tooyour kullanır **Getımage** uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="0b0fb-165">Merhaba geçiş de hello kanal tootake hello kullanır **Getımage** dönüş değeri ve hello istemci tarayıcısı için HTTP GetResponse çevir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="0b0fb-166">Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tooconfirm hello çalışmanızın o ana kadarki doğruluğunu.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="0b0fb-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b0fb-167">Example</span></span>
<span data-ttu-id="0b0fb-168">koddan hello WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="0b0fb-169">Adım 3: REST tabanlı WCF Hizmeti sözleşmesi toouse Service Bus uygulayın</span><span class="sxs-lookup"><span data-stu-id="0b0fb-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="0b0fb-170">REST stilinde WCF geçiş hizmeti oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan hello sözleşmeyi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="0b0fb-171">Merhaba sonraki adıma tooimplement hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="0b0fb-172">Bu adlı bir sınıf oluşturursunuz **Imageservice** hello kullanıcı tanımlı uygulayan **Iımagecontract** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="0b0fb-173">Merhaba sözleşmeyi uyguladıktan sonra bir App.config dosyası kullanarak hello arabirimi ardından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="0b0fb-174">Merhaba yapılandırma dosyası hello hello hizmetin adını, hello adını hello sözleşme ve hello geçiş hizmeti ile kullanılan toocommunicate Protokolü hello türü gibi hello uygulama için gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="0b0fb-175">Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="0b0fb-176">Olarak hello önceki adımlara REST stilinde sözleşme ve WCF geçiş sözleşmesi uygulama arasında çok az fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="0b0fb-177">tooimplement REST stilinde Service Bus Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="0b0fb-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="0b0fb-178">Adlı yeni bir sınıf oluşturun **Imageservice** hello hello tanımını hemen sonra **Iımagecontract** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="0b0fb-179">Merhaba **Imageservice** sınıfı uygulayan hello **Iımagecontract** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="0b0fb-180">Benzer tooother arabirim uygulamaları, farklı bir dosyada hello tanımı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="0b0fb-181">Ancak, Bu öğretici için hello uygulama aynı dosya hello arabirim tanımı hello görünür ve `Main()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="0b0fb-182">Merhaba uygulamak [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello özniteliği **ServiceBehaviorAttribute** sınıfı hello sınıfı tooindicate WCF sözleşmesinin bir uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="0b0fb-183">Önceden belirtildiği gibi bu ad alanı, geleneksel bir ad alanı değildir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="0b0fb-184">Bunun yerine, hello hello sözleşmeyi tanımlayan WCF mimarisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="0b0fb-185">Daha fazla bilgi için bkz: Merhaba [veri sözleşmesi adları](https://msdn.microsoft.com/library/ms731045.aspx) hello WCF belgelerinde konuda.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="0b0fb-186">Bir .jpg görüntüsü tooyour proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="0b0fb-187">Bu tarayıcı alma hello hello hizmet görüntüleyen bir resimdir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="0b0fb-188">Projenize sağ tıklayın ve ardından **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="0b0fb-189">Ardından **Var Olan Öğe**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-189">Then click **Existing Item**.</span></span> <span data-ttu-id="0b0fb-190">Kullanım hello **varolan öğeyi Ekle** iletişim kutusu toobrowse tooan .jpg uygun ve ardından **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="0b0fb-191">Merhaba dosya eklerken emin olun **tüm dosyaları** hello aşağı açılan liste sonraki toohello seçili **dosya adı:** alan.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="0b0fb-192">Bu öğreticinin geri kalanını Hello varsayar bu hello "image.jpg" Merhaba görüntü adıdır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="0b0fb-193">Farklı bir dosya varsa, toorename hello görüntüsü olması veya kod toocompensate değiştirmek.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="0b0fb-194">toomake hizmetini çalıştıran bu hello bulabilir hello resim dosyası olarak emin **Çözüm Gezgini** hello görüntü dosyasına sağ tıklayın ve ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="0b0fb-195">Merhaba, **özellikleri** kümesi bölmesi, **tooOutput dizin kopyalama** çok**yeniyse Kopyala**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="0b0fb-196">Bir başvuru toohello ekleme **System.Drawing.dll** derleme toohello proje ve ilişkili hello aşağıdaki eklemek `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="0b0fb-197">Merhaba, **Imageservice** sınıfı, eklemek isteğe bağlı olarak yükleri hello bit eşlem ve toosend hazırlar Oluşturucusu toohello istemci tarayıcısına hello.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="0b0fb-198">Merhaba önceki kod, hemen sonra hello aşağıdakileri ekleyin **Getımage** hello yönteminde **Imageservice** hello görüntüsünü içeren sınıf tooreturn bir HTTP iletisi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="0b0fb-199">Bu uygulama kullanan **MemoryStream** tooretrieve hello görüntü ve toohello tarayıcı akış için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="0b0fb-200">Merhaba akış noktasını sıfırdan başlatır, hello akış içeriğini .JPEG olarak bildirir ve hello bilgileri akışa sunar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="0b0fb-201">Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="0b0fb-202">Service Bus hello web hizmetini çalıştırmak için toodefine hello yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b0fb-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="0b0fb-203">İçinde **Çözüm Gezgini**, çift **App.config** tooopen onu hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="0b0fb-204">Merhaba **App.config** dosyası, hello hizmet adı, uç noktayı (Azure geçiş tarafından kullanıma sunulan birbirleriyle istemcilerin ve ana bilgisayarların toocommunicate diğer bir deyişle, hello konum) ve bağlama (kullanılan toocommunicate Protokolü hello türü) içerir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="0b0fb-205">Merhaba ana burada bu hello yapılandırılan hizmet uç noktası başvuruyor tooa farktır [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) bağlama.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="0b0fb-206">Merhaba `<system.serviceModel>` XML öğesi olan bir veya daha çok hizmeti tanımlayan WCF öğesidir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="0b0fb-207">Aşağıda, kullanılan toodefine hello hizmet adını ve uç nokta verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="0b0fb-208">Merhaba hello sonundaki `<system.serviceModel>` öğesi (ancak hala içinde `<system.serviceModel>`), ekleme bir `<bindings>` içeriği aşağıdaki hello sahip öğe.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="0b0fb-209">Merhaba uygulamada kullanılan hello bağlamaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="0b0fb-210">Birden çok bağlama tanımlayabilirsiniz ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="0b0fb-211">Merhaba önceki kod tanımlayan WCF geçiş [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) ile bağlama **öğesinin** çok ayarlamak**hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="0b0fb-212">Bu ayar, yukarıdaki bağlamayı kullanan bir uç noktanın istemci kimlik bilgilerini gerektirmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="0b0fb-213">Merhaba sonra `<bindings>` öğesi ekleme bir `<services>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="0b0fb-214">Benzer toohello bağlamalarla tek yapılandırma dosyasında birden çok hizmet tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="0b0fb-215">Ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="0b0fb-216">Bu adım önceden tanımlanmış hello varsayılan kullanan bir hizmet yapılandırır **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="0b0fb-217">Ayrıca hello varsayılan kullanır **sbTokenProvider**, hello sonraki adımda tanımlanan.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="0b0fb-218">Hello sonra `<services>` öğesini oluşturmak bir `<behaviors>` içeriği izleyerek, "SAS_KEY" hello ile değiştiriliyor hello bir öğesiyle *paylaşılan erişim imzası* hello daha önce edindiğiniz (SAS) anahtarı [Azure portalı ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="0b0fb-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="0b0fb-219">Merhaba, App.config yine de `<appSettings>` öğesi, hello Portalı'ndan daha önce edindiğiniz hello bağlantı dizesiyle değiştirin hello tüm bağlantı dize değeri.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="0b0fb-220">Merhaba gelen **yapı** menüsünde tıklatın **Çözümü Derle** toobuild hello çözümün tamamı.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="0b0fb-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b0fb-221">Example</span></span>
<span data-ttu-id="0b0fb-222">Merhaba aşağıdaki kod gösterir hello sözleşme ve hizmet uygulaması hello kullanarak Service Bus üzerinde çalışan REST tabanlı bir hizmetine **WebHttpRelayBinding** bağlama.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="0b0fb-223">Merhaba aşağıdaki örnek hello hizmetiyle ilişkili hello App.config dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="0b0fb-224">4. adım: Ana bilgisayar hello REST tabanlı WCF Hizmeti toouse Azure geçişi</span><span class="sxs-lookup"><span data-stu-id="0b0fb-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="0b0fb-225">Bu adım, nasıl toorun bir web hizmeti WCF geçiş ile bir konsol uygulaması kullanarak açıklar.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="0b0fb-226">Bu adımda yazılan hello kodu tam bir listesi aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="0b0fb-227">toocreate hello hizmeti için bir taban adresi</span><span class="sxs-lookup"><span data-stu-id="0b0fb-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="0b0fb-228">Merhaba, `Main()` işlevi bildiriminde, projenizin bir değişken toostore hello ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="0b0fb-229">Emin tooreplace olun `yourNamespace` hello geçiş ad alanı daha önce oluşturduğunuz hello adı.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="0b0fb-230">Service Bus, ad alanı toocreate benzersiz bir URI hello adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="0b0fb-231">Oluşturma bir `Uri` hello ad alanını temel hello hizmeti hello temel adres için örneği.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="0b0fb-232">toocreate ve hello web hizmeti ana bilgisayarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b0fb-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="0b0fb-233">Bu bölümde daha önce oluşturduğunuz hello URI adresini kullanarak hello web hizmeti ana bilgisayarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="0b0fb-234">Merhaba hizmet konağı hello ana bilgisayar uygulamasının örneğini oluşturan hello WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="0b0fb-235">İsteğe bağlı olarak bu örnek hello türü geçirir toocreate istediğiniz ana bilgisayarın (bir **Imageservice**), ve ayrıca istediğiniz tooexpose Merhaba ana bilgisayar uygulaması adresi hello.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="0b0fb-236">toorun hello web hizmeti ana bilgisayarı</span><span class="sxs-lookup"><span data-stu-id="0b0fb-236">toorun hello web service host</span></span>
1. <span data-ttu-id="0b0fb-237">Merhaba hizmeti açın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="0b0fb-238">Merhaba hizmet artık çalışır durumdadır.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-238">hello service is now running.</span></span>
2. <span data-ttu-id="0b0fb-239">Merhaba hizmetinin çalıştığını ve nasıl toostop hello hizmet belirten bir ileti görüntüler.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="0b0fb-240">Tamamlandığında, hello hizmet ana bilgisayarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="0b0fb-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="0b0fb-241">Example</span></span>
<span data-ttu-id="0b0fb-242">Aşağıdaki örneğine hello hello öğretici ve ana hello hizmeti bir konsol uygulamasında hello hizmet sözleşmesini ve önceki adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="0b0fb-243">ImageListener.exe adlı bir yürütülebilir koddan hello derleyin.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="0b0fb-244">Merhaba kodu derleme</span><span class="sxs-lookup"><span data-stu-id="0b0fb-244">Compiling hello code</span></span>
<span data-ttu-id="0b0fb-245">Merhaba çözümü derledikten sonra toorun Merhaba uygulaması hello:</span><span class="sxs-lookup"><span data-stu-id="0b0fb-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="0b0fb-246">Tuşuna **F5**, veya toohello yürütülebilir dosya konumu (ImageListener\bin\Debug\ImageListener.exe) toorun hello hizmet göz atın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="0b0fb-247">Tooperform hello sonraki adıma istedi gibi hello uygulama çalışırken, tutun.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="0b0fb-248">Hello adresini kopyalayıp hello komut isteminden bir tarayıcı toosee hello görüntüsüne yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="0b0fb-249">İşiniz bittiğinde, basın **Enter** hello komut istemi penceresi tooclose hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="0b0fb-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0fb-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b0fb-250">Next steps</span></span>
<span data-ttu-id="0b0fb-251">Merhaba Service Bus geçişi hizmetini kullanan bir uygulama oluşturduğunuza göre Azure geçişi hakkında daha fazla makaleleri toolearn aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0b0fb-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="0b0fb-252">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="0b0fb-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="0b0fb-253">Azure Geçiş’e genel bakış</span><span class="sxs-lookup"><span data-stu-id="0b0fb-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="0b0fb-254">Toouse hello WCF hizmeti .NET ile nasıl geçiş</span><span class="sxs-lookup"><span data-stu-id="0b0fb-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
