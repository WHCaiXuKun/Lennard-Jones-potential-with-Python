# Lennard-Jones-potential-with-Python
### Pythonを用いた空気のLennard-Jonesポテンシャルの分析
![][1]  
- [Lennard Jones potential][1]
- [Data][2]  
### 概要  
空気における分子間ポテンシャルエネルギーU[ev]は次の公式より計算する  
![](https://latex.codecogs.com/gif.latex?U%20%3D%204%20%5Cvarepsilon%20%5Cleft%5C%7B%20%5Cleft%28%20%5Cfrac%7B%5Csigma%20%7D%7Br%7D%20%5Cright%29%5E%7B12%7D%20-%20%5Cleft%28%20%5Cfrac%7B%5Csigma%20%7D%7Br%7D%20%5Cright%29%5E%7B6%7D%20%5Cright%5C%7D)....(1)

ここで、rは分子間距離、εは最小エネルギーポテンシャル、σは分子パラメータで、空気の場合σ=3.711Å及びε/k＝78.6Kである。ボルツマン係数k=1.38x10^-23J/kである。−6乗の引力項は、二つの原子の間の分散力、すなわち双極子-双極子間の相互作用によるものである。原子の永久双極子がゼロであっても、短時間をとった場合は電荷分布の揺らぎによる双極子が現れる。この双極子の電場により、もう一方の原子が分極し、誘起双極子が生じる。この相互作用ポテンシャルは原子間距離の-6乗に比例したものとなる。

一方、−12乗の斥力項は、電子雲の重なりによって反発力が働くためである。指数の−12は、−6乗のちょうど2乗で扱いやすいために選ばれることが多い。反発力の主な機構は、パウリの排他律によって、低いエネルギーの分子軌道に電子が入れないためである。

気体分子間の位置エネルギー（ポテンシャル）を数式を用いて近似的に表した一例で、気体分子の輸送現象（平均自由行程、拡散、粘性など）を考える場合に必要な、気体分子の直径を与える。 Lennard-Jones (1894-1954)は英国の物理化学者。   

```
df = pandas.read_excel("Lennard-Jones.xlsx")
df = df.loc[5:25, ["Unnamed: 1", "Unnamed: 3"]]
df.columns = ["オングストローム", "ポテンシャル"]
df.index = list(range(1,22))
```
データを読み込んだ後、必要なデータはオングストロームとポテンシャル二つしかないので、σ[Å]、	ε/k[K]、ｋ[J/K]などは削除して、df.loc[5:25, ["Unnamed: 1", "Unnamed: 3"]]でオングストロームとポテンシャルの数値だけを取った。これを新たのdfにした。dfの内容を確認すると、columnsとindexはごちゃごちゃして筋道が通っていないので、df.columns = ["オングストローム", "ポテンシャル"]でcolumnsの名前と数値を対応づけた。で、indexも５からではなく、１からにした。描いた曲線は円滑、平滑線でないため、
```
import matplotlib.pyplot as plt
import numpy as np
from matplotlib import font_manager
from scipy.interpolate import make_interp_spline
my_font = font_manager.FontProperties(fname="/System/Library/Fonts/ヒラギノ明朝 ProN.ttc")#fontを得る

x_smooth = np.linspace(x.min(), x.max(), 300)
y_smooth = make_interp_spline(x, y)(x_smooth)　#滑らかな曲線を描く
x, y = df["オングストローム"], df["ポテンシャル"]
plt.figure(figsize=(20, 8), dpi=80)
plt.title("図１空気のLennard-Jonesポテンシャル", fontproperties=my_font, size=20)
plt.xlabel("オングストローム", fontproperties=my_font, size=20)
plt.ylabel("ポテンシャル", fontproperties=my_font, size=20)
plt.plot(x_smooth, y_smooth, c="red")
plt.savefig("図１　空気のLennard-Jonesポテンシャル.png")
plt.show()
```
make_interp_splineにより、x軸をx_smooth、y軸をy_smoothで、平滑線を描くことができた。

[1]:https://github.com/Xiong-yinghao/Lennard-Jones-potential-with-Python/blob/main/%E5%9B%B3%EF%BC%91%E7%A9%BA%E6%B0%97%E3%81%AELennard-Jones%E3%83%9B%E3%82%9A%E3%83%86%E3%83%B3%E3%82%B7%E3%83%A3%E3%83%AB.png?raw=true

[1]:https://github.com/Xiong-yinghao/Lennard-Jones-potential-with-Python/blob/main/Lennard-Jones.ipynb
[2]:https://github.com/Xiong-yinghao/Lennard-Jones-potential-with-Python/blob/main/Lennard-Jones%E3%83%9B%E3%82%9A%E3%83%86%E3%83%B3%E3%82%B7%E3%83%A3%E3%83%AB.csv
