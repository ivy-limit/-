# -
字典部分代码

```c++
#include <iostream>
#include <sstream>
#include <fstream>
#include <string>
#include <vector>
#include <map>
#include <regex>
/*
    文件中只有数字，字母，字符“:”,“\n”
    map<string, map<int, vector<string>>>
        message   number     processed
        处理后的子字符串^
    密码中可以含有特殊字符，如：“!@#$%^&*_”之类。
    一般情况下最短长度不得少于8个字符。

*/
using namespace std;
typedef vector<string>  vectTemp;
typedef map<int, vectTemp>  mapTemp;
typedef map<string, mapTemp>  MapM;

int main(int args, char **argv)
{
    std::ifstream fin("Information.txt", std::ios::in);
    char line[1024]={0};
    int i=0;
    std::vector<std::string> x;
    while(fin.getline(line, sizeof(line)))
    {
        std::string word(line);
        x.push_back(word);
        i++;
    //    std::cout << x[i++] << std::endl;
    }

    fin.clear();
    fin.close();
    //std::cout << x[i-1] << std::endl;//the last line
//save as vector x

    vectTemp vectStr;
    mapTemp  mapVect;
    MapM     mapMap;

    string x1,x2;
//Traversal
    while(i--)
    {
        std::cout << x[i] << std::endl;
//remove
        std::string s (x[i]);
        std::regex e (":no\n");
        if(std::regex_search(s,e))
            continue;
//processing and save
        int a = s.find(":");
        int b = s.length();
    //    std::cout << a << " " << b << endl;
        x1 = s.substr(0,a);
        x2 = s.substr(a+1,b-a-1);
    //    std::cout << x1 << " " << x2 <<endl;
        int c = x2.length();
        int j = c;
        while(j)
        {
    //        std::cout << j << "---------" <<endl;
            for(int k=0;j<=c-k;k++)
                mapMap[x1][j].push_back(x2.substr(k,j));
            j--;
        }
    //    std::cout << mapMap[x1][5][0] << mapMap[x1][4][1] <<endl;
    }
//combination
    return 0;
}
