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
# <a name="certificates-overview-for-azure-cloud-services"></a>Azure Cloud Services sertifikalarına genel bakış
Sertifikalar ile Azure bulut Hizmetleri için kullanılır ([hizmet sertifikaları](#what-are-service-certificates)) ve hello yönetim API'si ile kimlik doğrulaması için ([yönetim sertifikaları](#what-are-management-certificates) zaman kullanarak izin ver hello Klasik Azure portalı ve değil Merhaba olmayan Klasik Azure portalı). Bu konuda iki sertifika türleri için genel bir bakış nasıl çok verir[oluşturma](#create) ve [dağıtmak](#deploy) bunları tooAzure.

Azure'da kullanılan sertifikalar x.509 v3 sertifikaları ve başka bir güvenilen sertifika tarafından imzalanan ya da kendinden imzalı olabilirler. Otomatik olarak imzalanan sertifika kendi oluşturucusu tarafından imzalanan, bu nedenle varsayılan olarak güvenilmiyor. Çoğu tarayıcılar bu sorunu yoksayabilirsiniz. Yalnızca geliştirme ve sınama bulut Hizmetleri zaman otomatik olarak imzalanan sertifikalar kullanmanız gerekir. 

Azure tarafından kullanılan sertifikalar, özel veya ortak anahtar içerebilir. Sertifikalara sahip bir yol tooidentify sağlayan bir parmak izi anlaşılır şekilde bunları. Bu parmak izine hello Azure kullanılan [yapılandırma dosyası](cloud-services-configure-ssl-certificate.md) bir bulut hizmeti sertifika tooidentify kullanmalıdır. 

## <a name="what-are-service-certificates"></a>Hizmet sertifikaları nelerdir?
Hizmet sertifikaları ekli toocloud hizmetler ve güvenli iletişim tooand hello hizmetinden etkinleştirin. Örneğin, bir web rolü dağıttıysanız toosupply sunulan bir HTTPS uç noktası doğrulanabilir bir sertifika istersiniz. Hizmet tanımında tanımlanan hizmeti, otomatik olarak dağıtılan toohello sanal makineyi, rol örneği çalıştıran sertifikalardır. 

Hizmet sertifikaları tooAzure Klasik yükleyebilirsiniz portal ya da kullanarak hello Azure Klasik portalı veya hello Klasik dağıtım modelini kullanarak. Hizmet sertifikaları özel bulut hizmeti ile ilişkilendirilmiş. Merhaba hizmet tanımı dosyasında tooa dağıtım atanmışlarsa.

Hizmet sertifikaları, Hizmetleri'nden ayrı olarak yönetilebilir ve farklı kişiler tarafından yönetiliyor olabilir. Örneğin, bir geliştirici bir BT yöneticisi tooAzure önceden yükledi tooa sertifika başvuruyor bir hizmet paketi yükleme. Bir BT yöneticisi, yönetin ve tooupload yeni bir hizmet paketi olmadan (Merhaba hizmetinin başlangıç yapılandırmasını değiştirme), bu sertifikayı yenilemek. Yeni bir hizmet paketi güncelleştirme hello mantıksal adı, depo adı ve hello sertifikasının konumunu hello hizmet tanımı dosyasında olduğundan ve hello sertifika parmak izi hello hizmet yapılandırma dosyasında belirtilen sırada mümkündür. tooupdate Merhaba, yalnızca yeni bir sertifika ve değişiklik hello parmak izi hello hizmet yapılandırma dosyasında değer gerekli tooupload sertifikasıdır.

>[!Note]
>Merhaba [bulut Hizmetleri ile ilgili SSS](cloud-services-faq.md) makale bazı sertifikalar hakkında yararlı bilgiler sahiptir.

## <a name="what-are-management-certificates"></a>Yönetim sertifikaları nelerdir?
Yönetim sertifikaları hello Klasik dağıtım modeliyle tooauthenticate izin verin. Birçok programlar ve araçlar (örneğin, Visual Studio veya hello Azure SDK'sı) Bu sertifika tooautomate yapılandırması ve çeşitli Azure hizmetlerine dağıtımını kullanın. Bunlar değil gerçekten ilgili toocloud hizmetlerdir. 

> [!WARNING]
> Dikkat et! Bu tür bir sertifika ile kimliklerini doğrulayan herkes izin bunların ilişkili toomanage hello abonelik. 
> 
> 

### <a name="limitations"></a>Sınırlamalar
Abonelik başına 100 Yönetim sertifikaları sınırı yoktur. Ayrıca belirli hizmet yöneticisinin kullanıcı kimliğini altındaki tüm abonelikler için 100 Yönetim sertifikaları sınırı vardır Merhaba Hesap Yöneticisi Hello kullanıcı kimliği zaten kullanılan tooadd 100 Yönetim sertifikaları ve sertifika gereksinimi yoktur, bir ortak yönetici tooadd hello ek sertifikalar ekleyebilirsiniz. 

100'den fazla sertifika eklemeden önce varolan bir sertifikayı yeniden bakın. Ortak Yöneticiler kullanarak olası gereksiz karmaşıklığı tooyour sertifika yönetimi işlemi ekler.

<a name="create"></a>
## <a name="create-a-new-self-signed-certificate"></a>Yeni bir otomatik olarak imzalanan sertifika oluşturma
Bunlar toothese ayarları izliyor olduğunuz sürece tüm aracı kullanılabilir toocreate otomatik olarak imzalanan sertifika kullanabilirsiniz:

* Bir X.509 sertifikası.
* Bir özel anahtar içerir.
* Anahtar Değişimi (.pfx dosyası) oluşturulur.
* Konu adı hello kullanılan etki alanı tooaccess hello bulut hizmeti eşleşmelidir.

    > Merhaba cloudapp.net için bir SSL sertifikası alınamıyor (veya herhangi bir için Azure ile ilgili) etki alanı; Merhaba sertifikanın konu adı hello özel etki alanı adı kullanılan tooaccess uygulamanızı eşleşmesi gerekir. Örneğin, **contoso.net**değil **contoso.cloudapp.net**.

* En az 2048 bit şifreleme.
* **Hizmet sertifika yalnızca**: istemci-tarafı sertifika hello bulunmalıdır *kişisel* sertifika deposu.

Vardır iki kolay yolları toocreate bir sertifika, Windows hello ile `makecert.exe` yardımcı programı veya IIS.

### <a name="makecertexe"></a>MakeCert.exe
Bu yardımcı program kullanım dışı bırakıldı ve artık aşağıda anlatılmıştır. Daha fazla bilgi için bkz: [bu MSDN makalesine](https://msdn.microsoft.com/library/windows/desktop/aa386968).

### <a name="powershell"></a>PowerShell
```powershell
$cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
$password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
```

> [!NOTE]
> Bir etki alanı yerine IP adresiyle toouse hello sertifika isterseniz, başlangıç IP adresi hello - DnsName parametresinde kullanın.


Bu toouse istiyorsanız [sertifika hello Yönetim Portalı ile](../azure-api-management-certs.md), tooa dışa **.cer** dosyası:

```powershell
Export-Certificate -Type CERT -Cert $cert -FilePath .\my-cert-file.cer
```

### <a name="internet-information-services-iis"></a>Internet Information Services (IIS)
Merhaba üzerinde birden çok sayfa olan kapak Internet nasıl toodo bu IIS ile. [Burada](https://www.sslshopper.com/article-how-to-create-a-self-signed-certificate-in-iis-7.html) harika bir bulunan yeni çalışmaktan de açıklanmaktadır. 

### <a name="java"></a>Java
Java kullanabileceğine[bir sertifika oluşturmak](../app-service-web/java-create-azure-website-using-java-sdk.md#create-a-certificate).

### <a name="linux"></a>Linux
[Bu](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) makalede nasıl toocreate SSH ile sertifikalar.

## <a name="next-steps"></a>Sonraki adımlar
[Hizmet sertifika toohello Klasik Azure portalı karşıya](cloud-services-configure-ssl-certificate.md) (veya hello [Azure portal](cloud-services-configure-ssl-certificate-portal.md)).

Karşıya bir [yönetim API sertifikası](../azure-api-management-certs.md) toohello Klasik Azure portalı. Hello Azure portalı, kimlik doğrulaması için yönetim sertifikaları kullanmaz.

