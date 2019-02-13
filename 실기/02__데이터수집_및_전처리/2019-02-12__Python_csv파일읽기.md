## 파이썬으로 csv파일 읽기 정리
csv파일은 데이터 과학에서 가장 흔하게 접하는 데이터 형식입니다.  
콤마(,)로 구분하며 탭이나 파이프(|)를 구분 문자로 사용하는 .tsv, .psv 확장자도 있습니다.  
.  
.  
'iris.csv'를 파이썬으로 읽는 예제로 여러 방법들을 알아보자
1. **기본 파이썬으로 csv 파일 읽기**
* csv 파일을 `'r'`모드로 열고 맨 윗줄을 `header`에 담아 `header_list`를 뿌려준다.
* header를 제외한 열들은 `for`문으로 한 열씩 출력한다.  
```python
IRIS_FILE = "iris.csv"
with open(IRIS_FILE, 'r', newline='') as file_reader:
    header = file_reader.readline()	# 첫 행 읽기
    header = header.strip()
    header_list = header.split(',')
    print(header_list)
    for row in file_reader:
        row = row.strip()		# 문자열의 양끝 공백, 탭, 개행문자 제거
        row_list = row.split(',')
        print(row_list)
```
출력 값은 다음과 같다
```
['"Sepal.Length"', '"Sepal.Width"', '"Petal.Length"', '"Petal.Width"', '"Species"']
['5.1', '3.5', '1.4', '0.2', '"setosa"']
['4.9', '3', '1.4', '0.2', '"setosa"']
['4.7', '3.2', '1.3', '0.2', '"setosa"']
['4.6', '3.1', '1.5', '0.2', '"setosa"']
['5', '3.6', '1.4', '0.2', '"setosa"']
['5.4', '3.9', '1.7', '0.4', '"setosa"']
['4.6', '3.4', '1.4', '0.3', '"setosa"']
['5', '3.4', '1.5', '0.2', '"setosa"']
.
.
.
```
헤더를 포함한 각 행이 값의 리스트로 표현되는 것을 볼 수 있다.  
.  
.  
2. **파이썬에 기본 내장된 csv모듈을 사용하여 csv파일 열기** 
* CSV 모듈을 사용하여 csv 파일을 읽기 위해서는 먼저 파이썬에 기본 내장된 csv 모듈을 import 한다. 
* 다음 .csv 파일을 오픈하고 파일객체를 csv.reader(파일객체) 에 넣으면 된다. 
* csv.reader() 함수는 Iterator 타입인 reader 객체를 리턴하므로 for 루프를 돌며 한 라인씩 가져올 수 있다. 
* 이때 리턴되는 각 라인은 컬럼들을 나열한 리스트(list) 타입이다.

```python
import csv

IRIS_FILE = "iris.csv"
with open(IRIS_FILE, 'r', newline='') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=",")
    for row in csv_reader:
        print(row)
```
출력 값은 다음과 같다
```
['Sepal.Length', 'Sepal.Width', 'Petal.Length', 'Petal.Width', 'Species']
['5.1', '3.5', '1.4', '0.2', 'setosa']
['4.9', '3', '1.4', '0.2', 'setosa']
['4.7', '3.2', '1.3', '0.2', 'setosa']
['4.6', '3.1', '1.5', '0.2', 'setosa']
['5', '3.6', '1.4', '0.2', 'setosa']
['5.4', '3.9', '1.7', '0.4', 'setosa']
['4.6', '3.4', '1.4', '0.3', 'setosa']
['5', '3.4', '1.5', '0.2', 'setosa']
['4.4', '2.9', '1.4', '0.2', 'setosa']
['4.9', '3.1', '1.5', '0.1', 'setosa']
.
.
.
```
각 열의 값이 리스트로 출력되는 것을 볼 수 있다.  
조금 더 예쁘게 출력하고자 한다면  
```python
import csv

IRIS_FILE = "iris.csv"
with open(IRIS_FILE, 'r', newline='') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter=",")
    line_count = 0
    for row in csv_reader:
        if line_count == 0:
            print(f'{", ".join(row)}')
            line_count += 1
        else:
            print(f'\t{", ".join(row)}')
            line_count += 1
    print(f'총 {line_count-1} 개의 데이터가 있습니다.')
```
위와 같이 읽고 출력해보자  
```
Sepal.Length, Sepal.Width, Petal.Length, Petal.Width, Species
	5.1, 3.5, 1.4, 0.2, setosa
	4.9, 3, 1.4, 0.2, setosa
	4.7, 3.2, 1.3, 0.2, setosa
	4.6, 3.1, 1.5, 0.2, setosa
	5, 3.6, 1.4, 0.2, setosa
	5.4, 3.9, 1.7, 0.4, setosa
	4.6, 3.4, 1.4, 0.3, setosa
	5, 3.4, 1.5, 0.2, setosa
	4.4, 2.9, 1.4, 0.2, setosa
	4.9, 3.1, 1.5, 0.1, setosa
	5.4, 3.7, 1.5, 0.2, setosa
	.
	.
	.
	6.7, 3, 5.2, 2.3, virginica
	6.3, 2.5, 5, 1.9, virginica
	6.5, 3, 5.2, 2, virginica
	6.2, 3.4, 5.4, 2.3, virginica
	5.9, 3, 5.1, 1.8, virginica
총 150 개의 데이터가 있습니다.
```
조금..은 예뻐졌다.!!  
.  
.  
3. **Pandas로 csv파일 열기**
Pandas패키지를 이용해서 csv파일을 읽어보자.  
```python
import pandas as pd

iris_df = pd.read_csv(IRIS_FILE)
print(iris_df)
```
??????????? 끝이다.. 간단쓰.. 출력 값은 다음과 같다.  
```
     Sepal.Length  Sepal.Width  Petal.Length  Petal.Width    Species
0             5.1          3.5           1.4          0.2     setosa
1             4.9          3.0           1.4          0.2     setosa
2             4.7          3.2           1.3          0.2     setosa
3             4.6          3.1           1.5          0.2     setosa
4             5.0          3.6           1.4          0.2     setosa
5             5.4          3.9           1.7          0.4     setosa
6             4.6          3.4           1.4          0.3     setosa
.
.
.  
144           6.7          3.3           5.7          2.5  virginica
145           6.7          3.0           5.2          2.3  virginica
146           6.3          2.5           5.0          1.9  virginica
147           6.5          3.0           5.2          2.0  virginica
148           6.2          3.4           5.4          2.3  virginica
149           5.9          3.0           5.1          1.8  virginica

[150 rows x 5 columns]
```
여기서 기존의 기본 파이썬, csv 모듈 방식과 다른 점은 `pd.read_csv(IRIS_FILE)`의 리턴 값이 데이터 프레임 이라는 자료형 이라는 것!  
R에서 데이터 프레임을 처음 접했었지만 파이썬에도 있었다! 역시나..  
파이썬의 기본 자료형은 아니기 때문에 사용에 유의하자! 나중에 NumPy나오면 한 번 더 얘기하자!
