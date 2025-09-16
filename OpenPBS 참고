# change PBS hostname
sed -i s/$old/$new/g /var/spool/torque/server_name
sed -i s/$old/$new/g /var/spool/torque/mom_priv/config
sed -i s/$old/$new/g /var/spool/torque/server_priv/acl_svr/acl_hosts
sed -i s/$old/$new/g /var/spool/torque/server_priv/acl_svr/managers
sed -i s/$old/$new/g /var/spool/torque/server_priv/acl_svr/operators
sed -i s/$old/$new/g /var/spool/torque/server_priv/nodes

#### vi /etc/pbs.conf
PBS_EXEC=/opt/pbs
PBS_SERVER=node00         #### 호스트네임 변경
PBS_START_SERVER=1
PBS_START_SCHED=1
PBS_START_COMM=1
PBS_START_MOM=1
PBS_HOME=/var/spool/pbs
PBS_CORE_LIMIT=unlimited
PBS_SCP=/bin/scp

[root@node02 ~]# qmgr -c "d n node00"                 ## 기존정보 삭제
[root@node02 ~]# qmgr -c "c n node01"                 ## 변경정보 추가