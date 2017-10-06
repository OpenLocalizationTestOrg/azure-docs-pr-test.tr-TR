---
title: aaaAzure bulut Hizmetleri rolleri ile ilgili SSS | Microsoft Docs
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
ms.openlocfilehash: b07a1990e031e60ae919a5f7c636945b89c7d3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-services-faq"></a><span data-ttu-id="f9d6b-104">Cloud Services SSS</span><span class="sxs-lookup"><span data-stu-id="f9d6b-104">Cloud Services FAQ</span></span>
<span data-ttu-id="f9d6b-105">Bu makalede, Microsoft Azure bulut hizmetleri hakkında sık sorulan bazı sorular yanıtlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-105">This article answers some frequently asked questions about Microsoft Azure Cloud Services.</span></span> <span data-ttu-id="f9d6b-106">Merhaba ziyaret edebilirsiniz [Azure destek SSS](http://go.microsoft.com/fwlink/?LinkID=185083) genel Azure fiyatlandırma ve destek bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-106">You can also visit hello [Azure Support FAQ](http://go.microsoft.com/fwlink/?LinkID=185083) for general Azure pricing and support information.</span></span> <span data-ttu-id="f9d6b-107">Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-107">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

## <a name="certificates"></a><span data-ttu-id="f9d6b-108">Sertifikalar</span><span class="sxs-lookup"><span data-stu-id="f9d6b-108">Certificates</span></span>
### <a name="where-should-i-install-my-certificate"></a><span data-ttu-id="f9d6b-109">My sertifika burada yüklemeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="f9d6b-109">Where should I install my certificate?</span></span>
* <span data-ttu-id="f9d6b-110">**Uygulamam**</span><span class="sxs-lookup"><span data-stu-id="f9d6b-110">**My**</span></span>  
  <span data-ttu-id="f9d6b-111">Uygulama sertifikayı özel anahtarla (\*.pfx, \*.p12).</span><span class="sxs-lookup"><span data-stu-id="f9d6b-111">Application Certificate with private key (\*.pfx, \*.p12).</span></span>
* <span data-ttu-id="f9d6b-112">**CA**</span><span class="sxs-lookup"><span data-stu-id="f9d6b-112">**CA**</span></span>  
  <span data-ttu-id="f9d6b-113">Tüm ara sertifikalarınız bu deposunda (ilke ve alt CA'lar) gidin.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-113">All your intermediate certificates go in this store (Policy and Sub CAs).</span></span>
* <span data-ttu-id="f9d6b-114">**KÖK**</span><span class="sxs-lookup"><span data-stu-id="f9d6b-114">**ROOT**</span></span>  
  <span data-ttu-id="f9d6b-115">Ana kök CA sertifikası burada gitmesi gereken şekilde Hello kök CA depolar.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-115">hello root CA store, so your main root CA cert should go here.</span></span>

### <a name="i-cant-remove-expired-certificate"></a><span data-ttu-id="f9d6b-116">Süresi dolan sertifika kaldırılamıyor.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-116">I can't remove expired certificate</span></span>
<span data-ttu-id="f9d6b-117">Azure kullanımda olduğu sırada bir sertifika kaldırmasını engeller.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-117">Azure prevents you from removing a certificate while it is in use.</span></span> <span data-ttu-id="f9d6b-118">Merhaba sertifikayı kullanan tooeither Sil hello dağıtımı veya güncelleştirme hello dağıtımı farklı veya yenilenmiş bir sertifika ile gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-118">You need tooeither delete hello deployment that uses hello certificate, or update hello deployment with a different or renewed certificate.</span></span>

### <a name="delete-an-expired-certificate"></a><span data-ttu-id="f9d6b-119">Süresi dolmuş bir sertifika Sil</span><span class="sxs-lookup"><span data-stu-id="f9d6b-119">Delete an expired certificate</span></span>
<span data-ttu-id="f9d6b-120">Hello sertifika kullanılmadığı sürece hello kullanabilirsiniz [Kaldır AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove bir sertifika.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-120">As long as hello certificate is not in use, you can use hello [Remove-AzureCertificate](https://msdn.microsoft.com/library/azure/mt589145.aspx) PowerShell cmdlet tooremove a certificate.</span></span>

### <a name="i-have-expired-certificates-named-windows-azure-service-management-for-extensions"></a><span data-ttu-id="f9d6b-121">Windows Azure hizmet yönetimi için Uzantılar adlı sertifikalar süresi dolmuş</span><span class="sxs-lookup"><span data-stu-id="f9d6b-121">I have expired certificates named Windows Azure Service Management for Extensions</span></span>
<span data-ttu-id="f9d6b-122">Uzak Masaüstü uzantısı hello gibi toohello bulut hizmeti uzantı eklendiğinde bu sertifikaları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-122">These certificates are created whenever an extension is added toohello cloud service such as hello Remote Desktop extension.</span></span> <span data-ttu-id="f9d6b-123">Bu sertifikalar yalnızca şifreleme ve hello özel yapılandırma hello uzantısı'nın şifresini çözmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-123">These certificates are only used for encrypting and decrypting hello private configuration of hello extension.</span></span> <span data-ttu-id="f9d6b-124">Bu sertifikalar zaman aşımına uğrarsa önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-124">It does not matter if these certificates expire.</span></span> <span data-ttu-id="f9d6b-125">Merhaba sona erme tarihi işaretlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-125">hello expiration date is not checked.</span></span>

### <a name="certificates-i-have-deleted-keep-reappearing"></a><span data-ttu-id="f9d6b-126">Silinmiş sertifikalar beliriyor</span><span class="sxs-lookup"><span data-stu-id="f9d6b-126">Certificates I have deleted keep reappearing</span></span>
<span data-ttu-id="f9d6b-127">Bu, büyük olasılıkla bir aracı gibi Visual Studio kullanıyorsanız nedeniyle beliriyor.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-127">These keep reappearing most likely because of a tool you're using, such as Visual Studio.</span></span> <span data-ttu-id="f9d6b-128">Her bir sertifika kullanarak bir aracıyla bağladığınızda, yeniden yüklenen tooAzure olur.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-128">Whenever you reconnect with a tool that is using a certificate, it will again be uploaded tooAzure.</span></span>

### <a name="my-certificates-keep-disappearing"></a><span data-ttu-id="f9d6b-129">My sertifikaları kayboluyor tutun</span><span class="sxs-lookup"><span data-stu-id="f9d6b-129">My certificates keep disappearing</span></span>
<span data-ttu-id="f9d6b-130">Merhaba sanal makine örneğini geri dönüştürüldüğünde, tüm yerel değişiklikler kaybolur.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-130">When hello virtual machine instance recycles, all local changes are lost.</span></span> <span data-ttu-id="f9d6b-131">Kullanım bir [başlangıç görevi](cloud-services-startup-tasks.md) tooinstall sertifikaları toohello sanal makineyi her zaman hello rol başlatır.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-131">Use a [startup task](cloud-services-startup-tasks.md) tooinstall certificates toohello virtual machine each time hello role starts.</span></span>

### <a name="i-cannot-find-my-management-certificates-in-hello-portal"></a><span data-ttu-id="f9d6b-132">My yönetim sertifikaları hello Portalı'nda bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="f9d6b-132">I cannot find my management certificates in hello portal</span></span>
<span data-ttu-id="f9d6b-133">[Yönetim sertifikaları](../azure-api-management-certs.md) yalnızca hello Klasik Azure portalı içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-133">[Management certificates](../azure-api-management-certs.md) are only available in hello Azure Classic Portal.</span></span> <span data-ttu-id="f9d6b-134">Merhaba geçerli Azure portalına yönetim sertifikaları kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-134">hello current Azure portal does not use management certificates.</span></span> 

### <a name="how-can-i-disable-a-management-certificate"></a><span data-ttu-id="f9d6b-135">Bir yönetim sertifikası nasıl devre dışı bırakabilirim?</span><span class="sxs-lookup"><span data-stu-id="f9d6b-135">How can I disable a management certificate?</span></span>
<span data-ttu-id="f9d6b-136">[Yönetim sertifikaları](../azure-api-management-certs.md) devre dışı bırakılamaz.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-136">[Management certificates](../azure-api-management-certs.md) cannot be disabled.</span></span> <span data-ttu-id="f9d6b-137">Bunları istemiyorsanız, bunları hello Klasik Azure portalı artık kullanılan toobe silin.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-137">You delete them through hello Azure Classic Portal when you do not want them toobe used anymore.</span></span>

### <a name="how-do-i-create-an-ssl-certificate-for-a-specific-ip-address"></a><span data-ttu-id="f9d6b-138">Belirli bir IP adresi için bir SSL sertifikası nasıl oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="f9d6b-138">How do I create an SSL certificate for a specific IP address?</span></span>
<span data-ttu-id="f9d6b-139">Merhaba hello içindeki yönergeleri izleyin [sertifika öğretici oluşturma](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="f9d6b-139">Follow hello directions in hello [create a certificate tutorial](cloud-services-certs-create.md).</span></span> <span data-ttu-id="f9d6b-140">Başlangıç IP adresi, DNS adı hello olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-140">Use hello IP address as hello DNS Name.</span></span>

## <a name="security"></a><span data-ttu-id="f9d6b-141">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="f9d6b-141">Security</span></span>
### <a name="disable-ssl-30"></a><span data-ttu-id="f9d6b-142">SSL 3.0 devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="f9d6b-142">Disable SSL 3.0</span></span>
<span data-ttu-id="f9d6b-143">toodisable SSL 3.0 ve TLS güvenlik kullanın, bu blog gönderisi konusunda belgelenen bir başlangıç görevi oluşturun: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span><span class="sxs-lookup"><span data-stu-id="f9d6b-143">toodisable SSL 3.0 and use TLS security, create a startup task which is documented on this blog post: https://azure.microsoft.com/en-us/blog/how-to-disable-ssl-3-0-in-azure-websites-roles-and-virtual-machines/</span></span>

### <a name="add-nosniff-tooyour-website"></a><span data-ttu-id="f9d6b-144">Ekleme **nosniff** tooyour Web sitesi</span><span class="sxs-lookup"><span data-stu-id="f9d6b-144">Add **nosniff** tooyour website</span></span>
<span data-ttu-id="f9d6b-145">Merhaba MIME türleri algılaması istemcilerinden tooprevent bir ayar ekleyin, *web.config* dosya.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-145">tooprevent clients from sniffing hello MIME types, add a setting in your *web.config* file.</span></span>

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

<span data-ttu-id="f9d6b-146">Ayrıca bu ayarı IIS'de olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-146">You can also add this as a setting in IIS.</span></span> <span data-ttu-id="f9d6b-147">Kullanım hello aşağıdaki komut ile Merhaba [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-147">Use hello following command with hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

```cmd
%windir%\system32\inetsrv\appcmd set config /section:httpProtocol /+customHeaders.[name='X-Content-Type-Options',value='nosniff']
```

### <a name="customize-iis-for-a-web-role"></a><span data-ttu-id="f9d6b-148">IIS web rolü için özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f9d6b-148">Customize IIS for a web role</span></span>
<span data-ttu-id="f9d6b-149">Merhaba IIS Başlangıç hello betikten kullanmak [ortak başlangıç görevleri](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) makalesi.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-149">Use hello IIS startup script from hello [common startup tasks](cloud-services-startup-tasks-common.md#configure-iis-startup-with-appcmdexe) article.</span></span>

## <a name="scaling"></a><span data-ttu-id="f9d6b-150">Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="f9d6b-150">Scaling</span></span>
### <a name="i-cannot-scale-beyond-x-instances"></a><span data-ttu-id="f9d6b-151">X ölçeklendirme olamaz örnekleri</span><span class="sxs-lookup"><span data-stu-id="f9d6b-151">I cannot scale beyond X instances</span></span>
<span data-ttu-id="f9d6b-152">Azure aboneliğinizi hello kullanabileceğiniz çekirdek sayısına bir sınır vardır.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-152">Your Azure Subscription has a limit on hello number of cores you can use.</span></span> <span data-ttu-id="f9d6b-153">Kullanılabilir tüm hello çekirdek kullanılırsa ölçeklendirme çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-153">Scaling will not work if you have used all hello cores available.</span></span> <span data-ttu-id="f9d6b-154">Bir sınır 100 çekirdek varsa, örneğin, bu 100 A1 boyuta sahip sanal makine örneklerini bulut hizmetiniz için olabilir veya sanal makine örnekleri 50 A2 boyutu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-154">For example, if you have a limit of 100 cores, this means you could have 100 A1 sized virtual machine instances for your cloud service, or 50 A2 sized virtual machine instances.</span></span>

## <a name="networking"></a><span data-ttu-id="f9d6b-155">Ağ</span><span class="sxs-lookup"><span data-stu-id="f9d6b-155">Networking</span></span>
### <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a><span data-ttu-id="f9d6b-156">Bir çoklu VIP bulut hizmetindeki bir IP rezerve edilemez</span><span class="sxs-lookup"><span data-stu-id="f9d6b-156">I can't reserve an IP in a multi-VIP cloud service</span></span>
<span data-ttu-id="f9d6b-157">Öncelikle, tooreserve hello IP için çalıştığınız bu hello sanal makine örneğini açık olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-157">First, make sure that hello virtual machine instance that you're trying tooreserve hello IP for is turned on.</span></span> <span data-ttu-id="f9d6b-158">İkinci olarak, ayrılmış IP'ler rahatsız hello hazırlama ve üretim dağıtımları için kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-158">Second, make sure that you're using Reserved IPs for bother hello staging and production deployments.</span></span> <span data-ttu-id="f9d6b-159">**Sağlamadığı** hello dağıtım yükseltme sırasında hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-159">**Do not** change hello settings while hello deployment is upgrading.</span></span>

## <a name="remote-desktop"></a><span data-ttu-id="f9d6b-160">Uzak Masaüstü</span><span class="sxs-lookup"><span data-stu-id="f9d6b-160">Remote desktop</span></span>
### <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a><span data-ttu-id="f9d6b-161">Nasıl yedeklerim Uzak Masaüstü bir NSG olduğunda?</span><span class="sxs-lookup"><span data-stu-id="f9d6b-161">How do I remote desktop when I have an NSG?</span></span>
<span data-ttu-id="f9d6b-162">Kuralları toohello noktalarında trafiğine izin veren NSG ekleme **3389** ve **20000**.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-162">Add rules toohello NSG that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="f9d6b-163">Uzak Masaüstü bağlantı noktasını kullanır **3389**.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-163">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="f9d6b-164">Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, hangi örneğinin tooconnect doğrudan denetleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-164">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="f9d6b-165">Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve hello istemci toosend bir RDP izin ver ve bir tek tek örnek tooconnect belirtin.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-165">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="f9d6b-166">Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000*** açılıp, hangi engellenmiş olabilir bir NSG varsa.</span><span class="sxs-lookup"><span data-stu-id="f9d6b-166">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>
