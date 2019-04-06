## ǰ��
���Ӱ�Ӿ�����Ƚ�����˼��Ԫ��������, ��ȻŪ����һ���������Ͷע��������ѧЩ����ѧϰing�����������ܷ�ͨ������ѧϰ��Ԥ����������

> ע: ���ﵱȻ�κ�û�й�����ҶĲ�����˼���������֡�

> Ϊ�˱���ֱ�ӱ���������ʵս�У���������ʹ�õ���**�¼�������**������.

Դ����: [����ѧϰ������](https://github.com/youerning/blog/tree/master/ml_and_horse_race)


## ���½ṹ
- ���ݻ�ȡ
- ���ݷ���
- ���ݿ��ӻ�
- ����ѧϰ
- �ܽ�

## ���ݻ�ȡ
�����¼��µ������վ����ֱ�ӷ�����Ҫ���ӣ�����û�бȽϺõ����ӣ����Բ��õ��̷߳��ʣ��±�����IP������Ȥ�Ŀ������бȽϺõ�ǽ�����Ļ������Լ��϶��̻߳��߶�Э��. ��scrapy֮��Ŀ���õĲ��࣬������д�ˡ�

��Ȼ�ܼ򵥣����Ǵ���Ҳ��300���У�����ֻ���߼���Դ�������ֱ�Ӳ鿴Դ���롣

### �ҳ�����
����**�۲�**��������ÿ�յ���������209/01/01֮�����һ��������IDֵ��2009/01/01��IDֵ��1����һ��������2���Դ����ƣ���ֹ��2019/03/29�գ�IDֵΪ8375.

����ʷ���ͨ���������ʽ����:
```
http://cn.turfclub.com.sg/Racing/Pages/ViewRaceResult/<ID>/All

��:
http://cn.turfclub.com.sg/Racing/Pages/ViewRaceResult/1/All
```
��˱�������ID��Χ���ܻ�ȡ������ʷ�����
����ʾ������:
```
base_url = "http://cn.turfclub.com.sg/Racing/Pages/ViewRaceResult/%s/All"
for num in range(start_num, 8376):
    url = base_url % num
    soup = download(url)
        
```

### �ҳ�����
����**�۲�**�����۾�����Ҫ�����ֶΡ�

![img/columns.png](img/columns.png)


### �洢����
Ϊ�˼��ٶ����ݿ����������ͨ��sqlite3�洢����.
����sqlite3�����ݸ�ʽ�洢�����csv�Ľ��������Դ����ֿ�鿴��

Sqlite3���ݽṹ����:

```
CREATE TABLE IF NOT EXISTS DATA
   (ID CHAR(30) PRIMARY KEY     NOT NULL,
   DATE         CHAR(20)    NOT NULL,
   LOCATION     CHAR(30) NOT NULL,
   LENGTH       INT     NOT NULL,
   TRACK        CHAR(30) NOT NULL,
   TRACK_TYPE   CHAR(30),
   TRACK_STATUS CHAR(30)     NOT NULL,
   RACE_NUM     INT     NOT NULL,
   H_NO         INT     NOT NULL,
   HORSE_NAME   CHAR(30)     NOT NULL,
   GEAR         CHAR(30),
   HORSE_RATING INT     NOT NULL,
   H_WT         REAL     NOT NULL,
   HCP_WT       REAL     NOT NULL,
   C_WT         REAL     NOT NULL,
   BAR          INT     NOT NULL,
   JOCKEY       CHAR(30)     NOT NULL,
   TRAINER      CHAR(30)     NOT NULL,
   RUNING_POSITION   CHAR(10)     NOT NULL,
   PI           INT     NOT NULL,
   TOTAL_SECONDS     INT,
   LBW          REAL     NOT NULL
   );
```


### С��
������˼���ǣ�����Щ�����������¼��µĽ�������������ҵĽ������Ҳ��֪��Ϊɶ����������ֻȡ�¼��µ����ݽ����

���о����е�IDֵû�н������Ҳ��֪��Ϊɶ��


> ע: �ڻ�ȡ�����У���Щ���ִ���Ĳ����Ƿǳ��ã�����һЩ�ַ������͵����ݣ�ժȡ�Ĳ����Ƿǳ�׼ȷ, ����GitHub�ֿ������ṩ�������ļ�����һС���ֻ������⣬ϣ����֪Ϥ��

## ���ݷ���
��һ�����ǽ�����������������һ�ھ��ǽ����ݽ���һЩͳ�Ʒ�������ͼ����һЩ���еĹ��ɡ�

### ׼������
���ȵ���python���ݷ���������

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```

�����������ͨ��pandas���ء�

```
import sqlite3
conn = sqlite3.connect('data.db')
df = pd.read_sql("SELECT * FROM DATA", conn, index_col="ID", parse_dates=["DATE"])
```

### �������
�鿴����
df.head()
```
DATE	LOCATION	LENGTH	TRACK	TRACK_TYPE	TRACK_STATUS	RACE_NUM	H_NO	HORSE_NAME	GEAR	...	H_WT	HCP_WT	C_WT	BAR	JOCKEY	TRAINER	RUNING_POSITION	PI	TOTAL_SECONDS	LBW
ID																					
2009-01-01-1-3-1	2009-01-01	�¼���	1700	unkonw	(POLYTRACK)	����	1	10	WINNIEDUN		...	440.0	52.0	52.0	3	M AU	HK TAN	1-1-1	1	0.0	0.0
2009-01-01-1-9-2	2009-01-01	�¼���	1700	unkonw	(POLYTRACK)	����	1	2	REGAL KNIGHT		...	457.0	59.0	57.0	9	E ASLAM	L TRELOAR	9-5-2	2	0.0	0.5
2009-01-01-1-10-3	2009-01-01	�¼���	1700	unkonw	(POLYTRACK)	����	1	3	JOYLUCK		...	477.0	58.5	58.5	10	N CALLOW	RB MARSH	11-10-3	3	0.0	1.3
2009-01-01-1-1-4	2009-01-01	�¼���	1700	unkonw	(POLYTRACK)	����	1	1	MAJESTIC KNIGHT		...	521.0	59.0	55.0	1	T. AFFANDI	L TRELOAR	4-3-4	4	0.0	1.8
2009-01-01-1-8-5	2009-01-01	�¼���	1700	unkonw	(POLYTRACK)	����	1	7	ELEVENTH AVENUE		...	477.0	54.5	54.5	8	R FRADD	M FREEDMAN	8-8-5	5	0.0	2.6
```

����ͳ��
df.descibe()
```

LENGTH	RACE_NUM	H_NO	HORSE_RATING	H_WT	HCP_WT	C_WT	BAR	PI	TOTAL_SECONDS	LBW
count	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000	88110.000000
mean	1331.634321	5.464317	6.324413	47.422812	495.280524	54.975701	54.326813	6.137975	6.339610	79.863567	5.974457
std	256.724820	2.977882	3.494310	20.767828	31.383475	2.532528	2.667349	3.383717	5.787673	20.725862	5.966324
min	1000.000000	1.000000	1.000000	0.000000	372.000000	45.500000	0.000000	0.000000	1.000000	0.000000	0.000000
25%	1200.000000	3.000000	3.000000	40.000000	474.000000	53.000000	52.500000	3.000000	3.000000	70.052500	2.100000
50%	1200.000000	5.000000	6.000000	49.000000	494.000000	55.500000	55.000000	6.000000	6.000000	73.650000	4.900000
75%	1600.000000	8.000000	9.000000	59.000000	516.000000	57.000000	56.500000	9.000000	9.000000	94.980000	8.200000
max	2400.000000	12.000000	18.000000	127.000000	647.000000	59.500000	59.500000	16.000000	99.000000	640.980000	99.800000
```

### �еķ�ʸ
�鿴�Լ�����Ȥ������

#### �鿴ÿƥ��ÿ���������ٶ�
����ȥ��total_secondsΪ��ĳ���

��ʵ��Ӧ�ý�ʱ���ֶε�ԭʼ���ݱ��������ģ�����ԭʼ������ʵ��0:00.00, 

��������Ϊ����ʱ�䵥λһ�����������β�һ����������ʱ�䵥λ�ϻ�����һ����ͷ��ľ������100��������ͷ��ľ�����1����ô1/100 ����10����

��������Ӧ��ȥ��С��1������, ����������ʵ������Щ�쳣������ȥ��С��50�Ľ��
```

df2 = df.query("TOTAL_SECONDS > 50")
df2["SPEED"] = df["LENGTH"] / df["TOTAL_SECONDS"]
df2["SPEED"].head()

ID
2009-04-03-1-8-1     16.605385
2009-04-03-1-5-2     16.568047
2009-04-03-1-7-3     16.560208
2009-04-03-1-10-4    16.554334
2009-04-03-1-3-5     16.495817
Name: SPEED, dtype: float64
```


#### �鿴ÿ����ʦÿ���������ٶ�

```
df2[["SPEED", "JOCKEY"]].groupby("JOCKEY").mean().sort_values(by="SPEED").tail()


            SPEED
JOCKEY	
��ά��	16.899374
ۭ����	16.952015
Ѧ����	16.969355
������	16.973066
������	17.204301

df2[["SPEED", "JOCKEY"]].groupby("JOCKEY").mean().mean()
SPEED    16.400328
dtype: float64
```


## ���ݿ��ӻ�
���ӻ��Լ�����Ȥ������ֵ

���ӻ��ٶȷֲ�

```
df2[["SPEED", "HORSE_NAME"]].groupby("HORSE_NAME").mean().hist(bins=20)
```
![img/speed_hist](img/speed_hist.png)

���ӻ���ƥ�ٶȵ���ʷ����

```
# ������һƥ��ʷ�������������������ƥ

speed_and_horse = df2[["SPEED", "HORSE_NAME"]]
pd.value_counts(speed_and_horse["HORSE_NAME"]).head()

������       89
��������      77
PACINO    71
̫���۹�      69
�׿���       68
Name: HORSE_NAME, dtype: int64

speed_and_horse.query('HORSE_NAME == "������"').plot(figsize=(16,9))
```
![img/history_speed](img/history_speed.png)

���Է�����ƥ����18����ǰ�����ϻ�����16.25���������ǻ�, ���ò����� ����18���Ժ�Ͳ����ˣ��������˰�

���Ǻ��п��������������������ǽ���������ǰ20����ƥ�����Ƴ���


˳�����һ�����������ǰ��ʮƥ�����ʷ���ݡ�

```
#  ���ȿ���ǰ��ʮ����ƥ
pd.value_counts(speed_and_horse["HORSE_NAME"]).head(20)

������                89
��������               77
PACINO             71
̫���۹�               69
�׿���                68
LUCKY SUN          67
NINTH AVENUE       66
��������               66
������                66
SHINKANSEN         65
DAAD'S THE WAY     65
��������               64
�°�                 64
INCREDIBLE HULK    64
����ʯ                64
ʥ��                 64
���                 64
���ӿ쳵               64
�޴����               64
CONQUEST           63
Name: HORSE_NAME, dtype: int64


plot_df = pd.DataFrame()
plt.rcParams['font.sans-serif'] = ['simhei']
for horse_name in pd.value_counts(speed_and_horse["HORSE_NAME"]).head(20).index:
    df_horse = speed_and_horse.query(f'HORSE_NAME == "{horse_name}"')["SPEED"].iloc[:63]

    plot_df[horse_name] = df_horse.reset_index()["SPEED"]


plot_df.plot(figsize=(16,9))
```
![img/history_speed20](img/history_speed20.png)


## ����ѧϰ
��֪����Ƿ�֪��������Ĺ������������������˭���ٶ���죬˭�ͻ�ʤ��������ҪԤ�����������Ӧ���ǱȽ�˭���ٶȿ죬�����ǿ��������εĸ��ʣ�����֮������һ���ع�����⡣

����ͳ������Իع�ɡ�
> Ϊɶ�������������ѧϰʲô�ģ�����ѽ

### ����ѡ��
����ѡ��������Ԥ��ֵ��Ԥ��ֵ�ܺ�ȷ��������ǰ����ٶȡ�

���ȿ�ֱ��ѡ�����������ӻ����¡�����ѡ���������C_WT(���)���Լ�HORSE_RATING(��ƥ����)��

> �����ָ������ƥ�䱸������������������ھ������ñ��ֱ�����ÿƥ���״̬��࣬��ǿ������

> ��ƥ�������������ƶ��Ĺ����֡�

���ӻ�һ��C_WT��SPEED֮��Ĺ�ϵ

```
# ���ﻹ��ѡ��鿴  "������"��ƥ��

df2.query('HORSE_NAME == "������"')[["C_WT", "SPEED"]].reset_index().plot.scatter(x="C_WT", y="SPEED", figsize=(16,9))

```
![img/c_wt_speed_cor](img/c_wt_speed_cor.png)

��ͼ������ɶ�����Ǵ��֪������ûɶ����ԣ��ɽ���seaborn��ֱ�۵Ŀ��ӻ�һ��


```
import seaborn as sns
j = sns.jointplot("C_WT", "SPEED", data=df2.query('HORSE_NAME == "������"')[["C_WT", "SPEED"]].reset_index(), kind="reg")
# j = sns.jointplot('Num of A', ' Ratio B', data = data_df, kind='reg', height=8)
j.annotate(stats.pearsonr)
```
![img/sns_c_wt_cor](img/sns_c_wt_cor.png)


���ӻ�һ��HORS_RATING��SPEED֮��Ĺ�ϵ

```
import seaborn as sns
import scipy.stats as stats

j = sns.jointplot("HORSE_RATING", "SPEED", data=df2.query('HORSE_NAME == "������"')[["HORSE_RATING", "SPEED"]].reset_index(), kind="reg")
j.annotate(stats.pearsonr)
```
![img/sns_h_rating_cor](img/sns_h_rating_cor.png)

�����Ի���ûɶ��ϵ��

��ʵ�����̫����ǲ��ʺ��������������ֲ������Ϊ�������һ������ʵս��ģ�ͣ�����ͽ�����������Ϊ�����ɡ�

> Ϊ�˻���ѧϰ��ѧϰ�ɣ� ǿ����ϣ�����

### ���ģ��
ѡһ��ģ�ͣ�����ѡ��LinearRegression��

```
from sklearn.linear_model import LinearRegression
df_lll = df2.query("HORSE_NAME == '������'")[["SPEED", "C_WT", "HORSE_RATING"]]
split_index = int(len(df_lll) * 0.6)
X_Train = df_lll[:split_index][["C_WT", "HORSE_RATING"]]
Y_Train = df_lll[:split_index][["SPEED"]]
X_Test = df_lll[split_index:][["C_WT", "HORSE_RATING"]]
Y_Test = df_lll[split_index:][["SPEED"]]

model = LinearRegression()
model.fit(X_Train.values, Y_Train.values)
```

�������ϵ�ģ�Ϳ��ӻ�һ��

```
from mpl_toolkits.mplot3d import Axes3D
fig = plt.figure()
ax = Axes3D(fig)
ax.set_xlabel("C_WT")
ax.set_xlabel("HORSE_RATING")
ax.set_xlabel("SPEED")
ax.scatter(X_Train["C_WT"].values, X_Train["HORSE_RATING"].values, Y_Train.values)
ax.plot_surface(X_Train["C_WT"].values, X_Train["HORSE_RATING"].values, model.predict(X_Train.values))
```
![img/model](himg/model.png)



## �ܽ�
��ʵ�ڻ���ѧϰ��һ��Ӧ�ý���������һ�£�����˵��ϴһ�¡�����û��ϵ��������֪��ûɶ����ϵġ�

���ڱ��ĵ�notebookҲ��Դ�������档�п���д��


## ���
��ʵ���ﲻӦ�û���������ģ�ͣ���Ϊ�����ĳɼ����ȷǳ��ߣ����߻��кܶ���������ŵĽ�����������ۻع黹�Ƿ���Ľ�������ܾ�ȷ���������ս��(����Ҳ�п������ҵ�ˮƽ����)��

��Ȼ����Ϊɶ��дƪ���£���֤һ�¿���

���Ǿ͸��˶��ԣ��Ҿ��û��ǿ�������һ�������и��ʵģ�û��Ҫ��ô��ȷ����ô�������ʵĹؼ����ھ�ֵ�ع飬��ÿƥ����ٶȻ�Χ����һ����ֵ�����𶯣�����������Ȥ����������һ����ϸ�µķ����ɡ�


