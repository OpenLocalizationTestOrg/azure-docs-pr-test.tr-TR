---
title: "Azure Service Fabric hizmetler için güvenli iletişim aaaHelp | Microsoft Docs"
description: "Toohelp güvenliğini nasıl iletişim güvenilir hizmetler için genel bakış çalıştıran bir Azure Service Fabric kümesi."
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
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

Güvenlik iletişim hello en önemli yönlerinden birisidir. Merhaba Reliable Services uygulama çerçevesi birkaç önceden oluşturulmuş iletişimi yığınları ve tooimprove güvenlik kullanabileceğiniz araçlar sağlar. Bu makalede nasıl kullanırken tooimprove güvenlik uzaktan iletişim hizmeti ve Windows Communication Foundation (WCF) iletişim yığını hello hakkında alınmaktadır.

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Hizmet remoting kullanırken hizmet korunmasına yardımcı olma
Var olan kullanıyoruz [örnek](service-fabric-reliable-services-communication-remoting.md) , açıklar nasıl tooset uzaktan iletişim güvenilir hizmetler için ayarlama. toohelp hizmet remoting kullanırken bir hizmeti güvenli hale getirme, aşağıdaki adımları izleyin:

1. Bir arabirim oluşturmak `IHelloWorldStateful`, hizmetiniz üzerinde uzaktan yordam çağrısı için kullanılabilecek hello yöntemleri tanımlar. Hizmetinizi kullanacak `FabricTransportServiceRemotingListener`, hello bildirilen `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` ad alanı. Bu bir `ICommunicationListener` remoting özellikleri sağlayan uygulama.

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. Dinleyici ayarları ve güvenlik kimlik bilgileri ekleyin.

    Güvenli, hizmet iletişimi hello kümedeki tüm hello düğümlerde yüklü toouse toohelp istediğiniz hello sertifikanın emin olun. Dinleyici ayarları ve güvenlik kimlik bilgileri sağlayabilir iki yolu vardır:

   1. Bunları doğrudan hello hizmet kodunda sağlar:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. Kullanarak sağlama bir [yapılandırma paketi](service-fabric-application-model.md):

       Ekleme bir `TransportSettings` hello settings.xml dosyasındaki bölümü.

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       Bu durumda, hello `CreateServiceReplicaListeners` yöntemi şöyle görünür:

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        Eklerseniz bir `TransportSettings` hello settings.xml dosyasındaki bölümünü `FabricTransportRemotingListenerSettings ` tüm hello Ayarları sayfasından Bu bölüm varsayılan olarak yüklenecektir.

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        Bu durumda, hello `CreateServiceReplicaListeners` yöntemi şöyle görünür:

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. Çağırdığınızda yöntemler güvenli bir hizmette hello kullanmak yerine hello remoting yığını kullanarak `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` sınıfı toocreate kullanımı bir hizmeti proxy'si `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`. Geçirin `FabricTransportRemotingSettings`, içeren `SecurityCredentials`.

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Merhaba istemci kodu bir hizmetin bir parçası çalışıyorsa, yükleyebilir `FabricTransportRemotingSettings` hello settings.xml dosyasından. Benzer toohello hizmeti kodu HelloWorldClientTransportSettings bölümünde daha önce gösterildiği gibi oluşturun. Değişiklikleri toohello istemci kodu aşağıdaki hello olun:

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    Merhaba istemci bir hizmetin bir parçası çalışır durumda değilse, client_name.settings.xml dosyası hello oluşturabilirsiniz hello client_name.exe olduğu aynı konumu. Ardından bu dosyada bir TransportSettings bölüm oluşturun.

    Eklerseniz, benzer toohello hizmeti, bir `TransportSettings` istemci settings.xml/client_name.settings.xml bölümünde `FabricTransportRemotingSettings` tüm hello Ayarları sayfasından Bu bölüm, varsayılan olarak yükler.

    Bu durumda, hello önceki kod daha basitleştiriliyor:  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a>Bir WCF tabanlı iletişim yığını kullanırken hizmet korunmasına yardımcı olma
Var olan kullanıyoruz [örnek](service-fabric-reliable-services-communication-wcf.md) nasıl tooset WCF tabanlı iletişim kurmak için güvenilir hizmetler yığın açıklar. toohelp bir WCF tabanlı iletişim yığını kullanırken bir hizmeti güvenli hale getirme, aşağıdaki adımları izleyin:

1. Merhaba hizmeti için toohelp güvenli hello WCF iletişimi dinleyicisi gerekir (`WcfCommunicationListener`), oluşturduğunuz. toodo bunu hello değiştirme `CreateServiceReplicaListeners` yöntemi.

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. Merhaba istemcisinde hello `WcfCommunicationClient` hello önceki oluşturulduğu sınıf [örnek](service-fabric-reliable-services-communication-wcf.md) değişmeden kalır. Ancak toooverride hello gerekir `CreateClientAsync` yöntemi `WcfCommunicationClientFactory`:

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    Kullanım `SecureWcfCommunicationClientFactory` toocreate WCF iletişimi istemcisi (`WcfCommunicationClient`). Merhaba istemci tooinvoke hizmet yöntemleri kullanın.

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a>Sonraki adımlar
* [Web API OWIN güvenilir Hizmetleri'ndeki ile](service-fabric-reliable-services-communication-webapi.md)
