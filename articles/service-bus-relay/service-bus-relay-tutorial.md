---
title: "aaaAzure Service Bus WCF geçişi Öğreticisi | Microsoft Docs"
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
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="acbb3-103">Azure WCF geçiş Öğreticisi</span><span class="sxs-lookup"><span data-stu-id="acbb3-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="acbb3-104">Bu öğretici nasıl basit bir WCF toobuild geçiş açıklar istemci uygulaması ve Azure geçişi kullanarak hizmet.</span><span class="sxs-lookup"><span data-stu-id="acbb3-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="acbb3-105">Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="acbb3-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="acbb3-106">Bu öğreticide, bir anlayış gerekli toocreate WCF geçiş istemcisi ve hizmet uygulaması hello adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="acbb3-107">Özgün WCF hizmetindeki benzerlerinde gibi bir hizmet her biri bir veya daha fazla hizmet işlemini kullanıma sunar, bir veya daha fazla uç noktaları, kullanıma sunan bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="acbb3-108">bir hizmetin Hello uç noktası hello hizmet bulunabileceği, bir adresi bir istemci hello hizmeti ve hello hizmet tooits istemciler tarafından sağlanan hello işlevselliği tanımlayan bir sözleşme ile iletişim kurması gereken hello bilgilerini içeren bir bağlama belirtir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="acbb3-109">WCF ve WCF geçiş arasındaki temel fark Hello bu hello uç bulutta hello yerine yerel olarak bilgisayarınızda kullanıma sunulan ' dir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="acbb3-110">Bu öğreticideki konu başlıklarını hello sırasıyla çalıştıktan sonra çalışan bir hizmetiniz ve hello hizmet hello işlemlerini çağırabilen bir istemci sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="acbb3-111">Merhaba ilk konu açıklar nasıl tooset bir hesap.</span><span class="sxs-lookup"><span data-stu-id="acbb3-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="acbb3-112">Merhaba sonraki adımlar açıklanmaktadır nasıl toodefine bir hizmeti kullanan bir sözleşme, nasıl tooimplement hello hizmet ve nasıl tooconfigure hello kod hizmetinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="acbb3-113">Ayrıca tanımladıkları nasıl toohost ve Çalıştır hello hizmeti.</span><span class="sxs-lookup"><span data-stu-id="acbb3-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="acbb3-114">Merhaba oluşturan hizmet kendiliğinden barındırılır ve hello istemci ve hizmet çalışması üzerinde hello aynı bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="acbb3-115">Merhaba hizmetini kodu veya bir yapılandırma dosyası kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="acbb3-116">Hello son üç adımda toocreate bir istemci uygulaması hello istemci uygulamasını yapılandırma ve oluşturma ve hello işlevselliği hello konağının erişebileceği bir istemci kullanın açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acbb3-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="acbb3-117">Prerequisites</span></span>

<span data-ttu-id="acbb3-118">toocomplete Bu öğreticiyi izleyerek hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="acbb3-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="acbb3-119">[Microsoft Visual Studio 2015 veya üzeri](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="acbb3-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="acbb3-120">Bu öğreticide Visual Studio 2017 kullanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="acbb3-121">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-121">An active Azure account.</span></span> <span data-ttu-id="acbb3-122">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir hesap oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="acbb3-123">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="acbb3-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="acbb3-124">Hizmet ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="acbb3-124">Create a service namespace</span></span>

<span data-ttu-id="acbb3-125">Merhaba ilk adımdır toocreate bir ad alanı ve tooobtain bir [paylaşılan erişim imzası (SAS)](../service-bus-messaging/service-bus-sas.md) anahtarı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="acbb3-126">Bir ad alanı aracılığıyla geçiş hizmetine hello kullanıma sunulan her uygulama için bir uygulama sınırı sağlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="acbb3-127">Hizmet ad alanı oluşturulduğunda bir SAS anahtarı hello sistem tarafından otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="acbb3-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="acbb3-128">Hizmet ad alanı ve SAS anahtarı birleşimi Hello Azure tooauthenticate erişim tooan uygulamanız için hello kimlik bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="acbb3-129">Merhaba izleyin [yönergeleri burada](relay-create-namespace-portal.md) toocreate geçiş ad alanı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="acbb3-130">WCF hizmet sözleşmesini tanımlama</span><span class="sxs-lookup"><span data-stu-id="acbb3-130">Define a WCF service contract</span></span>

