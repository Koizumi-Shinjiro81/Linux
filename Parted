df -Th
fdisk -l
parted /dec/sdc
p
mklabel gpt
mkpart - Enter - Enter - 0 - -1 -Enter
p
q
fdisk -l
mkfs.xfs /dev/sda1 -f
blkid - UUID 복사
vi /etc/fstab - UUID 붙여넣기 
gui가 지원안될경우
:.!blkid | grep /dev/sda1