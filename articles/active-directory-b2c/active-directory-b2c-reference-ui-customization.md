---
title: "Kullanıcı Arabirimi (UI) özelleştirme - Azure AD B2C | Microsoft Docs"
description: "Bir konu hello kullanıcı arabirimi (UI) özelleştirme Azure Active Directory B2C özelliklerinde hakkında"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 99f5a391-5328-471d-a15c-a2fafafe233d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 04f8c5f1277f8d4409cd10971d22a0ebd2024785
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-customize-hello-azure-ad-b2c-user-interface-ui"></a>Azure Active Directory B2C: hello Azure AD B2C kullanıcı arabirimini (UI) özelleştirme

Kullanıcı deneyimi uygulama kullanıma yönelik bir müşteri dönüştürmektir.  Müşteri, marka hello Görünüm ve yapısını ile kullanıcı deneyimleri hazırlayın tarafından temel artar. Azure Active Directory B2C (Azure AD B2C) kaydolma, oturum açma profili düzenleme özelleştirmenize olanak tanır ve parola sıfırlama piksel mükemmel denetimiyle sayfaları.

> [!NOTE]
> Bu makalede açıklanan hello sayfası kullanıcı Arabirimi özelleştirme özelliğini toohello oturum açma tek ilke, eşlik eden parola sıfırlama sayfası ve doğrulama e-postaları geçerli değildir.  Merhaba bu özellikleri kullanan [şirket markası özelliğini](../active-directory/active-directory-add-company-branding.md) yerine.
>

Bu makalede, aşağıdaki konularda hello yer almaktadır:

* Başlangıç sayfası kullanıcı Arabirimi özelleştirme özelliği.
* HTML içerik tooAzure Blob Storage ile Merhaba sayfası kullanıcı Arabirimi özelleştirme özelliğini kullanmak için karşıya yükleme için bir araç.
* Azure AD B2C tarafından geçişli stil sayfaları (CSS) kullanarak özelleştirebileceğiniz kullanılan kullanıcı Arabirimi öğeleri hello.
* Bu özelliği kullanan olduğunda en iyi yöntemler.

## <a name="hello-page-ui-customization-feature"></a>Başlangıç sayfası kullanıcı Arabirimi özelleştirme özelliği

Müşteri kaydolma, oturum açma parolası hello Görünüm ve yapısını özelleştirebilirsiniz sıfırlama ve profil düzenleme sayfaları (yapılandırarak [ilkeleri](active-directory-b2c-reference-policies.md)). Uygulama ve Azure AD B2C tarafından sunulan sayfaları arasında gezinme edilirken, müşterilerinizin sorunsuz bir deneyim kullanır.

Burada Azure AD B2C kullanan basit ve modern kullanıcı Arabirimi seçenekleri tooUI özelleştirme yaklaşımını diğer hizmetler.

