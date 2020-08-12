# 수업 2교시
- 생각 해 보세요 왜 리눅스-윈도우 공유폴더에서 빌드 하면 안되는지
  - 권한? 소유자 소유그룹 퍼미션 문제입니까?
    - 호스트 윈도우에서 공유폴더에서 파일하나, 디렉하나
      - 윈도우 7708
    - 게스트 리눅스에서 공유폴더 아래에 파일하나 디렉하나
      - 770권한 77
  - 리눅스 OS와 윈도우즈 대문자 소문자 구별시스템
    - 윈도우에서는 대소문자 구별이 없는데
    - 리눅스
  - 심볼릭링크 하드링크 등등..
    - 리눅스에서 인지하는데 윈도우에서 인지하지 못하는 , 특수파일 인지의 문제 
  - 결론 : 공유폴더에서 빌드하면 생기는 문제 -> 실수가 생긴다! 작업은 표준에서
    - 퍼미션 / 특수파일(링크, 파이프파일) / 파일경로 파일명 대소문자구별
    - 결국 os차이
- 리눅스유닉스에서 인식하는 파이프파일
- 결국 리눅스 디펜던시 한 것들은 공유폴더에서 하지 마라
```s
$ ls -l mypipe 
```
```s
prw-rw-r-- 1 dhkim dhkim 0  8월 10 13:50 mypipe
```    
- 심볼릭 링크파일
```
$ ln -s ~/Downloads/ sd
```
  - 이후 sd 열어보면 
> 00번 문제 챕터1 
```cpp
#include <stdio.h>
#define	NO	1000
int gv1 = 10, gv2 = 20;
int gv3;
int main(void)
{
    int lv1 = 1, lv2 = 2, lv3;
    printf("Main Start..\n");
#ifdef DEBUG
    printf("gv1:%d, gv2:%d, gv3:%d\n", gv1, gv2, gv3);
    printf("lv1:%d, lv2:%d, lv3:%d\n", lv1, lv2, lv3);
#endif
    lv3 = NO;
    printf("lv1:%d, lv2:%d, lv3:%d\n", lv1, lv2, lv3);
    printf("Main End...\n");
    return 0;
}
	

```
- #ifdef DEBUG : 라는게 DEBUG 가 선언되어 있으면 
- 리눅스에서는 실행파일의 확장자가 중요하지 않다. 
- 리눅스 커맨드는 대부분 c로 이루어져있다. 쉘 커맨드는 실행파일의 이름이였던것이다!!!
> gcc --save-temps 00.option-o.c
- 중간에 임시파일을 생성해라가 바로 이 ㅇㅂ션 
- 명령어 :  ll | ls 00.*
```s
00.option-o.c  00.option-o.i  00.option-o.o  00.option-o.s
```
  - 실행하는 주체인 하드웨어 CPU가 알아먹으려면 오직 기계어, 머신랭기지, 바이너리
  - 오픈소스 가져다 쓸때는 링커, 두번째가 전처리기(맨앞이 그다음이 맨 뒤가 )
> 프리프로세싱 과정
```s
$ gcc -E 00.option-o.c 
$ gcc -E 00.option-o.c > prepros.txt
```
- sdf
- sdf
- 
> 어셈블리 만들기
```s
$ gcc -S 01.option-E.i 
$ gcc -S 01.option-E.c 
```
- 확장자에 따라서 알아서 선택해주는게 gcc다 
- gcc는 사실 컬렉터야
    - 비주얼스튜디오 돌리면 알아차리지 못하게 돌려주는거야
    - 디버깅도 마찬가지 아래 돌아가는거 모르게
    - 그누 디버거는 GDB
    - 클라우드 리눅스 유닉스 서버잖아요? 쥐디비 쓰셔야되요, 그래픽디버거 안된다.
    - gdb를 눌러 실행, 나갈때는 bye quit exit 셋중에 하나임.
    - 이런것까지 기억 못함. 다만 셋중에 하나임.
    - 브레이크 포인트 
> gdb 사용하기
- 
```s
$ gcc 06.option-g.c -o 06r
$ gcc -g 06.option-g.c -o 06g
```
  - 쥐디비 커맨드를 몰라서 안하는거야 커맨드에서는 
  - 커맨드라인 gdb 도 있고, 그래픽모드 gdb가 있다. 커맨드라인에서 써야 쓸수있지
  - 
  ```s
  gdb 06r
  (gdb) list
  ```
> 5번, 컴파일타임에 디파인을 정할수 있다
```
sdfsdf
```
- 디파인없어서 에러나는거 보여줌
```s
$ gcc -DNO=1000 05.option-D.c 
$ ./a.out 
Main End.
```
- 컴파일타임에 no랑 bebug 둘다 선언해줌
```s
$ gcc -DNO=1000 -DDEBUG 05.option-D.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ./a.out 
lv1:1, lv2:1000
Main End.

```

> 4번 c옵션으로 링킹에러 검출
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc -c 04-1.link-main.c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc -c 04-2.link-func.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ls 04-*
04-1.link-main.c  04-1.link-main.o  04-2.link-func.c  04-2.link-func.o
```
- 링킹과정으로 컴파일해보면 라이브러리 문제인지 아닌지 확인
```
```
- 라이브러리 만드는거 너무 쉬운거야 오브젝트의 집합이다! 안해봐서 어려운거임
- gcc는 링커에게 전달, 링커를 직접 쓰는것보다 링커를 직접 쓰면 니들이 직접 나열해야되
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc -c 04-1.link-main.c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc -c 04-2.link-func.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ls 04-*
04-1.link-main.c  04-1.link-main.o  04-2.link-func.c  04-2.link-func.o
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ^C
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ^C
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 04-1.link-main.o 04-2.link-func.o 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 04-1.link-main.o 04-2.link-func.o printf.o
gcc: error: printf.o: No such file or directory
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 04-1.link-main.o 04-2.link-func.o
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ./a.out 
Main Start...
a:10, a2:20, b:0, b2:0, c:100, c2:32767
a:10, a2:20, b:11, b2:19, c:100, c2:101
```

> 7번 예제, 변수를 잔뜩 선언해놓고 안쓰면 나오는것들?
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ./a.out 
Main Start..
Main End...
```
- 내용을 보면 안쓰는거 많죠???
```s
$ cat 07.option-Wall.c 
```
```cpp
#include <stdio.h>

int gv1 = 10, gv2;

int main(void)  
{
    int lv1, lv2, lv3=30;
    const int lv4=10;
    short *p;

    printf("Main Start..\n");
    lv1 = 10;
    printf("Main End...\n");

    return 0;
}

```
- 이걸 찾는법
```s
$ gcc -Wall 07.option-Wall.c 
```
- Wall 옵션을 켜서 보면 보인단다.
```s
07.option-Wall.c: In function ‘main’:
07.option-Wall.c:9:12: warning: unused variable ‘p’ [-Wunused-variable]
     short *p;
            ^
