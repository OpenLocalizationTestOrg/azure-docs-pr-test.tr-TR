---
title: "aaaAzure depolama hesabı listesi"
description: "Eclipse için Hello Azure Araç Seti kullanarak depolama hesap ayarlarınızı yönetme"
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
ms.openlocfilehash: 35e25881ca95ae4050a26283e4726d9549b37f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-account-list"></a>Azure depolama hesabı listesi
Azure depolama hesaplarını etkinleştirme JDK, uygulama sunucusu ve isteğe bağlı bileşenler için yanı sıra durumu önbelleğe alma kullanırken depolamak için kullanılan konumlardan toobe indirin. Eclipse Eclipse çalışma alanında kullanılabilir tooyour projeleri bilinen depolama hesaplarının listesini tutar. tooopen hello **depolama hesapları** listesinde, Eclipse içinde kullanılan toomanage olan iletişim tıklatın **penceresi**, tıklatın **Tercihler**, genişletin **Azure** ve ardından **depolama hesapları**.

Merhaba aşağıdaki gösterir hello **depolama hesapları** iletişim.

![][ic719496]

Bu iletişim kutusunu da açılabilir bir **hesapları** hello aşağıdaki gibi depolama hesaplarını kullanmak iletişim kutularında bağlantı:

* Merhaba **JDK** hello sekmesinde **sunucu yapılandırması** iletişim.
* Merhaba **Server** hello sekmesinde **sunucu yapılandırması** iletişim.
* Merhaba **Bileşen Ekle** iletişim.
* Merhaba **önbelleğe alma** Özellikleri iletişim kutusu.

## <a name="tooimport-your-storage-accounts-using-a-publish-settings-file"></a>Depolama hesaplarını kullanarak tooimport yayımlama ayarları dosyası
1. Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **yayımlama ayarları dosyasını içeri aktar**.

2. (Bir yayımlama ayarları dosyası tooyour yerel makine zaten kaydedilmiş dosyalarınız varsa bu adımı atlayın.) Merhaba, **alma abonelik bilgilerini** iletişim kutusunda, tıklatın **yayımlama ayarları dosyası karşıdan**. Azure hesabınızda henüz tutulmaz içinde istendiğinde toolog olacaktır. Size sorulacaktır sonra toosave Azure yayımlama ayarları dosyası. (Merhaba elde edilen yönergeleri hello oturum açma sayfalarında - gösterilen yoksayabilirsiniz bunlar hello Azure portalı tarafından sağlanan ve Visual Studio kullanıcılar için tasarlanmıştır.) Tooyour yerel makine kaydedin.

3. Merhaba yine de **alma abonelik bilgilerini** iletişim kutusunda, hello tıklatın **Gözat** düğmesi, select hello yayımlama yerel olarak daha önce kaydettiğiniz ayarları dosyası ve ardından **açın**.

4. Tıklatın **Tamam** tooclose hello **alma abonelik bilgilerini** iletişim.

## <a name="toocreate-a-new-storage-account"></a>toocreate yeni bir depolama hesabı
1. Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.

2. Merhaba içinde **depolama hesabı Ekle** iletişim kutusunda, tıklatın **yeni**.

3. Merhaba içinde **yeni depolama hesabı** iletişim kutusunda, hello aşağıdaki değerleri belirtin:

   * Depolama hesabı adı.

   * Merhaba depolama hesabı konumu.

   * Merhaba depolama hesabı açıklaması.

   * Merhaba abonelik toowhich hello depolama hesabına ait.

4. Tıklatın **Tamam** tooclose hello **yeni depolama hesabı** iletişim.

Oluşturulan, depolama hesabı toobe için birkaç dakika sürebilir. Oluşturulduktan sonra tıklatın **Tamam** tooclose hello **depolama hesabı Ekle** iletişim ve yeni depolama hesabınız, kullanılabilir depolama hesaplarını toohello listesine eklenecek.

## <a name="tooadd-an-existing-storage-account-toohello-list"></a>Varolan bir depolama hesabı toohello listesini tooadd
1. Bir Azure depolama hesabı, bir oluşturma zaten yoksa hello adımları izleyerek hello listelenen **toocreate yeni bir depolama hesabı bölüm** üstünde. (Alternatif olarak, hello yeni bir depolama hesabı oluşturabilirsiniz [Azure Yönetim Portalı][Azure Management Portal].)

2. Merhaba içinde **depolama hesapları** iletişim kutusunda, tıklatın **Ekle**.

3. Merhaba içinde **depolama hesabı Ekle** iletişim için değerleri girin **adı** ve **erişim tuşu**. Merhaba hesap adı ve erişim anahtarı mevcut bir Azure depolama hesabı için olmalıdır. Kullanım hello **depolama** hello bölümünü [Azure Yönetim Portalı] [ Azure Management Portal] tooview depolama hesabı adları ve anahtarları. **Depolama hesabı Ekle** benzer toohello aşağıdaki iletişim kutusu görünür.
   
   ![][ic719497]

4. Tıklatın **Tamam** tooclose hello **depolama hesabı Ekle** iletişim.

## <a name="toomodify-a-storage-account-toouse-a-new-access-key"></a>toomodify bir depolama hesabı toouse yeni bir erişim anahtarı
1. Merhaba içinde **depolama hesapları** iletişim kutusunda, tooedit istediğiniz ve ardından hello depolama hesabını tıklatın **Düzenle**.

2. Merhaba içinde **Düzenle depolama hesabının erişim anahtarı** iletişim kutusunda, hello değiştirme **erişim tuşu** değeri.

3. Tıklatın **Tamam** tooclose hello **Düzenle depolama hesabının erişim anahtarı** iletişim.

## <a name="tooremove-a-storage-account-from-hello-list-maintained-in-eclipse"></a>tooremove Eclipse'te tutulan hello listesinden bir depolama hesabı
1. Merhaba içinde **depolama hesapları** iletişim kutusunda, tooedit istediğiniz ve ardından hello depolama hesabını tıklatın **kaldırmak**.

2. Tıklatın **Tamam** zaman istendiğinde tooremove hello depolama hesabı.

> [!NOTE]
> Merhaba üzerinden Hello depolama hesabı kaldırma **depolama hesapları** iletişim yalnızca onu kaldırır hello listesinden depolama hesapları Eclipse içinde görüntülenebilir. Merhaba depolama hesabı Azure aboneliğinizden kaldırmaz. Ayrıca, Eclipse aboneliğinizi hello ayrıntılarını yeniden yükler sonra hello depolama hesabı yeniden listenizde görüntülenebilir.
> 
> 

## <a name="see-also"></a>Ayrıca Bkz.
[Eclipse için Azure Araç Seti][Azure Toolkit for Eclipse]

[Yükleme hello Eclipse için Azure Araç Seti][Installing hello Azure Toolkit for Eclipse] 

[Eclipse'te Azure Merhaba Dünya uygulaması oluşturma][Creating a Hello World Application for Azure in Eclipse]

Azure Java ile kullanma hakkında daha fazla bilgi için bkz: Merhaba [Azure Java Geliştirici Merkezi][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic719496]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719496.png
[ic719497]: ./media/azure-toolkit-for-eclipse-azure-storage-account-list/ic719497.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn205108.aspx -->
