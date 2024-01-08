AD52: Operating System Laboratory Programs


Program 1: Program For System Calls Of Unix Operating System (fork, getpid, exit)
#include<stdio.h>
#include<unistd.h>
main()
{
int pid,pid1,pid2; 
pid=fork(); 
if(pid==-1)
{
printf(“ERROR IN PROCESS CREATION \n”);
exit(1);
}
if(pid!=0)
{
pid1=getpid();
printf(“\n the parent process ID is %d\n”, pid1);
}
else
{
pid2=getpid();
printf(“\n the child process ID is %d\n”, pid2);
}
}

2)FCFS

#include <stdio.h>
int main()
{
    int pid[15];
    int bt[15];
    int n;
    printf("Enter the number of processes: ");
    scanf("%d",&n);
 
    printf("Enter process id of all the processes: ");
    for(int i=0;i<n;i++)
    {
        scanf("%d",&pid[i]);
    }
 
    printf("Enter burst time of all the processes: ");
    for(int i=0;i<n;i++)
    {
        scanf("%d",&bt[i]);
    }
 
    int i, wt[n];
    wt[0]=0;
 
    //for calculating waiting time of each process
    for(i=1; i<n; i++)
    {
        wt[i]= bt[i-1]+ wt[i-1];
    }
 
    printf("Process ID     Burst Time     Waiting Time     TurnAround Time\n");
    float twt=0.0;
    float tat= 0.0;
    for(i=0; i<n; i++)
    {
        printf("%d\t\t", pid[i]);
        printf("%d\t\t", bt[i]);
        printf("%d\t\t", wt[i]);
 
        //calculating and printing turnaround time of each process
        printf("%d\t\t", bt[i]+wt[i]);
        printf("\n");
 
        //for calculating total waiting time
        twt += wt[i];
 
        //for calculating total turnaround time
        tat += (wt[i]+bt[i]);
    }
    float att,awt;
 
    //for calculating average waiting time
    awt = twt/n;
 
    //for calculating average turnaround time
    att = tat/n;
    printf("Avg. waiting time= %f\n",awt);
    printf("Avg. turnaround time= %f",att);
}

3)SJF

#include<stdio.h>
int main()
{
    int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,totalT=0,pos,temp;
    float avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
 
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("p%d:",i+1);
        scanf("%d",&bt[i]);
        p[i]=i+1;
    }
 
    //sorting of burst times
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(bt[j]<bt[pos])
                pos=j;
        }
 
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
 
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
 
    wt[0]=0;
 
    //finding the waiting time of all the processes
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
             //individual WT by adding BT of all previous completed processes
            wt[i]+=bt[j];
 
        //total waiting time
        total+=wt[i];   
    }
 
    //average waiting time
    avg_wt=(float)total/n;  
 
    printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        //turnaround time of individual processes
        tat[i]=bt[i]+wt[i]; 
 
        //total turnaround time
        totalT+=tat[i];      
        printf("\np%d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
 
    //average turnaround time
    avg_tat=(float)totalT/n;     
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f",avg_tat);
}


Program 4: To write a C program for implementation of Priority scheduling algorithms.

/*
 * C Program to Implement Priority Scheduling
 */
#include<stdio.h>
int main()
{
    int bt[20],p[20],pri[20],wt[20],tat[20],i,j,n,total=0,totalT=0,pos,temp;
    float avg_wt,avg_tat;
    printf("Enter number of process:");
    scanf("%d",&n);
    printf("\nEnter Burst Time:\n");
    for(i=0;i<n;i++)
    {
        printf("Enter Burst time p%d:",i+1);
        scanf("%d",&bt[i]);
        printf("Enter Priority p%d:",i+1);
        scanf("%d",&pri[i]);
        p[i]=i+1;
    }
    //sorting of burst times
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(pri[j]<pri[pos])
                pos=j;
        }
        temp=pri[i];
        pri[i]=pri[pos];
        pri[pos]=temp;
        
         temp=pri[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
        
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
    wt[0]=0;
    //finding the waiting time of all the processes
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
             //individual WT by adding BT of all previous completed processes
            wt[i]+=bt[j];
        //total waiting time
        total+=wt[i];   
    }
    //average waiting time
    avg_wt=(float)total/n;
    printf("\nProcess\t Burst Time \tPriority \t Waiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        //turnaround time of individual processes
        tat[i]=bt[i]+wt[i]; 
        //total turnaround time
        totalT+=tat[i];      
        printf("\np%d\t\t %d\t\t %d\t\t%d\t\t\t%d",p[i],bt[i],wt[i],pri[i],tat[i]);
    }
    //average turnaround time
    avg_tat=(float)totalT/n;     
    printf("\n\nAverage Waiting Time=%f",avg_wt);
    printf("\nAverage Turnaround Time=%f",avg_tat);
}





