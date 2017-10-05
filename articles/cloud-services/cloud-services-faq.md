---
title: Azure bulut Hizmetleri rolleri ile ilgili SSS | Microsoft Docs
description: "Azure Cloud Services hakkında sık sorulan sorular. Sertifikalar, web rolleri ve çalışan rolleri hakkında bazı sık sorulan soruları yanıtlar."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: d887f3b31693c414254dc01dac4dbdd6d9224b6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="54ef4-104">Cloud Services SSS</span><span class="sxs-lookup"><span data-stu-id="54ef4-104">Cloud Services FAQ</span></span>
<span data-ttu-id="54ef4-105">Bu makalede, Microsoft Azure bulut hizmetleri hakkında sık sorulan bazı sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="54ef4-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="54ef4-106">Ayrıca, ziyaret edebilirsiniz [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma ve destek bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="54ef4-106">You can also visit the [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="54ef4-107">Ayrıca başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.</span><span class="sxs-lookup"><span data-stu-id="54ef4-107">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="54ef4-108">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="54ef4-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="54ef4-109">My sertifika burada yüklemeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="54ef4-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="54ef4-110">**Uygulamam**</span><span class="sxs-lookup"><span data-stu-id="54ef4-110">**My**</span></span>  
  <span data-ttu-id="54ef4-111">Uygulama sertifikayı özel anahtarla (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="54ef4-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="54ef4-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="54ef4-112">**CA**</span></span>  
  <span data-ttu-id="54ef4-113">Tüm ara sertifikalarınız bu deposunda (ilke ve alt CA'lar) gidin.</span><span class="sxs-lookup"><span data-stu-id="54ef4-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="54ef4-114">**KÖK**</span><span class="sxs-lookup"><span data-stu-id="54ef4-114">**ROOT**</span></span>  
  <span data-ttu-id="54ef4-115">Ana kök CA sertifikası burada gitmesi gereken şekilde kök CA depolar.</span><span class="sxs-lookup"><span data-stu-id="54ef4-115">The root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="54ef4-116">Süresi dolan sertifika kaldırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="54ef4-116">I can't remove expired certificate</span></span>
<span data-ttu-id="54ef4-117">Azure kullanımda olduğu sırada bir sertifika kaldırmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="54ef4-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="54ef4-118">Sertifikayı kullanan dağıtımını silerseniz veya dağıtım farklı veya yenilenmiş bir sertifika ile güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="54ef4-118">You need to either delete the deployment that uses the certificate, or update the deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="54ef4-119">Süresi dolmuş bir sertifika Sil</span><span class="sxs-lookup"><span data-stu-id="54ef4-119">Delete an expired certificate</span></span>
<span data-ttu-id="54ef4-120">Sertifika kullanılmadığı sürece, kullanabileceğiniz [Kaldır AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet'ini bir sertifikayı kaldırın.</span><span class="sxs-lookup"><span data-stu-id="54ef4-120">As long as the certificate is not in use, you can use the [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet to remove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="54ef4-121">Windows Azure hizmet yönetimi için Uzantılar adlı sertifikalar süresi dolmuş</span><span class="sxs-lookup"><span data-stu-id="54ef4-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="54ef4-122">Bu sertifikalar, Uzak Masaüstü uzantısı gibi bulut hizmeti uzantı eklendiğinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="54ef4-122">These certificates are created whenever an extension is added to the cloud service such as the Remote Desktop extension.</span></span> <span data-ttu-id="54ef4-123">Bu sertifikalar yalnızca şifreleme ve uzantı özel yapılandırması şifresini çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="54ef4-123">These certificates are only used for encrypting and decrypting the private configuration of the extension.</span></span> <span data-ttu-id="54ef4-124">Bu sertifikalar zaman aşımına uğrarsa önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="54ef4-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="54ef4-125">Sona erme tarihini işaretlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="54ef4-125">The expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="54ef4-126">Silinmiş sertifikalar beliriyor</span><span class="sxs-lookup"><span data-stu-id="54ef4-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="54ef4-127">Bu, büyük olasılıkla bir aracı gibi Visual Studio kullanıyorsanız nedeniyle beliriyor.</span><span class="sxs-lookup"><span data-stu-id="54ef4-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="54ef4-128">Her bir sertifika kullanarak bir aracıyla bağladığınızda, Azure'a yeniden yüklenecek.</span><span class="sxs-lookup"><span data-stu-id="54ef4-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded to Azure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="54ef4-129">My sertifikaları kayboluyor tutun</span><span class="sxs-lookup"><span data-stu-id="54ef4-129">My certificates keep disappearing</span></span>
<span data-ttu-id="54ef4-130">Sanal makine örneğini geri dönüştürüldüğünde, tüm yerel değişiklikler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="54ef4-130">When the virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="54ef4-131">Kullanım bir [başlangıç görevi](cloud-services-startup-tasks.md) sertifikaları için sanal makine rolü her başlatılışında yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="54ef4-131">Use a [startup task](cloud-services-startup-tasks.md) to install certificates to the virtual machine each time the role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-the-portal"></a><span data-ttu-id="54ef4-132">My yönetim sertifikaları Portalı'nda bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="54ef4-132">I cannot find my management certificates in the portal</span></span>
<span data-ttu-id="54ef4-133">[Yönetim sertifikaları](../azure-api-management-certs.md) yalnızca Azure Klasik Portalı'nda bulunur.</span><span class="sxs-lookup"><span data-stu-id="54ef4-133">[Management certificates](../azure-api-management-certs.md) are only available in the Azure Classic Portal.</span></span> <span data-ttu-id="54ef4-134">Geçerli Azure portalına yönetim sertifikaları kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="54ef4-134">The current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="54ef4-135">Bir yönetim sertifikası nasıl devre dışı bırakabilirim?</span><span class="sxs-lookup"><span data-stu-id="54ef4-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="54ef4-136">[Yönetim sertifikaları](../azure-api-management-certs.md) devre dışı bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="54ef4-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="54ef4-137">Artık kullanılması istemediğinizde Klasik Azure Portalı aracılığıyla silin.</span><span class="sxs-lookup"><span data-stu-id="54ef4-137">You delete them through the Azure Classic Portal when you do not want them to be used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="54ef4-138">Belirli bir IP adresi için bir SSL sertifikası nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="54ef4-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="54ef4-139">İçindeki yönergeleri izleyin [sertifika öğretici oluşturma](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="54ef4-139">Follow the directions in the [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="54ef4-140">IP adresi DNS adı olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="54ef4-140">Use the IP address as the DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="54ef4-141">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="54ef4-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="54ef4-142">SSL 3.0 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="54ef4-142">Disable SSL 3.0</span></span>
<span data-ttu-id="54ef4-143">SSL 3.0 devre dışı bırakın ve TLS güvenlik kullanmak için bu blog gönderisi konusunda belgelenen bir başlangıç görevi oluşturun: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="54ef4-143">To disable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-to-your-website"></a><span data-ttu-id="54ef4-144">Ekleme **nosniff** Web sitesine</span><span class="sxs-lookup"><span data-stu-id="54ef4-144">Add **nosniff** to your website</span></span>
<span data-ttu-id="54ef4-145">MIME türleri algılaması istemcilerin önlemek için bir ayar ekleyin, *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="54ef4-145">To prevent clients from sniffing the MIME types, add a setting in your *web.config* file.</span></span>

```xml
<configuration>
   <system.webServer>
      <httpProtocol>
         <customHeaders>
            <add name="X-Content-Type-Options" value="nosniff" />
         </customHeaders>
      </httpProtocol>
   </system.webServer>
</configuration>
```

<span data-ttu-id="54ef4-146">Ayrıca bu ayarı IIS'de olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="54ef4-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="54ef4-147">Aşağıdaki komutla kullanmak [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.</span><span class="sxs-lookup"><span data-stu-id="54ef4-147">Use the following command with the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="54ef4-148">IIS web rolü için özelleştirme</span><span class="sxs-lookup"><span data-stu-id="54ef4-148">Customize IIS for a web role</span></span>
<span data-ttu-id="54ef4-149">IIS başlangıç komut dosyasını kullanın [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.</span><span class="sxs-lookup"><span data-stu-id="54ef4-149">Use the IIS startup script from the [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="54ef4-150">Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="54ef4-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="54ef4-151">X ölçeklendirme olamaz örnekleri</span><span class="sxs-lookup"><span data-stu-id="54ef4-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="54ef4-152">Azure aboneliğinizi kullanabileceğiniz çekirdek sayısına bir sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="54ef4-152">Your Azure Subscription has a limit on the number of cores you can use.</span></span> <span data-ttu-id="54ef4-153">Kullanılabilir tüm çekirdek kullanılırsa ölçeklendirme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="54ef4-153">Scaling will not work if you have used all the cores available.</span></span> <span data-ttu-id="54ef4-154">Bir sınır 100 çekirdek varsa, örneğin, bu 100 A1 boyuta sahip sanal makine örneklerini bulut hizmetiniz için olabilir veya sanal makine örnekleri 50 A2 boyutu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="54ef4-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="54ef4-155">Ağ</span><span class="sxs-lookup"><span data-stu-id="54ef4-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="54ef4-156">Bir çoklu VIP bulut hizmetindeki bir IP rezerve edilemez</span><span class="sxs-lookup"><span data-stu-id="54ef4-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="54ef4-157">İlk olarak, IP için ayrılacak çalıştığınız sanal makine örneğini açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54ef4-157">First, make sure that the virtual machine instance that you're trying to reserve the IP for is turned on.</span></span> <span data-ttu-id="54ef4-158">İkinci olarak, ayrılmış IP'ler rahatsız için hazırlama ve üretim dağıtımları kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="54ef4-158">Second, make sure that you're using Reserved IPs for bother the staging and production deployments.</span></span> <span data-ttu-id="54ef4-159">**Sağlamadığı** dağıtım yükseltme sırasında ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="54ef4-159">**Do not** change the settings while the deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="54ef4-160">Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="54ef4-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="54ef4-161">Nasıl yedeklerim Uzak Masaüstü bir NSG olduğunda?</span><span class="sxs-lookup"><span data-stu-id="54ef4-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="54ef4-162">Noktalarında trafiğine izin veren NSG kuralları eklemek **3389** ve **20000**.</span><span class="sxs-lookup"><span data-stu-id="54ef4-162">Add rules to the NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="54ef4-163">Uzak Masaüstü bağlantı noktasını kullanır **3389**.</span><span class="sxs-lookup"><span data-stu-id="54ef4-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="54ef4-164">Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, doğrudan bağlanmak için hangi örneğinin denetleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="54ef4-164">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="54ef4-165">*RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve istemcisinin bir RDP tanımlama bilgisi göndermek ve bağlanmak için tek bir örnek belirtin.</span><span class="sxs-lookup"><span data-stu-id="54ef4-165">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="54ef4-166">*RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.</span><span class="sxs-lookup"><span data-stu-id="54ef4-166">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
