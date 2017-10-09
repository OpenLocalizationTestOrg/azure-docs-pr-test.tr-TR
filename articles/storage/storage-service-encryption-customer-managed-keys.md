---
title: "aaaAzure depolama hizmeti şifrelemesi yönetilen anahtarları Azure anahtar Kasası'müşteri kullanarak | Microsoft Docs"
description: "Müşteri kullanarak hello verilerini alma anahtarları yönetildiğinde şifresini çözmek ve Azure Blob Depolama alanınızın hello hizmet tarafında hello veri depolarken Hello Azure depolama hizmeti şifrelemesi özelliği tooencrypt kullanın."
services: storage
documentationcenter: .net
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: lakasa
ms.openlocfilehash: 870cae2f258b356aa234f8bba65a023ac389be10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-service-encryption-using-customer-managed-keys-in-azure-key-vault"></a>Depolama hizmeti müşteri kullanarak şifreleme anahtarları Azure anahtar Kasası'yönetilen

Microsoft Azure korumak ve Kuruluş güvenliği ve uyumluluk taahhüt veri toomeet koruma kesinlikle taahhüt toohelping ' dir.  REST verilerinizi koruyabilmek için bir depolama hizmeti şifreleme (otomatik olarak toostorage yazarken, verileri şifreler ve onu alırken, verilerin şifresini çözer SSE), toouse yoludur. Merhaba şifreleme ve şifre çözme otomatiktir ve tamamen saydam ve 256 bit kullanan [AES şifreleme](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard), hello güçlü blok birini şifrelemeleri kullanılabilir.

Microsoft tarafından yönetilen şifreleme anahtarları ile SSE kullanabilir veya kendi şifreleme anahtarlarınızı kullanabilirsiniz. Bu makalede hello hakkında ikinci konuşur. Daha fazla SSE veya Microsoft tarafından yönetilen anahtarlar kullanılarak hakkında genel olarak, lütfen bilgi için [bekleyen veri için depolama hizmeti şifrelemesi](storage-service-encryption.md).

tooprovide hello özelliği toouse SSE Blob storage için kendi şifreleme anahtarları Azure anahtar kasası (AKV) ile tümleşiktir. Kendi şifreleme anahtarlarınızı oluşturup bunları AKV depolamak veya AKV'ın API'leri toogenerate şifreleme anahtarlarını kullanabilirsiniz. Yalnızca mu AKV toomanage izin ver ve anahtarlarınızı denetlemek, ayrıca, anahtar kullanımı, tooaudit sağlar. 

Neden toocreate kendi anahtarları istiyor? Hello özelliği toocreate dahil olmak üzere daha fazla esneklik sağlar, döndürme, devre dışı bırakmak ve erişim denetimleri ve tooaudit hello şifreleme anahtarları kullanılan tooprotect verilerinizi tanımlayın.

## <a name="sse-with-customer-managed-keys-preview"></a>SSE müşteri yönetilen anahtarlar Önizleme ile

Bu özellik şu anda önizleme sürümündedir. toouse bu özelliği, toocreate yeni bir depolama hesabı gerekir. Yeni bir anahtar kasası oluşturabilir ya da ve anahtar veya bir var olan anahtar kasasını ve anahtar kullanabilirsiniz. Merhaba depolama hesabı ve hello anahtar kasası hello olmalıdır aynı bölge, ancak bunlar farklı Aboneliklerde olabilir.

Merhaba önizlemede tooparticipate Lütfen kişi [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com). Şu özel bağlantıyı tooparticipate hello Önizleme'de sağlar.

