---
title: Azure RemoteApp karma koleksiyonu aaaHow toocreate | Microsoft Docs
description: "Bilgi nasıl toocreate tooyour iç ağa bağlanır RemoteApp dağıtımı."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Nasıl toocreate Azure RemoteApp karma koleksiyonu
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Okuma hello [duyuru](https://go.microsoft.com/fwlink/?linkid=821148) Ayrıntılar için.
> 
> 

Azure RemoteApp koleksiyonları iki tür vardır:

* Bulut: tamamen Azure'da yer alıyor. Tüm verileri hello bulutta toosave seçebilirsiniz (şekilde bir yalnızca bulut koleksiyonu) veya tooconnect, koleksiyon tooa VNET ve verileri orada kaydedin.   
* Karma: bir sanal ağ içeren şirket içi erişim için - bu hello kullan Azure ad ve şirket içi Active Directory ortamında gerektirir.

Gereken bilmiyorsanız? Kullanıma [ne tür bir koleksiyon için Azure RemoteApp zorunda](remoteapp-collections.md).

Bu öğretici bir karma koleksiyonu oluşturma hello işleminde size kılavuzluk eder. Sekiz adım vardır:

1. Karar [görüntü](remoteapp-imageoptions.md) toouse koleksiyonunuz için. Özel görüntü oluşturabilir veya aboneliğinizle dahil hello Microsoft görüntülerden birini kullanabilirsiniz.
2. Sanal ağınızı ayarlayın. Merhaba denetleyin [VNET planlama](remoteapp-planvnet.md) ve [boyutlandırma](remoteapp-vnetsizing.md) bilgi.
3. Bir koleksiyon oluşturun.
4. Koleksiyon tooyour yerel etki alanına katılın.
5. Şablon görüntüsü tooyour koleksiyonu ekleyin.
6. Dizin eşitlemesini yapılandırın. Azure Active Directory ya da 1) yapılandırma Azure Active Directory eşitleme hello parola eşitleme seçeneği ile tarafından veya 2) yapılandırma Azure Active Directory eşitleme hello parola eşitleme seçeneği ancak olan bir etki alanını kullanan olmadan ile tümleştirmenize Azure RemoteApp gerektirir Federasyon tooAD FS. Merhaba denetleyin [RemoteApp ile Active Directory için yapılandırma bilgilerini](remoteapp-ad.md).
7. RemoteApp uygulamaları yayımlayın.
8. Kullanıcı erişimi yapılandırın.

**Başlamadan önce**