Program 5: To write a C-program to implement the producer – consumer problem using semaphores.

PROGRAM:
#include<stdio.h>
int mutex=1,full=0,empty=3,x=0; main()
{
int n;
void producer(); void consumer(); 
int wait(int);
int signal(int); 
printf("\n1.PRODUCER\n2.CONSUMER\n3.EXIT\n"); 
while(1) 
{
printf("\nENTER YOUR CHOICE\n"); 
scanf("%d",&n);
switch(n)
{ 
case 1:
if((mutex==1)&&(empty!=0)) 
producer();
else
printf("BUFFER IS FULL");
 break;	
case 2: 
if((mutex==1)&&(full!=0)) 
consumer();
else
printf("BUFFER IS EMPTY");
break; 
case 3:
exit(0); 
break;
}
}
}
int wait(int s) 
{ 
return(--s); }

int signal(int s) 
{ 
return(++s); } 
void producer() 
{
mutex=wait(mutex); 
full=signal(full); 
empty=wait(empty); 
x++;
printf("\nproducer produces the item%d",x); 
mutex=signal(mutex); 
   }
void consumer() 
{ 
mutex=wait(mutex); 
full=wait(full); 
empty=signal(empty);
printf("\n consumer consumes item%d",x); 
x--;
mutex=signal(mutex); 
     }


Program 6: To write a c program to implement IPC using shared memory.

PROGRAM:
#include<stdio.h> 
#include<stdlib.h>
 #include<unistd.h> 
#include<string.h> 
#include<sys/ipc.h>
 #include<sys/shm.h> 
#include<sys/types.h> 
#define SEGSIZE 100
int main(int argc, char *argv[ ])
{
int shmid,cntr; key_t key; char *segptr;
char buff[]="poooda	";
key=ftok(".",'s');
if((shmid=shmget(key, SEGSIZE, IPC_CREAT | IPC_EXCL | 0666))== -1)
{
if((shmid=shmget(key,SEGSIZE,0))==-1)
{
perror("shmget"); exit(1);
}
}
else
{
printf("Creating a new shared memory seg \n");          
printf("SHMID:%d",shmid);
}
system("ipcs –m"); 
if((segptr=(char*)shmat(shmid,0,0))==(char*)-1)
{
perror("shmat"); exit(1);
}
printf("Writing data to shared memory…\n"); strcpy(segptr,buff);
printf("DONE\n");
printf("Reading data from shared memory…\n"); printf("DATA:-%s\n",segptr);  
printf("DONE\n");
printf("Removing shared memory Segment…\n"); 
if(shmctl(shmid,IPC_RMID,0)== -1)
printf("Can‟t Remove Shared memory Segment…\n"); 
else
printf("Removed Successfully");
}





7)Bankers algorithm 

