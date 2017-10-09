---
title: "Azure mikro aaaSimulate hataları | Microsoft Docs"
description: "Nasıl tooharden hizmetlerinizi normal ve durunda hatalarına karşı."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: 
ms.assetid: 44af01f0-ed73-4c31-8ac0-d9d65b4ad2d6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: 05467e291dfc0f12a021955f8ea540881ec10746
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="simulate-failures-during-service-workloads"></a>Hizmet iş yükleri sırasında hata benzetimleri yapma
Azure Service Fabric Hello Test Edilebilirlik senaryolarda geliştiriciler toonot ilgilenen bireysel hatalarıyla endişe etkinleştirin. Burada bir açık istemcisi iş yükünü ve hataları Interleaving gerekebilecek senaryo vardır. istemci iş yükü ve hataları Hello Interleaving hatası olduğunda hello hizmeti bazı eylemleri gerçekte gerçekleştirmeyi sağlar. Test Edilebilirlik sağlayan denetimi Hello düzeyini verildiğinde, bunlar hello iş yükü yürütmeye kesin noktalarda olabilir. Bu endüksiyon hatalarının Merhaba uygulaması farklı durumlarda sırasında hatalar bulabilir ve kalitesini artırmak.

## <a name="sample-custom-scenario"></a>Örnek özel senaryosu
Bu test, o interleaves hello iş yüküyle bir senaryo gösterilmektedir [normal ve durunda hatalarını](service-fabric-testability-actions.md#graceful-vs-ungraceful-fault-actions). Hizmet işlemleri veya en iyi sonuçlar için işlem hello ortasında Hello hataları kopyaladığınızda.

Şimdi dört iş yükleri kullanıma sunan bir hizmet örneği yol: A, B, C ve her karşılık gelen tooa iş akışları ve olması işlem D., depolama veya bir karışımını. Basitlik Hello artırmak amacıyla için biz örneğimizde hello iş yükleri soyut. Bu örnekte yürütülen hello farklı hataları şunlardır:

* RestartNode: Durunda hataya toosimulate bir makineyi yeniden başlatın.
* RestartDeployedCodePackage: Durunda hataya toosimulate hizmeti ana bilgisayar işlemi çöküyor.
* RemoveReplica: Normal hataya toosimulate yineleme kaldırma.
* MovePrimary: Normal hataya toosimulate çoğaltma hello Service Fabric yük dengeleyici tarafından tetiklenen taşır.

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll.

using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        // Replace these strings with hello actual version for your cluster and application.
        string clusterConnection = "localhost:19000";
        Uri applicationName = new Uri("fabric:/samples/PersistentToDoListApp");
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Workload Test...");
        try
        {
            RunTestAsync(clusterConnection, applicationName, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Workload Test failed: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Workload Test completed successfully.");
        return 0;
    }

    public enum ServiceWorkloads
    {
        A,
        B,
        C,
        D
    }

    public enum ServiceFabricFaults
    {
        RestartNode,
        RestartCodePackage,
        RemoveReplica,
        MovePrimary,
    }

    public static async Task RunTestAsync(string clusterConnection, Uri applicationName, Uri serviceName)
    {
        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);
        // Maximum time toowait for a service toostabilize.
        TimeSpan maxServiceStabilizationTime = TimeSpan.FromSeconds(120);

        // How many loops of faults you want tooexecute.
        uint testLoopCount = 20;
        Random random = new Random();

        for (var i = 0; i < testLoopCount; ++i)
        {
            var workload = SelectRandomValue<ServiceWorkloads>(random);
            // Start hello workload.
            var workloadTask = RunWorkloadAsync(workload);

            // While hello task is running, induce faults into hello service. They can be ungraceful faults like
            // RestartNode and RestartDeployedCodePackage or graceful faults like RemoveReplica or MovePrimary.
            var fault = SelectRandomValue<ServiceFabricFaults>(random);

            // Create a replica selector, which will select a primary replica from hello given service tootest.
            var replicaSelector = ReplicaSelector.PrimaryOf(PartitionSelector.RandomOf(serviceName));
            // Run hello selected random fault.
            await RunFaultAsync(applicationName, fault, replicaSelector, fabricClient);
            // Validate hello health and stability of hello service.
            await fabricClient.ServiceManager.ValidateServiceAsync(serviceName, maxServiceStabilizationTime);

            // Wait for hello workload toofinish successfully.
            await workloadTask;
        }
    }

    private static async Task RunFaultAsync(Uri applicationName, ServiceFabricFaults fault, ReplicaSelector selector, FabricClient client)
    {
        switch (fault)
        {
            case ServiceFabricFaults.RestartNode:
                await client.ClusterManager.RestartNodeAsync(selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RestartCodePackage:
                await client.ApplicationManager.RestartDeployedCodePackageAsync(applicationName, selector, CompletionMode.Verify);
                break;
            case ServiceFabricFaults.RemoveReplica:
                await client.ServiceManager.RemoveReplicaAsync(selector, CompletionMode.Verify, false);
                break;
            case ServiceFabricFaults.MovePrimary:
                await client.ServiceManager.MovePrimaryAsync(selector.PartitionSelector);
                break;
        }
    }

    private static Task RunWorkloadAsync(ServiceWorkloads workload)
    {
        throw new NotImplementedException();
        // This is where you trigger and complete your service workload.
        // Note that hello faults induced while your service workload is running will
        // fault hello primary service. Hence, you will need tooreconnect toocomplete or check
        // hello status of hello workload.
    }

    private static T SelectRandomValue<T>(Random random)
    {
        Array values = Enum.GetValues(typeof(T));
        T workload = (T)values.GetValue(random.Next(values.Length));
        return workload;
    }
}
```