<span data-ttu-id="acbb3-131">Merhaba hizmet sözleşmesini hangi işlemleri (web hizmeti terminolojisi yöntemler ve işlevlere hello) hello hizmet destekler belirtir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="acbb3-132">Sözleşmeler; C++, C# veya Visual Basic arabirimi tanımlamasıyla oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="acbb3-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="acbb3-133">Merhaba arabirimdeki her yöntem tooa belirli hizmet işlemi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="acbb3-134">Her bir arabirime hello olmalıdır [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliği uygulanan tooit ve her işlem hello olmalıdır [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) uygulanan öznitelik tooit.</span><span class="sxs-lookup"><span data-stu-id="acbb3-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="acbb3-135">Bir yöntemi varsa hello içeren bir arabirimdeki [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) özniteliğinde hello yok [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) özniteliği, yöntem kullanıma sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="acbb3-136">Bu görevler için Hello kodu aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="acbb3-137">Sözleşmeler ve hizmetlere daha büyük bir tartışma için bkz: [Hizmetleri Tasarlama ve uygulama](https://msdn.microsoft.com/library/ms729746.aspx) hello WCF belgelerinde içinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="acbb3-138">Geçiş sözleşme sahip bir arabirim oluşturma</span><span class="sxs-lookup"><span data-stu-id="acbb3-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="acbb3-139">Visual Studio Yönetici olarak açın hello hello programa sağ tıklayarak **Başlat** menü ve seçerek **yönetici olarak çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="acbb3-140">Yeni bir konsol uygulama projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-140">Create a new console application project.</span></span> <span data-ttu-id="acbb3-141">Merhaba tıklatın **dosya** menü ve seçin **yeni**, ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="acbb3-142">Merhaba, **yeni proje** iletişim kutusunda, tıklatın **Visual C#** (varsa **Visual C#** görüntülenmiyorsa, kısmına bakın **diğer diller**).</span><span class="sxs-lookup"><span data-stu-id="acbb3-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="acbb3-143">Merhaba tıklatın **konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="acbb3-144">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="acbb3-145">Merhaba Service Bus NuGet paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="acbb3-146">Bu paket otomatik olarak başvuruları toohello Service Bus kitaplıklarının yanı sıra hello WCF ekler **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="acbb3-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) tooprogrammatically erişim hello WCF'nin temel özelliklerine etkinleştirir hello ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="acbb3-148">Hizmet veri yolu hello nesnelerin çoğunu ve WCF toodefine Hizmet sözleşmeleri özniteliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="acbb3-149">Çözüm Gezgini'nde, hello projesine sağ tıklayın ve ardından **NuGet paketlerini Yönet...** . Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="acbb3-150">Bu hello proje adı hello seçili olun **sürümler** kutusu.</span><span class="sxs-lookup"><span data-stu-id="acbb3-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="acbb3-151">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="acbb3-152">Çözüm Gezgini'nde çift tıklayarak hello Program.cs dosyasının tooopen zaten değilse hello düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="acbb3-153">Merhaba aşağıdakileri ekleyin hello hello dosya üstündeki deyimleri kullanarak:</span><span class="sxs-lookup"><span data-stu-id="acbb3-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="acbb3-154">Değişiklik hello ad alanı adı varsayılan **EchoService** çok**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="acbb3-155">Bu öğretici hello C# ad alanı kullanır **Microsoft.ServiceBus.Samples**, yönetilen hello hello yapılandırma dosyasında kullanılan türü hello sözleşme tabanlı hello ad olduğu [hello WCF istemciyapılandırma](#configure-the-wcf-client) adım.</span><span class="sxs-lookup"><span data-stu-id="acbb3-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="acbb3-156">Bu örneği derlemek istediğinizde herhangi bir ad alanı belirtebilirsiniz; Ancak, ardından hello sözleşme ve hizmet hello ad alanlarını uygun şekilde, hello uygulama yapılandırma dosyasında değiştirmediğiniz sürece hello öğretici çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="acbb3-157">Merhaba App.config dosyası olmalıdır belirtilen hello ad hello aynı C# dosyalarınızda belirtilen hello ad alanı olarak.</span><span class="sxs-lookup"><span data-stu-id="acbb3-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="acbb3-158">Merhaba hemen sonra `Microsoft.ServiceBus.Samples` ad alanı bildirimi, ancak hello ad alanı içinde adlı yeni arabirimi tanımlayın `IEchoContract` ve hello geçerli `ServiceContractAttribute` ad alanı değerine sahip öznitelik toohello arabirimi `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="acbb3-159">Hello ad alanı değeri kodunuzu hello kapsam boyunca kullandığınız hello ad alanından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="acbb3-160">Bunun yerine, başlangıç ad alanı değeri bu sözleşme için benzersiz bir tanımlayıcı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="acbb3-161">Hello ad alanını açıkça belirlemek hello varsayılan ad alanı değeri toohello sözleşme adına eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="acbb3-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="acbb3-162">Koddan sonra hello ad alanı bildirimi hello yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="acbb3-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="acbb3-163">Genellikle, hello hizmet sözleşmesi ad alanı sürüm bilgilerini içeren bir adlandırma şeması içerir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="acbb3-164">Hello hizmet sözleşmesi ad içinde sürüm bilgileri de dahil olmak üzere yeni bir ad alanı ile yeni bir hizmet sözleşmesi tanımlayarak ve yeni bir uç noktada kullanıma Hizmetleri tooisolate önemli değişiklikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="acbb3-165">Bu şekilde, istemciler güncelleştirilmiş toobe gerek kalmadan toouse hello eski hizmet sözleşmelerini devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="acbb3-166">Sürüm bilgileri, bir tarihten veya bir derleme numarasından oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="acbb3-167">Daha fazla bilgi için bkz. [Hizmet Sürümü Oluşturma](http://go.microsoft.com/fwlink/?LinkID=180498).</span><span class="sxs-lookup"><span data-stu-id="acbb3-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="acbb3-168">Bu öğreticinin Hello amaçları doğrultusunda, düzeni hello hizmet sözleşmesi ad alanının adlandırma hello sürüm bilgilerini içermiyor.</span><span class="sxs-lookup"><span data-stu-id="acbb3-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="acbb3-169">Merhaba içinde `IEchoContract` arabirim, hello tek bir işlem hello için bir yöntem bildirin `IEchoContract` sözleşme çıkarır hello içinde arabirim ve hello geçerli `OperationContractAttribute` parçası olarak tooexpose istediğiniz özniteliği toohello yöntemi hello ortak WCF geçiş , aşağıdaki gibi Sözleşme:</span><span class="sxs-lookup"><span data-stu-id="acbb3-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="acbb3-170">Merhaba hemen sonra `IEchoContract` arabirim tanımı, hem de devralan bir kanal bildirin `IEchoContract` ve ayrıca toohello `IClientChannel` arabirimi, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="acbb3-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="acbb3-171">Bir kanal üzerinden hello ana bilgisayar ve istemci bilgileri tooeach diğer kullandıkları hello WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="acbb3-172">Daha sonra hello kanal tooecho bilgileri hello iki uygulama arasındaki karşı kod yazacaksınız.</span><span class="sxs-lookup"><span data-stu-id="acbb3-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="acbb3-173">Hello gelen **yapı** menüsünde tıklatın **Çözümü Derle** veya basın **Ctrl + Shift + B** tooconfirm hello çalışmanızın o ana kadarki doğruluğunu.</span><span class="sxs-lookup"><span data-stu-id="acbb3-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="acbb3-174">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-174">Example</span></span>

