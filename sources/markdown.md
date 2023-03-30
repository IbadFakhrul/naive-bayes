# Klasifikasi Naive Bayes

## Contoh:

|   age   | income | student | credit_rating | buys_computer |
| :-----: | :----: | :-----: | :-----------: | :-----------: |
|  <=30   |  high  |   no    |     fair      |      no       |
|  <=30   |  high  |   no    |   excellent   |      no       |
| 31...40 |  high  |   no    |     fair      |      yes      |
|   >40   | medium |   no    |     fair      |      yes      |
|   >40   |  low   |   yes   |     fair      |      yes      |
|   >40   |  low   |   yes   |   excellent   |      no       |
| 31...40 |  low   |   yes   |   excellent   |      yes      |
|  <=30   | medium |   no    |     fair      |      no       |
|  <=30   |  low   |   yes   |     fair      |      yes      |
|   >40   | medium |   yes   |     fair      |      yes      |
|  <=30   | medium |   yes   |   excellent   |      yes      |
| 31...40 | medium |   no    |   excellent   |      yes      |
| 31...40 |  high  |   yes   |     fair      |      yes      |
|   >40   | medium |   no    |   excellent   |      no       |

Class:

- C1: income = "low"
- C2: income = "medium"
- C3: income = "high"

Data Sample:

X = (age <=30, student = "yes", credit_rating = "fair", buys_computer = "yes")

**Langkah 1:**

Menghitung P(C), yaitu menghitung ada berapa jumlah data dari class di atas:

- P(income = "low") = 4/14 = 0.285714
- P(income = "medium") = 6/14 = 0.428571
- P(income = "high") = 4/14 = 0.285714

**Langkah 2:**

Menghitung P(X|C) dari setiap class, yaitu menghitung ada berapa jumlah data X yang berdasarkan data class di atas:

C1:

- P(age <=30|income = "low") = 1/4 = 0.25
- P(student = "yes"|income = "low") = 4/4 = 1
- P(credit_rating = "fair"|income = "low") = 2/4 = 0.5
- P(buys_computer = "yes"|income = "low") = 3/4 = 0.75

C2:

- P(age <=30|income = "medium") = 2/6 = 0.333333
- P(student = "yes"|income = "medium") = 2/6 = 0.333333
- P(credit_rating = "fair"|income = "medium") = 3/6 = 0.5
- P(buys_computer = "yes"|income = "medium") = 4/6 = 0.666667

C3:

- P(age <=30|income = "high") = 2/4 = 0.5
- P(student = "yes"|income = "high") = 1/4 = 0.25
- P(credit_rating = "fair"|income = "high") = 3/4 = 0.75
- P(buys_computer = "yes"|income = "high") = 2/4 = 0.5

**Langkah 3:**

X = (age <=30, student = "yes", credit_rating = "fair", buys_computer = "yes")

P(X|C):

- P(X|income = "low")
  0.25 * 1 * 0.5 * 0.75 = 0.09375

- P(X|income = "medium")
  0.333333 * 0.333333 * 0.5 * 0.666667 = 0.037036981

- P(X|income = "high")
  0.5 * 0.25 * 0.75 * 0.5 = 0.046875

P(X|C)*P(C):

- C1:
  0.09375*0.285714 = 0.026785688

- C2:
  0.037036981*0.428571 = 0.015872976

- C3:
  0.046875*0.285714 = 0.013392844

Yang memiliki nilai tertinggi adalah C1 atau income = "low", jadi jika ada inputan baru dengan data (`age <=30, student = "yes", credit_rating = "fair", buys_computer = "yes"`) tapi tidak ada data income, maka kemungkinan besar income-nya adalah low.



## Metode Gaussian

| age  | income | student | credit_rating | buys_computer |
| :--: | :----: | :-----: | :-----------: | :-----------: |
|  1   |  high  |    0    |       0       |       0       |
|  1   |  high  |    0    |       1       |       0       |
|  2   |  high  |    0    |       0       |       1       |
|  3   | medium |    0    |       0       |       1       |
|  3   |  low   |    1    |       0       |       1       |
|  3   |  low   |    1    |       1       |       0       |
|  2   |  low   |    1    |       1       |       1       |
|  1   | medium |    0    |       0       |       0       |
|  1   |  low   |    1    |       0       |       1       |
|  3   | medium |    1    |       0       |       1       |
|  1   | medium |    1    |       1       |       1       |
|  2   | medium |    0    |       1       |       1       |
|  2   |  high  |    1    |       0       |       1       |
|  3   | medium |    0    |       1       |       0       |

Di sini saya menggunakan sample dan class seperti contoh di atas, yaitu class income dan sample (`age <=30, student = "yes", credit_rating = "fair", buys_computer = "yes"`)



Hitung nilai mean (μ) dan standar deviasi (σ) dari setiap atribut dalam tabel

Nilai mean: 

| income |   age    | student  | credit_rating | buys_computer |
| :----: | :------: | :------: | :-----------: | :-----------: |
|  high  |   1.5    |   0.25   |     0.25      |      0.5      |
| medium | 2.166667 | 0.333333 |      0.5      |   0.666667    |
|  low   |   2.25   |    1     |      0.5      |     0.75      |

Standar deviasi:

| income |   age    | student  | credit_rating | buys_computer |
| :----: | :------: | :------: | :-----------: | :-----------: |
|  high  | 0.57735  |   0.5    |      0.5      |    0.57735    |
| medium | 0.983192 | 0.516398 |   0.547723    |   0.516398    |
|  low   | 0.957427 |    0     |    0.57735    |      0.5      |

Misal ada data baru seperti di bawah ini:

| age  | income | student | credit_rating | buys_computer |
| :--: | :----: | :-----: | :-----------: | :-----------: |
|  1   |   ?    |    1    |       0       |       1       |

Menggunakan persamaan Gaussian dengan rumus:

g(x, \mu, \sigma)=\frac{1}{\sqrt{2\pi}\sigma}e^{-\frac{x {μ^2}}{2 \sigma^2}}

dengan x adalah tiap data baru tadi, σ (sigma) adalah standar deviasi dan μ (mu) adalah nilai mean, misal:

g(x, \mu, \sigma)=\frac{1}{\sqrt{2\pi}*0.57735}e^{-\frac{1*1.5^2}{2*0.57735^2}}

Maka diperoleh:

| income |   age    | student  | credit_rating | buys_computer |
| :----: | :------: | :------: | :-----------: | :-----------: |
|  high  | 0.013347 | 0.397465 |   0.450386    |   0.268075    |
| medium | 0.020201 | 0.436085 |   0.411145    |   0.436085    |
|  low   | 0.014866 |    -     |   0.390046    |   0.146219    |

Lalu kalikan semua atribut yang sejajar dengan class, sehingga hasilnya:

| income |   age    | student  | credit_rating | buys_computer |  hasil   |
| :----: | :------: | :------: | :-----------: | :-----------: | :------: |
|  high  | 0.013347 | 0.397465 |   0.450386    |   0.268075    | 0.00064  |
| medium | 0.020201 | 0.436085 |   0.411145    |   0.436085    | 0.001579 |
|  slow  | 0.014866 |    -     |   0.390046    |   0.146219    | 0.000848 |

Dari hasil tersebut, data terbesar merupakan class medium, jadi jika terdapat sample data (`age <=30, student = "yes", credit_rating = "fair", buys_computer = "yes"`) tapi tidak ada data income, maka kemungkinan besar income-nya adalah medium.
