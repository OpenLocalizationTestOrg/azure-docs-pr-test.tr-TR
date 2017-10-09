---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - Analytics'i"
description: "Azure Mobile Engagement Analytics, izleme, Segment ve Pano sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04a7020a-ad74-4491-be69-0bd574890029
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 69c6ff8f5c8540f8ba8b85b9ffec55acc59329fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-analytics-monitoring-segmentation-and-dashboard-issues"></a>Analiz, izleme, Segment ve Pano sorunları için sorun giderme kılavuzu
Merhaba olası sorunlar aşağıda verilmiştir Azure Mobile Engagement'ın uygulamaları, cihazlar ve kullanıcılar hakkında bilgileri nasıl toplar karşılaşabilirsiniz.

## <a name="missingdelayed-information"></a>Eksik Gecikmeli bilgi
### <a name="issue"></a>Sorun
* Bilgi Analytics, Segment veya Pano görünmesini içinde ertelendi.
* İzleme bilgileri eksik.
* Analytics, Segment veya pano bilgileri eksik.
* Segment basarsa sınırlar.

### <a name="causes"></a>Neden olur.
* Merhaba Analytics API, İzleyici API kullanabilirsiniz ve herhangi bir veri UI hello eksik olması durumunda kesimleri API toosee hello API'leri görülebilir.
* Ardından Hello Azure Mobile Engagement SDK'sını uygulamanıza doğru tümleşik değilse hello Analytics, Segment, izleme veya panolar mümkün toosee bilgileri olmayacaktır.
* Parçaları olamaz oluşturulduktan sonra kesimleri yalnızca "kopya" (kopyalanır) veya "(silinir) yok" değiştirilebilir. Segmentler yalnızca 10 ölçüt içerebilir.
* İzleme bilgilerinin eksik hello en iyi şekilde tootest toosetup bir test cihazı, kaldırma ve/veya hello test aygıtta hello uygulamayı yeniden yükleyin.
* Bilgileri Analytics, Segment veya panolar için 24 saatte bir yenilenir.
* Yeni kesimleri bilgilerinde hello segment önceki bilgilere dayalı olsa bile oluşturulduktan sonra 24 saate kadar görüntülenmeyebilir.
* Analiz verilerinizi hello UI filtreleme, uygulamanızın hello sürüm ne olursa olsun bu türdeki tüm örnekler (örneğin gösterir "Adına göre filtre kilitleniyor" sürüm 1 ve sürüm 2, uygulamanızın gösterir).
* Başlangıç tarihi yanlış ayarlanmış olan telefon sahip bir kullanıcı hello süre yanlış gösterilebileceği şekilde hello süre analiz için hello kullanıcıların cihaz ayarları, başlangıç tarihinden temel alır.
* Merhaba düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı çok "test" iter, veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.

## <a name="cant-locate-items-in-ui"></a>Öğeleri kullanıcı Arabiriminde bulunamıyor
### <a name="issue"></a>Sorun
* Bazı yerleşik göre kesimleri oluşturulamıyor veya özel uygulama bilgisi ölçütleri etiketi.
* Bazı yerleşik bulunamıyor veya özel uygulama bilgisi ölçütleri Analytics, izleme veya panolar etiketi.
* Merhaba veri analizi, izleme, Segment veya panolar yorumlayamayacağı.

### <a name="causes"></a>Neden olur.
* Bazı öğeler yerleşik ve etiketleri yalnızca itme ölçüt olarak kullanılabilir, ancak olmayabilir uygulama bilgisi eklemişsiniz tooa segment veya Analytics, izleme veya Pano görünür. 
* Yerleşik öğeleri ve tooa segment olamaz etiketleri eklendi uygulama bilgileri için aynı hedefleyen bir kesiminde dayalı olarak işlevi her kampanya tooperform hello ölçütünde hedefleme toosetup listeye ihtiyacınız olacak.
* Merhaba bağlam menülerini hello Analytics, izleme, Segment ve panolar bölümlerini hello Azure Mobile Engagement UI daha fazla yardım için bkz. nasıl ve ne tooinformation.

## <a name="crash-troubleshooting"></a>Sorun giderme kilitlenme
### <a name="issue"></a>Sorun
* Uygulama analizi, izleme veya Pano görünmesini kilitleniyor.

### <a name="causes"></a>Neden olur.
* Analytics, izleme veya Pano görülen tootroubleshoot uygulaması kilitlenir hello SDK önceki sürümleri ile ilgili bilinen sorunlar için emin toocheck hello sürüm notları olun.
* toofurther kilitlenme olaya uygulamaların yüklü olduğu bir test aygıttan gerçekleştirmek ve cihaz Kimliğinizi hello Azure Mobile Engagement UI hello "İzleyici – olayları" bölümünde aramak uygulama sorunlarını giderin. Ardından, uygulama toocrash neden hello olay gerçekleştirin ve hello hello Azure Mobile Engagement UI "– monitör kilitlenme" bölümünü ek bilgi arayın. 