#include <stdio.h>  
int main()  
{  
    // P0, P1, P2, P3, P4 are the Process names here  
  
    int n, m, i, j, k;  
    n = 5;                         // Number of processes  
    m = 3;                         // Number of resources  
    int alloc[5][3] = {{0, 1, 0},  // P0 // Allocation Matrix  
                       {2, 0, 0},  // P1  
                       {3, 0, 2},  // P2  
                       {2, 1, 1},  // P3  
                       {0, 0, 2}}; // P4  
  
    int max[5][3] = {{7, 5, 3},  // P0 // MAX Matrix  
                     {3, 2, 2},  // P1  
                     {9, 0, 2},  // P2  
                     {2, 2, 2},  // P3  
                     {4, 3, 3}}; // P4  
  
    int avail[3] = {3, 3, 2}; // Available Resources  
  
    int f[n], ans[n], ind = 0;  
    for (k = 0; k < n; k++)  
    {  
        f[k] = 0;  
    }  
    int need[n][m];  
    for (i = 0; i < n; i++)  
    {  
        for (j = 0; j < m; j++)  
            need[i][j] = max[i][j] - alloc[i][j];  
    }  
    int y = 0;  
    for (k = 0; k < 5; k++)  
    {  
        for (i = 0; i < n; i++)  
        {  
            if (f[i] == 0)  
            {  
                int flag = 0;  
                for (j = 0; j < m; j++)  
                {  
                    if (need[i][j] > avail[j])  
                    {  
                        flag = 1;  
                        break;  
                    }  
                }  
                if (flag == 0)  
                {  
                    ans[ind++] = i;  
                    for (y = 0; y < m; y++)  
                        avail[y] += alloc[i][y];  
                    f[i] = 1;  
                }  
            }  
        }  
    }  
    int flag = 1;  
    for (int i = 0; i < n; i++)  
    {  
        if (f[i] == 0)  
        {  
            flag = 0;  
            printf("The following system is not safe");  
            break;  
        }  
    }  
    if (flag == 1)  
    {  
        printf("Following is the SAFE Sequence\n");  
        for (i = 0; i < n - 1; i++)  
            printf(" P%d ->", ans[i]);  
        printf(" P%d", ans[n - 1]);  
    }  
    return (0);  
}  


8)First fit

#include<stdio.h>
 
void main()
{
int bsize[10], psize[10], bno, pno, flags[10], allocation[10], i, j;
 
for(i = 0; i < 10; i++)
{
flags[i] = 0;
allocation[i] = -1;
}
printf("Enter no. of blocks: ");
scanf("%d", &bno);
printf("\nEnter size of each block: ");
for(i = 0; i < bno; i++)
scanf("%d", &bsize[i]);
 
printf("\nEnter no. of processes: ");
scanf("%d", &pno);
printf("\nEnter size of each process: ");
for(i = 0; i < pno; i++)
scanf("%d", &psize[i]);
for(i = 0; i < pno; i++)         //allocation as per first fit
for(j = 0; j < bno; j++)
if(flags[j] == 0 && bsize[j] >= psize[i])
{
allocation[j] = i;
flags[j] = 1;
break;
}
//display allocation details
printf("\nBlock no.\tsize\t\tprocess no.\t\tsize");
for(i = 0; i < bno; i++)
{
printf("\n%d\t\t%d\t\t", i+1, bsize[i]);
if(flags[i] == 1)
printf("%d\t\t\t%d",allocation[i]+1,psize[allocation[i]]);
else
printf("Not allocated");
}
}


9)Best fit
#include<stdio.h>
 
void main()
{
int fragment[20],b[20],p[20],i,j,nb,np,temp,lowest=9999;
static int barray[20],parray[20];
printf("\n\t\t\tMemory Management Scheme - Best Fit");
printf("\nEnter the number of blocks:");
scanf("%d",&nb);
printf("Enter the number of processes:");
scanf("%d",&np);
printf("\nEnter the size of the blocks:-\n");
for(i=1;i<=nb;i++)
    {
printf("Block no.%d:",i);
        scanf("%d",&b[i]);
    }
printf("\nEnter the size of the processes :-\n");
for(i=1;i<=np;i++)
    {
        printf("Process no.%d:",i);
        scanf("%d",&p[i]);
    }
for(i=1;i<=np;i++)
{
for(j=1;j<=nb;j++)
{
if(barray[j]!=1)
{
temp=b[j]-p[i];
if(temp>=0)
if(lowest>temp)
{
parray[i]=j;
lowest=temp;
}
}
}
fragment[i]=lowest;
barray[parray[i]]=1;
lowest=10000;
}
printf("\nProcess_no\tProcess_size\tBlock_no\tBlock_size\tFragment");
for(i=1;i<=np && parray[i]!=0;i++)
printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d",i,p[i],parray[i],b[parray[i]],fragment[i]);
}
