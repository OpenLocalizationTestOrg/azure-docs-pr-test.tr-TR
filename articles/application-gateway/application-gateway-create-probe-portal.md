---
title: "aaaCreate özel bir araştırma - Azure uygulama ağ geçidi - Azure portalı | Microsoft Docs"
description: "Nasıl toocreate özel bir araştırma uygulama ağ geçidi için hello portalını kullanarak bilgi edinin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Merhaba portalını kullanarak uygulama ağ geçidi için özel bir araştırma oluşturma

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Klasik PowerShell](application-gateway-create-probe-classic-ps.md)

Bu makalede, bir özel araştırma tooan varolan uygulama ağ geçidi hello Azure portal aracılığıyla ekleyin. Özel araştırmalara başarılı bir yanıt hello varsayılan web uygulaması üzerinde sağlamaz, uygulamaları veya belirli bir sağlık denetimi sayfası uygulamaları için kullanışlıdır.

## <a name="before-you-begin"></a>Başlamadan önce

Bir uygulama ağ geçidi zaten yoksa, ziyaret [bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md) toocreate bir uygulama ağ geçidi toowork ile.

## <a name="createprobe"></a>Merhaba araştırması oluştur

Araştırmalar iki adımlı bir işlem hello portal üzerinden yapılandırılır. Merhaba ilk adımı toocreate hello araştırması oluşturur. Merhaba ikinci adımda hello araştırma toohello arka uç http ayarları hello uygulama ağ geçidi ekleyin.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). Zaten bir hesabınız yoksa, için kaydolabilirsiniz bir [ücretsiz bir aylık deneme sürümü](https://azure.microsoft.com/free)

1. Hello Azure portal Sık Kullanılanlar bölmesi, tüm kaynaklar'ı tıklatın. Merhaba Hello uygulama ağ geçidi tüm kaynaklar dikey tıklayın. Zaten seçili hello abonelik çeşitli kaynaklar varsa, ada göre hello filtre partners.contoso.net girebilirsiniz... kutusunu tooeasily erişim hello uygulama ağ geçidi.

1. Tıklatın **yoklamaları** hello tıklatıp **Ekle** düğmesini tooadd bir araştırma.

  ![Doldurulan bilgilerle Ekle araştırma dikey penceresi][1]

1. Merhaba üzerinde **Ekle durumu araştırması** dikey penceresinde hello araştırma hello gerekli bilgileri doldurun ve tıklatın tamamlandığında **Tamam**.

  |**Ayar** | **Değer** | **Ayrıntılar**|
  |---|---|---|
  |**Ad**|customProbe|Bu değer hello Portalı'nda erişilebilir olan bir kolay ad toohello araştırma olur.|
  |**Protokol**|HTTP veya HTTPS | Sistem durumu araştırma hello hello protokolünü kullanır.|
  |**Ana bilgisayar**|yani contoso.com|Bu değer hello araştırması için kullanılan hello ana bilgisayar adıdır. Geçerli yalnızca çok siteli uygulama ağ geçidi üzerinde yapılandırılmış, aksi takdirde '127.0.0.1' kullanın. Bu değer hello VM ana bilgisayar adından farklıdır.|
  |**Path**|/ veya başka bir yolu|hello için tam bir url hello özel araştırma kalanı Hello. İle başlayan geçerli bir yol '/'. İçin http://contoso.com yalnızca Hello varsayılan yolu kullanın '/' |
  |**Aralığı (saniye)**|30|Ne sıklıkta hello araştırma toocheck sistem durumu için çalıştırılır. 30 saniyeden daha düşük tooset hello önerilmez.|
  |**Zaman aşımı (sn)**|30|zaman aşımından önce zaman hello araştırma Hello miktarını bekler. Merhaba zaman aşımı aralığı gereksinimlerini toobe bir http çağrısıyla tooensure hello arka uç health sayfasında yapılabilmesi için yeterince yüksek kullanılabilir.|
  |**Sağlıksız durum eşiği.**|3|Başarısız denemeleri toobe sağlıksız kabul sayısı. Sistem durumu denetimi başarısız olursa, arka uç hello 0 anlamına gelir eşiğinin sağlıksız hemen belirlenir.|

  > [!IMPORTANT]
  > Merhaba ana bilgisayar adı olan değil hello sunucu adı ile aynı. Bu değer hello hello uygulama sunucusunda çalışan hello sanal ana bilgisayar adıdır. Merhaba araştırma toohttp gönderilir: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Araştırma toohello ağ geçidi Ekle

Merhaba araştırma oluşturuldu, zaman tooadd olduğundan, toohello ağ geçidi. Araştırma ayarlar Itanium tabanlı sistemler için hello arka uç http ayarları hello uygulama ağ geçidi üzerinde ayarlanır.

1. Tıklatın **HTTP ayarları** hello uygulama ağ geçidi üzerinde toobring hello yapılandırma dikey yukarı hello penceresinde listelenen hello geçerli arka uç http Ayarları'ı tıklatın.

  ![HTTPS Ayarları penceresi][2]

1. Merhaba üzerinde **appGatewayBackEndHttpSettings** ayarlar dikey penceresi, onay hello **kullanım özel araştırma** onay kutusunu ve hello oluşturulan hello araştırma seçin [oluşturma hello araştırma](#createprobe) bölümü Merhaba üzerinde **özel araştırma** açılan...
Tamamlandığında, tıklayın **kaydetmek** ve hello ayarları uygulanır.

Merhaba varsayılan araştırma Merhaba varsayılan erişim toohello web uygulaması denetler. Özel bir araştırma oluşturuldu, hello uygulama ağ geçidi hello tanımlanan özel yol toomonitor durumu hello arka uç sunucuları için kullanır. Tanımlandı hello ölçütlere göre hello uygulama ağ geçidi hello araştırması belirtilen hello yolu denetler. Merhaba sağlıksız eşiğine ulaşıldıktan sonra hello çağrı toohost:Port / yolu bir HTTP 200 399 durumu yanıt döndürmüyor yoksa hello sunucu dışında döndürme alınır. Yeniden sağlıklı duruma geldiğinde algılama hello sağlıksız örneği toodetermine üzerinde devam eder. Merhaba örneği geri toohealthy sunucu havuzuna eklendikten sonra trafiği yeniden boyunca tooit ve yoklama toohello başlar örneği normal olarak kullanıcı belirtilen aralıkta devam eder.

## <a name="next-steps"></a>Sonraki adımlar

tooconfigure SSL boşaltma Azure uygulama ağ geçidi ile nasıl görürüm toolearn [SSL boşaltma yapılandırın](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

