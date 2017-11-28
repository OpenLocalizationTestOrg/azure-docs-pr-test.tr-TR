---
title: "Azure hizmet veri yolu WCF geçiş Öğreticisi | Microsoft Docs"
description: "Service Bus istemci uygulaması ve hizmeti WCF geçiş kullanarak oluşturun."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 5347bf85cad32b59677369d51a1f36529aef6662
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="608bb-103">Azure WCF geçiş Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="608bb-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="608bb-104">Bu öğretici basit bir WCF geçiş istemci uygulaması ve hizmeti Azure geçişi kullanarak nasıl oluşturulacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="608bb-104">This tutorial describes how to build a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="608bb-105">Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="608bb-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="608bb-106">Bu öğreticide, bir anlayış WCF geçiş istemci ve hizmet uygulaması oluşturmak için gereken adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-106">Working through this tutorial gives you an understanding of the steps that are required to create a WCF Relay client and service application.</span></span> <span data-ttu-id="608bb-107">Özgün WCF hizmetindeki benzerlerinde gibi bir hizmet her biri bir veya daha fazla hizmet işlemini kullanıma sunar, bir veya daha fazla uç noktaları, kullanıma sunan bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="608bb-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="608bb-108">Bir hizmetin uç noktası hizmetin bulunabileceği bir adres, istemcinin hizmetle iletişiminde paylaşması gereken bilgileri içeren bir bağlama ve hizmet tarafından istemcilerine sağlanan işlevselliği tanımlayan bir sözleşme belirtir.</span><span class="sxs-lookup"><span data-stu-id="608bb-108">The endpoint of a service specifies an address where the service can be found, a binding that contains the information that a client must communicate with the service, and a contract that defines the functionality provided by the service to its clients.</span></span> <span data-ttu-id="608bb-109">WCF ve WCF geçiş arasındaki temel fark, uç noktanın yerel olarak bilgisayarınızda yerine bulutta sunulur ' dir.</span><span class="sxs-lookup"><span data-stu-id="608bb-109">The main difference between WCF and WCF Relay is that the endpoint is exposed in the cloud instead of locally on your computer.</span></span>

<span data-ttu-id="608bb-110">Bu öğreticideki konu başlıklarını sırasıyla anlayıp uyguladıktan sonra çalışan bir hizmetiniz ve hizmetin işlemlerini çağırabilen bir istemciniz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="608bb-110">After you work through the sequence of topics in this tutorial, you will have a running service, and a client that can invoke the operations of the service.</span></span> <span data-ttu-id="608bb-111">İlk konu başlığında nasıl hesap ayarlanacağı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="608bb-111">The first topic describes how to set up an account.</span></span> <span data-ttu-id="608bb-112">Sonraki adımlarda sözleşme kullanan bir hizmet tanımlama, hizmeti uygulama ve koddaki hizmeti yapılandırma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-112">The next steps describe how to define a service that uses a contract, how to implement the service, and how to configure the service in code.</span></span> <span data-ttu-id="608bb-113">Ayrıca, hizmeti çalıştırma ve barındırma da açıklanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-113">They also describe how to host and run the service.</span></span> <span data-ttu-id="608bb-114">Oluşturan hizmet kendiliğinden barındırılır ve aynı bilgisayarda çalışır.</span><span class="sxs-lookup"><span data-stu-id="608bb-114">The service that is created is self-hosted and the client and service run on the same computer.</span></span> <span data-ttu-id="608bb-115">Hizmeti bir kod veya yapılandırma dosyası kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-115">You can configure the service by using either code or a configuration file.</span></span>

<span data-ttu-id="608bb-116">Son üç adımda istemci uygulaması oluşturma, istemci uygulamasını yapılandırma ve ana bilgisayarın işlevselliğine erişebilen bir istemci oluşturma ile bu istemciyi kullanma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-116">The final three steps describe how to create a client application, configure the client application, and create and use a client that can access the functionality of the host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="608bb-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="608bb-117">Prerequisites</span></span>

<span data-ttu-id="608bb-118">Bu öğreticiyi tamamlamak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="608bb-118">To complete this tutorial, you'll need the following:</span></span>

