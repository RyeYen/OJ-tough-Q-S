#include <iostream>
#include <string>
#include <vector>
#include <sstream>
#include <cctype>

using namespace std;

// 全局变量，用于存储字符串数组。使用大小为21的数组以支持1-20的索引。
string s[21];

// 声明 process 函数，因为 main 和 process 会相互调用
string process(stringstream& ss);

// 检查字符串是否为0到99999之间的有效数字
bool isValidNumber(const string& str) {
    if (str.empty() || str.length() > 5) {
        return false;
    }
    for (char const &c : str) {
        if (!isdigit(c)) {
            return false;
        }
    }
    return true;
}

// 处理表达式，可以递归地解析嵌套命令并返回值
string process(stringstream& ss) {
    string command;
    ss >> command;

    if (command == "copy") {
        int n = stoi(process(ss));
        int x = stoi(process(ss));
        int l = stoi(process(ss));
        return s[n].substr(x, l);
    } 
    
    if (command == "add") {
        string s1 = process(ss);
        string s2 = process(ss);
        if (isValidNumber(s1) && isValidNumber(s2)) {
            return to_string(stoi(s1) + stoi(s2));
        }
        return s1 + s2;
    } 
    
    if (command == "find") {
        string search_str = process(ss);
        int n = stoi(process(ss));
        size_t pos = s[n].find(search_str);
        if (pos == string::npos) {
            return to_string(s[n].length());
        }
        return to_string(pos);
    } 
    
    if (command == "rfind") {
        string search_str = process(ss);
        int n = stoi(process(ss));
        size_t pos = s[n].rfind(search_str);
        if (pos == string::npos) {
            return to_string(s[n].length());
        }
        return to_string(pos);
    }
    
    // 如果不是已知命令，则它是一个字面值（数值或字符串）
    return command;
}

int main() {
    // 关闭C++标准流与C标准流的同步，提高IO效率
    ios_base::sync_with_stdio(false);
    cin.tie(NULL);

    int n;
    cin >> n;

    // 读取初始的n个字符串
    // s[0]未使用，使数组索引与题目中的N（1-based）保持一致
    for (int i = 1; i <= n; ++i) {
        cin >> s[i];
    }

    string line;
    // 忽略之前cin留下的换行符，以便getline能正确读取第一行命令
    cin.ignore(); 

    // 循环读取并处理每一行命令
    while (getline(cin, line)) {
        if (line == "over") {
            break;
        }

        stringstream ss(line);
        string command;
        ss >> command;

        if (command == "insert") {
            string str_to_insert = process(ss);
            int N = stoi(process(ss));
            int X = stoi(process(ss));
            s[N].insert(X, str_to_insert);
        } else if (command == "reset") {
            string new_str = process(ss);
            int N = stoi(process(ss));
            s[N] = new_str;
        } else if (command == "print") {
            int N = stoi(process(ss));
            cout << s[N] << endl;
        } else if (command == "printall") {
            for (int i = 1; i <= n; ++i) {
                cout << s[i] << endl;
            }
        }
    }

    return 0;
}
