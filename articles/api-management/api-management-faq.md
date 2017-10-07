---
title: "aaaAzure API Yönetimi SSS | Microsoft Docs"
description: "Merhaba toocommon sorular, desenleri ve en iyi uygulamalar Azure API Management'te yanıtlar hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Azure API Yönetimi SSS
Merhaba yanıtlar toocommon sorular, desenleri ve en iyi uygulamaları için Azure API Management alın.

## <a name="contact-us"></a>Bizimle iletişim kurun
* [Nasıl ı hello Microsoft Azure API Management ekibi bir soru sorabilir miyim?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Sık sorulan sorular
* [Bir özelliğin önizlemede olduğunda ne anlama geliyor?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Merhaba bağlantı hello API Yönetimi ağ geçidi ve arka uç Hizmetlerim arasında nasıl güvenliğini sağlayabilirim?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [My yeni API Management hizmet örneği tooa örneği nasıl kopyalamak?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [My API Management örneği program aracılığıyla yönetebilir miyim?](#can-i-manage-my-api-management-instance-programmatically)
* [Bir kullanıcı toohello Yöneticiler grubunun nasıl eklenir?](#how-do-i-add-a-user-to-the-administrators-group)
* [Neden tooadd hello İlkesi Düzenleyicisi'nde kullanılamaz istiyorum olduğunu hello İlkesi mi?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [API sürümü oluşturma API Management'te nasıl kullanabilirim?](#how-do-i-use-api-versioning-in-api-management)
* [Tek bir API birden çok ortamında nasıl ayarlayabilirim?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [API Management ile SOAP kullanabilir miyim?](#can-i-use-soap-with-api-management)
* [Merhaba API Yönetimi ağ geçidi IP adresi sabit mi? Bu güvenlik duvarı kurallarında kullanabilir miyim?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [Bir OAuth 2.0 yetkilendirme sunucusu ile AD FS güvenliği yapılandırabilir miyim?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Hangi yönlendirme yöntemini API Management dağıtımları toomultiple coğrafi konumlarda kullanıyor mu?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [Azure Resource Manager şablonu toocreate API Management hizmet örneği kullanabilir miyim?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [Otomatik olarak imzalanan bir SSL sertifikası bir arka uç için kullanabilir miyim?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Tooclone bir GIT deposu çalıştığımda neden bir kimlik doğrulama hatası alıyorum?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [API Management Azure ExpressRoute ile çalışır mı?](#does-api-management-work-with-azure-expressroute)
* [Neden API Management içine dağıtıldığında biz sanal ağlar Resource Manager stilde ayrılmış bir alt ağ gerektiriyor mu?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [API Management bir VNET dağıtırken gereken hello en düşük alt ağ boyutu nedir?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [Bir abonelik tooanother bir API Management hizmeti taşıyabilir miyim?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Kısıtlamalar veya my API içeri aktarma bilinen sorunlar vardır?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Nasıl ı hello Microsoft Azure API Management ekibi bir soru sorabilir miyim?
Bize bu seçeneklerden birini kullanarak başvurabilir:

* Sorularınızı sonrası bizim [API Management MSDN Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Bir e-posta çok gönderme<mailto:apimgmt@microsoft.com>.
* Bize hello özellik isteği gönderin [Azure geri bildirim Forumunda](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Bir özelliğin önizlemede olduğunda ne anlama geliyor?
Bir özelliğin önizlemede olduğunda, biz etkin şekilde hello özelliği sizin için nasıl çalıştığını hakkında geri bildirim aramayı olduğunu anlamına gelir. Bir özellik Önizleme'de işlevsel olarak tamamlanır ancak biz yanıt toocustomer geribildirimini değiştirmek sonu hale getireceğiz mümkündür. Üretim ortamınızda önizleme özelliği üzerinde bağlı verme öneririz. Önizleme özelliklerini herhangi bir Geribildiriminiz varsa lütfen aracılığıyla hello kişi seçeneklerinde birini bize [nasıl miyim isteyin hello Microsoft Azure API Management ekibi soru?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Merhaba bağlantı hello API Yönetimi ağ geçidi ve arka uç Hizmetlerim arasında nasıl güvenliğini sağlayabilirim?
Çeşitli seçenekler toosecure hello hello API Yönetimi ağ geçidi ve arka uç hizmetlerini arasında bağlantınız. Şunları yapabilirsiniz:

* HTTP temel kimlik doğrulaması kullanın. Daha fazla bilgi için bkz: [API yapılandırma ayarları](api-management-howto-create-apis.md#configure-api-settings).
* Bölümünde açıklandığı gibi SSL karşılıklı kimlik doğrulaması kullanmak [toosecure arka uç Azure API Management'te istemci sertifikası kimlik doğrulaması kullanarak hizmetleri nasıl](api-management-howto-mutual-certificates.md).
* IP uygulamaları güvenilir listeye almayı arka uç hizmet kullanın. Standart veya Premium katman API Management örneği varsa, başlangıç IP adresi hello ağ geçidinin sabit kalır. Bu IP adresi, beyaz liste tooallow ayarlayabilirsiniz. Başlangıç IP adresi, API Management örneğinin hello Azure portal hello Pano alabilirsiniz.
* API Management örneği tooan Azure Virtual Network bağlayın.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>My yeni API Management hizmet örneği tooa örneği nasıl kopyalamak?
API Management örneği tooa yeni örneği toocopy isterseniz, birkaç seçeneğiniz vardır. Şunları yapabilirsiniz:

* Merhaba yedekleme ve geri yükleme API Management işlevi. Daha fazla bilgi için bkz: [nasıl kullanarak tooimplement olağanüstü durum kurtarma hizmeti yedekleme ve geri yükleme Azure API Management'te](api-management-howto-disaster-recovery-backup-restore.md).
* Kendi yedeği oluşturmak ve hello kullanarak geri yükleme özelliğini [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Merhaba REST API toosave ve istediğiniz hello Hizmet örneğinden hello varlıklar geri yükleme.
* Git kullanarak Hello hizmet yapılandırmasını indirmek ve tooa yeni örnek yükleyin. Daha fazla bilgi için bkz: [nasıl toosave ve Git kullanarak API Management hizmeti yapılandırmanızı yapılandırma](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>My API Management örneği program aracılığıyla yönetebilir miyim?
Evet, kullanarak API Management program aracılığıyla yönetebilirsiniz:

* Merhaba [API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Merhaba [Microsoft Azure ApiManagement Hizmet Yönetimi Kitaplığı SDK](http://aka.ms/apimsdk).
* Merhaba [hizmet dağıtımı](https://msdn.microsoft.com/library/mt619282.aspx) ve [Hizmet Yönetimi](https://msdn.microsoft.com/library/mt613507.aspx) PowerShell cmdlet'leri.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Bir kullanıcı toohello Yöneticiler grubunun nasıl eklenir?
Bir kullanıcı toohello Yöneticiler grubu eklemek için ne aşağıda verilmiştir:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tooupdate istediğiniz hello API Management örneği olan toohello kaynak grubuna gidin.
3. API Yönetimi'nde hello atamak **API Management katkıda bulunan** rol toohello kullanıcı.

Katkıda bulunan Azure PowerShell kullanma Hello yeni eklenen artık [cmdlet'leri](https://msdn.microsoft.com/library/mt613507.aspx). İşte nasıl içinde toosign yönetici olarak:

1. Kullanım hello `Login-AzureRmAccount` cmdlet toosign.
2. Ayarlama kullanarak hello hizmetine sahip hello bağlam toohello abonelik `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Kullanarak tek bir oturum açma URL'sini alma `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Merhaba URL tooaccess hello Yönetici portalı kullanın.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Neden tooadd hello İlkesi Düzenleyicisi'nde kullanılamaz istiyorum olduğunu hello İlkesi mi?
Tooadd görünür istediğiniz hello İlkesi soluk veya hello İlkesi Düzenleyicisi'nde gölgeli hello ilkesi için doğru hello kapsamında olduğundan emin olun. Her ilke bildirimi, toouse belirli kapsamlar ve ilke bölümlerindeki için tasarlanmıştır. tooreview hello İlkesi bölüm ve bir ilke kapsamları Bkz hello İlkesi'nin kullanım bölümüne [API Management ilkeleri](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>API sürümü oluşturma API Management'te nasıl kullanabilirim?
API Management'te birkaç seçenekleri toouse API sürüm vardır:

* API Management'te API'leri toorepresent farklı sürümlerini yapılandırabilirsiniz. Örneğin, iki farklı API'leri, MyAPIv1 ve MyAPIv2 olabilir. Bir geliştirici, geliştirici hello hello sürüm toouse istediği seçebilirsiniz.
* API'nizi sürüm segment, örneğin, https://my.api içermeyen bir hizmet URL'si ile de yapılandırabilirsiniz. Ardından, her işlemin üzerinde bir sürümü kesimi yapılandırmak [URL yeniden yazma](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) şablonu. Örneğin, bir işlem olabilir bir [URL şablonu](api-management-howto-add-operations.md#url-template) /Resource çağrılır ve bir [URL yeniden yazma](api-management-howto-add-operations.md#rewrite-url-template) şablonu adlı/v1/kaynak. Her işlem için ayrı ayrı hello sürüm kesim değeri değiştirebilirsiniz.
* Tookeep isterseniz seçili işlemlerini hello API'nin hizmeti URL'si "varsayılan" sürüm kesimdeki hello kullanan bir ilke kümesi [ayarlamak arka uç hizmetini](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) İlkesi toochange hello arka uç istek yolu.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Tek bir API birden çok ortamında nasıl ayarlayabilirim?
tooset Örneğin, bir test ortamı ve bir üretim ortamında tek bir API birden çok ortamı kurmak için iki seçeneğiniz vardır. Şunları yapabilirsiniz:

* Konak farklı API'leri aynı Kiracı hello.
* Konak farklı kiracıların aynı API'leri hello.

### <a name="can-i-use-soap-with-api-management"></a>API Management ile SOAP kullanabilir miyim?
[SOAP doğrudan](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/) desteği artık kullanılabilir durumdadır. Yöneticiler hello kendi SOAP hizmetinin WSDL içe aktarabilir ve Azure API Management SOAP ön uç oluşturur. Geliştirici portal belgeleri, test konsol, ilkeleri ve analizi SOAP Hizmetleri için kullanılabilir.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>Merhaba API Yönetimi ağ geçidi IP adresi sabit mi? Bu güvenlik duvarı kurallarında kullanabilir miyim?
Merhaba standart ve Premium Katmanlar hello genel IP adresi (VIP) hello API Management Kiracı bazı istisnalar hello Kiracı hello ömrü statik içindir. Bu durumlarda Hello IP adresi değişiklikleri:

* Merhaba hizmet silinir ve yeniden oluşturulacak.
* Merhaba hizmet aboneliği [askıya](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) veya [uyarı](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (örneğin, nonpayment) ve ardından reinstated.
* Eklediğiniz veya kaldırdığınız Azure sanal ağ (sanal ağ yalnızca hello Geliştirici ve Premium katmanı kullanabilirsiniz).

Merhaba bölge vacated ve ardından reinstated bölgeli dağıtımlar için bölgesel adresi değişiklikleri hello (yalnızca hello Premium katmanı çok bölge dağıtımı kullanabilirsiniz).

Bölgeli dağıtımı için yapılandırılmış premium katmanı kiracılar her bölge bir genel IP adresi atanır.

Hello Azure portal'hello Kiracı sayfasında, IP adresi (veya adresleri, bölgeli dağıtım) alabilirsiniz.

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>Bir OAuth 2.0 yetkilendirme sunucusu ile AD FS güvenliği yapılandırabilir miyim?
nasıl tooconfigure bir OAuth 2.0 yetkilendirme sunucusu Active Directory Federasyon Hizmetleri (AD FS) güvenlik, bkz: toolearn [kullanarak ADFS API Management](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Hangi yönlendirme yöntemini API Management dağıtımları toomultiple coğrafi konumlarda kullanıyor mu?
API Management kullanır hello [performans trafik yönlendirme yöntemini](../traffic-manager/traffic-manager-routing-methods.md#priority) dağıtımları toomultiple coğrafi konumlarda. Yönlendirilmiş toohello yakın API ağ geçidi gelen trafiğidir. Bir bölge çevrimdışı olursa, gelen trafiği otomatik olarak yönlendirilmiş toohello sonraki en yakın ağ geçididir. Yönlendirme yöntemleri hakkında daha fazla bilgi [Traffic Manager yönlendirme yöntemleri](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>Azure Resource Manager şablonu toocreate API Management hizmet örneği kullanabilir miyim?
Evet. Merhaba bkz [Azure API Management hizmeti](http://aka.ms/apimtemplate) hızlı başlangıç şablonları.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>Otomatik olarak imzalanan bir SSL sertifikası bir arka uç için kullanabilir miyim?
Evet. Nasıl toouse otomatik olarak imzalanan bir Güvenli Yuva Katmanı (SSL) sertifikası için bir arka uç aşağıda verilmiştir:

1. Oluşturma bir [arka uç](https://msdn.microsoft.com/library/azure/dn935030.aspx) API Management kullanarak varlık.
2. Set hello **skipCertificateChainValidation** özelliği çok**doğru**.
3. Tooallow otomatik olarak imzalanan sertifikalar artık istemiyorsanız hello arka uç varlığı silme veya ayarlayın hello **skipCertificateChainValidation** özelliği çok**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Tooclone bir Git deposu çalıştığımda neden bir kimlik doğrulama hatası alıyorum?
Git kimlik bilgisi Yöneticisi'ni kullanın ya da Visual Studio kullanarak tooclone bir Git deposu çalışıyorsanız, bilinen bir sorun hello Windows kimlik bilgileri iletişim kutusu içine çalışabilir. parola uzunluğu too127 karakter Hello iletişim kutusu sınırlar ve hello Microsoft tarafından oluşturulan parola tamsayıya dönüştürür. Merhaba parola kısaltmayı üzerinde çalışıyoruz. Şu an için lütfen Git deponuzu Git Bash tooclone kullanın.

### <a name="does-api-management-work-with-azure-expressroute"></a>API Management Azure ExpressRoute ile çalışır mı?
Evet. API Management Azure ExpressRoute ile çalışır.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Neden API Management içine dağıtıldığında biz sanal ağlar Resource Manager stilde ayrılmış bir alt ağ gerektiriyor mu?
API Management Hello ayrılmış bir alt ağ gereksinimini (PAAS V1 katman) Klasik dağıtım modelinde oluşturulmuş hello olgu, gelir. Resource Manager VNET'i (V2 katman) dağıtabilmeniz için olsa da, sonuçları toothat vardır. Merhaba V2 katmanında bir kaynak oluşturursanız, Azure Klasik dağıtım modelinde sıkı bir şekilde hello Resource Manager modeli ve bunu eşleşmediğinden, hello V1 katman hakkında bilmiyor ve sorunları oluşabilir, önceden ayrılmış bir IP toouse çalışırken API Management gibi tooa NIC (V2 üzerinde oluşturulur).
Azure Klasik ve Resource Manager modellerin fark hakkında daha fazla başvurmak çok toolearn[dağıtım modelleri arasında fark](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>API Management bir VNET dağıtırken gereken hello en düşük alt ağ boyutu nedir?
Merhaba en düşük alt ağ boyutunu gereken API Yönetimi toodeploy [/29](../virtual-network/virtual-networks-faq.md#configuration), Azure destekleyen hello en düşük alt ağ boyutunu olduğu.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>Bir abonelik tooanother bir API Management hizmeti taşıyabilir miyim?
Evet. toolearn nasıl bkz [kaynakları tooa yeni kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Kısıtlamalar veya my API içeri aktarma bilinen sorunlar vardır?
[Bilinen sorunlar ve kısıtlamalar](api-management-api-import-restrictions.md) açık API(Swagger) için WSDL ve WADL biçimlendirir.