* <span data-ttu-id="608bb-119">[Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="608bb-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="608bb-120">Bu öğreticide Visual Studio 2017 kullanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="608bb-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="608bb-121">An active Azure account.</span></span> <span data-ttu-id="608bb-122">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="608bb-123">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="608bb-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="608bb-124">Hizmet ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="608bb-124">Create a service namespace</span></span>

<span data-ttu-id="608bb-125">İlk adım bir ad alanı oluşturmak için elde etmek için ise bir [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) anahtarı.</span><span class="sxs-lookup"><span data-stu-id="608bb-125">The first step is to create a namespace, and to obtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="608bb-126">Bir ad alanı aracılığıyla geçiş hizmetine kullanıma sunulan her uygulama için bir uygulama sınırı sağlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-126">A namespace provides an application boundary for each application exposed through the relay service.</span></span> <span data-ttu-id="608bb-127">Hizmet ad alanı oluşturulduğunda sistem tarafından otomatik olarak bir SAS anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="608bb-127">A SAS key is automatically generated by the system when a service namespace is created.</span></span> <span data-ttu-id="608bb-128">Hizmet ad alanı ve SAS anahtarı birleşimi, bir uygulamaya erişim kimliğini doğrulamak Azure için kimlik bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-128">The combination of service namespace and SAS key provides the credentials for Azure to authenticate access to an application.</span></span> <span data-ttu-id="608bb-129">[Buradaki yönergeleri](relay-create-namespace-portal.md) izleyerek bir Geçiş ad alanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-129">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="608bb-130">WCF hizmet sözleşmesini tanımlama</span><span class="sxs-lookup"><span data-stu-id="608bb-130">Define a WCF service contract</span></span>

<span data-ttu-id="608bb-131">Hizmet sözleşmesi hangi işlemleri belirtir (yöntemler ve işlevlere web hizmeti terminolojisi) hizmeti destekler.</span><span class="sxs-lookup"><span data-stu-id="608bb-131">The service contract specifies what operations (the web service terminology for methods or functions) the service supports.</span></span> <span data-ttu-id="608bb-132">Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="608bb-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="608bb-133">Arabirimdeki her yöntem belirli bir hizmet işlemine karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="608bb-133">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="608bb-134">Her arabirimde [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğinin ve her işlemde de [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliğinin uygulanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-134">Each interface must have the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied to it, and each operation must have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied to it.</span></span> <span data-ttu-id="608bb-135">[ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğini içeren bir arabirimdeki yöntem [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliğine sahip değilse bu yöntem kullanıma sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="608bb-135">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="608bb-136">Bu görevlere ilişkin kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-136">The code for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="608bb-137">Sözleşmeler ve hizmetlere ilişkin daha fazla bilgi için WCF belgelerinde bulunan [Hizmetleri Tasarlama ve Uygulama](https://msdn.microsoft.com/library/ms729746.aspx) başlığına bakın.</span><span class="sxs-lookup"><span data-stu-id="608bb-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in the WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="608bb-138">Geçiş sözleşme sahip bir arabirim oluşturma</span><span class="sxs-lookup"><span data-stu-id="608bb-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="608bb-139">**Başlat** menüsünde programa sağ tıklayıp **Yönetici olarak çalıştır** seçeneğini belirleyip Visual Studio'yu yönetici olarak açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-139">Open Visual Studio as an administrator by right-clicking the program in the **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="608bb-140">Yeni bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-140">Create a new console application project.</span></span> <span data-ttu-id="608bb-141">**Dosya** menüsüne tıklayın, **Yeni** seçeneği belirleyin ve ardından **Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-141">Click the **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="608bb-142">**Yeni Proje** iletişim kutusunda, **Visual C#** öğesine tıklayın (**Visual C#** görünmezse **Diğer Diller** bölümüne bakın).</span><span class="sxs-lookup"><span data-stu-id="608bb-142">In the **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="608bb-143">Tıklatın **konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="608bb-143">Click the **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="608bb-144">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-144">Click **OK** to create the project.</span></span>

    ![][2]

3. <span data-ttu-id="608bb-145">Service Bus NuGet paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-145">Install the Service Bus NuGet package.</span></span> <span data-ttu-id="608bb-146">Bu paket otomatik olarak Service Bus kitaplıklarının yanı sıra WCF **System.ServiceModel** öğesine de başvurular ekler.</span><span class="sxs-lookup"><span data-stu-id="608bb-146">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="608bb-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx), WCF'nin temel özelliklerine programlamayla erişmenizi sağlayan ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="608bb-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables you to programmatically access the basic features of WCF.</span></span> <span data-ttu-id="608bb-148">Service Bus, hizmet sözleşmelerini tanımlamak için WCF'nin birçok nesnesini ve özniteliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-148">Service Bus uses many of the objects and attributes of WCF to define service contracts.</span></span>

    <span data-ttu-id="608bb-149">Çözüm Gezgini'nde projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet...** .</span><span class="sxs-lookup"><span data-stu-id="608bb-149">In Solution Explorer, right-click the project, and then click **Manage NuGet Packages...**.</span></span> <span data-ttu-id="608bb-150">**Gözat** sekmesine tıklayıp `Microsoft Azure Service Bus` için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="608bb-150">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="608bb-151">**Sürüm(ler)** kutusunda proje adının seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="608bb-151">Ensure that the project name is selected in the **Version(s)** box.</span></span> <span data-ttu-id="608bb-152">**Yükle**'ye tıklayın ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="608bb-152">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="608bb-153">Çözüm Gezgini'nde, zaten açılmamışsa Program.cs dosyasına çift tıklayarak dosyayı düzenleyicide açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-153">In Solution Explorer, double-click the Program.cs file to open it in the editor, if it is not already open.</span></span>
5. <span data-ttu-id="608bb-154">Aşağıdaki using deyimlerini dosyanın üst tarafına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="608bb-154">Add the following using statements at the top of the file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="608bb-155">Ad alanındaki varsayılan ad olan **EchoService**'i **Microsoft.ServiceBus.Samples** olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="608bb-155">Change the namespace name from its default name of **EchoService** to **Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="608bb-156">Bu öğretici C# ad alanı kullanır **Microsoft.ServiceBus.Samples**, ad alanı sözleşme tabanlı olduğu yönetilen yapılandırma dosyasında kullanılan türü [WCF istemcisini yapılandırma](#configure-the-wcf-client) adım.</span><span class="sxs-lookup"><span data-stu-id="608bb-156">This tutorial uses the C# namespace **Microsoft.ServiceBus.Samples**, which is the namespace of the contract-based managed type that is used in the configuration file in the [Configure the WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="608bb-157">Bu örneği derlemek istediğinizde herhangi bir ad alanını kullanabilirsiniz ancak uygulama yapılandırma dosyasında sözleşmenin ve hizmetin ad alanlarını uygun şekilde değiştirmezseniz bu öğretici çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="608bb-157">You can specify any namespace you want when you build this sample; however, the tutorial will not work unless you then modify the namespaces of the contract and service accordingly, in the application configuration file.</span></span> <span data-ttu-id="608bb-158">App.config dosyasında belirtilen ad alanının C# dosyalarınızda belirtilen ad alanıyla aynı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-158">The namespace specified in the App.config file must be the same as the namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="608bb-159">Hemen sonra `Microsoft.ServiceBus.Samples` ad alanı bildirimi, ancak ad alanı içinde adlı yeni arabirimi tanımlayın `IEchoContract` ve uygulama `ServiceContractAttribute` öznitelik ad alanı değerini içeren arabirime `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="608bb-159">Directly after the `Microsoft.ServiceBus.Samples` namespace declaration, but within the namespace, define a new interface named `IEchoContract` and apply the `ServiceContractAttribute` attribute to the interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="608bb-160">Kodunuzun kapsamında kullandığınız ad alanı ile ad alanı değeri farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-160">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="608bb-161">Ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="608bb-161">Instead, the namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="608bb-162">Ad alanını açıkça belirlemek, varsayılan ad alanı değerinin sözleşme adına eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="608bb-162">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span> <span data-ttu-id="608bb-163">Ad alanı bildiriminin sonra aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="608bb-163">Paste the following code after the namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="608bb-164">Genellikle, hizmet sözleşmesi ad alanı sürüm bilgilerini barındıran bir adlandırma şeması içerir.</span><span class="sxs-lookup"><span data-stu-id="608bb-164">Typically, the service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="608bb-165">Sürüm bilgilerini hizmet sözleşmesi ad alanına dahil etmek, hizmetlerin yeni bir ad alanı içeren yeni bir hizmet sözleşmesi tanımlayarak ve bu sözleşmeyi yeni bir uç noktada kullanıma sunarak büyük değişiklikleri yalıtmalarına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-165">Including version information in the service contract namespace enables services to isolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="608bb-166">Bu şekilde, istemciler güncelleştirmeye gerek kalmadan eski hizmet sözleşmelerini kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-166">In this manner, clients can continue to use the old service contract without having to be updated.</span></span> <span data-ttu-id="608bb-167">Sürüm bilgileri, bir tarihten veya bir derleme numarasından oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="608bb-167">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="608bb-168">Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="608bb-168">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="608bb-169">Bu öğreticinin amaçları doğrultusunda, hizmet sözleşmesi ad alanının adlandırma şeması sürüm bilgilerini içermez.</span><span class="sxs-lookup"><span data-stu-id="608bb-169">For the purposes of this tutorial, the naming scheme of the service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="608bb-170">İçinde `IEchoContract` arabirim, tek bir işlem için bir yöntem bildirin `IEchoContract` sözleşme arabirimde kullanıma sunduğu ve uygulama `OperationContractAttribute` öznitelik gibi genel WCF geçiş sözleşmesinin bir parçası olarak kullanıma sunmak istediğiniz yönteme:</span><span class="sxs-lookup"><span data-stu-id="608bb-170">Within the `IEchoContract` interface, declare a method for the single operation the `IEchoContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="608bb-171">`IEchoContract` arabirimi tanımından hemen sonra, aşağıda belirtildiği şekilde `IEchoContract` ve `IClientChannel` arabirimlerinden devralma işlemini gerçekleştiren bir kanal bildirin:</span><span class="sxs-lookup"><span data-stu-id="608bb-171">Directly after the `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also to the `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="608bb-172">Kanal, ana bilgisayar ve istemcinin bilgileri birbirlerine göndermek için kullandıkları WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="608bb-172">A channel is the WCF object through which the host and client pass information to each other.</span></span> <span data-ttu-id="608bb-173">Daha sonra, iki uygulama arasındaki bilgileri yansıtmak üzere kanalda kod yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="608bb-173">Later, you will write code against the channel to echo information between the two applications.</span></span>
10. <span data-ttu-id="608bb-174">Çalışmanızın o ana kadarki doğruluğunu onaylamak için **Derle** menüsünde **Çözümü Derle**'ye tıklayın veya **Ctrl+Shift+B**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-174">From the **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="608bb-175">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-175">Example</span></span>

<span data-ttu-id="608bb-176">Aşağıdaki kod bir WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-176">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="608bb-177">Oluşturulması tamamlandığına göre arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-177">Now that the interface is created, you can implement the interface.</span></span>

## <a name="implement-the-wcf-contract"></a><span data-ttu-id="608bb-178">WCF sözleşmesi uygulama</span><span class="sxs-lookup"><span data-stu-id="608bb-178">Implement the WCF contract</span></span>

<span data-ttu-id="608bb-179">Bir Azure geçişi oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan sözleşmeyi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-179">Creating an Azure relay requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="608bb-180">Arabirimi oluşturma hakkında daha fazla bilgi edinmek için önceki adıma bakın.</span><span class="sxs-lookup"><span data-stu-id="608bb-180">For more information about creating the interface, see the previous step.</span></span> <span data-ttu-id="608bb-181">Bir sonraki adım ise bu arabirimi uygulamaktır.</span><span class="sxs-lookup"><span data-stu-id="608bb-181">The next step is to implement the interface.</span></span> <span data-ttu-id="608bb-182">Bu adımda kullanıcı tanımlı `IEchoContract` arabirimini uygulayan `EchoService` adlı bir sınıf oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="608bb-182">This involves creating a class named `EchoService` that implements the user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="608bb-183">Arabirimi uyguladıktan sonra, bir App.config yapılandırma dosyası kullanarak arabirimi yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="608bb-183">After you implement the interface, you then configure the interface using an App.config configuration file.</span></span> <span data-ttu-id="608bb-184">Yapılandırma dosyasında hizmetin adı, sözleşmenin ve geçiş hizmeti ile iletişim kurmak için kullanılan protokol türü adı gibi uygulama için gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="608bb-184">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="608bb-185">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-185">The code used for these tasks is provided in the example following the procedure.</span></span> <span data-ttu-id="608bb-186">Hizmet sözleşmesini uygulama konusunda daha genel bilgiler için WCF belgelerinde [Hizmet Sözleşmelerini Uygulama](https://msdn.microsoft.com/library/ms733764.aspx) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="608bb-186">For a more general discussion about how to implement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in the WCF documentation.</span></span>

1. <span data-ttu-id="608bb-187">`IEchoContract` arabiriminin tanımından hemen sonra `EchoService` adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-187">Create a new class named `EchoService` directly after the definition of the `IEchoContract` interface.</span></span> <span data-ttu-id="608bb-188">`EchoService` sınıfı, `IEchoContract` arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="608bb-188">The `EchoService` class implements the `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="608bb-189">Diğer arabirim uygulamalarına benzer şekilde, tanımı farklı bir dosyada uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-189">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="608bb-190">Ancak bu öğreticide uygulama, arabirim tanımı ve `Main` yöntemiyle aynı dosyadadır.</span><span class="sxs-lookup"><span data-stu-id="608bb-190">However, for this tutorial, the implementation is located in the same file as the interface definition and the `Main` method.</span></span>
2. <span data-ttu-id="608bb-191">`IEchoContract` arabirimine [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) özniteliğini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-191">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the `IEchoContract` interface.</span></span> <span data-ttu-id="608bb-192">Öznitelik, hizmet adını ve ad alanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="608bb-192">The attribute specifies the service name and namespace.</span></span> <span data-ttu-id="608bb-193">Bunu yaptıktan sonra `EchoService` sınıfı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="608bb-193">After doing so, the `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="608bb-194">`EchoService` sınıfındaki `IEchoContract` arabiriminde tanımlanan `Echo` yöntemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-194">Implement the `Echo` method defined in the `IEchoContract` interface in the `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="608bb-195">Çalışmanızın doğruluğunu onaylamak için **Derle** menüsünde **Çözümü Derle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-195">Click **Build**, then click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="define-the-configuration-for-the-service-host"></a><span data-ttu-id="608bb-196">Hizmet ana bilgisayarı yapılandırmasını tanımlama</span><span class="sxs-lookup"><span data-stu-id="608bb-196">Define the configuration for the service host</span></span>

1. <span data-ttu-id="608bb-197">Yapılandırma dosyası, WCF yapılandırma dosyasına büyük ölçüde benzer.</span><span class="sxs-lookup"><span data-stu-id="608bb-197">The configuration file is very similar to a WCF configuration file.</span></span> <span data-ttu-id="608bb-198">Hizmet adını, uç noktayı (diğer bir deyişle, istemcilerin ve ana bilgisayarların birbirleriyle iletişim kurmak Azure geçiş gösteren konum) ve bağlamayı içerir (iletişim kurmak için kullanılan protokol türü).</span><span class="sxs-lookup"><span data-stu-id="608bb-198">It includes the service name, endpoint (that is, the location that Azure Relay exposes for clients and hosts to communicate with each other), and the binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="608bb-199">Yapılandırma dosyasının temel farkı, bu durumda yapılandırılan hizmet uç noktasının .NET Framework'ün bir parçası olmayan [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) bağlamasına başvuru sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="608bb-199">The main difference is that this configured service endpoint refers to a [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of the .NET Framework.</span></span> <span data-ttu-id="608bb-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hizmet tarafından tanımlanan bağlamalardan biridir.</span><span class="sxs-lookup"><span data-stu-id="608bb-200">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of the bindings defined by the service.</span></span>
2. <span data-ttu-id="608bb-201">**Çözüm Gezgini**'nde, App.config dosyasına çift tıklayarak dosyayı Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-201">In **Solution Explorer**, double-click the App.config file to open it in the Visual Studio editor.</span></span>
3. <span data-ttu-id="608bb-202">`<appSettings>` öğesinde, yer tutucuları hizmet ad alanınızdaki adla ve önceki adımların birinde kopyaladığınız SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="608bb-202">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="608bb-203">`<system.serviceModel>` etiketleri içinde, bir `<services>` öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-203">Within the `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="608bb-204">Bir tek yapılandırma dosyasında birden çok geçiş uygulamaları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-204">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="608bb-205">Ancak bu öğreticide yalnızca bir adet tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-205">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="608bb-206">`<services>` öğesi içinde, hizmetin adını tanımlamak için `<service>` öğesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-206">Within the `<services>` element, add a `<service>` element to define the name of the service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="608bb-207">`<service>` öğesi içinde, uç nokta sözleşmesinin konumunu ve uç noktaya yönelik bağlama türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-207">Within the `<service>` element, define the location of the endpoint contract, and also the type of binding for the endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="608bb-208">Uç nokta, istemcinin ana bilgisayar uygulamasını nerede arayacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-208">The endpoint defines where the client will look for the host application.</span></span> <span data-ttu-id="608bb-209">Daha sonra öğretici Azure geçiş aracılığıyla ana bilgisayarı tamamen kullanıma sunan bir URI oluşturmak için bu adımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-209">Later, the tutorial uses this step to create a URI that fully exposes the host through Azure Relay.</span></span> <span data-ttu-id="608bb-210">Bağlama TCP protokol olarak geçiş hizmeti ile iletişim kurmak için kullanıyoruz olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="608bb-210">The binding declares that we are using TCP as the protocol to communicate with the relay service.</span></span>
7. <span data-ttu-id="608bb-211">Çalışmanızın doğruluğunu onaylamak için **Derle** menüsüne ve **Çözümü Derle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-211">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="608bb-212">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-212">Example</span></span>

<span data-ttu-id="608bb-213">Aşağıdaki kod, hizmet sözleşmesinin uygulamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-213">The following code shows the implementation of the service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="608bb-214">Aşağıdaki kod, hizmet ana bilgisayarı ile ilişkilendirilen App.config dosyasının temel biçimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-214">The following code shows the basic format of the App.config file associated with the service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-to-register-with-the-relay-service"></a><span data-ttu-id="608bb-215">Geçiş hizmeti ile kaydetmek için bir temel web hizmeti barındırma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="608bb-215">Host and run a basic web service to register with the relay service</span></span>

<span data-ttu-id="608bb-216">Bu adım, bir Azure geçiş hizmetini çalıştırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="608bb-216">This step describes how to run an Azure Relay service.</span></span>

### <a name="create-the-relay-credentials"></a><span data-ttu-id="608bb-217">Geçiş kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="608bb-217">Create the relay credentials</span></span>

1. <span data-ttu-id="608bb-218">`Main()` içinde, konsol penceresinden okunan ad alanını ve SAS anahtarını depolayabileceğiniz iki değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-218">In `Main()`, create two variables in which to store the namespace and the SAS key that are read from the console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="608bb-219">SAS anahtarını daha sonra projenize erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="608bb-219">The SAS key will be used later to access your project.</span></span> <span data-ttu-id="608bb-220">Ad alanı, Hizmet URI'si oluşturmak için `CreateServiceUri` öğesine bir parametre olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="608bb-220">The namespace is passed as a parameter to `CreateServiceUri` to create a service URI.</span></span>
2. <span data-ttu-id="608bb-221">[TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) nesnesi kullanarak, kimlik bilgisi türü için SAS anahtarı kullanacağınızı bildirin.</span><span class="sxs-lookup"><span data-stu-id="608bb-221">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as the credential type.</span></span> <span data-ttu-id="608bb-222">Aşağıdaki kodu son adımda eklenen koddan hemen sonra ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-222">Add the following code directly after the code added in the last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-the-service"></a><span data-ttu-id="608bb-223">Hizmetin taban adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="608bb-223">Create a base address for the service</span></span>

<span data-ttu-id="608bb-224">Son adımda eklediğiniz kodun hemen ardından, oluşturma bir `Uri` hizmetin taban adresine örneği.</span><span class="sxs-lookup"><span data-stu-id="608bb-224">After the code you added in the last step, create a `Uri` instance for the base address of the service.</span></span> <span data-ttu-id="608bb-225">Bu URI; Service Bus şemasını, ad alanını ve hizmet arabiriminin yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="608bb-225">This URI specifies the Service Bus scheme, the namespace, and the path of the service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="608bb-226">"sb", Service Bus şeması için kullanılan bir kısaltmadır ve protokol olarak TCP'yi kullandığımızı belirtir.</span><span class="sxs-lookup"><span data-stu-id="608bb-226">"sb" is an abbreviation for the Service Bus scheme, and indicates that we are using TCP as the protocol.</span></span> <span data-ttu-id="608bb-227">Ayrıca bu durum, [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) bağlama olarak sunulduğunda da yapılandırma dosyasında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="608bb-227">This was also previously indicated in the configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as the binding.</span></span>

<span data-ttu-id="608bb-228">Bu öğretici için URI şudur: `sb://putServiceNamespaceHere.windows.net/EchoService`</span><span class="sxs-lookup"><span data-stu-id="608bb-228">For this tutorial, the URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-the-service-host"></a><span data-ttu-id="608bb-229">Oluşturma ve hizmet ana bilgisayarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="608bb-229">Create and configure the service host</span></span>

1. <span data-ttu-id="608bb-230">Bağlantı modunu `AutoDetect` olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-230">Set the connectivity mode to `AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="608bb-231">Bağlantı modunu hizmetin geçiş hizmeti ile iletişim için kullandığı protokolü açıklar; HTTP veya TCP.</span><span class="sxs-lookup"><span data-stu-id="608bb-231">The connectivity mode describes the protocol the service uses to communicate with the relay service; either HTTP or TCP.</span></span> <span data-ttu-id="608bb-232">Varsayılan ayarı kullanarak `AutoDetect`, hizmet TCP kullanılabilir değilse Azure geçiş amacıyla kullanılabilir durumdaysa TCP ve HTTP üzerinden bağlanma girişiminde bulunur.</span><span class="sxs-lookup"><span data-stu-id="608bb-232">Using the default setting `AutoDetect`, the service attempts to connect to Azure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="608bb-233">Bu durumun hizmetin istemci iletişimi için belirttiği protokole göre değişebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-233">Note that this differs from the protocol the service specifies for client communication.</span></span> <span data-ttu-id="608bb-234">Bu protokol, kullanılan bağlamaya göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="608bb-234">That protocol is determined by the binding used.</span></span> <span data-ttu-id="608bb-235">Örneğin, bir hizmet kullanabilirsiniz [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) , uç noktasında istemcileriyle HTTP üzerinden iletişim kurduğu bağlama.</span><span class="sxs-lookup"><span data-stu-id="608bb-235">For example, a service can use the [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="608bb-236">Aynı hizmeti belirtebilirsiniz **ConnectivityMode.AutoDetect** hizmeti ile Azure geçişi TCP üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="608bb-236">That same service could specify **ConnectivityMode.AutoDetect** so that the service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="608bb-237">Bu bölümün önceki kısımlarında oluşturduğunuz URI'yi kullanarak hizmet ana bilgisayarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-237">Create the service host, using the URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="608bb-238">Hizmet ana bilgisayarı, hizmetin örneğini oluşturan WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="608bb-238">The service host is the WCF object that instantiates the service.</span></span> <span data-ttu-id="608bb-239">Burada, hizmet ana bilgisayarını oluşturmak istediğiniz hizmet türüne (bir `EchoService` türü) ve hizmeti kullanıma sunmak istediğiniz adrese geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-239">Here, you pass it the type of service you want to create (an `EchoService` type), and also to the address at which you want to expose the service.</span></span>
3. <span data-ttu-id="608bb-240">Program.cs dosyasının üst kısmında, [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) ve [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description) öğelerine başvurular ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-240">At the top of the Program.cs file, add references to [System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="608bb-241">`Main()` öğesine geri dönüp, genel erişimi etkinleştirmek için uç noktayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="608bb-241">Back in `Main()`, configure the endpoint to enable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="608bb-242">Bu adımı uygulamanız genel olarak projeniz için akış ATOM incelenerek bulunabilir geçiş hizmeti bildirir.</span><span class="sxs-lookup"><span data-stu-id="608bb-242">This step informs the relay service that your application can be found publicly by examining the ATOM feed for your project.</span></span> <span data-ttu-id="608bb-243">**DiscoveryType** kısmını **özel** olarak ayarlarsanız bir istemci yine de hizmete erişebilir.</span><span class="sxs-lookup"><span data-stu-id="608bb-243">If you set **DiscoveryType** to **private**, a client would still be able to access the service.</span></span> <span data-ttu-id="608bb-244">Ancak, geçiş ad alanı aratıldığında hizmet görünmez.</span><span class="sxs-lookup"><span data-stu-id="608bb-244">However, the service would not appear when it searches the Relay namespace.</span></span> <span data-ttu-id="608bb-245">Bunun yerine, istemcinin uç nokta yolunu önceden bilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-245">Instead, the client would have to know the endpoint path beforehand.</span></span>
5. <span data-ttu-id="608bb-246">App.config dosyasında açıklanan hizmet uç noktalarına hizmet kimlik bilgilerini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="608bb-246">Apply the service credentials to the service endpoints defined in the App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="608bb-247">Bir önceki adımda da belirtildiği üzere, yapılandırma dosyasında birden çok hizmet ve uç nokta bildirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-247">As stated in the previous step, you could have declared multiple services and endpoints in the configuration file.</span></span> <span data-ttu-id="608bb-248">Birden çok hizmet ve uç nokta bildirirseniz bu kod yapılandırma dosyasına çapraz geçiş yapar ve kimlik bilgilerinin uygulanacağı tüm uç noktalara yönelik arama yapar.</span><span class="sxs-lookup"><span data-stu-id="608bb-248">If you had, this code would traverse the configuration file and search for every endpoint to which it should apply your credentials.</span></span> <span data-ttu-id="608bb-249">Ancak bu öğreticide yapılandırma dosyasının yalnızca bir uç noktası vardır.</span><span class="sxs-lookup"><span data-stu-id="608bb-249">However, for this tutorial, the configuration file has only one endpoint.</span></span>

### <a name="open-the-service-host"></a><span data-ttu-id="608bb-250">Hizmet ana bilgisayarını açma</span><span class="sxs-lookup"><span data-stu-id="608bb-250">Open the service host</span></span>

1. <span data-ttu-id="608bb-251">Hizmeti açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-251">Open the service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="608bb-252">Kullanıcıyı hizmetin çalıştığı konusunda bilgilendirin ve hizmetin nasıl kapatılacağını açıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-252">Inform the user that the service is running, and explain how to shut down the service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="608bb-253">Bu işlemi bitirdiğinizde, hizmet ana bilgisayarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="608bb-253">When finished, close the service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="608bb-254">Projeyi derlemek için **Ctrl+Shift+B**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-254">Press **Ctrl+Shift+B** to build the project.</span></span>

### <a name="example"></a><span data-ttu-id="608bb-255">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-255">Example</span></span>

<span data-ttu-id="608bb-256">Tamamlanmış hizmet kodunuzun şu şekilde görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="608bb-256">Your completed service code should appear as follows.</span></span> <span data-ttu-id="608bb-257">Kod hizmet sözleşmesini ve önceki kısımlarında öğreticide içerir ve hizmeti bir konsol uygulamasında barındırır.</span><span class="sxs-lookup"><span data-stu-id="608bb-257">The code includes the service contract and implementation from previous steps in the tutorial, and hosts the service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create the credentials object for the endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create the service URI based on the service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create the service host reading the configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create the ServiceRegistrySettings behavior for the endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add the Relay credentials to all endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open the service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            // Close the service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-the-service-contract"></a><span data-ttu-id="608bb-258">Hizmet sözleşmesi için bir WCF istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="608bb-258">Create a WCF client for the service contract</span></span>

<span data-ttu-id="608bb-259">Sonraki adım, bir istemci uygulaması oluşturun ve daha sonraki adımlarda gerçekleştireceksiniz hizmet sözleşmesini tanımlayan olmaktır.</span><span class="sxs-lookup"><span data-stu-id="608bb-259">The next step is to create a client application and define the service contract you will implement in later steps.</span></span> <span data-ttu-id="608bb-260">Bu adımların bir hizmet oluşturmak için kullanılan adımlara benzer olduğunu unutmayın: dosya, geçiş hizmetine bağlanmak için kimlik bilgilerini kullanarak ve benzeri bir App.config düzenleme sözleşme tanımlama.</span><span class="sxs-lookup"><span data-stu-id="608bb-260">Note that many of these steps resemble the steps used to create a service: defining a contract, editing an App.config file, using credentials to connect to the relay service, and so on.</span></span> <span data-ttu-id="608bb-261">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-261">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="608bb-262">Aşağıdaki işlemleri gerçekleştirerek geçerli Visual Studio çözümünde istemci için yeni bir proje oluşturun:</span><span class="sxs-lookup"><span data-stu-id="608bb-262">Create a new project in the current Visual Studio solution for the client by doing the following:</span></span>

   1. <span data-ttu-id="608bb-263">Çözüm Gezgini'nde, hizmetin barındıran çözümde bulunan geçerli çözüme (projeye değil) sağ tıklayın ve **Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-263">In Solution Explorer, in the same solution that contains the service, right-click the current solution (not the project), and click **Add**.</span></span> <span data-ttu-id="608bb-264">Ardından **Yeni Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-264">Then click **New Project**.</span></span>
   2. <span data-ttu-id="608bb-265">İçinde **Yeni Proje Ekle** iletişim kutusu, tıklatın **Visual C#** (varsa **Visual C#** görüntülenmiyorsa, altında Ara **diğer diller**) seçin **Konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="608bb-265">In the **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select the **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="608bb-266">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-266">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="608bb-267">Çözüm Gezgini'nde, **EchoClient** projesindeki Program.cs dosyasına çift tıklayarak düzenleyicide açın (zaten açılmış durumda değilse).</span><span class="sxs-lookup"><span data-stu-id="608bb-267">In Solution Explorer, double-click the Program.cs file in the **EchoClient** project to open it in the editor, if it is not already open.</span></span>
3. <span data-ttu-id="608bb-268">`EchoClient` olan varsayılan ad alanı adını `Microsoft.ServiceBus.Samples` olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="608bb-268">Change the namespace name from its default name of `EchoClient` to `Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="608bb-269">Yükleme [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus): Çözüm Gezgini'nde sağ **EchoClient** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="608bb-269">Install the [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click the **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="608bb-270">**Gözat** sekmesine tıklayıp `Microsoft Azure Service Bus` için arama yapın.</span><span class="sxs-lookup"><span data-stu-id="608bb-270">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="608bb-271">**Yükle**'ye tıklayın ve kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="608bb-271">Click **Install**, and accept the terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="608bb-272">Program.cs dosyasındaki [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) ad alanı için `using` deyimini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-272">Add a `using` statement for the [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in the Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="608bb-273">Hizmet sözleşmesi tanımını ad alanına aşağıdaki örnekte gösterilen şekilde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-273">Add the service contract definition to the namespace, as shown in the following example.</span></span> <span data-ttu-id="608bb-274">Bu tanımın **Service** projesinde kullanılan tanımla aynı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-274">Note that this definition is identical to the definition used in the **Service** project.</span></span> <span data-ttu-id="608bb-275">Bu kodu `Microsoft.ServiceBus.Samples` ad alanının üstüne eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-275">You should add this code at the top of the `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="608bb-276">İstemciyi derlemek için **Ctrl+Shift+B**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-276">Press **Ctrl+Shift+B** to build the client.</span></span>

### <a name="example"></a><span data-ttu-id="608bb-277">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-277">Example</span></span>

<span data-ttu-id="608bb-278">Aşağıdaki kodu Program.cs dosyasında geçerli durumunu gösteren **EchoClient** projesi.</span><span class="sxs-lookup"><span data-stu-id="608bb-278">The following code shows the current status of the Program.cs file in the **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-the-wcf-client"></a><span data-ttu-id="608bb-279">WCF istemcisini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="608bb-279">Configure the WCF client</span></span>

<span data-ttu-id="608bb-280">Bu adımda, daha önce bu öğreticide oluşturduğunuz hizmete erişen temel istemci uygulamasına yönelik bir App.config dosyası oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="608bb-280">In this step, you create an App.config file for a basic client application that accesses the service created previously in this tutorial.</span></span> <span data-ttu-id="608bb-281">Bu App.config dosyası sözleşmeyi, bağlamayı ve uç noktanın adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-281">This App.config file defines the contract, binding, and name of the endpoint.</span></span> <span data-ttu-id="608bb-282">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-282">The code used for these tasks is provided in the example following the procedure.</span></span>

1. <span data-ttu-id="608bb-283">Çözüm Gezgini'nde, **EchoClient** projesinde bulunan **App.config** dosyasına çift tıklayarak dosyayı Visual Studio düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-283">In Solution Explorer, in the **EchoClient** project, double-click **App.config** to open the file in the Visual Studio editor.</span></span>
2. <span data-ttu-id="608bb-284">`<appSettings>` öğesinde, yer tutucuları hizmet ad alanınızdaki adla ve önceki adımların birinde kopyaladığınız SAS anahtarı ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="608bb-284">In the `<appSettings>` element, replace the placeholders with the name of your service namespace, and the SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="608bb-285">system.serviceModel öğesi içinde `<client>` öğesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-285">Within the system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="608bb-286">Bu adım ile WCF stilinde istemci uygulaması tanımladığınızı bildirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-286">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="608bb-287">`client` öğesi içinde adı, sözleşmeyi ve uç noktaya yönelik bağlama türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-287">Within the `client` element, define the name, contract, and binding type for the endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="608bb-288">Bu adım, hizmet ve istemci uygulaması Azure geçiş ile iletişim kurmak için TCP kullandığı olgu tanımlanan sözleşme bitiş noktası adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-288">This step defines the name of the endpoint, the contract defined in the service, and the fact that the client application uses TCP to communicate with Azure Relay.</span></span> <span data-ttu-id="608bb-289">Uç nokta adı, bir sonraki adımda bu uç nokta yapılandırmasını hizmet URI'si ile bağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="608bb-289">The endpoint name is used in the next step to link this endpoint configuration with the service URI.</span></span>
5. <span data-ttu-id="608bb-290">Tıklatın **dosya**, ardından **Tümünü Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="608bb-290">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="608bb-291">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-291">Example</span></span>

<span data-ttu-id="608bb-292">Aşağıdaki kod, Echo istemciye yönelik App.config dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-292">The following code shows the App.config file for the Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-the-wcf-client"></a><span data-ttu-id="608bb-293">WCF istemcisini uygulama</span><span class="sxs-lookup"><span data-stu-id="608bb-293">Implement the WCF client</span></span>
<span data-ttu-id="608bb-294">Bu adımda, daha önce bu öğreticide oluşturduğunuz hizmete erişen bir temel istemci uygulaması yürütürsünüz.</span><span class="sxs-lookup"><span data-stu-id="608bb-294">In this step, you implement a basic client application that accesses the service you created previously in this tutorial.</span></span> <span data-ttu-id="608bb-295">Hizmete benzer şekilde, istemci Azure geçiş erişmek için aynı işlemlerin çoğunu gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="608bb-295">Similar to the service, the client performs many of the same operations to access Azure Relay:</span></span>

1. <span data-ttu-id="608bb-296">Bağlantı modunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-296">Sets the connectivity mode.</span></span>
2. <span data-ttu-id="608bb-297">Ana bilgisayar hizmetinin yer aldığı URI'yi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="608bb-297">Creates the URI that locates the host service.</span></span>
3. <span data-ttu-id="608bb-298">Güvenlik kimlik bilgilerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="608bb-298">Defines the security credentials.</span></span>
4. <span data-ttu-id="608bb-299">Bağlantıya kimlik bilgilerini uygular.</span><span class="sxs-lookup"><span data-stu-id="608bb-299">Applies the credentials to the connection.</span></span>
5. <span data-ttu-id="608bb-300">Bağlantıyı açar.</span><span class="sxs-lookup"><span data-stu-id="608bb-300">Opens the connection.</span></span>
6. <span data-ttu-id="608bb-301">Uygulamaya özgü görevleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="608bb-301">Performs the application-specific tasks.</span></span>
7. <span data-ttu-id="608bb-302">Bağlantıyı kapatır.</span><span class="sxs-lookup"><span data-stu-id="608bb-302">Closes the connection.</span></span>

<span data-ttu-id="608bb-303">Ancak, temel farklardan biri, hizmet için bir çağrı kullanır ancak istemci uygulamanın bir kanal geçiş hizmetine bağlanmak için kullanmasıdır **ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="608bb-303">However, one of the main differences is that the client application uses a channel to connect to the relay service, whereas the service uses a call to **ServiceHost**.</span></span> <span data-ttu-id="608bb-304">Bu görevler için kullanılan kod, aşağıdaki yordamın altındaki örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="608bb-304">The code used for these tasks is provided in the example following the procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="608bb-305">Bir istemci uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="608bb-305">Implement a client application</span></span>
1. <span data-ttu-id="608bb-306">Bağlantı modunu **AutoDetect** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-306">Set the connectivity mode to **AutoDetect**.</span></span> <span data-ttu-id="608bb-307">Aşağıdaki kodu **EchoClient** uygulamasının `Main()` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="608bb-307">Add the following code inside the `Main()` method of the **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="608bb-308">Konsoldan okunan hizmet ad alanı ve SAS anahtarına yönelik değerleri tutması için değişkenleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-308">Define variables to hold the values for the service namespace, and SAS key that are read from the console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="608bb-309">Geçiş Projenizde konak konumunu tanımlayan URI oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-309">Create the URI that defines the location of the host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="608bb-310">Hizmet ad alanı uç noktanız için kimlik bilgileri nesnesini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-310">Create the credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="608bb-311">App.config dosyasında tanımlanan yapılandırmayı yükleyen kanal fabrikasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="608bb-311">Create the channel factory that loads the configuration described in the App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="608bb-312">Kanal fabrikası, hizmet ve istemcinin iletişim kurmak için kullandığı bir kanal oluşturan WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="608bb-312">A channel factory is a WCF object that creates a channel through which the service and client applications communicate.</span></span>
6. <span data-ttu-id="608bb-313">Kimlik bilgileri geçerli.</span><span class="sxs-lookup"><span data-stu-id="608bb-313">Apply the credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="608bb-314">Kanalı oluşturup hizmet tarafından kullanılması için açın.</span><span class="sxs-lookup"><span data-stu-id="608bb-314">Create and open the channel to the service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="608bb-315">Yankı için işlevselliği ve temel kullanıcı arabirimini yazın.</span><span class="sxs-lookup"><span data-stu-id="608bb-315">Write the basic user interface and functionality for the echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text to echo (or [Enter] to exit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="608bb-316">Kanal nesnesi örneğinin kod tarafından hizmete yönelik bir ara sunucu olarak kullanıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-316">Note that the code uses the instance of the channel object as a proxy for the service.</span></span>
9. <span data-ttu-id="608bb-317">Kanalı ve fabrikayı kapatın.</span><span class="sxs-lookup"><span data-stu-id="608bb-317">Close the channel, and close the factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="608bb-318">Örnek</span><span class="sxs-lookup"><span data-stu-id="608bb-318">Example</span></span>

<span data-ttu-id="608bb-319">Tamamlanan kodu aşağıdaki gibi görünmelidir istemci uygulamasının nasıl oluşturulacağını, nasıl hizmet işlemlerini çağırma ve işlem çağrısından sonra istemciyi kapatma işlemlerinin nasıl gösteren tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="608bb-319">Your completed code should appear as follows, showing how to create a client application, how to call the operations of the service, and how to close the client after the operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text to echo (or [Enter] to exit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-the-applications"></a><span data-ttu-id="608bb-320">Uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="608bb-320">Run the applications</span></span>

1. <span data-ttu-id="608bb-321">Çözümü derlemek için **Ctrl+Shift+B**'ye basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-321">Press **Ctrl+Shift+B** to build the solution.</span></span> <span data-ttu-id="608bb-322">Bu işlem, daha önceki adımlarda oluşturduğunuz istemci ve hizmet projelerini derler.</span><span class="sxs-lookup"><span data-stu-id="608bb-322">This builds both the client project and the service project that you created in the previous steps.</span></span>
2. <span data-ttu-id="608bb-323">İstemci uygulamasını çalıştırmadan önce hizmet uygulamasının çalıştığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="608bb-323">Before running the client application, you must make sure that the service application is running.</span></span> <span data-ttu-id="608bb-324">Visual Studio'da bulunan Çözüm Gezgini'nde, **EchoService** çözümüne sağ tıklayın ve ardından **Özellikler**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-324">In Solution Explorer in Visual Studio, right-click the **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="608bb-325">Çözüm özellikleri iletişim kutusunda, **Başlangıç Projesi**'ne ve **Birden çok başlangıç projesi** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-325">In the solution properties dialog box, click **Startup Project**, then click the **Multiple startup projects** button.</span></span> <span data-ttu-id="608bb-326">**EchoService** çözümünün liste başında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="608bb-326">Make sure **EchoService** appears first in the list.</span></span>
4. <span data-ttu-id="608bb-327">**EchoService** ve **EchoClient** projeleri için **Eylem** kutusunu **Başlat** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-327">Set the **Action** box for both the **EchoService** and **EchoClient** projects to **Start**.</span></span>

    ![][5]
5. <span data-ttu-id="608bb-328">**Proje Bağımlılıkları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-328">Click **Project Dependencies**.</span></span> <span data-ttu-id="608bb-329">**Projeler** kutusunda **EchoClient** projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="608bb-329">In the **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="608bb-330">**Bağımlıdır** kutusunda **EchoService** projesinin seçildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="608bb-330">In the **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="608bb-331">**Özellikler** iletişim kutusunu kapatmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-331">Click **OK** to dismiss the **Properties** dialog.</span></span>
7. <span data-ttu-id="608bb-332">Her iki projeyi de çalıştırmak için **F5**'e basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-332">Press **F5** to run both projects.</span></span>
8. <span data-ttu-id="608bb-333">Her iki konsol penceresi de açılır ve sizden ad alanı adı ister.</span><span class="sxs-lookup"><span data-stu-id="608bb-333">Both console windows open and prompt you for the namespace name.</span></span> <span data-ttu-id="608bb-334">Öncelikle hizmetin çalıştırılması gerekir. **EchoService** konsol penceresinde ad alanına ad girin ve **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-334">The service must run first, so in the **EchoService** console window, enter the namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="608bb-335">Ardından SAS anahtarınız istenir.</span><span class="sxs-lookup"><span data-stu-id="608bb-335">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="608bb-336">SAS anahtarını girin ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-336">Enter the SAS key and press ENTER.</span></span>

    <span data-ttu-id="608bb-337">Konsol penceresinden örnek çıktı sunulur.</span><span class="sxs-lookup"><span data-stu-id="608bb-337">Here is example output from the console window.</span></span> <span data-ttu-id="608bb-338">Burada sağlanan değerlerin yalnızca örnek verme amacıyla oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-338">Note that the values provided here are for example purposes only.</span></span>

    <span data-ttu-id="608bb-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="608bb-339">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="608bb-340">Hizmet uygulaması, aşağıdaki örnekte görüldüğü şekilde konsol penceresini dinlediği adrese yazdırır.</span><span class="sxs-lookup"><span data-stu-id="608bb-340">The service application prints to the console window the address on which it's listening, as seen in the following example.</span></span>

    <span data-ttu-id="608bb-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span><span class="sxs-lookup"><span data-stu-id="608bb-341">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] to exit`</span></span>
10. <span data-ttu-id="608bb-342">**EchoClient** konsol penceresinde, az önce hizmet uygulaması için girdiğiniz bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="608bb-342">In the **EchoClient** console window, enter the same information that you entered previously for the service application.</span></span> <span data-ttu-id="608bb-343">İstemci uygulaması için aynı hizmet ad alanı ve SAS anahtarı değerlerini girmek üzere önceki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="608bb-343">Follow the previous steps to enter the same service namespace and SAS key values for the client application.</span></span>
11. <span data-ttu-id="608bb-344">Bu değerleri girdikten sonra istemci hizmete yönelik bir kanal açar ve aşağıdaki konsol çıktısı örneğinde görüldüğü şekilde bazı metinler girmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="608bb-344">After entering these values, the client opens a channel to the service and prompts you to enter some text as seen in the following console output example.</span></span>

    `Enter text to echo (or [Enter] to exit):`

    <span data-ttu-id="608bb-345">Hizmet uygulamasına gönderilecek metinleri girin ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-345">Enter some text to send to the service application and press Enter.</span></span> <span data-ttu-id="608bb-346">Bu metin, Echo hizmet işlemi aracılığıyla hizmete gönderilir ve aşağıdaki örnek çıktıda görüldüğü şekilde hizmet konsol penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="608bb-346">This text is sent to the service through the Echo service operation and appears in the service console window as in the following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="608bb-347">İstemci uygulaması, `Echo` işleminin dönüş değerini, diğer bir deyişle orijinal metni alır ve konsol penceresine yazdırır.</span><span class="sxs-lookup"><span data-stu-id="608bb-347">The client application receives the return value of the `Echo` operation, which is the original text, and prints it to its console window.</span></span> <span data-ttu-id="608bb-348">Aşağıda, istemci konsol penceresinden örnek çıktı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="608bb-348">The following is example output from the client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="608bb-349">Bu şekilde istemciden hizmete metin iletileri göndermeye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="608bb-349">You can continue sending text messages from the client to the service in this manner.</span></span> <span data-ttu-id="608bb-350">İşiniz bittiğinde her iki uygulamayı da sonlandırmak için istemci ve hizmet konsolu pencerelerinde Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="608bb-350">When you are finished, press Enter in the client and service console windows to end both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="608bb-351">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="608bb-351">Next steps</span></span>

<span data-ttu-id="608bb-352">Bu öğretici bir Azure geçiş istemci uygulaması ve hizmet veri yolu WCF aktarma özelliklerini kullanarak hizmeti oluşturmak nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="608bb-352">This tutorial showed how to build an Azure Relay client application and service using the WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="608bb-353">Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="608bb-353">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="608bb-354">Azure geçişi hakkında daha fazla bilgi edinmek için aşağıdaki konulara bakın.</span><span class="sxs-lookup"><span data-stu-id="608bb-354">To learn more about Azure Relay, see the following topics.</span></span>

* [<span data-ttu-id="608bb-355">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="608bb-355">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="608bb-356">Azure Geçiş’e genel bakış</span><span class="sxs-lookup"><span data-stu-id="608bb-356">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="608bb-357">.NET ile WCF geçişi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="608bb-357">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