toolearn daha başvurun toohello [SSS](#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).

> [!IMPORTANT]
> Bu makaledeki hello Önizleme önceki toofollowing hello adımları için kaydolmanız gerekir. Önizleme erişim olmadan yapmamayı mümkün tooenable hello portalında bu özellik olabilir.

## <a name="getting-started"></a>Başlarken
## <a name="step-1-create-a-new-storage-accountstorage-create-storage-accountmd"></a>1. adım: [yeni depolama hesabı oluşturma](storage-create-storage-account.md)

## <a name="step-2-enable-encryption"></a>2. adım: Etkinleştirme şifreleme
Hello kullanarak hello depolama hesabı için SSE etkinleştirebilirsiniz [Azure portal](https://portal.azure.com). Hello ayarları dikey penceresinde hello depolama hesabı için hello aşağıdaki şekilde gösterildiği gibi Blob hizmeti bölüm arayın ve şifreleme'yi tıklatın.

![Portal gösteren ekran görüntüsü şifreleme seçeneği](./media/storage-service-encryption/image1.png)
<br/>*Blob hizmeti için SSE etkinleştir*

Tooprogrammatically etkinleştirmek istediğiniz veya bir depolama hesabında depolama hizmeti şifrelemesi hello devre dışı bırakırsanız hello kullanabilirsiniz [Azure depolama kaynak sağlayıcısı REST API](https://docs.microsoft.com/en-us/rest/api/storagerp/?redirectedfrom=MSDN), hello [depolama kaynak sağlayıcısı istemci kitaplığı .NET için](https://docs.microsoft.com/en-us/dotnet/api/?redirectedfrom=MSDN), [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview?view=azurermps-4.0.0), veya hello [Azure CLI](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli).

Merhaba "kendi anahtarınızı kullan" onay kutusunu göremiyorsanız, bu ekranda, hello Önizleme için onaylanan değil. Lütfen e-posta çok gönderin[ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) ve onay isteyin.

![Şifreleme Önizleme gösteren portal ekran görüntüsü](./media/storage-service-encryption-customer-managed-keys/ssecmk1.png)

Varsayılan olarak, Microsoft tarafından yönetilen anahtarları SSE kullanır. toouse kendi anahtarlarını hello kutusunu denetleyin. Ardından, anahtarınızı URI belirtin veya bir anahtarı ve anahtar kasası hello seçiciden seçin.

## <a name="step-3-select-your-key"></a>3. adım: anahtarınızı seçin

![Portal ekran şifreleme gösteren kendi anahtar seçeneğini kullanın](./media/storage-service-encryption-customer-managed-keys/ssecmk2.png)

![Şifreleme ile anahtar URI seçenek girin gösteren portal ekran görüntüsü](./media/storage-service-encryption-customer-managed-keys/ssecmk3.png)

Merhaba depolama hesabı erişim toohello anahtar kasası yoksa hello aşağıdaki çalıştırabilirsiniz toohello gerekli anahtar kasası Azure Powershell toogrant erişim toohello depolama hesaplarını kullanarak komutu.

![Erişim için anahtar kasasını reddedildi gösteren portal ekran görüntüsü](./media/storage-service-encryption-customer-managed-keys/ssecmk4.png)

Ayrıca, toohello Azure anahtar Kasası'hello Azure portal'ın olma ve erişim toohello depolama hesabı verme hello Azure portal aracılığıyla erişim izni verebilir.

## <a name="step-4-copy-data-toostorage-account"></a>4. adım: veri toostorage hesabı kopyalama
Lütfen yeni depolama hesabınızda tootransfer veri istiyorsanız şifreli böylece çok başvurun[adım 3, Başlarken bölümünde kalan verileri için depolama hizmeti şifrelemesi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-3-copy-data-to-storage-account).

## <a name="step-5-query-hello-status-of-hello-encrypted-data"></a>5. adım: Sorgu hello hello durumunu veri şifrelenir.
şifrelenmiş hello veri tooquery hello durumu başvurun çok[adım 4, Başlarken bölümünde kalan verileri için depolama hizmeti şifrelemesi](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption#step-4-query-the-status-of-the-encrypted-data).

## <a name="frequently-asked-questions-about-storage-service-encryption-for-data-at-rest"></a>Sık sorulan bekleyen veri için depolama hizmeti şifrelemesi hakkında sorular
**S: Premium depolama kullanıyorum; Müşteri yönetilen anahtarlarla SSE kullanabilir miyim?**

A: Microsoft tarafından yönetilen ile SSE ve müşteri anahtarları Evet yönetilen standart depolama ve Premium depolama desteklenir. 

**S: yeni depolama hesapları ile SSE Azure PowerShell ve Azure CLI kullanarak etkin müşteri yönetilen anahtarlarla oluşturabiliyorum?**

Y: Evet.

**S: ne kadar daha fazla desteklemediğini Azure depolama maliyeti müşteriyle SSE anahtarları yönetilen etkin mi?**

Y: var. Azure anahtar kasası kullanmak için ilişkili bir maliyet Daha fazla ayrıntı şu adresi ziyaret edin [anahtar kasası fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/key-vault/). SSE kullanmak için ek bir maliyet yoktur.

**S: erişim toohello şifreleme anahtarlarını iptal?**

A: Evet erişimi dilediğiniz zaman iptal edebilirsiniz. Çeşitli yolları toorevoke erişim tooyour anahtar vardır. Lütfen çok başvurun[Azure anahtar kasası PowerShell](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.0.0) ve [Azure anahtar kasası CLI](https://docs.microsoft.com/en-us/cli/azure/keyvault) daha fazla ayrıntı için. Hello hesap şifreleme anahtarı Azure Storage tarafından erişilemez olduğundan erişim hakkının İptali etkili bir şekilde hello depolama hesabındaki erişim tooall BLOB'lar engeller.

**S: bir depolama hesabı ve anahtarı farklı bölgede oluşturabilirim?**

A: Hayır hello depolama hesabı ve anahtarı kasa anahtarı gerek toobe aynı bölgede hello. 

**S: SSE müşteri yönetilen anahtarlarla hello depolama hesabı oluşturulurken etkinleştirebilirim?**

Y: No Merhaba depolama hesabı oluşturulurken SSE etkinleştirdiğinizde, yalnızca Microsoft tarafından yönetilen tuşlarını kullanabilirsiniz. Toouse yönetilen müşteri anahtarları isterseniz tooupdate hello depolama hesabı özellikleri gerekir. REST kullanabilir veya hello depolama istemci kitaplığı tooprogrammatically biri depolama hesabınızı güncelleştirmek veya hello hesabı oluşturduktan sonra hello Azure Portal kullanarak hello depolama hesabı özelliklerini güncelleştirme.

**S: yönetilen anahtarları SSE müşteriyle kullanarak ı şifreleme devre dışı?**

A: Hayır anahtarları yönetilen SSE müşteriyle kullanarak sırasında şifreleme devre dışı bırakılamıyor. toodisable şifreleme tooswitch toousing Microsoft tarafından yönetilen anahtarlar gerekir. Hello Azure portal veya PowerShell kullanarak bunu yapabilirsiniz.

**S: yeni bir depolama hesabı oluşturduğunuzda, varsayılan olarak etkin SSE mi?**

Y: SSE varsayılan olarak etkin değildir; hello Azure portal tooenable kullanabilirsiniz. Program aracılığıyla da hello depolama kaynak sağlayıcısı REST API kullanarak bu özelliği etkinleştirebilirsiniz. 

**Depolama Hesabımı s: şifreleme etkinleştirilemiyor.**

Y: Resource Manager depolama hesabı mı? Klasik depolama hesapları desteklenmez. Müşteri yönetilen anahtarlarla SSE de yalnızca yeni oluşturulan Resource Manager depolama hesaplarında etkinleştirilebilir.

**S: olduğu SSE müşteriyle yalnızca belirli bölgelerine izin anahtarları yönetiliyor?**

Y: SSE yalnızca belirli bölgeler Bu önizleme için Blob storage için kullanılabilir. Lütfen e-posta [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) toocheck kullanılabilirlik ve önizleme hakkında ayrıntılar. 

**S: herhangi bir sorununuz veya tooprovide geri bildirim istediğiniz nasıl ı biriyle iletişim?**

A: Lütfen başvurun [ ssediscussions@microsoft.com ](mailto:ssediscussions@microsoft.com) tooStorage hizmeti şifreleme herhangi bir sorunla ilgili. 

## <a name="next-steps"></a>Sonraki adımlar

*   Hello kapsamlı güvenlik hakkında daha fazla bilgi için geliştiricilerin yetenekleri güvenli uygulamaları oluşturmak, lütfen hello bakın [depolama Güvenlik Kılavuzu](https://docs.microsoft.com/en-us/azure/storage/storage-security-guide).
*   Azure anahtar kasası hakkında genel bilgi için bkz: [Azure anahtar kasası nedir](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)?
*   Azure anahtar kasası kullanmaya başlama için bkz: [Azure anahtar kasası ile çalışmaya başlama](../key-vault/key-vault-get-started.md).