07.option-Wall.c:8:15: warning: unused variable ‘lv4’ [-Wunused-variable]
     const int lv4=10;
               ^~~
07.option-Wall.c:7:19: warning: unused variable ‘lv3’ [-Wunused-variable]
     int lv1, lv2, lv3=30;
                   ^~~
07.option-Wall.c:7:14: warning: unused variable ‘lv2’ [-Wunused-variable]
     int lv1, lv2, lv3=30;
              ^~~
07.option-Wall.c:7:9: warning: variable ‘lv1’ set but not used [-Wunused-but-set-variable]
     int lv1, lv2, lv3=30;
         ^~~
```
- 안쓴거 많으면 씨피유 실행이 느려진단다.
- 디버깅시에는 최적화하면 안되지만, 릴리즈모드 할때는 하면 안된단다.
- 오픈소느는 릴리즈, 디버깅할떄 잗
- 알고리즘 최적화 하려면 최적화의 원리를 이해 해야된단다. 

> 다른 강좌 홍보하면서 : 최적화
- 옵티마이즈 레벨 다르게, 실행속도, 바이너리 사이즈 달라진다!!!
```
   gcc -o0 03.option-c.c -o 03_0
   gcc -o1 03.option-c.c -o 03_1
   gcc -o2 03.option-c.c -o 03_2
   gcc -o3 03.option-c.c -o 03_3
```
- 사이즈 비교해야되는데 너무 작아서 안보인다.
```s
$ ls -al | grep 03_
-rwxrwxr-x 1 dhkim dhkim  8520  8월 10 11:30 03_0
-rwxrwxr-x 1 dhkim dhkim  8520  8월 10 11:30 03_1
-rwxrwxr-x 1 dhkim dhkim  8520  8월 10 11:30 03_2
-rwxrwxr-x 1 dhkim dhkim  8520  8월 10 11:30 03_3
```

> 06번, 
- 컴파일하는데
```s
$ gcc 08.option-l.c -o 08
```
- 쓰레드 함수 쓰는데 라이브러리 포함이 안되어있으면
```s
/tmp/cc3xSI3H.o: In function `main':
08.option-l.c:(.text+0x8f): undefined reference to `pthread_create'
collect2: error: ld returned 1 exit status
```

> 08 번 
- 전체
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.c -o 08
/tmp/cc3xSI3H.o: In function `main':
08.option-l.c:(.text+0x8f): undefined reference to `pthread_create'
collect2: error: ld returned 1 exit status
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.c -c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ll 08.option-l.
ls: cannot access '08.option-l.': No such file or directory
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ll | grep 08.option-l.
-rw-rw-r-- 1 dhkim dhkim   604  8월 10 10:22 08.option-l.c
-rw-rw-r-- 1 dhkim dhkim  2304  8월 10 11:35 08.option-l.o
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ rm 08.option-l.o 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ rm a.out 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ls
00.option-o.c  01.option-E.i  03_2              04-2.link-func.c  06r               prepros.txt
00.option-o.i  01.option-E.s  03_3              04-2.link-func.o  07.option-Wall.c  test
00.option-o.o  02.option-S.c  03.option-c.c     05.option-D.c     08.option-l.c
00.option-o.s  03_0           04-1.link-main.c  06g               09.option-I.c
01.option-E.c  03_1           04-1.link-main.o  06.option-g.c     myInclude
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.c -c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ls
00.option-o.c  01.option-E.i  03_2              04-2.link-func.c  06r               myInclude
00.option-o.i  01.option-E.s  03_3              04-2.link-func.o  07.option-Wall.c  prepros.txt
00.option-o.o  02.option-S.c  03.option-c.c     05.option-D.c     08.option-l.c     test
00.option-o.s  03_0           04-1.link-main.c  06g               08.option-l.o
01.option-E.c  03_1           04-1.link-main.o  06.option-g.c     09.option-I.c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ ll | grep 08.option-l.
-rw-rw-r-- 1 dhkim dhkim   604  8월 10 10:22 08.option-l.c
-rw-rw-r-- 1 dhkim dhkim  2304  8월 10 11:36 08.option-l.o
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.o
08.option-l.o: In function `main':
08.option-l.c:(.text+0x8f): undefined reference to `pthread_create'
collect2: error: ld returned 1 exit status
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.o -lpthread
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ gcc 08.option-l.o -l pthread

```
- 사실 표준라이브러리는 여기에 있단다.
```s
$ find ./ -name "stdio.h"
./include/c++/7/tr1/stdio.h
./include/stdio.h
./include/x86_64-linux-gnu/bits/stdio.h


$ find ./ -name "iostream"
./include/c++/7/iostream

```
- c표준도 gnu 표준 다르고 다른거 또 다르다

> 9번 
```s
$ gcc -I ./myInclude/ 09.option-I.c 
```
  - 
