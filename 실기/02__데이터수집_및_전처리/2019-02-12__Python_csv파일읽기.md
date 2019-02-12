## 파이썬으로 csv파일 읽기 정리
csv파일은 데이터 과학에서 가장 흔하게 접하는 데이터 형식입니다.  
콤마(,)로 구분하며 탭이나 파이프(|)를 구분 문자로 사용하는 .tsv, .psv 확장자도 있습니다.  
.  
.  
'iris.csv'를 파이썬으로 읽는 방법
  
1. **파이썬에 기본 내장된 csv 모듈** 
* CSV 파일을 읽기 위해서는 먼저 파이썬에 기본 내장된 csv 모듈을 import 한다. 
* 다음 .csv 파일을 오픈하고 파일객체를 csv.reader(파일객체) 에 넣으면 된다. 
* csv.reader() 함수는 Iterator 타입인 reader 객체를 리턴하므로 for 루프를 돌며 한 라인씩 가져올 수 있다. 
* 이때 리턴되는 각 라인은 컬럼들을 나열한 리스트(list) 타입이다.

```python
import csv

f = open('iris.csv','r', encoding="utf-8")
iris_csv = csv.reader(f)
for row in iris_csv:
    print(row)
f.close()
```
리턴 값은 다음과 같다
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
```
각 열의 값이 리스트로 출력되는 것을 볼 수 있다.  
조금 더 예쁘게 출력하고자 한다면  
```python
import csv

with open('iris.csv') as csv_file:
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
```
조금..은 예뻐졌다.!!
