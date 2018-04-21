
//consumer
#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<unistd.h>
#include<string.h>
#include<sys/stat.h>
#include<sys/ipc.h>
#include<sys/sem.h>
#include<sys/types.h>
#include<sys/shm.h>

main()
{
int shmid;
shmid=shmget(ftok("shm_file",31),100,0);
printf("Shared Memory id is: %d\n",shmid);
if(shmid==-1)
{
perror("Shared memory creation Staus");
exit(1);
}

void *attach_addr=shmat(shmid,0,SHM_RDONLY);
printf("\nAttached Memory begining address is: %d\n",attach_addr);

if((int)attach_addr==-1)
{
perror("Attaching Shared Memory Status");
exit(1);
}

struct sembuf sembuf_array[2];
int sem_id=semget(ftok("proj_file",13),0,0);
printf("Semaphore Creating value is: %d\n",sem_id);
if(sem_id==-1)
{
perror("Creating semaphore Status");
}

int i;
for(i=0;i<15;i++)
{
memset(&sembuf_array,0,sizeof(sembuf_array));
sembuf_array[0].sem_num=1;
sembuf_array[0].sem_op=-1;                      //wait
int ret_value=semop(sem_id,sembuf_array,1);
printf("\nSemop return value of wait is: %d\n",ret_value);
if(ret_value==-1)
{
perror("Semop return value status of wait status");
exit(0);
}

printf("%s\n",attach_addr);
sleep(2);

memset(&sembuf_array,0,sizeof(sembuf_array));
sembuf_array[0].sem_num=0;
sembuf_array[0].sem_op=1;
int ret_value1=semop(sem_id,sembuf_array,1);
printf("Semop return value of signal is:%d\n",ret_value1);
if(ret_value1==-1)
{
printf("Semop return value of Signal status");
}
}
}

//producer

#include<stdio.h>
#include<stdlib.h>
#include<errno.h>
#include<unistd.h>
#include<string.h>
#include<sys/stat.h>
#include<sys/ipc.h>
#include<sys/sem.h>
#include<sys/types.h>
#include<sys/shm.h>

main()
{
int shmid;
shmid=shmget(ftok("shm_file",31),100,0);
printf("Shared Memory id is: %d\n",shmid);
if(shmid==-1)
{
perror("Shared memory creation Staus");
exit(1);
}

void *attach_addr=shmat(shmid,0,0);
printf("Attached memory address is :%d\n",attach_addr);

if((int)attach_addr==-1)
{
perror("Attaching Shared Memory Status");
exit(1);
}

struct sembuf sembuf_array[2];
int sem_id=semget(ftok("proj_file",13),0,0);
printf("Semaphore Creating value is: %d\n",sem_id);
if(sem_id==-1)
{
perror("Creating semaphore Status");
}

int i;
for(i=0;i<15;i++)
{
memset(&sembuf_array,0,sizeof(sembuf_array));
sembuf_array[0].sem_num=0;
sembuf_array[0].sem_op=-1;                      //wait
int ret_value=semop(sem_id,sembuf_array,1);
printf("\nSemop return value of wait is: %d\n",ret_value);
if(ret_value==-1)
{
perror("Semop return value status of wait status");
exit(0);
}

sprintf(attach_addr,"helloworld %d\n",i);
sleep(5);

memset(&sembuf_array,0,sizeof(sembuf_array));
sembuf_array[0].sem_num=1;
sembuf_array[0].sem_op=1;
int ret_value1=semop(sem_id,sembuf_array,1);
printf("Semop return value of signal is:%d\n",ret_value1);
if(ret_value1==-1)
{
printf("Semop return value of Signal status");
}
}
}


//get

#include<stdio.h>
#include<sys/stat.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/ipc.h>
#include<sys/types.h>
#include<sys/sem.h>
#include<errno.h>

union semun
{
int val;
struct sem_id *buf;
ushort *array;
}

