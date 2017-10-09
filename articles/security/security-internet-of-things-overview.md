---
title: aaaSecure, nesnelerin interneti (IOT) azure'da | Microsoft Docs
description: " Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar. Bu makalede, anlamanıza yardımcı olur nasıl toosecure Azure IOT çözümlerinizde. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Nesnelerin interneti güvenliğine genel bakış
Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar. Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:

* Cihazlardan veri toplama
* Hareket halinde veri akışı çözümleme
* Büyük veri gruplarını depolama ve sorgulama
* Gerçek zamanlı ve geçmiş verileri görselleştirme
* Arka ofis sistemleriyle tümleştirme

Bu özellikler, Azure IOT paketi paketleri birlikte toodeliver önceden yapılandırılmış çözümler olarak özel uzantıları ile birden çok Azure Hizmetleri. Bu önceden yapılandırılmış çözümler, IOT çözümlerinizi toodeliver ele tooreduce hello zaman yardımcı genel IOT çözümü düzenlerinin temel uygulamalarıdır. Merhaba IOT yazılım geliştirme setlerini kullanan, özelleştirebilir ve bu çözümleri toomeet kendi gereksinimlerinizi genişletir. Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.

Hello Azure IOT paketi, IOT gereksinimleriniz için güçlü bir çözümdür. Ancak, IOT çözümlerinizi göz önünde bulundurularak hello başından tasarlanmıştır upmost önem derecesi vardır. Merhaba çalıştırmaları IOT cihaz sayısı nedeniyle, herhangi bir güvenlik olayı hızlı bir şekilde önemli sonuçları yaygın bir olayla haline gelebilir.

anladığınızdan toohelp nasıl toosecure, IOT çözümlerinizi bilgisinden hello sahibiz.

## <a name="security-architecture"></a>Güvenlik mimarisi
Sistem tasarlanırken önemli toounderstand hello olası tehditler toothat sistemidir ve hello sistem tasarlanmış ve tasarlanmış gibi uygun savunma buna göre ekleyin. Toodesign hello hello başlangıç üründen göz önünde bulundurularak ile nasıl bir saldırganın mümkün toocompromise bir sistem olabilir anlama uygun Azaltıcı Etkenler hello başından yerinde olduğundan emin olun yardımcı olması önemlidir.

Okuyarak IOT güvenlik mimarisi hakkında bilgi edinebilirsiniz [şeyler güvenlik mimarisi Internet](../iot-suite/iot-security-architecture.md).

Bu makalede aşağıdaki konularda hello ele alınmıştır:

* [Bir tehdit modeli ile güvenlik başlar](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [IOT güvenlik](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Tehdit modelleme hello Azure IOT başvuru mimarisi](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Plan hello güvenlikten
Merhaba IOT benzersiz güvenlik, gizlilik ve uyumluluk sorunları toobusinesses dünya çapında doğurur. Bu sorunları yazılım ve nasıl uygulandığı burada Uzayda Döndür geleneksel siber teknolojisi hello siber ve hello fiziksel dünyaları yakınsama ne olur IOT ilgilidir. IOT çözümleri koruma cihazları, bu cihazlar ve hello Bulut ve işleme ve depolama sırasında hello bulutta güvenli veri koruması arasında güvenli bağlantı güvenli sağlanmasını sağlama gerektirir. Bu tür işlevselliği karşı çalışan, ancak, kaynak kısıtlı cihazları, dağıtımları coğrafi dağıtılması ve bir çözüm içinde çok sayıda aygıt değildir.

Bilgi edinebilirsiniz nasıl toohandle güvenlik okuyarak bu alanlarda [plan hello nesnelerin interneti güvenlikten](../iot-suite/securing-iot-ground-up.md).

Merhaba, aşağıdaki konularda hello anlatılmaktadır:

* [Plan hello altyapısından güvenli](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure – işletmeniz için güvenli IOT altyapısı](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>En İyi Uygulamalar
Bir IOT altyapısını koruma sıkı güvenlik derinlemesine stratejisi gerektirir. Güvenli hale getirme gelen hello üzerinden aktarımda toosecurely sağlama aygıtlar, her katman genel internet daha yüksek güvenlik güvencesi oluşturuncaya kadar veri bütünlüğü koruma verileri hello bulutta hello genel altyapı.

Okuyarak nesnelerin interneti güvenlikle ilgili en iyi yöntemler öğrenebilirsiniz [en iyi güvenlik uygulamalarını, nesnelerin interneti](../iot-suite/iot-security-best-practices.md).

Merhaba, aşağıdaki konularda hello anlatılmaktadır:

* [IOT donanım üreticisinin/Tümleştirici](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [IOT Çözüm geliştiricisi](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [IOT çözüm dağıtıcı](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [IOT çözüm işleci](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
