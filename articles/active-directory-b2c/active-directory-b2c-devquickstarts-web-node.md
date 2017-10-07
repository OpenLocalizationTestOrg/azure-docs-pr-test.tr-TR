---
title: "Azure B2C için aaaAdd oturum açma tooa Node.js web uygulaması | Microsoft Docs"
description: "Nasıl toobuild bir Node.js web uygulaması, kullanıcıların bir B2C kiracısı kullanarak imzalar."
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: b4c334b1f7a0669df2d0864140603dc55bbb5408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-add-sign-in-tooa-nodejs-web-app"></a>Azure AD B2C: oturum açma tooa Node.js web uygulaması Ekle

**Passport**, Node.js için kimlik doğrulama ara yazılımıdır. Son derece esnek ve modüler olan Passport, Express tabanlı veya Restify web uygulamasına sorunsuz bir şekilde yüklenebilir. Bir dizi kapsamlı strateji; bir kullanıcı adı ve parola, Facebook, Twitter ve daha fazlası ile kimlik doğrulamasını destekler.

Azure Active Directory (Azure AD) için bir strateji geliştirdik. Bu modülü yükleyin ve ardından hello Azure AD ekleyin `passport-azure-ad` eklentisi.

toodo bunu yapmanız:

1. Bir uygulamayı Azure AD kullanarak kaydedin.
2. Uygulama toouse hello ayarlamak `passport-azure-ad` eklentisi.
3. Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın.
4. Kullanıcı verilerini yazdırın.