> v옵션 : 버벌스 수다스럽게 이것저것 다 말해준다
```s
$ gcc -v --save-temps 00.option-o.c 
```
- 나오면 결과물
```s
Using built-in specs.
COLLECT_GCC=gcc
COLLECT_LTO_WRAPPER=/usr/lib/gcc/x86_64-linux-gnu/7/lto-wrapper
OFFLOAD_TARGET_NAMES=nvptx-none
OFFLOAD_TARGET_DEFAULT=1
Target: x86_64-linux-gnu
Configured with: ../src/configure -v --with-pkgversion='Ubuntu 7.5.0-3ubuntu1~18.04' --with-bugurl=file:///usr/share/doc/gcc-7/README.Bugs --enable-languages=c,ada,c++,go,brig,d,fortran,objc,obj-c++ --prefix=/usr --with-gcc-major-version-only --program-suffix=-7 --program-prefix=x86_64-linux-gnu- --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --libdir=/usr/lib --enable-nls --enable-bootstrap --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --with-default-libstdcxx-abi=new --enable-gnu-unique-object --disable-vtable-verify --enable-libmpx --enable-plugin --enable-default-pie --with-system-zlib --with-target-system-zlib --enable-objc-gc=auto --enable-multiarch --disable-werror --with-arch-32=i686 --with-abi=m64 --with-multilib-list=m32,m64,mx32 --enable-multilib --with-tune=generic --enable-offload-targets=nvptx-none --without-cuda-driver --enable-checking=release --build=x86_64-linux-gnu --host=x86_64-linux-gnu --target=x86_64-linux-gnu
Thread model: posix
gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04) 
COLLECT_GCC_OPTIONS='-v' '-save-temps' '-mtune=generic' '-march=x86-64'
 /usr/lib/gcc/x86_64-linux-gnu/7/cc1 -E -quiet -v -imultiarch x86_64-linux-gnu 00.option-o.c -mtune=generic -march=x86-64 -fpch-preprocess -fstack-protector-strong -Wformat -Wformat-security -o 00.option-o.i
ignoring nonexistent directory "/usr/local/include/x86_64-linux-gnu"
ignoring nonexistent directory "/usr/lib/gcc/x86_64-linux-gnu/7/../../../../x86_64-linux-gnu/include"
#include "..." search starts here:
#include <...> search starts here:
 /usr/lib/gcc/x86_64-linux-gnu/7/include
 /usr/local/include
 /usr/lib/gcc/x86_64-linux-gnu/7/include-fixed
 /usr/include/x86_64-linux-gnu
 /usr/include
End of search list.
COLLECT_GCC_OPTIONS='-v' '-save-temps' '-mtune=generic' '-march=x86-64'
 /usr/lib/gcc/x86_64-linux-gnu/7/cc1 -fpreprocessed 00.option-o.i -quiet -dumpbase 00.option-o.c -mtune=generic -march=x86-64 -auxbase 00.option-o -version -fstack-protector-strong -Wformat -Wformat-security -o 00.option-o.s
GNU C11 (Ubuntu 7.5.0-3ubuntu1~18.04) version 7.5.0 (x86_64-linux-gnu)
	compiled by GNU C version 7.5.0, GMP version 6.1.2, MPFR version 4.0.1, MPC version 1.1.0, isl version isl-0.19-GMP

GGC heuristics: --param ggc-min-expand=100 --param ggc-min-heapsize=131072
GNU C11 (Ubuntu 7.5.0-3ubuntu1~18.04) version 7.5.0 (x86_64-linux-gnu)
	compiled by GNU C version 7.5.0, GMP version 6.1.2, MPFR version 4.0.1, MPC version 1.1.0, isl version isl-0.19-GMP

GGC heuristics: --param ggc-min-expand=100 --param ggc-min-heapsize=131072
Compiler executable checksum: b62ed4a2880cd4159476ea8293b72fa8
COLLECT_GCC_OPTIONS='-v' '-save-temps' '-mtune=generic' '-march=x86-64'
 as -v --64 -o 00.option-o.o 00.option-o.s
GNU assembler version 2.30 (x86_64-linux-gnu) using BFD version (GNU Binutils for Ubuntu) 2.30
COMPILER_PATH=/usr/lib/gcc/x86_64-linux-gnu/7/:/usr/lib/gcc/x86_64-linux-gnu/7/:/usr/lib/gcc/x86_64-linux-gnu/:/usr/lib/gcc/x86_64-linux-gnu/7/:/usr/lib/gcc/x86_64-linux-gnu/
LIBRARY_PATH=/usr/lib/gcc/x86_64-linux-gnu/7/:/usr/lib/gcc/x86_64-linux-gnu/7/../../../x86_64-linux-gnu/:/usr/lib/gcc/x86_64-linux-gnu/7/../../../../lib/:/lib/x86_64-linux-gnu/:/lib/../lib/:/usr/lib/x86_64-linux-gnu/:/usr/lib/../lib/:/usr/lib/gcc/x86_64-linux-gnu/7/../../../:/lib/:/usr/lib/
COLLECT_GCC_OPTIONS='-v' '-save-temps' '-mtune=generic' '-march=x86-64'
 /usr/lib/gcc/x86_64-linux-gnu/7/collect2 -plugin /usr/lib/gcc/x86_64-linux-gnu/7/liblto_plugin.so -plugin-opt=/usr/lib/gcc/x86_64-linux-gnu/7/lto-wrapper -plugin-opt=-fresolution=00.option-o.res -plugin-opt=-pass-through=-lgcc -plugin-opt=-pass-through=-lgcc_s -plugin-opt=-pass-through=-lc -plugin-opt=-pass-through=-lgcc -plugin-opt=-pass-through=-lgcc_s --build-id --eh-frame-hdr -m elf_x86_64 --hash-style=gnu --as-needed -dynamic-linker /lib64/ld-linux-x86-64.so.2 -pie -z now -z relro /usr/lib/gcc/x86_64-linux-gnu/7/../../../x86_64-linux-gnu/Scrt1.o /usr/lib/gcc/x86_64-linux-gnu/7/../../../x86_64-linux-gnu/crti.o /usr/lib/gcc/x86_64-linux-gnu/7/crtbeginS.o -L/usr/lib/gcc/x86_64-linux-gnu/7 -L/usr/lib/gcc/x86_64-linux-gnu/7/../../../x86_64-linux-gnu -L/usr/lib/gcc/x86_64-linux-gnu/7/../../../../lib -L/lib/x86_64-linux-gnu -L/lib/../lib -L/usr/lib/x86_64-linux-gnu -L/usr/lib/../lib -L/usr/lib/gcc/x86_64-linux-gnu/7/../../.. 00.option-o.o -lgcc --push-state --as-needed -lgcc_s --pop-state -lc -lgcc --push-state --as-needed -lgcc_s --pop-state /usr/lib/gcc/x86_64-linux-gnu/7/crtendS.o /usr/lib/gcc/x86_64-linux-gnu/7/../../../x86_64-linux-gnu/crtn.o
COLLECT_GCC_OPTIONS='-v' '-save-temps' '-mtune=generic' '-march=x86-64'
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch01/2.optionTest$ 
```


# 2장 Make
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02$ cd 2.make_gen/
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ ls
a.h  b.h  c.h  exam2.c  exam3.c  Makefile  task1.c  task2.c  task3.c  test1.c  test2.c  test3.c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ code .
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -c test1.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -c test2.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -c t
task1.c  task2.c  task3.c  test1.c  test1.o  test2.c  test2.o  test3.c  
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -c test3.c 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -c a.h 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ ls
a.h      b.h  exam2.c  Makefile  task2.c  test1.c  test2.c  test3.c
a.h.gch  c.h  exam3.c  task1.c   task3.c  test1.o  test2.o  test3.o
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -o test test1.o test2.o test3.
test3.c  test3.o  
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ gcc -o test test1.o test2.o test3.o 
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ ./test 
test1(11)
test2(22)
test3(33)
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch02/2.make_gen$ 
```
- 수작업 컴파일.. 젠장
- c코드 하나 수정하려면 오지게 많은거 해야되지만...
- make사용하면 알아서 다 자동으로됨
- 이외에도 다른기능들
  - .c파일이 변경되면 변경된것만 알아서
  - .h파일이 변경되면 변경된부분만 알아서 
  - 비주얼수튜디오도 사실 내부에 메이크가 돌고있던거지
- make도구의 룰을 이해 해야되요
  - 수정이 되었는지 아닌지는 모디파이 타임을 보고 알수있다
  - 그래서 터치 명령어로 시간만 바꾸고 테스트를 할 수 있다.
- 이런것들을 하기 위해서는 Makefile을 만들어야해, 이거 작성기법을 아는게 핵심이다.
- 리눅스랑 윈도우랑 다르다, EOF가 다르고 개행이 다름: 캐리지리턴, 뉴라인, 엔드오브파일
```s
$ rm *.o

