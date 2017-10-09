---
title: "aaaAzure sanal makine ölçek ayarlar ile ilgili SSS | Microsoft Docs"
description: "Sanal makine ölçek kümeleri hakkında sorular yanıtlar toofrequently alın."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a><span data-ttu-id="6ef2b-103">Azure sanal makine ölçek SSS ayarlar</span><span class="sxs-lookup"><span data-stu-id="6ef2b-103">Azure virtual machine scale sets FAQs</span></span>

<span data-ttu-id="6ef2b-104">Azure'da sanal makine ölçek hakkında sorular toofrequently ayarlar yanıtlar alın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-104">Get answers toofrequently asked questions about virtual machine scale sets in Azure.</span></span>

## <a name="autoscale"></a><span data-ttu-id="6ef2b-105">Otomatik Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="6ef2b-105">Autoscale</span></span>

### <a name="what-are-best-practices-for-azure-autoscale"></a><span data-ttu-id="6ef2b-106">Azure otomatik ölçeklendirme için en iyi uygulamalar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-106">What are best practices for Azure Autoscale?</span></span>

<span data-ttu-id="6ef2b-107">Otomatik ölçeklendirme için en iyi yöntemler için bkz: [otomatik ölçeklendirmeyi sanal makineler için en iyi uygulamaları](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-107">For best practices for Autoscale, see [Best practices for autoscaling virtual machines](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).</span></span>

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a><span data-ttu-id="6ef2b-108">Ana bilgisayar tabanlı ölçümleri kullanan otomatik ölçeklendirme ölçüm adlarını nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-108">Where do I find metric names for autoscaling that uses host-based metrics?</span></span>

<span data-ttu-id="6ef2b-109">Ana bilgisayar tabanlı ölçümleri kullanan otomatik ölçeklendirmeyi için ölçüm adları için bkz: [desteklenen Azure İzleyicisi ile ölçümleri](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-109">For metric names for autoscaling that uses host-based metrics, see [Supported metrics with Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).</span></span>

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a><span data-ttu-id="6ef2b-110">Herhangi bir Azure Service Bus konu ve sıra uzunluğuna göre otomatik ölçeklendirmeyi örnekleri bulunur?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-110">Are there any examples of autoscaling based on an Azure Service Bus topic and queue length?</span></span>

<span data-ttu-id="6ef2b-111">Evet.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-111">Yes.</span></span> <span data-ttu-id="6ef2b-112">Bir Azure Service Bus konu ve sıra uzunluğuna göre otomatik ölçeklendirmeyi örnekleri için bkz: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-112">For examples of autoscaling based on an Azure Service Bus topic and queue length, see [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).</span></span>

<span data-ttu-id="6ef2b-113">Service Bus kuyruğu için JSON aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-113">For a Service Bus queue, use hello following JSON:</span></span>

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

<span data-ttu-id="6ef2b-114">Bir depolama kuyruğu için JSON aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-114">For a storage queue, use hello following JSON:</span></span>

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

<span data-ttu-id="6ef2b-115">Örnek değerler kaynak Tekdüzen Kaynak Tanımlayıcıları (URI'ler) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-115">Replace example values with your resource Uniform Resource Identifiers (URIs).</span></span>


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a><span data-ttu-id="6ef2b-116">Mıyım otomatik ölçeklendirme ana bilgisayar tabanlı ölçümleri veya tanılama uzantısını kullanarak?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-116">Should I autoscale by using host-based metrics or a diagnostics extension?</span></span>

<span data-ttu-id="6ef2b-117">Otomatik ölçeklendirme ayarı, bir VM toouse ana bilgisayar düzeyinde ölçümleri veya konuk işletim sistemi tabanlı ölçümleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-117">You can create an autoscale setting on a VM toouse host-level metrics or guest OS-based metrics.</span></span>

<span data-ttu-id="6ef2b-118">Desteklenen ölçümleri listesi için bkz: [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-118">For a list of supported metrics, see [Azure Monitor autoscaling common metrics](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics).</span></span> 

<span data-ttu-id="6ef2b-119">Sanal makine ölçek kümeleri için tam bir örnek için bkz: [sanal makine ölçek kümeleri için Resource Manager şablonları kullanarak gelişmiş otomatik ölçeklendirme yapılandırmasını](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-119">For a full sample for virtual machine scale sets, see [Advanced autoscale configuration by using Resource Manager templates for virtual machine scale sets](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets).</span></span> 

<span data-ttu-id="6ef2b-120">Merhaba örnek hello ana bilgisayar düzeyinde CPU ölçüm ve bir ileti sayısı ölçümü kullanır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-120">hello sample uses hello host-level CPU metric and a message count metric.</span></span>



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-121">Uyarı kuralları bir sanal makine ölçek kümesinde nasıl ayarlarım?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-121">How do I set alert rules on a virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-122">PowerShell veya Azure CLI aracılığıyla sanal makine ölçek kümeleri için ölçümler üzerinde uyarılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-122">You can create alerts on metrics for virtual machine scale sets via PowerShell or Azure CLI.</span></span> <span data-ttu-id="6ef2b-123">Daha fazla bilgi için bkz: [Azure İzleyici PowerShell hızlı başlangıç örnekleri](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) ve [Azure İzleyici platformlar arası CLI hızlı başlangıç örnekleri](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-123">For more information, see [Azure Monitor PowerShell quick start samples](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) and [Azure Monitor cross-platform CLI quick start samples](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).</span></span>

<span data-ttu-id="6ef2b-124">Merhaba uç noktası Targetresourceıd hello sanal makine ölçek kümesinin şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-124">hello TargetResourceId of hello virtual machine scale set looks like this:</span></span> 

<span data-ttu-id="6ef2b-125">/Subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.COMPUTE/virtualMachineScaleSets/yourvmssname</span><span class="sxs-lookup"><span data-stu-id="6ef2b-125">/subscriptions/yoursubscriptionid/resourceGroups/yourresourcegroup/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmssname</span></span>

<span data-ttu-id="6ef2b-126">Tüm VM performans sayacı için bir uyarı hello ölçüm tooset seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-126">You can choose any VM performance counter as hello metric tooset an alert for.</span></span> <span data-ttu-id="6ef2b-127">Daha fazla bilgi için bkz: [Resource Manager tabanlı Windows VM'ler için konuk işletim sistemi ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) ve [Linux VM'ler için konuk işletim sistemi ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) hello içinde [Azure İzleyici otomatik ölçeklendirmeyi ortak ölçümleri](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)makalesi.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-127">For more information, see [Guest OS metrics for Resource Manager-based Windows VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) and [Guest OS metrics for Linux VMs](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) in hello [Azure Monitor autoscaling common metrics](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/) article.</span></span>

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a><span data-ttu-id="6ef2b-128">PowerShell kullanarak bir sanal makine ölçek göre otomatik ölçeklendirme nasıl ayarlayabilirim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-128">How do I set up autoscale on a virtual machine scale set by using PowerShell?</span></span>

<span data-ttu-id="6ef2b-129">PowerShell kullanarak bir sanal makine ölçek göre otomatik ölçeklendirme yukarı tooset hello blog yayınına bakın [nasıl tooadd otomatik ölçeklendirme tooan Azure sanal makine ölçek kümesi](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-129">tooset up autoscale on a virtual machine scale set by using PowerShell, see hello blog post [How tooadd autoscale tooan Azure virtual machine scale set](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).</span></span>




## <a name="certificates"></a><span data-ttu-id="6ef2b-130">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="6ef2b-130">Certificates</span></span>

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a><span data-ttu-id="6ef2b-131">Nasıl bir sertifika toohello VM güvenli bir şekilde sevk?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-131">How do I securely ship a certificate toohello VM?</span></span> <span data-ttu-id="6ef2b-132">Bir sanal makine ölçek kümesi toorun burada hello hello Web sitesi için SSL güvenli bir şekilde bir sertifikayı yapılandırmasından sevk bir Web sitesi nasıl sağlama?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-132">How do I provision a virtual machine scale set toorun a website where hello SSL for hello website is shipped securely from a certificate configuration?</span></span> <span data-ttu-id="6ef2b-133">(Merhaba ortak sertifika döndürme işlemi olması neredeyse hello yapılandırmasını güncelleştirme işlemi ile aynı.) Nasıl bir örnek zorunda toodo bu?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-133">(hello common certificate rotation operation would be almost hello same as a configuration update operation.) Do you have an example of how toodo this?</span></span> 

<span data-ttu-id="6ef2b-134">toosecurely sevk sertifika toohello VM, bir müşteri sertifikası, doğrudan bir Windows sertifika deposuna hello Müşteri'nin anahtar Kasası'ndan yükleyebilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-134">toosecurely ship a certificate toohello VM, you can install a customer certificate directly into a Windows certificate store from hello customer's key vault.</span></span>

<span data-ttu-id="6ef2b-135">JSON aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-135">Use hello following JSON:</span></span>

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

<span data-ttu-id="6ef2b-136">Merhaba kodu, Windows ve Linux destekler.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-136">hello code supports Windows and Linux.</span></span>

<span data-ttu-id="6ef2b-137">Daha fazla bilgi için bkz: [oluştur veya güncelleştir bir sanal makine ölçek kümesi](https://msdn.microsoft.com/library/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-137">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/mt589035.aspx).</span></span>


### <a name="example-of-self-signed-certificate"></a><span data-ttu-id="6ef2b-138">Otomatik olarak imzalanan sertifika örneği</span><span class="sxs-lookup"><span data-stu-id="6ef2b-138">Example of Self-signed certificate</span></span>

1.  <span data-ttu-id="6ef2b-139">Kendinden imzalı bir sertifika bir anahtar kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-139">Create a self-signed certificate in a key vault.</span></span>

    <span data-ttu-id="6ef2b-140">Merhaba aşağıdaki PowerShell komutlarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-140">Use hello following PowerShell commands:</span></span>

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    <span data-ttu-id="6ef2b-141">Bu komut hello Azure Resource Manager şablonu için giriş hello olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-141">This command gives you hello input for hello Azure Resource Manager template.</span></span>

    <span data-ttu-id="6ef2b-142">Bir örneğini nasıl otomatik olarak imzalanan bir sertifika bir anahtar kasasına toocreate görmek için [Service Fabric kümesi güvenlik senaryoları](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-142">For an example of how toocreate a self-signed certificate in a key vault, see [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).</span></span>

2.  <span data-ttu-id="6ef2b-143">Merhaba Resource Manager şablonu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-143">Change hello Resource Manager template.</span></span>

    <span data-ttu-id="6ef2b-144">Bu özellik çok ekleme**virtualMachineProfile**, hello bir parçası olarak, kaynak sanal makine ölçek kümesi:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-144">Add this property too**virtualMachineProfile**, as part of hello virtual machine scale set resource:</span></span>

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a><span data-ttu-id="6ef2b-145">SSH kimlik doğrulaması için bir SSH anahtar çifti toouse Resource Manager şablonu ayarlamak Linux sanal makine ölçek ile belirtebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-145">Can I specify an SSH key pair toouse for SSH authentication with a Linux virtual machine scale set from a Resource Manager template?</span></span>  

<span data-ttu-id="6ef2b-146">Evet.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-146">Yes.</span></span> <span data-ttu-id="6ef2b-147">Merhaba REST API için **osProfile** benzer toohello standart VM REST API'dır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-147">hello REST API for **osProfile** is similar toohello standard VM REST API.</span></span> 

<span data-ttu-id="6ef2b-148">Dahil **osProfile** şablonunuzda:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-148">Include **osProfile** in your template:</span></span>

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
<span data-ttu-id="6ef2b-149">Bu JSON bloğu kullanılan [hello 101 vm sshkey GitHub Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-149">This JSON block is used in [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>
 
<span data-ttu-id="6ef2b-150">Merhaba işletim sistemi profili de kullanılıyor [hello grelayhost.json GitHub hızlı başlatma şablonunu](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-150">hello OS profile also is used in [hello grelayhost.json GitHub quick start template](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).</span></span>

<span data-ttu-id="6ef2b-151">Daha fazla bilgi için bkz: [oluştur veya güncelleştir bir sanal makine ölçek kümesi](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-151">For more information, see [Create or update a virtual machine scale set](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).</span></span>
  

### <a name="how-do-i-remove-deprecated-certificates"></a><span data-ttu-id="6ef2b-152">Kullanım dışı sertifikaları nasıl kaldırılsın mı?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-152">How do I remove deprecated certificates?</span></span> 

<span data-ttu-id="6ef2b-153">tooremove sertifikalar, hello kasası sertifikalar listesinden Kaldır hello eski sertifika kullanım dışı.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-153">tooremove deprecated certificates, remove hello old certificate from hello vault certificates list.</span></span> <span data-ttu-id="6ef2b-154">Bilgisayarınızda hello listesinde tooremain istediğiniz tüm hello sertifikaları bırakın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-154">Leave all hello certificates that you want tooremain on your computer in hello list.</span></span> <span data-ttu-id="6ef2b-155">Bu hello sertifikayı, tüm VM'lerin kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-155">This does not remove hello certificate from all your VMs.</span></span> <span data-ttu-id="6ef2b-156">Ayrıca hello sertifika toonew hello sanal makine ölçek kümesindeki oluşturulan VM'ler eklemez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-156">It also does not add hello certificate toonew VMs that are created in hello virtual machine scale set.</span></span> 

<span data-ttu-id="6ef2b-157">Varolan vm'lerden tooremove hello sertifika, sertifika deposundan uzantı toomanually Kaldır hello sertifikaları özel bir komut dosyası yazma.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-157">tooremove hello certificate from existing VMs, write a custom script extension toomanually remove hello certificates from your certificate store.</span></span>
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a><span data-ttu-id="6ef2b-158">Nasıl ı mevcut bir SSH ortak anahtarı hello sanal makine ölçek kümesi SSH katmana sağlama sırasında Ekle?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-158">How do I inject an existing SSH public key into hello virtual machine scale set SSH layer during provisioning?</span></span> <span data-ttu-id="6ef2b-159">Toostore hello SSH ortak anahtarı değerleri Azure anahtar kasası istediğiniz ve bunları my Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-159">I want toostore hello SSH public key values in Azure Key Vault, and then use them in my Resource Manager template.</span></span>

<span data-ttu-id="6ef2b-160">Genel SSH anahtarı ile yalnızca bir hello VM'ler sağlıyorsanız tooput hello ortak anahtarlar, anahtar kasasında gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-160">If you are providing hello VMs only with a public SSH key, you don't need tooput hello public keys in Key Vault.</span></span> <span data-ttu-id="6ef2b-161">Ortak anahtarlar gizli değildir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-161">Public keys are not secret.</span></span>
 
<span data-ttu-id="6ef2b-162">Bir Linux VM oluşturduğunuzda SSH ortak anahtarları düz metin sağlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-162">You can provide SSH public keys in plain text when you create a Linux VM:</span></span>

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
<span data-ttu-id="6ef2b-163">linuxConfiguration öğe adı</span><span class="sxs-lookup"><span data-stu-id="6ef2b-163">linuxConfiguration element name</span></span> | <span data-ttu-id="6ef2b-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6ef2b-164">Required</span></span> | <span data-ttu-id="6ef2b-165">Tür</span><span class="sxs-lookup"><span data-stu-id="6ef2b-165">Type</span></span> | <span data-ttu-id="6ef2b-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6ef2b-166">Description</span></span>
--- | --- | --- | --- |  ---
<span data-ttu-id="6ef2b-167">SSH</span><span class="sxs-lookup"><span data-stu-id="6ef2b-167">ssh</span></span> | <span data-ttu-id="6ef2b-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="6ef2b-168">No</span></span> | <span data-ttu-id="6ef2b-169">Koleksiyon</span><span class="sxs-lookup"><span data-stu-id="6ef2b-169">Collection</span></span> | <span data-ttu-id="6ef2b-170">Merhaba SSH anahtar yapılandırması Linux işletim sistemi belirtir</span><span class="sxs-lookup"><span data-stu-id="6ef2b-170">Specifies hello SSH key configuration for a Linux OS</span></span>
<span data-ttu-id="6ef2b-171">Yol</span><span class="sxs-lookup"><span data-stu-id="6ef2b-171">path</span></span> | <span data-ttu-id="6ef2b-172">Evet</span><span class="sxs-lookup"><span data-stu-id="6ef2b-172">Yes</span></span> | <span data-ttu-id="6ef2b-173">Dize</span><span class="sxs-lookup"><span data-stu-id="6ef2b-173">String</span></span> | <span data-ttu-id="6ef2b-174">Burada hello SSH anahtarlarını veya sertifika yerleştirilmelidir hello Linux dosya yolunu belirtir</span><span class="sxs-lookup"><span data-stu-id="6ef2b-174">Specifies hello Linux file path where hello SSH keys or certificate should be located</span></span>
<span data-ttu-id="6ef2b-175">anahtar verileri</span><span class="sxs-lookup"><span data-stu-id="6ef2b-175">keyData</span></span> | <span data-ttu-id="6ef2b-176">Evet</span><span class="sxs-lookup"><span data-stu-id="6ef2b-176">Yes</span></span> | <span data-ttu-id="6ef2b-177">Dize</span><span class="sxs-lookup"><span data-stu-id="6ef2b-177">String</span></span> | <span data-ttu-id="6ef2b-178">Bir base64 ile kodlanmış SSH ortak anahtarını belirtir</span><span class="sxs-lookup"><span data-stu-id="6ef2b-178">Specifies a base64-encoded SSH public key</span></span>

<span data-ttu-id="6ef2b-179">Bir örnek için bkz: [hello 101 vm sshkey GitHub Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-179">For an example, see [hello 101-vm-sshkey GitHub quick start template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).</span></span>

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a><span data-ttu-id="6ef2b-180">I çalıştırdığınızda `Update-AzureRmVmss` birden fazla sertifika hello ekledikten sonra aynı kasası, görüyorum anahtarın hello ileti:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-180">When I run `Update-AzureRmVmss` after adding more than one certificate from hello same key vault, I see hello following message:</span></span>
 
><span data-ttu-id="6ef2b-181">Update-AzureRmVmss: /subscriptions/ < my abonelik-kimliği > yinelenen örnekleri listesi gizli içeren / devre dışı bırakılmış resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-181">Update-AzureRmVmss: List secret contains repeated instances of /subscriptions/<my-subscription-id>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, which is disallowed.</span></span>
 
<span data-ttu-id="6ef2b-182">Toore çalışırsanız, bu durum oluşabilir-aynı kasa hello mevcut kaynak kasası için yeni bir kasa sertifika kullanmak yerine hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-182">This can happen if you try toore-add hello same vault instead of using a new vault certificate for hello existing source vault.</span></span> <span data-ttu-id="6ef2b-183">Merhaba `Add-AzureRmVmssSecret` komutu düzgün çalışmaz ek gizli ekliyorsanız.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-183">hello `Add-AzureRmVmssSecret` command does not work correctly if you are adding additional secrets.</span></span>
 
<span data-ttu-id="6ef2b-184">tooadd hello öğesinden daha fazla gizli aynı anahtar kasası, güncelleştirme hello $vmss.properties.osProfile.secrets[0].vaultCertificates listesi.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-184">tooadd more secrets from hello same key vault, update hello $vmss.properties.osProfile.secrets[0].vaultCertificates list.</span></span>
 
<span data-ttu-id="6ef2b-185">Giriş yapısında Hello beklenen için bkz: [bir sanal makine oluştur veya güncelleştir kümesi](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-185">For hello expected input structure, see [Create or update a virtual machine set](https://msdn.microsoft.com/library/azure/mt589035.aspx).</span></span>
 
<span data-ttu-id="6ef2b-186">Merhaba gizli hello anahtar kasasına hello sanal makine ölçek kümesi nesnesi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-186">Find hello secret in hello virtual machine scale set object that is in hello key vault.</span></span> <span data-ttu-id="6ef2b-187">Ardından, hello kasayla ilişkili sertifikayı başvurusu (Merhaba URL ve hello gizli deposu adı) toohello listenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-187">Then, add your certificate reference (hello URL and hello secret store name) toohello list associated with hello vault.</span></span>

> [!NOTE] 
> <span data-ttu-id="6ef2b-188">Şu anda hello sanal makine ölçek kümesi API'sini kullanarak sertifikaları Vm'lerden kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-188">Currently, you cannot remove certificates from VMs by using hello virtual machine scale set API.</span></span>
>

<span data-ttu-id="6ef2b-189">Yeni VM'ler hello eski sertifika sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-189">New VMs will not have hello old certificate.</span></span> <span data-ttu-id="6ef2b-190">Ancak, hello sertifikası varsa ve hangi zaten dağıtılan VM'ler hello eski sertifika gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-190">However, VMs that have hello certificate and which are already deployed will have hello old certificate.</span></span>
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a><span data-ttu-id="6ef2b-191">Sertifikaları toohello sanal makineyi ölçeği hello sertifika hello gizli deposunda olduğunda hello parola sağlamadan Ayarla itme?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-191">Can I push certificates toohello virtual machine scale set without providing hello password, when hello certificate is in hello secret store?</span></span>

<span data-ttu-id="6ef2b-192">Komut dosyaları toohard kod parolalarda gerekmez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-192">You do not need toohard-code passwords in scripts.</span></span> <span data-ttu-id="6ef2b-193">Dinamik olarak parolaları almak hello izinlerle toorun hello dağıtım komut dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-193">You can dynamically retrieve passwords with hello permissions you use toorun hello deployment script.</span></span> <span data-ttu-id="6ef2b-194">Bir sertifika hello gizli deposu anahtar Kasası'nı taşır bir komut dosyası varsa, gizli deposu hello `get certificate` komut ayrıca hello parola hello .pfx dosyasının çıkarır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-194">If you have a script that moves a certificate from hello secret store key vault, hello secret store `get certificate` command also outputs hello password of hello .pfx file.</span></span>
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a><span data-ttu-id="6ef2b-195">Bir sanal makine ölçek virtualMachineProfile.osProfile hello gizli özelliği iş nasıl ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-195">How does hello Secrets property of virtualMachineProfile.osProfile for a virtual machine scale set work?</span></span> <span data-ttu-id="6ef2b-196">Merhaba certificateUrl özelliğini kullanarak bir sertifika için mutlak URI hello toospecify olduğunda neden hello sourceVault değeri gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-196">Why do I need hello sourceVault value when I have toospecify hello absolute URI for a certificate by using hello certificateUrl property?</span></span> 

<span data-ttu-id="6ef2b-197">Windows Uzaktan Yönetim (WinRM) sertifika başvurusu hello hello işletim sistemi profili gizli özelliği mevcut olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-197">A Windows Remote Management (WinRM) certificate reference must be present in hello Secrets property of hello OS profile.</span></span> 

<span data-ttu-id="6ef2b-198">Merhaba amacı hello kaynak kasası belirten bir kullanıcının Azure bulut hizmeti modeli kayıtlı tooenforce erişim denetimi listesi (ACL) İlkeleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-198">hello purpose of indicating hello source vault is tooenforce access control list (ACL) policies that exist in a user's Azure Cloud Service model.</span></span> <span data-ttu-id="6ef2b-199">Merhaba kaynak kasası belirtilmezse, izinleri toodeploy veya erişim gizli tooa anahtar kasası sahip olmayan kullanıcıların mümkün toothrough işlem kaynak sağlayıcısı (CRP) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-199">If hello source vault isn't specified, users who do not have permissions toodeploy or access secrets tooa key vault would be able toothrough a Compute Resource Provider (CRP).</span></span> <span data-ttu-id="6ef2b-200">ACL'ler bile mevcut kaynakları için mevcut.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-200">ACLs exist even for resources that do not exist.</span></span>

<span data-ttu-id="6ef2b-201">Yanlış kaynak kasa kimliği geçerli anahtar kasası URL'si ancak sağlarsanız, hello işlemi yoklama zaman bir hata bildirilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-201">If you provide an incorrect source vault ID but a valid key vault URL, an error is reported when you poll hello operation.</span></span>
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a><span data-ttu-id="6ef2b-202">Sanal makine ölçek kümesi varolan gizli tooan eklerseniz, hello gizli VM'ler, veya yalnızca yenilerini eklenen?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-202">If I add secrets tooan existing virtual machine scale set, are hello secrets injected into existing VMs, or only into new ones?</span></span> 

<span data-ttu-id="6ef2b-203">Sertifikaları tooall eklenen bile olanları önceden var olan Vm'leriniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-203">Certificates are added tooall your VMs, even preexisting ones.</span></span> <span data-ttu-id="6ef2b-204">UpgradePolicy özelliği, sanal makine ölçek kümesi çok ayarlanır**el ile**, hello sertifika hello VM üzerinde el ile güncelleştirme gerçekleştirdiğinizde toohello VM eklendi.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-204">If your virtual machine scale set upgradePolicy property is set too**manual**, hello certificate is added toohello VM when you perform a manual update on hello VM.</span></span>
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a><span data-ttu-id="6ef2b-205">Linux VM'ler için burada sertifikaları put?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-205">Where do I put certificates for Linux VMs?</span></span>

<span data-ttu-id="6ef2b-206">Linux VM'ler için toodeploy sertifikaları nasıl görürüm toolearn [sertifikaları tooVMs müşteri tarafından yönetilen bir anahtar Kasası'ndan dağıtmak](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-206">toolearn how toodeploy certificates for Linux VMs, see [Deploy certificates tooVMs from a customer-managed key vault](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).</span></span>
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a><span data-ttu-id="6ef2b-207">Yeni kasa sertifika tooa yeni bir sertifika nesnesi nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-207">How do I add a new vault certificate tooa new certificate object?</span></span>

<span data-ttu-id="6ef2b-208">tooadd bir kasa sertifika tooan varolan gizlilik hello aşağıdaki PowerShell örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-208">tooadd a vault certificate tooan existing secret, see hello following PowerShell example.</span></span> <span data-ttu-id="6ef2b-209">Yalnızca bir gizli nesnesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-209">Use only one secret object.</span></span>
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a><span data-ttu-id="6ef2b-210">Bir VM yeniden görüntü oluşturma toocertificates ne olur?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-210">What happens toocertificates if you reimage a VM?</span></span>

<span data-ttu-id="6ef2b-211">Bir VM yeniden görüntü oluşturma sertifikaları silinir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-211">If you reimage a VM, certificates are deleted.</span></span> <span data-ttu-id="6ef2b-212">Siler hello tüm işletim sistemi diski yeniden görüntüsünü oluşturuyor.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-212">Reimaging deletes hello entire OS disk.</span></span> 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a><span data-ttu-id="6ef2b-213">Bir sertifika hello anahtar Kasası'nı silersem ne olur?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-213">What happens if you delete a certificate from hello key vault?</span></span>

<span data-ttu-id="6ef2b-214">Merhaba gizli anahtar Kasası'hello silinir ve ardından çalıştırırsanız `stop deallocate` tüm VM'ler için ve sonra yeniden başlatın, bir hatayla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-214">If hello secret is deleted from hello key vault, and then you run `stop deallocate` for all your VMs and then start them again, you will encounter a failure.</span></span> <span data-ttu-id="6ef2b-215">Merhaba CRP tooretrieve hello gizli hello anahtar Kasası'ndan gerekiyor, ancak bu işlem gerçekleştirilemiyor Hello hatası oluşur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-215">hello failure occurs because hello CRP needs tooretrieve hello secrets from hello key vault, but it cannot.</span></span> <span data-ttu-id="6ef2b-216">Bu senaryoda, hello sanal makine ölçek kümesi modelden hello sertifikaları silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-216">In this scenario, you can delete hello certificates from hello virtual machine scale set model.</span></span> 

<span data-ttu-id="6ef2b-217">Merhaba CRP bileşen müşteri gizli kalmaz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-217">hello CRP component does not persist customer secrets.</span></span> <span data-ttu-id="6ef2b-218">Çalıştırırsanız `stop deallocate` hello sanal makine ölçek kümesindeki tüm VM'ler için hello önbellek silinir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-218">If you run `stop deallocate` for all VMs in hello virtual machine scale set, hello cache is deleted.</span></span> <span data-ttu-id="6ef2b-219">Bu senaryoda, gizli anahtar Kasası'hello alınır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-219">In this scenario, secrets are retrieved from hello key vault.</span></span>

<span data-ttu-id="6ef2b-220">Azure Service Fabric hello gizliliği (modelindeki hello tek doku Kiracı) önbelleğe alınmış bir kopyasını olduğundan ölçeğini olduğunda bu sorunla karşılaştığınızda yok.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-220">You don't encounter this problem when scaling out because there is a cached copy of hello secret in Azure Service Fabric (in hello single-fabric tenant model).</span></span>
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a><span data-ttu-id="6ef2b-221">Neden toospecify hello hello sertifika URL'si için tam olarak konum sahibim (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>) belirtilen gibi [Service Fabric kümesi güvenlik senaryoları](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-221">Why do I have toospecify hello exact location for hello certificate URL (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), as indicated in [Service Fabric cluster security scenarios](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?</span></span>
 
<span data-ttu-id="6ef2b-222">Hello Azure anahtar kasası belgelerine hello sürüm belirtilmezse, gizli anahtarı REST API alma hello gizli hello en son sürüm döndürmelidir bu hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-222">hello Azure Key Vault documentation states that hello Get Secret REST API should return hello latest version of hello secret if hello version is not specified.</span></span>
 
<span data-ttu-id="6ef2b-223">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6ef2b-223">Method</span></span> | <span data-ttu-id="6ef2b-224">URL</span><span class="sxs-lookup"><span data-stu-id="6ef2b-224">URL</span></span>
--- | ---
<span data-ttu-id="6ef2b-225">AL</span><span class="sxs-lookup"><span data-stu-id="6ef2b-225">GET</span></span> | <span data-ttu-id="6ef2b-226">https://mykeyvault.Vault.Azure.NET/Secrets/ {gizli-adı} / {gizli-version}? api-version = {api-version}</span><span class="sxs-lookup"><span data-stu-id="6ef2b-226">https://mykeyvault.vault.azure.net/secrets/{secret-name}/{secret-version}?api-version={api-version}</span></span>

<span data-ttu-id="6ef2b-227">Değiştirin {*gizli anahtarı adı*} hello adı ve Değiştir {*gizli sürüm*} hello hello gizli sürümüyle tooretrieve istiyor.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-227">Replace {*secret-name*} with hello name, and replace {*secret-version*} with hello version of hello secret you want tooretrieve.</span></span> <span data-ttu-id="6ef2b-228">Merhaba gizli sürüm dışarıda.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-228">hello secret version might be excluded.</span></span> <span data-ttu-id="6ef2b-229">Bu durumda, hello geçerli sürümü alınır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-229">In that case, hello current version is retrieved.</span></span>
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a><span data-ttu-id="6ef2b-230">Anahtar kasası kullandığınızda neden toospecify hello sertifika sürümü var mı?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-230">Why do I have toospecify hello certificate version when I use Key Vault?</span></span>

<span data-ttu-id="6ef2b-231">Merhaba anahtar kasası gereksinim toospecify hello sertifika sürümü Hello amacı, hangi sertifikanın Vm'leri üzerinde dağıtılan toohello kullanıcı işaretini toomake budur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-231">hello purpose of hello Key Vault requirement toospecify hello certificate version is toomake it clear toohello user what certificate is deployed on their VMs.</span></span>

<span data-ttu-id="6ef2b-232">Bir VM oluşturun ve ardından hello anahtar kasasına gizli güncelleştirirseniz hello yeni sertifika indirilen tooyour VM'ler değil.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-232">If you create a VM and then update your secret in hello key vault, hello new certificate is not downloaded tooyour VMs.</span></span> <span data-ttu-id="6ef2b-233">Ancak, sanal makineleri ve yeni VM'ler hello yeni parolası mı almak tooreference görünür.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-233">But your VMs appear tooreference it, and new VMs get hello new secret.</span></span> <span data-ttu-id="6ef2b-234">tooavoid Bu, gerekli tooreference gizli bir sürümü olan.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-234">tooavoid this, you are required tooreference a secret version.</span></span>

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-235">Ekibin toous .cer ortak anahtarlar olarak dağıtılan birkaç sertifika çalışır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-235">My team works with several certificates that are distributed toous as .cer public keys.</span></span> <span data-ttu-id="6ef2b-236">Bu sertifikalar tooa sanal makine ölçek kümesini dağıtmak için bir yaklaşım önerilir hello nedir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-236">What is hello recommended approach for deploying these certificates tooa virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-237">toodeploy .cer ortak anahtarları tooa sanal makine ölçek kümesi, yalnızca .cer dosyaları içeren bir .pfx dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-237">toodeploy .cer public keys tooa virtual machine scale set, you can generate a .pfx file that contains only .cer files.</span></span> <span data-ttu-id="6ef2b-238">toodo Bu, kullanım `X509ContentType = Pfx`.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-238">toodo this, use `X509ContentType = Pfx`.</span></span> <span data-ttu-id="6ef2b-239">Örneğin, C# veya PowerShell x509Certificate2 nesne olarak hello .cer dosyasını yüklemek ve ardından hello yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-239">For example, load hello .cer file as an x509Certificate2 object in C# or PowerShell, and then call hello method.</span></span> 

<span data-ttu-id="6ef2b-240">Daha fazla bilgi için bkz: [X509Certificate.Export yöntemi (X509ContentType, dize)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-240">For more information, see [X509Certificate.Export Method (X509ContentType, String)](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).</span></span>

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a><span data-ttu-id="6ef2b-241">Kullanıcıların toopass sertifikaları için bir seçenek base64 dize olarak görmüyorum.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-241">I do not see an option for users toopass in certificates as base64 strings.</span></span> <span data-ttu-id="6ef2b-242">Çoğu diğer kaynak sağlayıcıları bu seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-242">Most other resource providers have this option.</span></span>

<span data-ttu-id="6ef2b-243">bir sertifika bir base64 dizesi olarak geçirme tooemulate hello en son sürümü tutulan URL bir Resource Manager şablonu ayıklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-243">tooemulate passing in a certificate as a base64 string, you can extract hello latest versioned URL in a Resource Manager template.</span></span> <span data-ttu-id="6ef2b-244">Resource Manager şablonu JSON özelliğinde aşağıdaki hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-244">Include hello following JSON property in your Resource Manager template:</span></span>

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a><span data-ttu-id="6ef2b-245">Toowrap sertifikaları JSON nesnelerindeki anahtar kasalarını içinde gerekiyor?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-245">Do I have toowrap certificates in JSON objects in key vaults?</span></span>

<span data-ttu-id="6ef2b-246">Sanal makine ölçek kümeleri ve sanal makineleri, sertifikaları JSON nesneleri alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-246">In virtual machine scale sets and VMs, certificates must be wrapped in JSON objects.</span></span> 

<span data-ttu-id="6ef2b-247">Ayrıca hello içerik türü uygulama/x-pkcs12 destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-247">We also support hello content type application/x-pkcs12.</span></span> <span data-ttu-id="6ef2b-248">Uygulama/x-pkcs12 kullanma ile ilgili yönergeler için bkz: [Azure anahtar kasası PFX sertifikaları](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-248">For instructions on using application/x-pkcs12, see [PFX certificates in Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).</span></span>
 
<span data-ttu-id="6ef2b-249">Şu anda .cer dosyaları desteklemiyoruz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-249">We currently do not support .cer files.</span></span> <span data-ttu-id="6ef2b-250">toouse .cer, dışarı aktarma dosyaları bunları .pfx kapsayıcılarına.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-250">toouse .cer files, export them into .pfx containers.</span></span>



## <a name="compliance"></a><span data-ttu-id="6ef2b-251">Uyumluluk</span><span class="sxs-lookup"><span data-stu-id="6ef2b-251">Compliance</span></span>

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a><span data-ttu-id="6ef2b-252">Sanal makine ölçek PCI uyumlu ayarlar misiniz?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-252">Are virtual machine scale sets PCI-compliant?</span></span>

<span data-ttu-id="6ef2b-253">Sanal makine ölçek kümeleri hello CRP üstünde basit bir API katmandır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-253">Virtual machine scale sets are a thin API layer on top of hello CRP.</span></span> <span data-ttu-id="6ef2b-254">Her iki bileşenin hello işlem platformunda hello Azure hizmeti ağacında bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-254">Both components are part of hello compute platform in hello Azure service tree.</span></span>

<span data-ttu-id="6ef2b-255">Uyumluluk açısından bakıldığında, sanal makine ölçek kümeleri hello Azure işlem platformu, temel bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-255">From a compliance perspective, virtual machine scale sets are a fundamental part of hello Azure compute platform.</span></span> <span data-ttu-id="6ef2b-256">Bir takım, araçları, işlemler, dağıtım yöntemi, güvenlik denetimleri, yalnızca saat (JIT) derleme, izleme, uyarı ve benzeri hello CRP ile kendini paylaştıkları.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-256">They share a team, tools, processes, deployment methodology, security controls, just-in-time (JIT) compilation, monitoring, alerting, and so on, with hello CRP itself.</span></span> <span data-ttu-id="6ef2b-257">Sanal makine ölçek kümeleri olan ödeme kartı endüstrisi (PCI)-hello CRP hello geçerli PCI veri güvenliği standardı (DSS) kanıtlama parçası olduğundan uyumlu.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-257">Virtual machine scale sets are Payment Card Industry (PCI)-compliant because hello CRP is part of hello current PCI Data Security Standard (DSS) attestation.</span></span>

<span data-ttu-id="6ef2b-258">Daha fazla bilgi için bkz: [Microsoft Trust Center hello](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-258">For more information, see [hello Microsoft Trust Center](https://www.microsoft.com/TrustCenter/Compliance/PCI).</span></span>






## <a name="extensions"></a><span data-ttu-id="6ef2b-259">Uzantılar</span><span class="sxs-lookup"><span data-stu-id="6ef2b-259">Extensions</span></span>

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a><span data-ttu-id="6ef2b-260">Bir sanal makine ölçek kümesi uzantısının nasıl silebilirim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-260">How do I delete a virtual machine scale set extension?</span></span>

<span data-ttu-id="6ef2b-261">bir sanal makine ölçek toodelete uzantısı, aşağıdaki PowerShell örneğine kullanım hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-261">toodelete a virtual machine scale set extension, use hello following PowerShell example:</span></span>

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
<span data-ttu-id="6ef2b-262">Merhaba UzantıAdı değeri bulun `$vmss`.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-262">You can find hello extensionName value in `$vmss`.</span></span>
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a><span data-ttu-id="6ef2b-263">Operations Management Suite ile tümleşir şablon örnek bir sanal makine ölçek kümesi var mı?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-263">Is there a virtual machine scale set template example that integrates with Operations Management Suite?</span></span>

<span data-ttu-id="6ef2b-264">Operations Management Suite ile tümleşir şablon örnek bir sanal makine ölçek kümesi için hello ikinci örneğe bakın [Azure Service Fabric kümesi dağıtma ve günlük analizi kullanarak izlemeyi etkinleştir](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-264">For a virtual machine scale set template example that integrates with Operations Management Suite, see hello second example in [Deploy an Azure Service Fabric cluster and enable monitoring by using Log Analytics](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).</span></span>
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a><span data-ttu-id="6ef2b-265">Uzantılar, sanal makine ölçek kümeleri üzerinde paralel toorun gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-265">Extensions seem toorun in parallel on virtual machine scale sets.</span></span> <span data-ttu-id="6ef2b-266">Bu, my özel betik uzantısı toofail neden olur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-266">This causes my custom script extension toofail.</span></span> <span data-ttu-id="6ef2b-267">Toofix bu ne yapabilirim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-267">What can I do toofix this?</span></span>

<span data-ttu-id="6ef2b-268">sanal makine ölçek kümesindeki uzantısı sıralama hakkında toolearn bkz [uzantısı sıralaması Azure sanal makine ölçek kümeleri](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-268">toolearn about extension sequencing in virtual machine scale sets, see [Extension sequencing in Azure virtual machine scale sets](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).</span></span>
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-269">Nasıl ı hello parola VM'ler için my sanal makine ölçek kümesindeki sıfırlama?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-269">How do I reset hello password for VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-270">tooreset hello Parolada VM'ler için sanal makine ölçek kümesi, VM erişimi uzantılarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-270">tooreset hello password for VMs in your virtual machine scale set, use VM access extensions.</span></span> 

<span data-ttu-id="6ef2b-271">Aşağıdaki PowerShell örneğine hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-271">Use hello following PowerShell example:</span></span>

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-272">My sanal makine ölçek kümesindeki nasıl uzantısı tooall VM'ler eklensin mi?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-272">How do I add an extension tooall VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-273">Güncelleştirme ilkesi çok ayarlarsanız**otomatik**, hello şablonla dağıtarak hello yeni uzantısı özellikleri tüm VM'ler güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-273">If update policy is set too**automatic**, redeploying hello template with hello new extension properties updates all VMs.</span></span>

<span data-ttu-id="6ef2b-274">Güncelleştirme ilkesi çok ayarlarsanız**el ile**hello uzantısı güncelleştirin ve sonra tüm örneklerde Vm'leriniz el ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-274">If update policy is set too**manual**, first update hello extension, and then manually update all instances in your VMs.</span></span>

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a><span data-ttu-id="6ef2b-275">Varolan bir sanal makine ölçek kümesi ile ilişkilendirilmiş hello uzantılarını güncelleştirilmişse, etkilenen VM'ler mevcut olan?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-275">If hello extensions associated with an existing virtual machine scale set are updated, are existing VMs affected?</span></span> <span data-ttu-id="6ef2b-276">(Diğer bir deyişle, VM'ler hello *değil* eşleşme hello sanal makine ölçek kümesi modelinde?) Veya göz ardı edilir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-276">(That is, will hello VMs *not* match hello virtual machine scale set model?) Or are they ignored?</span></span> <span data-ttu-id="6ef2b-277">Var olan bir makine hizmet gösteriyor başlatıldığı ya da şu anda yürütülen hello sanal makine ölçek kümesinde yapılandırılmış hello komut dosyaları veya VM ilk oluşturulduğunda hello kullanıldığında yapılandırılmış hello betiklerdir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-277">When an existing machine is service-healed or reimaged, are hello scripts that are currently configured on hello virtual machine scale set executed, or are hello scripts that were configured when hello VM was first created used?</span></span>

<span data-ttu-id="6ef2b-278">Merhaba uzantısı hello sanal makine ölçek tanımında ayarlarsanız modeli güncelleştirilir ve hello upgradePolicy özelliği çok ayarlayın**otomatik**, hello VM'ler güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-278">If hello extension definition in hello virtual machine scale set model is updated and hello upgradePolicy property is set too**automatic**, it updates hello VMs.</span></span> <span data-ttu-id="6ef2b-279">Merhaba upgradePolicy özelliği çok ayarlanmışsa**el ile**, uzantıları işaretlenen hello modeli eşleşmeyen olarak.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-279">If hello upgradePolicy property is set too**manual**, extensions are flagged as not matching hello model.</span></span> 

<span data-ttu-id="6ef2b-280">Mevcut bir VM'yi hizmet gösteriyor ise, yeniden başlatma görünür ve hello uzantıları değil yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-280">If an existing VM is service-healed, it appears as a reboot, and hello extensions are not rerun.</span></span> <span data-ttu-id="6ef2b-281">Bunu yeniden, bu gibi ise hello işletim sistemi sürücüsü hello kaynak görüntü değiştirme.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-281">If it is reimaged, it's like replacing hello OS drive with hello source image.</span></span> <span data-ttu-id="6ef2b-282">Uzantılar gibi hello son modelinden herhangi uzmanlık çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-282">Any specialization from hello latest model, such as extensions, are run.</span></span>
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a><span data-ttu-id="6ef2b-283">Nasıl bir sanal makine ölçek kümesi tooan Azure AD etki alanına katılacak mısınız?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-283">How do I join a virtual machine scale set tooan Azure AD domain?</span></span>

<span data-ttu-id="6ef2b-284">bir sanal makine ölçek kümesi tooan Azure Active Directory (Azure AD) etki toojoin, bir uzantı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-284">toojoin a virtual machine scale set tooan Azure Active Directory (Azure AD) domain, you can define an extension.</span></span> 

<span data-ttu-id="6ef2b-285">toodefine bir uzantı hello JsonADDomainExtension özelliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-285">toodefine an extension, use hello JsonADDomainExtension property:</span></span>

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a><span data-ttu-id="6ef2b-286">My sanal makine ölçek kümesi uzantısı yeniden başlatma gerektiren bir şey tooinstall çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-286">My virtual machine scale set extension is trying tooinstall something that requires a reboot.</span></span> <span data-ttu-id="6ef2b-287">Örneğin, "commandToExecute": "powershell.exe - ExecutionPolicy Unrestricted Install-WindowsFeature – AD FS-Resource-Manager – Includemanagementtools"</span><span class="sxs-lookup"><span data-stu-id="6ef2b-287">For example, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools"</span></span>

<span data-ttu-id="6ef2b-288">Sanal makine ölçek kümesi uzantınızı tooinstall bir yeniden başlatma gerektiren bir şey çalışırsa, hello Azure Otomasyonu istenen durum yapılandırması (Automation DSC) uzantısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-288">If your virtual machine scale set extension is trying tooinstall something that requires a reboot, you can use hello Azure Automation Desired State Configuration (Automation DSC) extension.</span></span> <span data-ttu-id="6ef2b-289">Merhaba işletim sistemi Windows Server 2012 R2 ise, Azure hello Windows Management Framework (WMF) 5.0 Kurulumu, yeniden başlatmalar çeker ve hello yapılandırma ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-289">If hello operating system is Windows Server 2012 R2, Azure pulls in hello Windows Management Framework (WMF) 5.0 setup, reboots, and then continues with hello configuration.</span></span> 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-290">My sanal makine ölçek kümesindeki nasıl üzerinde kötü amaçlı yazılımdan koruma dışı?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-290">How do I turn on antimalware in my virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-291">kötü amaçlı yazılımdan koruma, sanal makine ölçekte üzerinde tooturn ayarlamak, aşağıdaki PowerShell örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-291">tooturn on antimalware on your virtual machine scale set, use hello following PowerShell example:</span></span>

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a><span data-ttu-id="6ef2b-292">Özel depolama hesabında barındırılan özel bir komut dosyası tooexecute ihtiyacım.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-292">I need tooexecute a custom script that's hosted in a private storage account.</span></span> <span data-ttu-id="6ef2b-293">Merhaba komut dosyasını başarıyla hello depolama genel olduğunda, ancak toouse bir paylaşılan erişim imzası (SAS) çalıştığınızda çalıştırır, başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-293">hello script runs successfully when hello storage is public, but when I try toouse a Shared Access Signature (SAS), it fails.</span></span> <span data-ttu-id="6ef2b-294">Bu ileti görüntülenir: "için geçerli paylaşılan erişim imzası zorunlu parametreler eksik".</span><span class="sxs-lookup"><span data-stu-id="6ef2b-294">This message is displayed: “Missing mandatory parameters for valid Shared Access Signature”.</span></span> <span data-ttu-id="6ef2b-295">Bağlantı + SAS yerel Bilgisayarım tarayıcıdan düzgün çalışır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-295">Link+SAS works fine from my local browser.</span></span>

<span data-ttu-id="6ef2b-296">tooexecute özel depolama hesabı, barındırılan özel bir komut dosyası hello depolama hesabı anahtarı ve ad ile korumalı ayarlarını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-296">tooexecute a custom script that's hosted in a private storage account, set up protected settings with hello storage account key and name.</span></span> <span data-ttu-id="6ef2b-297">Daha fazla bilgi için bkz: [için özel betik uzantısı Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-297">For more information, see [Custom Script Extension for Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).</span></span>







## <a name="networking"></a><span data-ttu-id="6ef2b-298">Ağ</span><span class="sxs-lookup"><span data-stu-id="6ef2b-298">Networking</span></span>
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a><span data-ttu-id="6ef2b-299">Ağ güvenlik grubu (NSG) tooa ölçek kümesi, olası tooassign, böylelikle hello kümesindeki tooall hello VM NIC'ler uygulanır?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-299">Is it possible tooassign a Network Security Group (NSG) tooa scale set, so that it will apply tooall hello VM NICs in hello set?</span></span>

<span data-ttu-id="6ef2b-300">Evet.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-300">Yes.</span></span> <span data-ttu-id="6ef2b-301">Merhaba Networkınterfaceconfiguration hello ağ profilinin bölümünde başvurarak tooa ölçek kümesi doğrudan bir ağ güvenlik grubu uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-301">A Network Security Group can be applied directly tooa scale set by referencing it in hello networkInterfaceConfigurations section of hello network profile.</span></span> <span data-ttu-id="6ef2b-302">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-302">Example:</span></span>

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a><span data-ttu-id="6ef2b-303">Ne yapmalıyım bir VIP takası hello aynı sanal makine ölçek ayarlar için abonelik ve aynı bölgede?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-303">How do I do a VIP swap for virtual machine scale sets in hello same subscription and same region?</span></span>

<span data-ttu-id="6ef2b-304">Varsa iki sanal makine ölçek Azure yük dengeleyici ön uç ile ayarlar ve bulundukları aynı abonelikte ve bölgede Merhaba, her biri hello ortak IP adreslerini serbest bırakma ve toohello diğer Ata.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-304">If you have two virtual machine scale sets with Azure Load Balancer front-ends, and they are in hello same subscription and region, you could deallocate hello public IP addresses from each one, and assign toohello other.</span></span> <span data-ttu-id="6ef2b-305">Bkz: [VIP takası: Mavi yeşil dağıtım Azure Kaynak Yöneticisi'nde](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) örneğin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-305">See [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) for example.</span></span> <span data-ttu-id="6ef2b-306">Hello kaynakları hello ağ düzeyinde serbest ve ayrılan. ancak bu bir gecikme anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-306">This does imply a delay though as hello resources are deallocated/allocated at hello network level.</span></span> <span data-ttu-id="6ef2b-307">Toouse Azure uygulama ağ geçidi iki arka uç havuzları ve yönlendirme kuralı ile çok daha hızlı seçenektir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-307">A faster option is toouse Azure Application Gateway with two backend pools, and a routing rule.</span></span> <span data-ttu-id="6ef2b-308">Alternatif olarak, uygulamanız ile barındırabilir [Azure uygulama hizmeti](https://azure.microsoft.com/en-us/services/app-service/) hazırlama ve üretim yuvası arasında hızlı geçişi için destek sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-308">Alternatively, you could host your application with [Azure App service](https://azure.microsoft.com/en-us/services/app-service/) which provides support for fast switching between staging and production slots.</span></span>
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a><span data-ttu-id="6ef2b-309">Özel IP adresleri toouse özel statik IP adresi ayırma için bir aralığı nasıl belirtin?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-309">How do I specify a range of private IP addresses toouse for static private IP address allocation?</span></span>

<span data-ttu-id="6ef2b-310">IP adresleri, belirttiğiniz bir alt ağdan seçilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-310">IP addresses are selected from a subnet that you specify.</span></span> 

<span data-ttu-id="6ef2b-311">sanal makine ölçek kümesi IP adreslerinin Hello ayırma yöntemi her zaman "dinamik" olmakla birlikte, bu IP adreslerine değiştirebilirsiniz anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-311">hello allocation method of virtual machine scale set IP addresses is always “dynamic,” but that doesn't mean that these IP addresses can change.</span></span> <span data-ttu-id="6ef2b-312">Bu durumda, "dinamik" yalnızca bir PUT İsteği hello IP adresi belirtmeyin anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-312">In this case, "dynamic" only means that you do not specify hello IP address in a PUT request.</span></span> <span data-ttu-id="6ef2b-313">Merhaba statik Hello alt kullanarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-313">Specify hello static set by using hello subnet.</span></span> 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a><span data-ttu-id="6ef2b-314">Bir sanal makine ölçek kümesi tooan mevcut Azure sanal ağı nasıl dağıtırım?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-314">How do I deploy a virtual machine scale set tooan existing Azure virtual network?</span></span> 

<span data-ttu-id="6ef2b-315">toodeploy bir sanal makine ölçek kümesi tooan mevcut Azure sanal ağı, bkz: [bir sanal makine ölçek kümesi tooan varolan sanal ağı dağıtmak](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-315">toodeploy a virtual machine scale set tooan existing Azure virtual network, see [Deploy a virtual machine scale set tooan existing virtual network](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet).</span></span> 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a><span data-ttu-id="6ef2b-316">Başlangıç IP adresi nasıl ekleyebilirim Merhaba bir sanal makine ölçek ilk VM şablonu toohello çıkış ayarlamak?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-316">How do I add hello IP address of hello first VM in a virtual machine scale set toohello output of a template?</span></span>

<span data-ttu-id="6ef2b-317">bir sanal makine ölçek kümesi toohello çıktıda bir şablonu ilk VM hello tooadd hello IP adresini bakın [ARM: Get VMSS'ın özel IP](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-317">tooadd hello IP address of hello first VM in a virtual machine scale set toohello output of a template, see [ARM: Get VMSS's private IPs](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).</span></span>

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a><span data-ttu-id="6ef2b-318">Ölçek kümesi ağ hızlandırılmış kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-318">Can I use scale sets with Accelerated Networking?</span></span>

<span data-ttu-id="6ef2b-319">Evet.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-319">Yes.</span></span> <span data-ttu-id="6ef2b-320">Hızlandırılmış toouse ağ iletişimi, Ölçek enableAcceleratedNetworking tootrue kümenin Networkınterfaceconfiguration ayarları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-320">toouse accelerated networking, set enableAcceleratedNetworking tootrue in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="6ef2b-321">Örneğin</span><span class="sxs-lookup"><span data-stu-id="6ef2b-321">E.g.</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a><span data-ttu-id="6ef2b-322">Ölçek kümesi tarafından kullanılan hello DNS sunucularının nasıl yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-322">How can I configure hello DNS servers used by a scale set?</span></span>

<span data-ttu-id="6ef2b-323">toocreate özel bir DNS yapılandırması ile VM ölçek kümesi, bir dnsSettings JSON paket toohello ölçek kümesi Networkınterfaceconfiguration bölüm ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-323">toocreate a VM scale set with a custom DNS configuration, add a dnsSettings JSON packet toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="6ef2b-324">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-324">Example:</span></span>
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a><span data-ttu-id="6ef2b-325">Ölçek kümesi tooassign ortak bir IP adresi tooeach VM nasıl yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-325">How can I configure a scale set tooassign a public IP address tooeach VM?</span></span>

<span data-ttu-id="6ef2b-326">VM ölçek kümesi toocreate atar genel bir IP adresi tooeach VM hello Microsoft.Compute/virtualMAchineScaleSets kaynak hello API sürümü 2017-03-30 olduğundan emin olun ve Ekle bir _publicipaddressconfiguration_ JSON paket toohello ölçek Ipconfigurations bölümünde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-326">toocreate a VM scale set that assigns a public IP address tooeach VM, make sure hello API version of hello Microsoft.Compute/virtualMAchineScaleSets resource is 2017-03-30, and add a _publicipaddressconfiguration_ JSON packet toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="6ef2b-327">Örnek:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-327">Example:</span></span>

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a><span data-ttu-id="6ef2b-328">Birden çok uygulama ağ geçitleri ile ölçek kümesi toowork yapılandırabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-328">Can I configure a scale set toowork with multiple Application Gateways?</span></span>

<span data-ttu-id="6ef2b-329">Evet.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-329">Yes.</span></span> <span data-ttu-id="6ef2b-330">Merhaba kaynak kimliği için birden çok uygulama ağ geçidi arka uç adres havuzu toohello ekleyebilirsiniz _applicationGatewayBackendAddressPools_ hello listesinde _Ipconfigurations_ ölçek kümenizi bölümü Ağ profili.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-330">You can add hello resource id's for multiple Application Gateway backend address pools toohello _applicationGatewayBackendAddressPools_ list in hello _ipConfigurations_ section of your scale set network profile.</span></span>

## <a name="scale"></a><span data-ttu-id="6ef2b-331">Ölçek</span><span class="sxs-lookup"><span data-stu-id="6ef2b-331">Scale</span></span>

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a><span data-ttu-id="6ef2b-332">Hangi durumda ı ikiden VM'ler ile ayarlamak bir sanal makine ölçek oluşturacak?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-332">In what case would I create a virtual machine scale set with fewer than two VMs?</span></span>

<span data-ttu-id="6ef2b-333">Nedenlerinden biri toocreate toouse hello esnek özelliklerini bir sanal makine ölçek kümesi bir sanal makine ölçek ikiden VM'ler ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-333">One reason toocreate a virtual machine scale set with fewer than two VMs would be toouse hello elastic properties of a virtual machine scale set.</span></span> <span data-ttu-id="6ef2b-334">Örneğin, maliyetleri çalıştıran VM ödeme olmadan bir sanal makine ölçek kümesi sıfır VM'ler toodefine ile altyapınızın dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-334">For example, you could deploy a virtual machine scale set with zero VMs toodefine your infrastructure without paying VM running costs.</span></span> <span data-ttu-id="6ef2b-335">Hazır toodeploy VM'ler olduğunda, daha sonra hello "kapasitesini" Merhaba sanal makine ölçek kümesi toohello üretim örnek sayısı artırın.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-335">Then, when you are ready toodeploy VMs, increase hello “capacity” of hello virtual machine scale set toohello production instance count.</span></span>

<span data-ttu-id="6ef2b-336">Bir sanal makineyi ölçeği ikiden VM'ler ile Ayarla oluşturabilirsiniz başka bir, kullanılabilirlik ile ayrık VM'ler kümesi kullanarak kullanılabilirlik az endişe olup olmadığınızı nedenidir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-336">Another reason you might create a virtual machine scale set with fewer than two VMs is if you're concerned less with availability than in using an availability set with discrete VMs.</span></span> <span data-ttu-id="6ef2b-337">Sanal makine ölçek kümeleri, yolu toowork fungible protokole işlem birimleri ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-337">Virtual machine scale sets give you a way toowork with undifferentiated compute units that are fungible.</span></span> <span data-ttu-id="6ef2b-338">Sanal makine ölçek kümeleri kullanılabilirlik kümeleri karşı temel fark yatan unsur bu bütünlüğünü olur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-338">This uniformity is a key differentiator for virtual machine scale sets versus availability sets.</span></span> <span data-ttu-id="6ef2b-339">Çok sayıda durum bilgisiz iş yükleri tek tek birim izlemez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-339">Many stateless workloads do not track individual units.</span></span> <span data-ttu-id="6ef2b-340">Merhaba iş yükü düşerse tooone işlem birimi ölçeklendirmek ve hello iş yükü arttığında toomany ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-340">If hello workload drops, you can scale down tooone compute unit, and then scale up toomany when hello workload increases.</span></span>

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-341">Merhaba bir sanal makine ölçek kümesindeki VM'lerin sayısını nasıl değişiyor?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-341">How do I change hello number of VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-342">bir sanal makine ölçek kümesindeki sanal makineleri toochange hello numarasını görmek [değiştirmek, bir sanal makine ölçek kümesinin hello örnek sayısı](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-342">toochange hello number of VMs in a virtual machine scale set, see [Change hello instance count of a virtual machine scale set](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).</span></span>

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a><span data-ttu-id="6ef2b-343">Belirli eşikleri dolduğunda özel uyarılar nasıl tanımlamak?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-343">How do I define custom alerts for when certain thresholds are reached?</span></span>

<span data-ttu-id="6ef2b-344">Belirtilen eşikler için uyarıları nasıl işleneceğini bazı esneklik bulunur.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-344">You have some flexibility in how you handle alerts for specified thresholds.</span></span> <span data-ttu-id="6ef2b-345">Örneğin, özelleştirilmiş Web kancalarını tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-345">For example, you can define customized webhooks.</span></span> <span data-ttu-id="6ef2b-346">Aşağıdaki Web kancası örneğine hello Resource Manager şablonu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-346">hello following webhook example is from a Resource Manager template:</span></span>

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

<span data-ttu-id="6ef2b-347">Bu örnekte, bir Eşiğe ulaşıldığında uyarı tooPagerduty.com gider.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-347">In this example, an alert goes tooPagerduty.com when a threshold is reached.</span></span>



## <a name="patching-and-operations"></a><span data-ttu-id="6ef2b-348">Düzeltme eki ve işlemleri</span><span class="sxs-lookup"><span data-stu-id="6ef2b-348">Patching and operations</span></span>

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a><span data-ttu-id="6ef2b-349">Varolan bir kaynak grubundaki bir ölçek nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-349">How do I create a scale set in an existing resource group?</span></span>

<span data-ttu-id="6ef2b-350">Ölçek kümeleri oluşturma var olan bir kaynak grubu henüz hello Azure portal ' mümkün değil, ancak bir ölçek dağıtma bir Azure Resource Manager şablonu ayarladığınızda var olan bir kaynak grubunu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-350">Creating scale sets in an existing resource group is not yet possible from hello Azure portal, but you can specify an existing resource group when deploying a scale set from an Azure Resource Manager template.</span></span> <span data-ttu-id="6ef2b-351">Varolan bir kaynak grubu, Azure PowerShell veya CLI kullanarak bir ölçek oluştururken de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-351">You can also specify an existing resource group when creating a scale set using Azure PowerShell or CLI.</span></span>

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a><span data-ttu-id="6ef2b-352">Tooanother kaynak grubu bir ölçek kümesi taşıyabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-352">Can we move a scale set tooanother resource group?</span></span>

<span data-ttu-id="6ef2b-353">Evet, Ölçek kümesi kaynakları tooa yeni abonelik veya kaynak grubu taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-353">Yes, you can move scale set resources tooa new subscription or resource group.</span></span>

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a><span data-ttu-id="6ef2b-354">TooI güncelleştirme nasıl tooa yeni görüntüsü my sanal makine ölçek kümesi?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-354">How tooI update my virtual machine scale set tooa new image?</span></span> <span data-ttu-id="6ef2b-355">Düzeltme eki uygulama nasıl yönetebilirim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-355">How do I manage patching?</span></span>

<span data-ttu-id="6ef2b-356">sanal makine ölçek kümesi tooa yeni görüntü ve toomanage düzeltme eki uygulama, tooupdate bkz [bir sanal makine ölçek kümesini yükseltme](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-356">tooupdate your virtual machine scale set tooa new image, and toomanage patching, see [Upgrade a virtual machine scale set](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).</span></span>

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a><span data-ttu-id="6ef2b-357">Merhaba yeniden görüntü oluşturma işlemi tooreset VM hello görüntüyü değiştirmeden kullanabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-357">Can I use hello reimage operation tooreset a VM without changing hello image?</span></span> <span data-ttu-id="6ef2b-358">(Diğer bir deyişle, bir VM toofactory ayarları sıfırlama istiyorum tooa yeni görüntüsü yerine.)</span><span class="sxs-lookup"><span data-stu-id="6ef2b-358">(That is, I want reset a VM toofactory settings rather than tooa new image.)</span></span>

<span data-ttu-id="6ef2b-359">Evet, hello görüntüyü değiştirmeden hello yeniden görüntü oluşturma işlemi tooreset VM kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-359">Yes, you can use hello reimage operation tooreset a VM without changing hello image.</span></span> <span data-ttu-id="6ef2b-360">Sanal makine ölçek kümesi varsa ancak, platform görüntüsü ile başvuran `version = latest`, VM'yi tooa güncelleştirebilirsiniz sonraki işletim sistemi yansımasını çağırdığınızda `reimage`.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-360">However, if your virtual machine scale set references a platform image with `version = latest`, your VM can update tooa later OS image when you call `reimage`.</span></span>

<span data-ttu-id="6ef2b-361">Daha fazla bilgi için bkz: [bir sanal makine ölçek kümesindeki tüm sanal makineleri yönetme](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span><span class="sxs-lookup"><span data-stu-id="6ef2b-361">For more information, see [Manage all VMs in a virtual machine scale set](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="6ef2b-362">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="6ef2b-362">Troubleshooting</span></span>

### <a name="how-do-i-turn-on-boot-diagnostics"></a><span data-ttu-id="6ef2b-363">Önyükleme tanılaması nasıl kapatırım?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-363">How do I turn on boot diagnostics?</span></span>

<span data-ttu-id="6ef2b-364">önyükleme tanılaması üzerinde tooturn ilk olarak, bir depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-364">tooturn on boot diagnostics, first, create a storage account.</span></span> <span data-ttu-id="6ef2b-365">Ardından, bu JSON bloğu, sanal makine ölçek kümesindeki put **virtualMachineProfile**ve hello sanal makine ölçek kümesini güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-365">Then, put this JSON block in your virtual machine scale set **virtualMachineProfile**, and update hello virtual machine scale set:</span></span>

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

<span data-ttu-id="6ef2b-366">Yeni VM oluşturulduğunda, hello hello VM InstanceView özelliği hello ekran görüntüsü vb. için hello ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-366">When a new VM is created, hello InstanceView property of hello VM shows hello details for hello screenshot, and so on.</span></span> <span data-ttu-id="6ef2b-367">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-367">Here's an example:</span></span>
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a><span data-ttu-id="6ef2b-368">Sanal makine özellikleri</span><span class="sxs-lookup"><span data-stu-id="6ef2b-368">Virtual machine properties</span></span>

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-369">Her VM için özellik bilgilerini birden fazla çağrı yapmadan nasıl sağlarım?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-369">How do I get property information for each VM without making multiple calls?</span></span> <span data-ttu-id="6ef2b-370">Örneğin, hello hata etki alanı her hello için 100 VM'ler my sanal makine ölçek kümesindeki nereden?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-370">For example, how would I get hello fault domain for each of hello 100 VMs in my virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-371">birden çok aramaları yapmadan her VM tooget özellik bilgilerini, çağırabilir `ListVMInstanceViews` bir REST API yaparak `GET` kaynak URI'si aşağıdaki hello üzerinde:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-371">tooget property information for each VM without making multiple calls, you can call `ListVMInstanceViews` by doing a REST API `GET` on hello following resource URI:</span></span>

<span data-ttu-id="6ef2b-372">/Subscriptions/ < ABONELİK_KİMLİĞİ > /resourceGroups/ < resource_group_name > /providers/Microsoft.Compute/virtualMachineScaleSets/ < scaleset_name > / virtualMachines? $expand = instanceView & $select = instanceView</span><span class="sxs-lookup"><span data-stu-id="6ef2b-372">/subscriptions/<subscription_id>/resourceGroups/<resource_group_name>/providers/Microsoft.Compute/virtualMachineScaleSets/<scaleset_name>/virtualMachines?$expand=instanceView&$select=instanceView</span></span>

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a><span data-ttu-id="6ef2b-373">Bir sanal makine ölçek kümesindeki toodifferent VM'ler t farklı uzantı bağımsız değişkenler geçirebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-373">Can I pass different extension arguments toodifferent VMs in a virtual machine scale set?</span></span>

<span data-ttu-id="6ef2b-374">Hayır, farklı uzantı bağımsız bir sanal makine ölçek kümesindeki toodifferent sanal makineleri geçiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-374">No, you cannot pass different extension arguments toodifferent VMs in a virtual machine scale set.</span></span> <span data-ttu-id="6ef2b-375">Ancak, uzantıları hello benzersiz hello gibi hello makine adı olarak çalışan VM özelliklerini bağlı olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-375">However, extensions can act based on hello unique properties of hello VM they are running on, such as on hello machine name.</span></span> <span data-ttu-id="6ef2b-376">Uzantıları hello VM hakkında daha fazla bilgi http://169.254.169.254 tooget örneği meta sorgulama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-376">Extensions also can query instance metadata on http://169.254.169.254 tooget more information about hello VM.</span></span>

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a><span data-ttu-id="6ef2b-377">Neden my sanal makine ölçek kümesi VM makine adları ve VM kimlikleri arasında boşluklar var mı?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-377">Why are there gaps between my virtual machine scale set VM machine names and VM IDs?</span></span> <span data-ttu-id="6ef2b-378">Örneğin: 0, 1, 3...</span><span class="sxs-lookup"><span data-stu-id="6ef2b-378">For example: 0, 1, 3...</span></span>

<span data-ttu-id="6ef2b-379">Sanal makine ölçek kümesi için sanal makine ölçek kümesi VM makine adları ve VM kimlikleri arasında boşluklar olan **overprovision** özelliği toohello varsayılan değer olarak ayarlanmış **doğru**.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-379">There are gaps between your virtual machine scale set VM machine names and VM IDs because your virtual machine scale set **overprovision** property is set toohello default value of **true**.</span></span> <span data-ttu-id="6ef2b-380">İşleminin çok ayarlanırsa**doğru**, oluşturulan istenenden daha fazla VM'ler.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-380">If overprovisioning is set too**true**, more VMs than requested are created.</span></span> <span data-ttu-id="6ef2b-381">Ek VM'ler silinir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-381">Extra VMs are then deleted.</span></span> <span data-ttu-id="6ef2b-382">Bu durumda, artırılmış dağıtım güvenilirlik elde ancak hello gider ve bitişik adlandırma bitişik ağ adresi çevirisi (NAT) kuralları.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-382">In this case, you gain increased deployment reliability, but at hello expense of contiguous naming and contiguous Network Address Translation (NAT) rules.</span></span> 

<span data-ttu-id="6ef2b-383">Bu özellik çok ayarlayabilirsiniz**false**.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-383">You can set this property too**false**.</span></span> <span data-ttu-id="6ef2b-384">Küçük sanal makine ölçek kümeleri için bu dağıtım güvenilirlik önemli ölçüde etkilemez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-384">For small virtual machine scale sets, this doesn't significantly affect deployment reliability.</span></span>

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a><span data-ttu-id="6ef2b-385">Bir sanal makine ölçek kümesindeki VM silme ve hello VM serbest bırakma arasındaki hello fark nedir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-385">What is hello difference between deleting a VM in a virtual machine scale set and deallocating hello VM?</span></span> <span data-ttu-id="6ef2b-386">Merhaba diğer üzerinde ne zaman seçmeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="6ef2b-386">When should I choose one over hello other?</span></span>

<span data-ttu-id="6ef2b-387">Merhaba bir sanal makine ölçek kümesindeki VM silme ve hello VM serbest bırakma arasındaki temel fark olan `deallocate` hello sanal sabit diskleri (VHD) silmez.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-387">hello main difference between deleting a VM in a virtual machine scale set and deallocating hello VM is that `deallocate` doesn’t delete hello virtual hard disks (VHDs).</span></span> <span data-ttu-id="6ef2b-388">İle çalışmaya ilişkin depolama maliyetleri vardır `stop deallocate`.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-388">There are storage costs associated with running `stop deallocate`.</span></span> <span data-ttu-id="6ef2b-389">Kullanın ya da diğer nedenler aşağıdaki hello biri için hello:</span><span class="sxs-lookup"><span data-stu-id="6ef2b-389">You might use one or hello other for one of hello following reasons:</span></span>

- <span data-ttu-id="6ef2b-390">İşlem maliyetleri ödeme toostop istiyor, ancak tookeep hello disk hello VM'ler durumunu istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-390">You want toostop paying compute costs, but you want tookeep hello disk state of hello VMs.</span></span>
- <span data-ttu-id="6ef2b-391">Toostart VM'ler kümesi bir sanal makine ölçek kümesi ölçeklendirme daha hızlı istiyor.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-391">You want toostart a set of VMs more quickly than you could scale out a virtual machine scale set.</span></span>
  - <span data-ttu-id="6ef2b-392">İlgili toothis senaryosu, kendi otomatik ölçeklendirme altyapısı ve istediğiniz daha hızlı uçtan uca ölçek oluşturmuş olabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-392">Related toothis scenario, you might have created your own autoscale engine and want a faster end-to-end scale.</span></span>
- <span data-ttu-id="6ef2b-393">Düz olmayan şekilde hata etki alanları veya güncelleştirme etki alanları arasında dağıtılan bir sanal makine ölçek kümesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-393">You have a virtual machine scale set that is unevenly distributed across fault domains or update domains.</span></span> <span data-ttu-id="6ef2b-394">Bu, seçmeli olarak VM'ler silinmiş veya VM'ler işleminin sonra silindi nedeniyle, olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-394">This might be because you selectively deleted VMs, or because VMs were deleted after overprovisioning.</span></span> <span data-ttu-id="6ef2b-395">Çalışan `stop deallocate` arkasından `start` hello sanal makinede ölçeği eşit Ayarla hello VM'ler hata etki alanları veya güncelleştirme etki alanları arasında dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6ef2b-395">Running `stop deallocate` followed by `start` on hello virtual machine scale set evenly distributes hello VMs across fault domains or update domains.</span></span>

