@master
#### vi /etc/exports
/usr/local       node*(rw,async,no_root_squash,no_all_squash,no_subtree_check)

exportfs -r

@slave
#### vi /etc/fstab
#### NFS
node00:/usr/local			  /usr/local		  nfs	  defaults	  0 0

mount -a