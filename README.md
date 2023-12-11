# Reddit_Konu_Tahmini
Reddit'teki postların text'ine bakılarak hangi konuya ait olduğunu bulmak
Öncelikle projemiz için gerekli olan kütüphaneleri bu alandan import ediyoruz.
![](image.png)
Reddit Api'sini kullanabilmemiz için Authorization sağlamamız gerekiyor. 
![Alt text](image-1.png)
Praw API kullanarak Redditteki post'ların self textini alabilmekteyiz. Alacağımız postların urllerini aşağıda liste şeklinde eklemekteyiz.

![Alt text](image-2.png)

Csv dosyamızı oluştururken başlangıçta iki adet sütunumuz mevcut. Bir sütunda textler, bir sütunda ise kategoriler tutuluyor. Kategoriler döngü içerisinde 125'er tane olacak şekilde Ekonomi,Sanat,Teknoloji,Politika konu başlıklarıyla dolduruluyor.
![Alt text](image-5.png)

Bu kısımda ise almış olduğumuz self textler halihazırda kirli olduğu için temizleme işlemlerini gerçekleştiriyoruz. Textlerimizi emojilerden, aralardaki boşluklardan, sembollerden arındırıyoruz
![Alt text](image-4.png)

Etiketleme

Clean Reddit Postlarının bulunduğu "data_cleaned.csv" dosyası dataframeye aktarılmıştır. 
Reddit Postlarının kategorileri kelime şeklinde kayıtlı olduğu için bu kategoriler 0, 1, 2, 3 gibi bilgisayarın anlayabileceği bir formata dönüştürülmelidir. 
Labels adında yeni bir kolon açılarak kategorisi ekonomi olan Reddit Postları için 0 rakamı, kategorisi sanat olan Reddit Postları için 1 rakamı, kategorisi teknoloji olan Reddit Postları için 2 rakamı ve kategorisi politika olan Reddit Postları için 3 rakamı labels olarak eklenmiştir.

![Alt text](etiketlemeresim.png)