<span data-ttu-id="acbb3-175">koddan hello WCF geçiş sözleşmesini tanımlayan temel bir arabirimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

<span data-ttu-id="acbb3-176">Merhaba arabirimi oluşturulur, hello arabirimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="acbb3-177">Uygulama hello WCF Sözleşmesi</span><span class="sxs-lookup"><span data-stu-id="acbb3-177">Implement hello WCF contract</span></span>

<span data-ttu-id="acbb3-178">Bir Azure geçişi oluşturmak için öncelikle bir arabirim kullanılarak tanımlanan hello sözleşmeyi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="acbb3-179">Merhaba arabirimi oluşturma hakkında daha fazla bilgi için hello önceki adıma bakın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="acbb3-180">Merhaba sonraki adıma tooimplement hello arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="acbb3-181">Bu adlı bir sınıf oluşturursunuz `EchoService` hello kullanıcı tanımlı uygulayan `IEchoContract` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="acbb3-182">Merhaba arabirimi uyguladıktan sonra bir App.config yapılandırma dosyası kullanarak hello arabirimi ardından yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="acbb3-183">Merhaba yapılandırma dosyası hello hello hizmetin adını, hello adını hello sözleşme ve hello geçiş hizmeti ile kullanılan toocommunicate Protokolü hello türü gibi hello uygulama için gerekli bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="acbb3-184">Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="acbb3-185">Nasıl tooimplement hizmet sözleşme hakkında daha fazla genel bilgi için bkz: [hizmet sözleşmelerini uygulama](https://msdn.microsoft.com/library/ms733764.aspx) hello WCF belgelerinde içinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="acbb3-186">Adlı yeni bir sınıf oluşturun `EchoService` hello hello tanımını hemen sonra `IEchoContract` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="acbb3-187">Merhaba `EchoService` sınıfı uygulayan hello `IEchoContract` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="acbb3-188">Benzer tooother arabirim uygulamaları, farklı bir dosyada hello tanımı uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="acbb3-189">Ancak, Bu öğretici için hello uygulama aynı dosya hello arabirim tanımı ve hello hello bulunan `Main` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="acbb3-190">Merhaba uygulamak [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello özniteliği `IEchoContract` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="acbb3-191">Merhaba özniteliği hello hizmet adı ve ad alanını belirtir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="acbb3-192">Bunu yaptıktan sonra hello `EchoService` sınıfı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="acbb3-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="acbb3-193">Uygulama hello `Echo` hello tanımlanmış yöntemi `IEchoContract` hello arabiriminde `EchoService` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="acbb3-194">Tıklatın **yapı**, ardından **yapı çözümü** tooconfirm hello çalışmanızın doğruluğunu.</span><span class="sxs-lookup"><span data-stu-id="acbb3-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="acbb3-195">Hello hizmet ana bilgisayarı için başlangıç yapılandırmasını tanımlama</span><span class="sxs-lookup"><span data-stu-id="acbb3-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="acbb3-196">Merhaba yapılandırma dosyası çok benzer tooa WCF yapılandırma dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="acbb3-197">Merhaba hizmet adı, uç noktayı (istemcilerin ve ana bilgisayarların birbirleriyle toocommunicate için Azure geçiş gösteren başka bir deyişle, hello konum) içerir ve hello bağlama (kullanılan toocommunicate Protokolü hello türü).</span><span class="sxs-lookup"><span data-stu-id="acbb3-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="acbb3-198">Merhaba ana bu yapılandırılan hizmet uç noktasının tooa başvuruyor farktır [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello .NET Framework parçası olmayan bağlama.</span><span class="sxs-lookup"><span data-stu-id="acbb3-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="acbb3-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) hello hizmeti tarafından tanımlanan hello bağlamaları biridir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="acbb3-200">İçinde **Çözüm Gezgini**, hello App.config dosyası tooopen çift tıklayın, hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="acbb3-201">Merhaba, `<appSettings>` öğesi hello yer tutucuları hizmet ad alanınızın hello adıyla değiştirin ve hello bir önceki adımda kopyaladığınız SAS anahtarı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="acbb3-202">Merhaba içinde `<system.serviceModel>` etiketler eklemek bir `<services>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="acbb3-203">Bir tek yapılandırma dosyasında birden çok geçiş uygulamaları tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="acbb3-204">Ancak bu öğreticide yalnızca bir adet tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="acbb3-205">Merhaba içinde `<services>` öğesi ekleme bir `<service>` öğesi toodefine hello hello hizmetin adını.</span><span class="sxs-lookup"><span data-stu-id="acbb3-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="acbb3-206">Merhaba içinde `<service>` öğesi hello uç nokta sözleşmesinin hello konumunu tanımlayın ve ayrıca hello endpoint yönelik bağlama türünü hello.</span><span class="sxs-lookup"><span data-stu-id="acbb3-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="acbb3-207">Hello endpoint hello istemci hello ana bilgisayar uygulamasını nerede arayacağını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="acbb3-208">Daha sonra bu adım toocreate tam olarak hello konak Azure geçiş aracılığıyla kullanıma sunan bir URI hello öğretici kullanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="acbb3-209">Merhaba bağlama TCP protokolü toocommunicate hello geçiş hizmeti ile Merhaba gibi kullanıyoruz olduğunu bildirir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="acbb3-210">Merhaba gelen **yapı** menüsünde tıklatın **yapı çözümü** tooconfirm hello çalışmanızın doğruluğunu.</span><span class="sxs-lookup"><span data-stu-id="acbb3-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="acbb3-211">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-211">Example</span></span>

<span data-ttu-id="acbb3-212">Merhaba aşağıdaki kod hello hizmet sözleşmesini hello uyarlamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-212">hello following code shows hello implementation of hello service contract.</span></span>

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

<span data-ttu-id="acbb3-213">Merhaba aşağıdaki kod hello hello hizmet ana bilgisayarı ile ilişkilendirilen hello App.config dosyasının temel biçimini gösterir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

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

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="acbb3-214">Hizmet barındırma ve temel bir web hizmeti tooregister hello geçiş ile çalıştırma</span><span class="sxs-lookup"><span data-stu-id="acbb3-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="acbb3-215">Bu adım nasıl toorun Azure geçiş açıklar hizmet.</span><span class="sxs-lookup"><span data-stu-id="acbb3-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="acbb3-216">Merhaba geçiş kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="acbb3-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="acbb3-217">İçinde `Main()`, hangi toostore hello ad alanında iki değişkeni oluşturun ve hello hello konsol penceresinden okunan SAS anahtarı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="acbb3-218">Merhaba SAS anahtar projeniz kullanılan sonraki tooaccess olacaktır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="acbb3-219">Merhaba ad alanı bir parametre olarak geçirilen çok`CreateServiceUri` toocreate hizmet URI'si.</span><span class="sxs-lookup"><span data-stu-id="acbb3-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="acbb3-220">Kullanarak bir [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) nesne, hello kimlik bilgisi türü olarak bir SAS anahtarı kullanarak bildirin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="acbb3-221">Merhaba doğrudan hello son adımda eklediğiniz hello koddan sonra aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="acbb3-222">Merhaba hizmeti için bir taban adresi oluşturma</span><span class="sxs-lookup"><span data-stu-id="acbb3-222">Create a base address for hello service</span></span>

<span data-ttu-id="acbb3-223">Merhaba son adımda eklediğiniz hello koddan sonra oluşturma bir `Uri` hello hizmeti hello temel adres için örneği.</span><span class="sxs-lookup"><span data-stu-id="acbb3-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="acbb3-224">Bu URI hello Service Bus şemasını, başlangıç ad alanı ve hello hizmet arabirimi hello yolunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="acbb3-225">"sb" ifadesinin kısaltmasıdır hello Service Bus şeması için ve biz hello protokol olarak TCP kullanıyoruz gösterir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="acbb3-226">Bu aynı zamanda daha önce hello yapılandırma dosyasında belirtilir zaman [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) olarak hello bağlama belirtildi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="acbb3-227">Bu öğretici için hello URI'dir `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="acbb3-228">Oluşturma ve hello hizmet ana bilgisayarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="acbb3-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="acbb3-229">Merhaba bağlantı modunu çok ayarlamak`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="acbb3-230">Merhaba Protokolü hello hizmeti kullanan toocommunicate hello geçiş hizmeti ile Merhaba bağlantı modunu açıklar; HTTP veya TCP.</span><span class="sxs-lookup"><span data-stu-id="acbb3-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="acbb3-231">Merhaba varsayılan ayarı kullanarak `AutoDetect`, hello hizmeti çalışır tooconnect tooAzure geçiş kullanılabilir durumdaysa TCP ve HTTP üzerinden TCP kullanılabilir değilse.</span><span class="sxs-lookup"><span data-stu-id="acbb3-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="acbb3-232">Bu hello Protokolü hello hizmetinden farklıdır Not istemci iletişimi için belirtir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="acbb3-233">Bu protokol, kullanılan hello bağlama tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="acbb3-234">Örneğin, bir hizmet hello kullanabilirsiniz [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) , uç noktasında istemcileriyle HTTP üzerinden iletişim kurduğu bağlama.</span><span class="sxs-lookup"><span data-stu-id="acbb3-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="acbb3-235">Aynı hizmeti belirtebilirsiniz **ConnectivityMode.AutoDetect** hello hizmeti ile Azure geçişi TCP üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="acbb3-236">Bu bölümde daha önce oluşturulan URI hello kullanarak hello hizmet ana bilgisayarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="acbb3-237">Merhaba hizmet konağı hello hizmeti başlatır hello WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="acbb3-238">Merhaba türü geçirdiğiniz burada toocreate istediğiniz hizmet (bir `EchoService` türü) ve ayrıca istediğiniz tooexpose hello hizmet toohello adresi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="acbb3-239">Merhaba Program.cs dosyasının Hello üstünde çok başvurular ekleyin[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) ve [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="acbb3-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="acbb3-240">Geri `Main()`, hello uç nokta tooenable genel erişim yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="acbb3-241">Bu adımı uygulamanız genel olarak hello ATOM akışı projeniz için inceleyerek bulunabileceğini hello geçiş hizmeti bildirir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="acbb3-242">Ayarlarsanız **DiscoveryType** çok**özel**, bir istemci mümkün tooaccess hello hizmeti olması.</span><span class="sxs-lookup"><span data-stu-id="acbb3-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="acbb3-243">Ancak, hello geçiş ad alanı aradığında hello hizmet görünmez.</span><span class="sxs-lookup"><span data-stu-id="acbb3-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="acbb3-244">Bunun yerine, hello istemci tooknow hello bitiş noktası yolu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="acbb3-245">Uygulama hello hizmeti kimlik bilgileri hello App.config dosyasında tanımlanan toohello hizmet uç noktaları:</span><span class="sxs-lookup"><span data-stu-id="acbb3-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="acbb3-246">Merhaba önceki adımda belirtildiği gibi birden çok hizmet ve uç noktaları hello yapılandırma dosyasında bildirilen.</span><span class="sxs-lookup"><span data-stu-id="acbb3-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="acbb3-247">Bildirirseniz Bu kod hello yapılandırma dosyasını ve arama çapraz her uç nokta toowhich için kimlik bilgilerinizi uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="acbb3-248">Ancak, bu öğreticide, tek bir uç nokta hello yapılandırma dosyası vardır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="acbb3-249">Açık hello hizmet konağı</span><span class="sxs-lookup"><span data-stu-id="acbb3-249">Open hello service host</span></span>

1. <span data-ttu-id="acbb3-250">Merhaba hizmeti açın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="acbb3-251">Hizmet hello hello kullanıcı çalıştıran ve açıklayan bilgilendirmek nasıl tooshut hello hizmeti kapalı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="acbb3-252">Tamamlandığında, hello hizmet ana bilgisayarını kapatın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="acbb3-253">Tuşuna **Ctrl + Shift + B** toobuild hello projesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="acbb3-254">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-254">Example</span></span>

<span data-ttu-id="acbb3-255">Tamamlanmış hizmet kodunuzun şu şekilde görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="acbb3-256">ana bilgisayar hizmeti bir konsol uygulamasında hello ve Hello kod hello öğreticide hello hizmet sözleşmesini ve önceki adımları içerir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

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

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="acbb3-257">Merhaba hizmet sözleşmesi için bir WCF istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="acbb3-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="acbb3-258">Merhaba sonraki adımı toocreate bir istemci uygulaması ve daha sonraki adımlarda gerçekleştireceksiniz hello hizmet sözleşmesini tanımlama.</span><span class="sxs-lookup"><span data-stu-id="acbb3-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="acbb3-259">Bu adımların hello adımlara benzer olduğunu unutmayın kullanılan toocreate hizmet: bir App.config düzenleme sözleşme tanımlama, kimlik bilgileri tooconnect toohello geçişi hizmetini kullanma vb..</span><span class="sxs-lookup"><span data-stu-id="acbb3-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="acbb3-260">Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="acbb3-261">Merhaba aşağıdakileri yaparak hello geçerli Visual Studio çözümüne hello istemci için yeni bir proje oluşturun:</span><span class="sxs-lookup"><span data-stu-id="acbb3-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="acbb3-262">Çözüm Gezgini'nde, buna hello hello hizmeti içeren aynı çözüm, hello geçerli çözüme (Merhaba proje değil) sağ tıklayın ve **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="acbb3-263">Ardından **Yeni Proje**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="acbb3-264">Merhaba, **Yeni Proje Ekle** iletişim kutusu, tıklatın **Visual C#** (varsa **Visual C#** görüntülenmiyorsa, kısmına bakın **diğer diller**) seçin hello **Konsol uygulaması (.NET Framework)** şablonu ve adlandırın **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="acbb3-265">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="acbb3-266">Çözüm Gezgini'nde hello hello Program.cs dosyasına çift tıklayarak **EchoClient** proje tooopen zaten değilse hello düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="acbb3-267">Değişiklik hello ad alanı adı varsayılan `EchoClient` çok`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="acbb3-268">Merhaba yüklemek [Service Bus NuGet paketi](https://www.nuget.org/packages/WindowsAzure.ServiceBus): hello Çözüm Gezgini'nde sağ **EchoClient** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="acbb3-269">Merhaba tıklatın **Gözat** sekmesini ve ardından arama `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="acbb3-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="acbb3-270">Tıklatın **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="acbb3-271">Ekleme bir `using` hello bildirimi [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) hello Program.cs dosyasındaki ad alanı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="acbb3-272">Hello hizmet sözleşmesi tanımını toohello ad hello aşağıdaki örnekte gösterildiği gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="acbb3-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="acbb3-273">Bu tanım hello kullanılan aynı toohello tanımını olduğuna dikkat edin **hizmet** projesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="acbb3-274">Bu kod hello hello üstünde eklemelisiniz `Microsoft.ServiceBus.Samples` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="acbb3-275">Tuşuna **Ctrl + Shift + B** toobuild hello istemci.</span><span class="sxs-lookup"><span data-stu-id="acbb3-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="acbb3-276">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-276">Example</span></span>

<span data-ttu-id="acbb3-277">Merhaba aşağıdaki kod hello Program.cs dosyasının geçerli durumunu hello hello gösterir **EchoClient** projesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

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

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="acbb3-278">Merhaba WCF istemcisini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="acbb3-278">Configure hello WCF client</span></span>

<span data-ttu-id="acbb3-279">Bu adımda, daha önce bu öğreticide oluşturduğunuz hello hizmete erişen temel istemci uygulamasına yönelik bir App.config dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="acbb3-280">Bu App.config dosyası hello sözleşme, bağlama ve hello uç noktanın adı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="acbb3-281">Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="acbb3-282">Çözüm Gezgini'nde, hello **EchoClient** projesi, çift **App.config** tooopen hello dosyasını hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="acbb3-283">Merhaba, `<appSettings>` öğesi hello yer tutucuları hizmet ad alanınızın hello adıyla değiştirin ve hello bir önceki adımda kopyaladığınız SAS anahtarı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="acbb3-284">Add Hello system.serviceModel öğesi içinde bir `<client>` öğesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="acbb3-285">Bu adım ile WCF stilinde istemci uygulaması tanımladığınızı bildirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="acbb3-286">Merhaba içinde `client` öğesi hello adı, sözleşmeyi ve hello uç noktası için bağlama türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="acbb3-287">Bu adım hello uç noktası, hello hizmeti ve Merhaba istemci uygulaması ile Azure geçişi TCP toocommunicate kullandığını hello olgu tanımlanan hello sözleşme hello adını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="acbb3-288">Merhaba uç nokta adı kullanılan hello toolink Bu uç nokta yapılandırması hello hizmet URI'si ile sonraki adım.</span><span class="sxs-lookup"><span data-stu-id="acbb3-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="acbb3-289">Tıklatın **dosya**, ardından **Tümünü Kaydet**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="acbb3-290">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-290">Example</span></span>

<span data-ttu-id="acbb3-291">Merhaba aşağıdaki kodu hello Echo istemciye için hello App.config dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-291">hello following code shows hello App.config file for hello Echo client.</span></span>

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

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="acbb3-292">Uygulama hello WCF istemcisi</span><span class="sxs-lookup"><span data-stu-id="acbb3-292">Implement hello WCF client</span></span>
<span data-ttu-id="acbb3-293">Bu adımda, bu öğreticide daha önce oluşturduğunuz hello hizmete erişen bir temel istemci uygulaması uygulayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="acbb3-294">Benzer toohello hizmeti hello istemci hello çoğunu gerçekleştirir aynı işlemleri tooaccess Azure geçişi:</span><span class="sxs-lookup"><span data-stu-id="acbb3-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="acbb3-295">Merhaba bağlantı modunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="acbb3-296">Merhaba hello ana bilgisayar hizmetinin yer URI oluşturur.</span><span class="sxs-lookup"><span data-stu-id="acbb3-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="acbb3-297">Merhaba güvenlik kimlik bilgilerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="acbb3-298">Merhaba kimlik bilgilerini toohello bağlantı geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="acbb3-299">Merhaba bağlantı açar.</span><span class="sxs-lookup"><span data-stu-id="acbb3-299">Opens hello connection.</span></span>
6. <span data-ttu-id="acbb3-300">Merhaba uygulamaya özgü görevleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="acbb3-301">Merhaba bağlantıyı kapatır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-301">Closes hello connection.</span></span>

<span data-ttu-id="acbb3-302">Merhaba hizmeti bir çağrı çok kullanır ancak bununla birlikte, hello temel farklar Merhaba istemci uygulaması bir kanal tooconnect toohello geçiş hizmetini kullanan biri**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="acbb3-303">Bu görevler için kullanılan hello kod aşağıdaki hello yordamın hello örnekte sağlanır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="acbb3-304">Bir istemci uygulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="acbb3-304">Implement a client application</span></span>
1. <span data-ttu-id="acbb3-305">Merhaba bağlantı modunu çok ayarlamak**otomatik algıla**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="acbb3-306">Merhaba içindeki kodu aşağıdaki hello eklemek `Main()` hello yöntemi **EchoClient** uygulama.</span><span class="sxs-lookup"><span data-stu-id="acbb3-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="acbb3-307">Merhaba konsoldan okunan değişkenleri toohold hello değerleri hello hizmet ad alanı ve SAS anahtarı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="acbb3-308">Merhaba geçiş projenizde hello konak hello konumunu tanımlayan URI oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="acbb3-309">Hizmet ad alanı uç noktanız için Hello kimlik bilgisi nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="acbb3-310">Merhaba App.config dosyasında açıklanan hello yapılandırmayı yükleyen hello kanal fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acbb3-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="acbb3-311">Kanal fabrikası üzerinden hello hizmet ve istemci uygulamaları iletişim kanalı oluşturan WCF nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="acbb3-312">Merhaba kimlik bilgileri geçerli.</span><span class="sxs-lookup"><span data-stu-id="acbb3-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="acbb3-313">Oluşturun ve hello kanal toohello hizmeti açın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="acbb3-314">Merhaba temel kullanıcı arabirimini ve hello Yankı için işlevselliği yazma.</span><span class="sxs-lookup"><span data-stu-id="acbb3-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

    <span data-ttu-id="acbb3-315">Merhaba kod bir proxy olarak hello hello kanal nesnesinin örneğini hello hizmeti için kullandığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="acbb3-316">Merhaba kanal ve Kapat hello Fabrika kapatın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="acbb3-317">Örnek</span><span class="sxs-lookup"><span data-stu-id="acbb3-317">Example</span></span>

<span data-ttu-id="acbb3-318">Tamamlanan kodu aşağıdaki gibi görünmelidir nasıl toocreate bir istemci uygulaması, nasıl toocall hello hello hizmet işlemlerini ve nasıl tooclose hello istemci hello işleminden sonra çağrı gösteren tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="acbb3-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

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

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
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

## <a name="run-hello-applications"></a><span data-ttu-id="acbb3-319">Merhaba uygulamaları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="acbb3-319">Run hello applications</span></span>

1. <span data-ttu-id="acbb3-320">Tuşuna **Ctrl + Shift + B** toobuild hello çözümü.</span><span class="sxs-lookup"><span data-stu-id="acbb3-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="acbb3-321">Bu, hello istemci projesi ve hello önceki adımlarda oluşturduğunuz hello hizmet projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="acbb3-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="acbb3-322">Önce çalışan hello istemci uygulama, hello hizmet uygulamasının çalıştığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="acbb3-323">Visual Studio'da Çözüm Gezgini'nde hello sağ **EchoService** çözüm, ardından **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="acbb3-324">Merhaba çözüm Özellikleri iletişim kutusunda, tıklatın **başlangıç projesi**, hello ardından **birden fazla başlangıç projesi** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="acbb3-325">Emin olun **EchoService** hello listede ilk olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="acbb3-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="acbb3-326">Set hello **eylem** hem hello kutusunu **EchoService** ve **EchoClient** çok projeleri**Başlat**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="acbb3-327">**Proje Bağımlılıkları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="acbb3-328">Merhaba, **projeleri** kutusunda **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="acbb3-329">Merhaba, **bağlıdır** kutusunda, emin olun **EchoService** denetlenir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="acbb3-330">Tıklatın **Tamam** toodismiss hello **özellikleri** iletişim.</span><span class="sxs-lookup"><span data-stu-id="acbb3-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="acbb3-331">Tuşuna **F5** toorun her iki proje.</span><span class="sxs-lookup"><span data-stu-id="acbb3-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="acbb3-332">Her iki konsol penceresi açın ve hello ad alanı adı ister.</span><span class="sxs-lookup"><span data-stu-id="acbb3-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="acbb3-333">Merhaba hizmeti ilk olarak, bunu hello içinde çalıştırılmalıdır **EchoService** konsol penceresinde, hello ad girin ve ardından basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="acbb3-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="acbb3-334">Ardından SAS anahtarınız istenir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="acbb3-335">Merhaba SAS anahtarını girin ve ENTER tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="acbb3-336">Burada, hello konsol penceresinden örnek çıktı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-336">Here is example output from hello console window.</span></span> <span data-ttu-id="acbb3-337">Örneğin yalnızca amaçları şunlardır Hello değerleri sağlanan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="acbb3-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="acbb3-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="acbb3-339">Merhaba hizmet uygulaması toohello konsol penceresinde hello adresi üzerinde dinleme yaptığı, aşağıdaki örneğine hello görülen yazdırır.</span><span class="sxs-lookup"><span data-stu-id="acbb3-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="acbb3-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="acbb3-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="acbb3-341">Merhaba, **EchoClient** konsol penceresinde, girin hello hello hizmet uygulaması için daha önce girdiğiniz aynı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="acbb3-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="acbb3-342">Merhaba önceki adımları tooenter hello izleyin aynı hizmet ad alanı ve SAS anahtarı Merhaba istemci uygulaması için değerler.</span><span class="sxs-lookup"><span data-stu-id="acbb3-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="acbb3-343">Bu değerleri girdikten sonra hello istemci kanal toohello hizmet açar ve hello aşağıdaki konsol çıktısı örneğinde görüldüğü şekilde bazı metinler, tooenter ister.</span><span class="sxs-lookup"><span data-stu-id="acbb3-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="acbb3-344">Bazı metin toosend toohello hizmet uygulaması girin ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="acbb3-345">Bu metin toohello hizmeti hello Echo hizmet işlemi aracılığıyla gönderilir ve hello hizmet konsol penceresinde hello örnek çıktı aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="acbb3-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="acbb3-346">Merhaba istemci uygulaması hello hello dönüş değerini alan `Echo` hello orijinal metni alır ve bunu yazdıran işlemi tooits konsol penceresinde.</span><span class="sxs-lookup"><span data-stu-id="acbb3-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="acbb3-347">Merhaba, hello istemci konsol penceresinden örnek çıktı verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="acbb3-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="acbb3-348">Bu şekilde hello istemci toohello hizmetinden metin iletileri göndermeye devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acbb3-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="acbb3-349">İşiniz bittiğinde, içinde hello istemci ve hizmet Konsolu windows tooend her iki uygulamayı basın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acbb3-350">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acbb3-350">Next steps</span></span>

<span data-ttu-id="acbb3-351">Bu öğretici, Service Bus WCF geçiş yeteneklerine toobuild Azure geçiş istemci uygulaması ve hizmeti kullanılarak nasıl hello gösterdi.</span><span class="sxs-lookup"><span data-stu-id="acbb3-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="acbb3-352">Kullanıldığı benzer bir öğretici [Service Bus Mesajlaşma hizmeti](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), bkz: [Service Bus kuyrukları ile çalışmaya başlama](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="acbb3-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="acbb3-353">toolearn Azure geçişi hakkında daha fazla bilgi aşağıdaki konularda hello bakın.</span><span class="sxs-lookup"><span data-stu-id="acbb3-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="acbb3-354">Azure Service Bus mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="acbb3-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="acbb3-355">Azure Geçiş’e genel bakış</span><span class="sxs-lookup"><span data-stu-id="acbb3-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="acbb3-356">Toouse hello WCF hizmeti .NET ile nasıl geçiş</span><span class="sxs-lookup"><span data-stu-id="acbb3-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png
