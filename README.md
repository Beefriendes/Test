#include <iostream>
#include <vector>
#include <string>

using namespace std;

int direct[4][2] = { { 1, 0 }, { 0, 1 }, { -1, 0 }, { 0, -1 } }; // 下、右、上、左

bool IsValid( int x, int y, int column, int line );


bool IsValid( int x, int y, int column, int line ) {

  if ( x >= 0 && y >= 0 && x < column && y < line )
    return true;
    
  return false;

}


int main() {

  int column, line, num = 0;
  string input, temp;
  vector<string> data;
  vector<string> data_num;
  bool judge = false;
  
  cin >> column >> line;
  
  while ( column != 0 || line != 0 ) {
    
    if ( judge )
      cout << "\n";
      
    judge = true;
    num++;
    int nowx = 0, nowy = 0;
    
    for ( int i = 0; i < line; i++ ) 
      temp = temp + "0";
    
    
    for ( int i = 0; i < column; i++ ) {
      cin >> input;
      data.push_back( input );
      data_num.push_back( temp );
     // cout << data_num[i];
    }
  
    for ( int x = 0; x < column; x++ ) {
    
      for ( int y = 0; y < line; y++ ) {
      
        if ( data[x][y] == '*' ) {
          
          data_num[x][y] = '9';
          nowx = x - 1;
          nowy = y - 1;
                
          for ( int i = 0; i < 4; i++ ) {
            for ( int j = 0; j < 2; j++ ) {
             
              nowx = nowx + direct[i][0];
              nowy = nowy + direct[i][1];
              
              if ( IsValid( nowx, nowy, column, line ) ) 
                data_num[nowx][nowy] = data_num[nowx][nowy] + 1;

            }
            
          }
          
        }
        
        
      }
    }
    
    cout << "Field #" << num << ":\n";
    
    for ( int x = 0; x < column; x++ ) {
    
      for ( int y = 0; y < line; y++ ) {
   
        if ( data_num[x][y] >= '9' )
          cout << '*';
        else
          cout << data_num[x][y];
        
      }
      
      cout << endl;
      
    }
    
    data.clear();
    temp.clear();
    data_num.clear();
    
    cin >> column >> line;
  }
  


}
