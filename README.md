<h1> Project I_ROLLUP </h1>

<h4> Implementing ROLLUP and CUBE Operations in PostgreSQL </h4>
<p>
Extended <b>GROUP BY</b> operation in postgresql-9.3.5 to allow <b>GROUP BY CUBE</b> and <b>GROUP BY ROLLUP</b> operations. The repository contains modified source of postgresql-9.3.5 as well as a patch file <i>patch_i_roll_up.txt</i> for these changes. There is also <i>populateDB.sql</i> script to enter sample data in the database.
</p>

<h4> Steps to Run </h4>
<ul>
 <li>Download postgresql-9.3.5 source</li>
 <li>cd to directory where the source is downloaded</li>
 <li>patch -p1 &lt; &lt; path to patch file &gt;</li>
 <li>export POSTGRES_INSTALLDIR=&lt;path to install dir&rt;</li>
 <li>export POSTGRES_SRCDIR=&lt;path to postgre source dir&rt;</li>
 <li>cd ${POSTGRES_SRCDIR}</li>
 <li>./configure --prefix=${POSTGRES_INSTALLDIR} --enable-debug</li>
 <li>make | tee make.out</li>
 <li>make install | tee make_install.out</li>
 <li>export LD_LIBRARY_PATH=${POSTGRES_INSTALLDIR}/lib:${LD_LIBRARY_PATH}</li>
 <li>export PATH=${POSTGRES_INSTALLDIR}/bin:${PATH}</li>
 <li>export PGDATA=${POSTGRES_INSTALLDIR}/data</li>
 <li>initdb -D ${PGDATA}</li>
 <li>postmaster -D  $PGDATA > logfile 2>&1 &</li>
</ul>

<h4>NOTE 1</h4>
<p>If you are running on a shared machine, you may need to change the port on which 
postgresql listens from the defaulty of 5432 to some other port.  Otherwise there will
be a port clash.  To avoid this, Edit <i> ${POSTGRES_INSTALLDIR}/data/postgresql.conf </i>
uncomment port=5432, and change it to (say) 9432. </p>

<h4> Create Database </h4>
 createdb -p 9432 test

<h4> To Run on multi-user server </h4>
 psql -p 9432 test

<h4> To Stop the server </h4>
 pg_ctl stop

<h4> To Run in single-user mode </h4>
 postgres --single -D ${PGDATA} test
