---
title: "Azure API Management'te grupları kullanarak aaaManage Geliştirici hesapları | Microsoft Docs"
description: "Nasıl toomanage Geliştirici kullanarak hesapları öğrenin Azure API Management'te grupları"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Azure API Management'te nasıl toocreate ve kullanım grupları toomanage Geliştirici hesapları
API Management'te, ürünlerin toodevelopers kullanılan toomanage hello görünürlüğünü gruplarıdır. İlk yapılan görünür toogroups ürünleri olan ve sonra bu gruplara geliştiriciler görüntülemek ve hello gruplarıyla ilişkili toohello ürünleri abone. 

API Management aşağıdaki sabit sistem gruplarına hello sahiptir.

* **Yöneticiler**: Azure aboneliği yöneticileri bu grubun üyesidir. Yöneticiler API Management hizmet örneklerini yönetir API'leri, işlemleri ve geliştiriciler tarafından kullanılan ürünleri hello oluşturma.
* **Geliştiriciler**: Kimliği doğrulanmış geliştirici portalı kullanıcıları bu gruba girer. Geliştiriciler, Apı'lerinizi kullanan uygulamalar oluşturmak hello müşterilerdir. Geliştiriciler erişim toohello Geliştirici Portalı verilir ve hello bir API'nin işlemlerini çağıran uygulamalar oluşturun.
* **Konuklar** -kimliği doğrulanmamış Geliştirici portalı kullanıcıları, bu gruba bir API Management örneği sonbaharda hello Geliştirici portalını ziyaret eden olası müşteriler gibi. Bunlar hello özelliği tooview API'leri gibi bazı salt okunur erişim hakkı verilebilir, ancak çağıramama.

Toplama toothese sistem gruplarında yöneticiler özel gruplar oluşturabilir veya [ilişkili Azure Active Directory kiracılarındaki dış grupları yararlanan][leverage external groups in associated Azure Active Directory tenants]. Özel ve dış gruplar tooAPI ürünleri erişmek ve geliştiricilere görünürlük vererek sistem grupları yanında kullanılabilir. Örneğin, özel bir grup oluşturmak için belirli bir ile ilişkili Geliştiriciler iş ortağı kuruluş ve erişim izni yalnızca ilgili API'leri içeren bir üründen toohello API'leri. Bir kullanıcı birden fazla grubun üyesi olabilir.

Bu kılavuz, nasıl bir API Management örneğinin yöneticileri yeni gruplar eklemek ve ürünleri ve geliştiricilerin ilişkilendirmek gösterir.

> [!NOTE]
> Ayrıca toocreating ve hello yayımcı portalında gruplarını yönetme, oluşturabilir ve gruplarınızı hello API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.
> 
> 

## <a name="create-group"></a>Bir grup oluşturun
toocreate yeni bir grubu tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda. Bu toohello API Management yayımcı portalına götürür.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklatın **grupları** hello gelen **API Management** sol hello ve ardından menüsünde **Grup Ekle**.

![Yeni Grup Ekle][api-management-add-group]

Merhaba grubu ve isteğe bağlı bir açıklama için benzersiz bir ad girin ve tıklayın **kaydetmek**.

![Yeni Grup Ekle][api-management-add-group-window]

Merhaba yeni Grup hello grupları sekmesini tooedit hello görüntülenen **adı** veya **açıklama** hello grubunun hello hello listedeki hello grup adını tıklatın. toodelete hello grubu tıklatın **silmek**.

![Eklenen grubu][api-management-new-group]

Merhaba grup oluşturulur, ürünleri ve geliştiriciler ile ilişkili olabilir.

## <a name="associate-group-product"></a>Bir grup ürünü ile ilişkilendirme
tooassociate bir ürüne sahip bir grubu tıklatın **ürünleri** hello gelen **API Management** hello menüsünde sol ve ardından hello istenen ürün hello adına tıklayın.

![Görünürlüğü Ayarla][api-management-add-group-to-product]

Select hello **görünürlük** tooadd sekmesinde ve grupları ve hello ürünün tooview hello geçerli grupları kaldırın. tooadd veya kaldırma grupları denetleyin veya grupları ve tıklatın hello istenen için hello onay kutusunun işaretini kaldırın **kaydetmek**.

![Görünürlüğü Ayarla][api-management-add-group-to-product-visibility]

> [!NOTE]
> bkz: tooadd Azure Active Directory grupları [nasıl tooauthorize Geliştirici kullanarak hesapları Azure API Management'te Azure Active Directory](api-management-howto-aad.md).
> 
> Merhaba tooconfigure gruplarından **görünürlük** bir ürün sekmesini tıklatın, **grupları yönet**.
> 
> 

Bir ürün grubu ile ilişkili olduğunda, o gruptaki geliştiriciler görüntüleyebilir ve toohello ürün abone.

## <a name="associate-group-developer"></a>Grupları geliştiricilerle ilişkilendirme
Geliştiriciler ile tooassociate gruplar **kullanıcılar** hello gelen **API Management** sol hello ve hello geliştiriciler yanındaki kutuyu hello menüsünden istediğiniz tooassociate sahip bir grup.

![Geliştirici toogroup Ekle][api-management-add-group-to-developer]

Geliştiriciler denetlenir Hello istenen sonra hello istenen hello grubunda tıklayın **tooGroup ekleme** açılır. Geliştiriciler kaldırılabilir gruplarından hello kullanarak **grubundan** açılır. 

![Geliştiriciler][api-management-add-group-to-developer-saved]

Merhaba ilişkilendirme hello Geliştirici ve hello grubu arasında eklendikten sonra hello görüntüleyebilirsiniz **kullanıcılar** sekmesi.

## <a name="next-steps"> </a>Sonraki adımlar
* Bir geliştirici tooa grubuna eklendikten sonra görüntüleyin ve bu grupla ilişkili toohello ürünleri abone olun. Daha fazla bilgi için bkz: [oluşturma ve Azure API Management'te bir ürün yayımlama][How create and publish a product in Azure API Management],
* Ayrıca toocreating ve hello yayımcı portalında gruplarını yönetme, oluşturabilir ve gruplarınızı hello API Management REST API kullanarak yönetmek [grup](https://msdn.microsoft.com/library/azure/dn776329.aspx) varlık.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
