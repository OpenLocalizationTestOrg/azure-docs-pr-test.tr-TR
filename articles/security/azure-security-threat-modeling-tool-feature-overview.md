---
title: "Microsoft tehdit modelleme aracı - Azure | Microsoft Docs"
description: "Tehdit modelleme aracında kullanılabilir tüm özellikler hakkında bilgi edinin"
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
ms.openlocfilehash: 621ff305d7e782f85eeaae6c3fb02031673549c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Tehdit modelleme aracı özelliğine genel bakış

Biz gereksinimlerini modelleme, tehdit tehdit modelleme Aracı'nı kullanmak seçtiğiniz memnunuz! Bunu yapmadıysanız, ziyaret  **[tehdit modelleme aracı ile çalışmaya başlama](./azure-security-threat-modeling-tool-getting-started.md)**  temellerini öğrenin.

> Aracımız sık sık güncelleştirilir, genellikle, en son özellikleri ve geliştirmeleri görmek için bu kılavuzu kontrol edin.

"Oluştur bir yeni Model" düğmesini tıklatarak aşağıdaki görüntü benzer boş başlangıç sayfasını açar:

![Boş başlangıç sayfası](./media/azure-security-threat-modeling-tool/tmtstart.png)

Tehdit modeli kullanılarak oluşturulan bizim ekibi tarafından  **[Başlarken](./azure-security-threat-modeling-tool-getting-started.md)**  örnek, şimdi aracında kullanılabilir tüm özellikleri bugün göz atın.

