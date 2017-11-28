---
title: "aaaCloud Hizmetleri ve yönetim sertifikaları | Microsoft Docs"
description: "Nasıl toocreate ve kullanım sertifikaları Microsoft Azure ile bilgi edinin"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: fc70d00d-899b-4771-855f-44574dc4bfc6
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: 69cb5467ece58a91dae06b4120954aeb2826bde1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="certificates-overview-for-azure-cloud-services"></a><span data-ttu-id="7f501-103">Azure Cloud Services sertifikalarına genel bakış</span><span class="sxs-lookup"><span data-stu-id="7f501-103">Certificates overview for Azure Cloud Services</span></span>
<span data-ttu-id="7f501-104">Sertifikalar ile Azure bulut Hizmetleri için kullanılır ([hizmet sertifikaları](#what-are-service-certificates)) ve hello yönetim API'si ile kimlik doğrulaması için ([yönetim sertifikaları](#what-are-management-certificates) zaman kullanarak izin ver hello Klasik Azure portalı ve değil Merhaba olmayan Klasik Azure portalı).</span><span class="sxs-lookup"><span data-stu-id="7f501-104">Certificates are used in Azure for cloud services ([service certificates](#what-are-service-certificates)) and for authenticating with hello management API ([management certificates](#what-are-management-certificates) when using hello Azure classic portal and not hello non-classic Azure portal).</span></span> <span data-ttu-id="7f501-105">Bu konuda iki sertifika türleri için genel bir bakış nasıl çok verir[oluşturma](#create) ve [dağıtmak](#deploy) bunları tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7f501-105">This topic gives a general overview of both certificate types, how too[create](#create) and [deploy](#deploy) them tooAzure.</span></span>

<span data-ttu-id="7f501-106">Azure'da kullanılan sertifikalar x.509 v3 sertifikaları ve başka bir güvenilen sertifika tarafından imzalanan ya da kendinden imzalı olabilirler.</span><span class="sxs-lookup"><span data-stu-id="7f501-106">Certificates used in Azure are x.509 v3 certificates and can be signed by another trusted certificate or they can be self-signed.</span></span> <span data-ttu-id="7f501-107">Otomatik olarak imzalanan sertifika kendi oluşturucusu tarafından imzalanan, bu nedenle varsayılan olarak güvenilmiyor.</span><span class="sxs-lookup"><span data-stu-id="7f501-107">A self-signed certificate is signed by its own creator, therefore it is not trusted by default.</span></span> <span data-ttu-id="7f501-108">Çoğu tarayıcılar bu sorunu yoksayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f501-108">Most browsers can ignore this problem.</span></span> <span data-ttu-id="7f501-109">Yalnızca geliştirme ve sınama bulut Hizmetleri zaman otomatik olarak imzalanan sertifikalar kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f501-109">You should only use self-signed certificates when developing and testing your cloud services.</span></span> 

<span data-ttu-id="7f501-110">Azure tarafından kullanılan sertifikalar, özel veya ortak anahtar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7f501-110">Certificates used by Azure can contain a private or a public key.</span></span> <span data-ttu-id="7f501-111">Sertifikalara sahip bir yol tooidentify sağlayan bir parmak izi anlaşılır şekilde bunları.</span><span class="sxs-lookup"><span data-stu-id="7f501-111">Certificates have a thumbprint that provides a means tooidentify them in an unambiguous way.</span></span> <span data-ttu-id="7f501-112">Bu parmak izine hello Azure kullanılan [yapılandırma dosyası](cloud-services-configure-ssl-certificate.md) bir bulut hizmeti sertifika tooidentify kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7f501-112">This thumbprint is used in hello Azure [configuration file](cloud-services-configure-ssl-certificate.md) tooidentify which certificate a cloud service should use.</span></span> 

## <a name="what-are-service-certificates"></a><span data-ttu-id="7f501-113">Hizmet sertifikaları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="7f501-113">What are service certificates?</span></span>
<span data-ttu-id="7f501-114">Hizmet sertifikaları ekli toocloud hizmetler ve güvenli iletişim tooand hello hizmetinden etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="7f501-114">Service certificates are attached toocloud services and enable secure communication tooand from hello service.</span></span> <span data-ttu-id="7f501-115">Örneğin, bir web rolü dağıttıysanız toosupply sunulan bir HTTPS uç noktası doğrulanabilir bir sertifika istersiniz.</span><span class="sxs-lookup"><span data-stu-id="7f501-115">For example, if you deployed a web role, you would want toosupply a certificate that can authenticate an exposed HTTPS endpoint.</span></span> <span data-ttu-id="7f501-116">Hizmet tanımında tanımlanan hizmeti, otomatik olarak dağıtılan toohello sanal makineyi, rol örneği çalıştıran sertifikalardır.</span><span class="sxs-lookup"><span data-stu-id="7f501-116">Service certificates, defined in your service definition, are automatically deployed toohello virtual machine that is running an instance of your role.</span></span> 

<span data-ttu-id="7f501-117">Hizmet sertifikaları tooAzure Klasik yükleyebilirsiniz portal ya da kullanarak hello Azure Klasik portalı veya hello Klasik dağıtım modelini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7f501-117">You can upload service certificates tooAzure classic portal either using hello Azure classic portal or by using hello classic deployment model.</span></span> <span data-ttu-id="7f501-118">Hizmet sertifikaları özel bulut hizmeti ile ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="7f501-118">Service certificates are associated with a specific cloud service.</span></span> <span data-ttu-id="7f501-119">Merhaba hizmet tanımı dosyasında tooa dağıtım atanmışlarsa.</span><span class="sxs-lookup"><span data-stu-id="7f501-119">They are assigned tooa deployment in hello service definition file.</span></span>

<span data-ttu-id="7f501-120">Hizmet sertifikaları, Hizmetleri'nden ayrı olarak yönetilebilir ve farklı kişiler tarafından yönetiliyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="7f501-120">Service certificates can be managed separately from your services, and may be managed by different individuals.</span></span> <span data-ttu-id="7f501-121">Örneğin, bir geliştirici bir BT yöneticisi tooAzure önceden yükledi tooa sertifika başvuruyor bir hizmet paketi yükleme.</span><span class="sxs-lookup"><span data-stu-id="7f501-121">For example, a developer may upload a service package that refers tooa certificate that an IT manager has previously uploaded tooAzure.</span></span> <span data-ttu-id="7f501-122">Bir BT yöneticisi, yönetin ve tooupload yeni bir hizmet paketi olmadan (Merhaba hizmetinin başlangıç yapılandırmasını değiştirme), bu sertifikayı yenilemek.</span><span class="sxs-lookup"><span data-stu-id="7f501-122">An IT manager can manage and renew that certificate (changing hello configuration of hello service) without needing tooupload a new service package.</span></span> <span data-ttu-id="7f501-123">Yeni bir hizmet paketi güncelleştirme hello mantıksal adı, depo adı ve hello sertifikasının konumunu hello hizmet tanımı dosyasında olduğundan ve hello sertifika parmak izi hello hizmet yapılandırma dosyasında belirtilen sırada mümkündür.</span><span class="sxs-lookup"><span data-stu-id="7f501-123">Updating without a new service package is possible because hello logical name, store name, and location of hello certificate is in hello service definition file and while hello certificate thumbprint is specified in hello service configuration file.</span></span> <span data-ttu-id="7f501-124">tooupdate Merhaba, yalnızca yeni bir sertifika ve değişiklik hello parmak izi hello hizmet yapılandırma dosyasında değer gerekli tooupload sertifikasıdır.</span><span class="sxs-lookup"><span data-stu-id="7f501-124">tooupdate hello certificate, it's only necessary tooupload a new certificate and change hello thumbprint value in hello service configuration file.</span></span>

>[!Note]
><span data-ttu-id="7f501-125">Merhaba [bulut Hizmetleri ile ilgili SSS](cloud-services-faq.md) makale bazı sertifikalar hakkında yararlı bilgiler sahiptir.</span><span class="sxs-lookup"><span data-stu-id="7f501-125">hello [Cloud Services FAQ](cloud-services-faq.md) article has some helpful information about certificates.</span></span>

## <a name="what-are-management-certificates"></a><span data-ttu-id="7f501-126">Yönetim sertifikaları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="7f501-126">What are management certificates?</span></span>
<span data-ttu-id="7f501-127">Yönetim sertifikaları hello Klasik dağıtım modeliyle tooauthenticate izin verin.</span><span class="sxs-lookup"><span data-stu-id="7f501-127">Management certificates allow you tooauthenticate with hello classic deployment model.</span></span> <span data-ttu-id="7f501-128">Birçok programlar ve araçlar (örneğin, Visual Studio veya hello Azure SDK'sı) Bu sertifika tooautomate yapılandırması ve çeşitli Azure hizmetlerine dağıtımını kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f501-128">Many programs and tools (such as Visual Studio or hello Azure SDK) use these certificates tooautomate configuration and deployment of various Azure services.</span></span> <span data-ttu-id="7f501-129">Bunlar değil gerçekten ilgili toocloud hizmetlerdir.</span><span class="sxs-lookup"><span data-stu-id="7f501-129">These are not really related toocloud services.</span></span> 

> [!WARNING]
> <span data-ttu-id="7f501-130">Dikkat et!</span><span class="sxs-lookup"><span data-stu-id="7f501-130">Be careful!</span></span> <span data-ttu-id="7f501-131">Bu tür bir sertifika ile kimliklerini doğrulayan herkes izin bunların ilişkili toomanage hello abonelik.</span><span class="sxs-lookup"><span data-stu-id="7f501-131">These types of certificates allow anyone who authenticates with them toomanage hello subscription they are associated with.</span></span> 
> 
> 

### <a name="limitations"></a><span data-ttu-id="7f501-132">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="7f501-132">Limitations</span></span>
<span data-ttu-id="7f501-133">Abonelik başına 100 Yönetim sertifikaları sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="7f501-133">There is a limit of 100 management certificates per subscription.</span></span> <span data-ttu-id="7f501-134">Ayrıca belirli hizmet yöneticisinin kullanıcı kimliğini altındaki tüm abonelikler için 100 Yönetim sertifikaları sınırı vardır</span><span class="sxs-lookup"><span data-stu-id="7f501-134">There is also a limit of 100 management certificates for all subscriptions under a specific service administrator’s user ID.</span></span> <span data-ttu-id="7f501-135">Merhaba Hesap Yöneticisi Hello kullanıcı kimliği zaten kullanılan tooadd 100 Yönetim sertifikaları ve sertifika gereksinimi yoktur, bir ortak yönetici tooadd hello ek sertifikalar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7f501-135">If hello user ID for hello account administrator has already been used tooadd 100 management certificates and there is a need for more certificates, you can add a co-administrator tooadd hello additional certificates.</span></span> 

<span data-ttu-id="7f501-136">100'den fazla sertifika eklemeden önce varolan bir sertifikayı yeniden bakın.</span><span class="sxs-lookup"><span data-stu-id="7f501-136">Before adding more than 100 certificates, see if you can reuse an existing certificate.</span></span> <span data-ttu-id="7f501-137">Ortak Yöneticiler kullanarak olası gereksiz karmaşıklığı tooyour sertifika yönetimi işlemi ekler.</span><span class="sxs-lookup"><span data-stu-id="7f501-137">Using co-administrators adds potentially unneeded complexity tooyour certificate management process.</span></span>

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a><span data-ttu-id="7f501-138">Yeni bir otomatik olarak imzalanan sertifika oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f501-138">Create a new self-signed certificate</span></span>
<span data-ttu-id="7f501-139">Bunlar toothese ayarları izliyor olduğunuz sürece tüm aracı kullanılabilir toocreate otomatik olarak imzalanan sertifika kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7f501-139">You can use any tool available toocreate a self-signed certificate as long as they adhere toothese settings:</span></span>

* <span data-ttu-id="7f501-140">Bir X.509 sertifikası.</span><span class="sxs-lookup"><span data-stu-id="7f501-140">An X.509 certificate.</span></span>
* <span data-ttu-id="7f501-141">Bir özel anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="7f501-141">Contains a private key.</span></span>
* <span data-ttu-id="7f501-142">Anahtar Değişimi (.pfx dosyası) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7f501-142">Created for key exchange (.pfx file).</span></span>
* <span data-ttu-id="7f501-143">Konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="7f501-143">Subject name must match hello domain used tooaccess hello cloud service.</span></span>

    > <span data-ttu-id="7f501-144">Merhaba cloudapp.net için bir SSL sertifikası alınamıyor (veya herhangi bir için Azure ile ilgili) etki alanı; Merhaba sertifikanın konu adı hello özel etki alanı adı kullanılan tooaccess uygulamanızı eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f501-144">You cannot acquire an SSL certificate for hello cloudapp.net (or for any Azure-related) domain; hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="7f501-145">Örneğin, **contoso.net**değil **contoso.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="7f501-145">For example, **contoso.net**, not **contoso.cloudapp.net**.</span></span>

* <span data-ttu-id="7f501-146">En az 2048 bit şifreleme.</span><span class="sxs-lookup"><span data-stu-id="7f501-146">Minimum of 2048-bit encryption.</span></span>
* <span data-ttu-id="7f501-147">**Hizmet sertifika yalnızca**: istemci-tarafı sertifika hello bulunmalıdır *kişisel* sertifika deposu.</span><span class="sxs-lookup"><span data-stu-id="7f501-147">**Service Certificate Only**: Client-side certificate must reside in hello *Personal* certificate store.</span></span>

<span data-ttu-id="7f501-148">Vardır iki kolay yolları toocreate bir sertifika, Windows hello ile `makecert.exe` yardımcı programı veya IIS.</span><span class="sxs-lookup"><span data-stu-id="7f501-148">There are two easy ways toocreate a certificate on Windows, with hello `makecert.exe` utility, or IIS.</span></span>

### <a name="makecertexe"></a><span data-ttu-id="7f501-149">MakeCert.exe</span><span class="sxs-lookup"><span data-stu-id="7f501-149">Makecert.exe</span></span>
<span data-ttu-id="7f501-150">Bu yardımcı program kullanım dışı bırakıldı ve artık aşağıda anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7f501-150">This utility has been deprecated and is no longer documented here.</span></span> <span data-ttu-id="7f501-151">Daha fazla bilgi için bkz: [bu MSDN makalesine](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span><span class="sxs-lookup"><span data-stu-id="7f501-151">For more information, see [this MSDN article](https://msdn.microsoft.com/library/windows/desktop/aa386968).</span></span>

### <a name="powershell"></a><span data-ttu-id="7f501-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f501-152">PowerShell</span></span>
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> <span data-ttu-id="7f501-153">Bir etki alanı yerine IP adresiyle toouse hello sertifika isterseniz, başlangıç IP adresi hello - DnsName parametresinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="7f501-153">If you want toouse hello certificate with an IP address instead of a domain, use hello IP address in hello -DnsName parameter.</span></span>


<span data-ttu-id="7f501-154">Bu toouse istiyorsanız [sertifika hello Yönetim Portalı ile](../azure-api-management-certs.md), tooa dışa **.cer** dosyası:</span><span class="sxs-lookup"><span data-stu-id="7f501-154">If you want toouse this [certificate with hello management portal](../azure-api-management-certs.md), export it tooa **.cer** file:</span></span>

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a><span data-ttu-id="7f501-155">Internet Information Services (IIS)</span><span class="sxs-lookup"><span data-stu-id="7f501-155">Internet Information Services (IIS)</span></span>
<span data-ttu-id="7f501-156">Merhaba üzerinde birden çok sayfa olan kapak Internet nasıl toodo bu IIS ile.</span><span class="sxs-lookup"><span data-stu-id="7f501-156">There are many pages on hello internet that cover how toodo this with IIS.</span></span> <span data-ttu-id="7f501-157">[Burada](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) harika bir bulunan yeni çalışmaktan de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7f501-157">[Here](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) is a great one I found that I think explains it well.</span></span> 

### <a name="java"></a><span data-ttu-id="7f501-158">Java</span><span class="sxs-lookup"><span data-stu-id="7f501-158">Java</span></span>
<span data-ttu-id="7f501-159">Java kullanabileceğine[bir sertifika oluşturmak](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span><span class="sxs-lookup"><span data-stu-id="7f501-159">You can use Java too[create a certificate](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).</span></span>

### <a name="linux"></a><span data-ttu-id="7f501-160">Linux</span><span class="sxs-lookup"><span data-stu-id="7f501-160">Linux</span></span>
<span data-ttu-id="7f501-161">[Bu](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makalede nasıl toocreate SSH ile sertifikalar.</span><span class="sxs-lookup"><span data-stu-id="7f501-161">[This](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article describes how toocreate certificates with SSH.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f501-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7f501-162">Next steps</span></span>
<span data-ttu-id="7f501-163">[Hizmet sertifika toohello Klasik Azure portalı karşıya](cloud-services-configure-ssl-certificate.md) (veya hello [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="7f501-163">[Upload your service certificate toohello Azure classic portal](cloud-services-configure-ssl-certificate.md) (or hello [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).</span></span>

<span data-ttu-id="7f501-164">Karşıya bir [yönetim API sertifikası](../azure-api-management-certs.md) toohello Klasik Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="7f501-164">Upload a [management API certificate](../azure-api-management-certs.md) toohello Azure classic portal.</span></span> <span data-ttu-id="7f501-165">Hello Azure portalı, kimlik doğrulaması için yönetim sertifikaları kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="7f501-165">hello Azure portal does not use management certificates for authentication.</span></span>

