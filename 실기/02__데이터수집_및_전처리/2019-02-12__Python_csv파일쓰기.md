## 파이썬으로 csv파일 쓰기 정리
.  
.  
.  
* 데이터를 새로운 csv파일로 만드는 방법에 대해 정리해 보자  
* 임의의 데이터 'file'을 생성해주자
```python
file = []
file_header = ['Mon','Tue','Wed','Tur','Fri','Sat','Sun']
file.append(file_header)
file.append([1,1,1,1,1,1,1])
file.append([2,2,2,2,2,2,2])
file.append([3,3,3,3,3,3,3])
```

1. **파이썬 기본 코드**  
```python
OUT_CSV = 'out.csv'
with open(OUT_CSV, 'w', newline='')as csv_out_file:
    csv_out_file.write(','.join(file[0]) + '\n')
    for row in range(1, len(file)):
        csv_out_file.write(','.join(map(str,file[row])) + '\n')
```
* 임의의 리스트 `file`을 만들어서 'out.csv'로 쓰는 코드이다.  
* `'w'`(쓰기:write)로 `file[0]`(헤더 영역) 그리고 반복문으로 3개의 열을 'out.csv'에 출력한다.  
![image](https://user-images.githubusercontent.com/34496143/52693490-36b09a00-2faa-11e9-88d7-eb8ea94d9b2f.png)
.  
.  
.  
2. **csv모듈 사용**  
```python
OUT_CSV = 'out.csv'
with open(OUT_CSV, 'w', newline='') as csv_out_file:
    file_writer = csv.writer(csv_out_file, delimiter=',')
    for row in file:
        file_writer.writerow(row)
```
* `csv.writer()`함수를 사용하여 출력 파일에 쓰는 데 사용할 `file_writer`객체를 만든다.  
* 이 함수의 두 번째 인수 `delimiter=','` 는 기본값 이므로 입력 및 출력 파일이 ','로 구분됐다면 굳이 쓰지 않아도 된다.  
* 세미콜론';', 또는 탭'\t' 등으로 구분된 파일이라면 인수를 지정해야 한다.  
.  
.  
.  
3. **Pandas 사용**
```python
OUT_CSV = 'out.csv'
file_df = pd.DataFrame(data=file[1:], columns=file[0])
file_df.to_csv(OUT_CSV, mode='w', index=False)
```  
* 임의의 데이터 file을 **Pandas**의 데이터프레임 자료형으로 변환하여 `file_df`변수에 담고  
* `to_csv()`함수를 사용하면 저장 완료.. 정말 간단하다.
