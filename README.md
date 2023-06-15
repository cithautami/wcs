# Web Crawling & Scraping

## Created by:
`Arien Citha Utami: (G1501221008)`
`Rpubs: https://rpubs.com/cithautami/wcs`
`STA1562 Manajemen Database Statistika`

# **Packages**

```{r}
library(Rcrawler)
library(rvest)
library(dplyr)
library(pander)
library(stringr)
library(purrr)
library(wordcloud)
library(tm)
library(slam)
```

# **Data**

## **Scuba School International (SSI)**

Scuba Schools International (SSI) didirikan pada tahun 1970 dengan visi memungkinkan siapa saja untuk belajar cara menyelam dengan aman. Saat ini, SSI adalah agen pelatihan berbasis bisnis profesional terbesar di dunia, dengan 3.500+ Pusat Pelatihan dan lebih dari 100.000 Profesional SSI di 150+ negara.

Selama lebih dari 50 tahun, SSI telah menyediakan program dan materi pelatihan berkualitas tinggi untuk program Recreational Scuba, Extended Range, Freediving, Mermaid, Swim, dan Lifeguard dari level pemula hingga Pelatih Instruktur. Dengan materi digital dan cetak yang tersedia dalam lebih dari 40 bahasa di lebih dari 3.500 lokasi Pusat Pelatihan dan Resor SSI internasional, SSI memungkinkan orang untuk merasakan dunia bawah laut di seluruh dunia.

## **Pengakuan Internasional**

SSI sepenuhnya mewujudkan industri dengan menjadi anggota pendiri RSTC (Dewan Pelatihan Scuba Rekreasi) dan memegang sertifikasi ISO (Organisasi Internasional untuk Standardisasi) yang diakui secara internasional dan berperan aktif dalam menetapkan standar pelatihan minimum industri. Sederhananya, Sertifikasi SSI diterima di seluruh dunia, di mana pun Anda memilih untuk menyelam – SSI jelas merupakan nama yang dapat Anda percayai.

## **Program Bersertifikasi ISO**

1. ISO 11121 untuk Penyelam Dasar
2. ISO 24801-1 untuk Penyelam Scuba
3. ISO 24801-2 untuk Penyelam Perairan Terbuka
4. ISO 24801-3 untuk Panduan Selam
5. ISO 21417 untuk Panduan Kelautan SSI
6. ISO 11107 untuk Nitrox Udara yang Diperkaya
7. ISO 13293 untuk Blender Gas
8. ISO 24802-1 untuk Asisten Instruktur
9. ISO 24802-2 untuk Instruktur Perairan Terbuka
10. ISO 13970 untuk Instruktur Snorkeling

## **Eksplorasi Data**

Mendefinisikan url yang digunakan.

```{r}
url <- 'https://www.divessi.com/en/mydiveguide/continents'
url
```
Memperlihatkan tampilan website.

```{r}
knitr::include_graphics("E:/S2/Semester 2/MDS/UAS/Responsi/website-ssi.png")
```

# **Web Crawling**

```{r}
links <- LinkExtractor(url, ExternalLInks = TRUE)
str(links)
links
```

Terlihat bahwa ada 118 link pada website, diantaranya 106 link internal dan 12 link eksternal. 

# **Web Scraping**

## **Destination by Continents**

Web scraping akan diaplikasikan pada 6 continents yang ada di dunia sebagai berikut:

1. Africa
2. Asia
3. Australia
4. Europe
5. North America
6. South America

Maka dilakukan pemisahan link sesuai continent masing-masing yaitu kolom 26 - 31.

```{r}
africa <- links$InternalLinks[26]
asia <- links$InternalLinks[27]
australia <- links$InternalLinks[28]
europe <- links$InternalLinks[29]
north_america <- links$InternalLinks[30]
south_america <- links$InternalLinks[31]
```

Melihat keterangan di dalam masing-masing continents.

```{r}
# melakukan web scraping
webpage <- read_html(url) %>% html_node(css = '.cardshelf-inner')
webpage

# mengambil heading h3
places <- webpage %>% html_nodes('h3') %>% html_text()
places

# mengambil isi konten bagian dari heading h3
notes <- read_html(url) %>% html_elements('.overlay-content') %>% html_text()
notes

# membuat tabel data web scraping
table <- data.frame(places = places,
                           notes = notes)
table
```

### **Africa**

Diving in Africa you can explore the wonders of the Red Sea or discover hidden gems like St. Helena Island.

```{r}
# mendefinisikan web scraping
html_africa <- read_html(africa)
html_africa

# melakukan web scraping
webpage_africa <- read_html(africa) %>% html_node(css = '.cardshelf-inner')
webpage_africa

# mengambil heading h3
places_africa <- webpage_africa %>% html_nodes('h3') %>% html_text()
places_africa

# mengambil isi konten bagian dari heading h3
notes_africa <- read_html(africa) %>% html_elements('.overlay-content') %>% html_text()
notes_africa

# membuat tabel data web scraping
table_africa <- data.frame(places = places_africa,
                           notes = notes_africa)
table_africa
```

