---
title: "Uygulama yükseltme: veri seri hale getirme | Microsoft Docs"
description: "Veri seri hale getirme ve uygulama yükseltmelerini nasıl etkilediği için en iyi uygulamalar."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Veri seri hale getirme uygulama yükseltme nasıl etkiler
İçinde bir [uygulama yükseltmesinde](service-fabric-application-upgrade.md), hello yükseltmedir uygulanan tooa alt düğümler, aynı anda bir yükseltme etki alanı. Bu işlem sırasında bazı yükseltme etki alanları hello daha yeni sürümü, uygulamanızın üzerinde ve bazı yükseltme etki alanları, uygulamanızın hello eski sürümü. Merhaba piyasaya çıkma sırasında hello yeni sürümü, uygulamanızın mümkün tooread hello eski sürümü verilerinizi olmalıdır ve hello eski sürümü, uygulamanızın verilerinizin mümkün tooread hello yeni sürüm olmalıdır. Merhaba veri biçimi ileriye ve geriye dönük uyumlu hello yükseltme değilse başarısız ya da kötüsü, veri kayıp bozuk veya. Hangi veri biçimi oluşturduğunu ve verilerinizi ileriye ve geriye doğru olduğundan emin olmanın en iyi yöntemleri sunar bu makalede ele uyumlu.

## <a name="what-makes-up-your-data-format"></a>Veri biçiminiz ne yapar?
Azure Service Fabric içinde kalıcı ve çoğaltılan hello veriler, C# sınıflardan gelir. Kullanan uygulamalar için [güvenilir koleksiyonları](service-fabric-reliable-services-reliable-collections.md), hello güvenilir sözlükler ve Kuyruklar hello nesneleri verilerdir. Kullanan uygulamalar için [Reliable Actors](service-fabric-reliable-actors-introduction.md), yani hello aktör durumunu yedekleme hello. Bu C# sınıfları seri hale getirilebilir toobe kalıcı ve çoğaltılır. Bu nedenle, hello veri biçimi hello alanlar ve bunlar serileştirilir nasıl, de serileştirilir özellikleri tarafından tanımlanır. Örneğin, bir `IReliableDictionary<int, MyClass>` hello verilerdir seri hale getirilmiş bir `int` ve seri hale getirilmiş bir `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Veri biçimi değişiklik sonucunda ortaya çıkan kod değişiklikleri
Merhaba veri biçimi C# sınıfları tarafından belirlenir. bu yana değişiklikler toohello sınıfları bir veri biçimi değişmesine neden olabilir. Sıralı yükseltmeye işleyebilir tooensure Bakımı alınan hello veri değişikliği biçimi. Veri biçimi değişiklik neden olabilir Örnekler:

* Ekleyerek veya kaldırarak alanları veya özellikleri
* Alanlar ve Özellikler yeniden adlandırma
* Merhaba türlerini alanların veya özelliklerini değiştirme
* Merhaba sınıf adı veya ad alanı değiştirme

### <a name="data-contract-as-hello-default-serializer"></a>Varsayılan serileştirici hello gibi veri sözleşmesi
Merhaba veri eski bir olsa bile Hello seri hale getirici hello veri okumak ve hello geçerli sürüme seri durumdan çıkarmak için genellikle sorumlu veya *yeni* sürümü. Merhaba varsayılan serileştirici olduğu hello [veri sözleşmesi seri hale getirici](https://msdn.microsoft.com/library/ms733127.aspx), iyi tanımlanmış sürüm kuralları vardır. Güvenilir koleksiyonları geçersiz kılınmış hello seri hale getirici toobe izin ver, ancak Reliable Actors şu anda yapın. Merhaba veri serileştirici yükseltmeyi etkinleştirme önemli bir rol oynar. Merhaba veri sözleşmesi seri hale getirici için Service Fabric uygulamaları öneririz hello seri hale getirici ' dir.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Merhaba veri biçimi çalışırken yükseltme nasıl etkiler
Çalışırken yükseltme sırasında burada hello seri hale getirici karşılaşabilir eski bir iki ana senaryo vardır veya *yeni* verilerinizin sürümü:

1. Bir düğüm yükseltilir ve yedekleme başladıktan sonra yeni seri hale getirici hello hello eski sürümü tarafından kalıcı toodisk edildi hello veri yükler.
2. Hello çalışırken yükseltme sırasında hello küme hello eski ve yeni sürümler, kodunuzun bir karışımını içerir. Çoğaltmaları farklı yükseltme etki alanlarında yerleştirilebilir ve çoğaltmaları veri tooeach diğer hello yeni ve/veya eski Gönder verilerinizin sürümü hello yeni ve/veya eski sürümü, seri hale getirici tarafından karşılaşılabilir.

> [!NOTE]
> "yeni sürümü" ve "eski sürümü" Merhaba toohello sürümünü çalıştıran kodunuzu buraya bakın. Merhaba "Yeni seri hale getirici" Merhaba yeni sürümde, uygulamanızın yürütüyor toohello seri hale getirici kodu gösterir. Hello "yeni veri" Merhaba yeni uygulamanızı sürümünden serileştirilmiş toohello C# sınıfı gösterir.
> 
> 

kod iki sürümü hello ve veri biçimi ileriye ve geriye doğru olmalıdır uyumlu. Uyumlu değillerse, yükseltmesinde hello başarısız olabilir veya veri kaybı olabilir. Merhaba karşılaştığında hello kodu veya seri hale getirici özel durumları veya bir hata başka bir sürüm atabilir çünkü yükseltmesinde hello başarısız olabilir. Örneğin, yeni bir özellik eklendi ancak isteğe bağlı olarak hello eski seri hale getirici seri durumdan çıkarma sırasında atar, veriler kaybolabilir.

Veri sözleşmesi verilerinizi uyumlu olmasını sağlamaya yönelik çözüm önerilen hello değil. Ekleme, kaldırma ve alanları değiştirme için iyi tanımlanmış sürüm kuralları vardır. Ayrıca, bilinmeyen alanlarla ilgilenme hello seri hale getirme ve seri durumdan çıkarma işlemi takma ve sınıf devralma ile ilgili destek içerir. Daha fazla bilgi için bkz: [kullanarak veri sözleşmesi](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama kullanarak Visual Studio yükseltme](service-fabric-application-upgrade-tutorial.md) Visual Studio kullanarak bir uygulama yükseltme yol gösterir.

[Uygulama Powershell kullanarak yükseltme](service-fabric-application-upgrade-tutorial-powershell.md) PowerShell kullanarak bir uygulama yükseltme yol gösterir.

Uygulamanızı kullanarak yükseltme nasıl kontrol [yükseltme parametreleri](service-fabric-application-upgrade-parameters.md).

Uygulamanız çok başvurarak yükseltirken toouse işlevselliği nasıl Gelişmiş öğrenin[Gelişmiş konular](service-fabric-application-upgrade-advanced.md).

Toohello adımlarda başvurarak uygulama yükseltmeleri sık karşılaşılan sorunları düzeltmek [sorun giderme uygulama yükseltmelerini ](service-fabric-application-upgrade-troubleshooting.md).

