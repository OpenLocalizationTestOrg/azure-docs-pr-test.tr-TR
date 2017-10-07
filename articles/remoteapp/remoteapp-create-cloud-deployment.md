---
title: Azure RemoteApp bulut koleksiyonu aaaHow toocreate | Microsoft Docs
description: "Nasıl toocreate verileri kaydeder Azure RemoteApp dağıtımını hello Azure bulut öğrenin."
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
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Nasıl toocreate Azure RemoteApp bulut koleksiyonu
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

İki tür [Azure RemoteApp koleksiyonu](remoteapp-collections.md) vardır: 

* Bulut: tamamen Azure'da yer alıyor. Tüm verileri hello bulutta toosave seçebilirsiniz (şekilde bir yalnızca bulut koleksiyonu) veya tooconnect, koleksiyon tooa VNET ve verileri orada kaydedin.   
* Karma: bir sanal ağ içeren şirket içi erişim için - bu hello kullan Azure ad ve şirket içi Active Directory ortamında gerektirir.

Bu öğretici bir bulut koleksiyonu oluşturma hello işleminde size kılavuzluk eder. Dört adım vardır: 

1. Bir Azure RemoteApp koleksiyonu oluşturun.
2. İsteğe bağlı olarak dizin eşitlemesini yapılandırın. Azure AD kullanıyorsanız + Active Directory, elinizde toosynchronize kullanıcılar, kişiler ve parolalar, şirket içi Active Directory tooyour Azure AD kiracısı.
3. Uygulama yayımlama.
4. Kullanıcı erişimi yapılandırın.

**Başlamadan önce**

Merhaba koleksiyonu oluşturmadan önce toodo hello aşağıdaki gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp için. 
* Toogrant erişmek istediğiniz hello kullanıcılar hakkında bilgi toplayın. Bu, Microsoft hesap bilgileri veya kullanıcılar için Active Directory iş hesabı bilgileri olabilir.
* Bu yordam, ya da devam eden toouse bir aboneliğinizin bir parçası olarak sağlanan hello şablon görüntülerinin veya zaten sahip toouse istediğiniz hello şablon görüntüsü karşıya varsayar. Tooupload farklı şablon görüntüsü gerekiyorsa, bunu hello şablon görüntüleri sayfasından yapabilirsiniz. Tıklatmanız **şablon görüntüsü karşıya** ve hello hello sihirbazdaki adımları izleyin. 
* Toouse hello Office 365 ProPlus görüntüsünü istiyorsunuz? Bilgileri inceleyin [burada](remoteapp-officesubscription.md).
* Tooprovide özel uygulamalar veya LOB programlarının istiyorsunuz? Yeni bir [görüntü](remoteapp-imageoptions.md) ve bulut koleksiyonunuzda kullanın.
* Şekil tooconnect tooa VNET ihtiyacınız olup olmadığı. Tooconnect tooa VNET seçerseniz hello karşıladığından emin olun [yönergeleri boyutlandırma](remoteapp-vnetsizing.md) ve [tooRemoteApp bağlanabilir](remoteapp-vnet.md). Merhaba denetleyin [VNET planlama makale ](remoteapp-planvnet.md)daha fazla bilgi için.
* VNET kullanıyorsanız, toojoin isteyip istemediğinize karar verin, tooyour yerel Active Directory etki alanı.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>1. adım: Bulut koleksiyonu - olan veya olmayan bir sanal ağ oluşturma
Kullanım hello aşağıdaki adımları çok**bir yalnızca bulut koleksiyonu oluşturma**:

1. Merhaba Yönetim Portalı'nda toohello RemoteApp sayfasına gidin.
2. Tıklatın **yeni > Hızlı Oluştur**.
3. Koleksiyonunuz için bir ad girin ve bölgenizi seçin.
4. Merhaba planı toouse - standart ya da temel istediğinizi seçin.
5. Bu koleksiyon için Hello şablonu toouse seçin. 
   
    **İpucu:** aboneliğiniz RemoteApp için birlikte [şablon görüntüleri](remoteapp-images.md) , içeren Office 365 veya Office 2013 (deneme kullanımı için) programları, bazı (Word gibi) yayımlanan ve diğerleri toopublish hazır. Ayrıca, yeni bir oluşturabilirsiniz [görüntü](remoteapp-imageoptions.md) ve bulut koleksiyonunuzda kullanın.
6. Tıklatın **oluşturma RemoteApp koleksiyonu**.
   
    **Önemli:** koleksiyonunuzu too30 dakika tooprovision alabilir.

Azure RemoteApp koleksiyonunuzun oluşturulduktan sonra hello koleksiyonu hello adına çift tıklayın. Merhaba getirecek **Hızlı Başlangıç** sayfası - burada hello koleksiyonu yapılandırmayı tamamlamak budur.

Kullanım hello aşağıdaki adımları toocreate bir **bulut + VNET koleksiyonu**:

