---
title: "Azure RemoteApp karma koleksiyonu oluşturma | Microsoft Docs"
description: "İç ağınıza bağlanır RemoteApp dağıtımı oluşturmayı öğrenin."
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
ms.openlocfilehash: 346a5fe3e4011985e4247ceef0d5ca858049fd28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-hybrid-collection-for-azure-remoteapp"></a>Azure RemoteApp karma koleksiyonu oluşturma
> [!IMPORTANT]
> Azure RemoteApp 31 Ağustos 2017’de kullanımdan kaldırılacaktır. Ayrıntılı bilgi için [duyuruyu](https://go.microsoft.com/fwlink/?linkid=821148) okuyun.
> 
> 

Azure RemoteApp koleksiyonları iki tür vardır:

* Bulut: tamamen Azure'da yer alıyor. Tüm verileri bulutta kaydetmeyi seçebilirsiniz (şekilde bir yalnızca bulut koleksiyonu) veya koleksiyonunuz bir VNET'e bağlayın ve oradaki verileri kaydetmek için.   
* Karma: bir sanal ağ içeren şirket içi erişim için - bu kullanım Azure ad ve şirket içi Active Directory ortamında gerektirir.

Gereken bilmiyorsanız? Kullanıma [ne tür bir koleksiyon için Azure RemoteApp zorunda](remoteapp-collections.md).

Bu öğretici bir karma koleksiyonu oluşturma işleminde size kılavuzluk eder. Sekiz adım vardır:

1. Karar [görüntü](remoteapp-imageoptions.md) koleksiyonunuz için kullanmak. Özel görüntü oluşturabilir veya aboneliğinizle dahil Microsoft görüntülerden birini kullanabilirsiniz.
2. Sanal ağınızı ayarlayın. Kullanıma [VNET planlama](remoteapp-planvnet.md) ve [boyutlandırma](remoteapp-vnetsizing.md) bilgi.
3. Bir koleksiyon oluşturun.
4. Koleksiyonunuz yerel etki alanınıza ekleyin.
5. Şablon görüntüsü, koleksiyona ekleyin.
6. Dizin eşitlemesini yapılandırın. Azure RemoteApp ya da 1) yapılandırma Azure Active Directory eşitleme parola eşitleme seçeneğiyle ya da 2) yapılandırma Azure Active Directory eşitleme parola eşitleme seçeneği ancak için AD FS federasyon etki alanını kullanan olmadan Azure Active Directory ile tümleştirme gerektirir. Kullanıma [RemoteApp ile Active Directory için yapılandırma bilgilerini](remoteapp-ad.md).
7. RemoteApp uygulamaları yayımlayın.
8. Kullanıcı erişimi yapılandırın.

**Başlamadan önce**

Koleksiyon oluşturmadan önce aşağıdakileri yapmanız gerekir:

