---
title: "aaaMicrosoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Merhaba tehdit modelleme aracı kullanılabilir tüm hello özellikler hakkında bilgi edinin"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Tehdit modelleme aracı özelliğine genel bakış

Biz toouse hello tehdit modelleme aracı gereksinimlerini modelleme, tehdit için seçtiğiniz memnunuz! Bunu yapmadıysanız, ziyaret  **[hello tehdit modelleme aracı ile çalışmaya başlama](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn hello temelleri.

> Aracımız sık sık güncelleştirilir, böylece bu denetleyin genellikle toosee bizim en son özellikleri ve geliştirmeleri Kılavuzu.

Merhaba "Oluşturmak bir yeni Model" düğmesini tıklatarak boş başlangıç sayfası, benzer toohello görüntünün altına açar:

![Boş başlangıç sayfası](./media/azure-security-threat-modeling-tool/tmtstart.png)

Merhaba tehdit modeli kullanılarak oluşturulan ekibimiz hello içinde tarafından  **[Başlarken](./azure-security-threat-modeling-tool-getting-started.md)**  örnek, şimdi hello aracında kullanılabilir tüm hello özellikler bugün göz atın.

![Temel tehdit modeli](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Gezinme

Merhaba yerleşik özellikleri girmeden önce hello aracında bulunan hello ana bileşeni üzerinden edelim

### <a name="menu-items"></a>Menü öğeleri

Merhaba deneyimi benzer tooother Microsoft ürünleri olmalıdır. Merhaba en üst düzey menü öğeleri arasında giderek başlayalım:

![Menü öğeleri](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etiket                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Dosya** | <ul><li>Açın, kaydetme ve dosyaları kapatın</li><li>Oturum seçeneğinde OneDrive'nın hesapları</li><li>Paylaşım bağlantılar (Görünüm + Düzenle)</li><li>Dosya bilgilerini görüntüleme</li><li>Yeni şablon tooExisting modelleri Uygula</li></ul> |
| **Düzenleme** | Geri alma/Eylemler, iyi bir kopyalama, yapıştırma ve delete olarak yinele |
| **Görünümü** | <ul><li>Arasında geçiş **analiz** ve **tasarım** görünümleri</li><li>Açık kapalı windows (e.g.stencils, öğe özellikleri ve iletileri)</li><li>Düzen toodefault ayarlarını sıfırla</li></ul> |
| **Diyagramı** | Diyagramları ekleme/silme ve diyagramları "sekmeleri" arasında gidin |
| **Raporlar** | HTML raporları tooshare başkalarıyla oluşturma |
| **Yardım** | Kılavuzlar toohelp hello aracını kullanın |

Merhaba en üst düzey menü kısayolları Hello simgeler şunlardır:

| Simgesi                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Açık** | Yeni bir dosya açar |
| **Kaydet** | Geçerli dosya kaydeder |
| **Tasarım** | Tasarım görünümüne modelleri oluşturabileceğiniz gider |
| **Çözümleme** | Tehditler ve bunların özelliklerini gösterir oluşturulan |
| **Diyagrama ekleyin** | Yeni Diyagram (Excel'de benzer toonew sekmeleri) ekler |
| **Diyagram Sil** | Geçerli diyagram siler |
| **Kes/kopyala/yapıştır** | Keser/kopyaları/yapıştırır öğeleri |
| **Geri alma/yineleme** | Eylemler alır/Yinele |
| **Yakınlaştırma / Uzaklaştır** | Ve daha iyi bir görünüm için hello diyagramı yakınlaştırır |
| **Geri Bildirim** | Açılır hello MSDN Forumu |

### <a name="canvas"></a>Tuvale

Burada, sürükleyip elemanlara hello alanı. Sürükle ve bırak olan hello hızlı ve en verimli şekilde toobuild modeller. Ayrıca, sağ tıklayın ve aşağıda gösterildiği gibi kullanmakta olduğunuz hello öğeleri genel sürümlerini ekler hello menüsünden seçin.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Merhaba şablon hello tuvalde bırakılıyor

![Tuvale bırakma](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Merhaba şablonda tıklatarak

![Öğe özellikleri](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Şablonlar

Bulabileceğiniz burada tüm şablonlar seçili hello şablonunu temel alan kullanılabilir toouse. Merhaba sağ öğeleri bulamazsanız, başka bir şablonu kullanmayı deneyin veya bir toofit gereksinimlerinizi değiştirin. Genellikle, mümkün toofind kategoriler altında olanları hello gibi bir birleşimi olmalıdır:

| Şablon adı                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **İşlem** | Uygulamalar, tarayıcı eklentileri, iş parçacıkları, sanal makineler |
| **Dış etkileşen** | Kimlik doğrulama sağlayıcıları, tarayıcıları, kullanıcılar, Web uygulamaları |
| **Veri deposu** | Önbellek, depolama, yapılandırma dosyalarını, veritabanları, kayıt defteri |
| **Veri akışı** | İkili, ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, adlandırılmış kanal, RPC/DCOM, SMB, UDP |
| **Çizgi/Kenarlık sınır güven** | Şirket ağları, Internet, makine, korumalı alan, kullanıcı/çekirdek modu |

### <a name="notesmessages"></a>Notlar/iletileri

| Bileşen                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **İletileri** | Öğeler arasında hiçbir veri akışları gibi bir hata olduğunda kullanıcıları uyarır iç aracı mantığı |
| **Notlar** | El ile notları eklenen toohello dosyası mühendislik ekipleri tarafından baştan tasarım hello ve işlem gözden geçirin |

### <a name="element-properties"></a>Öğe özellikleri

Bunlar, seçili hello öğeleri tarafından farklılık gösterir. Güven sınırları dışında 3 genel seçimleri diğer tüm öğeleri içerir:

| Öğe özelliği                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Ad** | Kolay tanınan, işlemler, depolar, interactors ve akışlar toobe adlandırma yararlı |
| **Kapsamının dışında** | Seçili olduğunda, hello öğesi hello tehdit nesil matris (önerilmez) dışında alınır |
| **Kapsam dışında nedeni** | Doğrulama alanı toolet kullanıcılar kapsamının dışında seçilmedi neden bilmeniz |

Özellikleri her öğe kategorisi altında değiştirilir. Öğesi her tooinspect hello kullanılabilir Seçenekler'i tıklatın veya daha fazla hello şablonu toolearn açın. Şimdi hello özellikler alınamadı.

## <a name="welcome-screen"></a>Hoş Geldiniz ekranı

Merhaba Hoş Geldiniz ekranı hello uygulama açtığınızda gördüğünüz hello ilk şeydir.

### <a name="open-a-model"></a>Bir model açın

"Açık bir modeli" düğmenin üzerine getirildiğinde, 2 gizli seçeneklerini gösterir: "Dan bu bilgisayarı açma" ve "Aç onedrive" Merhaba ikinci, hello oturum açma işlemine aracılığıyla OneDrive, başarılı bir kimlik doğrulamasından sonra toopick klasörleri ve dosyaları izin verme işlenirken hello hello Dosya Aç ekran, ilk açılır.

![Açık modeli](./media/azure-security-threat-modeling-tool/openmodel.png)

![Bilgisayardan veya OneDrive Aç](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Geri bildirim, öneriler ve sorunları

Bu seçeneğin belirlenmesi için SDL araçları toohello MSDN Forumları olur. Geçici çözümler ve yeni fikirleri gibi hello aracı hakkında başkalarının ne dediğini çıkışı mükemmel şekilde toocheck olur.

![Geri Bildirim](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Tasarım görünümü

Her açın veya yeni bir model oluşturma toohello Tasarım görünümüne gidersiniz.

### <a name="adding-elements"></a>Öğeler ekleme

Merhaba kılavuzda tooadd öğeleri 2 yolu vardır:

- **Sürükleme ve bırakma** – hello İstenen öğe toohello kılavuz sürükleyin sonra hello öğe özellikleri tooprovide ek bilgileri kullanın.
- **Sağ tıklayın** – sağ hello kılavuz üzerinde herhangi bir yere tıklayın ve hello açılır menüsünden seçin. Bu öğe genel bir gösterimini Merhaba ekranında görüntülenir.

### <a name="connecting-elements"></a>Bağlama öğeleri

Merhaba aracında tooconnect öğeleri 2 yolu vardır:

- **Sürükleme ve bırakma** – hello istenen veri akışı toohello kılavuz sürükleyin ve her iki uca toohello uygun öğeleri bağlayın.
- **Shift + tıklayın** – (veri gönderme) hello ilk öğesini tıklatın, basılı hello SHIFT tuşunu sonra select hello ikinci öğesi (veri alma). Sağ tıklatın ve "Bağlan" seçin İki yönlü veri akışı kullanıyorsanız, hello sırası gibi önemli değildir.

### <a name="properties"></a>Özellikler

Merhaba şemada yerleştirilen hello şablonlar değiştirilebilir tüm hello özellikleri gösterir. toosee hello özellikler, yalnızca hello şablonda tıklayın ve hello bilgileri buna uygun olarak doldurulur. önce ve sonra "Şablon hello diyagram üzerine sürüklediğiniz bir veritabanı" Merhaba örnekte gösterilir:

#### <a name="before"></a>Önce

![Önce](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Sonra

![Sonra](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>İletiler

Merhaba ileti penceresinde bir tehdit modeli oluşturmak ve tooelements tooconnect veri akışları unutursanız, tooact bildirir. Tooignore veya izleyin seçebilirsiniz hello yönergeleri toofix hello sorun. 

![İletiler](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Notlar

İletileri tooNotes sekmelerinden değiştirme, tooadd notları tooyour diyagramı toocapture tüm düşüncelerinizi sağlar

## <a name="analysis-view"></a>Analiz görünümü

İşiniz bittiğinde, diyagram oluşturma, tooanalysis görünüm giderek toohello üst menü seçimlerini ve hello Büyüteç sonraki toohello boyama paleti seçme geçiş.

![Analiz görünümü](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Oluşturulan tehdit seçimi

Üzerinde bir tehdit tıkladığınızda, üç benzersiz işlevler yararlanabilirsiniz:

| Özellik                               | Bilgi      |
| --------------------------------------- | ------------ |
| **Okuma göstergesi** | <p>Tehdit şimdi kolayca zaten gittiğiniz aracılığıyla hello öğeleri izlemenize yardımcı olabilir okunur olarak işaretlendi</p><p>![Okuma/okunmamış göstergesi](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Etkileşim odak** | <p>Etkileşim toothat tehdit ait hello diyagramındaki vurgulanmış</p><p>![Etkileşim odak](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **İş parçacığı özellikleri** | <p>Merhaba tehdit Özellikler penceresinde hello tehdit hakkında ek bilgi doldurulur</p><p>![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Öncelik değiştirme

Oluşturulan her tehdit Hello öncelik düzeyini değiştirme de kendi renkleri toomake değiştirir, kolay tooidentify yüksek, Orta ve düşük öncelik tehditleri.

![Öncelik değiştirme](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Tehdit özellikleri düzenlenebilir alanları

Yukarıdaki Hello resimde görüldüğü gibi kullanıcılar hello aracı tarafından oluşturulan hello bilgilerini değiştirebilir bir ayrıca gerekçe gibi bilgi toocertain alanları ekleyin. Bu alanların hello şablon tarafından oluşturulan her tehdit için daha fazla bilgiye ihtiyacınız varsa, kullanmaları toomake değişiklikleri olacak şekilde.

![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Reports

Değişen öncelikleri işiniz bittiğinde ve tehdit her güncelleştirme hello durumunu oluşturulan sonra siz hello dosyasını kaydedin veya çok "rapor" giderek ve ardından "tam rapor oluştur." bir raporu yazdırın Tooname hello rapor istenir ve bunu yaptığınızda, aşağıdaki benzeri toohello görüntü görmeniz gerekir:

![Rapor](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Sonraki adımlar

Lütfen gidin tooour toocontribute hello topluluk için bir şablon  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  sayfası. **[Karşıdan](https://aka.ms/tmtpreview)**  hello aracı tooget kullanmaya bugün.
