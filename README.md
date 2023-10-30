# EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS
## FIRST COME FIRST SERVE

### AIM:
To write a program for the first come first serve method of disc scheduling.

### DESCRIPTION:
Disk scheduling is schedule I/O requests arriving for the disk.

It is important because: -

Multiple I/O requests may arrive by different processes and only one I/O request can be served at a time
by the disk controller. Thus other I/O requests need to wait in the waiting queue and need to be
scheduled.

Two or more request may be far from each other so can result in greater disk head movement.
Hard drives are one of the slowest parts of the computer system and thus need to be accessed in an
efficient manner

FCFS is the simplest of all the Disk Scheduling Algorithms. In FCFS, the requests are addressed in the
order they arrive in the disk queue.

### PROGRAM:
```

#include <stdio.h>
#include <stdlib.h>
int main()
{
int RQ[100],i,n,TotalHeadMoment=0,initial;
printf ("Enter the number of Requests\n");
scanf("%d",&n);
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++)
scanf("%d",&RQ[i]);
printf("Enter initial head position\n");
scanf("%d",&initial);
for(i=0;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
printf("Total head moment is %d",TotalHeadMoment);
return 0;
}
```

### OUTPUT:
  
![Screenshot 2023-10-08 204204](https://github.com/Aishwarya-TM/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/127846109/a18fe07e-2e54-4400-9d7d-78e10d234555)

### RESULT:
Thus the implementation of the program for first come first serve disc scheduling has been
successfully executed.


## SHORTEST SEEK TIME FIRST

### AIM:
To write a program for the first come first serve method of disc scheduling.

### DESCRIPTION:
Shortest seek time first (SSTF) algorithm

Shortest seek time first (SSTF) algorithm selects the disk I/O request which requires the least disk arm
movement from its current position regardless of the direction. It reduces the total seek time as compared
to FCFS.

### PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
int RQ[100],i,n,TotalHeadMoment=0,initial,count=0;
printf("Enter the number of Requests\n");
scanf("%d",&n);
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++)
scanf("%d",&RQ[i]);
printf("Enter initial head position\n");
scanf("%d",&initial);
while(count!=n)
{
int min=1000,d,index;
for(i=0;i<n;i++)
{
d=abs(RQ[i]-initial);
if(min>d)
{
min=d;
index=i;
}
}
TotalHeadMoment=TotalHeadMoment+min;
initial=RQ[index];
RQ[index]=1000;
count++;
}
printf("Total head movement is %d",TotalHeadMoment);
return 0;
}

```

### OUTPUT:

![Screenshot 2023-10-08 204225](https://github.com/Aishwarya-TM/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/127846109/52055641-f28c-4d32-ab7b-f50d08a6428a)


### RESULT:
Thus the implementation of the program for shortest seek time first disc scheduling has been
successfully executed.

## SCAN

### AIM:
To write a program for the first come first serve method of disc scheduling.

### DESCRIPTION:
SCAN

It is also called as Elevator Algorithm. In this algorithm, the disk arm moves into a particular direction
till the end, satisfying all the requests coming in its path, and then it turns backend moves in the reverse
direction satisfying requests coming in its path.

It works in the way an elevator works, elevator moves in a direction completely till the last floor of that
direction and then turns back.

### PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move;
printf("Enter the number of Requests\n");
scanf("%d",&n);
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++)
scanf("%d",&RQ[i]);
printf("Enter initial head position\n");
scanf("%d",&initial);
printf("Enter total disk size\n");
scanf("%d",&size);
printf("Enter the head movement direction for high 1 and for low 0\n");
scanf("%d",&move);
for(i=0;i<n;i++)
{
for(j=0;j<n-i-1;j++)
{
if(RQ[j]>RQ[j+1])
{
int temp;
temp=RQ[j];
RQ[j]=RQ[j+1];
RQ[j+1]=temp;
}
}
}
int index;
for(i=0;i<n;i++)
{
if(initial<RQ[i])
{
index=i;
break;
}
}
if(move==1)
{
for(i=index;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
// last movement for max size
TotalHeadMoment=TotalHeadMoment+abs(size-RQ[i-1]-1);
initial = size-1;
for(i=index-1;i>=0;i--)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
}
else
{
for(i=index-1;i>=0;i--)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
TotalHeadMoment=TotalHeadMoment+abs(RQ[i+1]-0);
initial =0;
for(i=index;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
}
printf("Total head movement is %d",TotalHeadMoment);
return 0;
}

```
### OUTPUT:

![Screenshot 2023-10-08 204237](https://github.com/Aishwarya-TM/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/127846109/722601de-9db8-4732-8e97-1ddc820d8392)

### RESULT:
Thus the implementation of the program for SCAN disc scheduling has been successfully executed.
## LOOK
### AIM:
To write a program for the first come first serve method of disc scheduling.

### DESCRIPTION:
Look

It is similar to the SCAN disk scheduling algorithm except for the difference that the disk arm in spite of
going to the end of the disk goes only to the last request to be serviced in front of the head and then
reverses its direction from there only. Thus, it prevents the extra delay which occurred due to unnecessary
traversal to the end of the disk.

### PROGRAM:
```
#include<stdio.h>
#include<stdlib.h>
int main()
{
int RQ[100],i,j,n,TotalHeadMoment=0,initial,size,move;
printf("Enter the number of Requests\n");
scanf("%d",&n);
printf("Enter the Requests sequence\n");
for(i=0;i<n;i++)
scanf("%d",&RQ[i]);
printf("Enter initial head position\n");
scanf("%d",&initial);
printf("Enter total disk size\n");
scanf("%d",&size);
printf("Enter the head movement direction for high 1 and for low 0\n");
scanf("%d",&move);
for(i=0;i<n;i++)
{
for(j=0;j<n-i-1;j++)
{
if(RQ[j]>RQ[j+1])
{
int temp;
temp=RQ[j];
RQ[j]=RQ[j+1];
RQ[j+1]=temp;
}
}
}
int index;
for(i=0;i<n;i++)
{
if(initial<RQ[i])
{
index=i;
break;
}
}
if(move==1)
{
for(i=index;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
for(i=index-1;i>=0;i--)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
}
else
{
for(i=index-1;i>=0;i--)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
for(i=index;i<n;i++)
{
TotalHeadMoment=TotalHeadMoment+abs(RQ[i]-initial);
initial=RQ[i];
}
}
printf("Total head movement is %d",TotalHeadMoment);
return 0;
}
```
### OUTPUT:

![Screenshot 2023-10-08 204253](https://github.com/Aishwarya-TM/OS-EX.11-IMPLEMENTATION-OF-DISK-SCHEDULING-ALGORITHMS/assets/127846109/5657aa8c-0ed7-4eaa-b207-4710836bbbb4)

### RESULT:
Thus the implementation of the program for LOOK disc scheduling has been successfully executed.
