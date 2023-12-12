# **Kütüphane İmport İşlemleri**


![c1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/aa67808d-f823-450f-910e-178f5f5a7f1a)



**Öncelikle bu alandan projemiz için gerekli kütüphaneleri import ediyoruz**

**praw:** Reddit apisine erişim için kullanılır

**csv:** Formatında veri okumak ve yazmak için araçlar sağlar

**re:** Düzenli ifadeler ile çalışmak için araçlar sağlar.

**pandas as pd:** Veri analizi kütüphanesidir. Verileri temizlemek ve manipüle etmek, istatistiksel analiz yapmak ve verileri görselleştirmek için işlevler sağlar.

**requests:** HTTP isteklerini yapmak için kullanılır. Web sitelerinden ve API'lerden veri almak için kullanışlıdır.

**nltk:** Doğal dil işleme (NLP) için çeşitli araçlar sağlayan Natural Language Toolkit (NLTK) kütüphanesini içerir.

**string:** Python'un yerleşik string modülüne erişimi sağlar. Metinleri manipüle etmek ve çalışmak için işlevler sunar.

**contextlib:** Otomatik olarak kaynakları temizlemek için kullanılan bağlam yöneticilerini yönetmek için araçlar sağlar.


# **Praw Api Kullanımı**

![c2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/3556fbac-219b-4944-9837-d0ffd9212343)

Reddit API kullanabilmemiz için Reddit’ten izin almamız gerekmektedir. 

Reddit hesabımıza giriş yaparak application oluşturma izni aldıktan sonra tarafımıza verilen bilgilerle API’ya dosyamız üzerinden giriş yaparız.


# **URL’Leri saklama**


![b2e5a9ae-8934-43a1-86dd-ad008b17f826](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/77d78b6c-2a24-405b-982f-e8cf6f6962d3)

Praw API yardımıyla Çekeceğimiz 500 adet postun textini kullanabilmekteyiz. 

Bu işlem için 500 adet postumuzun linkini urls[] adlı listemizde tutmaktayız. 

Daha sonrasında bu url’lerin içerikleri kullanılacaktır.


# **CSV Dosyası Oluşturma ve Yazma**

![c4](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/9d6e956a-65ff-4f48-b4ec-de8f8be612c3)


Verisitemizi csv dosyamızın içerisinde oluşturacağız. 

Csv dosyamızı sonrasında görsel gösterim için dataframe’e aktaracağız fakat öncelikle bu işlem için de verilerimizi csv dosyamıza aktarmamız gerekmektedir. 

Csv dosyamızın içerisinde 2 adet  başlık bulunacaktır. 

Text başlığı altında 500 adet url’mizin bulunduğu postların içerisindeki textler(selftext) bulunacaktır. 

Kategori başlığının ilk 125 satırında ekonomi, sonraki 125 satırında sanat, sonraki 125 satırında teknoloji, son 125 satırında ise politika yazacaktır.


# **Verisetini Temizleme**

![69fc5aec-1ef1-4ccf-8b6d-64814cc632cf](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/dde72f97-27eb-41be-aefb-2d5c5396cabd)


Bu hücremizde veri setimizi tamamen emojilerden, boşluklardan ve sembollerden arındırmaktayız. 

Ardından düzenlenmiş ve temizlenmiş verilerimizi data_cleaned.csv dosyamıza yazarız.


# **trainvetest.ipynb’nin import Kısmı**


![26799abb-fa52-4596-a2e1-780265c38879](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/88753aa9-93fb-4b07-8fe0-45ba5c9a5134)

**Numpy:** NumPy, Python'da bilimsel hesaplamalar ve veri analizi için kullanılan bir kütüphanedir. 

NumPy, çok boyutlu diziler ve matrisler ile çalışmamızı sağlar. NumPy dizileri, Python listelerinden farklı olarak her bir elemanının aynı veri tipinde olması gerekir. 

Bu, NumPy dizilerini bilimsel hesaplamalar için daha verimli hale getirir.




# **Modelin Oluşturulmaya Başlanması**

## **Etiketleme**

Clean Reddit Postlarının bulunduğu "data_cleaned.csv" dosyası dataframeye aktarılmıştır. 
Reddit Postlarının kategorileri kelime şeklinde kayıtlı olduğu için bu kategoriler 0, 1, 2, 3 gibi bilgisayarın anlayabileceği bir formata dönüştürülmelidir. 
Labels adında yeni bir kolon açılarak kategorisi ekonomi olan Reddit Postları için 0 rakamı, kategorisi sanat olan Reddit Postları için 1 rakamı, kategorisi teknoloji olan Reddit Postları için 2 rakamı ve kategorisi politika olan Reddit Postları için 3 rakamı labels olarak eklenmiştir.

![etiketlemeresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/994b0bce-ffdd-41b0-802e-bb949923a22d)

## **Verisetinin Parçalanması**

