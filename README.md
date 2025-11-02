#include <bits/stdc++.h>
using namespace std;

string reviewCode(const string &code) {
    int lines = count(code.begin(), code.end(), '\n');
    int semi = count(code.begin(), code.end(), ';');
    int loops = (code.find("for") != string::npos || code.find("while") != string::npos);
    stringstream ss;

    ss << "📋 Code Review Report\n";
    ss << "-----------------------\n";
    ss << "📄 Số dòng: " << lines << "\n";
    ss << "🧩 Số dấu ';': " << semi << "\n";
    ss << (loops ? "✅ Có sử dụng vòng lặp.\n" : "⚠️ Không phát hiện vòng lặp.\n");
    ss << "\nGợi ý cải thiện:\n";

    if (code.find("using namespace std") == string::npos)
        ss << "- Thêm `using namespace std;` nếu bạn không dùng std::\n";
    if (code.find("int main") == string::npos)
        ss << "- Thiếu hàm main().\n";
    if (lines > 50)
        ss << "- Code hơi dài, chia nhỏ hàm.\n";

    ss << "\nĐánh giá: " << (lines < 20 ? "Ngắn gọn ✅" : "Có thể tối ưu ⚙️") << "\n";
    return ss.str();
}

int main() {
    cout << "=== Code Reviewer Bot 🤖 ===\n";
    cout << "Nhập code của bạn (kết thúc bằng dòng trống):\n";
    string line, input;
    while (getline(cin, line) && !line.empty()) input += line + '\n';
    cout << "\n\n" << reviewCode(input);
}
