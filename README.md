Project I_ROLLUP

Implementing ROLLUP and CUBE Operations in PostgreSQL

Steps to Run
------------
 Download postgresql-9.3.5 source
 cd to directory where the source is downloaded
 patch -p1 < < path to patch file > 
 export POSTGRES_INSTALLDIR=<path to install dir>
 export POSTGRES_SRCDIR=<path to postgre source dir>
 cd ${POSTGRES_SRCDIR}
 ./configure --prefix=${POSTGRES_INSTALLDIR} --enable-debug
 make | tee make.out
 make install | tee make_install.out
 export LD_LIBRARY_PATH=${POSTGRES_INSTALLDIR}/lib:${LD_LIBRARY_PATH}
 export PATH=${POSTGRES_INSTALLDIR}/bin:${PATH}
 export PGDATA=${POSTGRES_INSTALLDIR}/data
 initdb -D ${PGDATA}
 postmaster -D  $PGDATA > logfile 2>&1 &

NOTE 1: If you are running on a shared machine, you may need to change the port on which 
postgresql listens from the defaulty of 5432 to some other port.  Otherwise there will
be a port clash.  To avoid this, Edit ${POSTGRES_INSTALLDIR}/data/postgresql.conf
uncomment port=5432, and change it to (say) 9432. 

 createdb -p 9432 test

To Run on multi-user server
 psql -p 9432 test

To Stop the server 
 pg_ctl stop

To Run in single-user mode
 postgres --single -D ${PGDATA} test
