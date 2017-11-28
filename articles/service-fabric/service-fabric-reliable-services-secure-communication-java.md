---
title: "Azure Service Fabric hizmetler için güvenli iletişim aaaHelp | Microsoft Docs"
description: "Toohelp güvenliğini nasıl iletişim güvenilir hizmetler için genel bakış çalıştıran bir Azure Service Fabric kümesi."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="e3bc8-103">Güvenli iletişim Azure Service Fabric hizmetler için Yardım</span><span class="sxs-lookup"><span data-stu-id="e3bc8-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e3bc8-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="e3bc8-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="e3bc8-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="e3bc8-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="e3bc8-106">Hizmet remoting kullanırken hizmet korunmasına yardımcı olma</span><span class="sxs-lookup"><span data-stu-id="e3bc8-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="e3bc8-107">Biz varolan kullanmaya başlayacağınız [örnek](service-fabric-reliable-services-communication-remoting-java.md) , açıklar nasıl tooset uzaktan iletişim güvenilir hizmetler için ayarlama.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="e3bc8-108">toohelp hizmet remoting kullanırken bir hizmeti güvenli hale getirme, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e3bc8-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="e3bc8-109">Bir arabirim oluşturmak `HelloWorldStateless`, hizmetiniz üzerinde uzaktan yordam çağrısı için kullanılabilecek hello yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="e3bc8-110">Hizmetinizi kullanacak `FabricTransportServiceRemotingListener`, hello bildirilen `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` paket.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="e3bc8-111">Bu bir `CommunicationListener` remoting özellikleri sağlayan uygulama.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="e3bc8-112">Dinleyici ayarları ve güvenlik kimlik bilgileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="e3bc8-113">Güvenli, hizmet iletişimi hello kümedeki tüm hello düğümlerde yüklü toouse toohelp istediğiniz hello sertifikanın emin olun.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="e3bc8-114">Dinleyici ayarları ve güvenlik kimlik bilgileri sağlayabilir iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="e3bc8-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="e3bc8-115">Kullanarak sağlama bir [yapılandırma paketi](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="e3bc8-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="e3bc8-116">Ekleme bir `TransportSettings` hello settings.xml dosyasındaki bölümü.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="e3bc8-117">Bu durumda, hello `createServiceInstanceListeners` yöntemi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e3bc8-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="e3bc8-118">Eklerseniz bir `TransportSettings` hello settings.xml dosyasındaki tüm öneki olmadan bölümünde `FabricTransportListenerSettings` tüm hello Ayarları sayfasından Bu bölüm varsayılan olarak yüklenecektir.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="e3bc8-119">Bu durumda, hello `CreateServiceInstanceListeners` yöntemi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e3bc8-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="e3bc8-120">Çağırdığınızda yöntemler güvenli bir hizmette hello kullanmak yerine hello remoting yığını kullanarak `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` sınıfı toocreate kullanımı bir hizmeti proxy'si `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="e3bc8-121">Merhaba istemci kodu bir hizmetin bir parçası çalışıyorsa, yükleyebilir `FabricTransportSettings` hello settings.xml dosyasından.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="e3bc8-122">Benzer toohello hizmeti kodu TransportSettings bölümünde daha önce gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e3bc8-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="e3bc8-123">Değişiklikleri toohello istemci kodu aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="e3bc8-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
