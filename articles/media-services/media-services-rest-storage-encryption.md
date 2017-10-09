---
title: "aaaEncrypting içeriğinizi AMS REST API kullanarak depolama şifrelemesi ile"
description: "Bilgi nasıl tooencrypt içeriğinizi AMS REST API'lerini kullanarak depolama şifrelemesi ile."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: d5f8cb8dd1dcded76c9fededccc772d8102ccbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="5945b-103">İçeriğinizi depolama şifrelemesi ile şifreleme</span><span class="sxs-lookup"><span data-stu-id="5945b-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="5945b-104">Tooencrypt önerilir yerel olarak AES 256 kullanarak içeriğinizi bit şifrelemesi ve tooAzure bunu depolanacağı depolama şifrelenen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5945b-104">It is highly recommended tooencrypt your content locally using AES-256 bit encryption and then upload it tooAzure Storage where it will be stored encrypted at rest.</span></span>

<span data-ttu-id="5945b-105">Bu makalede AMS depolama şifrelemesi genel bir bakış sunar ve nasıl tooupload hello depolama içeriğin şifreli gösterir:</span><span class="sxs-lookup"><span data-stu-id="5945b-105">This article gives an overview of AMS storage encryption and shows you how tooupload hello storage encrypted content:</span></span>

* <span data-ttu-id="5945b-106">Bir içerik anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5945b-106">Create a content key.</span></span>
* <span data-ttu-id="5945b-107">Bir varlık oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5945b-107">Create an Asset.</span></span> <span data-ttu-id="5945b-108">Merhaba AssetCreationOption tooStorageEncryption hello varlık oluştururken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5945b-108">Set hello AssetCreationOption tooStorageEncryption when creating hello Asset.</span></span>
  
     <span data-ttu-id="5945b-109">Şifrelenmiş varlıklar içerik anahtarlarla ilişkili toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="5945b-109">Encrypted assets have toobe associated with content keys.</span></span>
* <span data-ttu-id="5945b-110">Bağlantı hello içerik anahtar toohello varlığı.</span><span class="sxs-lookup"><span data-stu-id="5945b-110">Link hello content key toohello asset.</span></span>  
* <span data-ttu-id="5945b-111">Ayarlama hello şifreleme ilgili hello AssetFile varlıklar üzerinde parametreleri.</span><span class="sxs-lookup"><span data-stu-id="5945b-111">Set hello encryption related parameters on hello AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="5945b-112">Dikkat edilmesi gerekenler</span><span class="sxs-lookup"><span data-stu-id="5945b-112">Considerations</span></span> 

