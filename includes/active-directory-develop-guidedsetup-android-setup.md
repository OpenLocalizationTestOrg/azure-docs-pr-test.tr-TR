
## <a name="set-up-your-project"></a>Projenizin kurulumunu

Bunun yerine bu örneği ait Android Studio projesi indirme istiyor musunuz? [Bir proje indirme](https://github.com/Azure-Samples/active-directory-android-native-v2/archive/master.zip)ve geçin [yapılandırma adımı](#create-an-application-express) kod örneği, yürütmeden önce yapılandırmak için.

### <a name="create-a-new-project"></a>Yeni bir proje oluşturma 
1.  Android Studio'yu açın ve ardından **dosya** > **yeni** > **yeni proje**.
2.  Uygulamanızı adlandırın ve ardından **sonraki**.
3.  Seçin **API 21 ya da daha yeni (Android 5.0)**ve ardından **sonraki**.
4.  Bırakın **boş etkinlik** olduğu gibi seçin **sonraki**ve ardından **son**.


### <a name="add-msal-to-your-project"></a>MSAL projenize ekleyin
1.  Android Studio'da seçin **Gradle betikleri** > **build.gradle (modül: uygulama)**.
2.  Altında **bağımlılıkları**, aşağıdaki kodu yapıştırın:

    ```ruby  
    compile ('com.microsoft.identity.client:msal:0.1.+') {
        exclude group: 'com.android.support', module: 'appcompat-v7'
    }
    compile 'com.android.volley:volley:1.0.0'
    ```

<!--start-collapse-->
### <a name="about-this-package"></a>Bu paketi hakkında

Önceki kod pakette Microsoft kimlik doğrulama kitaplığı yükler. MSAL alınırken, önbelleğe alma ve Azure Active Directory v2 bitiş noktası tarafından korunan API'leri erişmek için kullanılan kullanıcı belirteçleri yenilemeyi işler.
<!--end-collapse-->

## <a name="create-the-application-ui"></a>Uygulama kullanıcı Arabirimi oluşturma

1. Git **res** > **düzeni**ve ardından açın **activity_main.xml**. 
2. Etkinlik düzeninden değiştirme `android.support.constraint.ConstraintLayout` veya için diğer `LinearLayout`.
3. Ekleme `android:orientation="vertical"` özelliğine `LinearLayout` düğümü.
4. Aşağıdaki kodu yapıştırın `LinearLayout` düğüm, geçerli içerik değiştirme:

    ```xml
    <TextView
        android:text="Welcome, "
        android:textColor="#3f3f3f"
        android:textSize="50px"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginLeft="10dp"
        android:layout_marginTop="15dp"
        android:id="@+id/welcome"
        android:visibility="invisible"/>

    <Button
        android:id="@+id/callGraph"
        android:text="Call Microsoft Graph"
        android:textColor="#FFFFFF"
        android:background="#00a1f1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="200dp"
        android:textAllCaps="false" />

    <TextView
        android:text="Getting Graph Data..."
        android:textColor="#3f3f3f"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginLeft="5dp"
        android:id="@+id/graphData"
        android:visibility="invisible"/>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dip"
        android:layout_weight="1"
        android:gravity="center|bottom"
        android:orientation="vertical" >

        <Button
            android:text="Sign Out"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginBottom="15dp"
            android:textColor="#FFFFFF"
            android:background="#00a1f1"
            android:textAllCaps="false"
            android:id="@+id/clearCache"
            android:visibility="invisible" />
    </LinearLayout>
    ```
