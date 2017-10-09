---
title: "aaaCreate ve Azure portalı panoları paylaşmak | Microsoft Docs"
description: "Bu makalede, Azure portalını nasıl toocreate ve düzenleme panolarında hello açıklanmaktadır."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 0facd10fe3284d7ad9a9e29791e5af5b5b95c97f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-share-dashboards-in-hello-azure-portal"></a>Oluşturma ve hello Azure portal panolarında paylaşma
Birden çok panolar oluşturun ve erişim tooyour Azure sahip başkalarıyla paylaşmadan abonelikleri.  Bu makalede oluşturma, düzenleme, yayımlama ve yönetme erişimi toodashboards hello temelleri gider.

## <a name="create-a-dashboard"></a>Bir pano oluşturun
toocreate bir Pano seçin hello **yeni Pano** sonraki toohello geçerli Pano kişinin adı düğmesine tıklayın.  

![bir pano oluşturun](./media/azure-portal-dashboards/new-dashboard.png)

Bu eylem, yeni, boş, özel bir Pano oluşturur ve burada panonuzu adlandırın ve ekleyebilir veya kutucukları yeniden özelleştirme moduna geçirir.  Bu modda, hello daraltılabilir parçasında galeri alır hello sol gezinti menüsü.  Merhaba döşeme galeri Azure kaynaklarınızın çeşitli şekillerde döşeme bulmanıza olanak sağlar: tarafından göz atabilirsiniz [kaynak grubu](../azure-resource-manager/resource-group-overview.md#resource-groups), göre kaynak türü, göre [etiketi](../azure-resource-manager/resource-group-using-tags.md), ya da kaynak ada göre arayarak.  

![Pano özelleştirme](./media/azure-portal-dashboards/customize-dashboard.png)

Döşeme sürükleyip istediğiniz yere hello Pano yüzeyine bırakarak ekleyin.

Yeni bir kategori yok **genel** belirli bir kaynakla ilişkili olmayan kutucuklar için.  Bu örnekte, hello Markdown kutucuğu sabitleyin.  Bu kutucuğu tooadd özel içerik tooyour panoyu kullanın.  Merhaba döşeme destekleyen düz metin [Markdown söz dizimi](https://daringfireball.net/projects/markdown/syntax)ve HTML sınırlı sayıda.  (Güvenlik için ekleme gibi işlemler yapamayacağı `<script>` etiketler veya belirli hello portalıyla engelleyebilmesi CSS stil öğesi kullanın.) 

![markdown Ekle](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a>Bir Pano Düzenle
Panonuz oluşturduktan sonra kutucukları hello döşeme galeri veya hello döşeme Kanatlar gösterimini sabitleyebilirsiniz. Şimdi, kaynak grubu hello gösterimini sabitleyin. Öğe veya hello kaynak grubu dikey hello göz atarken ya da sabitleyebilirsiniz. Her iki yaklaşımın hello döşeme hello kaynak grubu gösterimini sabitleme neden.

![PIN toodashboard](./media/azure-portal-dashboards/pin-to-dashboard.png)

Merhaba öğeyi sabitleme sonra Panonuzda görüntülenir.

![Görünüm Panosu](./media/azure-portal-dashboards/view-dashboard.png)

Bir Markdown kutucuk ve bir kaynak grubu sabitlenmiş toohello Panosu sahibiz, biz yeniden boyutlandırma ve uygun bir düzen hello kutucukları yeniden.

Vurgulama ve seçerek "..." veya bir kutucuğa sağ tıklayarak bu döşeme için tüm hello bağlamsal komutları görebilirsiniz. Varsayılan olarak, iki öğe vardır:

1. **Panodan sabitleme** – hello panosundan kaldırır hello döşeme
2. **Özelleştirme** – girer modu özelleştirme

![Döşeme özelleştirme](./media/azure-portal-dashboards/customize-tile.png)

Seçerek özelleştirme, yeniden boyutlandırma ve kutucukları yeniden Sırala. tooresize kutucuğu, select hello görüntü aşağıdaki gösterildiği gibi hello bağlam menüsünden Yeni boyutunu hello.

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-tile.png)

Veya herhangi bir boyutta hello döşeme destekliyorsa, hello alt sağ köşesinde toohello istenen boyutu sürükleyebilirsiniz.

![Döşeme yeniden boyutlandırma](./media/azure-portal-dashboards/resize-corner.png)

Kutucukları yeniden boyutlandırma sonra hello Pano görüntüleyin.

![Görünümü kutucuğu](./media/azure-portal-dashboards/view-tile.png)

Bir Pano özelleştirme bittiğinde, hello seçmeniz yeterlidir **özelleştirme Bitti** tooexit özelleştirme modu veya sağ tıklatın ve seçin **özelleştirme Bitti** hello bağlam menüsünden.

## <a name="publish-a-dashboard-and-manage-access-control"></a>Bir Pano yayımlayın ve erişim denetimi yönetin
Bir Pano oluşturduğunuzda, görebileceğiniz tek kişi hello olduğu anlamına gelir varsayılan olarak özeldir.  toomake onu görünen tooothers hello kullanın **paylaşımı** yanında görüntülenen düğmesini hello diğer Pano komutları.

![Pano paylaşımı](./media/azure-portal-dashboards/share-dashboard.png)

Bir abonelik ve kaynak grubu, Pano toobe için yayımlanan toochoose istenir. tooseamlessly hello ekosistemi panolar tümleştirmek, (size bir e-posta adresi yazarak paylaşamaz şekilde) paylaşılan panoları Azure kaynaklarını uyguladık.  Çoğu hello döşeme hello portalında tarafından görüntülenen erişim toohello bilgileri tarafından yönetilir [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md). Bir erişim denetimi açısından bakıldığında, paylaşılan Pano sanal makine ya da bir depolama hesabı hiç farklı değildir.  

Bir Azure aboneliğiniz varsa ve ekibinizin üyeleri hello rolleri atanmış düşünelim **sahibi**, **katkıda bulunan**, veya **okuyucu** hello abonelik.  Sahipler veya katkıda bulunanlar kullanıcılar mümkün toolist, görünüm olan, oluşturmak, değiştirmek veya bu abonelik içindeki panoları silin.  Okuyucular kullanıcılar mümkün toolist ve görünüm panolar, ancak değiştirin veya silin.  Okuyucu erişimi olan kullanıcılar mümkün toomake yerel düzenlemeleri tooa paylaşılan Pano, ancak şu toopublish bu değişiklikleri geri toohello sunucu.  Ancak, bunlar hello panonun kendi kullanmak için özel bir kopyasını yapabilirsiniz.  Her zaman olduğu gibi tek tek döşeme hello Panoda için karşılık gelen hello kaynaklara göre kendi erişim denetim kurallarını uygulayın.  

Kolaylık olması için bir kaynak grubunda panolar nereye bir desen doğrultusunda aradığınız deneyimi kılavuzları hello portalını yayımlama **panolar**.  

![Pano yayımlama](./media/azure-portal-dashboards/publish-dashboard.png)

Ayrıca, Pano tooa belirli bir kaynak grubunu toopublish tercih edebilirsiniz.  Bu Pano için Hello erişim denetimi hello kaynak grubu için hello erişim denetimi ile eşleşir.  Kaynak grubunda hello kaynakları yönetebilir kullanıcılar toohello mimarilere de.

![Pano tooresource Grup yayımlama](./media/azure-portal-dashboards/publish-to-resource-group.png)

Panonuz yayımlandıktan sonra hello **paylaşım + erişim** denetim bölmesinde yenileyin ve bir bağlantı toomanage kullanıcı erişimi toohello panosu da dahil olmak üzere hello yayımlanan Pano hakkında bilgi gösterir.  Bu bağlantıyı hello standart rol tabanlı erişim denetimi kullanılan dikey toomanage erişim herhangi bir Azure kaynağı için başlatır.  Her zaman geri toothis görünümü seçerek alabilirsiniz **paylaşımı**.

![erişim denetimi yönetme](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a>Sonraki adımlar
* toomanage kaynaklara bakın [yönetmek Azure kaynakları portal üzerinden](../azure-resource-manager/resource-group-portal.md).
* toodeploy kaynaklara bakın [kaynakları Resource Manager şablonları ve Azure portalı ile dağıtma](../azure-resource-manager/resource-group-template-deploy-portal.md).

