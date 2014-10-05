# 安装并配置MPI开发环境

作者： 马超 mctt90@gmail.com

---

**1. 保证C/C++环境已经配置完毕** <br><br>
在ubuntu系统下可以使用如下命令
```bash
sudo apt-get install gcc
sudo apt-get install g++
```
<br>
**2. 在MPICH官网下载tar包**<br><br>
网址: http://www.mpich.org/downloads/

**3. 解压**<br><br>
解压并进入文件
```bash
tar xvf mpich-3.1.2.tar.gz
cd mpich-3.1.2
```
<br>
**4. 编译并安装**<br><br>

```bash
sudo ./configure --prefix=/home/alex/mpich --enable-cxx --enable-threads=multiple --enable-sharedlibs=gcc --with-mpe --disable-f77 --disable-f90 --disable-fortran
sudo make
sudo make install
```
<br>
**5. 设置MPI C/C++编译器环境变量**<br><br>

```bash
sudo vim /etc/profile
# 在文件中添加
export MPI_ROOT=/home/alex/mpich
export PATH=$MPI_ROOT/bin:$PATH
source /etc/profile
```
<br>
**6. 编写本地测试程序,以C++为例**<br><br>
创建mpitest.cpp文件

```c++
#include "mpi.h"
#include <iostream>

using namespace std;

int main(int argc, char **argv) {

    int myid, numprocs;
    int namelen;
    char processor_name[MPI_MAX_PROCESSOR_NAME];

    MPI_Init (&argc, &argv);
    MPI_Comm_rank (MPI_COMM_WORLD, &myid);
    MPI_Comm_size (MPI_COMM_WORLD, &numprocs);
    MPI_Get_processor_name (processor_name, &namelen);
    cout << "Hello world! Process " << myid << " of " <<  numprocs << " on " << processor_name;
    MPI_Finalize ();

    return 0;
}
```
<br>
编译并运行
```bash
mpicxx ./mpitest.cpp
mpirun -np 4 ./a.out
mpiexec -np 4 ./a.out
```
