---
title: "g++ in Ubuntu16.04"
excerpt: "Ubuntu 16.04버전에서 g++ 사용하기?"

categories:
  - Linux
tags:
  - Linux
  - c++
  - g++
  - String
last_modified_at: 2020-07-26
---  

## g++ -std=c++11
- 프로그램 코드 작성을 마치고 Ubuntu 16.04 환경에서 g++을 이용해 컴파일을 하던 도중 오류가 발생하게 되었다. 오류는 아래와 같다.
```
xxxx.cpp: In function ‘int main(int, char**)’:
xxxx.cpp:45:47: error: ‘to_string’ was not declared in this scope
     string x = to_string(Table[tableIdx].first); x.append("\n"); 
```  
- 오류에 대해 찾아보던 도중 to_string()이 c++11 이상에서만 작동이 된다는 것을 알게 되었다. 따라서 g++ 의 std 버전을 c++11로 맞추어 컴파일을 수행해줘야 한다는 것을 알게 되었다. 
컴파일을 하는 방법은 아래와 같다.

```
g++ -std=c++11 [xxx.cpp] -o xxx
```  