$ rm test

$ make
gcc -c test1.c
gcc -c test2.c
gcc -c test3.c
gcc -o test test1.o test2.o test3.o

#존나중요한거 탭으로 개행해야 된단다!

```

- 메이크파일 
- Makefile이랑 makefile (맨앞 대소문자 구별) -> 둘다 존재할시
  - 윈도우는 두개 구별못해
  - 순서는 Gnu->make->Make 이다.
  - 하지만, 두개 같이 쓰지 마라, 될수있음 한가지만 써라
- 메이크에서의 타겟 
  - 이름을 안주면 첫번째 타겟이 작동한다는거
  - 타겟 이름을 지정하면 특정파일만 컴파일
- 메이크파일에서 - 옵션을 주면 에러나도 아래로 실행됨
  - 
> 유틸리티 설치하자
```s
$ sudo apt install xutils-dev 
```

- 디펜던시 있는거 정보를 찾아주면 Makedep
```s
cat Makefile
test : test1.o test2.o test3.o #선결조건, 프리 리콰이어먼트, 디펜던시
	make dep
	gcc -o test test1.o test2.o test3.o
	#존나중요한거 탭으로 개행해야 된단다!

test1.o : test1.c a.h b.h# 디펜던시 다 넣어줘라
	gcc -c test1.c

test2.o : test2.c a.h b.h# 디펜던시 다 넣어줘라
	gcc -c test2.c

test3.o : test3.c a.h b.h# 디펜던시 다 넣어줘라
	gcc -c test3.c

clean: #dummy traget, phony target : 의존성 디펜던시가 없는 타겟
	-rm test1.o test2.o test3.o
	-rm test

dep:
	gccmakedep test1.c test2.c test3.c
# DO NOT DELETE
test1.o: test1.c /usr/include/stdc-predef.h a.h /usr/include/stdio.h \
 /usr/include/x86_64-linux-gnu/bits/libc-header-start.h \
 /usr/include/features.h /usr/include/x86_64-linux-gnu/sys/cdefs.h \
 ...................................
 /usr/include/string.h \
 /usr/include/x86_64-linux-gnu/bits/types/locale_t.h \
 /usr/include/x86_64-linux-gnu/bits/types/__locale_t.h \
 /usr/include/strings.h b.h
test2.o: test2.c /usr/include/stdc-predef.h a.h /usr/include/stdio.h \
 /usr/include/x86_64-linux-gnu/bits/libc-header-start.h \
 /usr/include/features.h /usr/include/x86_64-linux-gnu/sys/cdefs.h \
 /usr/include/x86_64-linux-gnu/bits/wordsize.h \
 /usr/include/x86_64-linux-gnu/bits/long-double.h \
 .................................
 /usr/include/string.h \
 /usr/include/x86_64-linux-gnu/bits/types/locale_t.h \
 /usr/include/x86_64-linux-gnu/bits/types/__locale_t.h \
 /usr/include/strings.h c.h
test3.o: test3.c /usr/include/stdc-predef.h a.h /usr/include/stdio.h \
 /usr/include/x86_64-linux-gnu/bits/libc-header-start.h \
 /usr/include/features.h /usr/include/x86_64-linux-gnu/sys/cdefs.h \
 /usr/include/x86_64-linux-gnu/bits/wordsize.h \
 /usr/include/x86_64-linux-gnu/bits/long-double.h \
 .......................................
 /usr/include/x86_64-linux-gnu/bits/sysmacros.h \
 /usr/include/x86_64-linux-gnu/bits/pthreadtypes.h \
 /usr/include/x86_64-linux-gnu/bits/thread-shared-types.h \
 /usr/include/x86_64-linux-gnu/bits/pthreadtypes-arch.h \
 /usr/include/alloca.h /usr/include/x86_64-linux-gnu/bits/stdlib-float.h \
 /usr/include/string.h \
 /usr/include/x86_64-linux-gnu/bits/types/locale_t.h \
 /usr/include/x86_64-linux-gnu/bits/types/__locale_t.h \
 /usr/include/strings.h b.h c.h
```
- 디펜던시라는건 내 어플리케이션이 빌드되기 위해서 필요한 조건들, 뭔가를 디펜던시에 있는것들을 

> 쉐환경변수
- echo $PATH
- printenv, env
- echo {$PATH} : 변수명을 표기할때

> 프리디파인 플래그 인터널 플래그 차이
```s
$ cat Makefile
OBJS := test1.o test2.o test3.o 
CC := gcc
CFLAGS := -g -Wall -O2 -DNO


test : $(OBJS)
	$(CC) -o test $(OBJS)
	#존나중요한거 탭으로 개행해야 된단다!

test1.o : test1.c # 디펜던시 다 넣어줘라
	$(CC) $(CFLAGS) -c test1.c

test2.o : test2.c # 디펜던시 다 넣어줘라
	$(CC) $(CFLAGS) -c test2.c

test3.o : test3.c # 디펜던시 다 넣어줘라
	$(CC) $(CFLAGS) -c test3.c

clean: #dummy traget, phony target : 의존성 디펜던시가 없는 타겟
	-rm test1.o test2.o test3.o
	-rm test
```
- 플래그  , CFLAGS, LDFLAGS, 
- 네이티브 컴파일, 크로스컴파일 쓰는거 차이는 
- LDFLAGS := -lpthreadd


> 라이브러리
- $ gcc -c task1.c 
```s
$ nm task1.o
                 U atoi
0000000000000000 D data
0000000000000020 T f1
0000000000000000 T f2
                 U _GLOBAL_OFFSET_TABLE_
0000000000000044 T main
                 U printf
                 U sleep
