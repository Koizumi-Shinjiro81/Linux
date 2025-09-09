@슬레이브 @사용자로 들어오기
cp -r /etc/skel/.bash_profile ~/.
cp -r /etc/skel/mvapich2.hosts ~/.
cp -r /etc/skel/openmpi.hosts ~/.
cp -r /usr/local/src/test_src/cpi.c ~/.

#### vi ~/.bash_profile @@ MPI Compiler 사용
source /usr/local/intel/oneapi/compiler/latest/env/vars.sh intel64     ## Intel Compiler v21
#source /usr/local/intel/oneapi/mpi/latest/env/vars.sh intel64          ## Intel MPI v21
#source /usr/local/intel/oneapi/mkl/latest/env/vars.sh intel64          ## Intel MKL v21
#export MPICH=/usr/local/mpi/intel21/mpich-4.1.2                         ## MPICH   v4.1.2
#export MPICH=/usr/local/mpi/intel21/openmpi-5.0.0                      ## OPENMPI v5.0.0

export PATH=${PATH}:${IOAPI}:${HOME}/bin:.:~:
export MANPATH=${MANPATH}

for i in $MPICH $NETCDF $PNETCDF $PIO $NCARG_ROOT $GrADS $HDF4 $HDF5 $NCO $NCVIEW $HDFVIEW $GMT $CDO ; do
  if [ ! -z $i ]; then
    if [ -d $i/bin ]; then export PATH=$i/bin:$PATH ; fi
    if [ -d $i/lib ]; then export LD_LIBRARY_PATH=$i/lib:$LD_LIBRARY_PATH ; fi
    if [ -d $i/sbin -a `id -u` = 0 ]; then export PATH=$i/sbin:$PATH ; fi
    if [ -d $i/man ]; then export MANPATH=$MANPATH:$i/man ; fi
  fi
done
unset i

source ~/.bash_profile

#### vi mpich.hosts
node01:2
node00:2

#### 복사
mpicc -o cpi.o cpi.c

#### 단일노드로 계산
mpirun -np 2 250306_mpi_test 

#### 노드를 다넣어서 계산
mpirun -machinefile ./mpich.hosts -np 4 250306_mpi_test