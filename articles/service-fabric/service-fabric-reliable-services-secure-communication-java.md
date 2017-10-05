---
title: "Güvenli iletişim için Azure Service Fabric Hizmetleri'nde Yardım | Microsoft Docs"
description: "Güvenilir hizmetler için iletişimi güvenli hale getirmek nasıl genel bakış çalıştıran bir Azure Service Fabric kümesi."
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
ms.openlocfilehash: c4634e3d8efb1745fffcfe3e647e43d867038716
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="fe970-103">Güvenli iletişim Azure Service Fabric hizmetler için Yardım</span><span class="sxs-lookup"><span data-stu-id="fe970-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe970-104">Windows üzerinde C#</span><span class="sxs-lookup"><span data-stu-id="fe970-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="fe970-105">Linux üzerinde Java</span><span class="sxs-lookup"><span data-stu-id="fe970-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="fe970-106">Hizmet remoting kullanırken hizmet korunmasına yardımcı olma</span><span class="sxs-lookup"><span data-stu-id="fe970-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="fe970-107">Biz varolan kullanmaya başlayacağınız [örnek](service-fabric-reliable-services-communication-remoting-java.md) nasıl uzaktan iletişim için güvenilir hizmetler ayarlanacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fe970-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how to set up remoting for reliable services.</span></span> <span data-ttu-id="fe970-108">Hizmet remoting kullanırken bir hizmeti güvenli hale getirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="fe970-108">To help secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="fe970-109">Bir arabirim oluşturmak `HelloWorldStateless`, hizmetiniz üzerinde uzaktan yordam çağrısı için kullanılabilecek yöntemleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="fe970-109">Create an interface, `HelloWorldStateless`, that defines the methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="fe970-110">Hizmetinizi kullanacak `FabricTransportServiceRemotingListener`, içinde bildirilen `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` paket.</span><span class="sxs-lookup"><span data-stu-id="fe970-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in the `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="fe970-111">Bu bir `CommunicationListener` remoting özellikleri sağlayan uygulama.</span><span class="sxs-lookup"><span data-stu-id="fe970-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

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
2. <span data-ttu-id="fe970-112">Dinleyici ayarları ve güvenlik kimlik bilgileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe970-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="fe970-113">Hizmet iletişimi güvenli hale getirmek için kullanmak istediğiniz sertifikayı kümedeki tüm düğümlerde yüklü olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fe970-113">Make sure that the certificate that you want to use to help secure your service communication is installed on all the nodes in the cluster.</span></span> <span data-ttu-id="fe970-114">Dinleyici ayarları ve güvenlik kimlik bilgileri sağlayabilir iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="fe970-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="fe970-115">Kullanarak sağlama bir [yapılandırma paketi](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="fe970-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="fe970-116">Ekleme bir `TransportSettings` settings.xml dosyasındaki bölümü.</span><span class="sxs-lookup"><span data-stu-id="fe970-116">Add a `TransportSettings` section in the settings.xml file.</span></span>

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

       <span data-ttu-id="fe970-117">Bu durumda, `createServiceInstanceListeners` yöntemi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="fe970-117">In this case, the `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="fe970-118">Eklerseniz bir `TransportSettings` herhangi öneki olmadan settings.xml dosyasındaki bölümünü `FabricTransportListenerSettings` tüm ayarları varsayılan olarak bu bölümünden yüklenir.</span><span class="sxs-lookup"><span data-stu-id="fe970-118">If you add a `TransportSettings` section in the settings.xml file without any prefix, `FabricTransportListenerSettings` will load all the settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="fe970-119">Bu durumda, `CreateServiceInstanceListeners` yöntemi şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="fe970-119">In this case, the `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="fe970-120">Çağırdığınızda yöntemler güvenli bir hizmette kullanmak yerine uzaktan iletişim yığını kullanarak `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` hizmeti proxy'si oluşturmak, kullanmak için sınıf `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="fe970-120">When you call methods on a secured service by using the remoting stack, instead of using the `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class to create a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="fe970-121">İstemci kodu bir hizmetin bir parçası çalışıyorsa, yükleyebilir `FabricTransportSettings` settings.xml dosyasından.</span><span class="sxs-lookup"><span data-stu-id="fe970-121">If the client code is running as part of a service, you can load `FabricTransportSettings` from the settings.xml file.</span></span> <span data-ttu-id="fe970-122">Daha önce gösterildiği gibi hizmet koduna benzer TransportSettings bir bölüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe970-122">Create a TransportSettings section that is similar to the service code, as shown earlier.</span></span> <span data-ttu-id="fe970-123">İstemci kodu aşağıdaki değişiklikleri yapın:</span><span class="sxs-lookup"><span data-stu-id="fe970-123">Make the following changes to the client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
