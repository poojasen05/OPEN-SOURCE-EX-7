# OPEN-SOURCE-EX-7

## NAME: POOJA S
## REGNO: 212223040146
## DEPT: CSE

## AIM:
To create a physical volume, volume group, and logical volume in RHEL, format it with EXT3, mount it to a directory, and make the mount persistent using `/etc/fstab`.

## PROCEDURE:

### **STEP 1:**  
Create a Physical Volume  
```bash
sudo pvcreate /dev/sdb
```

### **STEP 2:**  
Create a Volume Group with PE size 8MB  
```bash
sudo vgcreate -s 8M vg_backup /dev/sdb
```

### **STEP 3:**  
Check the PE size  
```bash
vgdisplay vg_backup | grep "PE Size"
```

### **STEP 4:**  
Expected output  
```bash
PE Size               8.00 MiB
```

### **STEP 5:**  
Create Logical Volume with 50 extents  
```bash
sudo lvcreate -l 50 -n lv_app_logs vg_backup
```

### **STEP 6:**  
Format the Logical Volume with ext3  
```bash
sudo mkfs.ext3 /dev/vg_backup/lv_app_logs
```

### **STEP 7:**  
Create mount point and mount the LV  
```bash
sudo mkdir /production
sudo mount /dev/vg_backup/lv_app_logs /production
```

### **STEP 8:**  
Verify the mounted filesystem  
```bash
df -h /production
```

### **STEP 9:**  
Make the mount persistent  
```bash
echo "/dev/vg_backup/lv_app_logs /production ext3 defaults 0 0" | sudo tee -a /etc/fstab
```

## OUTPUT:
![image](https://github.com/user-attachments/assets/2bc7f3e4-5d96-4279-a121-a13bee89eb99)

## RESULT:
The physical volume, volume group, logical volume, and persistent mount were successfully created and verified in the Red Hat Linux environment.
