---
title: "Azure RemoteApp bulut koleksiyonu oluşturma | Microsoft Docs"
description: "Verileri Azure bulutunda kaydeder Azure RemoteApp dağıtımı oluşturmayı öğrenin."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 52d5a073c0de42a77cd7163bf402ed2cdf598d95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-cloud-collection-of-azure-remoteapp"></a>Azure RemoteApp bulut koleksiyonu oluşturma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

İki tür [Azure RemoteApp koleksiyonu](remoteapp-collections.md) vardır: 

* Bulut: tamamen Azure'da yer alıyor. Tüm verileri bulutta kaydetmeyi seçebilirsiniz (şekilde bir yalnızca bulut koleksiyonu) veya koleksiyonunuz bir VNET'e bağlayın ve oradaki verileri kaydetmek için.   
* Karma: bir sanal ağ içeren şirket içi erişim için - bu kullanım Azure ad ve şirket içi Active Directory ortamında gerektirir.

Bu öğretici bir bulut koleksiyonu oluşturma işleminde size kılavuzluk eder. Dört adım vardır: 

1. Bir Azure RemoteApp koleksiyonu oluşturun.
2. İsteğe bağlı olarak dizin eşitlemesini yapılandırın. Azure AD kullanıyorsanız + Active Directory sahip kullanıcılar, kişiler ve parolaların şirket içi Active directory'nizden Azure AD kiracınıza eşitlemek.
3. Uygulama yayımlama.
4. Kullanıcı erişimi yapılandırın.

**Başlamadan önce**

Koleksiyon oluşturmadan önce aşağıdakileri yapmanız gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp için. 
* Erişim vermek istediğiniz kullanıcıları hakkında bilgi toplayın. Bu, Microsoft hesap bilgileri veya kullanıcılar için Active Directory iş hesabı bilgileri olabilir.
* Bu yordam, ya da aboneliğinizin bir parçası olarak sağlanan şablonu görüntülerden birini kullanacağınız veya zaten sahip kullanmak istediğiniz şablon görüntüsü karşıya varsayar. Farklı bir şablon görüntü karşıya yüklemek ihtiyacınız varsa, şablon görüntüleri sayfasından yapabilirsiniz. Tıklatmanız **şablon görüntüsü karşıya** ve sihirbazdaki adımları izleyin. 
* Office 365 ProPlus görüntüsünü kullanmak istediğiniz? Bilgileri inceleyin [burada](remoteapp-officesubscription.md).
* Özel uygulamalar veya programlar LOB istiyorsunuz? Yeni bir [görüntü](remoteapp-imageoptions.md) ve bulut koleksiyonunuzda kullanın.
* Bir sanal AĞA bağlanmak gereken çıkışı şekil. Bir sanal AĞA bağlanmak seçerseniz, karşıladığından emin olun [yönergeleri boyutlandırma](remoteapp-vnetsizing.md) ve [RemoteApp'e bağlanmak](remoteapp-vnet.md). Kullanıma [VNET planlama makale ](remoteapp-planvnet.md)daha fazla bilgi için.
* VNET kullanıyorsanız, yerel Active Directory etki alanınıza ekleyin istediğinize karar verin.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>1. adım: Bulut koleksiyonu - olan veya olmayan bir sanal ağ oluşturma
Aşağıdaki adımları kullanın **bir yalnızca bulut koleksiyonu oluşturma**:

1. Yönetim Portalı'nda RemoteApp sayfasına gidin.
2. Tıklatın **yeni > Hızlı Oluştur**.
3. Koleksiyonunuz için bir ad girin ve bölgenizi seçin.
4. -Standart ya da temel kullanmak istediğiniz planı seçin.
5. Bu koleksiyon için kullanılacak şablonu seçin. 
   
    **İpucu:** aboneliğiniz RemoteApp için birlikte [şablon görüntüleri](remoteapp-images.md) Office 365 veya Office 2013 (deneme kullanımı için) programları, (Word gibi) bazı yayımlanan içeren ve diğerleri yayımlamak için hazır. Ayrıca, yeni bir oluşturabilirsiniz [görüntü](remoteapp-imageoptions.md) ve bulut koleksiyonunuzda kullanın.
6. Tıklatın **oluşturma RemoteApp koleksiyonu**.
   
    **Önemli:** koleksiyonunuzu sağlanması 30 dakika sürebilir.

Azure RemoteApp koleksiyonunuzun oluşturulduktan sonra koleksiyon adına çift tıklayın. Getirecek **Hızlı Başlangıç** sayfası - burada koleksiyonu yapılandırmayı tamamlamak budur.

Oluşturmak için aşağıdaki adımları kullanın bir **bulut + VNET koleksiyonu**:

1. Yönetim Portalı'nda Azure RemoteApp sayfasına gidin.
2. Tıklatın **yeni** > **ile VNET oluşturma**.
3. Koleksiyonunuz için bir ad girin.
4. -Standart ya da temel kullanmak istediğiniz planı seçin.
5. Önceden oluşturulmuş sanal ağ seçin. Bunun nasıl yapılacağını bilmiyorsanız? Şu an için adımları bulunan [karma](remoteapp-create-hybrid-deployment.md) konu.
6. Koleksiyonunuz etki alanınıza ekleyin istediğinize karar verin. Yanıt Evet ise, Azure AD tümleştirmek için AD Connect kullanmanız gerekir ve Active Directory ortamınızı. Kapsanan olarak aşağıda içinde **2. adım**.
7. Tıklatın **oluşturma RemoteApp koleksiyonu**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>2. adım: Active Directory dizin eşitleme (isteğe bağlı) yapılandırma
Active Directory kullanmak istiyorsanız, Azure RemoteApp kullanıcılar, kişiler ve parolalar Azure Active Directory kiracınıza eşitlemek için Azure Active Directory ve şirket içi Active Directory arasında dizin eşitlemesi gerektirir. Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) planlama bilgileri için. De doğrudan gidebilirsiniz [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) bilgi.

