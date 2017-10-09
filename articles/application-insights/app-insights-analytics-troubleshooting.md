---
title: Azure Application Insights analizleri aaaTroubleshoot | Microsoft Docs
description: "Application Insights analytics sorunları? Buradan başlayın. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9bbd5859-3584-4d80-9b6d-d5910fa48baa
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/11/2016
ms.author: bwren
ms.openlocfilehash: e3be2fbc0237440d3b8a736484434a9f276296c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-analytics-in-application-insights"></a>Application Insights Analiz Sorunlarını Giderme
Sorun [uygulama Öngörüler Analytics](app-insights-analytics.md)? Buradan başlayın. Analytics hello güçlü arama Azure Application Insights, aracıdır.

## <a name="limits"></a>Sınırlar
* Şu anda, sorgu sonuçları haftanın son verilerini sınırlı toojust olur.
* Biz test tarayıcılar: Chrome, sınır ve Internet Explorer'ın en son sürümleri.

## <a name="known-incompatible-browser-extensions"></a>Bilinen uyumlu tarayıcı uzantıları
* Ghostery

Merhaba uzantıyı devre dışı bırakmak veya farklı bir tarayıcı kullanın.

## <a name="e-a"></a>"Beklenmeyen hata"
![Beklenmeyen hata ekranı](./media/app-insights-analytics-troubleshooting/010.png)

İç hata portal çalışma zamanı sırasında – işlenmeyen bir özel durum oluştu.

* Merhaba tarayıcının önbelleğini temizlemek. 

## <a name="e-b"></a>403... Lütfen tooreload deneyin
![403... Lütfen tooreload deneyin](./media/app-insights-analytics-troubleshooting/020.png)

Bir kimlik doğrulaması ile ilgili (kimlik doğrulaması veya erişim belirteci oluşturma sırasında) hata oluştu. Merhaba portal çok tarayıcı ayarları değiştirmeden kurtarma yolu yoktur.

* Doğrulama [üçüncü taraf tanımlama bilgilerini etkin](#cookies) hello tarayıcıda. 

## <a name="authentication"></a>403... güvenlik bölgesi doğrulayın
![403.. .verify güvenlik bölgesi](./media/app-insights-analytics-troubleshooting/030.png)

Bir kimlik doğrulaması ile ilgili (kimlik doğrulaması veya erişim belirteci oluşturma sırasında) hata oluştu. Merhaba portal çok tarayıcı ayarları değiştirmeden kurtarma yolu yoktur.

1. Doğrulama [üçüncü taraf tanımlama bilgilerini etkin](#cookies) hello tarayıcıda. 
2. Sık kullanılan, yer işareti veya kaydedilen bağlantı tooopen hello Analytics portalı kullandınız mı? Merhaba bağlantı kaydedildiğinde kullandığınızdan farklı kimlik ile oturum açtığınızı?
3. (Tüm pencereleri kapattıktan sonra) içinde-özel/ıncognito tarayıcı penceresi kullanmayı deneyin. Kimlik bilgilerinizi tooprovide sahip olacaksınız. 
4. Başka bir (normal) tarayıcı penceresi açın ve çok gidin[Azure](https://portal.azure.com). Oturumu kapatın. Bağlantı açabilir ve hello doğru kimlik bilgilerinizle oturum açın.
5. Güvenilir bölgeye ayarlar desteklenmez kenarı ve Internet Explorer kullanıcıların da bu hatayı elde edebilirsiniz.
   
    Her ikisi de doğrulayın [Analytics portalı](https://analytics.applicationinsights.io) ve [Azure Active Directory portalında](https://portal.azure.com) hello olan aynı güvenlik bölgesi:
   
   * Internet Explorer'da açın **Internet Seçenekleri**, **güvenlik**, **Güvenilen siteler**, **siteleri**:
     
     ![Internet Seçenekleri iletişim kutusunda, bir site ekleme tooTrusted siteler](./media/app-insights-analytics-troubleshooting/033.png)
     
     Aşağıdaki URL'lere hello dahil olan hello Web siteleri listesinde o hello emin olun diğerleri de dahildir:
     
     https://Analytics.applicationinsights.io<br/>
     https://login.microsoftonline.com<br/>
     https://login.windows.net

## <a name="e-d"></a>404 ... Kaynak bulunamadı
![404... kaynak bulunamadı](./media/app-insights-analytics-troubleshooting/040.png)

Uygulama kaynağı Application Insights silindi ve artık kullanılamıyor. Merhaba URL toohello analitik sayfası kaydedilirse, bu durum oluşabilir.

## <a name="e-e"></a>403 ... Yok
![403... yetkili değil](./media/app-insights-analytics-troubleshooting/050.png)

Bu uygulama izni tooopen analizleri sahip değilsiniz.

* Merhaba bağlantı birisinden mı aldınız? Toomake hello olduğundan emin isteyin [okuyucular veya katkıda bulunanlar bu kaynak grubu için](app-insights-resources-roles-access-control.md).
* Farklı kimlik bilgileri kullanarak hello bağlantısı kaydettiniz? Açık hello [Azure portal](https://portal.azure.com), oturumu kapatın ve ardından hello doğru kimlik bilgilerini sağlayan bu bağlantıyı yeniden deneyin.

## <a name="html-storage"></a>403 ... HTML5 depolaması
HTML5 localStorage ve sessionStorage portalımıza kullanır.

* Chrome: Ayarları, gizlilik, içerik ayarları.
* Internet Explorer: Internet Seçenekleri, Gelişmiş sekmesinde, güvenlik, DOM depolama etkinleştir

![403... tooenable HTML5 depolama deneyin](./media/app-insights-analytics-troubleshooting/060.png)

## <a name="e-g"></a>404 ... Abonelik bulunamadı
![404 ... Abonelik bulunamadı](./media/app-insights-analytics-troubleshooting/070.png)

Merhaba URL'si geçersiz. 

* Açık hello uygulama kaynak [Application Insights portalındaki](https://portal.azure.com). Ardından hello Analytics düğmesini kullanın.

## <a name="e-h"></a>404... sayfa yok
![404 ... Sayfa yok](./media/app-insights-analytics-troubleshooting/080.png)

Merhaba URL'si geçersiz.

* Açık hello uygulama kaynak [Application Insights portalındaki](https://portal.azure.com). Ardından hello Analytics düğmesini kullanın.

## <a name="cookies"></a>Üçüncü taraf tanımlama bilgilerini etkinleştirin
  Bkz: [nasıl toodisable üçüncü taraf tanımlama bilgilerini](http://www.digitalcitizen.life/how-disable-third-party-cookies-all-major-browsers), ancak çok ihtiyacımız fark**etkinleştirmek** bunları.


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]