### **Asia**

Some of the world’s most paradisiac diving destinations in Asia can be found in Indonesia, Maldives, Malaysia, the Philippines, and Thailand.

```{r}
# mendefinisikan web scraping
html_asia <- read_html(asia)
html_asia

# melakukan web scraping
webpage_asia <- read_html(asia) %>% html_node(css = '.cardshelf-inner')
webpage_asia

# mengambil heading h3
places_asia <- webpage_asia %>% html_nodes('h3') %>% html_text()
places_asia

# mengambil isi konten bagian dari heading h3
notes_asia <- read_html(asia) %>% html_elements('.overlay-content') %>% html_text()
notes_asia

# membuat tabel data web scraping
table_asia <- data.frame(places = places_asia,
                           notes = notes_asia)
table_asia
```

### **Australia**

The world’s largest coral reef, the Great Barrier Reef is the essence of diving in Australia.

```{r}
# mendefinisikan web scraping
html_australia <- read_html(australia)
html_australia

# melakukan web scraping
webpage_australia <- read_html(australia) %>% html_node(css = '.cardshelf-inner')
webpage_australia

# mengambil heading h3
places_australia <- webpage_australia %>% html_nodes('h3') %>% html_text()
places_australia

# mengambil isi konten bagian dari heading h3
notes_australia <- read_html(australia) %>% html_elements('.overlay-content') %>% html_text()
notes_australia

# membuat tabel data web scraping
table_australia <- data.frame(places = places_australia,
                           notes = notes_australia)
table_australia
```

### **Europe**

The best places to dive in Europe include Greece, France, Italy, Germany, Spain, Turkey, and Croatia among many others.

```{r}
# mendefinisikan web scraping
html_europe <- read_html(europe)
html_europe

# melakukan web scraping
webpage_europe <- read_html(europe) %>% html_node(css = '.cardshelf-inner')
webpage_europe

# mengambil heading h3
places_europe <- webpage_europe %>% html_nodes('h3') %>% html_text()
places_europe

# mengambil isi konten bagian dari heading h3
notes_europe <- read_html(europe) %>% html_elements('.overlay-content') %>% html_text()
notes_europe

# membuat tabel data web scraping
table_europe <- data.frame(places = places_europe,
                           notes = notes_europe)
table_europe
```

### **North America**

North America offers a wide variety of adventures for every type of diver such as ice diving in Alaska or cenote diving in Mexico.

```{r}
# mendefinisikan web scraping
html_north_america <- read_html(north_america)
html_north_america

# melakukan web scraping
webpage_north_america <- read_html(north_america) %>% html_node(css = '.cardshelf-inner')
webpage_north_america

# mengambil heading h3
places_north_america <- webpage_north_america %>% html_nodes('h3') %>% html_text()
places_north_america

# mengambil isi konten bagian dari heading h3
notes_north_america <- read_html(north_america) %>% html_elements('.overlay-content') %>% html_text()
notes_north_america

# membuat tabel data web scraping
table_north_america <- data.frame(places = places_north_america,
                           notes = notes_north_america)
table_north_america
```

### **South America**

In South America, you will find plenty of dive sites to choose from, including Ilhabela, Abrolhos Archipelago, and Easter Island.

```{r}
# mendefinisikan web scraping
html_south_america <- read_html(south_america)
html_south_america

# melakukan web scraping
webpage_south_america <- read_html(south_america) %>% html_node(css = '.cardshelf-inner')
webpage_south_america

# mengambil heading h3
places_south_america <- webpage_south_america %>% html_nodes('h3') %>% html_text()
places_south_america

# mengambil isi konten bagian dari heading h3
notes_south_america <- read_html(south_america) %>% html_elements('.overlay-content') %>% html_text()
notes_south_america

# membuat tabel data web scraping
table_south_america <- data.frame(places = places_south_america,
                           notes = notes_south_america)
table_south_america
```

## **Zogg Product**

Zoggs adalah merek kacamata renang, alat bantu pelatihan, pakaian renang, dan produk terkait lainnya. Perusahaan ini diluncurkan di Sydney, Australia pada tahun 1992 dan merupakan merek pertama yang menawarkan perlindungan UV dan tali pengikat split sebagai fitur standar pada semua kacamata.

Mendefinisikan url yang digunakan dan memperlihatkan tampilan website.

```{r}
knitr::include_graphics("E:/S2/Semester 2/MDS/UAS/Responsi/website-zogg.png")
```

Memulai scraping pada data website zogg product.