main()
{
int sem_id,ret_value;
unsigned short sem_values[2];
sem_id=semget(ftok("proj_file",13),0,0);
printf("Value of semaphore id created is : %d\n", sem_id);
if(sem_id==-1)
{
perror("Creating Semaphore Id Status");
}

union semun unget;
unget.array=sem_values;

ret_value=semctl(sem_id,0,GETALL,unget);
printf("The return value of semctl is : %d\n",ret_value);
if(ret_value==-1)
{
perror("Get Semaphore return value status is");
}
printf("\nThe value of semaphores1 is:%d\nThe value of semaphore2 is:%d\n",unget.array[0],unget.array[1]);
}


//set

#include<stdio.h>
#include<sys/ipc.h>
#include<sys/sem.h>
#include<errno.h>
#include<unistd.h>
#include<sys/stat.h>
#include<stdlib.h>
union semun
{
  int val;
  struct semid_ds *buf;
  ushort *array;
};

main ()
{
  int ret_value, sem_id;
  unsigned short sem_values[2] = { 1, 1 };

  sem_id = semget(ftok("proj_file", 13), 0, 0);
  printf("\nSemaphore id created is: %d\n", sem_id);
  if(sem_id == -1)
    {
      perror("Creating semaphore id status");
      exit(1);
    }
  union semun setun;
  setun.array = sem_values;


  ret_value = semctl(sem_id, 0, SETALL, setun);

  printf("Return value of semctl is %d\n", ret_value);
  if(ret_value == -1)
    {
      perror ("Return value status of semctl");
    }
  printf("\nThe value of semaphore1 set is:%d\nThe value of semaphore2 set is:%d\n",setun.array[0],setun.array[1]);
}


// wait

#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<sys/ipc.h>
#include<sys/sem.h>
#include<errno.h>

main()
{
int sem_id,ret_value;
sem_id=semget(ftok("proj_file",13),0,0);
printf("The value of semaphore id created is: %d\n",sem_id);
if(sem_id==-1)
{
printf("Creating semaphore Id status");
}

struct sembuf sembuf_array[2];
memset(&sembuf_array,0,sizeof(sembuf_array));

sembuf_array[0].sem_num=0;
sembuf_array[0].sem_op=-1;
sembuf_array[1].sem_num=1;
sembuf_array[1].sem_op=-1;

ret_value=semop(sem_id,sembuf_array,2);
printf("\nReturn value of semop is:%d\n",ret_value);
if(ret_value==-1)
{
perror("Semop return value status is");
}

}

//sig_semaphore

#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<sys/sem.h>
#include<sys/ipc.h>
#include<string.h>

/*struct sembuf
{
unsigned short sem_num; //semaphore number
short sem_op;
short sem_flg;
};*/

main()
{
int sem_id,ret_value;
sem_id=semget(ftok("proj_file",13),0,0);
printf("The value of semaphore id created is: %d\n",sem_id);
if(sem_id==-1)
{
perror("Creating semaphore Id status");
}

struct sembuf sembuf_array[2];
memset(&sembuf_array,0,sizeof(sembuf_array));

sembuf_array[0].sem_num=0;
sembuf_array[0].sem_op=1;
sembuf_array[1].sem_num=1;
sembuf_array[1].sem_op=1;

ret_value=semop(sem_id,sembuf_array,2);
printf("Return value of semaphore operation is : %d\n",ret_value);
if(ret_value==-1)
{
perror("Semop return value status");
}

}

// create sema

#include<stdio.h>
#include<sys/types.h>
#include<sys/sem.h>
#include<sys/stat.h>
#include<errno.h>
#include<unistd.h>
#include<stdlib.h>
main()
{

int sem_id = semget(ftok("proj_file",13), 2, IPC_CREAT | S_IRWXU);
printf("Semaphore Id created is:%d\n", sem_id);
if(sem_id == -1)
{
perror("Semaphore creating status:");
exit (1);
}
}






