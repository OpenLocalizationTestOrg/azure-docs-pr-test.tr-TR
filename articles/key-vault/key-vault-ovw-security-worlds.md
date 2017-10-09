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
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a><span data-ttu-id="43c1c-102">Azure anahtar kasası güvenlik dünyaları ve coğrafi sınırlar</span><span class="sxs-lookup"><span data-stu-id="43c1c-102">Azure Key Vault security worlds and geographic boundaries</span></span>

<span data-ttu-id="43c1c-103">Azure anahtar kasası çok kiracılı bir hizmet olduğundan ve her Azure konumu donanım güvenlik modülleri (HSM'ler) havuzu kullanır.</span><span class="sxs-lookup"><span data-stu-id="43c1c-103">Azure Key Vault is a multi-tenant service and uses a pool of Hardware Security Modules (HSMs) in each Azure location.</span></span> 

<span data-ttu-id="43c1c-104">Tüm HSM'ler aynı coğrafi bölge paylaşımına hello Azure konumlardaki aynı şifreleme sınırı (Thales güvenlik Dünyası) hello.</span><span class="sxs-lookup"><span data-stu-id="43c1c-104">All HSMs at Azure locations in hello same geographic region share hello same cryptographic boundary (Thales Security World).</span></span> <span data-ttu-id="43c1c-105">Toohello ABD coğrafi konuma ait olduğundan Örneğin, Doğu ABD ve Batı ABD paylaşmak aynı güvenlik hello world.</span><span class="sxs-lookup"><span data-stu-id="43c1c-105">For example, East US and West US share hello same security world because they belong toohello US geo location.</span></span> <span data-ttu-id="43c1c-106">Benzer şekilde, tüm Azure konumları Japonya paylaşımda aynı güvenlik dünyası ve Avustralya, Hindistan, tüm Azure konumlarda hello ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="43c1c-106">Similarly, all Azure locations in Japan share hello same security world and all Azure locations in Australia, India, and so on.</span></span> 

## <a name="backup-and-restore-behavior"></a><span data-ttu-id="43c1c-107">Yedekleme ve geri yükleme davranışı</span><span class="sxs-lookup"><span data-stu-id="43c1c-107">Backup and restore behavior</span></span>

<span data-ttu-id="43c1c-108">Bu koşulların her ikisi de doğruysa sürece tooa konumda başka bir Azure anahtar kasası anahtar Azure konumu olabilir birinde bir anahtar Kasası'ndan alınan bir yedeklemeyi geri:</span><span class="sxs-lookup"><span data-stu-id="43c1c-108">A backup taken of a key from a key vault in one Azure location can be restored tooa key vault in another Azure location, as long as both of these conditions are true:</span></span>

- <span data-ttu-id="43c1c-109">Hello Azure her ikisi de konumları ait toohello aynı coğrafi konum</span><span class="sxs-lookup"><span data-stu-id="43c1c-109">Both of hello Azure locations belong toohello same geographical location</span></span>
- <span data-ttu-id="43c1c-110">Merhaba anahtar kasalarını her ikisi de toohello ait aynı Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="43c1c-110">Both of hello key vaults belong toohello same Azure subscription</span></span>

<span data-ttu-id="43c1c-111">Örneğin, belirli bir aboneliğe Batı Hindistan, bir anahtar kasasına bir anahtar tarafından gerçekleştirilecek bir yedekleme yalnızca olabilir hello anahtar kasasına geri yüklenen tooanother aynı abonelikte ve coğrafi konum; Batı Hindistan, Orta Hindistan veya Güney Hindistan.</span><span class="sxs-lookup"><span data-stu-id="43c1c-111">For example, a backup taken by a given subscription of a key in a key vault in West India, can only be restored tooanother key vault in hello same subscription and geo location; West India, Central India or South India.</span></span>

## <a name="regions-and-products"></a><span data-ttu-id="43c1c-112">Bölgeler ve ürünler</span><span class="sxs-lookup"><span data-stu-id="43c1c-112">Regions and products</span></span>

- [<span data-ttu-id="43c1c-113">Azure bölgeleri</span><span class="sxs-lookup"><span data-stu-id="43c1c-113">Azure regions</span></span>](https://azure.microsoft.com/regions/)
- [<span data-ttu-id="43c1c-114">Bölgeye göre Microsoft ürünleri</span><span class="sxs-lookup"><span data-stu-id="43c1c-114">Microsoft products by region</span></span>](https://azure.microsoft.com/regions/services/)

<span data-ttu-id="43c1c-115">Bölgeler hello tablolardaki ana başlıklar olarak gösterilen eşlenen toosecurity dünyaları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="43c1c-115">Regions are mapped toosecurity worlds, shown as major headings in hello tables:</span></span>

<span data-ttu-id="43c1c-116">Örneğin, bölge makale tarafından Hello ürünlerinde hello **Americas** sekmesi içerir Doğu ABD, Orta ABD, Batı ABD tüm eşleme toohello Americas bölge.</span><span class="sxs-lookup"><span data-stu-id="43c1c-116">In hello products by region article, for example, hello **Americas** tab contains EAST US, CENTRAL US, WEST US all mapping toohello Americas region.</span></span> 

>[!NOTE]
><span data-ttu-id="43c1c-117">Bir özel durum BİZE savunma Bakanlığı Doğu ve BİZE savunma Bakanlığı merkezi kendi güvenlik dünyaları olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="43c1c-117">An exception is that US DOD EAST and US DOD CENTRAL have their own security worlds.</span></span> 

<span data-ttu-id="43c1c-118">Benzer şekilde, hello üzerinde **Avrupa** sekmesinde, Kuzey Avrupa ve Batı Avrupa, her ikisi de eşlenir toohello Avrupa bölgesi.</span><span class="sxs-lookup"><span data-stu-id="43c1c-118">Similarly, on hello **Europe** tab, NORTH EUROPE and WEST EUROPE both map toohello Europe region.</span></span> <span data-ttu-id="43c1c-119">Merhaba aynı de hello üzerinde geçerlidir **Asya Pasifik** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="43c1c-119">hello same is also true on hello **Asia Pacific** tab.</span></span>