```{r}
# mengambil link yang menarik untuk dieksplorasi
zogg <- 'links$ExternalLinks[5]'
zogg

# scraping data khusus swimwear perempuan pages 1 dan 2
zogg_1 <- 'https://www.zoggs.com/en_GB/swimwear/womens?p=1'
zogg_2 <- 'https://www.zoggs.com/en_GB/swimwear/womens?p=2'
zogg_1
zogg_2

# memindahkan dalam bentuk webpage
webpage_zogg_1 <- read_html(zogg_1)
webpage_zogg_2 <- read_html(zogg_2)
webpage_zogg_1
webpage_zogg_2

# product dan menghilangkan karakter "\n" yang mengganggu
product_1 <- webpage_zogg_1 %>%
  html_nodes(".product-item-link") %>%
  html_text(trim = T) %>%
  str_replace_all('\\n+',' ')
product_1

product_2 <- webpage_zogg_2 %>%
  html_nodes(".product-item-link") %>%
  html_text(trim = T) %>%
  str_replace_all('\\n+',' ')
product_2

# price
price_1 <- webpage_zogg_1 %>%
  html_nodes(".price") %>%
  html_text(trim =T)
price_1

price_2 <- webpage_zogg_2 %>%
  html_nodes(".price") %>%
  html_text(trim =T)
price_2

# membuat tabel product & price
zogg_prod_price_1 <- data.frame(product = product_1, price = price_1)
zogg_prod_price_2 <- data.frame(product = product_2, price = price_2)
zogg_prod_price_1
zogg_prod_price_2
table_zogg <- rbind(zogg_prod_price_1, zogg_prod_price_2)
table_zogg
```

# **Connect to MongoDB Atlas**

## **Membuat Koneksi**

Membuat koneksi dari R ke MongoDB untuk proses integrasi data dengan mendefinisikan dengan nama `atlas`.

```{r include=FALSE}
library(mongolite)
atlas <- 'mongodb+srv://cithautami:<password>@cluster0.vfwj8kw.mongodb.net/?retryWrites=true&w=majority'
atlas
```

## **Membuat Database & Collection**

Proses integrasi data.

```{r}
africa_collection <- mongo(collection = "africa", 
                         db = "dive_site",
                         url = atlas)

asia_collection <- mongo(collection = "asia", 
                         db = "dive_site",
                         url = atlas)

australia_collection <- mongo(collection = "australia", 
                         db = "dive_site",
                         url = atlas)

europe_collection <- mongo(collection = "europe", 
                         db = "dive_site",
                         url = atlas)

north_america_collection <- mongo(collection = "north_america", 
                         db = "dive_site",
                         url = atlas)

south_america_collection <- mongo(collection = "south_america", 
                         db = "dive_site",
                         url = atlas)

zogg_collection <- mongo(collection = "zogg", 
                         db = "product_zogg",
                         url = atlas)
```

Insert tabel dari R ke MongoDB.

```{r}
africa_collection$insert(table_africa)
asia_collection$insert(table_asia)
australia_collection$insert(table_australia)
europe_collection$insert(table_europe)
north_america_collection$insert(table_north_america)
south_america_collection$insert(table_south_america)
zogg_collection$insert(table_zogg)
```

Memperlihatkan hasil integrasi data yang sudah berhasil dilakukan pada data dive site by continent.

```{r}
knitr::include_graphics("E:/S2/Semester 2/MDS/UAS/Responsi/mongodb-dive-site.png")
```

Memperlihatkan hasil integrasi data yang sudah berhasil dilakukan pada data zogg product.

```{r}
knitr::include_graphics("E:/S2/Semester 2/MDS/UAS/Responsi/mongodb-zogg.png")
```

# **Visualisasi Data**

Visualisasi data yang digunakan kali ini adalah wordcloud. Wordcloud merupakan representasi visual/gambar dari data berupa kata. Wordcloud dibentuk dengan cara visualisasi kumpulan kata dengan berbagai ukuran, bentuk, dan warna sesuai kebutuhan. Semakin tebal dan besar kata muncul dalam wordcloud maka semakin sering kata tersebut disebutkan. Semakin sering kata disebutkan maka dapat dianalogikan bahwa kata tersebut semakin penting ada dalam suatu kalimat.

```{r}
text <- rbind(table_africa, table_asia, table_australia, table_europe, table_north_america, table_south_america)
wordcloud(text)
```

Wordcloud diatas menjelaskan bahwa kata yang paling sering disebutkan dalam website adalah `the`, `and`, `diving`, dan `offers`. Ini sesuai dengan tujuan website dibuat yaitu menawarkan pengalaman diving pada berbagai benua/continent yang ada di dunia. Analisis lebih lanjut bisa dilakukan dengan melakukan crawling url lain yang terkait kemudian lakukan scraping pada teks yang didapatkan dalam crawling tersebut.

Semoga bermanfaat!
