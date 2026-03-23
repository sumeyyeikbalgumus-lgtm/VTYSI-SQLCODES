# VTYSI-SQLCODES
MY SQL CODES
create database KutuphaneSistemi
use KutuphaneSistemi
create table Adresler(
adresNo int Primary Key not null identity(1,1),
sehir nvarchar(50) not null,
mahalle nvarchar(50),
binaNo int,
postakodu int,
ulke nvarchar(50) not null,
cadde nvarchar(50)
);

create table Uyeler(
uyeNo int Primary Key identity(1,1) not null,
uyeAdi nvarchar(100) not null,
uyeSoyadi nvarchar(100) not null,
cinsiyet char(2),
telefon nvarchar(50),
eposta nvarchar(50)
);

alter table Uyeler 
add  adresNo INT 
constraint "uyeler_adresler" 
foreign key(adresNo) References Adresler(adresNo);

use KutuphaneSistemi
CREATE TABLE kutuphane (
    kutuphaneNo INT PRIMARY KEY,
    kutuphaneIsmi NVARCHAR(50),
    Aciklama NVARCHAR(50),
    adresNo INT CONSTRAINT "kutuphane_adresler" FOREIGN KEY (adresNo) REFERENCES Adresler(adresNo)
);
create table kitaplar(
ISBN nvarchar(50) not null Primary Key,
kitapAdi nvarchar(50) not null,
sayfaSayisi int,
YayinTarihi datetime
);

create table emanet(
emanetNo int Primary Key not null identity(1,1),
emanetTarihi datetime,
teslimTarihi datetime,
uyeNo int foreign key (uyeNo)references Uyeler(uyeNo),
ISBN nvarchar(50) foreign key (ISBN) REFERENCES Kitaplar (ISBN)
);

create table kategori(
kategoriNo int primary key identity(1,1) not null,
kategoriAdi nvarchar(100) not null,
);

create table yazarlar(
yazarNo int primary key identity(1,1) not null,
yazarAdi nvarchar(50) not null,
yazarSoyadi nvarchar(25) not null,
);

create table kategori_kitap(
id int primary key not null identity(1,1),
ISBN nvarchar(50) foreign key (ISBN) references kitaplar (ISBN),
kategoriNo int foreign key (kategoriNo) references kategori (kategoriNo)
);

create table kitap_yazarlar(
id int primary key not null identity(1,1),
ISBN nvarchar(50) foreign key (ISBN) references kitaplar (ISBN),
yazarNo int foreign key (yazarNo) references yazarlar (yazarNo)
);

create table kitap_kutuphane(
id int primary key not null identity(1,1),
miktar int not null,
ISBN nvarchar(50) foreign key (ISBN) references kitaplar (ISBN),
kutuphaneNo int foreign key (kutuphaneNo) references kutuphane (kutuphaneNo)
);