<span data-ttu-id="5945b-113">Toodeliver depolama şifrelenmiş varlık isterseniz hello varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5945b-113">If you want toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy.</span></span> <span data-ttu-id="5945b-114">Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini belirtilen.</span><span class="sxs-lookup"><span data-stu-id="5945b-114">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy.</span></span> <span data-ttu-id="5945b-115">Daha fazla bilgi için bkz: [varlık teslim ilkeleri yapılandırma](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="5945b-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="5945b-116">Varlıklar Media Services erişirken, HTTP istekleri özel üstbilgi alanlarını ve değerlerini ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5945b-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="5945b-117">Daha fazla bilgi için bkz: [Media Services REST API geliştirme için Kurulum](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="5945b-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

## <a name="connect-toomedia-services"></a><span data-ttu-id="5945b-118">TooMedia Hizmetleri'ne Bağlama</span><span class="sxs-lookup"><span data-stu-id="5945b-118">Connect tooMedia Services</span></span>

<span data-ttu-id="5945b-119">Nasıl tooconnect toohello AMS API, bkz. bilgi [Azure AD kimlik doğrulaması ile erişim hello Azure Media Services API](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5945b-119">For information on how tooconnect toohello AMS API, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

>[!NOTE]
><span data-ttu-id="5945b-120">Başarıyla toohttps://media.windows.net bağladıktan sonra başka bir Media Services URI belirleme 301 bir yeniden yönlendirme alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5945b-120">After successfully connecting toohttps://media.windows.net, you will receive a 301 redirect specifying another Media Services URI.</span></span> <span data-ttu-id="5945b-121">Sonraki çağrılar toohello yapmanız gereken yeni bir URI.</span><span class="sxs-lookup"><span data-stu-id="5945b-121">You must make subsequent calls toohello new URI.</span></span>

## <a name="storage-encryption-overview"></a><span data-ttu-id="5945b-122">Depolama Şifrelemesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="5945b-122">Storage encryption overview</span></span>
<span data-ttu-id="5945b-123">Merhaba AMS depolama şifrelemesi uygulayan **AES CTRL** mod şifreleme toohello tüm dosyası.</span><span class="sxs-lookup"><span data-stu-id="5945b-123">hello AMS storage encryption applies **AES-CTR** mode encryption toohello entire file.</span></span>  <span data-ttu-id="5945b-124">AES-CTRL, rastgele uzunlukta verileri doldurma gerek kalmadan şifreleyebilirsiniz bir blok şifreleme modudur.</span><span class="sxs-lookup"><span data-stu-id="5945b-124">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="5945b-125">Merhaba AES algoritması ve ardından XOR lık hello çıktısını AES hello veri tooencrypt sahip olan bir sayaç bloğun şifreleyerek çalışır veya şifrelerini çözme.</span><span class="sxs-lookup"><span data-stu-id="5945b-125">It operates by encrypting a counter block with hello AES algorithm and then XOR-ing hello output of AES with hello data tooencrypt or decrypt.</span></span>  <span data-ttu-id="5945b-126">kullanılan hello sayaç blok hello InitializationVector toobytes 0 too7 hello sayaç değerinin hello değerini kopyalayarak oluşturulur ve 8 bayt too15 hello sayaç değerinin toozero ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5945b-126">hello counter block used is constructed by copying hello value of hello InitializationVector toobytes 0 too7 of hello counter value and bytes 8 too15 of hello counter value are set toozero.</span></span> <span data-ttu-id="5945b-127">Merhaba 16 bayt sayacı bloğunun, 8 bayt too15 (yani hello en az önemli bayt), bir sonraki her işlenen veri bloğu için artar ve bir basit 64 bit işaretsiz tamsayıyı ağ bayt sırasında tutulan olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5945b-127">Of hello 16 byte counter block, bytes 8 too15 (i.e. hello least significant bytes) are used as a simple 64 bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="5945b-128">Bu tamsayı, artan hello en büyük değeri (0xFFFFFFFFFFFFFFFF) ulaşırsa hello sayacın (yani 0 bayt too7) 64 bit hello diğer etkilemeden hello blok sayaç toozero (8 bayt too15) sıfırlar unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5945b-128">Note that if this integer reaches hello maximum value (0xFFFFFFFFFFFFFFFF) then incrementing it resets hello block counter toozero (bytes 8 too15) without affecting hello other 64 bits of hello counter (i.e. bytes 0 too7).</span></span>   <span data-ttu-id="5945b-129">Sipariş toomaintain hello güvenlik hello AES CTRL modu şifreleme her içerik anahtarı her dosya için benzersiz olacaktır için InitializationVector değeri için belirtilen bir anahtarı tanımlayıcı hello ve dosyaları 2'den olacaktır ^ uzunluğu 64 engeller.</span><span class="sxs-lookup"><span data-stu-id="5945b-129">In order toomaintain hello security of hello AES-CTR mode encryption, hello InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="5945b-130">Hiçbir zaman bir sayaç değeri olan tooensure budur verilen anahtarla yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5945b-130">This is tooensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="5945b-131">Merhaba CTRL modu hakkında daha fazla bilgi için bkz: [Bu wiki sayfa](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (Merhaba wiki makalesi kullanır hello terimi "InitializationVector" yerine "Nonce").</span><span class="sxs-lookup"><span data-stu-id="5945b-131">For more information about hello CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (hello wiki article uses hello term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="5945b-132">Kullanım **depolama şifreleme** tooencrypt AES 256 kullanarak yerel olarak Temizle içeriğinizi bit şifrelemesi ve tooAzure depolanır depolama şifrelenen yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5945b-132">Use **Storage Encryption** tooencrypt your clear content locally using AES-256 bit encryption and then upload it tooAzure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="5945b-133">Depolama şifrelemesi ile korunan varlıklar otomatik olarak şifrelenmemiş ve bir şifrelenmiş dosya sistemi önceki tooencoding ve yeni bir çıkış varlığı olarak geri isteğe bağlı olarak yeniden şifrelenmiş önceki toouploading yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5945b-133">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior tooencoding, and optionally re-encrypted prior toouploading back as a new output asset.</span></span> <span data-ttu-id="5945b-134">Depolama şifrelemesinin birincil kullanım durumu hello yüksek kaliteli giriş medya dosyalarınızın güçlü şifrelemeyle diskte rest toosecure istediğiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="5945b-134">hello primary use case for storage encryption is when you want toosecure your high quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="5945b-135">Sipariş toodeliver depolama şifrelenmiş varlık'da, Media Services toodeliver içeriğinizi nasıl istediğiniz bilmesi için hello varlığın teslim ilkesini yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5945b-135">In order toodeliver a storage encrypted asset, you must configure hello asset’s delivery policy so Media Services knows how you want toodeliver your content.</span></span> <span data-ttu-id="5945b-136">Varlığınızı akışı önce sunucu kaldırır hello depolama şifrelemesi ve akışlar hello kullanarak içeriğinizi akış hello teslim ilkesini (örneğin, AES, ortak şifreleme veya şifreleme) belirtildi.</span><span class="sxs-lookup"><span data-stu-id="5945b-136">Before your asset can be streamed, hello streaming server removes hello storage encryption and streams your content using hello specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="5945b-137">Şifreleme için kullanılan ContentKeys oluşturma</span><span class="sxs-lookup"><span data-stu-id="5945b-137">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="5945b-138">Şifrelenmiş varlıklar depolama şifreleme anahtarıyla ilişkili toobe sahip.</span><span class="sxs-lookup"><span data-stu-id="5945b-138">Encrypted assets have toobe associated with Storage Encryption key.</span></span> <span data-ttu-id="5945b-139">Merhaba içerik anahtar toobe hello varlık dosyaları oluşturmadan önce şifreleme için kullanılan oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5945b-139">You must create hello content key toobe used for encryption before creating hello asset files.</span></span> <span data-ttu-id="5945b-140">Bu bölümde açıklanmıştır nasıl toocreate bir içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5945b-140">This section describes how toocreate a content key.</span></span>

<span data-ttu-id="5945b-141">Merhaba şifrelenmiş toobe istediğiniz varlıklarla ilişkilendireceğiniz içerik anahtarları oluşturmak için genel adımlar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5945b-141">hello following are general steps for generating content keys that you will associate with assets that you want toobe encrypted.</span></span> 

1. <span data-ttu-id="5945b-142">Depolama şifrelemesi için rastgele bir 32 baytlık AES anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5945b-142">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="5945b-143">Bu ilişkili tüm dosyalar anlamına gelir, varlık için içerik anahtarı hello olacaktır, varlıkla toouse aynı içerik anahtarı şifre çözme sırasında hello.</span><span class="sxs-lookup"><span data-stu-id="5945b-143">This will be hello content key for your asset, which means all files associated with that asset will need toouse hello same content key during decryption.</span></span> 
2. <span data-ttu-id="5945b-144">Merhaba çağrısı [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) ve [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) yöntemleri tooget hello kullanılan tooencrypt olmalıdır doğru X.509 sertifikası, içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5945b-144">Call hello [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods tooget hello correct X.509 Certificate that must be used tooencrypt your content key.</span></span>
3. <span data-ttu-id="5945b-145">İçerik hello X.509 sertifikasının ortak anahtarı hello anahtarınızla şifreleyin.</span><span class="sxs-lookup"><span data-stu-id="5945b-145">Encrypt your content key with hello public key of hello X.509 Certificate.</span></span> 
   
   <span data-ttu-id="5945b-146">Media Services .NET SDK'sı ile OAEP hello şifreleme yaparken RSA kullanır.</span><span class="sxs-lookup"><span data-stu-id="5945b-146">Media Services .NET SDK uses RSA with OAEP when doing hello encryption.</span></span>  <span data-ttu-id="5945b-147">Merhaba .NET örnekte görebilirsiniz [EncryptSymmetricKeyData işlevi](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="5945b-147">You can see a .NET example in hello [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="5945b-148">Başlangıç anahtarı tanımlayıcısı ve içerik anahtarı kullanılarak hesaplanan bir sağlama toplamı değeri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5945b-148">Create a checksum value calculated using hello key identifier and content key.</span></span> <span data-ttu-id="5945b-149">.NET örnek aşağıdaki hello hello sağlama toplamı hello GUID hello anahtarı tanımlayıcısı bir kısmını kullanarak hesaplar ve hello içerik anahtarı temizleyin.</span><span class="sxs-lookup"><span data-stu-id="5945b-149">hello following .NET example calculates hello checksum using hello GUID part of hello key identifier and hello clear content key.</span></span>

        public static string CalculateChecksum(byte[] contentKey, Guid keyId)
        {
            const int ChecksumLength = 8;
            const int KeyIdLength = 16;

            byte[] encryptedKeyId = null;

            // Checksum is computed by AES-ECB encrypting hello KID
            // with hello content key.
            using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
            {
                rijndael.Mode = CipherMode.ECB;
                rijndael.Key = contentKey;
                rijndael.Padding = PaddingMode.None;

                ICryptoTransform encryptor = rijndael.CreateEncryptor();
                encryptedKeyId = new byte[KeyIdLength];
                encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
            }

            byte[] retVal = new byte[ChecksumLength];
            Array.Copy(encryptedKeyId, retVal, ChecksumLength);

            return Convert.ToBase64String(retVal);
        }

1. <span data-ttu-id="5945b-150">Merhaba ile Merhaba içerik anahtarı oluşturun **EncryptedContentKey** (toobase64 kodlu dize dönüştürülen), **ProtectionKeyId**, **ProtectionKeyType**,  **ContentKeyType**, ve **sağlama toplamı** önceki adımlarda almış değerleri.</span><span class="sxs-lookup"><span data-stu-id="5945b-150">Create hello Content key with hello **EncryptedContentKey** (converted toobase64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="5945b-151">Depolama şifrelemesi için hello aşağıdaki özellikleri hello istek gövdesinde yer alması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5945b-151">For storage encryption, hello following properties should be included in hello request body.</span></span>

    <span data-ttu-id="5945b-152">İstek gövdesi özelliği</span><span class="sxs-lookup"><span data-stu-id="5945b-152">Request body property</span></span>    | <span data-ttu-id="5945b-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5945b-153">Description</span></span>
    ---|---
    <span data-ttu-id="5945b-154">Kimlik</span><span class="sxs-lookup"><span data-stu-id="5945b-154">Id</span></span> | <span data-ttu-id="5945b-155">Merhaba biz oluşturan ContentKey kimliği kendisini izleyen hello kullanarak biçimi, "nb:kid:UUID:<NEW GUID>".</span><span class="sxs-lookup"><span data-stu-id="5945b-155">hello ContentKey Id which we generate ourselves using hello following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="5945b-156">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="5945b-156">ContentKeyType</span></span> | <span data-ttu-id="5945b-157">Bu içerik anahtarı için bir tamsayı olarak hello içerik anahtar türü budur.</span><span class="sxs-lookup"><span data-stu-id="5945b-157">This is hello content key type as an integer for this content key.</span></span> <span data-ttu-id="5945b-158">Biz depolama şifrelemesi için 1 hello değeri geçirin.</span><span class="sxs-lookup"><span data-stu-id="5945b-158">We pass hello value 1 for storage encryption.</span></span>
    <span data-ttu-id="5945b-159">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="5945b-159">EncryptedContentKey</span></span> | <span data-ttu-id="5945b-160">256 bitlik (32 bayt) bir değer olan yeni bir içerik anahtarı değeri oluşturuyoruz.</span><span class="sxs-lookup"><span data-stu-id="5945b-160">We create a new content key value which is a 256-bit (32 byte) value.</span></span> <span data-ttu-id="5945b-161">başlangıç anahtarı hello GetProtectionKeyId ve GetProtectionKey yöntemleri için bir HTTP GET isteği yürüterek Microsoft Azure Media Services'den alıyoruz hello depolama şifreleme X.509 sertifikası kullanılarak şifrelenir.</span><span class="sxs-lookup"><span data-stu-id="5945b-161">hello key is encrypted using hello storage encryption X.509 certificate which we retrieve from Microsoft Azure Media Services by executing a HTTP GET request for hello GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="5945b-162">.NET kodu aşağıdaki hello bir örnek olarak bkz: Merhaba **EncryptSymmetricKeyData** tanımlanan yöntemi [burada](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="5945b-162">As an example, see hello following .NET code: hello  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="5945b-163">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="5945b-163">ProtectionKeyId</span></span> | <span data-ttu-id="5945b-164">Bu olduğu hello koruma anahtar kimliği için kullanılan tooencrypt edildi hello depolama şifreleme X.509 sertifikası bizim içerik anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5945b-164">This is hello protection key id for hello storage encryption X.509 certificate that was used tooencrypt our content key.</span></span>
    <span data-ttu-id="5945b-165">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="5945b-165">ProtectionKeyType</span></span> | <span data-ttu-id="5945b-166">Bu hello şifreleme için kullanılan tooencrypt hello içerik anahtar: hello koruma anahtarı türüdür.</span><span class="sxs-lookup"><span data-stu-id="5945b-166">This is hello encryption type for hello protection key that was used tooencrypt hello content key.</span></span> <span data-ttu-id="5945b-167">Bu değer StorageEncryption(1) Bizim örneğimizde olur.</span><span class="sxs-lookup"><span data-stu-id="5945b-167">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="5945b-168">Sağlama toplamı</span><span class="sxs-lookup"><span data-stu-id="5945b-168">Checksum</span></span> |<span data-ttu-id="5945b-169">Merhaba MD5 hello içerik anahtarı için hesaplanan sağlama.</span><span class="sxs-lookup"><span data-stu-id="5945b-169">hello MD5 calculated checksum for hello content key.</span></span> <span data-ttu-id="5945b-170">Merhaba içerik anahtarı kimliği içerikle hello şifreleyerek hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="5945b-170">It is computed by encrypting hello content Id with hello content key.</span></span> <span data-ttu-id="5945b-171">Merhaba örnek kodu nasıl toocalculate hello sağlama toplamı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5945b-171">hello example code demonstrates how toocalculate hello checksum.</span></span>


### <a name="retrieve-hello-protectionkeyid"></a><span data-ttu-id="5945b-172">Merhaba ProtectionKeyId alma</span><span class="sxs-lookup"><span data-stu-id="5945b-172">Retrieve hello ProtectionKeyId</span></span>
<span data-ttu-id="5945b-173">Aşağıdaki örnek hello nasıl tooretrieve hello ProtectionKeyId, hello sertifika içerik anahtarınızı şifrelerken kullanmak için bir sertifika parmak izini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5945b-173">hello following example shows how tooretrieve hello ProtectionKeyId, a certificate thumbprint, for hello certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="5945b-174">Bu adım toomake makinenizde hello uygun sertifika zaten sahip olduğunuzdan emin yapın.</span><span class="sxs-lookup"><span data-stu-id="5945b-174">Do this step toomake sure that you already have hello appropriate certificate on your machine.</span></span>

<span data-ttu-id="5945b-175">İsteği:</span><span class="sxs-lookup"><span data-stu-id="5945b-175">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net

<span data-ttu-id="5945b-176">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="5945b-176">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-hello-protectionkey-for-hello-protectionkeyid"></a><span data-ttu-id="5945b-177">Merhaba ProtectionKey hello ProtectionKeyId alma</span><span class="sxs-lookup"><span data-stu-id="5945b-177">Retrieve hello ProtectionKey for hello ProtectionKeyId</span></span>
<span data-ttu-id="5945b-178">Merhaba aşağıdaki örnekte nasıl hello ProtectionKeyId kullanarak tooretrieve hello X.509 sertifikası hello önceki adımda aldığınız gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5945b-178">hello following example shows how tooretrieve hello X.509 certificate using hello ProtectionKeyId you received in hello previous step.</span></span>

<span data-ttu-id="5945b-179">İsteği:</span><span class="sxs-lookup"><span data-stu-id="5945b-179">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="5945b-180">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="5945b-180">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-hello-content-key"></a><span data-ttu-id="5945b-181">Merhaba içerik anahtarı oluşturun</span><span class="sxs-lookup"><span data-stu-id="5945b-181">Create hello content key</span></span>
<span data-ttu-id="5945b-182">Merhaba X.509 sertifikası alınır ve kendi ortak anahtar tooencrypt içerik anahtarınızı kullanılan sonra oluşturmanız bir **ContentKey** varlık ve onun özellik değerlerinin buna uygun olarak ayarla.</span><span class="sxs-lookup"><span data-stu-id="5945b-182">After you have retrieved hello X.509 certificate and used its public key tooencrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="5945b-183">Ne zaman ayarlamalısınız hello değerlerden biri hello hello türü anahtarıdır içerik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5945b-183">One of hello values that you must set when create hello content key is hello type.</span></span> <span data-ttu-id="5945b-184">Merhaba depolama şifrelemesi durumunda hello '1' değeridir.</span><span class="sxs-lookup"><span data-stu-id="5945b-184">In case of hello storage encryption, hello value is '1'.</span></span> 

<span data-ttu-id="5945b-185">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir **ContentKey** ile bir **ContentKeyType** depolama şifreleme ("1") ve hello için ayarladığınız **ProtectionKeyType** Ayarla "0" çok koruma anahtarı kimliği hello tooindicate hello X.509 sertifika parmak izi ' dir.</span><span class="sxs-lookup"><span data-stu-id="5945b-185">hello following example shows how toocreate a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and hello **ProtectionKeyType** set too"0" tooindicate that hello protection key Id is hello X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="5945b-186">İstek</span><span class="sxs-lookup"><span data-stu-id="5945b-186">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.11
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="5945b-187">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="5945b-187">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="5945b-188">Bir varlık oluşturun</span><span class="sxs-lookup"><span data-stu-id="5945b-188">Create an asset</span></span>
<span data-ttu-id="5945b-189">örnekte gösterildiği nasıl aşağıdaki hello toocreate bir varlık.</span><span class="sxs-lookup"><span data-stu-id="5945b-189">hello following example shows how toocreate an asset.</span></span>

<span data-ttu-id="5945b-190">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5945b-190">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="5945b-191">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5945b-191">**HTTP Response**</span></span>

<span data-ttu-id="5945b-192">Başarılı olursa, hello aşağıdaki verilir:</span><span class="sxs-lookup"><span data-stu-id="5945b-192">If successful, hello following is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-hello-contentkey-with-an-asset"></a><span data-ttu-id="5945b-193">Merhaba ContentKey bir varlıkla ilişkilendirme</span><span class="sxs-lookup"><span data-stu-id="5945b-193">Associate hello ContentKey with an Asset</span></span>
<span data-ttu-id="5945b-194">Merhaba ContentKey oluşturduktan sonra hello aşağıdaki örnekte gösterildiği gibi hello $links işlemi kullanarak, varlık ile ilişkilendirin:</span><span class="sxs-lookup"><span data-stu-id="5945b-194">After creating hello ContentKey, associate it with your Asset using hello $links operation, as shown in hello following example:</span></span>

<span data-ttu-id="5945b-195">İsteği:</span><span class="sxs-lookup"><span data-stu-id="5945b-195">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.11
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="5945b-196">Yanıtı:</span><span class="sxs-lookup"><span data-stu-id="5945b-196">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="5945b-197">Bir AssetFile oluşturma</span><span class="sxs-lookup"><span data-stu-id="5945b-197">Create an AssetFile</span></span>
<span data-ttu-id="5945b-198">Merhaba [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) varlığı temsil eden bir blob kapsayıcısında depolanır ses veya video dosyası.</span><span class="sxs-lookup"><span data-stu-id="5945b-198">hello [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="5945b-199">Bir varlık dosyası her zaman bir varlıkla ilişkilidir ve bir varlığı bir veya daha çok varlık dosyaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5945b-199">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="5945b-200">bir varlık dosyası nesne bir blob kapsayıcısında dijital bir dosyayla ilişkili değilse hello Media Services Kodlayıcısı görev başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="5945b-200">hello Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="5945b-201">Bu hello Not **AssetFile** örneği ve hello gerçek medya dosyası olan iki farklı nesneler.</span><span class="sxs-lookup"><span data-stu-id="5945b-201">Note that hello **AssetFile** instance and hello actual media file are two distinct objects.</span></span> <span data-ttu-id="5945b-202">Merhaba medya dosyası hello gerçek medya içeriği içerirken hello AssetFile örneği hello medya dosyası hakkındaki meta verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="5945b-202">hello AssetFile instance contains metadata about hello media file, while hello media file contains hello actual media content.</span></span>

<span data-ttu-id="5945b-203">Bir blob kapsayıcıya bir dijital medyayı dosyanızı karşıya sonra hello kullanacağı **birleştirme** medya dosyanızın (Bu konuda gösterilmez) hakkında bilgi içeren HTTP isteği tooupdate hello AssetFile.</span><span class="sxs-lookup"><span data-stu-id="5945b-203">After you upload your digital media file into a blob container, you will use hello **MERGE** HTTP request tooupdate hello AssetFile with information about your media file (not shown in this topic).</span></span> 

<span data-ttu-id="5945b-204">**HTTP isteği**</span><span class="sxs-lookup"><span data-stu-id="5945b-204">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.11
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="5945b-205">**HTTP yanıtı**</span><span class="sxs-lookup"><span data-stu-id="5945b-205">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
