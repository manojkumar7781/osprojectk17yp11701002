# osprojectk17yp11701002
program on longest time remaining first
#include <stdio.h>
#include<unistd.h>
 
struct process { 
	int processno; 
	int AT; 
	int BT; 

	 
	int BTbackup; 
	int WT; 
	int TAT; 
	int CT; 
}; 


struct process p[3]; 


int totaltime = 0; 
int prefinaltotal = 0; 
 
int findlargest(int at) 
{ 
	int max = 0, i; 
	for (i = 0; i < 3; i++) { 
		if (p[i].AT <= at) { 
			if (p[i].BT > p[max].BT) 
				max = i; 
		} 
	} 

	 
	return max; 
} 


int findCT() 
{ 

	int index; 
	int flag = 0; 
	int i = p[0].AT; 
	while (1) { 
		if (i <= 3) { 
			index = findlargest(i); 
		} 

		else
			index = findlargest(3); 
		

		p[index].BT -= 1; 
		totaltime += 1; 
		i++; 

		if (p[index].BT == 0) { 
			p[index].CT = totaltime; 
			
		}  

	
		if (totaltime == prefinaltotal) 
			break; 
	}
} 

int main() 
{ 

	int i; 


	for (i = 0; i < 3; i++) {
	if(i==0) {
		p[i].processno =2102;}
		else if(i==1) {
		p[i].processno =2132;}
		else if(i==2) {
		p[i].processno =2152;}
	} 


	for (i = 0; i < 3; i++) 
	{ 
		p[i].AT =0; 
	} 

 
	for (i =0; i <3; i++) { 


		if(i==0) {
		p[i].BT =4; 
		p[i].BTbackup = p[i].BT; 
		prefinaltotal += p[i].BT;
	}
	else if(i==1) {
		p[i].BT =2; 
		p[i].BTbackup = p[i].BT; 
		prefinaltotal += p[i].BT;
	}
	else if(i==2) {
		p[i].BT =8; 
		p[i].BTbackup = p[i].BT; 
		prefinaltotal += p[i].BT;
	}
	} 

 
	printf("PNo\tAT\tBT\n"); 

	for (i = 0; i < 3; i++) { 
		printf( "%d\t",p[i].processno); 
		printf("%d\t",p[i].AT); 
		printf("%d\t",p[i].BT); 
		printf("\n"); 
	} 
	printf("\n"); 


	totaltime += p[0].AT; 


	prefinaltotal += p[0].AT; 
	findCT(); 
	int totalWT = 0; 
	int totalTAT = 0; 
	for (i = 0; i < 3; i++) { 
		
		p[i].TAT = p[i].CT - p[i].AT; 
		p[i].WT = p[i].TAT - p[i].BTbackup; 

 
		totalWT += p[i].WT; 

		 
		totalTAT += p[i].TAT; 
	} 


	printf("PNo\tAT\tBT\tCT\tTAT\tWT\n"); 

	for (i = 0; i < 3; i++) { 
		printf("%d\t",p[i].processno);
		printf("%d\t",p[i].AT); 
		printf("%d\t",p[i].BTbackup); 
		printf("%d\t",p[i].CT ); 
		printf("%d\t",p[i].TAT ); 
		printf("%d\t",p[i].WT ); 
		printf("\n"); 
	} 

	printf("\n"); 
	printf("Total TAT = %d\n",totalTAT); 
	printf("Average TAT = %d\n",totalTAT / 3.0); 
	printf("Total WT = %d\n" ,totalWT); 
	printf("Average WT =  %d\n",totalWT / 3.0); 
	return 0; 
}