```
- nm 유틸리티를 쓰면은 ELF 파일속 들어있는 정보를 출력함, 이게 심볼테이블이라고 한다.
- gcc @@.c
- nm a.out
  - 링크는 스타트업코드, 라이브러리 등등 다 연결해줌, 주소맵핑도 해줌
  - 주소를 맵핑해주는게 링커다
  ```
    0000000000000820 R _IO_stdin_used
                    w _ITM_deregisterTMCloneTable
                    w _ITM_registerTMCloneTable
    0000000000000810 T __libc_csu_fini
    00000000000007a0 T __libc_csu_init
                    U __libc_start_main@@GLIBC_2.2.5
    000000000000071e T main
                    U printf@@GLIBC_2.2.5
    0000000000000640 t register_tm_clones
                    U sleep@@GLIBC_2.2.5
    00000000000005d0 T _start
    0000000000201018 D __TMC_END__

  ```
  - 여기서 주소가 없으면 다이나믹 링킹, 주소가 없고 컴파일타임에 실행시 정보를 연결함,
  - 포함은 안되지만, 실행할때 가져오면 
  - 실행할떄 언제든지 정보를 끌고올수 있도록... 다이나믹 링킹이 디폴트임

- 스테틱과 다이나믹 링킹
  - 스테틱 링킹 : 그냥 떄려박아 사이즈 무쟈게 커짐. -> 메모리 엄청나게 퍼먹음
  - 다이니믹 링킹 확인 : ldd a.out
- 스태틱 링킹 : $ gcc task1.o -static -o a.st
```s
$ ls -l a.*
-rwxrwxr-x 1 dhkim dhkim   8464  8월 10 16:49 a.out
-rwxrwxr-x 1 dhkim dhkim 845000  8월 10 17:00 a.st
```
- 스테틱 링킹 함부러 하면 
- 다이내믹 링킹 하면 절대 안되는 경우 임베디드
  - 크로스컴파일러 설치해서 빌드하면->다이나믹 링킹
  - 타겟에서 돌려면 스태틱 링킹 해야된다..
  - 펌웨어나 RTOS는 무적권 스테틱으로 해야된다.
- 리눅스에서 작업하려면 다해야되는데.. 
  - 다이나믹 링킹 라이브러리
  - 스태틱 링킹 라이브러리
- ELF 임베디드 빼줘야한다?? 무슨말?
  -
- 다이나믹 링킹과 스태틱 링킹 하는거는 링커스크립트에서 하는건가??

> 
```s
$ gcc app.c 
app.c:4:10: fatal error: testlib.h: No such file or directory
 #include "testlib.h"
          ^~~~~~~~~~~
compilation terminated.
```
- 위 인클루드 없는 문제 해결
```s
$ gcc app.c 
app.c:4:10: fatal error: testlib.h: No such file or directory
 #include "testlib.h"
          ^~~~~~~~~~~
compilation terminated.

```
- I 옵션으로 

- :/usr/lib/x86_64-linux-gnu 경로에서
```
$ nm libc.a
```
- 찾아보기 $ nm libc.a | grep printf
```
$ ar -t libc.a
```

- ar 명령어로 공유라이브러리 
$ ar -t libtest.a 
max.o
min.o


> 복습
- 환경변수 보는법 env printenv
- 환경변수 중 LD_LIBRARY_PATH 라는 환경변수가 있는데
- PATH 라는 환경변수는 실행파일이 존재하는 위치
- 쉘의 변수는 데이터타입이 오로직 스트링, 스트링으로 값을 주고받을수뿐이 없다
- 구분자는 콜론 : 이걸로 스트링과 스트링 사이에 구분을 해주는 구분자임
- 로케이터나 링크 스크립트에게 환경 변수 알려줌
```
$ LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/dhkim/Desktop/Li_Opbuild/lou/ch03/1.libTest1_st
```
- 항상 써야한다면 배쉬알씨에다가 이 내용을 집어넣어놔라
- 리눅스를 잘 쓰시려면 쉘의 기본하고 쉘 스크립트 쉘 프로그래밍 이건 기본이야 기본!!!!!
> etc아래 설정파일로 넣어논는게 있어요(슈퍼유저 권한 필요)
- 모든사용자가 거의 쓰는 라이브러리라면 슈퍼유저권한자에게 등록을 하는게 좋다.
- $ sudo gedit /etc/ld.so.conf 
  - 여기다가 쉐어드 라이브러리의 경로를 추가하면 된다!
> 다이나믹 링킹
- 실행시점에 다이나믹 링킹을 
- 링킹타임(빌드타임에 링킹)
  - 다이나믹 링킹, 쉐어드 라이브러리의 정보를, a.out에 안넣고 런타임에 로딩하는 기법, 실행시점에 쉐어드 라이브러리를 로딩하는 기법
  - 링킹도 안하고 런타임에 링킹하는 기법이 있다( 빌드타임 링킹)
  - 결국 두가지 런타임링킹/빌드타임 링킹
  - 런타임링킹은 a.out 
- 실행시점에 로딩하는게 아니고 ?? -> 다이나믹 로딩을 해주는 특수 라이브러리라 필요하다, 제품을 만들떄 아주 중요함

> 제품 만들떄 아주 중요한
- 런타임에 쉐어드 라이브러리를 오픈해주는거임
- /home/dhkim/Desktop/Li_Opbuild/lou/ch03/1.libTest1_st/libDynamic
```cpp
//dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch03/1.libTest1_st/libDynamic$ cat dltest.c 
/* dltest.c */

#include <stdio.h>
#include <stdlib.h>
#include <dlfcn.h>


typedef int (*FP)(int, int);