![Temel tehdit modeli](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Gezinme

İçinde yerleşik özellikler girmeden önce aracında bulunan ana bileşeni üzerinden edelim

### <a name="menu-items"></a>Menü öğeleri

Deneyimi diğer Microsoft ürünlerine benzer olmalıdır. Üst düzey menü öğeleri arasında giderek başlayalım:

![Menü öğeleri](./media/azure-security-threat-modeling-tool/menuitems.png)

| Etiket                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Dosya** | <ul><li>Açın, kaydetme ve dosyaları kapatın</li><li>Oturum seçeneğinde OneDrive'nın hesapları</li><li>Paylaşım bağlantılar (Görünüm + Düzenle)</li><li>Dosya bilgilerini görüntüleme</li><li>Varolan modeli yeni şablonu Uygula</li></ul> |
| **Düzenleme** | Geri alma/Eylemler, iyi bir kopyalama, yapıştırma ve delete olarak yinele |
| **Görünümü** | <ul><li>Arasında geçiş **analiz** ve **tasarım** görünümleri</li><li>Açık kapalı windows (e.g.stencils, öğe özellikleri ve iletileri)</li><li>Düzen varsayılan ayarlarına sıfırlama</li></ul> |
| **Diyagramı** | Diyagramları ekleme/silme ve diyagramları "sekmeleri" arasında gidin |
| **Raporlar** | Diğer kişilerle paylaşmak için HTML rapor oluşturma |
| **Yardım** | Aracı'nı kullanmanıza yardımcı olmak için size yol gösterir |

Üst düzey menü kısayolları simgeler şunlardır:

| Simgesi                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Açık** | Yeni bir dosya açar |
| **Kaydet** | Geçerli dosya kaydeder |
| **Tasarım** | Tasarım görünümüne modelleri oluşturabileceğiniz gider |
| **Çözümleme** | Tehditler ve bunların özelliklerini gösterir oluşturulan |
| **Diyagrama ekleyin** | Yeni Diyagram (Excel yeni sekmelerde benzer) ekler |
| **Diyagram Sil** | Geçerli diyagram siler |
| **Kes/kopyala/yapıştır** | Keser/kopyaları/yapıştırır öğeleri |
| **Geri alma/yineleme** | Eylemler alır/Yinele |
| **Yakınlaştırma / Uzaklaştır** | Ve daha iyi bir görünüm için diyagramı yakınlaştırır |
| **Geri Bildirim** | MSDN Forumu açar |

### <a name="canvas"></a>Tuvale

Burada, sürükleyip elemanlara alanı. Sürükle ve bırak yoludur modelleri oluşturmak için hızlı ve en iyi yoldur. Ayrıca, sağ tıklayın ve aşağıda gösterildiği gibi kullanmakta olduğunuz öğeleri genel sürümlerini ekler menüsünde seçin.

#### <a name="dropping-the-stencil-on-the-canvas"></a>Tuvalde şablon bırakılıyor

![Tuvale bırakma](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-the-stencil"></a>Şablon üzerinde tıklatarak

![Öğe özellikleri](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Şablonlar

Kullanılabilir tüm şablonlar bulabileceğiniz seçilen şablona dayalı. Sağ öğeleri bulamazsanız, başka bir şablonu kullanmayı deneyin veya bir gereksinimlerinize uyacak şekilde değiştirin. Genellikle, kategoriler ve olanlar gibi bir birleşimini bulamıyor olması gerekir:

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
| **Notlar** | Dosyaya mühendislik tasarımı ve gözden geçirme işlemi boyunca ekipleri tarafından eklenen el ile notları |

### <a name="element-properties"></a>Öğe özellikleri

Bunlar, seçili öğeler farklılık gösterir. Güven sınırları dışında 3 genel seçimleri diğer tüm öğeleri içerir:

| Öğe özelliği                               | Ayrıntılar      |
| --------------------------------------- | ------------ |
| **Ad** | Yararlı, işlemler, depolar, interactors ve akışlar kolayca tanınması için adlandırma |
| **Kapsamının dışında** | Seçili olduğunda, öğe (önerilmez) tehdit nesil matris dışı alınır |
| **Kapsam dışında nedeni** | Kapsam dışında neden bilmesini sağlamak üzere gerekçe alanları seçilmedi |

Özellikleri her öğe kategorisi altında değiştirilir. Kullanılabilir seçenekler inceleyin veya daha fazla bilgi için şablon açmak için her öğesini tıklatın. Şimdi özellikler alınamadı.

## <a name="welcome-screen"></a>Hoş Geldiniz ekranı

Hoş Geldiniz ekranında uygulama açtığınızda gördüğünüz ilk şeydir.

### <a name="open-a-model"></a>Bir model açın

"Açık bir modeli" düğmenin üzerine getirildiğinde, 2 gizli seçeneklerini gösterir: "Dan bu bilgisayarı açma" ve "Aç onedrive" İkinci, oturum açma işlemine aracılığıyla, OneDrive, başarılı bir kimlik doğrulamasından sonra dosya ve klasörleri seçmenize olanak sağlayan alır ancak ilk Dosya Aç ekranı açılır.

![Açık modeli](./media/azure-security-threat-modeling-tool/openmodel.png)

![Bilgisayardan veya OneDrive Aç](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Geri bildirim, öneriler ve sorunları

Bu seçeneğin belirlenmesi için SDL araçları MSDN Forumları olur. Geçici çözümler ve yeni fikirleri dahil olmak üzere aracı hakkında başkalarının ne dediğini denetlemek için harika bir yoludur.

![Geri Bildirim](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Tasarım görünümü

Her açın veya yeni bir model oluşturma Tasarım görünümüne gidersiniz.

### <a name="adding-elements"></a>Öğeler ekleme

Kılavuzda öğeler eklemek için 2 yolu vardır:

- **Sürükleme ve bırakma** – İstenen öğe kılavuza sürükleyin ve ardından ek bilgi sağlamak için öğe özelliklerini kullanın.
- **Sağ tıklayın** – sağ kılavuzda herhangi bir yere tıklayın ve açılan menüden seçin. Bu öğe genel bir gösterimini ekranında görüntülenir.

### <a name="connecting-elements"></a>Bağlama öğeleri

Öğeleri aracında bağlamak için 2 yolu vardır:

- **Sürükleme ve bırakma** – istenen veri akışı kılavuza sürükleyin ve uygun öğeleri için her iki ucuna bağlayın.
- **Shift + tıklayın** – (veri gönderme) ilk öğeyi tıklatın, tuşuna basın ve Shift tuşunu basılı tutun ve sonra da (veri alma) ikinci öğesini seçin. Sağ tıklatın ve "Bağlan" seçin İki yönlü veri akışı kullanıyorsanız, sipariş gibi önemli değildir.

### <a name="properties"></a>Özellikler

Diyagramda yerleştirilen şablonlar değiştirilebilir tüm özellikleri gösterir. Özelliklerini görmek için şablon üzerinde tıklamanız yeterlidir ve bilgileri buna uygun olarak doldurulur. Aşağıdaki örnek, önce ve sonra "Şablon diyagram üzerine sürüklediğiniz bir veritabanı" gösterir:

#### <a name="before"></a>Önce

![Önce](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Sonra

![Sonra](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>İletiler

Bir tehdit modeli oluşturmak ve veri akışları öğelere bağlanmak unutursanız, ileti penceresinde hareket size bildirir. Yok sayın veya sorunu düzeltmek için yönergeleri izleyin seçebilirsiniz. 

![İletiler](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Notlar

İletileri sekmelerinden Notlar geçiş Notlar tüm düşüncelerinizi yakalamak için diyagrama eklemenize izin verir

## <a name="analysis-view"></a>Analiz görünümü

İşiniz bittiğinde, diyagram oluşturma, analiz görünümüne üst menü seçimleri gidip Büyüteç boyama palet yanındaki seçme geçebilir.

![Analiz görünümü](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Oluşturulan tehdit seçimi

Üzerinde bir tehdit tıkladığınızda, üç benzersiz işlevler yararlanabilirsiniz:

| Özellik                               | Bilgi      |
| --------------------------------------- | ------------ |
| **Okuma göstergesi** | <p>Tehdit şimdi kolayca zaten gittiğiniz aracılığıyla öğeleri izlemenize yardımcı olabilir okunur olarak işaretlendi</p><p>![Okuma/okunmamış göstergesi](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Etkileşim odak** | <p>Tehdit vurgulanır ait diyagramdaki etkileşimi</p><p>![Etkileşim odak](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **İş parçacığı özellikleri** | <p>Tehdit hakkında ek bilgi tehdit Özellikler penceresinde doldurulur</p><p>![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Öncelik değiştirme

Oluşturulan her tehdit öncelik düzeyini değiştirme, yüksek, Orta ve düşük öncelik tehditleri tanımlamak kolaylaştırmak için kendi renkleri değiştirir.

![Öncelik değiştirme](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Tehdit özellikleri düzenlenebilir alanları

Yukarıdaki resimde görüldüğü gibi kullanıcılar aracı tarafından oluşturulan bilgileri değiştirebilir bir gerekçe gibi bazı alanları ayrıca bilgi ekleyin. Bu alanların şablon tarafından oluşturulan her tehdit için daha fazla bilgiye ihtiyacınız varsa, değişiklikler yapmak için kullanmaları için.

![İş parçacığı özellikleri](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Reports

Bir kez değişen öncelikleri işiniz bittiğinde ve oluşturulan her tehdit durumunu güncelleştirme, siz dosyayı kaydedin veya "Rapor" ve ardından "Tam rapor oluştur." giderek bir raporu yazdırma Rapor adı istenir ve bunu yaptığınızda, aşağıdaki görüntü benzer bir şey görmeniz gerekir:

![Rapor](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Sonraki adımlar

Bir şablon için topluluğa katkıda bulunmak için lütfen Git bizim  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  sayfası. **[Karşıdan](https://aka.ms/tmtpreview)**  bugün başlamak için aracı.
