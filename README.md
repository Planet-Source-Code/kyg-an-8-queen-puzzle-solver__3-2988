<div align="center">

## An 8 queen puzzle solver


</div>

### Description

solves the 8 queen puzzle using random generator and recursion. results in very fast answers for a chess board of any size, specified in the code
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[KYG](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/kyg.md)
**Level**          |Beginner
**User Rating**    |5.0 (10 globes from 2 users)
**Compatibility**  |C\+\+ \(general\), Microsoft Visual C\+\+
**Category**       |[Algorithms](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/algorithms__3-29.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/kyg-an-8-queen-puzzle-solver__3-2988/archive/master.zip)





### Source Code

```
//By koon yiak
//feel free to use the code and
//to tell me about possible improvements
#include <iostream.h>
#include <stdlib.h>
#include <time.h>
const int chessboardsize=40;	//size of chessboard
enum{empty, queen, used};	//status
struct move{				//movement direction
	int x;
	int y;
};
struct chessboard{			//chessboard type
int size;
int square[chessboardsize][chessboardsize];
int usedsquares;
int noqueens;
};
void setqueenmovdi(move *whatmove, chessboard *board, move *curcoor);
void main()
{
	move curcoor;
	move NE; NE.x=1; NE.y=1;	//define digonal movements
	move NW; NW.x=-1; NW.y=1;
	move SE; SE.x=1; SE.y=-1;
	move SW; SW.x=-1; SW.y=-1;
	chessboard board;
	board.size=chessboardsize;
//	srand(time(0));
	while(board.noqueens!=board.size ){
		board.usedsquares=0;
		board.noqueens=0;
		for(int i=0;i<board.size;i++)for(int j=0;j<board.size;j++)board.square[i][j]=0;
		while(board.usedsquares<board.size*board.size)
		{
			curcoor.x=rand()%board.size;
			curcoor.y=rand()%board.size;;
			if(board.square[curcoor.x][curcoor.y]==empty){
				board.square[curcoor.x][curcoor.y]=queen;
				++board.usedsquares;
				++board.noqueens;
			}else continue;
			for(int horiz=0;horiz<board.size;horiz++)if(board.square[horiz][curcoor.y]==empty){board.square[horiz][curcoor.y]=used;++board.usedsquares;}
			for(int verti=0;verti<board.size;verti++)if(board.square[curcoor.x][verti]==empty){board.square[curcoor.x][verti]=used;++board.usedsquares;}
			board.square[curcoor.x][curcoor.y]=queen;
			setqueenmovdi(&NE,&board,&curcoor);
			setqueenmovdi(&NW,&board,&curcoor);
			setqueenmovdi(&SE,&board,&curcoor);
			setqueenmovdi(&SW,&board,&curcoor);
		}
	}
	cout<<endl;
	for(int i2=0;i2<board.size;i2++){
		for(int j2=0;j2<board.size;j2++)cout<<board.square[i2][j2];
		cout<<endl;
	}
}
void setqueenmovdi(move *whatmove,chessboard *board,move *curcoor)
{
	move next;
	next.x=curcoor->x+whatmove->x; next.y=curcoor->y+whatmove->y;
	if(next.x<0||next.x>board->size-1||next.y<0||next.y>board->size-1)return;
	if(board->square[next.x][next.y]==empty){
		board->square[next.x][next.y]=used;
		++board->usedsquares;
	}
	setqueenmovdi(whatmove,board,&next);
	return;
}
```