Modelin başarısını doğru şekilde ölçebilmek için modeli eğittiğimiz veriler ile test ettiğimiz veriler farklı olmalıdır. Modelin eğitilmiş olduğu verileri tekrar modele gönderirsek model bu veriler ile eğitildiği için başarısı yüksek ve yanıltıcı olacaktır. Bu yüzden verisetini parçalamamız gerekir. Bu projede verisetinin %80 'i modeli eğitmek için, %20 'si de modeli test etmek için kullanılacaktır.
Aşağıda verisetinin nasıl parçalanacağının bir örneği gösterilmiştir.

![verisetininparçalanmasıresim](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/b54bd9cb-e47a-42c7-87dd-99e168d5eb71)

## **Reddit Postlarının Vektörel Matrisinin Çıkarılması**

Reddit Postlarını metinden oluştuğu için bunun bilgisayar ortamında işlenmesi mümkün değildir bu yüzden veriler sayısal değerlere dönüştürülmelidir. 
Bir sözlük oluşturularak dökümandaki her kelime için bir indexleme yapılır. 
Daha sonra hangi index numarasına sahip kelimenin hangi Reddit Postunda kaç kere geçtiği hesaplanarak sayma matrisi oluşturulur. 
Bu işlemi yaparken tf-idf vectorizer kullanılarak bir kelimenin döküman içindeki önemi istatistiksel olarak hesaplanmıştır. 
Bu sayede her Reddit Postunda geçen model için anlamsız kelimelerin önemi düşürülmüştür yani stopwordsler tekrardan ayıklanmıştır.

 ## **Modellerin Eğitilmesi**

Daha önceden parçalanmış olan X_train ve y_train verileri Naive Bayes ve Support Vector Machine modeline gönderilerek modeller eğitilmiştir. Eğitim sonucunda modellerin accuracy ve f1 score değerleri hesaplanmıştır. Modelleri eğitmek için sklearn kütüphanesi kullanılmıştır.

 
 ## **Modellerin Başarısının Hesaplanması**

Modelin başarısı hem train hem test verileri üzerinden Accuracy ve F1 score ile ölçülmüştür. 
Alınan sonuçlar aşağıda bulunmaktadır.

![resim1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/35953f64-c1d3-4a4c-a791-861858b90226)     ![resim2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/a6fda108-2dd6-4600-98b0-245c3c6c64bc)


 ## **Kategorilere Göre Başarı Dağılımları**

Kategorilere göre modellerin test verisetindeki başarı dağılımları classification_report() fonksiyonu kullanılarak hesaplanmıştır. 
Alınan sonuçlar aşağıda bulunmaktadır.

![3 1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/3e808213-bbde-49e6-82a5-9271a6de48f8)      ![3 2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/6362cda9-31ff-4066-a738-8b40534b8535)


Sonuçlar incelendiğinde Her iki modelin de en başarılı tahmin yaptığı kategorinin ekonomi kategorisi olduğunu görülmektedir. 



 ## **Modellerin Reddit Postlarına Göre Yaptığı Tahminler**

Aşağıdaki görseldeki kolonlarda, Reddit Postu, Reddit Postunun bulunduğu kategori, Naive Bayes modelinin Reddit postu için tahmini ve Support Vector Machine modelinin Reddit Postu için tahmini gösterilmektedir.

0=ekonomi , 1=sanat , 2=teknoloji , 3=politika


![4](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/2e26a021-fcc9-4a9e-9db7-6a7d29eaaa8e)

Reddit Postlarının kategorilerine ve modellerin yaptığı tahminlere bakıldığında modeller oldukça iyi çalışıyor gibi gözüküyor. 94. Reddit Postuna bakıldığında naive bayes modelinin bu Reddit Postu için yanlış tahmin yaptığını görüyoruz.


 ## **Modellerin Hata Oranları**

 Modellerin hata oranlarını tespit etmek için 2 farklı metrik kullanılmıştır. Bunlar Ortalama Kare Hatası(MSE) ve Ortalama Mutlak Hata(MAE) dir.

Ortalama Kare Hatası(MSE)
Ortalama Kare Hatası tahmin edilen sonuçlarınızın gerçek sayıdan ne kadar farklı olduğuna dair size mutlak bir sayı verir.

Ortalama Mutlak Hata(MAE)
Ortalama mutlak hata, mutlak hata değerinin toplamını alır, hata terimlerinin toplamının daha doğrudan bir temsilidir.


![5](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/789a0d1f-20fe-49ca-a37a-c7bcf7d0ef1b)


Sonuçlar incelendiğinde Naive Bayes modelinin Support Vector Machine modeline göre biraz daha fazla hata yaptığını görüyoruz.


# **Manuel Reddit Postu Testi**

Modeli manuel olarak test etmek için elle bazı Reddit Postları girilecek ve modelin bu Reddit Postlarının hangi kategoriye ait olduğunu tahmin etmesi istenecektir. Test sonuçları aşağıda gösterilmiştir.

**Test1:**

![test1](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/b40707dd-45a0-470d-bf99-de270a80da5d)


**Test2:**