Merhaba koleksiyonu oluşturmadan önce toodo hello aşağıdaki gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp için.
* Bir kullanıcı hesabı, Active Directory toouse hello Azure RemoteApp hizmet hesabı oluşturun. Bunu yalnızca makineler toohello etki alanına katılması bu hesap için hello kısıtlayın.
* Şirket içi ağınız hakkında bilgi toplayın: IP adresi bilgileri ve VPN cihaz ayrıntıları.
* Merhaba yüklemek [Azure PowerShell](/powershell/azure/overview) modülü.
* Toogrant erişmek istediğiniz hello kullanıcılar hakkında bilgi toplayın. Azure Active Directory kullanıcı asıl adı hello (örneğin, name@contoso.com) her kullanıcı için. UPN eşleşen Azure AD bu hello emin olun ve Active Directory.
* Şablon görüntüsü seçin. Azure RemoteApp şablon görüntüsü hello uygulamaları ve kullanıcılarınız için toopublish istediğiniz programları içerir. Bkz: [Azure RemoteApp görüntü seçenekleri](remoteapp-imageoptions.md) daha fazla bilgi için.
* Toouse hello Office 365 ProPlus görüntüsünü istiyorsunuz? Bilgileri inceleyin [burada](remoteapp-officesubscription.md).
* [RemoteApp için Active Directory yapılandırma](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>1. adım: sanal ağınızı ayarlama
Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz. Bir sanal ağ yerel ağınızda RemoteApp uzak kaynaklar üzerinden kullanıcılara erişim verilerinizi olanak sağlar. Dağıtılan sanal makineler toothat sanal ağ ve bir Azure sanal ağı kullanarak, koleksiyonun doğrudan ağ erişim tooother Azure hizmetleri sağlar.

Merhaba gözden emin olun [VNET planlama](remoteapp-planvnet.md) ve [VNET boyutu](remoteapp-vnetsizing.md) ağınızı oluşturmadan önce bilgi.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Bir Azure sanal ağ oluşturun ve tooyour Active Directory dağıtımı katılın
Başlangıç oluşturarak bir [sanal ağ](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Bu hello üzerinde gerçekleştirilir **ağ** hello Azure portal sekmesindedir. Sanal ağ toohello eşitlenmiş tooyour Azure Active Directory Kiracı Active Directory dağıtımı tooconnect gerekir.

Bkz: [hello Azure portal kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) daha fazla bilgi için.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Sanal ağınızı Azure RemoteApp için hazır olduğundan emin olun
Koleksiyonunuz oluşturmadan önce yeni bir sanal ağ hazır olduğundan emin olalım. Bu hello aşağıdakileri yaparak doğrulayabilirsiniz:

1. RemoteApp için oluşturduğunuz hello sanal ağın hello alt ağ içinde bir Azure sanal makine oluşturun.
2. Uzak Masaüstü tooconnect toohello sanal makine kullanın. (Tıklatın **bağlanmak**.)
3. Toohello katılması toouse RemoteApp için istediğiniz aynı Active Directory dağıtımı.

Çalıştı mı? Sanal ağ ve alt Azure RemoteApp için hazır!

Azure sanal makineler oluşturma ve Uzak Masaüstü'nü toothem bağlanma hakkında daha fazla bilgi bulabilirsiniz [burada](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>2. adım: bir Azure RemoteApp koleksiyonu oluşturma
1. Merhaba, [Azure portal](http://manage.windowsazure.com)gidin toohello Azure RemoteApp sayfası.
2. Tıklatın **yeni > ile VNET oluşturma**.
3. Koleksiyonunuz için bir ad girin.
4. Merhaba planı toouse - standart ya da temel istediğinizi seçin.
5. Sanal ağınızı hello açılan listesi ve alt ağınızı arasından seçim yapın.
6. Toojoin seçin, tooyour etki alanı.
7. Tıklatın **oluşturma RemoteApp koleksiyonu**.

Azure RemoteApp koleksiyonunuzun oluşturulduktan sonra hello koleksiyonu hello adına çift tıklayın. Merhaba getirecek **Hızlı Başlangıç** sayfası - burada hello koleksiyonu yapılandırmayı tamamlamak budur.

Bir şeyler yanlış gitmiş? Merhaba denetleyin [sorun giderme bilgileri karma koleksiyon](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>3. adım: Koleksiyon toohello yerel etki alanınıza bağlamak
1. Merhaba üzerinde **Hızlı Başlangıç** sayfasında, **yerel bir etki alanına katılma**.
2. Hello Azure RemoteApp hizmet hesabı tooyour yerel Active Directory etki alanı ekleyin. Merhaba etki alanı adını, kuruluş birimi, hizmet hesabı kullanıcı adı ve parola gerekir.
   
    Toplanan, hello adımları uyguladığınız hello bilgi budur [Azure RemoteApp için Active Directory'yi Yapılandır](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>4. adım: Bağlantı tooan Azure RemoteApp görüntüsü
Azure RemoteApp şablon görüntüsü kullanıcılarla tooshare istediğiniz hello programları içerir. Oluşturabilir ya da yeni bir [şablon görüntüsü](remoteapp-imageoptions.md) veya (bir zaten içeri aktarılan veya tooAzure RemoteApp karşıya) bağlantı tooan mevcut görüntü. Hello Azure RemoteApp tooone de bağlayabilirsiniz [şablon görüntüleri](remoteapp-images.md) Office 365 veya Office 2013 (deneme kullanımı için) programları içerir.

Merhaba yeni görüntüsü yüklüyorsanız tooenter gereksinim hello adı ve hello görüntüsü için başlangıç konumu seçin. Merhaba sonraki sayfada hello Sihirbazı'nın, PowerShell cmdlet'leri - kopya kümesini görmek ve yükseltilmiş Windows PowerShell komut istemi tooupload hello belirtilen görüntüden bu cmdlet'leri çalıştırmak.

Yalnızca tooan varolan şablon görüntüsü bağlıyorsanız hello görüntü adını, konumunu ve ilişkili Azure abonelik belirtin.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>5. adım: Active Directory dizin eşitlemesini yapılandırma
Azure Active Directory ya da 1) yapılandırma Azure Active Directory eşitleme hello parola eşitleme seçeneği ile tarafından veya 2) yapılandırma Azure Active Directory eşitleme hello parola eşitleme seçeneği ancak olan bir etki alanını kullanan olmadan ile tümleştirmenize Azure RemoteApp gerektirir Federasyon tooAD FS.

Kullanıma [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - Bu makale ayarladığınız dizin tümleştirme 4 adımda yardımcı olur.

Bkz: [dizin eşitleme yol haritası](http://msdn.microsoft.com//library/azure/hh967642.aspx) planlama bilgileri ve ayrıntılı adımlar için.

## <a name="step-6-publish-apps"></a>6. adım: uygulama yayımlama
Bir Azure RemoteApp hello uygulama veya program tooyour kullanıcıların sağlaması uygulamadır. Merhaba şablon görüntüsü için hello koleksiyonu karşıya bulunur. Bir kullanıcı bir uygulama eriştiğinde, yerel ortamlarında toorun görünür, ancak gerçekten Azure üzerinde çalışıyor.

Kullanıcıların uygulamaları erişebilmeniz için önce toopublish gerekiyor bunları – bu, kullanıcıların erişim hello uygulamalarınızı hello Uzak Masaüstü istemcisi aracılığıyla sağlar.

Birden çok uygulama tooyour koleksiyonu yayımlayabilirsiniz. Merhaba yayımlama sayfasından tıklatın **Yayımla** tooadd bir uygulama. Hello ya da yayımlayabilirsiniz **Başlat** menü hello şablon görüntüsü ya da hello şablon görüntüsü hello uygulamasının hello yol belirtme. Hello tooadd seçerseniz **Başlat** menüsünde hello program tooadd seçin. Tooprovide hello yolu toohello uygulama seçerseniz, hello uygulama ve hello şablon görüntüsü üzerinde yüklü hello yolu toowhere için bir ad sağlayın.

## <a name="step-7-configure-user-access"></a>7. adım: kullanıcı erişimini yapılandırma
Koleksiyonunuz oluşturduğunuza göre uzak kaynaklarınızı toobe mümkün toouse istediğiniz tooadd hello kullanıcıların gerekir. hello abonelikle erişim tooneed tooexist hello Active Directory kiracısında ilgili sağladığınız hello kullanıcılar bu Azure RemoteApp koleksiyonu toocreate kullanılır.

1. Merhaba hızlı başlangıç sayfasından tıklatın **kullanıcı erişimini yapılandırma**.
2. Toogrant erişim için istediğiniz Hello iş hesabını (Active Directory) veya Microsoft hesabını girin.
   
   **Notlar:**
   
   Merhaba kullandığınızdan emin olun  *user@domain.com*  biçimi.
   
   Office 365 ProPlus koleksiyonunuzda kullanıyorsanız, kullanıcılarınız için hello Active Directory kimlikleri kullanmanız gerekir. Bu lisans doğrulama yardımcı olur.
3. Hello kullanıcılar doğrulandıktan sonra tıklayın **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar - başarıyla oluşturulan ve dağıtılan Azure RemoteApp karma koleksiyonu. Merhaba sonraki adım, kullanıcılarınızın hello uzak masaüstü istemcisini yükleyip toohave olacaktır. Merhaba istemci hello URL'sini hello Azure RemoteApp hızlı başlangıç sayfasında bulabilirsiniz. Ardından, kullanıcıların oturum hello istemci uygulamasına sahip ve yayımladığınız hello uygulamalara erişim.

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Toplama toorating bu makalede, aşağıda yorum yapmamanın, değişiklikleri toohello makalesi kendisini yapıp olduğunu biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Yukarı doğru ilerleyin ve tıklatın **GitHub üzerinde Düzenle** toomake değişiklikleri - olanlar gelen gözden geçirilmek üzere toous ve biz üzerlerinde edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada göreceğiniz.