int main(void)
{
    void *handle;
	FP fp_max, fp_min;
    char *error;

    handle = dlopen("libtest.so", RTLD_LAZY);
    if(!handle) {
        fputs(dlerror(), stderr);
        exit(1);
    }
    fp_max = dlsym(handle, "max");
    if((error = dlerror()) != NULL) {
        fprintf(stderr, "%s", error);
        exit(1);
    }
    fp_min = dlsym(handle, "min");
    if((error = dlerror()) != NULL) {
        fprintf(stderr, "%s", error);
        exit(1);
    }
    printf("max(7, 4) : %d\n", fp_max(7, 4));
    printf("min(5, 2) : %d\n", fp_min(5, 2));
    dlclose(handle);

    return 0;
}
```
- 그냥 컴파일하면 
- $ gcc dltest.c
```
/tmp/ccOZR2iw.o: In function `main':
dltest.c:(.text+0x16): undefined reference to `dlopen'
dltest.c:(.text+0x2d): undefined reference to `dlerror'
dltest.c:(.text+0x55): undefined reference to `dlsym'
dltest.c:(.text+0x5e): undefined reference to `dlerror'
dltest.c:(.text+0x9c): undefined reference to `dlsym'
dltest.c:(.text+0xa5): undefined reference to `dlerror'
dltest.c:(.text+0x122): undefined reference to `dlclose'
collect2: error: ld returned 1 exit status
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch03/1.libTest1_st/libDynamic$ gcc dltest.c -c
```
- 에러 뜨니까 gcc -c 로 캄파일 옵션 줘야함
- 그러면 그냥 오브젝트 파일만 떠서 실행이 안되지나ㅏ??
- 실행파일 만들기 위해서는 
  - gcc dltest.c -ldl
- ld 라이브러리 패스에 넣던가
- 풀패스를 넣던가
- etc 아래에 넣던가
- 협업할때 중요, 라이브러리는 다른데서 만들고 어플은 여기서만들고, 라이브러리는 다른사람 다른회사
- 디바이스 제어하는 라이브러리/ 네트워크 프로토콜 제어 라이브러리/ 장비벤더 등은 
  - 같이 링킹해서 만들거나 디바이스 드라이버 라이브러리는 한다던가 하면 
> 다이나믹 링킹(so) 파일 사용을 위해서는
  - etc/so.conf 어쩌고에 경로 등록
  - 쉘에다가 LD_LIBRARY_PATH
> 강사님 약력소개
  - 모바일 프레임워크 , 모바일 OS, 우리삼성 엘지 안드로이드프레임웍 할 OS 등등..
  - 프레임워크 섭렵을 다 하면 이 기능을 무지무지하게 중요함
  - 라이브러리 모르면 이건 개죽음이다.
  - 프레임워크 모르면 기능을 넣을수 없다.
  - 지금 배우시는이게 괭장히 중요해요 
  - 리눅스를 잘하면 안드로이드 라즈베리 잘해요
  - 그런경우에 IOT 웹캠 라즈베리 기반 연동한다거나 오픈소스가 갱장히 많아요.
  - 여러분이 필요한거 조금 수정해서 그냥 쓰면 되는데, 지금 이걸 알면 바로 쓸수 있다는 말이죠. 라이브러리 이해해야되요
  - 빌드는 make, cmake 이해해야되요
  - 오픈되어있는 소스 가져다가 바로 이해하면 되는거에요
  - 빌드시스템이 진짜 중요해요
  - 라이브러리 제어 : 
  - 안드로이드 개복잡해요
  - 프레임웍은 C++
  - 할은 c단
  - 자바 어플리케이션은 가상머신,
  - 무지무지하게 복잡한 하이라키를 가지고ㅓ있는게 안드로이드야
  - 안드로이드 빌드시스템을 쓰지않으면 어려워, 안드로이 빌드시스템은 결국 메이크, 전체빌드는 결국 메이크에여
  - 엔드유저단 어플 만드는사람은 시스템을 모른다
    - 사실 그런건 아니야, 자바단 어플은 자바만, 시스템에 들어오려면 시스템 여결 내부는 결국 make로 되어있다
    - 결론은 make가 중요하다
  - 안드로이드 미들웨어 HAL 이런거
  - 진짜 하드웨어 움직이려면 c로 가야함. 동영상 그런건 결국 하드웨어 자바단은 결국 껍데기이다.
  - 프레임워크나 이런코드들은 결국 C++이나 C임 실제 시스템은 저 두개가 없음 안돌아간다
  - 시스템을 만들려면 어플단만 가지고는 만들 수 없다.
  - 링킹이 두가지 스택 다이나믹
    - 스태틱 라이브러리
    - 다이나믹 링킹 쉐어드 라이브러리 
      - 로딩시점 두가지
        - 스타틱 로딩 : a.out에 들어가있어서 링킹타임에 링크되어있어야
        - 런타임 로딩 : 링크를 하지않고 로딩 이게 개중요@@@@@@@@@
          - 협업할떄 중요 -> 안드로이드도 이거 씀
        - 언어가 제공하는 라이브러리만 쓰지않음. 이런 라이브러리를 거대하게 만들려면 하나의 기업이 하는거고 그것도 so파일등으로 제공되고
        - 링크타임에 so를 포함할수없기도 하고, 런타임에 
        - 자바에서 출발할수 있다. 메모리쪽에 올린다거나 하는 것들은 커널레이어의 c레벨에서 출발한다. 
        - 상위레이어를 쓰더라도 커널이 핵심이고, 커널직접대화는 c레벨, C++도 일부 가능
        - c/c++ 같이 쓰려면 걸림돌 네이밍컨벤션 어쩌고가 중요하다

## 챕터3 2번, 라이브러리를 make로 만들어보세요
  - 메이크파일을 수정해서 채워주세요
  - 써먹어 봐야 본인꼐 된다
  - 라이브러리 확장자(규칙)
    - 윈도은 DLL
    - 리눅스 동적은 .so / 정적은 .a
    - 안드로이드도 정책은 리눅스와 같기때문에 커널이 뭔지가 개 중요하다

## 챕터3 1번인가? appSRC 를 수정해서 만들어주세요
  - 골뱅이가 뭔가..@는 뿌지리자마라
  - make 스크립트에서 소괄호 중괄호 차이 - CC에서
  - 씨발 개어렵네

# 4장 Cmake
  - 검색해라

# 5장 make의 고급기법
  - 
  ```s
  CC = gcc
  CFLAGS := -O2 -Wall -g
  SRCS = test1.c test2.c test3.c
  OBJS = $(SRCS:.c=.o)
  LIB_OUT = libtest.a
  APP_OBJ = task1.o task2.o
  APP_OUT = $(APP_OBJ:.o=)

  test: $(LIB_OUT) $(APP_OUT)

  $(LIB_OUT) : lib/min.o lib/max.o
      $(AR) $(ARFLAGS) -o $@ $^

  ..............
  task1 : task1.o
      $(CC) $(LDFLAGS) -o $@ $<

  ..............
  task2 : task2.o
      $(CC) $(LDFLAGS) -o $@ $<

  ...... : CFLAGS = -fPIC -O2 -Wall -g

  clean:
      -rm -f lib/*.o
      -rm $(APP_OUT) $(APP_OBJ) $(LIB_OUT) 
-  Type  :qa!  and press <Enter> to abandon all changes and exit Vim                  26,38-41      All

  ```
  - 타겟 스페시픽 빌드 하는거 고급make
  - 원래 c플래그는 이렇게 되어있음
  - 나는 lib 아래에 있는 , lib에 있는 모든쩜씨
  - 무슨말하는건지 모르겠다 열받네
  ```
  CC = gcc
  CFLAGS := -O2 -Wall -g
  SRCS = test1.c test2.c test3.c
  OBJS = $(SRCS:.c=.o)
  LIB_OUT = libtest.a
  APP_OBJ = task1.o task2.o
  APP_OUT = $(APP_OBJ:.o=)

  test: $(LIB_OUT) $(APP_OUT)

  $(LIB_OUT) : lib/min.o lib/max.o
    $(AR) $(ARFLAGS) -o $@ $^

  tast1 : LDFLAGS := -static
  task1 : task1.o
    $(CC) $(LDFLAGS) -o $@ $<


  tast2 : LDFLAGS := -static
  task2 : task2.o
    $(CC) $(LDFLAGS) -o $@ $<

  lib/%.o : CFLAGS = -fPIC -O2 -Wall -g

  clean:
    -rm -f lib/*.o
    -rm $(APP_OUT) $(APP_OBJ) $(LIB_OUT) 

  ``` 
  - 결국 말하고싶은거 두가지
    - 타겟 스페시픽 베리어블
    - 패턴 스페시픽 베리어블
> 링커는 ld : 
gcc 링킹해야되는 시점에 ld 불러주는거 G
gcc 는 콜렉터
디폴트로 포함되어야하는걸 다 지정해줘야하니까 복잡해
커널빌드 안드빌드는 ld를 직접 쓰는경우가 나와요

임베디드 링커스크립트 메모리
- 
> 강사님의 조언
- 링킹드가지
- 라이브러리
- 주소정리
- 임베디드는 주소까지 지정해야되는거
- 범용은 고정(어플단은 가장)
- 임베디드는 피지컬주소랑 매핑
- 링커스크립트에서 조정해야되요
- 임베디드 cmake가 훨씬 좋다, 우리가 make 만드는것보다 훨씬 잘만들어줘
- cmake만 배워도 될꺼같지만 문제가 발생
- 이런기능이 어떻게 도는지 모르니까 make 를 배워야 됨, 상호보완적이야
- 앞으로는 cmake 가 주로
- 기존에 레거시 호환을 위해서는 cmake 를 
- 자바도 네이티브를 같이 링크할때는 안드로이드 스튜디오 네이티브 같이 링크 라이브러리 cmake 같이 돌아요 요즘엔 씨메이크
- 오토컨프는 굳이 안써도 될꺼같은데 컨피규레이션, gcc make dep같은거 
- cmake 
- 거대 빌드시스템은 믹스해서 써요 어떤건
- 호환가능한 영역은 cmake 커널은 완전스페시픽 커널은 make
- cmake 한계, make와 cmake는 상호보완적
- menuconfig : 어플툴 굳이 gui로 안한다 하면, 커맨드라인에서 하는것도 있어요, 일반 사용자가 어려워하니까 그래픽툴, 컨피그레이션 해야 빌드하는거
- 빌드시스템 거대한다던가 관심있으신분들은
  - educ.or.kr : 국가인적자원컨소시엄 -> 무료교육 들어라
  - 최적화 한번 꼭 들으세요, 포인터와 최적화
  - c와 c++ 
  - 스마트 단말을 위한 임베디드 리눅스 시스템 구추과정 : os빌드 등..
    - 가상메모리 피지컬메모리 어떻게 매핑되는지, 직접 os 만들지 않으셔도, os잘알면 어플 잘만든다.
    - 넌블락킹 블락킹의 의미가 도대체 뭔건지, 쓰레드 프로세스 동기화처리 진짜 어떻게 되는건지 커널
    - 내 어플이 어떤상태의 제어를 받는건지

> 3번째 이그잼플 어싸인먼트 각종 차의의 설명
- /Li_Opbuild/lou/ch05/make_app_st/03.assignment
```s
#/ch05/make_app_st/03.assignment$ cat makefile 
CC = gcc
CFLAGS = -O2 -Wall -g
SRCS = test1.c test2.c
OBJS1 = $(SRCS:.c=.o)
OBJS2 := $(SRCS:.c=.o)
# 위 두가지가 틀리다.



SRCS += test3.c
OBJS = $(SRCS:.c=.o)

test: $(OBJS)
	$(CC) -o $@ $^

info:
	@echo "SRCS-->"
	@echo $(SRCS)
	@echo "OBJS-->"
	@echo $(OBJS)
	@echo "OBJS1-->"
	@echo $(OBJS1)
	@echo "OBJS2-->"
	@echo $(OBJS2)
clean:
	rm $(OBJS) test

dep:
	gccmakedep $(SRCS)

```
- 여기서 할일
 ```
 make info
 ```
- 단순하고 짧은거에서는 심플이콜과 리커시브 이콜이 같다. 하지만 큰거는 다르다.!!! 이거를 말하고자 함.

> 컨디셔널 이콜을 만들어보자(여기서 추가)
- 1단계 시작전
```s
libtest.a : lib/min.o lib/max.o
    ................
    ................

```
- 2단계 : 이렇게할수도있지만
```s
libtest.a : lib/min.o lib/max.o
    cd lib #make에서 이렇가 하면 안된다, 커맨드라인에서는 되는데, 
    #메이크돌리면 서브쉘 따로돌기때문에, 현제 쉘에서만 움직이고,
    #이 문제 해결을 위해서는 ;를 붙여줘야 한다
    cd ../
    cd lib; # 귀찮잖아? 유용한 매크로는 @D 매크로 쓰면
    $(AR) ${ARFLAGS} $@ $^

```
- 3단계 : 이렇게 하면 된다..
```s
libtest.a : lib/min.o lib/max.o
    cd $(<D); $(AR) ${ARFLAGS} -o $@ ${^F}
    mv ${<D}/$@ .
```
- 어디서 이 명령들이 실행되는지 중요하다


> 소스랑 오브젝트 같이 있으면 짜증나니까 오브젝트 파일 때려박는것
- @ : 커맨드 자체는 에코하지 말아라
- 
```s
```
- 완성본
```s
/lou/ch05/make_app_st/04.macro_DF_st$ cat makefile 
CC = gcc
CFLAGS = -O2 -Wall -g
LDFLAGS =

all : libtest.a test

libtest.a : lib/min.o lib/max.o
	cd $(<D); $(AR) ${ARFLAGS} -o $@ ${^F}
	mv ${<D}/$@ .것

test : test_objs
	@$(CC) $(LDFLAGS) -o $@ app/objs/*

test_objs : app/src/test1.o app/src/test2.o app/src/test3.o
	@cd $(<D); mkdir ../objs; mv $(^F) ../objs

lib/%.o : CFLAGS = -fPIC -O2 -Wall -g
	#패턴 스패시픽

clean:
	-rm -f lib/*.o
	-rm -f app/objs/*.o
	-rm  libtest.a test


```
- 
```s
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch05/make_app_st/04.macro_DF_st$ make
gcc -fPIC -O2 -Wall -g   -c -o lib/min.o lib/min.c
gcc -fPIC -O2 -Wall -g   -c -o lib/max.o lib/max.c
cd lib; ar rv -o libtest.a min.o max.o
ar: creating libtest.a
a - min.o
a - max.o
mv lib/libtest.a .것
gcc -O2 -Wall -g   -c -o app/src/test1.o app/src/test1.c
gcc -O2 -Wall -g   -c -o app/src/test2.o app/src/test2.c
gcc -O2 -Wall -g   -c -o app/src/test3.o app/src/test3.c
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch05/make_app_st/04.macro_DF_st$ ls
app  lib  makefile  test
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch05/make_app_st/04.macro_DF_st$ cd ../
01.macro_order/        03.assignment/         05.make_vpath/         07.recursive_make_st2/
02.target_specific_st/ 04.macro_DF_st/        06.make_dep_st/        make_include/
dhkim@dhkim-VXK:~/Desktop/Li_Opbuild/lou/ch05/make_app_st/04.macro_DF_st$ ls -R .
.:
app  lib  makefile  test

./app:
objs  src

./app/objs:
test1.o  test2.o  test3.o

./app/src:
a.h  b.h  c.h  test1.c  test2.c  test3.c

./lib:
max.c  max.o  min.c  min.o

```

> vfath 알아두면 유용해요
- $? : 
- $@ :
- $ make VPATH=./sub 한단계 아래 폴더 시점에서 make 돌리는 기법임
```s
```
- 
```s
```
- 
```s
```

# 오픈소스 돌리기
> bash쉘
 # 6번예제
 - 메이크파일이 없고 컨피겨

 ```s
 makefile : 
    @echo "Generate makefile..."
    @rm -f $@
    @cp Make.mk $@
    .............


 ```
 - 를 변경하기
 ```s
 makefile : 
	@echo "Generate makefile..."
	@rm -f $@
	@cp Make.mk $@
	$(CC) -M ${SRCS} >> $@

 ```
 - 여기서 결론은 메이크파일을 만드는 configure가 있단다
> 07번은 리커시브 메이크로 니들이 직접 해봐라
  - 거꾸로 채우는 바텀업이 더 좋다
  - libSrc에 있는걸 스태틱과 다이나믹 라이브러리로 
  - 바텀업으로 올라오면서 만들어보세요
  - 리커시브 메이크 내가 동작을 안하는데 완성형 파일을 좀 줄수 있니
> 전체메이크
  - 스테틱 라이브러리
    - VPATH 잡아놔서 쓸 수 있단다. VPATH 썻기때문에 가능한거란다
    - make 엔터치면 
    - APP static 
    - 챕터5-7 리커시브 메이크 
    - 스타틱 라이브러리부터 빌드하는거 하나 넣어야겠는걸?
    - 아 씨발 무슨 개소리인지 모르겠다ㅏㅏㅏㅏㅏㅏㅏㅏ
> cmake
- cmake 파일 지우는거 지울려면 노가다로 지웠거든요
- 쉘 스크립트로 진행한단다
```s
$ cat myrm.sh 
#!/bin/bash
rm CMakeCache.txt
rm cmake_install.cmake
rm Makefile
rm -rf CMakeFiles
```
- cmake 빌드 위치를 지정할 수 있다.
- 디렉토리 지정해서 빌드하는옵션 : cmake -H 홈 
- 이렇게 돌려라 : $ cmake -H. -Bbuild
```s
$ cmake -H. -Bbuild
```
> 메이크를 모르고 빌드하는법
```s
$ cmake --build .
```
- 아래 이걸 가지고 배우는거야, 빌드할수 있는 모든 타겟이 있음
```s
$ cmake --build . --target help
```
- 이
```s
$ cmake --build . --target clean
```


> 빌드타입
  - 빌드타입을 디버그나 릴리즈로도 할수 있고
  - 커맨드라인에서 

> 라이브러리도 CMAKE로 빌드할 수 있다
  ```s
  cmake CMakeLists.txt 
  cmake -H. -Bbuild
  cd build/
  cmake --build .
  ```
  - 라이브러리도 아주아주 쉽게 빌드할 수 있다 : /home/dhkim/Desktop/Li_Opbuild/lou/ch04/2.var_cmd/4.var_trg_add_lib_st/cmake/libs/build
  - cmake 갱장히 잘 설명하는원서 : 
  - 우리나라 일반 튜토리얼 자세한 설명 없어요
  > http://androidxref.com/
  - 씨텍 씨스콥 존나게 공부해라
  - 저 안드로이드 소스 디렉토리
  - 안드로이드 어플 
  ```
  Full Search	
  Definition	
  Symbol	
  File Path	
  History
  ```
  - 자동완성 RC파일에 추가해서 기능은 저변은 다 만들어져 있다 검색이든 뭐든 다 있다. 파일보완 씨스코프 씨택 파일 공통으로 바꿀수 있다 못할께 없다 !!!!!!!
  - 리눅스 어플리케이션의 배포
> 빌드옵션 08번 예제 Cmake
  - 아 순서 존나 뒤죽박죽하네 개가튼거
  - 경로 : /lou/ch04/2.var_cmd/8.build_option_st/cmake
  ```s
  set (LIB_PATH 
  set ()
  add_library()

  set (INC_PATH "./include")
  include_directories (${INC_PATH})
  
  link_libraries(mytest)
  set (LIB_PATH 
  set ()
  add_executable()
  ```
  ```s
  set(ELIB_PATH ${HOME})
  include_directories($)
  #내 홈디렉, 홈디렉의 환경변수를 끌어다 쓴다
  include_directories()
  link_directories(${ELIB_PATH}/lib)

  add executable(app_static ${APP_SRCS})
  add executable(app_shared ${APP_SRCS})

  target_link_libraries(app_static mytest -static)
  ```
  - cmake 문법이니까 기억
  - 대충 탬플릿 만들어놓고 가져다가 쓰세요
  - 아 씨발...

  >  $ /lou/ch05/cmake_app_st/03.add_custom_target_st/cmake/CMakeLists.txt 
    ```s
    ##
    ## CMakeLists.txt : for CMake Application Programming
    ##
    ##		Kim Soo Hyun(@")
    ##
    PROJECT ( "CMake - Add Custom Target" LANGUAGES C )
    CMAKE_MINIMUM_REQUIRED ( VERSION 3.10 )
    SET ( CMAKE_BUILD_TYPE Release )
    #SET ( CMAKE_BUILD_TYPE Debug )
    SET ( CMAKE_VERBOSE_MAKEFILE true )

    SET (SRCS test1.c test2.c test3.c)
    ADD_EXECUTABLE ( mytest ${SRCS} )
    MESSAGE ( ${CMAKE_PROJECT_NAME} )

    ................
    ```
  - 이씨발..
  - 
  ```
  add_custom_target(backup
    COMMENT "BACKUP...."
    COMMADN ""
    COMMADN ""
    )
  ```
> 0번 
```s
/lou/ch05/cmake_app_st/00.option_test_st$ ls
1.cmake-D  2.cmake-E  3.cmake-G

```
- D옵션 : 데피니션??말했다는데
- E옵션 : 
  - man cmake
  - cmake -E help
  - 쉘커맨드를 cmake로 매핑해놓은거다
- 개같은거 원리를 설명해라 이말이야
> 닌자
- $ sudo apt install ninja-build 
- 이건 웹이나 자바를 돌리는 건데요
```s
$ cmake -G help
CMake Error: Could not create named generator help

Generators
  Unix Makefiles               = Generates standard UNIX makefiles.
  Ninja                        = Generates build.ninja files.
  Watcom WMake                 = Generates Watcom WMake makefiles.
  CodeBlocks - Ninja           = Generates CodeBlocks project files.
  CodeBlocks - Unix Makefiles  = Generates CodeBlocks project files.
  CodeLite - Ninja             = Generates CodeLite project files.
  CodeLite - Unix Makefiles    = Generates CodeLite project files.
  Sublime Text 2 - Ninja       = Generates Sublime Text 2 project files.
  Sublime Text 2 - Unix Makefiles
                               = Generates Sublime Text 2 project files.
  Kate - Ninja                 = Generates Kate project files.
  Kate - Unix Makefiles        = Generates Kate project files.
  Eclipse CDT4 - Ninja         = Generates Eclipse CDT 4.0 project files.
  Eclipse CDT4 - Unix Makefiles= Generates Eclipse CDT 4.0 project files.
  KDevelop3                    = Generates KDevelop 3 project files.
  KDevelop3 - Unix Makefiles   = Generates KDevelop 3 project files.


```