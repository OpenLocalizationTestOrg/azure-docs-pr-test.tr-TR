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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Güvenli iletişim Azure Service Fabric hizmetler için Yardım
> [!div class="op_single_selector"]
> * [Windows üzerinde C#](service-fabric-reliable-services-secure-communication.md)
> * [Linux üzerinde Java](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Hizmet remoting kullanırken hizmet korunmasına yardımcı olma
Biz varolan kullanmaya başlayacağınız [örnek](service-fabric-reliable-services-communication-remoting-java.md) , açıklar nasıl tooset uzaktan iletişim güvenilir hizmetler için ayarlama. toohelp hizmet remoting kullanırken bir hizmeti güvenli hale getirme, aşağıdaki adımları izleyin:

1. Bir arabirim oluşturmak `HelloWorldStateless`, hizmetiniz üzerinde uzaktan yordam çağrısı için kullanılabilecek hello yöntemleri tanımlar. Hizmetinizi kullanacak `FabricTransportServiceRemotingListener`, hello bildirilen `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` paket. Bu bir `CommunicationListener` remoting özellikleri sağlayan uygulama.

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
2. Dinleyici ayarları ve güvenlik kimlik bilgileri ekleyin.

    Güvenli, hizmet iletişimi hello kümedeki tüm hello düğümlerde yüklü toouse toohelp istediğiniz hello sertifikanın emin olun. Dinleyici ayarları ve güvenlik kimlik bilgileri sağlayabilir iki yolu vardır:

   1. Kullanarak sağlama bir [yapılandırma paketi](service-fabric-application-model.md):

       Ekleme bir `TransportSettings` hello settings.xml dosyasındaki bölümü.

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

       Bu durumda, hello `createServiceInstanceListeners` yöntemi şöyle görünür:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Eklerseniz bir `TransportSettings` hello settings.xml dosyasındaki tüm öneki olmadan bölümünde `FabricTransportListenerSettings` tüm hello Ayarları sayfasından Bu bölüm varsayılan olarak yüklenecektir.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Bu durumda, hello `CreateServiceInstanceListeners` yöntemi şöyle görünür:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Çağırdığınızda yöntemler güvenli bir hizmette hello kullanmak yerine hello remoting yığını kullanarak `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` sınıfı toocreate kullanımı bir hizmeti proxy'si `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Merhaba istemci kodu bir hizmetin bir parçası çalışıyorsa, yükleyebilir `FabricTransportSettings` hello settings.xml dosyasından. Benzer toohello hizmeti kodu TransportSettings bölümünde daha önce gösterildiği gibi oluşturun. Değişiklikleri toohello istemci kodu aşağıdaki hello olun:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```
