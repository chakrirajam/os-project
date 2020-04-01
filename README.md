# os-project
Os project
Name: Rajam chakradar 
Registration number:11713751 
Roll number:67 
E-mail: chakradarrajam05434@gmail.com 
GitHub link: 
 
 
4. Consider the scenario, there are 3 student processes and 1 teacher process. Students are supposed to do their assignments and they need 3 things for that-pen, paper and question paper. The teacher has an infinite supply of all the three things. One students has pen, another has paper and another has question paper. The teacher places two things on a shared table and the student having the third complementary thing makes the assignment and tells the teacher on completion. The teacher then places another two things out of the three and again the student having the third thing makes the assignment and tells the teacher on completion. This cycle continues. WAP to synchronise the teacher and the students. 
 
●	Two types of people can enter into a library- students and teachers. After entering the library, the visitor searches for the required books and gets them. In order to get them issued, he goes to the single CPU which is there to process the issuing of books. Two types of queues are there at the counter-one for students and one for teachers. A student goes and stands at the tail of the queue for students and similarly the teacher goes and stands at the tail of the queue for teachers (FIFO). If a student is being serviced and a teacher arrives at the counter, he would be the next person to get service (PRIORITY-non preemptive). If two teachers arrive at the same time, they will stand in their queue to get service (FIFO). WAP to ensure that the system works in a non-chaotic  manner. 
●	If a teacher is being served and during the period when he is being served, another 
 
teacher comes, then that teacher would get the service next. This process might continue leading to increase in waiting time of students. Ensure in your program that the waiting time of students is minimized. 
 
Explanation: 
1.	In the given solution I have taken all the student processes and resources in 2D array and initialized then to 0. 
2.	I have made 3 student processes in three different functions which will be executed by single s_thread and one t_thread for execution of teacher process. 
3.	User will get a menu to select any two out of three resources that are to be placed on shared table. 
4.	If one process is completed there will be a message printed on the screen saying process is completed. 
5.	When one process is executing no other student or teacher process will execute and for achieving this I have used Mutex lock. 
6.	When a process starts to execute it acquires the lock and when it completes the execution releases the lock. 
7.	After completion of all the three processes the program will end. 
Code : 
#include<stdio.h> 
#include<stdlib.h> 
#include<pthread.h> #include<stdbool.h> int student[3][4]={0}; void *teacher(); void *student1(); void *student2(); void *student3(); pthread_mutex_t lck; int ch1,ch2; 
int r1,r2; 
 
int main() 
{ 	 
printf("\t\t\t---Welcome---\n"); 
 	pthread_mutex_init(&lck,NULL);\ 
student[1][1]=1; 
 	student[2][2]=2;student[3][3]=1; 
 pthread_t t_thread;  pthread_t s_thread; printf("Resources Menu: \n\t\tPress '1' for pen\n\t\tPress '2' for paper \n\t\tPress '3' for   question_paper \n");   
 	while(1) 
{ if(student[1][4]==1 && student[2][4]==1 && student[3][4]==1){break;} pthread_create(&t_thread, NULL, teacher, NULL); pthread_join(t_thread,NULL); 
 	     
if((ch1==1 && ch2==2 || ch2==1 && ch1==2 ) && student[3][4]==0) 
{ 
 	pthread_create(&s_thread, NULL, student3, NULL);  	pthread_join(s_thread,NULL); 
} 
else if((ch1==1 && ch2==3 || ch2==1 && ch1==3 ) && student[2][4]==0) 
{ pthread_create(&s_thread, NULL, student2, NULL); 
 	pthread_join(s_thread,NULL); 
} 
else if((ch1==2 && ch2==3 || ch2==2 && ch1==3 ) && student[1][4]==0) 
{ 
 	pthread_create(&s_thread, NULL, student1, NULL); pthread_join(s_thread,NULL); 
} else { 
 	printf("\n\tError (007): try again.. with different choices.\n"); 
} 
} 
printf("\n\t----Done---\n"); 
} 
 
 
void *teacher() 
{ pthread_mutex_lock(&lck); 
 	printf("\nFirst Resource on shared tabel:-\t");  	scanf("%d",&ch1); 
 	printf("Second Resource on shared tabel:-\t");  	scanf("%d",&ch2); 
 	pthread_mutex_unlock(&lck); 
} 
 