## <a name="step-3-publish-apps"></a>3. adım: uygulama yayımlama
Bir Azure RemoteApp uygulama veya Kullanıcılarınıza sağladığınız programı uygulamadır. Koleksiyon için karşıya şablon görüntüsü bulunur. Bir kullanıcı bir uygulama eriştiğinde, yerel ortamlarında çalıştırmak için uygulamayı görünür, ancak gerçekten, azure'da sanal makine çalışıyor. 

Kullanıcılarınızın uygulamaları erişebilmeniz için önce bunları yayımlamanız gerekir – uygulamaları sağlar yayımlama kullanıcılarınızın uygulamaları Uzak Masaüstü istemcisi üzerinden erişim.

Azure RemoteApp koleksiyonunuzun birden fazla uygulama yayımlayabilirsiniz. Yayımlama sayfasından tıklatın **Yayımla** bir program eklemek için. Gelen ya da yayımlayabilirsiniz **Başlat** menü şablon görüntüsünün veya uygulama için şablon görüntüsü üzerinde yolunu belirterek. Ekleme seçerseniz **Başlat** menüsünde yayımlamak için uygulamayı seçin. Uygulamanın yolunu sağlamak seçerseniz, uygulama ve şablon görüntüsü yüklendiği yolu için bir ad sağlayın.

## <a name="step-4-configure-user-access"></a>4. adım: kullanıcı erişimini yapılandırma
Koleksiyonunuz oluşturduğunuza göre uzak kaynaklar kullanabilmek için istediğiniz kullanıcıları eklemeniz gerekir. Active Directory kullanıyorsanız, abonelikle ilişkili Active Directory Kiracı mevcut gerek erişebilmesi kullanıcılar, bu koleksiyonu oluşturmak için kullanılır.

1. Hızlı başlangıç sayfasından tıklatın **kullanıcı erişimini yapılandırma**. 
2. İçin erişim vermek istediğiniz iş hesabını (Active Directory) veya Microsoft hesabını girin.
   
   **Notlar:** 
   
   Kullandığınızdan emin olun  *user@domain.com*  biçimi.
   
   Office 365 ProPlus koleksiyonunuzda kullanıyorsanız, kullanıcılarınız için Active Directory kimlikleri kullanmanız gerekir. Bu lisans doğrulama yardımcı olur. 
3. Kullanıcıların doğrulandıktan sonra tıklatın **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar - başarıyla oluşturulan ve dağıtılan Azure RemoteApp bulut koleksiyonu. Sonraki adım, uzak masaüstü istemcisini yükleyip, kullanıcılarınızın sağlamaktır. Azure RemoteApp hızlı başlangıç sayfasında istemcinin URL bulabilirsiniz. Ardından, kullanıcıların oturum istemci uygulamasına sahip ve, yayımlanan uygulamalara erişim.

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Bu makaleyi derecelendirmenin ve aşağıda yorum yapmamanın yanı sıra makalede değişiklik de yapabileceğinizi biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Değişiklik yapmak için yukarı doğru ilerleyin ve **GitHub üzerinde düzenle**’ye tıklayın; bu değişiklikler incelenmek üzere bize gönderilir ve kabul edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada görünür.

