---
ms.assetid: 
title: "aaaAzure anahtar kasası güvenlik dünyaları | Microsoft Docs"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Azure anahtar kasası güvenlik dünyaları ve coğrafi sınırlar

Azure anahtar kasası çok kiracılı bir hizmet olduğundan ve her Azure konumu donanım güvenlik modülleri (HSM'ler) havuzu kullanır. 

Tüm HSM'ler aynı coğrafi bölge paylaşımına hello Azure konumlardaki aynı şifreleme sınırı (Thales güvenlik Dünyası) hello. Toohello ABD coğrafi konuma ait olduğundan Örneğin, Doğu ABD ve Batı ABD paylaşmak aynı güvenlik hello world. Benzer şekilde, tüm Azure konumları Japonya paylaşımda aynı güvenlik dünyası ve Avustralya, Hindistan, tüm Azure konumlarda hello ve benzeri. 

## <a name="backup-and-restore-behavior"></a>Yedekleme ve geri yükleme davranışı

Bu koşulların her ikisi de doğruysa sürece tooa konumda başka bir Azure anahtar kasası anahtar Azure konumu olabilir birinde bir anahtar Kasası'ndan alınan bir yedeklemeyi geri:

- Hello Azure her ikisi de konumları ait toohello aynı coğrafi konum
- Merhaba anahtar kasalarını her ikisi de toohello ait aynı Azure aboneliği

Örneğin, belirli bir aboneliğe Batı Hindistan, bir anahtar kasasına bir anahtar tarafından gerçekleştirilecek bir yedekleme yalnızca olabilir hello anahtar kasasına geri yüklenen tooanother aynı abonelikte ve coğrafi konum; Batı Hindistan, Orta Hindistan veya Güney Hindistan.

## <a name="regions-and-products"></a>Bölgeler ve ürünler

- [Azure bölgeleri](https://azure.microsoft.com/regions/)
- [Bölgeye göre Microsoft ürünleri](https://azure.microsoft.com/regions/services/)

Bölgeler hello tablolardaki ana başlıklar olarak gösterilen eşlenen toosecurity dünyaları şunlardır:

Örneğin, bölge makale tarafından Hello ürünlerinde hello **Americas** sekmesi içerir Doğu ABD, Orta ABD, Batı ABD tüm eşleme toohello Americas bölge. 

>[!NOTE]
>Bir özel durum BİZE savunma Bakanlığı Doğu ve BİZE savunma Bakanlığı merkezi kendi güvenlik dünyaları olmasıdır. 

Benzer şekilde, hello üzerinde **Avrupa** sekmesinde, Kuzey Avrupa ve Batı Avrupa, her ikisi de eşlenir toohello Avrupa bölgesi. Merhaba aynı de hello üzerinde geçerlidir **Asya Pasifik** sekmesi.



