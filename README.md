# Tower-of-Hanoi
The Tower of Hanoi is a famous mathematical puzzle that consists of three nods and a number of disks of different sizes. Objective of the game is to move the disks from one node to another. Rules of the puzzle includes only being able to place a smaller disk on top of a bigger disk and only being able to move one disk at a time.

Coded in C

#include <stdio.h>
#include<string.h>
#include<unistd.h>
#include<stdlib.h>


int peg1[9],peg2[9],peg3[9];

//I made this so I dont have to keep creating the pegs
void pegtemp(int num){
        switch(num){
                case 0:
                        printf("          |          ");
                        break;
                case 1:
                        printf("         +|+         ");
                        break;
                case 2:
                        printf("        ++|++        ");
                        break;
                case 3:
                        printf("       +++|+++       ");
                        break;
                case 4:
                        printf("      ++++|++++      ");
                        break;
                case 5:
                        printf("     +++++|+++++     ");
                        break;
                case 6:
                        printf("    ++++++|++++++    ");
                        break;
                case 7:
                        printf("   +++++++|+++++++   ");
                        break;
                case 8:
                        printf("  ++++++++|++++++++  ");
                        break;
                case 9:
                        printf(" +++++++++|+++++++++ ");
                        break;
		case 10:
			printf("XXXXXXXXXXXXXXXXXXXXX     XXXXXXXXXXXXXXXXXXXXX     XXXXXXXXXXXXXXXXXXXXX\n");
			break;
		case 11:
			printf("          |                         |                         |          \n");
			break;
    }
}


void display_pegs(){
	int i;
	pegtemp(11);	
	for (i = 8; i>=0; i--){
		pegtemp(peg1[i]);
		printf("     ");
		pegtemp(peg2[i]);
		printf("     ");
		pegtemp(peg3[i]);
		printf("\n");
	}
	pegtemp(10);
}
void move(int pegA[9], int pegB[9]){
    int i, temp;
    for (i = 8; i >= 0; i--){
        if (pegA[i] != 0){
            temp = pegA[i];
            pegA[i] = 0;
            break;
        }
    }
    
    for(i = 0; i < 9; i++){
        if(pegB[i] == 0){
            pegB[i] = temp;
            break;
        }
    }
    display_pegs();
    sleep(1);
} 
void toh(int nod, int from[9], int to[9], int helper[9]){
    if (nod > 1) toh(nod-1,from,helper,to);
    move(from,to);
    if (nod > 1) toh(nod-1,helper,to,from);
    
}
int main(int argc, char *argv[]){
    int num_of_disks = atoi(argv[1]);
    if(argc != 2){
        printf("Needs exactly \"2\" command line arguments\n");
        return 0;
    }else if(num_of_disks < 1 || num_of_disks > 9){
        printf("Incorrect argument: Must be integer in the range of \"1 to 9\"\n");    
        return 0;
    } 
    
    int i;
    int temp = num_of_disks;
    for (i = 0; i < 9; i++){
        peg1[i] = temp;
        temp--;
        if (temp == 0){
            break;
        }
    }
    display_pegs();
    sleep(1);
    toh(num_of_disks,peg1,peg2,peg3);
    printf("\ndone\n");
}



