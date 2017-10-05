---
title: "Azure depolama hesabı listesi"
description: "Eclipse için Azure Araç Seti kullanarak depolama hesap ayarlarınızı yönetme"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: bbacfcd8-dbf5-4265-a930-59f508de5325
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: f859efa389d3fe0b4b7b16255d57f1aa13123319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-account-list"></a>Azure depolama hesabı listesi
Azure depolama hesapları JDK, uygulama sunucusu ve isteğe bağlı bileşenler için yanı sıra durumu önbelleğe alma kullanırken depolamak için kullanılacak yükleme konumları sağlar. Eclipse projelerinizi Eclipse çalışma alanında kullanılabilir bilinen depolama hesaplarının listesini tutar. Açmak için **depolama hesapları** Eclipse içinde bu listesini yönetmek için kullanılan iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure**ve ardından **depolama hesapları**.

Aşağıdaki gösterildiği **depolama hesapları** iletişim.

![][ic719496]

Bu iletişim kutusunu da açılabilir bir **hesapları** aşağıdaki gibi depolama hesaplarını kullanmak iletişim kutularında bağlantı:

* **JDK** sekmesinde **sunucu yapılandırması** iletişim.
* **Server** sekmesinde **sunucu yapılandırması** iletişim.
* **Bileşen Ekle** iletişim.
* **Önbelleğe alma** Özellikleri iletişim kutusu.

## <a name="to-import-your-storage-accounts-using-a-publish-settings-file"></a>Yayımlama ayarları dosyası kullanarak depolama hesaplarınızı içeri aktarmak için
1. İçinde **depolama hesapları** iletişim kutusunda, tıklatın **yayımlama ayarları dosyasını içeri aktar**.

2. (Yerel makinenize yayımlama ayarları dosyası kaydettiyseniz bu adımı atlayın.) İçinde **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**. Azure hesabınızda henüz tutulmaz, oturum açmak için istenir. Ardından Azure yayımlama ayarları dosyası istenir. (Oturum açma sayfalarında - gösterilen elde edilen yönergeleri yoksayabilirsiniz bunlar Azure portalı tarafından sağlanan ve Visual Studio kullanıcılar için tasarlanmıştır.) Yerel makinenize kaydedin.

3. Hala **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **Gözat** düğmesi, yerel olarak daha önce kaydettiğiniz yayımlama ayarları dosyasını seçin ve ardından **açmak**.

4. Tıklatın **Tamam** kapatmak için **alma abonelik bilgilerini** iletişim.

## <a name="to-create-a-new-storage-account"></a>Yeni bir depolama hesabı oluşturmak için
1. İçinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.

2. İçinde **depolama hesabı Ekle** iletişim kutusunda, tıklatın **yeni**.

3. İçinde **yeni depolama hesabı** iletişim kutusunda, aşağıdaki değerleri belirtin:

   * Depolama hesabı adı.

   * Depolama hesabı konumu.

   * Depolama hesabı açıklaması.

   * Depolama hesabına ait olduğu abonelik.

4. Tıklatın **Tamam** kapatmak için **yeni depolama hesabı** iletişim.

Oluşturulacak depolama hesabınız için birkaç dakika sürebilir. Oluşturulduktan sonra tıklatın **Tamam** kapatmak için **depolama hesabı Ekle** iletişim ve yeni depolama hesabınız, kullanılabilir depolama alanı hesaplar listesine eklenir.

## <a name="to-add-an-existing-storage-account-to-the-list"></a>Mevcut bir depolama hesabını listeye eklemek için
1. Bir Azure depolama hesabı zaten yoksa, listelenen adımları izleyerek oluşturun **yeni bir depolama hesabı bölüm oluşturmak için** üstünde. (Alternatif olarak, yeni bir depolama hesabı oluşturabilirsiniz [Azure Yönetim Portalı][Azure Management Portal].)

2. İçinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.

3. İçinde **depolama hesabı Ekle** iletişim için değerleri girin **adı** ve **erişim tuşu**. Hesap adı ve erişim anahtarı mevcut bir Azure depolama hesabı için olmalıdır. Kullanım **depolama** bölümünü [Azure Yönetim Portalı] [ Azure Management Portal] depolama hesabı adları ve anahtarlarını görüntülemek için. **Depolama hesabı Ekle** iletişim aşağıdakine benzer görünür.
   
   ![][ic719497]

4. Tıklatın **Tamam** kapatmak için **depolama hesabı Ekle** iletişim.

## <a name="to-modify-a-storage-account-to-use-a-new-access-key"></a>Yeni bir erişim anahtarı kullanmak üzere bir depolama hesabı değiştirmek için
1. İçinde **depolama hesapları** iletişim, depolama hesabına o düzenlemek istiyorsanız tıklatın ve ardından **Düzenle**.

2. İçinde **Düzenle depolama hesabının erişim anahtarı** iletişim kutusunda, değiştirmek **erişim tuşu** değeri.

3. Tıklatın **Tamam** kapatmak için **Düzenle depolama hesabının erişim anahtarı** iletişim.

## <a name="to-remove-a-storage-account-from-the-list-maintained-in-eclipse"></a>Eclipse'te tutulan listesinden bir depolama hesabını kaldırmak için
1. İçinde **depolama hesapları** iletişim, depolama hesabına o düzenlemek istiyorsanız tıklatın ve ardından **kaldırmak**.

2. Tıklatın **Tamam** depolama hesabını kaldırmak isteyip istemediğiniz sorulduğunda.

> [!NOTE]
> Üzerinden depolama hesabı kaldırma **depolama hesapları** iletişim yalnızca onu kaldırır listesinden depolama hesaplarının Eclipse içinde görüntülenebilir. Depolama hesabı Azure aboneliğinizden kaldırmaz. Ayrıca, Eclipse aboneliğinizi ayrıntılarını yeniden yükler sonra depolama hesabını yeniden listenizde görüntülenebilir.
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Eclipse için Azure araç setini yükleme][Installing the Azure Toolkit for Eclipse] 

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
