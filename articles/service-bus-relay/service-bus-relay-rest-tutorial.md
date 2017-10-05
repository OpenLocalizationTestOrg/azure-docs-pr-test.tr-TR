---
title: "Azure geçişi kullanarak Service Bus REST Öğreticisi | Microsoft Docs"
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
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="63939-103">Azure WCF geçişi REST Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="63939-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="63939-104">Bu öğretici, REST tabanlı bir arabirimi kullanıma sunan basit bir Azure geçişi ana bilgisayar uygulaması derlemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="63939-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="63939-105">REST, HTTP istekleri üzerinden Service Bus API'lerine erişmek için web tarayıcısı gibi bir web istemcisi sunar.</span><span class="sxs-lookup"><span data-stu-id="63939-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="63939-106">Öğretici, Service Bus üzerinde bir REST hizmeti oluşturmak için programlama modeli Windows Communication Foundation (WCF) REST kullanır.</span><span class="sxs-lookup"><span data-stu-id="63939-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="63939-107">Daha fazla bilgi için WCF belgelerinde [WCF REST Programlama Modeli](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) ve [Hizmetleri Tasarlama ve Uygulama](/dotnet/framework/wcf/designing-and-implementing-services) konularına bakın.</span><span class="sxs-lookup"><span data-stu-id="63939-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="63939-108">1. Adım: Ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="63939-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="63939-109">Azure'da geçiş özelliklerini kullanmaya başlamak için öncelikle bir hizmet ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="63939-110">Ad alanı, uygulamanızda bulunan Azure kaynaklarını adreslemek için içeriğin kapsamını belirleyen bir kapsayıcı sunar.</span><span class="sxs-lookup"><span data-stu-id="63939-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="63939-111">[Buradaki yönergeleri](relay-create-namespace-portal.md) izleyerek bir Geçiş ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="63939-112">2. adım: Azure geçiş ile kullanmak için REST tabanlı WCF hizmet sözleşmesini tanımlama</span><span class="sxs-lookup"><span data-stu-id="63939-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="63939-113">Bir WCF REST stilinde hizmet oluşturduğunuzda sözleşme tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="63939-114">Sözleşmede ana bilgisayarın hangi işlemleri desteklediği belirtilir.</span><span class="sxs-lookup"><span data-stu-id="63939-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="63939-115">Bir hizmet işlemi, web hizmeti yöntemi olarak düşünülebilir.</span><span class="sxs-lookup"><span data-stu-id="63939-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="63939-116">Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="63939-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="63939-117">Arabirimdeki her yöntem belirli bir hizmet işlemine karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="63939-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="63939-118">[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğinin her arabirime ve [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliğinin her işleme uygulanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="63939-119">Arabirimdeki bir yöntem [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğine sahip olup [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliğine sahip olmazsa bu yöntem kullanıma sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="63939-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="63939-120">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="63939-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="63939-121">Bir WCF sözleşmesi ve REST stili sözleşmesi arasındaki birincil fark bir özelliğe ektir [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="63939-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="63939-122">Bu özellik sayesinde arabiriminizdeki bir yöntem ile arabirimin diğer tarafındaki bir yöntemi eşleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63939-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="63939-123">Bu durumda, HTTP GET işlemine bir yöntem bağlamak için [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) özniteliğini kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="63939-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="63939-124">Bu özellik, Service Bus'ın arabirime gönderilen komutları doğru şekilde almasını ve yorumlamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="63939-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="63939-125">Bir arabirim ile bir sözleşme oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="63939-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="63939-126">Visual Studio'yu yönetici olarak açın: **Başlangıç** menüsünde programa sağ tıklayıp **Yönetici olarak çalıştır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="63939-127">Yeni bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-127">Create a new console application project.</span></span> <span data-ttu-id="63939-128">**Dosya** menüsüne tıklayın ve **Yeni** seçeneğini belirleyip **Proje** seçimini yapın.</span><span class="sxs-lookup"><span data-stu-id="63939-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="63939-129">**Yeni Proje** iletişim kutusunda **Visual C#** seçeneğine tıklayıp **Konsol Uygulaması** şablonuna tıklayın ve **ImageListener** olarak adlandırın.</span><span class="sxs-lookup"><span data-stu-id="63939-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="63939-130">Varsayılan **Konum**'u kullanın.</span><span class="sxs-lookup"><span data-stu-id="63939-130">Use the default **Location**.</span></span> <span data-ttu-id="63939-131">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="63939-132">Visual Studio, bir C# projesi için `Program.cs` dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="63939-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="63939-133">Bu sınıf, bir konsol uygulaması projesinin doğru şekilde derlenmesi için gerekli olan boş `Main()` yöntemi içerir.</span><span class="sxs-lookup"><span data-stu-id="63939-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="63939-134">Service Bus hizmetine başvurular ekleyin ve Service Bus NuGet paketini yükleyerek projede **System.ServiceModel.dll** öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="63939-135">Bu paket otomatik olarak Service Bus kitaplıklarının yanı sıra WCF **System.ServiceModel** öğesine de başvurular ekler.</span><span class="sxs-lookup"><span data-stu-id="63939-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="63939-136">Çözüm Gezgini'nde **ImageListener** projesine sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="63939-137">**Gözat** sekmesine tıklayıp `Microsoft Azure Service Bus` aramasını gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="63939-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="63939-138">**Yükle**'ye tıklayın ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="63939-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="63939-139">Projede **System.ServiceModel.Web.dll** öğesine açık olarak bir başvuru eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="63939-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="63939-140">a.</span><span class="sxs-lookup"><span data-stu-id="63939-140">a.</span></span> <span data-ttu-id="63939-141">Çözüm Gezgini'nde, **Başvurular** klasörüne sağ tıklayın ve proje klasöründe **Başvuru Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="63939-142">b.</span><span class="sxs-lookup"><span data-stu-id="63939-142">b.</span></span> <span data-ttu-id="63939-143">**Başvuru Ekle** iletişim kutusunda, sol taraftaki **Altyapı** sekmesine tıklayın ve **Ara** kutusuna **System.ServiceModel.Web** yazın.</span><span class="sxs-lookup"><span data-stu-id="63939-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="63939-144">**System.ServiceModel.Web** öğesinin onay kutusunu işaretleyin ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="63939-145">Aşağıdaki `using` deyimlerini Program.cs dosyasının üstüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="63939-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx), WCF'nin temel özelliklerine programlama erişimi sağlayan ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="63939-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="63939-147">WCF geçiş, birçok nesnesini ve özniteliklerini WCF hizmet sözleşmelerini tanımlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="63939-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="63939-148">Geçiş uygulamalarınızın çoğunda bu ad alanı kullanır.</span><span class="sxs-lookup"><span data-stu-id="63939-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="63939-149">Benzer şekilde, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) yardımcı iletişim Azure geçişi ve istemci web tarayıcısı ile nesne kanal tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="63939-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="63939-150">Son olarak [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx), web tabanlı uygulamalar oluşturmanıza olanak sağlayan türleri içerir.</span><span class="sxs-lookup"><span data-stu-id="63939-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="63939-151">`ImageListener` ad alanını **Microsoft.ServiceBus.Samples** olarak yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="63939-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="63939-152">Ad alanı bildiriminin büyük ayracını açtıktan hemen sonra **IImageContract** adlı yeni bir arabirim tanımlayın ve `http://samples.microsoft.com/ServiceModel/Relay/` değerini içeren arabirime **ServiceContractAttribute** özniteliğini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="63939-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="63939-153">Kodunuzun kapsamında kullandığınız ad alanı ile ad alanı değeri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="63939-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="63939-154">Ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır ve sürüm bilgisini içermelidir.</span><span class="sxs-lookup"><span data-stu-id="63939-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="63939-155">Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="63939-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="63939-156">Ad alanını açıkça belirlemek, varsayılan ad alanı değerinin sözleşme adına eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="63939-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="63939-157">`IImageContract` arabirimi içinde, `IImageContract` sözleşmesinin arabirimde kullanıma sunduğu tek bir işlem için bir yöntem bildirin ve genel Service Bus sözleşmesinin bir parçası olarak kullanıma sunmak istediğiniz yönteme `OperationContractAttribute` özniteliğini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="63939-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="63939-158">**OperationContract** özniteliği içinde **WebGet** değerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="63939-159">Geçiş hizmeti yol HTTP GET isteklerini için bunu sağlar yapmak `GetImage`ve dönüş değerlerini çevirmek için `GetImage` HTTP GETRESPONSE yanıtına içine.</span><span class="sxs-lookup"><span data-stu-id="63939-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="63939-160">Bu öğreticinin sonraki bölümlerinde, bu yönteme erişmek ve tarayıcıdaki görüntüyü görüntülemek için bir web tarayıcısı kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="63939-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="63939-161">`IImageContract` tanımından hemen sonra, `IImageContract` ve `IClientChannel` arabirimlerinden devralma işlemini gerçekleştiren bir kanal bildirin.</span><span class="sxs-lookup"><span data-stu-id="63939-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="63939-162">Kanal, hizmet ve istemcilerin bilgileri birbirlerine göndermek için kullandıkları WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="63939-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="63939-163">Daha sonra, ana bilgisayar uygulamanızda kanal oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="63939-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="63939-164">Azure geçiş sonra kullanan bu kanalı HTTP GET isteklerini tarayıcıya geçirmek için **Getımage** uygulaması.</span><span class="sxs-lookup"><span data-stu-id="63939-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="63939-165">Geçiş kanalı almak için de kullanır **Getımage** dönüş değeri ve istemci tarayıcısı için HTTP GetResponse çevir.</span><span class="sxs-lookup"><span data-stu-id="63939-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="63939-166">Çalışmanızın o ana kadarki doğruluğunu onaylamak için **Derle** menüsünde **Çözümü Derle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="63939-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="63939-167">Example</span></span>
<span data-ttu-id="63939-168">Aşağıdaki kod bir WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="63939-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="63939-169">Adım 3:Service Bus hizmetini kullanmak için REST tabanlı WCF hizmeti sözleşmesi uygulama</span><span class="sxs-lookup"><span data-stu-id="63939-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="63939-170">REST stilinde WCF geçiş hizmeti oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan sözleşmeyi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="63939-171">Bir sonraki adım ise bu arabirimi uygulamaktır.</span><span class="sxs-lookup"><span data-stu-id="63939-171">The next step is to implement the interface.</span></span> <span data-ttu-id="63939-172">Bu adımda kullanıcı tanımlı **IImageContract** arabirimini uygulayan **ImageService** adlı bir sınıf oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="63939-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="63939-173">Sözleşmeyi uyguladıktan sonra, App.config dosyası kullanarak arabirimi yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="63939-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="63939-174">Yapılandırma dosyasında hizmetin adı, sözleşmenin ve geçiş hizmeti ile iletişim kurmak için kullanılan protokol türü adı gibi uygulama için gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="63939-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="63939-175">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="63939-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="63939-176">Önceki adımlara benzer şekilde, REST stilinde sözleşme ve WCF geçiş sözleşmesi uygulama arasında çok az fark yoktur.</span><span class="sxs-lookup"><span data-stu-id="63939-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="63939-177">REST stilinde Service Bus sözleşmesini uygulama</span><span class="sxs-lookup"><span data-stu-id="63939-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="63939-178">**IImageContract** arabiriminin tanımından hemen sonra **ImageService** adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="63939-179">**ImageService** sınıfı, **IImageContract** arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="63939-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="63939-180">Diğer arabirim uygulamalarına benzer şekilde, tanımı farklı bir dosyada uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63939-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="63939-181">Ancak bu öğreticide uygulama, arabirim tanımı ve `Main()` yöntemiyle aynı dosyada görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="63939-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="63939-182">Sınıfın WCF sözleşmesinin bir uygulaması olduğunu belirtmek için **IImageService** sınıfına [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) özniteliğini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="63939-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="63939-183">Önceden belirtildiği gibi bu ad alanı, geleneksel bir ad alanı değildir.</span><span class="sxs-lookup"><span data-stu-id="63939-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="63939-184">Bunun yerine, ad alanı sözleşmeyi tanımlayan WCF mimarisinin bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="63939-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="63939-185">Daha fazla bilgi için WCF belgelerinde [Veri Sözleşmesi Adları](https://msdn.microsoft.com/library/ms731045.aspx) konu başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="63939-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="63939-186">Projenize bir .jpg görüntüsü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="63939-187">Bu resim, hizmetin alıcı tarayıcıda gösterdiği resimdir.</span><span class="sxs-lookup"><span data-stu-id="63939-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="63939-188">Projenize sağ tıklayın ve ardından **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="63939-189">Ardından **Var Olan Öğe**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-189">Then click **Existing Item**.</span></span> <span data-ttu-id="63939-190">Uygun bir .jpg aramak için **Var Olan Öğeyi Ekle** iletişim kutusunu kullanın ve **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="63939-191">Dosya eklerken **Dosya adı:** alanının yanındaki açılır listede **Tüm Dosyalar** seçeneğinin belirlendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="63939-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="63939-192">Bu öğreticinin bundan sonraki bölümlerinde görüntü adının "image.jpg" olduğu varsayılır.</span><span class="sxs-lookup"><span data-stu-id="63939-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="63939-193">Farklı bir dosyanız varsa görüntüyü tekrar adlandırmanız veya dengelemek için kodunu değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="63939-194">Çalışan hizmetin görüntü dosyasını bulabileceğinden emin olmak için **Çözüm Gezgini**'nde görüntü dosyasına sağ tıklayın ve **Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="63939-195">**Özellikler** bölmesinde, **Çıktı Dizinine Kopyala** seçeneğini **Daha yeniyse kopyala** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="63939-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="63939-196">Projede **System.Drawing.dll** derlemesine başvuru ekleyin ve aşağıdaki ilişkili `using` deyimlerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="63939-197">**ImageService** sınıfında, bit eşlemi yükleyen ve istemci tarayıcıya göndermek için hazırlayan aşağıdaki oluşturucuyu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="63939-198">Önceki koddan hemen sonra görüntüyü içeren HTTP iletisini döndürmek için **ImageService** sınıfında aşağıdaki **GetImage** yöntemini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="63939-199">Bu uygulamalar, görüntüyü almak ve tarayıcıda akış için hazırlamak üzere **MemoryStream** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63939-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="63939-200">Akış noktasını sıfırdan başlatır, akış içeriğini .jpeg olarak bildirir ve bilgileri akışa sunar.</span><span class="sxs-lookup"><span data-stu-id="63939-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="63939-201">**Derle** menüsünde **Çözümü Derle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="63939-202">Service Bus üzerinde web hizmetini çalıştırmak için yapılandırma tanımlama</span><span class="sxs-lookup"><span data-stu-id="63939-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="63939-203">**Çözüm Gezgini**'nde, **App.config** dosyasına çift tıklayarak dosyayı Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="63939-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="63939-204">**App.config** dosya içeren hizmet adını, uç noktayı (diğer bir deyişle, Azure geçiş sunan istemcilerin ve ana bilgisayarların birbirleriyle iletişim kurmak konum) ve bağlamayı (iletişim kurmak için kullanılan protokol türü).</span><span class="sxs-lookup"><span data-stu-id="63939-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="63939-205">Ana burada yapılandırılan hizmet uç noktasının farktır bir [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) bağlama.</span><span class="sxs-lookup"><span data-stu-id="63939-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="63939-206">`<system.serviceModel>` XML öğesi, bir veya birden çok hizmeti tanımlayan WCF öğesidir.</span><span class="sxs-lookup"><span data-stu-id="63939-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="63939-207">Burada ise hizmet adını ve uç noktayı tanımlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63939-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="63939-208">`<system.serviceModel>` öğesinin alt kısmına (ancak hala `<system.serviceModel>` içinde) aşağıdaki içeriğe sahip olan `<bindings>` öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="63939-209">Bu işlem, uygulamada kullanılan bağlamaları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="63939-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="63939-210">Birden çok bağlama tanımlayabilirsiniz ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="63939-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="63939-211">Önceki kod WCF geçiş tanımlar [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) ile bağlama **öğesinin** kümesine **hiçbiri**.</span><span class="sxs-lookup"><span data-stu-id="63939-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="63939-212">Bu ayar, yukarıdaki bağlamayı kullanan bir uç noktanın istemci kimlik bilgilerini gerektirmeyeceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="63939-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="63939-213">`<bindings>` öğesinden sonra `<services>` öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="63939-214">Bağlamalara benzer şekilde tek bir yapılandırma dosyasında birden çok hizmet tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63939-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="63939-215">Ancak bu öğreticide yalnızca bir tane tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="63939-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="63939-216">Bu adımda, önceden tanımlanan varsayılan **webHttpRelayBinding** bağlamasını kullanan bir hizmet yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="63939-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="63939-217">Ayrıca, bir sonraki adımda tanımlanan varsayılan **sbTokenProvider** öğesi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="63939-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="63939-218">Sonra `<services>` öğesini oluşturmak bir `<behaviors>` "SAS_KEY" değiştirerek aşağıdaki içeriğe sahip öğe *paylaşılan erişim imzası* elde ettiğiniz (SAS) anahtarıyla [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="63939-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="63939-219">Yine App.config dosyasında `<appSettings>` öğesinde, tüm bağlantı dizesi değerini portaldan daha önce edindiğiniz bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63939-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="63939-220">Çözümün tamamını derlemek için **Derle** menüsünde **Çözümü Derle** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="63939-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="63939-221">Örnek</span><span class="sxs-lookup"><span data-stu-id="63939-221">Example</span></span>
<span data-ttu-id="63939-222">Aşağıdaki kodda, **WebHttpRelayBinding** bağlamasını kullanan Service Bus üzerinde çalışan REST tabanlı hizmete yönelik sözleşme ve hizmet uygulaması gösterilir.</span><span class="sxs-lookup"><span data-stu-id="63939-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="63939-223">Aşağıdaki örnek, hizmetle ilişkilendirilen App.config dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="63939-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="63939-224">4. adım: Azure geçiş kullanmak için REST tabanlı WCF Hizmeti barındırma</span><span class="sxs-lookup"><span data-stu-id="63939-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="63939-225">Bu adım, WCF geçiş ile bir konsol uygulaması kullanarak bir web hizmetini çalıştırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="63939-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="63939-226">Bu adımda yazılan kodların tam listesi yordamdan sonraki örnekte verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="63939-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="63939-227">Hizmet için taban adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="63939-227">To create a base address for the service</span></span>
1. <span data-ttu-id="63939-228">İçinde `Main()` işlevi bildiriminde, projenizin ad depolamak için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="63939-229">Değiştirdiğinizden emin olun `yourNamespace` daha önce oluşturduğunuz geçiş ad alanı adına sahip.</span><span class="sxs-lookup"><span data-stu-id="63939-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="63939-230">Service Bus, benzersiz bir URI oluşturmak için ad alanınızdaki adı kullanır.</span><span class="sxs-lookup"><span data-stu-id="63939-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="63939-231">Ad alanını temel alan hizmetin taban adresine yönelik `Uri` örneğini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="63939-232">Web hizmeti ana bilgisayarını oluşturma ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="63939-232">To create and configure the web service host</span></span>
* <span data-ttu-id="63939-233">Bu bölümün önceki kısımlarında oluşturulan URI adresini kullanarak web hizmeti ana bilgisayarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="63939-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="63939-234">Hizmet ana bilgisayarı, ana bilgisayar uygulamasının örneğini oluşturan WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="63939-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="63939-235">Bu örnek, hizmet ana bilgisayarını oluşturmak istediğiniz ana bilgisayar türüne (bir **ImageService**) ve ana bilgisayar uygulamasını kullanıma sunmak istediğiniz adrese geçirir.</span><span class="sxs-lookup"><span data-stu-id="63939-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="63939-236">Web hizmeti ana bilgisayarını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="63939-236">To run the web service host</span></span>
1. <span data-ttu-id="63939-237">Hizmeti açın.</span><span class="sxs-lookup"><span data-stu-id="63939-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="63939-238">Hizmet artık çalışır durumdadır.</span><span class="sxs-lookup"><span data-stu-id="63939-238">The service is now running.</span></span>
2. <span data-ttu-id="63939-239">Hizmetin çalıştığını ve nasıl durdurulacağını belirten bir ileti görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="63939-240">Bu işlemi bitirdiğinizde, hizmet ana bilgisayarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="63939-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="63939-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="63939-241">Example</span></span>
<span data-ttu-id="63939-242">Aşağıdaki örnek, hizmet sözleşmesini ve bu öğreticinin önceki kısımlarında yer alan uygulamayı içerir ve hizmeti bir konsol uygulamasında barındırır.</span><span class="sxs-lookup"><span data-stu-id="63939-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="63939-243">Aşağıdaki kodu ImageListener.exe adlı bir yürütülebilir dosyada derleyin.</span><span class="sxs-lookup"><span data-stu-id="63939-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="63939-244">Kod derleme</span><span class="sxs-lookup"><span data-stu-id="63939-244">Compiling the code</span></span>
<span data-ttu-id="63939-245">Çözümü derledikten sonra uygulamayı çalıştırmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="63939-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="63939-246">Hizmeti çalıştırmak için **F5**'e basın veya yürütülebilir dosya konumuna gözatın (ImageListener\bin\Debug\ImageListener.exe).</span><span class="sxs-lookup"><span data-stu-id="63939-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="63939-247">Uygulamayı çalışır durumda tutmak için bir sonraki adımı gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="63939-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="63939-248">Görüntüye bakmak için komut istemindeki adresi kopyalayıp bir tarayıcıya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="63939-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="63939-249">İşiniz bittiğinde uygulamayı kapatmak için komut istemi penceresinde **Enter**'a basın.</span><span class="sxs-lookup"><span data-stu-id="63939-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63939-250">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63939-250">Next steps</span></span>
<span data-ttu-id="63939-251">Service Bus geçişi hizmetini kullanan bir uygulama oluşturduğunuza göre Azure geçişi hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="63939-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="63939-252">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="63939-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="63939-253">Azure Geçiş’e genel bakış</span><span class="sxs-lookup"><span data-stu-id="63939-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="63939-254">.NET ile WCF geçişi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="63939-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com