* [Kaydolun](https://azure.microsoft.com/services/remoteapp/) Azure RemoteApp için.
* Azure RemoteApp hizmeti hesabı olarak kullanılacak Active Directory'de bir kullanıcı hesabı oluşturun. Bunu yalnızca makine etki alanına katılması bu hesap için kısıtlayın.
* Şirket içi ağınız hakkında bilgi toplayın: IP adresi bilgileri ve VPN cihaz ayrıntıları.
* Yükleme [Azure PowerShell](/powershell/azure/overview) modülü.
* Erişim vermek istediğiniz kullanıcıları hakkında bilgi toplayın. Azure Active Directory kullanıcı asıl adı gerekir (örneğin, name@contoso.com) her kullanıcı için. UPN Azure AD arasında eşleştiğinden emin olun ve Active Directory.
* Şablon görüntüsü seçin. Azure RemoteApp şablon görüntüsü uygulamalar ve kullanıcılarınız için yayımlamak istediğiniz programları içerir. Bkz: [Azure RemoteApp görüntü seçenekleri](remoteapp-imageoptions.md) daha fazla bilgi için.
* Office 365 ProPlus görüntüsünü kullanmak istediğiniz? Bilgileri inceleyin [burada](remoteapp-officesubscription.md).
* [RemoteApp için Active Directory yapılandırma](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>1. adım: sanal ağınızı ayarlama
Mevcut bir Azure sanal ağı kullanan bir karma koleksiyon dağıtabilir veya yeni bir sanal ağ oluşturabilirsiniz. Bir sanal ağ yerel ağınızda RemoteApp uzak kaynaklar üzerinden kullanıcılara erişim verilerinizi olanak sağlar. Azure sanal ağını kullanarak diğer Azure Hizmetleri ve bu sanal ağ için Dağıtılmış sanal makineleri koleksiyonu doğrudan ağ erişimi sağlar.

Gözden geçirmeniz emin olun [VNET planlama](remoteapp-planvnet.md) ve [VNET boyutu](remoteapp-vnetsizing.md) ağınızı oluşturmadan önce bilgi.

### <a name="create-an-azure-vnet-and-join-it-to-your-active-directory-deployment"></a>Bir Azure sanal ağ oluşturun ve Active Directory dağıtımınızı katılın
Başlangıç oluşturarak bir [sanal ağ](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Bu işlem üzerinde gerçekleştirilir **ağ** Azure portalında sekmesi. Azure Active Directory kiracınızın eşitlenen Active Directory dağıtımı için sanal ağınıza bağlanmak için gerekir.

Bkz: [Azure portalını kullanarak bir sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) daha fazla bilgi için.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Sanal ağınızı Azure RemoteApp için hazır olduğundan emin olun
Koleksiyonunuz oluşturmadan önce yeni bir sanal ağ hazır olduğundan emin olalım. Bu, aşağıdakileri yaparak doğrulayabilirsiniz:

1. RemoteApp için oluşturduğunuz sanal ağ alt ağ içindeki bir Azure sanal makine oluşturun.
2. Sanal makineye bağlanmak için Uzak Masaüstü'nü kullanın. (Tıklatın **bağlanmak**.)
3. RemoteApp için kullanmak istediğiniz aynı Active Directory dağıtımına ekleyin.

Çalıştı mı? Sanal ağ ve alt Azure RemoteApp için hazır!

Uzak Masaüstü'nü onlara Azure sanal makineler oluşturma ve bağlanma hakkında daha fazla bilgi bulabilirsiniz [burada](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>2. adım: bir Azure RemoteApp koleksiyonu oluşturma
1. İçinde [Azure portal](http://manage.windowsazure.com)Azure RemoteApp sayfasına gidin.
2. Tıklatın **yeni > ile VNET oluşturma**.
3. Koleksiyonunuz için bir ad girin.
4. -Standart ya da temel kullanmak istediğiniz planı seçin.
5. Sanal ağınızı listesi ve alt ağınızı açılır listeden seçin.
6. Etki alanına katılmak seçin.
7. Tıklatın **oluşturma RemoteApp koleksiyonu**.

Azure RemoteApp koleksiyonunuzun oluşturulduktan sonra koleksiyon adına çift tıklayın. Getirecek **Hızlı Başlangıç** sayfası - burada koleksiyonu yapılandırmayı tamamlamak budur.

Bir şeyler yanlış gitmiş? Kullanıma [sorun giderme bilgileri karma koleksiyon](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-to-the-local-domain"></a>3. adım: Bağlantı koleksiyonunuza yerel etki alanı
1. Üzerinde **Hızlı Başlangıç** sayfasında, **yerel bir etki alanına katılma**.
2. Azure RemoteApp hizmet hesabını yerel Active Directory etki alanınıza ekleyin. Etki alanı adını, kuruluş birimi, hizmet hesabı kullanıcı adı ve parola gerekir.
   
    Topladığınız içindeki adımları uyguladığınız varsa bilgileri budur [Azure RemoteApp için Active Directory'yi Yapılandır](remoteapp-ad.md).

## <a name="step-4-link-to-an-azure-remoteapp-image"></a>4. adım: Azure RemoteApp görüntüsü Bağla
Azure RemoteApp şablon görüntüsü kullanıcılarla paylaşmak istediğiniz programları içerir. Oluşturabilir ya da yeni bir [şablon görüntüsü](remoteapp-imageoptions.md) veya varolan bir görüntü (bir zaten içeri aktarılan veya Azure RemoteApp karşıya) bağlantı. Azure RemoteApp birine de bağlayabilirsiniz [şablon görüntüleri](remoteapp-images.md) Office 365 veya Office 2013 (deneme kullanımı için) programları içerir.

Yeni görüntüyü yüklüyorsanız, bir ad girin ve görüntünün konumunu seçin gerekir. Sihirbazın sonraki sayfasında PowerShell cmdlet'leri - kopya kümesini görmek ve bu cmdlet'leri belirtilen görüntüyü karşıya yüklemek için yükseltilmiş bir Windows PowerShell isteminde çalıştırın.

Yalnızca var olan bir şablon görüntüsü bağlanıyorsanız, görüntü adı, konumu ve ilişkili Azure abonelik belirtin.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>5. adım: Active Directory dizin eşitlemesini yapılandırma
Azure RemoteApp ya da 1) yapılandırma Azure Active Directory eşitleme parola eşitleme seçeneğiyle ya da 2) yapılandırma Azure Active Directory eşitleme parola eşitleme seçeneği ancak için AD FS federasyon etki alanını kullanan olmadan Azure Active Directory ile tümleştirme gerektirir.

Kullanıma [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - Bu makale ayarladığınız dizin tümleştirme 4 adımda yardımcı olur.

Bkz: [dizin eşitleme yol haritası](http://msdn.microsoft.com//library/azure/hh967642.aspx) planlama bilgileri ve ayrıntılı adımlar için.

## <a name="step-6-publish-apps"></a>6. adım: uygulama yayımlama
Bir Azure RemoteApp uygulama veya Kullanıcılarınıza sağladığınız programı uygulamadır. Koleksiyon için karşıya şablon görüntüsü bulunur. Bir kullanıcı bir uygulama eriştiğinde, yerel ortamlarında çalıştırmak için görünür, ancak gerçekten Azure üzerinde çalışıyor.

Kullanıcılarınız erişebilir, bunları yayımlamanız gerekir – bu sağlar önce kullanıcılarınızın Uzak Masaüstü istemcisi üzerinden uygulamalara erişin.

Koleksiyonunuz için birden fazla uygulama yayımlayabilirsiniz. Yayımlama sayfasından tıklatın **Yayımla** bir uygulama eklemek için. Gelen ya da yayımlayabilirsiniz **Başlat** menü şablon görüntüsünün veya uygulama için şablon görüntüsü üzerinde yolunu belirterek. Ekleme seçerseniz **Başlat** menüsünde program eklemek için seçin. Uygulamanın yolunu sağlamak seçerseniz, uygulama ve şablon görüntüsü yüklendiği yolu için bir ad sağlayın.

## <a name="step-7-configure-user-access"></a>7. adım: kullanıcı erişimini yapılandırma
Koleksiyonunuz oluşturduğunuza göre uzak kaynaklar kullanabilmek için istediğiniz kullanıcıları eklemeniz gerekir. Abonelikle ilişkili Active Directory Kiracı mevcut gerek erişim sağladığınız kullanıcıların bu Azure RemoteApp koleksiyonunu oluşturmak için kullanılır.

1. Hızlı başlangıç sayfasından tıklatın **kullanıcı erişimini yapılandırma**.
2. İçin erişim vermek istediğiniz iş hesabını (Active Directory) veya Microsoft hesabını girin.
   
   **Notlar:**
   
   Kullandığınızdan emin olun  *user@domain.com*  biçimi.
   
   Office 365 ProPlus koleksiyonunuzda kullanıyorsanız, kullanıcılarınız için Active Directory kimlikleri kullanmanız gerekir. Bu lisans doğrulama yardımcı olur.
3. Kullanıcıların doğrulandıktan sonra tıklayın **kaydetmek**.

## <a name="next-steps"></a>Sonraki adımlar
İşte bu kadar - başarıyla oluşturulan ve dağıtılan Azure RemoteApp karma koleksiyonu. Sonraki adım, uzak masaüstü istemcisini yükleyip, kullanıcılarınızın sağlamaktır. Azure RemoteApp hızlı başlangıç sayfasında istemcinin URL bulabilirsiniz. Ardından, kullanıcıların oturum istemci uygulamasına sahip ve, yayımlanan uygulamalara erişim.

### <a name="help-us-help-you"></a>Yardımımıza katkıda bulunun
Bu makaleyi derecelendirmenin ve aşağıda yorum yapmamanın yanı sıra makalede değişiklik de yapabileceğinizi biliyor muydunuz? Eksik bir şeyler mi var? Yanlış bir şeyler mi var? Kafa karıştırıcı bir şeyler mi yazdım? Değişiklik yapmak için yukarı doğru ilerleyin ve **GitHub üzerinde düzenle**’ye tıklayın; bu değişiklikler incelenmek üzere bize gönderilir ve kabul edildikten sonra değişiklikleriniz ve iyileştirmeleriniz burada görünür.