1. Merhaba Yönetim Portalı'nda toohello Azure RemoteApp sayfasına gidin.
2. Tıklatın **yeni** > **ile VNET oluşturma**.
3. Koleksiyonunuz için bir ad girin.
4. Merhaba planı toouse - standart ya da temel istediğinizi seçin.
5. Merhaba, önceden oluşturduğunuz sanal ağ seçin. Bilmiyorsanız nasıl toodo? Hello şimdilik hello adımlardır [karma](remoteapp-create-hybrid-deployment.md) konu.
6. Koleksiyon tooyour etki alanınızın toojoin istediğinize karar verin. Yanıt Evet ise, toouse AD Connect toointegrate Azure AD ile Active Directory ortamınızı ihtiyacınız olacaktır. Kapsanan olarak aşağıda içinde **2. adım**.
7. Tıklatın **oluşturma RemoteApp koleksiyonu**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>2. adım: Active Directory dizin eşitleme (isteğe bağlı) yapılandırma
Active Directory toouse istiyorsanız, Azure RemoteApp Azure Active Directory ve, şirket içi Active Directory toosynchronize kullanıcıları, kişileri ve parolaları tooyour Azure Active Directory kiracısı arasında dizin eşitlemesi gerektirir. Bkz: [Azure RemoteApp için Active Directory yapılandırma](remoteapp-ad.md) planlama bilgileri için. De doğrudan çok gidebilirsiniz[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) bilgi.

## <a name="step-3-publish-apps"></a>3. adım: uygulama yayımlama
Bir Azure RemoteApp hello uygulama veya program tooyour kullanıcıların sağlaması uygulamadır. Merhaba şablon görüntüsü için hello koleksiyonu karşıya bulunur. Bir uygulama, hello uygulama bir kullanıcının eriştiği toorun yerel ortamlarında görünür, ancak gerçekten, azure'da sanal makine çalışıyor. 

Kullanıcıların uygulamaları erişebilmeniz için önce toopublish gerekiyor bunları – uygulamaları sağlar, kullanıcılarınızın hello uygulamaları aracılığıyla erişim yayımlama hello Uzak Masaüstü İstemcisi.

Birden çok uygulamaları tooyour Azure RemoteApp koleksiyonu yayımlayabilirsiniz. Merhaba yayımlama sayfasından tıklatın **Yayımla** tooadd bir program. Hello ya da yayımlayabilirsiniz **Başlat** menü hello şablon görüntüsü ya da hello şablon görüntüsü hello uygulamasının hello yol belirtme. Hello tooadd seçerseniz **Başlat** menüsünde hello uygulama toopublish seçin. Tooprovide hello yolu toohello uygulama seçerseniz, hello uygulama ve hello şablon görüntüsü üzerinde yüklü hello yolu toowhere için bir ad sağlayın.

## <a name="step-4-configure-user-access"></a>4. adım: kullanıcı erişimini yapılandırma
Koleksiyonunuz oluşturduğunuza göre uzak kaynaklarınızı toobe mümkün toouse istediğiniz tooadd hello kullanıcıların gerekir. Active Directory kullanıyorsanız, erişim tooneed tooexist hello Active Directory kiracısında hello abonelikle, ilişkili sağladığınız hello kullanıcılar bu koleksiyonu toocreate kullanılır.

1. Merhaba hızlı başlangıç sayfasından tıklatın **kullanıcı erişimini yapılandırma**. 
2. Toogrant erişim için istediğiniz Hello iş hesabını (Active Directory) veya Microsoft hesabını girin.
   
   **Notlar:** 
   
   Merhaba kullandığınızdan emin olun  *user@domain.com*  biçimi.
   
   Office 365 ProPlus koleksiyonunuzda kullanıyorsanız, kullanıcılarınız için hello Active Directory kimlikleri kullanmanız gerekir. Bu lisans doğrulama yardımcı olur. 
3. Merhaba kullanıcılar doğrulandıktan sonra tıklatın **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar - başarıyla oluşturulan ve dağıtılan Azure RemoteApp bulut koleksiyonu. Merhaba sonraki adım, kullanıcılarınızın hello uzak masaüstü istemcisini yükleyip toohave olacaktır. Merhaba istemci hello URL'sini hello Azure RemoteApp hızlı başlangıç sayfasında bulabilirsiniz. Ardından, kullanıcıların oturum hello istemci uygulamasına sahip ve yayımladığınız hello uygulamalara erişim.

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Toplama toorating bu makalede, aşağıda yorum yapmamanın, değişiklikleri toohello makalesi kendisini yapıp olduğunu biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Yukarı doğru ilerleyin ve tıklatın **GitHub üzerinde Düzenle** toomake değişiklikleri - olanlar gelen gözden geçirilmek üzere toous ve biz üzerlerinde edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada göreceğiniz.