void *student2() 
{ 	 
 	pthread_mutex_lock(&lck); 
 	printf("\nChoices Made = 'pen', 'question_paper'\n");  	student[2][4]=1; 
 	printf("\n\tStudent 2 has Completed the assignment. \n"); 
 	pthread_mutex_unlock(&lck); 
} 
 
void *student3() 
{ 	 
 	pthread_mutex_lock(&lck);  	printf("\nChoices Made = 'pen', 'paper'\n"); 
 	student[3][4]=1; 
 	printf("\n\tStudent 3 has Completed the assignment.\n"); 
 	pthread_mutex_unlock(&lck); 
} 
 
void *student1() 
{ 	 
 	pthread_mutex_lock(&lck); 
 	printf("\nChoices Made = 'paper', 'question_paper'\n");  	student[1][4]=1; 
 printf("\n\tStudent 1 has Completed the assignment.\n");  
 	pthread_mutex_unlock(&lck); 
} 

Screenshot of output :


 
 
Explanation: 
In priority scheduling algorithm each process has a priority associated with it and as each process hits the queue, it is stored in based on its priority so that process with higher priority are dealt with first. It should be noted that equal priority processes are scheduled in FCFS order 
 	To prevent high priority processes from running indefinitely the scheduler may decrease the priority of the currently running process at each clock tick (i.e., at each clock interrupt). If this action causes its priority to drop below that of the next highest process, a process switch occurs. Alternatively, each process may be assigned a maximum time quantum that it is allowed to run. When this quantum is used up, the next highest priority process is given a chance to run.

The problem occurs when the operating system gives a particular task a very low priority, so it sits in the queue for a larger amount of time, not being dealt with by the CPU. If this process is something the user needs, there could be a very long wait, this process is known as “Starvation” or “Infinite Blocking”.

Code : 
#include<stdio.h>
 
int main()
{
    int bt[20],p[20],wt[20],tat[20],pr[20],i,j,n,total=0,pos,temp,avg_wt,avg_tat;
    printf("Enter Total Number of Process:");
    scanf("%d",&n);
 
    printf("\nEnter Burst Time and Priority\n");
    for(i=0;i<n;i++)
    {
        printf("\nP[%d]\n",i+1);
        printf("Burst Time:");
        scanf("%d",&bt[i]);
        printf("Priority:");
        scanf("%d",&pr[i]);
        p[i]=i+1;           //contains process number
    }
 
    //sorting burst time, priority and process number in ascending order using selection sort
    for(i=0;i<n;i++)
    {
        pos=i;
        for(j=i+1;j<n;j++)
        {
            if(pr[j]<pr[pos])
                pos=j;
        }
 
        temp=pr[i];
        pr[i]=pr[pos];
        pr[pos]=temp;
 
        temp=bt[i];
        bt[i]=bt[pos];
        bt[pos]=temp;
 
        temp=p[i];
        p[i]=p[pos];
        p[pos]=temp;
    }
 
    wt[0]=0;	//waiting time for first process is zero
 
    //calculate waiting time
    for(i=1;i<n;i++)
    {
        wt[i]=0;
        for(j=0;j<i;j++)
            wt[i]+=bt[j];
 
        total+=wt[i];
    }
 
    avg_wt=total/n;      //average waiting time
    total=0;
 
    printf("\nProcess\t    Burst Time    \tWaiting Time\tTurnaround Time");
    for(i=0;i<n;i++)
    {
        tat[i]=bt[i]+wt[i];     //calculate turnaround time
        total+=tat[i];
        printf("\nP[%d]\t\t  %d\t\t    %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
    }
 
    avg_tat=total/n;     //average turnaround time
    printf("\n\nAverage Waiting Time=%d",avg_wt);
    printf("\nAverage Turnaround Time=%d\n",avg_tat);
 
	return 0;
}

Screenshot of output :

