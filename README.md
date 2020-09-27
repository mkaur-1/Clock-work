# Clock-work code1
#include<iostream>
#include<cstdio>
#include<ctime>
using namespace std;
const int COLS=4;
const int ROWS=5;
const char CLOCK_CHAR='*';
const char* const codes[]={"11101010101010101110",
  // digit 1 
  "01000100010001000100",
  // digit 2 
  "11100010111010001110",
  // digit 3 
  "11100010111000101110",
  // digit 4 
  "10101010111000100010",
  // digit 5 
  "11101000111000101110",
  // digit 6 
  "11101000111010101110",
  // digit 7 
  "1110001000100010001",
  // digit 8 
  "11101010111010101110",
  // digit 9 
  "11101010111000100010",
  // semi-colon separator 
  "00000100000001000000"
};
char canvas[ROWS][COLS*5]={{0}};
void storeDigit(int digit,int offset);
int main()
{
	start:
		time_t t;
		time(&t);
		tm* local=localtime(&t);
		int hour=local->tm_hour;
		int min=local->tm_min;
		storeDigit(hour/10,0);
		storeDigit(hour%10,4);
		storeDigit(10,8);
		storeDigit(min/10,12);
		storeDigit(min%10,16);
		for(int row=0;row<ROWS;row++)
		{
			for(int col=0;col<COLS*5;col++)
			{
				printf("%c",canvas[row][col]);
			}
			cout<<endl;
		}
		cout<<"Clock updating in 15 secs";
		system("cls");
		goto start;
		return 0;
	}
	void storeDigit(int digit,int offset)
	{
		for(int row=0;row<ROWS;row++)
		{
			for(int col=0;col<COLS;col++)
			{
				int x=offset+col;
				int y=row;
				int dot=COLS*row +col;
				if('1'==codes[digit][dot])
				{
					canvas[y][x]=CLOCK_CHAR;
				}
			}
		}
		}	

