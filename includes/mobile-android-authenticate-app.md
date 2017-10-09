
1. Başlangıç projesi Android Studio'da açın.

2. İçinde **Proje Gezgini** Android Studio'da hello ToDoActivity.java dosyasını açın ve içeri aktarma deyimlerini aşağıdaki hello ekleyin:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Yöntem toohello aşağıdaki hello eklemek **ToDoActivity** sınıfı:

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Bu kod bir yöntem toohandle hello Google kimlik doğrulama işlemi oluşturur. Bir iletişim kutusu hello hello kimliği doğrulanmış kullanıcının Kimliğini görüntüler. Yalnızca başarılı bir kimlik doğrulaması devam edebilirsiniz.

    > [!NOTE]
    > Google dışında bir kimlik sağlayıcısı kullanıyorsanız, toohello geçirilen hello değeri değiştirmek **oturum açma** değerleri aşağıdaki Merhaba, yöntemi tooone: _MicrosoftAccount_, _Facebook_, _Twitter_, veya _windowsazureactivedirectory_.

4. Merhaba, **onCreate** yöntemi, hello başlatır hello koddan sonra aşağıdaki kod hello eklemek `MobileServiceClient` nesnesi.

        authenticate();

    Bu çağrı hello kimlik doğrulama işlemi başlatır.

5. Koddan sonra kalan hello taşıma `authenticate();` hello içinde **onCreate** yöntemi tooa yeni **createTable** yöntemi:

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure yeniden yönlendirme works beklendiği gibi parçacığını aşağıdaki hello eklemek _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Android uygulamanızın redirectUriScheme too_build.gradle_ ekleyin.

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. Com.Android.support:customtabs:23.0.1 toohello bağımlılıkları, build.gradle ekleyin:

      bağımlılıklar {/ /... 'com.android.support:customtabs:23.0.1' derleme}

9. Merhaba gelen **çalıştırmak** menüsünde tıklatın **uygulamayı çalıştırın** toostart hello uygulama ve seçilen kimlik sağlayıcınızı oturum açın.

> [!WARNING]
> Merhaba URL belirtilen düzeni büyük/küçük harf duyarlıdır.  Emin tüm oluşumlarını `{url_scheme_of_you_app}` kullanım hello aynı durumda.

Başarılı bir şekilde imzalanmış, hello uygulama hatasız çalışması gerektiğini ve mümkün tooquery hello arka uç hizmeti olması ve güncelleştirmeleri toodata yapın.
