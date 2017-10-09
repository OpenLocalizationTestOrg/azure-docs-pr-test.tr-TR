---
title: "aaaConfigure bildirimleri ve e-posta şablonları Azure API Management | Microsoft Docs"
description: "Bilgi nasıl tooconfigure bildirimleri ve e-posta şablonları Azure API Management'te."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Nasıl tooconfigure bildirimleri ve e-posta Azure API Management şablonları
API Management tooconfigure bildirimleri belirli olayları ve hello Yöneticiler ve geliştiriciler API Management örneği ile kullanılan toocommunicate tooconfigure hello e-posta şablonları için hello yeteneği sağlar. Bu konu, tooconfigure bildirimleri için kullanılabilir olayları nasıl hello gösterir ve bu olaylar için kullanılan hello e-posta şablonlarını yapılandırma genel bir bakış sağlar.

## <a name="publisher-notifications"></a>Yayımcı bildirimleri yapılandırma
tooconfigure bildirimleri tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

![Yayımcı portalı][api-management-management-console]

> [!NOTE] 
> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.

Tıklatın **bildirimleri** hello gelen **API Management** hello menüsünde sol tooview hello kullanılabilir bildirim.

![Yayımcı bildirimleri][api-management-publisher-notifications]

Merhaba aşağıdaki olaylar listesi bildirimleri için yapılandırılabilir.

* **(Onay gerektiren) abonelik istekler** - belirtilen e-posta alıcılarını hello ve kullanıcıların onay gerektiren API ürünleri için abonelik isteklerini hakkında e-posta bildirimleri alır.
* **Yeni abonelikler** - belirtilen e-posta alıcılarını hello ve kullanıcıların yeni API ürün abonelikleri hakkında e-posta bildirimleri alır.
* **Uygulama Galerisi isteklerini** - belirtilen e-posta alıcılarını hello ve yeni uygulamalar gönderilen toohello uygulama Galerisi olduğunda kullanıcıların e-posta bildirimleri alır.
* **Gizli** - belirtilen e-posta alıcılarını hello ve kullanıcıların e-posta gizli kopya tüm gönderilen e-postaların toodevelopers olarak alır.
* **Yeni bir sorun veya yorum** - belirtilen e-posta alıcılarını hello ve kullanıcıların, yeni bir sorun olduğunda e-posta bildirimlerini alacak veya yorum hello Geliştirici portalında gönderildi.
* **Hesabı Kapat iletisi** - belirtilen e-posta alıcılarını hello ve kullanıcıların bir hesap kapalı olduğunda e-posta bildirimleri alır.
* **Yaklaşan abonelik kota sınırına** - e-posta alıcılarını aşağıdaki hello ve abonelik kullanım Kapat toousage kota aldığında kullanıcıların e-posta bildirimleri alır.

Her olay için hello e-posta adresi metin kutusunu kullanarak e-posta alıcılarını belirtebilirsiniz veya kullanıcıların bir listeden seçebilirsiniz.

bildirim, toospecify hello e-posta adresleri toobe girin bunları hello e-posta adresi metin kutusuna. Birden çok e-posta adresi varsa, bunları ayrı virgülle ayırın.

![Bildirim alıcılarını][api-management-email-addresses]

bildirim, toospecify hello kullanıcılar toobe tıklatın **alıcı ekleyin**hello bildirim hello kullanıcılar toobe yanındaki kutuyu ve tıklatın **Tamam**.

> [!NOTE] 
> Yalnızca Yöneticiler hello listesinde görüntülenir.


Merhaba bildirim alıcılarını yapılandırdıktan sonra tıklatın **kaydetmek** tooapply hello bildirim alıcılarını güncelleştirildi.

> [!NOTE] 
> Merhaba çıktığınızda giderseniz **yayımcı bildirimleri** sekmesini hello yayımcı portalı, kaydedilmemiş değişiklikler var. olursa uyarıları.


## <a name="email-templates"></a>E-posta şablonlarını yapılandırma
API Management e-posta şablonlarını yönetme ve hello hizmetini kullanarak hello indirmelere içinde gönderilen e-posta iletilerini Merhaba sağlar. e-posta şablonlarını aşağıdaki hello sağlanır.

* Onaylanan uygulama Galerisi gönderme
* Geliştirici diğer harf
* Bildirim yaklaşan Geliştirici kota sınırı
* Kullanıcı Davet Et
* Yeni Yorum tooan sorunu eklendi
* Alınan yeni sorun
* Yeni Abonelik etkinleştirildi
* Yenilenen abonelik onayı
* Abonelik isteği reddettiğinde
* Abonelik isteği alındı

Bu şablonlar değiştirilebilir istenen şekilde.

tooview ve hello e-posta şablonlarını API Management Örneğiniz için yapılandırmak için tıklayın **bildirimleri** hello gelen **API Management** sol hello ve select hello menüsünde **e-posta şablonları**  sekmesi.

![E-posta şablonları][api-management-email-templates]

tooview veya belirli bir şablon Değiştir, hello seçin **şablonları** aşağı açılan liste.

![E-posta şablonları listesi][api-management-email-templates-list]

Düz metin biçiminde bir konu ve gövde tanımı'nda HTML biçiminde her e-posta şablonu yok. Her öğe özelleştirilebilir istenen şekilde.

![E-posta şablonu Düzenleyicisi][api-management-email-template]

Merhaba **parametreleri** listesini içeren bir liste parametrelerden biri, hangi olduğunda hello konusu ya da gövdesi eklenen, hello e-posta gönderildiğinde değiştirilen hello atanan değer olacaktır. bir parametre tooinsert burada hello parametresi toogo istiyor ve hello parametre adının hello ok toohello sol tıklayın hello imleç yerleştirin.

Tıklatın **Önizleme** veya **bir sınama Gönder** toosee nasıl hello e-posta arayın veya bir test e-posta gönderin.

> [!NOTE] 
> Merhaba parametreleri önizleme ya da bir test gönderme gerçek değerlerle değiştirilmez.

toosave hello değişiklikleri toohello e-posta şablonu, tıklatın **kaydetmek**, veya toocancel hello değişiklikleri **iptal**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
