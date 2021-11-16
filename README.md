# JEP 적용 방법
JEP 라이브러리는 Microsoft Visual C++ 2019 컴파일러와 호환이 되지 않는 경우가 발생할 수 있다.   
전부 삭제 한 후, Microsoft Visual C++ 2017 Build Tools를 다운받는다. (Microsoft Visual C++ Community를 이용해서 다운받으면 편함)
>[JEP](https://github.com/ninia/jep)   
해당 링크에서 JEP 라이브러리를 다운받은 상태에서 CLI로 JEP 라이브러리의 setup.py가 존재하는 경로로 접근해 
```python
python setup.py build
```
명령어를 통해 build 폴더를 생성한 후 
CLI(관리자로 접속)에서 
```ts
pip install jep
```
명령어 실행 후, 만약 mt.exe를 찾을 수 없다는 에러가 뜬다면 

>시스템 환경 변수 -> Path
```
C:\Program Files (x86)\Windows Kits\10\bin\10.0.17763.0\x86
```
경로를 추가한다.
```ts
pip show pip
pip show jep
```
를 통해 인터프리터 Location 확인 후, 
```java
Jep jep = new Jep(false, 해당 Location);
```
으로 객체 JEP 객체를 생성한다.

만약 *no jep in java.library.path* 에러가 뜰 경우, 
>시스템 환경 변수 -> Path
```
본인의 파이썬 설치 경로 
python executable ex) ...\\Python\\Python38\\Lib\\site-packages, ...\\Python\\Python38\\Lib\\site-packages\jep
```
두 개의 경로를 추가한 후 재부팅한다.

>**그래도 안될 경우**    
위의 방법에서 setup.py를 통해 build한 jep.jar 파일이 아닌 pip install jep를 통해 build한 jep.jar를 프로젝트의 build path에 추가한다.

그 후 프로젝트를 run하면 pandas, numpy 등등 파이썬 외부 모듈이 정상적으로 import 되어지는 것을 확인할 수 있는데 
```python
from ortools.linear_solver import pywraplp
```
와 같은 **Microsoft Visual C++ 2019 compiler에 의존**하는 모듈들이 문제가 생길 수 있다.   
그럼 Microsoft Visual C++ 2019 compiler를 다운받으면 정상적으로 import가 가능해진다.

* 참고로 Jython은 Python 2.7 version 이후로 업데이트가 없기 때문에 numpy, pandas 등 외부 모듈 사용에 제한이 있음.

