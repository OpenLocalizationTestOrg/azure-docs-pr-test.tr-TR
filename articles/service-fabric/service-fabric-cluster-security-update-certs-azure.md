---
title: "Bir Azure Service Fabric kümesindeki sertifikaları yönetme | Microsoft Docs"
description: "Yeni sertifikalar, geçiş sertifikası eklemek ve sertifika için veya bir Service Fabric kümesinden kaldırmak açıklar."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="bdb1d-103">Ekleme veya Azure Service Fabric kümesi için sertifikaları kaldırın</span><span class="sxs-lookup"><span data-stu-id="bdb1d-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="bdb1d-104">Service Fabric'ın X.509 sertifikaları nasıl kullandığı tanımak ve hakkında bilgi sahibi olmanız önerilir [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="bdb1d-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="bdb1d-105">Anlamanız gerekir hangi küme sertifika ve devam etmeden önce ne için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="bdb1d-106">Service fabric, istemci sertifikalarını yanı sıra küme oluşturma sırasında sertifika güvenliği yapılandırdığınızda iki küme sertifikalar, birincil ve ikincil bir belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="bdb1d-107">Başvurmak [Portalı aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-portal.md) veya [Azure Resource Manager aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-arm.md) oluşturma süresi sırasında ayarlama ile ilgili ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="bdb1d-108">Yalnızca bir küme sertifika belirtirseniz, zaman oluşturmak, sonra birincil sertifikası olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="bdb1d-109">Küme oluşturulduktan sonra ikincil olarak yeni bir sertifika ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb1d-110">Güvenli bir küme için her zaman en az bir geçerli (değil iptal edilmiş ve süresi dolan değil) küme dağıtılan sertifika (birincil veya ikincil) (değilse, çalışan küme durur) gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="bdb1d-111">süre sonu, tüm geçerli sertifikaların düşmeden önce 90 gün sistem, bir uyarı izleme ve ayrıca bir uyarı sistem durumu olayı düğümde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="bdb1d-112">Şu anda hiçbir e-posta veya var. Bu konuyla ilgili service fabric gönderir herhangi bir bildirim</span><span class="sxs-lookup"><span data-stu-id="bdb1d-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="bdb1d-113">Portalı kullanarak bir ikincil küme sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="bdb1d-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="bdb1d-114">Azure portalı üzerinden ikincil küme sertifika eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="bdb1d-115">Azure powershell için kullanmak zorunda.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="bdb1d-116">İşlem, bu belgenin sonraki bölümlerinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="bdb1d-117">Portalı kullanarak küme sertifikaları değiştirme</span><span class="sxs-lookup"><span data-stu-id="bdb1d-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="bdb1d-118">Birincil ve ikincil değiştirmek istiyorsanız bir ikincil küme sertifika başarıyla dağıttıktan sonra güvenlik dikey penceresine gidin ve bağlam menüsünden birincil sertifika ile ikincil cert takas 'Birincil ile değiştirme' seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![Sertifika değiştirme][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="bdb1d-120">Portalı kullanarak bir küme sertifikayı Kaldır</span><span class="sxs-lookup"><span data-stu-id="bdb1d-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="bdb1d-121">Güvenli bir küme için (dağıtılan en az bir geçerli değil iptal edilmiş ve süresi dolan değil) sertifika (birincil veya ikincil) her zaman gerekir aksi durumda, küme çalışmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="bdb1d-122">İçin küme güvenlik, güvenlik dikey penceresine gitmek için kullanılan ikincil bir sertifikayı kaldırın ve ikincil sertifika bağlam menüsünden 'Delete' seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="bdb1d-123">Maksadınızı birincil olarak işaretlenmiş sertifikayı kaldırmak için ise, ikincil kopya ilk değiştirme ve yükseltme tamamlandıktan sonra ikincil silmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="bdb1d-124">Resource Manager Powershell kullanarak bir ikincil sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="bdb1d-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="bdb1d-125">Bu adımları, Kaynak Yöneticisi'ni nasıl çalıştığını iyi ve en az bir Resource Manager şablonu kullanarak bir Service Fabric kümesi dağıttıysanız ve kullanışlı kümesi için kullanılan şablonu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="bdb1d-126">JSON kullanarak rahat olduğu da varsayılır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb1d-127">Örnek bir şablon ve boyunca veya bir başlangıç noktası olarak izlemek için kullanabileceğiniz parametreler arıyorsanız sonra buradan indirin [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="bdb1d-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="bdb1d-128">Kaynak Yöneticisi şablonunuzu düzenleyin</span><span class="sxs-lookup"><span data-stu-id="bdb1d-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="bdb1d-129">Aşağıdaki boyunca kolaylığı için örnek 5-VM-1-NodeTypes-Secure_Step2.JSON biz yapmadan tüm düzenlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="bdb1d-130">Örnek şu adresten edinilebilir [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="bdb1d-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="bdb1d-131">**Tüm adımları izlediğinizden emin olun**</span><span class="sxs-lookup"><span data-stu-id="bdb1d-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="bdb1d-132">**1. adım:** küme dağıtmak için kullanılan Resource Manager şablonu açın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="bdb1d-133">(Yukarıdaki depoyu örnek indirdiyseniz, güvenli bir küme dağıtmak için 5-VM-1-NodeTypes-Secure_Step1.JSON kullanın ve bu şablonu açın).</span><span class="sxs-lookup"><span data-stu-id="bdb1d-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="bdb1d-134">**2. adım:** Ekle **iki yeni parametreler** "secCertificateThumbprint" ve "secCertificateUrlValue", şablonunuzun parametre bölümüne "dize" yazın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="bdb1d-135">Aşağıdaki kod parçacığını kopyalayın ve şablonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="bdb1d-136">Şablonunuzu kaynak bağlı olarak bu, tanımlanan şekilde sonraki adımına geçmek zaten olabilir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="bdb1d-137">**3. adım:** değişiklik yapma **Microsoft.ServiceFabric/clusters** kaynak - şablonunuzda "Microsoft.ServiceFabric/clusters" kaynak tanımı'nı bulun.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="bdb1d-138">Bu tanım özellikleri altında "Sertifika" JSON bulacaksınız aşağıdaki JSON parçacığı gibi görünmelidir etiketi:</span><span class="sxs-lookup"><span data-stu-id="bdb1d-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="bdb1d-139">Yeni bir etiket "thumbprintSecondary" ekleyin ve "[parameters('secCertificateThumbprint')]" bir değer verin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="bdb1d-140">Kaynak tanımı aşağıdaki gibi görünmelidir artık bunu (kaynağınız şablona bağlı olarak, aşağıdaki parçacığı gibi tam olarak olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="bdb1d-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="bdb1d-141">İsterseniz **rollover cert**, ardından yeni sertifika birincil olarak belirtin ve geçerli birincil ikincil olarak taşıma.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="bdb1d-142">Bu, geçerli birincil sertifikanızı rollover içinde bir dağıtım adımı yeni sertifikayı sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="bdb1d-143">**4. adım:** değişiklik yapma **tüm** **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="bdb1d-144">"Publisher" gidin: "Microsoft.Azure.ServiceFabric" altında "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="bdb1d-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="bdb1d-145">Service fabric yayımcı ayarlarında şöyle bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="bdb1d-147">Yeni sertifika girişler ekleyin</span><span class="sxs-lookup"><span data-stu-id="bdb1d-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="bdb1d-148">Özellikleri artık aşağıdaki gibi görünmelidir</span><span class="sxs-lookup"><span data-stu-id="bdb1d-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="bdb1d-150">İsterseniz **rollover cert**, ardından yeni sertifika birincil olarak belirtin ve geçerli birincil ikincil olarak taşıma.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="bdb1d-151">Bu, geçerli sertifikanızı rollover içinde bir dağıtım adımı yeni sertifikayı sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="bdb1d-152">Özellikleri artık aşağıdaki gibi görünmelidir</span><span class="sxs-lookup"><span data-stu-id="bdb1d-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="bdb1d-154">**5. adım:** değişiklik yapma **tüm** **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="bdb1d-155">"VaultCertificates" gidin:, "OSProfile" altında.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="bdb1d-156">Bu gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="bdb1d-158">SecCertificateUrlValue ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="bdb1d-159">Aşağıdaki kod parçacığında kullanın:</span><span class="sxs-lookup"><span data-stu-id="bdb1d-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="bdb1d-160">Sonuçta elde edilen Json aşağıdakine benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="bdb1d-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="bdb1d-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="bdb1d-162">4 ve 5 tüm Nodetypes/Microsoft.Compute/virtualMachineScaleSets kaynak tanımlarında şablonunuzda yinelenen olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="bdb1d-163">Bunlardan birini kaçırılması durumunda, sertifika üzerinde VMSS ve öngörülemeyen sonuçlara (, küme güvenlik için kullanabileceğiniz geçerli sertifika şunun; giderek küme de dahil olmak üzere kümenizdeki sahip yüklenmemiş</span><span class="sxs-lookup"><span data-stu-id="bdb1d-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="bdb1d-164">Bu nedenle çift, devam etmeden önce lütfen denetleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="bdb1d-165">Şablon dosyanızın yukarıya eklenen yeni parametreleri yansıtacak şekilde düzenleyin</span><span class="sxs-lookup"><span data-stu-id="bdb1d-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="bdb1d-166">Örnekten kullanıyorsanız [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) izlemek için örnek 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON içinde değişiklik başlatmak için</span><span class="sxs-lookup"><span data-stu-id="bdb1d-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="bdb1d-167">Resource Manager şablonu parametreniz dosya düzenleme, secCertificateThumbprint ve secCertificateUrlValue için iki yeni parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="bdb1d-168">Şablon Azure'a dağıtma</span><span class="sxs-lookup"><span data-stu-id="bdb1d-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="bdb1d-169">Şimdi şablonunuzu Azure'da dağıtmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="bdb1d-170">Bir Azure PS sürüm 1 + komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="bdb1d-171">Azure hesabınızda oturum açın ve belirli azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="bdb1d-172">Bu, birden fazla azure aboneliği erişen çok kişi için önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="bdb1d-173">Şablonu dağıtmadan önce test edin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="bdb1d-174">Kümeniz için dağıtılan aynı kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="bdb1d-175">Şablon, kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="bdb1d-176">Kümeniz için dağıtılan aynı kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="bdb1d-177">New-AzureRmResourceGroupDeployment komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="bdb1d-178">Varsayılan değer olduğundan modunu belirtmek gerekmez **artımlı**.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb1d-179">Mod tamamlandı olarak ayarlarsanız, şablonunuzda olmayan kaynakları yanlışlıkla silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="bdb1d-180">Bu nedenle bu senaryoda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="bdb1d-181">Aynı powershell doldurulmuş bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="bdb1d-182">Dağıtım tamamlandıktan sonra yeni sertifikayı kullanarak, kümeye bağlanın ve bazı sorgular gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="bdb1d-183">Yapabileceklerinizi varsa.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-183">If you are able to do.</span></span> <span data-ttu-id="bdb1d-184">Sonra eski sertifika silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="bdb1d-185">Kendinden imzalı bir sertifika kullanıyorsanız, yerel TrustedPeople sertifika deponuza almayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="bdb1d-186">Hızlı başvuru için güvenli bir kümeye bağlanmak için komutu İşte</span><span class="sxs-lookup"><span data-stu-id="bdb1d-186">For quick reference here is the command to connect to a secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="bdb1d-187">Hızlı başvuru için küme durumu almak için komutu aşağıda verilmiştir</span><span class="sxs-lookup"><span data-stu-id="bdb1d-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="bdb1d-188">Uygulama sertifikalarını kümeye dağıtma.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="bdb1d-189">Keyvault düğümlere dağıtılan sertifikaları sağlamak için yukarıdaki adımları 5'te özetlendiği gibi aynı adımları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="bdb1d-190">yalnızca tanımlanır ve farklı parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="bdb1d-191">Ekleme veya istemci sertifikaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="bdb1d-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="bdb1d-192">Küme sertifikalara ek olarak, service fabric kümesi yönetim işlemlerini gerçekleştirmek için istemci sertifikaları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="bdb1d-193">İstemci sertifikalarını - yönetici iki tür ekleyebilirsiniz veya salt okunur.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="bdb1d-194">Bunlar daha sonra küme üzerinde sorgu işlemleri ve yönetim işlemleri erişimi denetlemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="bdb1d-195">Varsayılan olarak, küme sertifikaları ve izin verilen yönetici sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="bdb1d-196">istemci sertifikalarını herhangi bir sayıda belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="bdb1d-197">Service fabric kümesi için yapılandırma güncelleştirmesi içinde her eklendiği/silindiği sonuçları</span><span class="sxs-lookup"><span data-stu-id="bdb1d-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="bdb1d-198">İstemci sertifikalarını - yönetici ekleme veya salt okunur Portalı aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="bdb1d-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="bdb1d-199">Güvenlik dikey penceresine gidin ve '+ kimlik doğrulama' düğmesini güvenlik dikey pencerenin en üstünde.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="bdb1d-200">' Kimlik doğrulama türü' - 'Salt okunur istemci' veya 'Yönetici istemci' 'Kimlik doğrulama Ekle' dikey penceresinde seçin</span><span class="sxs-lookup"><span data-stu-id="bdb1d-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="bdb1d-201">Şimdi yetkilendirme yöntemi seçin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-201">Now choose the Authorization method.</span></span> <span data-ttu-id="bdb1d-202">Bu, Service Fabric, bu sertifikayı konu adı veya parmak izini kullanarak araması gerektiğini olup olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="bdb1d-203">Genel olarak, bu konu adının yetkilendirme yöntemi kullanmak için en iyi güvenlik yöntemi değildir.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![İstemci sertifikası ekleme][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="bdb1d-205">İstemci sertifikalarının - yönetici veya salt okunur Portalı'nı kullanarak silme</span><span class="sxs-lookup"><span data-stu-id="bdb1d-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="bdb1d-206">İçin küme güvenlik, güvenlik dikey penceresine gitmek için kullanılan ikincil bir sertifikayı kaldırın ve belirli bir sertifika bağlam menüsünden 'Delete' seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="bdb1d-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="bdb1d-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bdb1d-207">Next steps</span></span>
<span data-ttu-id="bdb1d-208">Küme yönetimi hakkında daha fazla bilgi için bu makaleler okuyun:</span><span class="sxs-lookup"><span data-stu-id="bdb1d-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="bdb1d-209">Service Fabric kümesi yükseltme işlemi ve sizden beklentileri</span><span class="sxs-lookup"><span data-stu-id="bdb1d-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="bdb1d-210">İstemciler için rol tabanlı erişim Kurulumu</span><span class="sxs-lookup"><span data-stu-id="bdb1d-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