![test2](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/ca4775b9-51db-494b-b74c-ed37721d973c)


**Test3:**

![test3](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/35e02842-e112-48af-b77a-a730aebd14ef)


**Test4:**

![test4](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/7e2434d0-9398-4b4b-bfb0-b8d8bc4c0f50)


**Test5:**

![test5](https://github.com/canbich/Reddit_Konu_Tahmini/assets/116785114/1f201db4-9e4e-4385-aa25-54a572921546)

# **SONUÇ**


Sonuca bakıldığında yapılan projede seçilen modelin ne kadar önemli olduğu görülmektedir.
Yapılan farklı projelerde farklı modeller daha iyi sonuç verebilmektedir.
Her proje için seçilen modelin kendine göre bazı avantajları ve dezavantajları vardır.
Model seçiminde bu avantajları ve dezavantajları göz önüne alarak model seçimi yapılmalıdır.
Modelin bize en düşük hata oranı ile sonuçları göstermesini isteriz ve bu isteğimizi yerine getiren modeli seçmek bizim sorumluluğumuzdur.
Model seçiminin önemi kadar verisetinin güzel bir şekilde hazırlanmış olması, verisetindeki noktalama işaretleri ve modele olumsuz etki edecek stopwordslerden arındırılmış olması, verisetindeki verilerin miktari, eğitim-test verilerinin parçalanma oranı vs. modelin başarısına etki eden çok önemli faktörlerdir. 

Bu projede ulaşılan başarı oranı(%61 NB ve %77 SVM) yüksek bir başarı oranına sahip değildir bunun en temel sebebi verisetini oluştururken farklı kategorilerden aldığımız Reddit postlarıdır ve bunları sayılarıdır çünkü her kategoriden 125 tane veri çektik bu verilerin az olması sebebiyle bu başarı oranlarına sahibiz.
Eğer ki verisetinde ki verilerin sayısını her kategori için 125 tane değilde 10 bin tane yapsaydık bu testler daha fazla veriye maruz kalacağı için kategori işlemlerini daha düzgün yapacaktı çünkü elimizde ne kadar çok veri varsa testler o denli doğru çalışacaktır.

Yukarıda da belirtitğimiz gibi, 4 farklı kategoriden 125'er tane veri alarak bir veriseti oluşturduk. Toplamda bu 500 tane veriyle bir dil eğitmeye çalıştık. Sonuç olarak verilerin az olması sebebiyle dilimizi düzgün bir şekilde eğitemedik.Dilin düzgün bir şekilde eğitilebilmesi için daha çok veriye ihtiyacımız var. Ancak Redditten aldığımız veriler sınırlı olduğu için ve daha fazlasını ekleyemediğimiz için dilimiz yeteri kadar beslenemedi. Bundan dolayı incelenen text'in hangi kategoriye ait olduğunu yeteri kadar düzgün belirleyemiyoruz. Bunun çözümü basit ama elimizde ki imkanlar el vermediği için çözemiyoruz.Çözümü şudur ki yukarıda da belirttiğimiz gibi verisetinin çok fazla veriden oluşması bu sorunun çözümüdür. Ancak Reddit platformunda ki verilerin azlığı sebebiyle bunu gerçekleştiremiyoruz. 
Ancak geçici bir çözüm olarak analiz edeceğimiz text'in kelime sayısını olabildiğince fazla tutarak dilimizin bu text'in kategorisini analiz etmesine yardımcı olabiliriz. 


Yukarıda ki test3, test4, test5 bu çözüme uygun olarak analiz edilmiştir ve bir nebzede olsa dilimiz doğru tahminde bulunmuştur.
test1 ve test2 sadece 1 cümleden oluşan ve yeterince kelime olmayan testlerdir ve bu testlerin kategorilerinin yanlış tahmin edildiğini görüyoruz.
test1'de kategori olarak kesinlikle teknoloji ve test2'de de kategori olarak kesinlikle ekonomi çıkması gerekirken sanat ve politika çıkıyor bunu sebebi verisetinin az sayıda veriden oluşmasıdır.
test3,test4,test5'de bu çözüme dayalı bir süreç yürütebilmek için her test için 10 cümlelik bir text yazdık.
test3'de kategori olarak kesinlikle sanat çıkması gerekiyor ve gerçekten sanat çıkıyor çünkü analiz ettiğimiz text'in kelime sayısını olabildiğince fazla tuttuk ve yukarıda belirttiğimiz çözüm ile bu durumu ispatladık. 
Benzer şekilde test4'de kategori olarak kesinlikle politika  ve test5'de ise kesinlik teknoloji çıkması gerekiyor ve gerçekten dilimiz tahminlerini doğru yapıyor.


**Özetle dil modelimizin hata oranını düşürebilmemiz için oluşturmuş olduğumuz veriseti’nin boyutu büyük olmalıdır ve içerisindeki verilerin birbirlerine benzememesi gerekmektedir. Bu sayede dil modelimizi daha iyi eğitebiliriz ve hata oranımızı düşürebiliriz.**