İşte nasıl çalışır?: Azure AD B2C, müşterinizin tarayıcıda kodu çalıştırır ve adlı modern bir yaklaşım kullanır [çıkış noktaları arası kaynak paylaşımı (CORS)](http://www.w3.org/TR/cors/).  Çalışma zamanında, ilkede belirttiğiniz URL'den içeriği yüklenir. Farklı sayfaları için farklı URL'ler belirtebilirsiniz. Azure AD B2C ' eklenen bir HTML parçasını, URL'den yüklenen içeriğe birleştirilen sonra hello görüntülenen tooyour müşteri sayfasıdır. Toodo ihtiyacınız olan tek şey:

1. Doğru biçimlendirilmiş HTML5 ile boş bir içerik oluşturma `<div id="api"></div>` öğesi bulunan bir yerde hello `<body>`. Bu öğe işaretleri hello Azure AD B2C içerik nerede eklenir.
1. Bir HTTPS uç noktası, içerik ana bilgisayar (izin verilen CORS'yi). Her ikisini de almak ve seçenekleri istek yöntemleri CORS yapılandırırken etkinleştirilmelidir unutmayın.
1. Azure AD B2C ekler CSS toostyle hello kullanıcı Arabirimi öğeleri kullanın.

### <a name="a-basic-example-of-customized-html"></a>Özelleştirilmiş HTML temel örneği

Aşağıdaki örnek hello tootest bu özelliği kullanabilirsiniz hello en temel HTML içeriktir. Kullanım hello [Yardımcısı aracı](active-directory-b2c-reference-ui-customization-helper-tool.md) tooupload ve bu içerik, Azure Blob Depolama alanında yapılandırın. Ardından hello temel, stilize olmayan düğmeleri & form alanlarını her sayfada görüntülenen ve işlevsel olduğunu doğrulayın.

```HTML
<!DOCTYPE html>
<html>
    <head>
        <title>!Add your title here!</title>
    </head>
    <body>
        <div id="api"></div>   <!-- Leave this element empty because Azure AD B2C will insert content here. -->
    </body>
</html>
```

## <a name="test-out-hello-ui-customization-feature"></a>Merhaba UI Özelleştirme özelliği test

Bizim örnek HTML ve CSS içerik kullanarak hello UI Özelleştirme özelliği çıkışı tootry istiyorsunuz?  Biz sağladığınız [Yardımcısı aracı](active-directory-b2c-reference-ui-customization-helper-tool.md) yükler ve Azure Blob Depolama alanınızda örnek içeriği yapılandırır.

> [!NOTE]
> Herhangi bir yere UI içeriğinizi barındırabilir: web sunucularında, CDN'ler, AWS S3, dosya paylaşım sistemleri, vs. Merhaba içerik CORS'yi genel kullanıma açık bir HTTPS uç noktası üzerinde barındırılıyorsa sürece, iyi toogo demektir. Azure Blob Depolama yalnızca yalnızca tanım amaçlıdır kullanıyoruz.
>

## <a name="hello-ui-fragments-embedded-by-azure-ad-b2c"></a>Azure AD B2C tarafından katıştırılmış hello UI parçaları

Merhaba aşağıdaki bölümlerde listelenmiştir hello Azure AD B2C birleştirir hello HTML5 parçaları `<div id="api"></div>` öğesi bulunan, içeriği. **Bu parçasının HTML 5 içeriğinizi koymayın.** Hello Azure AD B2C hizmeti bunları çalışma zamanında ekler. Bu parçasının kendi geçişli stil sayfaları (CSS) tasarlarken başvuru olarak kullanabilirsiniz.

### <a name="fragment-inserted-into-hello-identity-provider-selection-page"></a>"Kimlik sağlayıcısı seçimi sayfası" Merhaba eklenen parçası

Bu sayfa kullanıcı hello sağlayıcıları kaydolma veya oturum açma sırasında seçebileceği kimlik listesini içerir. Bu düğme, Facebook ve Google + veya yerel hesaplar (e-posta adresi veya kullanıcı adına göre) gibi sosyal kimlik sağlayıcıları içerir.

```HTML
<div id="api" data-name="IdpSelections">
    <div class="intro">
         <p>Sign up</p>
    </div>

    <div>
        <ul>
            <li>
                <button class="accountButton" id="FacebookExchange">Facebook</button>
            </li>
            <li>
                <button class="accountButton" id="GoogleExchange">Google+</button>
            </li>
            <li>
                <button class="accountButton" id="SignUpWithLogonEmailExchange">Email</button>
            </li>
        </ul>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-local-account-sign-up-page"></a>"Yerel hesap kayıt sayfasına" Merhaba eklenen parçası

Bu sayfa bir e-posta adresi veya bir kullanıcı adı göre kaydolma yerel hesap için bir form içerir. Merhaba form metin giriş kutusuna, parola giriş kutusu, radyo düğmesi, tek seçimlik açılan kutuları ve çoklu seçim onay kutuları gibi farklı giriş denetimlerini içerebilir.

```HTML
<div id="api" data-name="SelfAsserted">
    <div class="intro">
        <p>Create your account by providing hello following details</p>
    </div>

    <div id="attributeVerification">
        <div class="errorText" id="passwordEntryMismatch" style="display: none;">hello password entry fields do not match. Please enter hello same password in both fields and try again.</div>
        <div class="errorText" id="requiredFieldMissing" style="display: none;">A required field is missing. Please fill out all required fields and try again.</div>
        <div class="errorText" id="fieldIncorrect" style="display: none;">One or more fields are filled out incorrectly. Please check your entries and try again.</div>
        <div class="errorText" id="claimVerificationServerError" style="display: none;"></div>
        <div class="attr" id="attributeList">
            <ul>
                <li>
                    <div class="attrEntry validate">
                        <div>
                            <div class="verificationInfoText" id="email_intro" style="display: inline;">Verification is necessary. Please click Send button.</div>
                            <div class="verificationInfoText" id="email_info" style="display:none">Verification code has been sent tooyour inbox. Please copy it toohello input box below.</div>
                            <div class="verificationSuccessText" id="email_success" style="display:none">E-mail address verified. You can now continue.</div>
                            <div class="verificationErrorText" id="email_fail_retry" style="display:none">Incorrect code, try again.</div>
                            <div class="verificationErrorText" id="email_fail_no_retry" style="display:none">Exceeded number of retries you need toosend new code.</div>
                            <div class="verificationErrorText" id="email_fail_server" style="display:none">Server error, please try again</div>
                            <div class="verificationErrorText" id="email_incorrect_format" style="display:none">Incorect format.</div>
                        </div>

                    <div class="helpText show">This information is required</div>
                        <label>Email</label>
                        <input id="email" class="textInput" type="text" placeholder="Email" required="" autofocus=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Email address that can be used toocontact you.');" class="tiny">What is this?</a>

                    <div class="buttons verify" claim_id="email">
                        <div id="email_ver_wait" class="working" style="display: none;"></div>
                            <label id="email_ver_input_label" for="email_ver_input" style="display: none;">Verification code</label>
                            <input id="email_ver_input" type="text" placeholder="Verification code" style="display:none">
                            <button id="email_ver_but_send" class="sendButton" type="button" style="display: inline;">Send verification code</button>
                            <button id="email_ver_but_verify" class="verifyButton" type="button" style="display:none">Verify code</button>
                            <button id="email_ver_but_resend" class="sendButton" type="button" style="display:none">Send new code</button>
                            <button id="email_ver_but_edit" class="editButton" type="button" style="display:none">Change e-mail</button>
                            <button id="email_ver_but_default" class="defaultButton" type="button" style="display:none">Default</button>
                        </div>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ " ( ) ; .This information is required</div>
                        <label>Enter password</label>
                        <input id="password" class="textInput" type="password" placeholder="Enter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title="8-16 characters, containing 3 out of 4 of hello following: Lowercase characters, uppercase characters, digits (0-9), and one or more of hello following symbols: @ # $ % ^ &amp; * - _ + = [ ] { } | \ : ' , ? / ` ~ &quot; ( ) ; ." required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Enter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"> This information is required</div>
                        <label>Reenter password</label>
                        <input id="reenterPassword" class="textInput" type="password" placeholder="Reenter password" pattern="^((?=.*[a-z])(?=.*[A-Z])(?=.*\d)|(?=.*[a-z])(?=.*[A-Z])(?=.*[^A-Za-z0-9])|(?=.*[a-z])(?=.*\d)(?=.*[^A-Za-z0-9])|(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]))([A-Za-z\d@#$%^&amp;*\-_+=[\]{}|\\:',?/`~&quot;();!]|\.(?!@)){8,16}$" title=" " required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Reenter password');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Name</label>
                        <input id="displayName" class="textInput" type="text" placeholder="Name" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your display name.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Gender</label>
                        <input id="extension_Gender_F" name="extension_Gender" type="radio" value="F" autofocus="">
                        <label for="extension_Gender_F">Female</label>
                        <input id="extension_Gender_M" name="extension_Gender" type="radio" value="M">
                        <label for="extension_Gender_M">Male</label>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>Loyalty number</label>
                        <input id="extension_MemNum" class="textInput" type="text" placeholder="Loyalty number"><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Membership number');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText"></div>
                        <label>State</label>
                        <select class="dropdown_single" id="state">
                            <option style="display:none" disabled="disabled" value="placeholder" selected="">State</option>
                            <option value="WA">Washington</option>
                            <option value="NY">New York</option>
                            <option value="CA">California</option>
                        </select>
                        <a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('Your residential state or province.');" class="tiny">What is this?</a>
                    </div>
                </li>
                <li>
                    <div class="attrEntry">
                        <div class="helpText">This information is required</div>
                        <label>Zip code</label>
                        <input id="postalCode" class="textInput" type="text" placeholder="Zip code" required=""><a href="javascript:void(0)" onclick="selfAssertedClient.showHelp('hello postal code of your address.');" class="tiny">What is this?</a>
                    </div>
                </li>
            </ul>
        </div>
        <div class="buttons"> <button id="continue" disabled="">Create</button> <button id="cancel">Cancel</button></div>
    </div>
    <div class="verifying-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="verifying_blurb"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-social-account-sign-up-page"></a>"" Sosyal hesap kayıt sayfasına"Merhaba parça eklenen

Bu sayfa, Facebook veya Google + gibi sosyal kimlik sağlayıcısından var olan bir hesabı kullanarak kaydolmak görünebilir.  Ek bilgi hello son kaydolma formu kullanarak kullanıcıdan toplanması gereken olduğunda kullanılır. Bu sayfa (Merhaba önceki bölümde gösterilmiştir) benzer toohello yerel hesap kaydolma hello parola giriş alanları hello özel durumla sayfasıdır.

### <a name="fragment-inserted-into-hello-unified-sign-up-or-sign-in-page"></a>Merhaba "Birleşik kayıt veya oturum açma sayfasına" eklenen parçası

Bu sayfa, hem kaydolma ve oturum açma Facebook veya Google + veya yerel hesaplar gibi sosyal kimlik sağlayıcıları kullanan müşteriler, işler.

```HTML
<div id="api" data-name="Unified">
        <div class="social" role="form">
               <div class="intro">
                       <h2>Sign in with your social account</h2>
               </div>
               <div class="options">
                       <div><button class="accountButton firstButton" id="MicrosoftAccountExchange" tabindex="1">msa</button></div>
                       <div><button class="accountButton" id="FacebookExchange" tabindex="1">fb</button></div>
               </div>
        </div>
        <div class="divider">
               <h2>OR</h2>
        </div>
        <div class="localAccount" role="form">
               <div class="intro">
                       <h2>Sign in with your existing account</h2>
               </div>
               <div class="error pageLevel" aria-hidden="true" style="display: none;">
                       <p role="alert"></p>
               </div>
               <div class="entry">
                       <div class="entry-item">
                               <label for="logonIdentifier">Email Address</label> 
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="email" id="logonIdentifier" name="LogonIdentifier" pattern="^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$" placeholder="LogonIdentifier" value="" tabindex="1">
                       </div>
                       <div class="entry-item">
                               <div class="password-label"> <label for="password">Password</label><a id="forgotPassword" tabindex="2">Forgot your password?</a></div>
                               <div class="error itemLevel" aria-hidden="true" style="display: none;">
                                      <p role="alert"></p>
                               </div>
                               <input type="password" id="password" name="Password" placeholder="Password" tabindex="1">
                       </div>
                       <div class="working"></div>
                       <div class="buttons"> <button id="next" tabindex="1">Sign in</button> </div>
               </div>
               <div class="divider">
                       <h2>OR</h2>
               </div>
               <div class="create">
                       <p>Don't have an account?<a id="createAccount" tabindex="1">Sign up now</a> </p>
               </div>
        </div>
</div>
```

### <a name="fragment-inserted-into-hello-multi-factor-authentication-page"></a>"Çok faktörlü kimlik doğrulaması sayfasında" Merhaba eklenen parçası

Bu sayfada, kullanıcıların telefon numaralarına (metin veya sesli kullanarak) kaydolma veya oturum açma sırasında doğrulayabilirsiniz.

```HTML
<div id="api" data-name="Phonefactor">
    <div id="phonefactor_initial">
        <div class="intro">
            <p>Enter a number below that we can send a code via SMS or phone tooauthenticate you.</p>
        </div>
        <div class="errorText" id="errorMessage" style="display:none"></div>
        <div class="phoneEntry" id="phoneEntry">
            <div class="phoneNumber">
                <select id="countryCode" style="display:inline-block">
                    <option value="+93">Afghanistan (+93)</option>
                    <!-- Not all country codes listed -->
                    <option value="+44">United Kingdom (+44)</option>
                    <option value="+1" selected="">United States (+1)</option>
                    <!-- Not all country codes listed -->
                </select>
            </div>
            <div class="phoneNumber">
                <input type="text" id="localNumber" style="display:inline-block" placeholder="Phone number">
            </div>
        </div>
        <div id="codeVerification" style="display:none">
            <div>
                <p>Enter your verification code below, or <button id="retryCode" class="textButton">send a new code</button></p>
                <input type="text" id="verificationCode" placeholder="Verification code">
            </div>
        </div>
        <div class="buttons">
            <button id="verifyCode" class="sendInitialCodeButton">Send Code</button>
            <button id="verifyPhone" style="display:inline-block">Call Me</button>
            <button id="cancel" style="display:inline-block">Cancel</button>
        </div>
    </div>
    <div class="dialing-modal">
        <div class="preloader"> <img src="https://login.microsoftonline.com/static/img/win8loader.gif" alt="Please wait"></div>
        <div id="dialing_blurb"></div><div id="dialing_number"></div>
    </div>
</div>
```

### <a name="fragment-inserted-into-hello-error-page"></a>"" Hata sayfası"Merhaba eklenen parçası

```HTML
<div id="api" class="error-page-content" data-name="GlobalException">
    <h2>Sorry, but we're having trouble signing you in.</h2>
    <div class="error-page-help">We track these errors automatically, but if hello problem persists feel free toocontact us. In hello meantime, please try again.</div>
    <div class="error-page-messagedetails">Your administrator hasn't provided any contact details.</div>
    <div class="error-page-messagedetails">
        <div class="error-page-correlationid">Correlation ID:1c4f0397-c6e4-4afe-bf74-42f488f2f15f</div>
        <div>Timestamp:2015-09-14 23:22:35Z</div>
        <div class="error-page-detail">AADB2C90065: A B2C client-side error 'Access is denied.' has occurred requesting hello remote resource.</div>
    </div>
</div>
```

## <a name="localizing-your-html-content"></a>HTML içeriğinizi yerelleştirme

Açarak HTML içeriğinizi yerelleştirebilirsiniz ['Dil özelleştirme'](active-directory-b2c-reference-language-customization.md).  Bu özelliği etkinleştirmek, Azure AD B2C tooforward hello parametresi, Open ID Connect verir `ui-locales`, tooyour uç noktası.  İçeriğinize dile özgü bu parametre özelleştirilmiş tooprovide HTML sayfalarını kullanabilirsiniz.

## <a name="things-tooremember-when-building-your-own-content"></a>Kendi içerik oluştururken şeyler tooremember

Toouse hello sayfası kullanıcı Arabirimi özelleştirme özelliğini planlıyorsanız, en iyi uygulamaları izleyerek hello gözden geçirin:

* Yoksa hello Azure AD B2C'ın varsayılan içeriği Kopyala ve toomodify denemesi. Bu en iyi toobuild, başvuru olarak karalama ve toouse varsayılan içerikten HTML5 içeriktir.
* Güvenlik nedenleriyle, biz, tooinclude izin verme içeriğinizde herhangi bir JavaScript. Gerekenler çoğu hello kutu dışı kullanılabilir olması gerekir. Aksi takdirde, kullanın [kullanıcı sesi](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c) toorequest yeni işlevsellik.
* Tarayıcı sürümleri desteklenir:
  * Internet Explorer 11, 10, sınır
  * Internet Explorer 9, 8 için sınırlı destek
  * Google Chrome 42.0 ve üstü
  * Mozilla Firefox 38.0 ve üstü
