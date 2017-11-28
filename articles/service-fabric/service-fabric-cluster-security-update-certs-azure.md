---
title: "Azure Service Fabric kümesi aaaManage sertifikaları | Microsoft Docs"
description: "Service Fabric kümesinden tooor tooadd yeni sertifikalar, geçiş sertifikası ve Kaldır nasıl sertifika açıklar."
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
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="11ff0-103">Ekleme veya Azure Service Fabric kümesi için sertifikaları kaldırın</span><span class="sxs-lookup"><span data-stu-id="11ff0-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="11ff0-104">Service Fabric'ın X.509 sertifikaları nasıl kullandığı tanımak ve hello ile ilgili bilgi sahibi olmanız önerilir [küme güvenlik senaryoları](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="11ff0-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="11ff0-105">Anlamanız gerekir hangi küme sertifika ve devam etmeden önce ne için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="11ff0-106">Yapılandırdığınızda sertifikalar, birincil ve ikincil bir iki küme belirtmenizi Service fabric sağlar, ayrıca tooclient sertifikalarda küme oluşturma sırasında güvenlik sertifika.</span><span class="sxs-lookup"><span data-stu-id="11ff0-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="11ff0-107">Çok başvuran[Portalı aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-portal.md) veya [Azure Resource Manager aracılığıyla azure bir küme oluşturma](service-fabric-cluster-creation-via-arm.md) oluşturma süresi sırasında ayarlama ile ilgili ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="11ff0-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="11ff0-108">Yalnızca bir küme sertifika belirtirseniz, zaman oluşturabilir, ardından, hello birincil sertifikası olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="11ff0-109">Küme oluşturulduktan sonra ikincil olarak yeni bir sertifika ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="11ff0-110">Güvenli bir küme için her zaman en az bir geçerli (değil iptal edilmiş ve süresi dolan değil) küme sertifika'ni (birincil veya ikincil) dağıtılan gerekir (değilse, hello küme çalışmamaya başlar).</span><span class="sxs-lookup"><span data-stu-id="11ff0-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="11ff0-111">süre sonu, tüm geçerli sertifikaların düşmeden önce 90 gün hello sistem, bir uyarı izleme ve ayrıca bir uyarı sistem durumu olayı hello düğümde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="11ff0-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="11ff0-112">Şu anda hiçbir e-posta veya var. Bu konuyla ilgili service fabric gönderir herhangi bir bildirim</span><span class="sxs-lookup"><span data-stu-id="11ff0-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="11ff0-113">Merhaba portalı kullanarak bir ikincil küme sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="11ff0-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="11ff0-114">İkincil küme sertifika hello Azure portal eklenemez.</span><span class="sxs-lookup"><span data-stu-id="11ff0-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="11ff0-115">Sahip olduğunuz toouse Azure powershell söz konusu.</span><span class="sxs-lookup"><span data-stu-id="11ff0-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="11ff0-116">Merhaba işlemi, bu belgenin sonraki bölümlerinde gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="11ff0-117">Merhaba küme sertifikaları Hello portal kullanarak değiştirme</span><span class="sxs-lookup"><span data-stu-id="11ff0-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="11ff0-118">Birincil ve ikincil tooswap hello istiyorsanız bir ikincil küme sertifika başarıyla dağıttıktan sonra toohello güvenlik dikey gidin ve hello bağlam menüsü tooswap hello ikincil sertifikayla hello 'Birincil ile değiştirme' seçeneği seçin Merhaba birincil sertifika.</span><span class="sxs-lookup"><span data-stu-id="11ff0-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Sertifika değiştirme][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="11ff0-120">Merhaba portalı kullanarak bir küme sertifikayı Kaldır</span><span class="sxs-lookup"><span data-stu-id="11ff0-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="11ff0-121">Güvenli bir küme için (dağıtılan en az bir geçerli değil iptal edilmiş ve süresi dolan değil) sertifika (birincil veya ikincil) her zaman gerekir aksi durumda, hello küme çalışmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="11ff0-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="11ff0-122">tooremove küme güvenlik, Bul toohello güvenlik dikey ve select hello 'Delete' seçeneği hello bağlam menüsünden hello ikincil sertifika kullanılmasını ikincil bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="11ff0-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="11ff0-123">Maksadınızı tooswap gerekir, birincil olarak işaretlenmiş tooremove hello sertifika ise ile ilk ikincil hello ve hello ikincil hello yükseltme tamamlandıktan sonra silin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="11ff0-124">Resource Manager Powershell kullanarak bir ikincil sertifika Ekle</span><span class="sxs-lookup"><span data-stu-id="11ff0-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="11ff0-125">Bu adımları, Kaynak Yöneticisi'ni nasıl çalıştığını iyi ve en az bir Resource Manager şablonu kullanarak bir Service Fabric kümesi dağıttıysanız ve hello kümesi kullanışlı tooset kullanılan hello şablonuna sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="11ff0-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="11ff0-126">JSON kullanarak rahat olduğu da varsayılır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="11ff0-127">Örnek bir şablon ve toofollow boyunca veya bir başlangıç noktası olarak kullanabileceğiniz parametreler arıyorsanız sonra buradan indirin [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="11ff0-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="11ff0-128">Kaynak Yöneticisi şablonunuzu düzenleyin</span><span class="sxs-lookup"><span data-stu-id="11ff0-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="11ff0-129">Aşağıdaki boyunca kolaylığı için örnek 5-VM-1-NodeTypes-Secure_Step2.JSON biz yapmadan tüm hello düzenlemeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="11ff0-130">Merhaba örnek şu adreste [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="11ff0-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="11ff0-131">**Tüm hello adımları toofollow emin olun**</span><span class="sxs-lookup"><span data-stu-id="11ff0-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="11ff0-132">**1. adım:** , küme toodeploy kullanılan hello Resource Manager şablonu açın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="11ff0-133">(Merhaba örnek deposuna yukarıda hello yüklediyseniz 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy güvenli bir küme kullanın ve bu şablonu açın).</span><span class="sxs-lookup"><span data-stu-id="11ff0-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="11ff0-134">**2. adım:** Ekle **iki yeni parametreler** "secCertificateThumbprint" ve "secCertificateUrlValue" türü "dize" toohello parametresi bölümü.</span><span class="sxs-lookup"><span data-stu-id="11ff0-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="11ff0-135">Aşağıdaki kod parçacığını hello kopyalayın ve toohello şablonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="11ff0-136">Bağlı olarak Hello kaynak şablonunuzun zaten bu tanımlanan sahip, bu durumda toohello sonraki adım taşıma.</span><span class="sxs-lookup"><span data-stu-id="11ff0-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
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
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="11ff0-137">**3. adım:** toohello değişiklik yapma **Microsoft.ServiceFabric/clusters** kaynak - şablonunuzda hello "Microsoft.ServiceFabric/clusters" kaynak tanımı bulun.</span><span class="sxs-lookup"><span data-stu-id="11ff0-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="11ff0-138">Bu tanım özellikleri altında "Sertifika" JSON bulacaksınız hello JSON parçacığı aşağıdaki gibi görünmelidir etiketi:</span><span class="sxs-lookup"><span data-stu-id="11ff0-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="11ff0-139">Yeni bir etiket "thumbprintSecondary" ekleyin ve "[parameters('secCertificateThumbprint')]" bir değer verin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="11ff0-140">Merhaba kaynak tanımı hello aşağıdaki gibi görünmelidir artık bunu (kaynağınız hello şablonu bağlı olarak, tam olarak hello gibi aşağıdaki parçacığı olmayabilir).</span><span class="sxs-lookup"><span data-stu-id="11ff0-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="11ff0-141">Çok istiyorsanız**rollover hello cert**, ikincil olarak birincil ve taşıma hello geçerli birincil olarak hello yeni sertifika belirtin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="11ff0-142">Bu, geçerli birincil sertifika toohello yeni sertifikanızı tek bir dağıtım adımda hello geçişi sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="11ff0-143">**4. adım:** değişiklik yapma çok**tüm** hello **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - hello Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı.</span><span class="sxs-lookup"><span data-stu-id="11ff0-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="11ff0-144">Kaydırma toohello "publisher": "Microsoft.Azure.ServiceFabric" altında "virtualMachineProfile".</span><span class="sxs-lookup"><span data-stu-id="11ff0-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="11ff0-145">Merhaba service fabric yayımcı ayarlarında, şöyle bir şey görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="11ff0-147">Merhaba yeni sertifika girişleri tooit Ekle</span><span class="sxs-lookup"><span data-stu-id="11ff0-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="11ff0-148">Merhaba özellikleri artık aşağıdaki gibi görünmelidir</span><span class="sxs-lookup"><span data-stu-id="11ff0-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="11ff0-150">Çok istiyorsanız**rollover hello cert**, ikincil olarak birincil ve taşıma hello geçerli birincil olarak hello yeni sertifika belirtin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="11ff0-151">Bu, geçerli sertifika toohello yeni sertifikanızı tek bir dağıtım adımda hello geçişi sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


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
<span data-ttu-id="11ff0-152">Merhaba özellikleri artık aşağıdaki gibi görünmelidir</span><span class="sxs-lookup"><span data-stu-id="11ff0-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="11ff0-154">**5. adım:** çok değişiklik**tüm** hello **Microsoft.Compute/virtualMachineScaleSets** kaynak tanımları - hello Microsoft.Compute/virtualMachineScaleSets kaynak bulun tanımı.</span><span class="sxs-lookup"><span data-stu-id="11ff0-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="11ff0-155">Toohello "vaultCertificates" kaydırma:, "OSProfile" altında.</span><span class="sxs-lookup"><span data-stu-id="11ff0-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="11ff0-156">Bu gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="11ff0-158">Merhaba secCertificateUrlValue tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="11ff0-159">Aşağıdaki kod parçacığında hello kullan:</span><span class="sxs-lookup"><span data-stu-id="11ff0-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="11ff0-160">Json kaynaklanan hello aşağıdakine benzer görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="11ff0-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="11ff0-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="11ff0-162">4 ve 5 tüm hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets kaynak tanımlarında şablonunuzda yinelenen olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="11ff0-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="11ff0-163">Bunlardan birini kaçırılması durumunda hello sertifika üzerinde bu VMSS yüklenmemiş ve (, bu hello küme güvenlik için kullanabilirsiniz. geçerli sertifika şunun; giderek hello küme de dahil olmak üzere kümenizdeki öngörülemeyen sonuçlara gerekir</span><span class="sxs-lookup"><span data-stu-id="11ff0-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="11ff0-164">Bu nedenle çift, devam etmeden önce lütfen denetleyin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="11ff0-165">Yukarıda eklediğiniz şablon dosyası tooreflect hello yeni parametrelerinizi Düzenle</span><span class="sxs-lookup"><span data-stu-id="11ff0-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="11ff0-166">Merhaba hello örnekten kullanıyorsanız [git deposuna](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow bunların, hello örnek 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON içinde toomake değişiklikleri başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="11ff0-167">Resource Manager şablonu parametreniz dosya düzenleme, hello iki yeni parametrelerini secCertificateThumbprint ve secCertificateUrlValue ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="11ff0-168">Merhaba şablonu tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="11ff0-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="11ff0-169">Artık hazır toodeploy şablonu tooAzure şunlardır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="11ff0-170">Bir Azure PS sürüm 1 + komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="11ff0-171">Tooyour Azure hesabı oturum ve hello belirli azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="11ff0-172">Bu, bir azure aboneliği daha erişim toomore sahip çok kişi için önemli bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="11ff0-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="11ff0-173">Test hello şablon önceki toodeploying onu.</span><span class="sxs-lookup"><span data-stu-id="11ff0-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="11ff0-174">Kullanım hello kümenizi halen dağıtılmış durumda aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="11ff0-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="11ff0-175">Merhaba şablonu tooyour kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="11ff0-176">Kullanım hello kümenizi halen dağıtılmış durumda aynı kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="11ff0-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="11ff0-177">Merhaba New-AzureRmResourceGroupDeployment komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="11ff0-178">Merhaba varsayılan değer olduğundan toospecify hello modu gerekmez **artımlı**.</span><span class="sxs-lookup"><span data-stu-id="11ff0-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="11ff0-179">Mod tooComplete ayarlarsanız, şablonunuzda olmayan kaynakları yanlışlıkla silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="11ff0-180">Bu nedenle bu senaryoda kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="11ff0-181">Örneği burada verilmiştir bir doldurulmuş hello aynı powershell.</span><span class="sxs-lookup"><span data-stu-id="11ff0-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="11ff0-182">Merhaba dağıtım tamamlandıktan sonra küme tooyour kullanarak bağlanan yeni bir sertifika hello ve bazı sorgular gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="11ff0-183">Mümkün toodo varsa.</span><span class="sxs-lookup"><span data-stu-id="11ff0-183">If you are able toodo.</span></span> <span data-ttu-id="11ff0-184">Ardından hello eski sertifika silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="11ff0-185">Kendinden imzalı bir sertifika kullanıyorsanız, tooimport unutmayın, yerel TrustedPeople sertifika deposuna bunları.</span><span class="sxs-lookup"><span data-stu-id="11ff0-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="11ff0-186">Hızlı başvuru için hello komutu tooconnect tooa güvenli küme İşte</span><span class="sxs-lookup"><span data-stu-id="11ff0-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

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
<span data-ttu-id="11ff0-187">Hızlı başvuru için işte hello komutu tooget küme durumu</span><span class="sxs-lookup"><span data-stu-id="11ff0-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="11ff0-188">Uygulama sertifikaları toohello kümesini dağıtma.</span><span class="sxs-lookup"><span data-stu-id="11ff0-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="11ff0-189">Adım 5'te bir keyvault toohello düğümleri dağıtılan toohave hello sertifikalarının yukarıda özetlendiği gibi aynı adımları hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="11ff0-190">yalnızca tanımlanır ve farklı parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="11ff0-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="11ff0-191">Ekleme veya istemci sertifikaları kaldırma</span><span class="sxs-lookup"><span data-stu-id="11ff0-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="11ff0-192">Toplama toohello küme sertifikalarda istemci sertifikaları tooperform yönetim işlemlerini service fabric kümesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="11ff0-193">İstemci sertifikalarını - yönetici iki tür ekleyebilirsiniz veya salt okunur.</span><span class="sxs-lookup"><span data-stu-id="11ff0-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="11ff0-194">Bunlar ardından kullanılan toocontrol erişim toohello yönetici işlemleri ve sorgu işlemleri hello kümede olabilir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="11ff0-195">Varsayılan olarak, hello küme sertifikaları toohello izin verilen yönetici sertifikalar listesine eklenir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="11ff0-196">istemci sertifikalarını herhangi bir sayıda belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11ff0-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="11ff0-197">Bir yapılandırma güncelleştirme toohello service fabric kümesi her eklendiği/silindiği sonuçları</span><span class="sxs-lookup"><span data-stu-id="11ff0-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="11ff0-198">İstemci sertifikalarını - yönetici ekleme veya salt okunur Portalı aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="11ff0-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="11ff0-199">Toohello güvenlik dikey gidin ve seçin hello '+ kimlik doğrulama' hello güvenlik dikey üstünde düğmesi.</span><span class="sxs-lookup"><span data-stu-id="11ff0-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="11ff0-200">Merhaba 'Kimlik doğrulama türü' - 'Salt okunur istemci' veya 'Yönetici istemci' Hello 'Kimlik doğrulama Ekle' dikey penceresinde, seçin</span><span class="sxs-lookup"><span data-stu-id="11ff0-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="11ff0-201">Şimdi hello yetkilendirme yöntemi seçin.</span><span class="sxs-lookup"><span data-stu-id="11ff0-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="11ff0-202">Bu, bu sertifikayı hello konu adı veya hello parmak izini kullanarak görünmelidir olup olmadığını tooService doku gösterir.</span><span class="sxs-lookup"><span data-stu-id="11ff0-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="11ff0-203">Genel olarak, bu konu adı iyi güvenlik uygulaması toouse hello yetkilendirme yöntemi değil.</span><span class="sxs-lookup"><span data-stu-id="11ff0-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![İstemci sertifikası ekleme][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="11ff0-205">İstemci sertifikalarını - yönetici veya salt okunur kullanarak silinmesini hello portalı</span><span class="sxs-lookup"><span data-stu-id="11ff0-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="11ff0-206">tooremove küme güvenlik, Bul toohello güvenlik dikey ve select hello 'Delete' seçeneği hello bağlam menüsünden hello belirli sertifika kullanılmasını ikincil bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="11ff0-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="11ff0-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11ff0-207">Next steps</span></span>
<span data-ttu-id="11ff0-208">Küme yönetimi hakkında daha fazla bilgi için bu makaleler okuyun:</span><span class="sxs-lookup"><span data-stu-id="11ff0-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="11ff0-209">Service Fabric kümesi yükseltme işlemi ve sizden beklentileri</span><span class="sxs-lookup"><span data-stu-id="11ff0-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="11ff0-210">İstemciler için rol tabanlı erişim Kurulumu</span><span class="sxs-lookup"><span data-stu-id="11ff0-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


