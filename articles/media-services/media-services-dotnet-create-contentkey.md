---
title: .NET ile ContentKeys aaaCreate
description: "TooAssets nasıl erişim güvenli sağlayan toocreate içerik anahtarları hakkında bilgi edinin."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 35909c64e8393e228be75c464a034ffc40122952
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-contentkeys-with-net"></a>.NET ile ContentKeys oluşturma
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

Media Services toocreate sağlar ve şifrelenmiş varlıklar gönderin. A **ContentKey** güvenli erişim tooyour sağlar **varlık**s. 

Yeni bir varlık oluşturduğunuzda (örneğin, önce [dosyaları karşıya yükleme](media-services-dotnet-upload-files.md)), şifreleme seçenekleri aşağıdaki hello belirtebilirsiniz: **StorageEncrypted**, **CommonEncryptionProtected**, veya **EnvelopeEncryptionProtected**. 

Tooyour istemcileri varlıklar iletirken yapabilecekleriniz [dinamik olarak şifrelenmiş varlıklar toobe için yapılandırma](media-services-dotnet-configure-asset-delivery-policy.md) iki şifrelemeleri aşağıdaki hello biriyle: **DynamicEnvelopeEncryption** veya  **DynamicCommonEncryption**.

Şifrelenmiş varlıklar sahip ilişkili toobe **ContentKey**s. Bu makalede nasıl toocreate bir içerik anahtarı.

> [!NOTE]
> Yeni bir oluştururken **StorageEncrypted** varlık kullanarak hello Media Services .NET SDK hello **ContentKey** otomatik olarak oluşturulan ve hello varlık ile bağlanır.
> 
> 

## <a name="contentkeytype"></a>ContentKeyType
Ne zaman ayarlamalısınız hello değerlerden biri oluşturma içerik anahtarıdır hello içerik anahtar türü. Değerleri aşağıdaki hello birini seçin. 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is hello default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <a id="envelope_contentkey"></a>Zarf türü ContentKey oluşturma
Merhaba aşağıdaki kod parçacığını bir içerik anahtarı hello Zarf şifreleme türü oluşturur. Ardından hello anahtar hello belirtilen varlık ile ilişkilendirir.

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

Arama

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a>Ortak tür ContentKey oluşturma
Merhaba aşağıdaki kod parçacığını bir içerik anahtarı hello ortak şifreleme türü oluşturur. Ardından hello anahtar hello belirtilen varlık ile ilişkilendirir.

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate hello key with hello asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
Arama

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