Bu öğretici için kod Hello [Github'da korunur](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS). yapabilecekleriniz toofollow boyunca [hello uygulamanın çatısını bir .zip dosyası karşıdan](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip). Ayrıca hello çatıyı kopyalayabilirsiniz:

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

Tamamlanan Merhaba uygulaması hello Bu öğreticinin sonunda sağlanır.

## <a name="get-an-azure-ad-b2c-directory"></a>Azure AD B2C dizini alma

Azure AD B2C'yi kullanabilmek için önce dizin veya kiracı oluşturmanız gerekir.  Dizin; tüm kullanıcılarınız, uygulamalarınız, gruplarınız ve daha fazlası için bir kapsayıcıdır. Henüz yoksa devam etmeden önce bu kılavuzda [bir B2C dizini oluşturun](active-directory-b2c-get-started.md).

## <a name="create-an-application"></a>Uygulama oluşturma

Ardından B2C dizininizde uygulama toocreate gerekir. Bu, uygulamanız ile güvenli toocommunicate gereken bilgileri Azure AD'ye verir. Hem istemci uygulaması hello ve web API tarafından tek bir temsil **uygulama kimliği**, bir mantıksal uygulama içerdikleri için. Uygulama, bir toocreate izleyin [bu yönergeleri](active-directory-b2c-app-registration.md). Şunları yaptığınızdan emin olun:

- Dahil bir **web uygulaması**/**web API'si** hello uygulamada.
- **Yanıt URL'si** olarak `http://localhost:3000/auth/openid/return` adresini girin. Bu kod örneği için hello varsayılan URL değil.
- Uygulamanız için bir **Uygulama gizli anahtarı** oluşturun ve bunu kopyalayın. Buna daha sonra ihtiyacınız olacak. Bu değer toobe gerektiğini Not [XML kaçışlı](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) kullanmadan önce.
- Kopya hello **uygulama kimliği** diğer bir deyişle atanan tooyour uygulama. Buna da daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a>İlkelerinizi oluşturma

Azure AD B2C'de her kullanıcı deneyimi, bir [ilke](active-directory-b2c-reference-policies.md) ile tanımlanır. Bu uygulama üç kimlik deneyimi içerir: Kaydolma, oturum açma ve Facebook ile oturum açma. Toocreate açıklandığı gibi her tür Bu ilkeyi gereken [ilke başvurusu makalesinde](active-directory-b2c-reference-policies.md#create-a-sign-up-policy). Üç ilkenizi oluştururken şunları yaptığınızdan emin olun:

- Merhaba seçin **görünen adı** ve diğer kaydolma özniteliklerini kaydolma ilkenizde.
- Merhaba seçin **görünen adı** ve **nesne kimliği** her ilkede uygulamanın talep. Diğer talepleri de seçebilirsiniz.
- Kopya hello **adı** oluşturduktan sonra her ilkenin. Merhaba önekine sahip olmalıdır `b2c_1_`.  Bu ilke adlarına daha sonra ihtiyacınız olacak.

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

Üç ilkenizi oluşturduktan sonra hazır toobuild olduğunuz uygulamanızı.

Bu makalenin nasıl toouse hello ilkeleri oluşturduğunuz kapsamadığını unutmayın. toolearn ile Merhaba ilkelerinin Azure AD B2C'de nasıl çalıştığı hakkında başlangıç [.NET web uygulamasıyla çalışmaya başlama Öğreticisi](active-directory-b2c-devquickstarts-web-dotnet.md).

## <a name="add-prerequisites-tooyour-directory"></a>Önkoşullar tooyour Dizin Ekle

Zaten orada değilseniz hello komut satırında, dizinleri tooyour kök klasörü değiştirin. Merhaba aşağıdaki komutları çalıştırın:

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

Ayrıca, kullandık `passport-azure-ad` bizim önizlemede hello hello hızlı başlangıç çatısında önizlememiz için.

- `npm install passport-azure-ad`

Bu hello kitaplıkları yükleyecek, `passport-azure-ad` bağlıdır.

## <a name="set-up-your-app-toouse-hello-passport-nodejs-strategy"></a>Uygulama toouse hello Passport Node.js stratejisi ayarlayın
Merhaba Express ara yazılım toouse hello Openıd Connect kimlik doğrulama protokolü yapılandırın. Passport oturum açma ve oturum kapatma isteklerini kullanılan tooissue olması, kullanıcı oturumlarını yönetmek ve diğer eylemler boyunca kullanıcılar hakkında bilgi alın.

Açık hello `config.js` hello proje hello kökünde bulunan dosya ve hello uygulamanızın yapılandırma değerlerini girin `exports.creds` bölümü.
- `clientID`: Merhaba **uygulama kimliği** tooyour uygulama hello kayıt Portalı'nda atanmış.
- `returnURL`: Merhaba **yeniden yönlendirme URI'si** hello portalda girdiğiniz.
- `tenantName`: hello Kiracı adı, bu gibi bir durumda uygulamanızın **contoso.onmicrosoft.com**.

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Açık hello `app.js` hello hello proje kökündeki dosyasında. Çağrı tooinvoke hello aşağıdaki hello eklemek `OIDCStrategy` birlikte stratejisi `passport-azure-ad`.


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

Yalnızca toohandle oturum açma isteklerini başvurulan hello stratejiyi kullanın.

```JavaScript
// Use hello OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
Passport, tüm stratejileri (Twitter ve Facebook dahil) için benzer bir desen kullanır. Tüm strateji yazıcıları toothis düzeni uyması. Merhaba stratejisi baktığınızda geçirdiğinizi görebilirsiniz bir `function()` belirtece sahip ve bir `done` hello parametre olarak. tüm işlemlerini tamamladıktan sonra hello stratejisi tooyou gelir. Merhaba kullanıcı saklayabilir ve böylece için yeniden tooask gerekmeyen hello belirteci kaydedin;.

> [!IMPORTANT]
Merhaba önceki kod hello kimlik doğrulamasını tüm kullanıcıları alır. Bu otomatik kayıttır. Üretim sunucularını kullandığınızda, ayarladığınız kayıt işlemiyle ilerlemiş sürece kullanıcılar toolet istemezsiniz. Tüketici uygulamalarında bu deseni sıkça görebilirsiniz. Bunlar, tooregister Facebook kullanarak izin verir, ancak ek bilgiler toofill bunlar isteyin sonra. Uygulamamız bir örnek olmasaydı, biz döndürülen hello belirteç nesnesinden bir e-posta adresi ayıklayın ve ardından ek bilgi hello kullanıcı toofill isteyin. Bu bir test sunucusu olduğundan, biz kullanıcıların toohello bellek içi veritabanına eklemeniz yeterlidir.

Tookeep izleme, oturum açmış kullanıcıların izin hello yöntemler ekleyen Passport'un gerektirdiği gibi. Bu, kullanıcı bilgilerini serileştirmeyi ve seri durumdan çıkarmayı kapsar:

```JavaScript

// Passport session setup. (Section 2)

//   toosupport persistent sign-in sessions, Passport needs toobe able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing hello user ID when Passport serializes a user
//   and finding hello user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array toohold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

Merhaba kod tooload hello Express altyapısını ekleyin. Merhaba aşağıdakileri hello varsayılan kullandığımızı görebilirsiniz `/views` ve `/routes` Express'in sağladığı düzeni.

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware toosupport
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

Merhaba eklemek `POST` kapalı el yollar hello gerçek oturum açma isteklerini toohello `passport-azure-ad` altyapısı:

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. hello first step in OpenID authentication involves redirecting
//   hello user tooan OpenID provider. After hello user is authenticated,
//   hello OpenID provider redirects hello user back toothis application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in hello Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it redirects hello user toohello home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware tooauthenticate the
//   request. If authentication fails, hello user will be redirected back toothe
//   sign-in page. Otherwise, hello primary route function will be called.
//   In this example, it will redirect hello user toohello home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-tooissue-sign-in-and-sign-out-requests-tooazure-ad"></a>Passport tooissue oturum açma ve oturum kapatma isteklerini tooAzure AD kullanın

Uygulamanızı hello v2.0 uç noktası ile düzgün şekilde yapılandırılmış toocommunicate hello Openıd Connect kimlik doğrulama protokolü kullanarak sunulmuştur. `passport-azure-ad`alınan kimlik doğrulama iletileri hazırlayın, Azure AD'den belirteçleri doğrulamak ve kullanıcı oturumu koruma hello ayrıntılarını önemli. Tüm bu kalır, kullanıcılarınızın toogive olan bir şekilde toosign ve oturum out ve toogather açan kullanıcılar hakkında ek bilgi.

İlk olarak, hello varsayılan, oturum açma, hesap ve oturum kapatma yöntemlerini tooyour ekleyin `app.js` dosyası:

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in hello Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

tooreview bu yöntemleri ayrıntılı:
- Merhaba `/` rota yönlendiren toohello `index.ejs` (varsa) geçirerek hello kullanıcı hello istekte görünümü.
- Merhaba `/account` rota ilk doğrular, doğrulanır (Bu aşağıda için uygulama hello). Böylece hello kullanıcı hakkında ek bilgi alabilir hello istekte sonra hello kullanıcı geçirir.
- Merhaba `/login` rota çağrıları hello `azuread-openidconnect` doğrulayıcıdan `passport-azure-ad`. İşlemi başarılı değil, hello rota hello kullanıcı geri çok yönlendiren`/login`.
- `/logout` yalnızca `logout.ejs` öğesini (ve yolunu) çağırır. Bu tanımlama bilgilerini temizler ve ardından döndürür kullanıcı geri çok hello`index.ejs`.


Merhaba son kısmı için `app.js`, hello eklemek `EnsureAuthenticated` hello yöntemi `/account` rota.

```JavaScript

// Simple route middleware tooensure that hello user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs toobe protected. If
//   hello request is authenticated (typically via a persistent sign-in session),
//   then hello request will proceed. Otherwise, hello user will be redirected toothe
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

Son olarak, hello sunucusu kendisini oluşturmak içinde `app.js`.

```JavaScript

app.listen(3000);

```


## <a name="create-hello-views-and-routes-in-express-toocall-your-policies"></a>Merhaba görünümler oluşturabilir ve hızlı toocall ilkelerinizi yönlendirir

Şimdi `app.js` öğeniz tamamlandı. Tooadd hello yollar ve toocall hello oturum açma ve kaydolma ilkeler izin görünümleri yeterlidir. Bunlar ayrıca hello işlemek `/logout` ve `/login` oluşturduğunuz yollar.

Merhaba oluşturmak `/routes/index.js` hello kök dizininin altındaki yol.

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

Merhaba oluşturmak `/routes/user.js` hello kök dizininin altındaki yol.

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

Bu basit yollar istekleri tooyour görünümleri geçirin. Var olan hello kullanıcı içerirler.

Merhaba oluşturmak `/views/index.ejs` hello kök dizininin altında görünümü. Bu, oturum açma ve oturum kapatma için ilkeleri çağıran basit bir sayfadır. Ayrıca toograb hesap bilgileri kullanabilirsiniz. Merhaba koşullu kullanabileceğinizi unutmayın `if (!user)` içinde hello kullanıcı geçirilir gibi hello isteği tooprovide kanıtlayan bilgiler hello kullanıcının oturum.

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

Merhaba oluşturma `/views/account.ejs` ek bilgileri görüntüleyebilmek hello kök dizininin altındaki görüntülemek, `passport-azure-ad` hello kullanıcı isteğine koyulan.

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

Artık uygulamanızı oluşturabilir ve çalıştırabilirsiniz.

Çalıştırma `node app.js` ve çok gidin`http://localhost:3000`


Kaydolma veya e-posta veya Facebook kullanarak toohello uygulamada oturum açın. Oturumu kapatın ve farklı kullanıcı olarak tekrar oturum açın.

##<a name="next-steps"></a>Sonraki adımlar

Başvuru için hello tamamlandı (yapılandırma değerleriniz olmadan) örnek [bir .zip dosyası olarak sağlanan](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip). Aynı zamanda GitHub'dan kopyalayabilirsiniz:

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

Gelişmiş konular toomore üzerinde şimdi taşıyabilirsiniz. Deneyebilecekleriniz:

[Node.js içinde hello B2C modeli kullanarak bir web API güvenliğini sağlama](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on toomore advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing hello your B2C App's UX >>]()

-->
