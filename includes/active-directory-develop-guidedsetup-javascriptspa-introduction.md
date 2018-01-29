# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a>Bir JavaScript tek sayfa uygulama (SPA) Microsoft Graph API çağrısı

Bu kılavuz bir JavaScript tek sayfa uygulama (SPA) kişisel, iş ne kaydolabilirsiniz gösterir ve Okul hesapları, erişim belirteci almak ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırın.

### <a name="how-this-guide-works"></a>Bu kılavuz nasıl çalışır?

![Bu kılavuz tarafından oluşturulan örnek uygulaması nasıl çalışır](media/active-directory-develop-guidedsetup-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a>Daha Fazla Bilgi

Bu kılavuz tarafından oluşturulan örnek uygulamayı Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sorgulamak bir JavaScript SPA sağlar. Bir kullanıcı oturum açtığında, sonra bu senaryo için bir erişim belirteci istenen ve HTTP isteklerini authorization üstbilgisi yoluyla eklenir. Belirteç edinme ve yenileme Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından işlenir.

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a>Kitaplıkları

Bu kılavuz aşağıdaki kitaplığı kullanır:

|Kitaplık|Açıklama|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|JavaScript Önizleme için Microsoft kimlik doğrulama kitaplığı|

> [!NOTE]
> *msal.js* hedefleri *Azure Active Directory v2 endpoint* -oturum açmak ve belirteçleri almak kişisel ve iş, okul hesapları sağlar. *Azure Active Directory v2 endpoint* sahip [bazı sınırlamalar](..\articles\active-directory\develop\active-directory-v2-limitations.md). Yalnızca iş ve Okul hesapları ilgileniyorsanız kullanmak *adal.js* ve *V1 endpoint*. Okuma v1 ve v2 uç noktaları arasındaki farkları anlamak için [v1 v2 karşılaştırma](..\articles\active-directory\develop\active-directory-v2-compare.md).

<!--end-collapse-->
